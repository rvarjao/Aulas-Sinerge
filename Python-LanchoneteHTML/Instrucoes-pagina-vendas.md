# Aula 2: Sistema da Lanchonete — Criando Vendas

## 1. Tema da aula

Nesta aula, vamos continuar o sistema da lanchonete.

Na aula anterior, já tínhamos:

```text
CRUD de produtos
CRUD de clientes
páginas HTML
conexão com banco de dados
templates com Flask
```

Agora vamos criar a parte de **vendas**.

A página inicial do sistema será usada para:

```text
iniciar uma nova venda
listar as vendas já realizadas
visualizar uma venda
cancelar uma venda
```

---

## 2. Tabelas usadas nesta aula

As tabelas já existem no banco de dados.

Vamos usar:

```text
clientes
- id
- nome

produtos
- id
- nome
- valor_sugerido

vendas
- id
- cliente_id
- data_hora

vendas_produtos
- id
- produto_id
- venda_id
- preco
- quantidade
```

A tabela `vendas` guarda os dados principais da venda.

A tabela `vendas_produtos` guarda os produtos incluídos em cada venda.

---

## 3. Objetivos da aula

Ao final da aula, você deverá ser capaz de:

```text
listar vendas realizadas
iniciar uma nova venda para um cliente
adicionar produto a uma venda
visualizar os produtos de uma venda
calcular o valor total da venda
cancelar uma venda sem apagar do banco
entender relacionamento entre tabelas
```

---

# Parte 1: Conceito importante

## 4. Por que venda não deve ser excluída?

Em sistemas reais, uma venda representa uma operação que aconteceu.

Por isso, normalmente não apagamos uma venda diretamente do banco de dados.

Em vez de excluir, usamos o conceito de **cancelar venda**.

Excluir uma venda pode causar problemas como:

```text
perder histórico financeiro
alterar relatórios antigos
dificultar conferência
apagar registros importantes
prejudicar o controle do caixa
```

Por isso, vamos cancelar a venda marcando-a como cancelada.

---

## 5. Ajuste recomendado na tabela vendas

A tabela `vendas` atual possui:

```text
id
cliente_id
data_hora
```

Para permitir cancelamento, vamos adicionar duas colunas:

```sql
ALTER TABLE vendas
ADD COLUMN IF NOT EXISTS cancelada BOOLEAN DEFAULT FALSE;

ALTER TABLE vendas
ADD COLUMN IF NOT EXISTS cancelada_em TIMESTAMP;
```

Assim, a venda não será apagada.

Ela ficará marcada como cancelada.

---

# Parte 2: Como será a página inicial

## 6. Estrutura da página inicial

A página inicial terá este formato:

```text
Nova venda

[select com clientes] [Criar nova venda]


Vendas realizadas

-------------------------------------------------------------
ID | Cliente | Quantidade de produtos | Valor | Status | Ações
-------------------------------------------------------------
1  | Ana     | 3                      | 25.50 | Ativa  | Visualizar | Cancelar
2  | Bruno   | 1                      | 8.00  | Ativa  | Visualizar | Cancelar
```

A página inicial não será um dashboard completo ainda.

Ela terá apenas:

```text
formulário para iniciar venda
tabela com resumo das vendas realizadas
```

---

## 7. Fluxo da nova venda

O fluxo será:

```text
1. O usuário acessa a página inicial.
2. Escolhe um cliente no select.
3. Clica em Criar nova venda.
4. O sistema abre a página da nova venda com o nome do cliente.
5. A venda ainda não existe no banco.
6. O usuário escolhe um produto e informa a quantidade.
7. Ao adicionar o primeiro produto, o sistema cria a venda.
8. O sistema adiciona o produto à venda.
9. A venda passa a ter um ID.
10. O sistema abre a tela de visualização da venda.
```

Importante:

```text
A venda só será criada no banco quando tiver pelo menos um produto.
```

Isso evita criar vendas vazias.

---

# Parte 3: Atualizando a página inicial

## 8. Alterando a rota `/`

No arquivo `app.py`, substitua a rota `/` por esta:

```python
@app.route("/")
def index():
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("SELECT id, nome FROM clientes ORDER BY nome")
    clientes = cursor.fetchall()

    cursor.execute("""
        SELECT
            vendas.id,
            clientes.nome,
            COALESCE(SUM(vendas_produtos.quantidade), 0) AS quantidade_produtos,
            COALESCE(SUM(vendas_produtos.preco * vendas_produtos.quantidade), 0) AS valor_total,
            vendas.cancelada
        FROM vendas
        INNER JOIN clientes ON clientes.id = vendas.cliente_id
        LEFT JOIN vendas_produtos ON vendas_produtos.venda_id = vendas.id
        GROUP BY vendas.id, clientes.nome, vendas.cancelada
        ORDER BY vendas.id DESC
    """)
    vendas = cursor.fetchall()

    cursor.close()
    conexao.close()

    return render_template(
        "index.html",
        clientes=clientes,
        vendas=vendas
    )
```

Essa rota faz duas consultas principais:

```text
busca os clientes para preencher o select
busca o resumo das vendas para montar a tabela
```

---

## 9. Entendendo a consulta de vendas

A consulta principal é esta:

```sql
SELECT
    vendas.id,
    clientes.nome,
    COALESCE(SUM(vendas_produtos.quantidade), 0) AS quantidade_produtos,
    COALESCE(SUM(vendas_produtos.preco * vendas_produtos.quantidade), 0) AS valor_total,
    vendas.cancelada
FROM vendas
INNER JOIN clientes ON clientes.id = vendas.cliente_id
LEFT JOIN vendas_produtos ON vendas_produtos.venda_id = vendas.id
GROUP BY vendas.id, clientes.nome, vendas.cancelada
ORDER BY vendas.id DESC
```

Ela busca:

```text
id da venda
nome do cliente
quantidade total de produtos vendidos
valor total da venda
status de cancelamento
```

O cálculo do valor da venda é feito com:

```sql
SUM(vendas_produtos.preco * vendas_produtos.quantidade)
```

Isso significa:

```text
preço vezes quantidade
somado para todos os produtos daquela venda
```

Usamos `COALESCE` para evitar valor vazio caso alguma venda não tenha produtos.

---

## 10. Atualizando o arquivo `index.html`

Substitua o conteúdo do arquivo `templates/index.html` por:

```html
{% extends "base.html" %}

{% block conteudo %}

<h2>Vendas</h2>

<h3>Nova venda</h3>

<form action="/vendas/nova" method="get">
    <select name="cliente_id" required>
        <option value="">Selecione um cliente</option>

        {% for cliente in clientes %}
            <option value="{{ cliente[0] }}">{{ cliente[1] }}</option>
        {% endfor %}
    </select>

    <button type="submit">Criar nova venda</button>
</form>

<h3>Vendas realizadas</h3>

<table>
    <thead>
        <tr>
            <th>ID</th>
            <th>Cliente</th>
            <th>Quantidade de produtos</th>
            <th>Valor da venda</th>
            <th>Status</th>
            <th>Ações</th>
        </tr>
    </thead>

    <tbody>
        {% for venda in vendas %}
        <tr>
            <td>{{ venda[0] }}</td>
            <td>{{ venda[1] }}</td>
            <td>{{ venda[2] }}</td>
            <td>R$ {{ venda[3] }}</td>
            <td>
                {% if venda[4] %}
                    Cancelada
                {% else %}
                    Ativa
                {% endif %}
            </td>
            <td>
                <div class="acoes">
                    <a class="botao-link" href="/vendas/{{ venda[0] }}">Visualizar</a>

                    {% if not venda[4] %}
                    <form action="/vendas/{{ venda[0] }}/cancelar" method="post" style="margin: 0;">
                        <button class="botao-excluir" type="submit">Cancelar venda</button>
                    </form>
                    {% endif %}
                </div>
            </td>
        </tr>
        {% endfor %}
    </tbody>
</table>

{% endblock %}
```

---

# Parte 4: Página de nova venda

## 11. A venda ainda não terá ID

Quando o usuário selecionar um cliente e clicar em **Criar nova venda**, vamos abrir uma nova página.

Essa página mostrará:

```text
nome do cliente
select com produtos
campo de quantidade
botão para adicionar produto
```

Mas a venda ainda não será criada no banco.

A venda só será criada depois que o primeiro produto for adicionado.

---

## 12. Criando a rota `/vendas/nova`

No arquivo `app.py`, adicione:

```python
@app.route("/vendas/nova")
def nova_venda():
    cliente_id = request.args.get("cliente_id")

    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute(
        "SELECT id, nome FROM clientes WHERE id = %s",
        (cliente_id,)
    )
    cliente = cursor.fetchone()

    cursor.execute(
        "SELECT id, nome, valor_sugerido FROM produtos ORDER BY nome"
    )
    produtos = cursor.fetchall()

    cursor.close()
    conexao.close()

    return render_template(
        "nova_venda.html",
        cliente=cliente,
        produtos=produtos
    )
```

Aqui usamos:

```python
request.args.get("cliente_id")
```

Porque o formulário da página inicial usa `method="get"`.

---

## 13. Criando o arquivo `nova_venda.html`

Dentro da pasta `templates`, crie o arquivo:

```text
nova_venda.html
```

Conteúdo:

```html
{% extends "base.html" %}

{% block conteudo %}

<h2>Nova venda</h2>

<p><strong>Cliente:</strong> {{ cliente[1] }}</p>

<p>
    A venda ainda não foi criada no banco.
    Ela será criada somente quando o primeiro produto for adicionado.
</p>

<h3>Adicionar produto</h3>

<form action="/vendas/adicionar-produto" method="post">
    <input type="hidden" name="cliente_id" value="{{ cliente[0] }}">

    <select name="produto_id" required>
        <option value="">Selecione um produto</option>

        {% for produto in produtos %}
            <option value="{{ produto[0] }}">
                {{ produto[1] }} - R$ {{ produto[2] }}
            </option>
        {% endfor %}
    </select>

    <input type="number" name="quantidade" placeholder="Quantidade" min="1" required>

    <button type="submit">Adicionar produto</button>
</form>

<a href="/">Voltar</a>

{% endblock %}
```

---

# Parte 5: Criando a venda ao adicionar produto

## 14. Lógica da criação da venda

Quando o usuário adicionar o primeiro produto, o sistema deverá:

```text
1. Receber cliente_id, produto_id e quantidade.
2. Buscar o valor_sugerido do produto.
3. Criar a venda na tabela vendas.
4. Pegar o id da venda criada.
5. Inserir o produto na tabela vendas_produtos.
6. Redirecionar para a visualização da venda.
```

---

## 15. Criando a rota `/vendas/adicionar-produto`

No arquivo `app.py`, adicione:

```python
@app.route("/vendas/adicionar-produto", methods=["POST"])
def adicionar_produto_nova_venda():
    cliente_id = request.form["cliente_id"]
    produto_id = request.form["produto_id"]
    quantidade = request.form["quantidade"]

    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute(
        "SELECT valor_sugerido FROM produtos WHERE id = %s",
        (produto_id,)
    )
    produto = cursor.fetchone()
    preco = produto[0]

    cursor.execute(
        "INSERT INTO vendas (cliente_id, data_hora) VALUES (%s, NOW()) RETURNING id",
        (cliente_id,)
    )
    venda_id = cursor.fetchone()[0]

    cursor.execute(
        """
        INSERT INTO vendas_produtos (venda_id, produto_id, preco, quantidade)
        VALUES (%s, %s, %s, %s)
        """,
        (venda_id, produto_id, preco, quantidade)
    )

    conexao.commit()

    cursor.close()
    conexao.close()

    return redirect(f"/vendas/{venda_id}")
```

A linha:

```python
RETURNING id
```

serve para recuperar o ID da venda que acabou de ser criada.

---

# Parte 6: Visualizando uma venda

## 16. Criando a rota de visualização

No arquivo `app.py`, adicione:

```python
@app.route("/vendas/<int:venda_id>")
def visualizar_venda(venda_id):
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("""
        SELECT
            vendas.id,
            clientes.nome,
            vendas.data_hora,
            vendas.cancelada
        FROM vendas
        INNER JOIN clientes ON clientes.id = vendas.cliente_id
        WHERE vendas.id = %s
    """, (venda_id,))
    venda = cursor.fetchone()

    cursor.execute("""
        SELECT
            produtos.nome,
            vendas_produtos.quantidade,
            vendas_produtos.preco,
            vendas_produtos.quantidade * vendas_produtos.preco AS subtotal
        FROM vendas_produtos
        INNER JOIN produtos ON produtos.id = vendas_produtos.produto_id
        WHERE vendas_produtos.venda_id = %s
        ORDER BY vendas_produtos.id
    """, (venda_id,))
    itens = cursor.fetchall()

    cursor.execute("""
        SELECT
            COALESCE(SUM(quantidade * preco), 0)
        FROM vendas_produtos
        WHERE venda_id = %s
    """, (venda_id,))
    total = cursor.fetchone()[0]

    cursor.close()
    conexao.close()

    return render_template(
        "visualizar_venda.html",
        venda=venda,
        itens=itens,
        total=total
    )
```

---

## 17. Criando o arquivo `visualizar_venda.html`

Dentro da pasta `templates`, crie:

```text
visualizar_venda.html
```

Conteúdo:

```html
{% extends "base.html" %}

{% block conteudo %}

<h2>Venda #{{ venda[0] }}</h2>

<p><strong>Cliente:</strong> {{ venda[1] }}</p>
<p><strong>Data/hora:</strong> {{ venda[2] }}</p>

<p>
    <strong>Status:</strong>
    {% if venda[3] %}
        Cancelada
    {% else %}
        Ativa
    {% endif %}
</p>

<h3>Produtos da venda</h3>

<table>
    <thead>
        <tr>
            <th>Produto</th>
            <th>Quantidade</th>
            <th>Preço</th>
            <th>Subtotal</th>
        </tr>
    </thead>

    <tbody>
        {% for item in itens %}
        <tr>
            <td>{{ item[0] }}</td>
            <td>{{ item[1] }}</td>
            <td>R$ {{ item[2] }}</td>
            <td>R$ {{ item[3] }}</td>
        </tr>
        {% endfor %}
    </tbody>
</table>

<h3>Total: R$ {{ total }}</h3>

<a href="/">Voltar</a>

{% endblock %}
```

---

# Parte 7: Cancelando venda

## 18. Cancelar não é excluir

Agora vamos criar a ação de cancelar venda.

O sistema não vai apagar a venda.

Ele apenas vai alterar o campo `cancelada` para `TRUE`.

---

## 19. Criando a rota de cancelamento

No arquivo `app.py`, adicione:

```python
@app.route("/vendas/<int:venda_id>/cancelar", methods=["POST"])
def cancelar_venda(venda_id):
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute(
        """
        UPDATE vendas
        SET cancelada = TRUE,
            cancelada_em = NOW()
        WHERE id = %s
        """,
        (venda_id,)
    )

    conexao.commit()

    cursor.close()
    conexao.close()

    return redirect("/")
```

Depois disso, a venda continuará aparecendo na tabela, mas com o status:

```text
Cancelada
```

---

# Parte 8: Código completo das novas rotas

## 20. Rotas de vendas no `app.py`

Adicione estas rotas ao arquivo `app.py`.

```python
@app.route("/")
def index():
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("SELECT id, nome FROM clientes ORDER BY nome")
    clientes = cursor.fetchall()

    cursor.execute("""
        SELECT
            vendas.id,
            clientes.nome,
            COALESCE(SUM(vendas_produtos.quantidade), 0) AS quantidade_produtos,
            COALESCE(SUM(vendas_produtos.preco * vendas_produtos.quantidade), 0) AS valor_total,
            vendas.cancelada
        FROM vendas
        INNER JOIN clientes ON clientes.id = vendas.cliente_id
        LEFT JOIN vendas_produtos ON vendas_produtos.venda_id = vendas.id
        GROUP BY vendas.id, clientes.nome, vendas.cancelada
        ORDER BY vendas.id DESC
    """)
    vendas = cursor.fetchall()

    cursor.close()
    conexao.close()

    return render_template(
        "index.html",
        clientes=clientes,
        vendas=vendas
    )


@app.route("/vendas/nova")
def nova_venda():
    cliente_id = request.args.get("cliente_id")

    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute(
        "SELECT id, nome FROM clientes WHERE id = %s",
        (cliente_id,)
    )
    cliente = cursor.fetchone()

    cursor.execute(
        "SELECT id, nome, valor_sugerido FROM produtos ORDER BY nome"
    )
    produtos = cursor.fetchall()

    cursor.close()
    conexao.close()

    return render_template(
        "nova_venda.html",
        cliente=cliente,
        produtos=produtos
    )


@app.route("/vendas/adicionar-produto", methods=["POST"])
def adicionar_produto_nova_venda():
    cliente_id = request.form["cliente_id"]
    produto_id = request.form["produto_id"]
    quantidade = request.form["quantidade"]

    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute(
        "SELECT valor_sugerido FROM produtos WHERE id = %s",
        (produto_id,)
    )
    produto = cursor.fetchone()
    preco = produto[0]

    cursor.execute(
        "INSERT INTO vendas (cliente_id, data_hora) VALUES (%s, NOW()) RETURNING id",
        (cliente_id,)
    )
    venda_id = cursor.fetchone()[0]

    cursor.execute(
        """
        INSERT INTO vendas_produtos (venda_id, produto_id, preco, quantidade)
        VALUES (%s, %s, %s, %s)
        """,
        (venda_id, produto_id, preco, quantidade)
    )

    conexao.commit()

    cursor.close()
    conexao.close()

    return redirect(f"/vendas/{venda_id}")


@app.route("/vendas/<int:venda_id>")
def visualizar_venda(venda_id):
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("""
        SELECT
            vendas.id,
            clientes.nome,
            vendas.data_hora,
            vendas.cancelada
        FROM vendas
        INNER JOIN clientes ON clientes.id = vendas.cliente_id
        WHERE vendas.id = %s
    """, (venda_id,))
    venda = cursor.fetchone()

    cursor.execute("""
        SELECT
            produtos.nome,
            vendas_produtos.quantidade,
            vendas_produtos.preco,
            vendas_produtos.quantidade * vendas_produtos.preco AS subtotal
        FROM vendas_produtos
        INNER JOIN produtos ON produtos.id = vendas_produtos.produto_id
        WHERE vendas_produtos.venda_id = %s
        ORDER BY vendas_produtos.id
    """, (venda_id,))
    itens = cursor.fetchall()

    cursor.execute("""
        SELECT
            COALESCE(SUM(quantidade * preco), 0)
        FROM vendas_produtos
        WHERE venda_id = %s
    """, (venda_id,))
    total = cursor.fetchone()[0]

    cursor.close()
    conexao.close()

    return render_template(
        "visualizar_venda.html",
        venda=venda,
        itens=itens,
        total=total
    )


@app.route("/vendas/<int:venda_id>/cancelar", methods=["POST"])
def cancelar_venda(venda_id):
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute(
        """
        UPDATE vendas
        SET cancelada = TRUE,
            cancelada_em = NOW()
        WHERE id = %s
        """,
        (venda_id,)
    )

    conexao.commit()

    cursor.close()
    conexao.close()

    return redirect("/")
```

---

# Parte 9: Atividade dos alunos

## 21. Testando o fluxo

Cada aluno deverá testar:

```text
1. Cadastrar pelo menos 3 clientes.
2. Cadastrar pelo menos 5 produtos.
3. Voltar para a página inicial.
4. Escolher um cliente.
5. Clicar em Criar nova venda.
6. Verificar se aparece o nome do cliente.
7. Escolher um produto.
8. Informar a quantidade.
9. Adicionar o produto.
10. Verificar que a venda ganhou um ID.
11. Voltar para a página inicial.
12. Verificar se a venda apareceu na tabela.
13. Clicar em Visualizar.
14. Conferir os dados da venda.
15. Cancelar a venda.
16. Verificar que ela não foi apagada.
```

---

## 22. Perguntas para reflexão

Responda:

```text
1. Por que uma venda não deve ser excluída?
2. Qual é a diferença entre cancelar e excluir?
3. Por que a venda só é criada depois de adicionar o primeiro produto?
4. Para que serve a tabela vendas?
5. Para que serve a tabela vendas_produtos?
6. Como o sistema calcula o valor total da venda?
7. O que significa RETURNING id?
8. Por que usamos SUM()?
9. Por que usamos COALESCE()?
10. Como poderíamos permitir adicionar mais produtos em uma venda já criada?
```

---

# Conclusão

Nesta aula, criamos uma primeira versão do módulo de vendas.

A página inicial agora possui:

```text
formulário para iniciar nova venda
select com clientes
tabela com vendas realizadas
botão para visualizar venda
botão para cancelar venda
```

Também aprendemos que:

```text
vendas devem ser canceladas, não excluídas
```

Isso preserva o histórico do sistema e deixa os dados mais confiáveis.

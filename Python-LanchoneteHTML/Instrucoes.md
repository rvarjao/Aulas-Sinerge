# Aula: Sistema da Lanchonete com Python Server, HTML e Banco de Dados

## 1. Tema da aula

Nesta aula, vamos juntar o servidor Python da lanchonete com páginas HTML.

Vamos criar uma aplicação web simples usando:

* Python;
* Flask;
* HTML com templates;
* Banco de dados já existente;
* Arquivo `.env` para configurar a conexão;
* CRUD completo de produtos;
* Estrutura inicial para CRUD de clientes.

O CRUD de produtos será feito completo durante a aula.

O CRUD de clientes ficará como desafio para os alunos.

---

## 2. Schema do banco de dados

As tabelas já estão criadas no banco.

Vamos usar o seguinte modelo:

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

Nesta aula, vamos trabalhar principalmente com:

```text
produtos
clientes
```

As tabelas de vendas serão usadas em uma próxima aula.

---

## 3. Objetivos da aula

Ao final da aula, você deverá ser capaz de:

* Criar um servidor web com Python e Flask.
* Criar rotas para páginas HTML.
* Conectar o Python ao banco de dados usando `.env`.
* Listar dados vindos do banco.
* Cadastrar produtos.
* Editar produtos.
* Excluir produtos.
* Criar páginas com formulário e tabela.
* Reaproveitar a lógica de produtos para implementar clientes.

---

## 4. Estrutura do projeto

Crie uma pasta chamada:

```text
sistema_lanchonete
```

Dentro dela, crie esta estrutura:

```text
sistema_lanchonete/
│
├── app.py
├── database.py
├── .env
├── requirements.txt
│
└── templates/
    ├── base.html
    ├── index.html
    ├── produtos.html
    ├── editar_produto.html
    ├── clientes.html
    └── editar_cliente.html
```

---

## 5. Instalando as bibliotecas

No terminal, dentro da pasta do projeto, execute:

```bash
pip install flask psycopg2-binary python-dotenv
```

Essas bibliotecas serão usadas para:

```text
flask          criar o servidor web
psycopg2       conectar ao banco PostgreSQL
python-dotenv  ler as configurações do arquivo .env
```

Depois, crie o arquivo `requirements.txt`:

```txt
flask
psycopg2-binary
python-dotenv
```

---

## 6. Criando o arquivo `.env`

Crie um arquivo chamado `.env` na raiz do projeto.

Exemplo:

```env
DB_HOST=localhost
DB_PORT=5432
DB_NAME=lanchonete
DB_USER=postgres
DB_PASSWORD=sua_senha
```

Caso esteja usando um banco remoto, como Aiven, preencha com os dados fornecidos pelo serviço.

Exemplo:

```env
DB_HOST=seu-host.aivencloud.com
DB_PORT=12345
DB_NAME=defaultdb
DB_USER=avnadmin
DB_PASSWORD=sua_senha
```

O arquivo `.env` serve para guardar informações sensíveis fora do código principal.

---

# Parte 1: Conexão com o banco de dados

## 7. Criando o arquivo `database.py`

Crie o arquivo `database.py`.

Ele será responsável por conectar o Python ao banco de dados.

```python
import os
import psycopg2
from dotenv import load_dotenv


load_dotenv()


def conectar():
    conexao = psycopg2.connect(
        host=os.getenv("DB_HOST"),
        port=os.getenv("DB_PORT"),
        database=os.getenv("DB_NAME"),
        user=os.getenv("DB_USER"),
        password=os.getenv("DB_PASSWORD")
    )

    return conexao
```

---

# Parte 2: Criando o servidor Python

## 8. Criando o arquivo `app.py`

Crie o arquivo `app.py`.

Comece com este código:

```python
from flask import Flask, render_template, request, redirect
from database import conectar


app = Flask(__name__)


@app.route("/")
def index():
    return render_template("index.html")


if __name__ == "__main__":
    app.run(debug=True)
```

Execute o servidor:

```bash
python app.py
```

Acesse no navegador:

```text
http://127.0.0.1:5000
```

---

# Parte 3: Criando o layout base

## 9. Criando o arquivo `base.html`

Dentro da pasta `templates`, crie o arquivo `base.html`.

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Sistema da Lanchonete</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 40px;
            background: #f5f5f5;
        }

        header {
            background: #333;
            color: white;
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 20px;
        }

        nav a {
            color: white;
            margin-right: 15px;
            text-decoration: none;
            font-weight: bold;
        }

        main {
            background: white;
            padding: 20px;
            border-radius: 8px;
        }

        form {
            margin-bottom: 20px;
            display: flex;
            gap: 10px;
            align-items: center;
        }

        input {
            padding: 8px;
            font-size: 14px;
        }

        button {
            padding: 8px 12px;
            cursor: pointer;
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        th {
            background: #eee;
        }

        th, td {
            border: 1px solid #ccc;
            padding: 8px;
            text-align: left;
        }

        .acoes {
            display: flex;
            gap: 8px;
        }

        .botao-link {
            padding: 6px 10px;
            background: #ddd;
            color: black;
            text-decoration: none;
            border-radius: 4px;
        }

        .botao-excluir {
            background: #d9534f;
            color: white;
            border: none;
            border-radius: 4px;
        }

        .aviso {
            background: #fff3cd;
            padding: 15px;
            border: 1px solid #ffeeba;
            border-radius: 6px;
        }
    </style>
</head>
<body>

    <header>
        <h1>Sistema da Lanchonete</h1>

        <nav>
            <a href="/">Início</a>
            <a href="/produtos">Produtos</a>
            <a href="/clientes">Clientes</a>
            <a href="#">Vendas</a>
        </nav>
    </header>

    <main>
        {% block conteudo %}
        {% endblock %}
    </main>

</body>
</html>
```


# Entendendo os templates HTML

## O que são templates?

No Flask, as páginas HTML ficam dentro da pasta:

```text
templates/
```

Essas páginas são chamadas de **templates**.

Um template é um arquivo HTML que pode receber informações vindas do Python.

Por exemplo, no Python podemos ter uma lista de produtos:

```python
produtos = [
    (1, "Coxinha", 6.50),
    (2, "Suco", 5.00),
    (3, "Pastel", 8.00)
]
```

E o HTML pode usar essa lista para montar uma tabela automaticamente.

---

## HTML comum x Template

Um HTML comum é fixo.

Exemplo:

```html
<h1>Produtos</h1>
<p>Coxinha</p>
<p>Suco</p>
```

Já um template pode receber dados do Python.

Exemplo:

```html
<h1>Produtos</h1>

{% for produto in produtos %}
    <p>{{ produto[1] }}</p>
{% endfor %}
```

Nesse caso, o Flask vai repetir o `<p>` para cada produto da lista.

---

# O que é `render_template()`?

No arquivo `app.py`, usamos:

```python
return render_template("produtos.html", produtos=produtos)
```

Isso significa:

```text
renderizar o arquivo produtos.html
e enviar para ele a variável produtos
```

A primeira parte indica qual página HTML será carregada:

```python
"produtos.html"
```

A segunda parte envia dados para o template:

```python
produtos=produtos
```

O primeiro `produtos` é o nome que será usado dentro do HTML.

O segundo `produtos` é a variável que veio do Python.

Exemplo:

```python
return render_template("produtos.html", produtos=produtos)
```

Dentro do HTML, podemos acessar essa lista assim:

```html
{% for produto in produtos %}
    {{ produto[1] }}
{% endfor %}
```

---

# O que significa `{% extends "base.html" %}`?

No nosso projeto, criamos um arquivo chamado:

```text
base.html
```

Ele é o layout principal do sistema.

Nele ficam partes que se repetem em todas as páginas, como:

```text
cabeçalho
menu
estilo CSS
estrutura principal
```

Em vez de repetir esse código em todas as páginas, usamos:

```html
{% extends "base.html" %}
```

Isso significa:

```text
esta página vai usar o base.html como modelo principal
```

Por exemplo, o arquivo `produtos.html` começa assim:

```html
{% extends "base.html" %}
```

Então ele aproveita o cabeçalho, o menu e o estilo que já estão no `base.html`.

---

# O que são `block` e `endblock`?

No arquivo `base.html`, existe esta parte:

```html
<main>
    {% block conteudo %}
    {% endblock %}
</main>
```

Esse trecho cria um espaço vazio chamado `conteudo`.

Cada página poderá preencher esse espaço com seu próprio conteúdo.

Por exemplo, no arquivo `produtos.html`:

```html
{% extends "base.html" %}

{% block conteudo %}

<h2>Produtos</h2>

<p>Aqui ficará a página de produtos.</p>

{% endblock %}
```

Isso significa:

```text
use o layout base.html
e coloque este conteúdo dentro do bloco chamado conteudo
```

O resultado final será como se o Flask montasse uma página assim:

```html
<header>
    menu do sistema
</header>

<main>
    <h2>Produtos</h2>
    <p>Aqui ficará a página de produtos.</p>
</main>
```

---

# O que significa `{{ }}`?

As chaves duplas servem para mostrar valores vindos do Python dentro do HTML.

Exemplo no Python:

```python
nome = "Coxinha"
return render_template("exemplo.html", nome=nome)
```

No HTML:

```html
<p>{{ nome }}</p>
```

Resultado no navegador:

```html
<p>Coxinha</p>
```

No nosso sistema, usamos:

```html
{{ produto[0] }}
{{ produto[1] }}
{{ produto[2] }}
```

Considerando que cada produto vem do banco assim:

```python
(1, "Coxinha", 6.50)
```

Temos:

```text
produto[0] = id
produto[1] = nome
produto[2] = valor_sugerido
```

Por isso, no HTML:

```html
<td>{{ produto[0] }}</td>
<td>{{ produto[1] }}</td>
<td>R$ {{ produto[2] }}</td>
```

Será exibido:

```text
1 | Coxinha | R$ 6.50
```

---

# O que significa `{% for produto in produtos %}`?

Esse comando cria uma repetição dentro do HTML.

Ele funciona parecido com o `for` do Python.

No Python, poderíamos escrever:

```python
for produto in produtos:
    print(produto)
```

No template HTML, escrevemos:

```html
{% for produto in produtos %}
    <tr>
        <td>{{ produto[0] }}</td>
        <td>{{ produto[1] }}</td>
        <td>{{ produto[2] }}</td>
    </tr>
{% endfor %}
```

Isso significa:

```text
para cada produto dentro da lista de produtos,
crie uma linha na tabela
```

Se a lista tiver 3 produtos, o Flask criará 3 linhas na tabela.

---

## Exemplo completo do `for`

Imagine que o Python enviou esta lista:

```python
produtos = [
    (1, "Coxinha", 6.50),
    (2, "Suco", 5.00),
    (3, "Pastel", 8.00)
]
```

E o HTML tem este código:

```html
<table>
    <tbody>
        {% for produto in produtos %}
        <tr>
            <td>{{ produto[0] }}</td>
            <td>{{ produto[1] }}</td>
            <td>R$ {{ produto[2] }}</td>
        </tr>
        {% endfor %}
    </tbody>
</table>
```

O navegador receberá algo parecido com isto:

```html
<table>
    <tbody>
        <tr>
            <td>1</td>
            <td>Coxinha</td>
            <td>R$ 6.50</td>
        </tr>

        <tr>
            <td>2</td>
            <td>Suco</td>
            <td>R$ 5.00</td>
        </tr>

        <tr>
            <td>3</td>
            <td>Pastel</td>
            <td>R$ 8.00</td>
        </tr>
    </tbody>
</table>
```

Ou seja, o template gera o HTML final automaticamente.

---

# O que significa `{% endfor %}`?

Todo `for` precisa ser fechado com:

```html
{% endfor %}
```

Ele indica onde termina a repetição.

Exemplo:

```html
{% for produto in produtos %}
    <p>{{ produto[1] }}</p>
{% endfor %}
```

Se esquecer o `endfor`, o Flask não saberá onde a repetição termina e o programa apresentará erro.

---

# O que significa `{% if cliente %}`?

Também podemos usar condição dentro do template.

Exemplo:

```html
{% if cliente %}
    <p>Cliente encontrado.</p>
{% else %}
    <p>Cliente não encontrado.</p>
{% endif %}
```

Isso funciona parecido com o `if` do Python.

No nosso arquivo `editar_cliente.html`, usamos:

```html
{% if cliente %}

<form action="/clientes/{{ cliente[0] }}/atualizar" method="post">
    <input type="text" name="nome" value="{{ cliente[1] }}" required>
    <button type="submit">Salvar alterações</button>
</form>

{% else %}

<p>Cliente não encontrado ou função ainda não implementada.</p>

{% endif %}
```

Isso significa:

```text
se existir um cliente, mostre o formulário de edição
senão, mostre uma mensagem de aviso
```

---

# Resumo dos comandos de template

| Comando                     | Para que serve                                   |
| --------------------------- | ------------------------------------------------ |
| `{% extends "base.html" %}` | Usa o arquivo `base.html` como modelo            |
| `{% block conteudo %}`      | Inicia uma área que será preenchida pela página  |
| `{% endblock %}`            | Fecha o bloco de conteúdo                        |
| `{{ variavel }}`            | Mostra um valor vindo do Python                  |
| `{% for item in lista %}`   | Repete um trecho do HTML para cada item da lista |
| `{% endfor %}`              | Fecha o laço de repetição                        |
| `{% if condicao %}`         | Cria uma condição                                |
| `{% else %}`                | Define o que acontece se a condição for falsa    |
| `{% endif %}`               | Fecha a condição                                 |

---

# Fluxo completo

Quando acessamos a rota `/produtos`, acontece isto:

```text
1. O navegador pede a página /produtos
2. O Flask executa a função listar_produtos()
3. O Python consulta os produtos no banco de dados
4. O Python envia a lista para produtos.html
5. O produtos.html usa extends para aproveitar o base.html
6. O block conteudo preenche a área principal da página
7. O for percorre os produtos
8. O template monta uma tabela HTML
9. O navegador mostra a página pronta
```

Esse é o caminho:

```text
Banco de dados → Python → Template HTML → Navegador
```


---

## 10. Criando a página inicial `index.html`

Dentro da pasta `templates`, crie o arquivo `index.html`.

```html
{% extends "base.html" %}

{% block conteudo %}

<h2>Página inicial</h2>

<p>Bem-vindo ao sistema da lanchonete.</p>

<p>Use os links acima para acessar as áreas do sistema.</p>

<div class="aviso">
    <h3>Espaço reservado para Vendas</h3>
    <p>
        Em uma próxima aula, esta área será usada para registrar vendas,
        escolher clientes, escolher produtos e calcular o total da compra.
    </p>
</div>

{% endblock %}
```

---

# Parte 4: CRUD de Produtos

A tabela de produtos possui os campos:

```text
id
nome
valor_sugerido
```

A página de produtos terá este formato:

```text
[input para nome do produto] [input para valor sugerido] [botão para submeter]

[tabela com os produtos]
```

---

## 11. Criando a rota para listar produtos

No arquivo `app.py`, adicione esta rota antes do `if __name__ == "__main__":`.

```python
@app.route("/produtos")
def listar_produtos():
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("SELECT id, nome, valor_sugerido FROM produtos ORDER BY id")
    produtos = cursor.fetchall()

    cursor.close()
    conexao.close()

    return render_template("produtos.html", produtos=produtos)
```

Essa rota busca os produtos no banco e envia a lista para o template `produtos.html`.

---

## 12. Criando a página `produtos.html`

Dentro da pasta `templates`, crie o arquivo `produtos.html`.

```html
{% extends "base.html" %}

{% block conteudo %}

<h2>Produtos</h2>

<form action="/produtos/cadastrar" method="post">
    <input type="text" name="nome" placeholder="Nome do produto" required>
    <input type="number" name="valor_sugerido" placeholder="Valor sugerido" step="0.01" required>
    <button type="submit">Cadastrar produto</button>
</form>

<table>
    <thead>
        <tr>
            <th>ID</th>
            <th>Produto</th>
            <th>Valor sugerido</th>
            <th>Ações</th>
        </tr>
    </thead>

    <tbody>
        {% for produto in produtos %}
        <tr>
            <td>{{ produto[0] }}</td>
            <td>{{ produto[1] }}</td>
            <td>R$ {{ produto[2] }}</td>
            <td>
                <div class="acoes">
                    <a class="botao-link" href="/produtos/{{ produto[0] }}/editar">Editar</a>

                    <form action="/produtos/{{ produto[0] }}/excluir" method="post" style="margin: 0;">
                        <button class="botao-excluir" type="submit">Excluir</button>
                    </form>
                </div>
            </td>
        </tr>
        {% endfor %}
    </tbody>
</table>

{% endblock %}
```

Agora acesse:

```text
http://127.0.0.1:5000/produtos
```

---

## 13. Criando a rota para cadastrar produto

No arquivo `app.py`, adicione:

```python
@app.route("/produtos/cadastrar", methods=["POST"])
def cadastrar_produto():
    nome = request.form["nome"]
    valor_sugerido = request.form["valor_sugerido"]

    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute(
        "INSERT INTO produtos (nome, valor_sugerido) VALUES (%s, %s)",
        (nome, valor_sugerido)
    )

    conexao.commit()

    cursor.close()
    conexao.close()

    return redirect("/produtos")
```

Teste cadastrando alguns produtos:

```text
Coxinha - 6.50
Suco - 5.00
Pastel - 8.00
Refrigerante - 7.00
```

---

## 14. Criando a rota para abrir a tela de edição

No arquivo `app.py`, adicione:

```python
@app.route("/produtos/<int:id>/editar")
def editar_produto(id):
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute(
        "SELECT id, nome, valor_sugerido FROM produtos WHERE id = %s",
        (id,)
    )

    produto = cursor.fetchone()

    cursor.close()
    conexao.close()

    return render_template("editar_produto.html", produto=produto)
```

---

## 15. Criando a página `editar_produto.html`

Dentro da pasta `templates`, crie o arquivo `editar_produto.html`.

```html
{% extends "base.html" %}

{% block conteudo %}

<h2>Editar produto</h2>

<form action="/produtos/{{ produto[0] }}/atualizar" method="post">
    <input type="text" name="nome" value="{{ produto[1] }}" required>
    <input type="number" name="valor_sugerido" value="{{ produto[2] }}" step="0.01" required>
    <button type="submit">Salvar alterações</button>
</form>

<a href="/produtos">Voltar para produtos</a>

{% endblock %}
```

---

## 16. Criando a rota para atualizar produto

No arquivo `app.py`, adicione:

```python
@app.route("/produtos/<int:id>/atualizar", methods=["POST"])
def atualizar_produto(id):
    nome = request.form["nome"]
    valor_sugerido = request.form["valor_sugerido"]

    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute(
        "UPDATE produtos SET nome = %s, valor_sugerido = %s WHERE id = %s",
        (nome, valor_sugerido, id)
    )

    conexao.commit()

    cursor.close()
    conexao.close()

    return redirect("/produtos")
```

Teste:

```text
1. Cadastre um produto.
2. Clique em editar.
3. Altere o nome ou o valor sugerido.
4. Salve.
5. Veja se a tabela foi atualizada.
```

---

## 17. Criando a rota para excluir produto

No arquivo `app.py`, adicione:

```python
@app.route("/produtos/<int:id>/excluir", methods=["POST"])
def excluir_produto(id):
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute(
        "DELETE FROM produtos WHERE id = %s",
        (id,)
    )

    conexao.commit()

    cursor.close()
    conexao.close()

    return redirect("/produtos")
```

Teste:

```text
1. Cadastre um produto.
2. Clique em excluir.
3. Verifique se ele saiu da tabela.
```

---

# Parte 5: Código completo do `app.py`

Ao final, o arquivo `app.py` deverá ficar assim:

```python
from flask import Flask, render_template, request, redirect
from database import conectar


app = Flask(__name__)


@app.route("/")
def index():
    return render_template("index.html")


@app.route("/produtos")
def listar_produtos():
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("SELECT id, nome, valor_sugerido FROM produtos ORDER BY id")
    produtos = cursor.fetchall()

    cursor.close()
    conexao.close()

    return render_template("produtos.html", produtos=produtos)


@app.route("/produtos/cadastrar", methods=["POST"])
def cadastrar_produto():
    nome = request.form["nome"]
    valor_sugerido = request.form["valor_sugerido"]

    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute(
        "INSERT INTO produtos (nome, valor_sugerido) VALUES (%s, %s)",
        (nome, valor_sugerido)
    )

    conexao.commit()

    cursor.close()
    conexao.close()

    return redirect("/produtos")


@app.route("/produtos/<int:id>/editar")
def editar_produto(id):
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute(
        "SELECT id, nome, valor_sugerido FROM produtos WHERE id = %s",
        (id,)
    )

    produto = cursor.fetchone()

    cursor.close()
    conexao.close()

    return render_template("editar_produto.html", produto=produto)


@app.route("/produtos/<int:id>/atualizar", methods=["POST"])
def atualizar_produto(id):
    nome = request.form["nome"]
    valor_sugerido = request.form["valor_sugerido"]

    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute(
        "UPDATE produtos SET nome = %s, valor_sugerido = %s WHERE id = %s",
        (nome, valor_sugerido, id)
    )

    conexao.commit()

    cursor.close()
    conexao.close()

    return redirect("/produtos")


@app.route("/produtos/<int:id>/excluir", methods=["POST"])
def excluir_produto(id):
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute(
        "DELETE FROM produtos WHERE id = %s",
        (id,)
    )

    conexao.commit()

    cursor.close()
    conexao.close()

    return redirect("/produtos")


# ----------------------------------------------------
# ROTAS DE CLIENTES
# Estas rotas serão completadas pelos alunos.
# A tabela clientes possui:
# id
# nome
# ----------------------------------------------------

@app.route("/clientes")
def listar_clientes():
    # Buscar clientes no banco de dados
    # SELECT id, nome FROM clientes ORDER BY id
    # Enviar a lista para o template clientes.html
    return render_template("clientes.html", clientes=[])


@app.route("/clientes/cadastrar", methods=["POST"])
def cadastrar_cliente():
    # Receber o nome do formulário
    # Inserir o cliente no banco de dados
    # INSERT INTO clientes (nome) VALUES (%s)
    # Redirecionar para /clientes
    pass


@app.route("/clientes/<int:id>/editar")
def editar_cliente(id):
    # Buscar o cliente pelo ID
    # SELECT id, nome FROM clientes WHERE id = %s
    # Enviar o cliente para o template editar_cliente.html
    return render_template("editar_cliente.html", cliente=None)


@app.route("/clientes/<int:id>/atualizar", methods=["POST"])
def atualizar_cliente(id):
    # Receber o nome atualizado
    # Atualizar o cliente no banco de dados
    # UPDATE clientes SET nome = %s WHERE id = %s
    # Redirecionar para /clientes
    pass


@app.route("/clientes/<int:id>/excluir", methods=["POST"])
def excluir_cliente(id):
    # Excluir o cliente pelo ID
    # DELETE FROM clientes WHERE id = %s
    # Redirecionar para /clientes
    pass


if __name__ == "__main__":
    app.run(debug=True)
```

---

# Parte 6: Página de clientes

A tabela `clientes` possui somente:

```text
id
nome
```

O HTML já ficará pronto, mas as funções em Python serão completadas pelos alunos.

## 18. Criando o arquivo `clientes.html`

Dentro da pasta `templates`, crie o arquivo `clientes.html`.

```html
{% extends "base.html" %}

{% block conteudo %}

<h2>Clientes</h2>

<form action="/clientes/cadastrar" method="post">
    <input type="text" name="nome" placeholder="Nome do cliente" required>
    <button type="submit">Cadastrar cliente</button>
</form>

<table>
    <thead>
        <tr>
            <th>ID</th>
            <th>Cliente</th>
            <th>Ações</th>
        </tr>
    </thead>

    <tbody>
        {% for cliente in clientes %}
        <tr>
            <td>{{ cliente[0] }}</td>
            <td>{{ cliente[1] }}</td>
            <td>
                <div class="acoes">
                    <a class="botao-link" href="/clientes/{{ cliente[0] }}/editar">Editar</a>

                    <form action="/clientes/{{ cliente[0] }}/excluir" method="post" style="margin: 0;">
                        <button class="botao-excluir" type="submit">Excluir</button>
                    </form>
                </div>
            </td>
        </tr>
        {% endfor %}
    </tbody>
</table>

{% endblock %}
```

---

## 19. Criando o arquivo `editar_cliente.html`

Dentro da pasta `templates`, crie o arquivo `editar_cliente.html`.

```html
{% extends "base.html" %}

{% block conteudo %}

<h2>Editar cliente</h2>

{% if cliente %}

<form action="/clientes/{{ cliente[0] }}/atualizar" method="post">
    <input type="text" name="nome" value="{{ cliente[1] }}" required>
    <button type="submit">Salvar alterações</button>
</form>

{% else %}

<p>Cliente não encontrado ou função ainda não implementada.</p>

{% endif %}

<a href="/clientes">Voltar para clientes</a>

{% endblock %}
```

---

# Parte 7: Atividade dos alunos

## 20. Missão

Agora que o CRUD de produtos está funcionando, implemente o CRUD de clientes.

A tabela de clientes possui apenas dois campos:

```text
id
nome
```

Você deverá completar as funções:

```python
listar_clientes()
cadastrar_cliente()
editar_cliente(id)
atualizar_cliente(id)
excluir_cliente(id)
```

---

## 21. Dicas

Compare produtos e clientes.

Produtos usa:

```sql
SELECT id, nome, valor_sugerido FROM produtos ORDER BY id
```

Clientes deverá usar:

```sql
SELECT id, nome FROM clientes ORDER BY id
```

Produtos usa:

```sql
INSERT INTO produtos (nome, valor_sugerido) VALUES (%s, %s)
```

Clientes deverá usar:

```sql
INSERT INTO clientes (nome) VALUES (%s)
```

Produtos usa:

```sql
UPDATE produtos SET nome = %s, valor_sugerido = %s WHERE id = %s
```

Clientes deverá usar:

```sql
UPDATE clientes SET nome = %s WHERE id = %s
```

Produtos usa:

```sql
DELETE FROM produtos WHERE id = %s
```

Clientes deverá usar:

```sql
DELETE FROM clientes WHERE id = %s
```

---

## 22. Checklist da atividade

Marque quando concluir:

```text
[ ] A página /clientes abre corretamente
[ ] O formulário de cadastro de clientes aparece na tela
[ ] A tabela de clientes aparece na tela
[ ] O cliente é cadastrado no banco
[ ] O cliente aparece na tabela
[ ] O botão editar abre a tela de edição
[ ] O cliente é atualizado corretamente
[ ] O botão excluir remove o cliente
[ ] O sistema volta para /clientes após cadastrar, editar ou excluir
```

---

# Parte 8: Testes

## 23. Testando produtos

Cadastre estes produtos:

```text
Coxinha - 6.50
Pastel - 8.00
Suco - 5.00
Refrigerante - 7.00
```

Depois teste:

```text
Editar Coxinha para Coxinha de Frango
Alterar Suco de 5.00 para 6.00
Excluir Refrigerante
```

---

## 24. Testando clientes

Cadastre estes clientes:

```text
Ana
Bruno
Carlos
Daniela
```

Depois teste:

```text
Editar Ana para Ana Souza
Excluir Carlos
```

---

# Parte 9: Preparação para vendas

As tabelas de vendas já existem:

```text
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

Em uma próxima aula, poderemos usar essas tabelas para registrar uma venda.

A ideia será:

```text
1. Escolher um cliente
2. Criar uma venda
3. Escolher produtos
4. Informar quantidade
5. Salvar os produtos vendidos
6. Calcular o total
```

A tabela `vendas_produtos` permitirá guardar vários produtos dentro da mesma venda.

---

# Parte 10: Perguntas para reflexão

Responda no caderno ou em um arquivo de texto:

1. O que é uma rota?
2. Para que serve o arquivo `.env`?
3. Por que não colocamos a senha do banco diretamente no código?
4. Para que serve o arquivo `database.py`?
5. Qual é a função do `render_template()`?
6. Qual é a função do `redirect()`?
7. Qual é a diferença entre uma rota GET e uma rota POST?
8. O que acontece quando cadastramos um produto?
9. O que acontece quando excluímos um produto?
10. Por que o CRUD de clientes é parecido com o CRUD de produtos?
11. Como a tabela `vendas` se relaciona com `clientes`?
12. Como a tabela `vendas_produtos` se relaciona com `produtos`?

---

# Conclusão

Nesta aula, criamos uma aplicação web simples para a lanchonete.

Usamos:

```text
Python
Flask
HTML
Templates
Banco de dados
.env
CRUD
```

Implementamos o CRUD completo de produtos usando a tabela:

```text
produtos
- id
- nome
- valor_sugerido
```

E deixamos o CRUD de clientes como desafio, usando a tabela:

```text
clientes
- id
- nome
```

Esse projeto será a base para a próxima etapa: registrar vendas usando clientes e produtos.

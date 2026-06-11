# Aula — Introdução a Rotas e Templates com Python

## Tema da aula

Criação de páginas web usando **Python**, **Flask**, **rotas** e **templates HTML**.

Nesta aula, vamos criar páginas estáticas, mas elas não serão abertas diretamente pelo navegador como arquivos `.html`.

Agora, o navegador acessará uma **rota**, o Python receberá essa requisição e devolverá um **template HTML**.

---

# Objetivo da aula

Criar um pequeno site chamado:

## Portal Web da Lanchonete

O sistema terá algumas páginas iniciais:

* Página inicial
* Conteúdos estudados
* Produtos
* Cardápio
* Sobre o projeto

Cada página será acessada por uma rota em Python.

Exemplo:

```text
/               → página inicial
/conteudos      → página de conteúdos
/produtos       → página de produtos
/cardapio       → página de cardápio
/sobre          → página sobre o projeto
```

---

# O que você irá praticar

Nesta atividade, você irá praticar:

* criação de um projeto Python;
* instalação do Flask;
* criação de rotas;
* uso de templates HTML;
* organização de arquivos;
* navegação entre páginas;
* uso da função `render_template`;
* criação de páginas HTML estáticas dentro da pasta `templates`.

---

# Parte 1 — Criando a pasta do projeto

Crie uma pasta chamada:

```text
portal_lanchonete
```

Dentro dela, crie um arquivo chamado:

```text
app.py
```

Depois, crie uma pasta chamada:

```text
templates
```

A estrutura inicial deverá ficar assim:

```text
portal_lanchonete/
    app.py
    templates/
```

---

# Parte 2 — Instalando o Flask

No terminal, dentro da pasta do projeto, instale o Flask:

```bash
pip install flask
```

O Flask será usado para criar as rotas e exibir as páginas HTML.

---

# Parte 3 — Criando o primeiro arquivo Python

Abra o arquivo `app.py` e escreva o código inicial:

```python
from flask import Flask, render_template

app = Flask(__name__)


@app.route("/")
def inicio():
    return render_template("index.html")


if __name__ == "__main__":
    app.run(debug=True)
```

Explicação:

```python
from flask import Flask, render_template
```

Importa o Flask e a função que permite chamar arquivos HTML da pasta `templates`.

```python
app = Flask(__name__)
```

Cria a aplicação Flask.

```python
@app.route("/")
```

Define a rota principal do site.

```python
def inicio():
    return render_template("index.html")
```

Quando o usuário acessar `/`, o Python irá carregar o template `index.html`.

```python
app.run(debug=True)
```

Inicia o servidor em modo de desenvolvimento.

---

# Parte 4 — Criando o primeiro template

Dentro da pasta `templates`, crie o arquivo:

```text
index.html
```

A estrutura do projeto ficará assim:

```text
portal_lanchonete/
    app.py
    templates/
        index.html
```

Agora escreva o conteúdo abaixo no arquivo `index.html`:

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Portal Web da Lanchonete</title>
</head>
<body>

    <h1>Portal Web da Lanchonete</h1>

    <nav>
        <a href="/">Início</a> |
        <a href="/conteudos">Conteúdos</a> |
        <a href="/produtos">Produtos</a> |
        <a href="/cardapio">Cardápio</a> |
        <a href="/sobre">Sobre</a>
    </nav>

    <h2>Bem-vindo</h2>

    <p>
        Este é o portal inicial do sistema da lanchonete.
    </p>

    <p>
        Nesta etapa, estamos usando Python para exibir páginas HTML através de rotas.
    </p>

    <h2>Funcionalidades futuras</h2>

    <ul>
        <li>Cadastro de clientes</li>
        <li>Cadastro de produtos</li>
        <li>Registro de vendas</li>
        <li>Consulta de produtos</li>
        <li>Relatórios simples</li>
    </ul>

</body>
</html>
```

Observe que os links não apontam mais para arquivos como:

```text
produtos.html
```

Agora eles apontam para rotas:

```text
/produtos
```

---

# Parte 5 — Executando o projeto

No terminal, dentro da pasta do projeto, execute:

```bash
python app.py
```

O terminal deverá mostrar algo parecido com:

```text
Running on http://127.0.0.1:5000
```

Abra o navegador e acesse:

```text
http://127.0.0.1:5000
```

Você deverá ver a página inicial do Portal Web da Lanchonete.

---

# Parte 6 — Criando novas rotas

Agora vamos criar outras páginas no Python.

No arquivo `app.py`, adicione as rotas abaixo:

```python
from flask import Flask, render_template

app = Flask(__name__)


@app.route("/")
def inicio():
    return render_template("index.html")


@app.route("/conteudos")
def conteudos():
    return render_template("conteudos.html")


@app.route("/produtos")
def produtos():
    return render_template("produtos.html")


@app.route("/cardapio")
def cardapio():
    return render_template("cardapio.html")


@app.route("/sobre")
def sobre():
    return render_template("sobre.html")


if __name__ == "__main__":
    app.run(debug=True)
```

Cada rota chama um template diferente.

Exemplo:

```python
@app.route("/produtos")
def produtos():
    return render_template("produtos.html")
```

Isso significa:

```text
Quando o usuário acessar /produtos,
o Python irá mostrar o arquivo produtos.html
que está dentro da pasta templates.
```

---

# Parte 7 — Criando o template de conteúdos

Dentro da pasta `templates`, crie o arquivo:

```text
conteudos.html
```

Adicione o seguinte conteúdo:

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Conteúdos Estudados</title>
</head>
<body>

    <h1>Conteúdos Estudados</h1>

    <nav>
        <a href="/">Início</a> |
        <a href="/conteudos">Conteúdos</a> |
        <a href="/produtos">Produtos</a> |
        <a href="/cardapio">Cardápio</a> |
        <a href="/sobre">Sobre</a>
    </nav>

    <h2>Tabela de conteúdos</h2>

    <table border="1">
        <tr>
            <th>Aula</th>
            <th>Tema</th>
            <th>Descrição</th>
        </tr>
        <tr>
            <td>1</td>
            <td>Python básico</td>
            <td>Variáveis, entrada e saída de dados</td>
        </tr>
        <tr>
            <td>2</td>
            <td>Condicionais</td>
            <td>Uso de if, elif e else</td>
        </tr>
        <tr>
            <td>3</td>
            <td>Funções</td>
            <td>Organização do código em partes menores</td>
        </tr>
        <tr>
            <td>4</td>
            <td>Menus</td>
            <td>Criação de menus usando while</td>
        </tr>
        <tr>
            <td>5</td>
            <td>Rotas e templates</td>
            <td>Criação de páginas web com Python e Flask</td>
        </tr>
    </table>

</body>
</html>
```

Teste no navegador:

```text
http://127.0.0.1:5000/conteudos
```

---

# Parte 8 — Criando o template de produtos

Dentro da pasta `templates`, crie o arquivo:

```text
produtos.html
```

Adicione o seguinte conteúdo:

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Produtos</title>
</head>
<body>

    <h1>Produtos da Lanchonete</h1>

    <nav>
        <a href="/">Início</a> |
        <a href="/conteudos">Conteúdos</a> |
        <a href="/produtos">Produtos</a> |
        <a href="/cardapio">Cardápio</a> |
        <a href="/sobre">Sobre</a>
    </nav>

    <h2>Lista de produtos</h2>

    <table border="1">
        <tr>
            <th>Produto</th>
            <th>Categoria</th>
            <th>Preço</th>
        </tr>
        <tr>
            <td>Coxinha</td>
            <td>Salgado</td>
            <td>R$ 6,00</td>
        </tr>
        <tr>
            <td>Suco natural</td>
            <td>Bebida</td>
            <td>R$ 5,00</td>
        </tr>
        <tr>
            <td>Brigadeiro</td>
            <td>Doce</td>
            <td>R$ 3,00</td>
        </tr>
        <tr>
            <td>Pastel</td>
            <td>Salgado</td>
            <td>R$ 7,00</td>
        </tr>
    </table>

</body>
</html>
```

Teste no navegador:

```text
http://127.0.0.1:5000/produtos
```

---

# Parte 9 — Criando o template de cardápio

Dentro da pasta `templates`, crie o arquivo:

```text
cardapio.html
```

Adicione o seguinte conteúdo:

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Cardápio</title>
</head>
<body>

    <h1>Cardápio</h1>

    <nav>
        <a href="/">Início</a> |
        <a href="/conteudos">Conteúdos</a> |
        <a href="/produtos">Produtos</a> |
        <a href="/cardapio">Cardápio</a> |
        <a href="/sobre">Sobre</a>
    </nav>

    <h2>Produtos disponíveis</h2>

    <div>
        <h3>Coxinha</h3>
        <p>Categoria: Salgado</p>
        <p>Preço: R$ 6,00</p>
    </div>

    <div>
        <h3>Suco natural</h3>
        <p>Categoria: Bebida</p>
        <p>Preço: R$ 5,00</p>
    </div>

    <div>
        <h3>Brigadeiro</h3>
        <p>Categoria: Doce</p>
        <p>Preço: R$ 3,00</p>
    </div>

    <div>
        <h3>Pastel</h3>
        <p>Categoria: Salgado</p>
        <p>Preço: R$ 7,00</p>
    </div>

</body>
</html>
```

Teste no navegador:

```text
http://127.0.0.1:5000/cardapio
```

---

# Parte 10 — Criando o template sobre

Dentro da pasta `templates`, crie o arquivo:

```text
sobre.html
```

Adicione o seguinte conteúdo:

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Sobre o Projeto</title>
</head>
<body>

    <h1>Sobre o Projeto</h1>

    <nav>
        <a href="/">Início</a> |
        <a href="/conteudos">Conteúdos</a> |
        <a href="/produtos">Produtos</a> |
        <a href="/cardapio">Cardápio</a> |
        <a href="/sobre">Sobre</a>
    </nav>

    <h2>O que é este projeto?</h2>

    <p>
        Este projeto é uma primeira versão visual do sistema da lanchonete.
    </p>

    <p>
        Nesta etapa, estamos aprendendo como o Python pode exibir páginas HTML
        usando rotas e templates.
    </p>

    <h2>Próximas etapas</h2>

    <ol>
        <li>Enviar dados do Python para o HTML</li>
        <li>Usar listas de produtos no Python</li>
        <li>Mostrar produtos usando repetição no template</li>
        <li>Criar formulários</li>
        <li>Conectar o sistema ao banco de dados</li>
    </ol>

</body>
</html>
```

Teste no navegador:

```text
http://127.0.0.1:5000/sobre
```

---

# Parte 11 — Estrutura final do projeto

Ao final da aula, o projeto deverá estar assim:

```text
portal_lanchonete/
    app.py
    templates/
        index.html
        conteudos.html
        produtos.html
        cardapio.html
        sobre.html
```

O arquivo `app.py` deverá estar assim:

```python
from flask import Flask, render_template

app = Flask(__name__)


@app.route("/")
def inicio():
    return render_template("index.html")


@app.route("/conteudos")
def conteudos():
    return render_template("conteudos.html")


@app.route("/produtos")
def produtos():
    return render_template("produtos.html")


@app.route("/cardapio")
def cardapio():
    return render_template("cardapio.html")


@app.route("/sobre")
def sobre():
    return render_template("sobre.html")


if __name__ == "__main__":
    app.run(debug=True)
```

---

# Parte 12 — O que está acontecendo no sistema

Quando o usuário acessa:

```text
http://127.0.0.1:5000/produtos
```

O Flask procura no arquivo `app.py` uma rota correspondente:

```python
@app.route("/produtos")
def produtos():
    return render_template("produtos.html")
```

Essa rota chama o template:

```text
produtos.html
```

O template está dentro da pasta:

```text
templates/
```

Então o fluxo é:

```text
Navegador → rota → função Python → template HTML → página exibida
```

---

# Regras da atividade

1. O projeto deve usar Flask.
2. O arquivo principal deve se chamar `app.py`.
3. Os arquivos HTML devem ficar dentro da pasta `templates`.
4. Cada página deve ter uma rota própria.
5. Cada rota deve chamar um template usando `render_template`.
6. Os links do menu devem apontar para rotas, e não para arquivos `.html`.
7. O conteúdo dos templates pode ser estático nesta etapa.
8. Todas as páginas devem ter menu de navegação.
9. O projeto deve rodar usando `python app.py`.

---

# Atividade para entregar

Crie o projeto `portal_lanchonete` com as seguintes rotas:

```text
/               → página inicial
/conteudos      → conteúdos estudados
/produtos       → lista de produtos
/cardapio       → cardápio
/sobre          → sobre o projeto
```

Cada rota deve exibir um template HTML diferente.

Cada template deve ter:

* título principal;
* menu de navegação;
* conteúdo relacionado à página.

A página `conteudos.html` deve ter uma tabela com os conteúdos estudados.

A página `produtos.html` deve ter uma tabela de produtos.

A página `cardapio.html` deve mostrar produtos em blocos.

A página `sobre.html` deve explicar o objetivo do projeto.

---

# Desafio extra

Crie uma nova rota:

```text
/clientes
```

Essa rota deverá chamar o template:

```text
clientes.html
```

No arquivo `app.py`, adicione:

```python
@app.route("/clientes")
def clientes():
    return render_template("clientes.html")
```

Depois crie o arquivo `clientes.html` dentro da pasta `templates`.

A página deve ter uma tabela com clientes fictícios:

```html
<table border="1">
    <tr>
        <th>Nome</th>
        <th>Telefone</th>
        <th>Observação</th>
    </tr>
    <tr>
        <td>Ana</td>
        <td>99999-1111</td>
        <td>Gosta de suco natural</td>
    </tr>
    <tr>
        <td>Bruno</td>
        <td>99999-2222</td>
        <td>Prefere salgados</td>
    </tr>
</table>
```

Não esqueça de adicionar o link `/clientes` no menu das páginas.

---

# Perguntas para responder

1. Para que serve o Flask?
2. O que é uma rota?
3. Para que serve o `@app.route("/")`?
4. Para que serve a função `render_template()`?
5. Onde devem ficar os arquivos HTML no Flask?
6. Qual é a diferença entre acessar `produtos.html` e acessar `/produtos`?
7. O que acontece quando o usuário acessa a rota `/cardapio`?
8. Por que os links do menu usam `/produtos` em vez de `produtos.html`?

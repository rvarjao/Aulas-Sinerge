# Aula — Introdução a Páginas Web Estáticas

## Tema da aula

Criação de páginas HTML estáticas para preparar o desenvolvimento de um sistema web com Python.

Nas próximas aulas, essas páginas serão usadas como base para trabalhar com **rotas** e **templates** em Python.

---

# Objetivo da aula

Nesta aula, você irá criar um pequeno site estático chamado:

## Portal Web da Lanchonete

Esse site será uma primeira versão visual do sistema da lanchonete que será desenvolvido nas próximas aulas.

Por enquanto, não usaremos Python, banco de dados ou formulários funcionando.
O objetivo é entender como criar páginas HTML, menus de navegação e tabelas de conteúdo.

---

# O que você irá praticar

Nesta atividade, você irá praticar:

* criação de arquivos HTML;
* estrutura básica de uma página;
* uso de títulos;
* uso de parágrafos;
* criação de links;
* criação de listas;
* criação de tabelas;
* organização de arquivos em uma pasta;
* navegação entre páginas.

---

# Parte 1 — Criando a pasta do projeto

Crie uma pasta para o projeto com o nome:

```text
portal_lanchonete
```

Dentro dessa pasta, crie os seguintes arquivos:

```text
index.html
conteudos.html
produtos.html
cardapio.html
sobre.html
```

A estrutura da pasta deverá ficar assim:

```text
portal_lanchonete/
    index.html
    conteudos.html
    produtos.html
    cardapio.html
    sobre.html
```

---

# Parte 2 — Criando a estrutura básica do HTML

Abra o arquivo `index.html` e adicione a estrutura básica:

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Portal Web da Lanchonete</title>
</head>
<body>

</body>
</html>
```

Agora, dentro da tag `<body>`, adicione um título:

```html
<h1>Portal Web da Lanchonete</h1>
```

O arquivo ficará assim:

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Portal Web da Lanchonete</title>
</head>
<body>

    <h1>Portal Web da Lanchonete</h1>

</body>
</html>
```

---

# Parte 3 — Criando o menu de navegação

Ainda no arquivo `index.html`, abaixo do título, crie um menu com links para as páginas do projeto:

```html
<nav>
    <a href="index.html">Início</a> |
    <a href="conteudos.html">Conteúdos</a> |
    <a href="produtos.html">Produtos</a> |
    <a href="cardapio.html">Cardápio</a> |
    <a href="sobre.html">Sobre</a>
</nav>
```

Esse menu será usado em todas as páginas.

O arquivo `index.html` ficará assim:

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
        <a href="index.html">Início</a> |
        <a href="conteudos.html">Conteúdos</a> |
        <a href="produtos.html">Produtos</a> |
        <a href="cardapio.html">Cardápio</a> |
        <a href="sobre.html">Sobre</a>
    </nav>

</body>
</html>
```

---

# Parte 4 — Criando a página inicial

Na página `index.html`, abaixo do menu, adicione uma apresentação do projeto:

```html
<h2>Bem-vindo</h2>

<p>
    Este é o portal inicial do sistema da lanchonete.
    Nesta primeira etapa, estamos criando apenas páginas estáticas em HTML.
</p>

<p>
    Nas próximas aulas, essas páginas serão exibidas usando Python,
    rotas e templates.
</p>
```

Agora adicione uma lista com as futuras funcionalidades do sistema:

```html
<h2>Funcionalidades futuras</h2>

<ul>
    <li>Cadastro de clientes</li>
    <li>Cadastro de produtos</li>
    <li>Registro de vendas</li>
    <li>Consulta de produtos</li>
    <li>Relatórios simples</li>
</ul>
```

Código completo da página `index.html`:

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
        <a href="index.html">Início</a> |
        <a href="conteudos.html">Conteúdos</a> |
        <a href="produtos.html">Produtos</a> |
        <a href="cardapio.html">Cardápio</a> |
        <a href="sobre.html">Sobre</a>
    </nav>

    <h2>Bem-vindo</h2>

    <p>
        Este é o portal inicial do sistema da lanchonete.
        Nesta primeira etapa, estamos criando apenas páginas estáticas em HTML.
    </p>

    <p>
        Nas próximas aulas, essas páginas serão exibidas usando Python,
        rotas e templates.
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

---

# Parte 5 — Criando a página de conteúdos

Abra o arquivo `conteudos.html`.

Adicione a estrutura básica:

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
        <a href="index.html">Início</a> |
        <a href="conteudos.html">Conteúdos</a> |
        <a href="produtos.html">Produtos</a> |
        <a href="cardapio.html">Cardápio</a> |
        <a href="sobre.html">Sobre</a>
    </nav>

</body>
</html>
```

Agora, abaixo do menu, adicione uma tabela com os conteúdos estudados:

```html
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
        <td>HTML</td>
        <td>Criação de páginas web estáticas</td>
    </tr>
</table>
```

Código completo da página `conteudos.html`:

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
        <a href="index.html">Início</a> |
        <a href="conteudos.html">Conteúdos</a> |
        <a href="produtos.html">Produtos</a> |
        <a href="cardapio.html">Cardápio</a> |
        <a href="sobre.html">Sobre</a>
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
            <td>HTML</td>
            <td>Criação de páginas web estáticas</td>
        </tr>
    </table>

</body>
</html>
```

---

# Parte 6 — Criando a página de produtos

Abra o arquivo `produtos.html`.

Adicione a estrutura básica com menu:

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
        <a href="index.html">Início</a> |
        <a href="conteudos.html">Conteúdos</a> |
        <a href="produtos.html">Produtos</a> |
        <a href="cardapio.html">Cardápio</a> |
        <a href="sobre.html">Sobre</a>
    </nav>

</body>
</html>
```

Agora, abaixo do menu, crie uma tabela de produtos:

```html
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
```

Código completo da página `produtos.html`:

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
        <a href="index.html">Início</a> |
        <a href="conteudos.html">Conteúdos</a> |
        <a href="produtos.html">Produtos</a> |
        <a href="cardapio.html">Cardápio</a> |
        <a href="sobre.html">Sobre</a>
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

---

# Parte 7 — Criando a página de cardápio

Abra o arquivo `cardapio.html`.

Essa página terá uma visualização diferente dos produtos, usando blocos de informações em vez de tabela.

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
        <a href="index.html">Início</a> |
        <a href="conteudos.html">Conteúdos</a> |
        <a href="produtos.html">Produtos</a> |
        <a href="cardapio.html">Cardápio</a> |
        <a href="sobre.html">Sobre</a>
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

---

# Parte 8 — Criando a página sobre

Abra o arquivo `sobre.html`.

Essa página deverá explicar o objetivo do projeto.

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
        <a href="index.html">Início</a> |
        <a href="conteudos.html">Conteúdos</a> |
        <a href="produtos.html">Produtos</a> |
        <a href="cardapio.html">Cardápio</a> |
        <a href="sobre.html">Sobre</a>
    </nav>

    <h2>O que é este projeto?</h2>

    <p>
        Este projeto é uma primeira versão do sistema da lanchonete.
        Nesta etapa, estamos criando apenas páginas estáticas usando HTML.
    </p>

    <p>
        Futuramente, o sistema poderá cadastrar clientes, produtos e vendas.
        Também poderá buscar informações em um banco de dados.
    </p>

    <h2>Próximas etapas</h2>

    <ol>
        <li>Transformar as páginas em templates HTML</li>
        <li>Criar rotas usando Python</li>
        <li>Enviar dados do Python para o HTML</li>
        <li>Conectar o sistema ao banco de dados</li>
        <li>Criar formulários de cadastro</li>
    </ol>

</body>
</html>
```

---

# Parte 9 — Testando as páginas

Depois de criar os arquivos, abra o arquivo `index.html` no navegador.

Teste se os links do menu funcionam:

* clique em Conteúdos;
* clique em Produtos;
* clique em Cardápio;
* clique em Sobre;
* volte para Início.

Verifique se todas as páginas abrem corretamente.

---

# Parte 10 — Entendendo o que foi feito

Nesta aula, criamos várias páginas HTML separadas.

Cada página é um arquivo:

```text
index.html
conteudos.html
produtos.html
cardapio.html
sobre.html
```

O navegador abre diretamente esses arquivos.

Na próxima etapa, vamos mudar essa lógica.

Em vez de abrir diretamente o arquivo:

```text
produtos.html
```

O usuário acessará uma rota:

```text
/produtos
```

E o Python será responsável por mostrar a página correta.

Exemplo da próxima aula:

```python
@app.route("/produtos")
def produtos():
    return render_template("produtos.html")
```

Assim, o caminho será:

```text
Navegador → Rota → Python → Template HTML → Página exibida
```

---

# Atividade para entregar

Crie um site estático com as seguintes páginas:

1. `index.html`
2. `conteudos.html`
3. `produtos.html`
4. `cardapio.html`
5. `sobre.html`

Todas as páginas devem ter:

* título principal;
* menu de navegação;
* conteúdo relacionado ao tema da página.

A página `conteudos.html` deve ter uma tabela com os conteúdos estudados.

A página `produtos.html` deve ter uma tabela de produtos da lanchonete.

A página `cardapio.html` deve mostrar os produtos em blocos separados.

A página `sobre.html` deve explicar o objetivo do projeto.

---

# Desafio extra

Adicione uma nova página chamada:

```text
clientes.html
```

Essa página deverá ter uma tabela com clientes fictícios da lanchonete.

Exemplo:

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

Não esqueça de adicionar o link para `clientes.html` no menu de todas as páginas.

---

# Perguntas para responder no caderno

1. Para que serve uma página HTML?
2. Para que serve a tag `<a>`?
3. Qual é a diferença entre uma lista `<ul>` e uma lista `<ol>`?
4. Para que usamos uma tabela em HTML?
5. O que acontece quando clicamos em um link?
6. Qual será a diferença entre abrir um arquivo `produtos.html` e acessar uma rota `/produtos` em Python?

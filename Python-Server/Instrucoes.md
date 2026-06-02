# Aula — Sistema de Lanchonete com Python e Banco de Dados

## Índice
- [1. Contexto do sistema](#Aula-1---Contexto-do-sistema)
- [2. Cadastrando clientes e produtos com Python](#Aula-2---Cadastrando-Clientes-e-Produtos-com-Python)


## Aula 1 - Contexto do sistema

## Objetivo da aula

Nesta aula, vamos criar a primeira parte de um sistema de lanchonete usando Python e PostgreSQL.

O sistema será conectado a um banco de dados real na internet.

Ao final da aula, você deverá conseguir:

* criar um projeto em Python;
* instalar a biblioteca de conexão com PostgreSQL;
* configurar os dados do banco;
* testar a conexão;
* criar as tabelas do sistema da lanchonete.

---

# 1. Contexto do sistema

Vamos imaginar uma lanchonete que precisa registrar suas vendas.

A lanchonete possui:

* clientes;
* produtos;
* vendas;
* produtos vendidos em cada venda.

Exemplo:

```
Cliente: Ana

Venda:
- 2 coxinhas
- 1 refrigerante
```

Para organizar essas informações, vamos usar quatro tabelas:

```
clientes
produtos
vendas
vendas_produtos
```

---

# 2. Entendendo as tabelas

## Diagrama do banco

O diagrama do banco é o seguinte:

![Diagrama do banco](DB-Schema.png)



## Tabela clientes

A tabela `clientes` guarda as pessoas que compram na lanchonete.

Campos:

```
id
nome
```

Exemplo:

```
id | nome
1  | Ana
2  | Bruno
3  | Carlos
```

---

## Tabela produtos

A tabela `produtos` guarda os produtos vendidos pela lanchonete.

Campos:

```
id
nome
valor_sugerido
```

Exemplo:

```
id | nome          | valor_sugerido
1  | Coxinha       | 6.50
2  | Refrigerante  | 5.00
3  | Pastel        | 8.00
```

---

## Tabela vendas

A tabela `vendas` guarda o registro de que uma venda aconteceu.

Campos:

```
id
cliente_id
data_hora
```

Exemplo:

```
id | cliente_id | data_hora
1  | 1          | 2026-06-02 10:30:00
```

Importante:

```
cliente_id indica qual cliente fez a compra.
```

Ou seja, a venda não guarda diretamente o nome da pessoa.
Ela guarda o ID do cliente.

---

## Tabela vendas_produtos

A tabela `vendas_produtos` guarda os produtos que fazem parte de uma venda.

Campos:

```
id
produto_id
venda_id
preco
quantidade
```

Exemplo:

```
id | produto_id | venda_id | preco | quantidade
1  | 1          | 1        | 6.50  | 2
2  | 2          | 1        | 5.00  | 1
```

Explicação:

```
A tabela vendas diz que uma venda aconteceu.

A tabela vendas_produtos diz quais produtos foram comprados nessa venda.
```

---

# 3. Criando a pasta do projeto

Crie uma pasta chamada:

```
lanchonete-python
```

Dentro dessa pasta, crie dois arquivos:

```
config.py
main.py
```

A estrutura ficará assim:

```
lanchonete-python/
    config.py
    main.py
```

---

# 4. Instalando a biblioteca do PostgreSQL

Abra o terminal dentro da pasta do projeto e execute:

```
pip install psycopg[binary]
```

Essa biblioteca permite que o Python se conecte ao banco PostgreSQL.

---

# 5. Criando o arquivo config.py

Abra o arquivo `config.py` e coloque o seguinte código:

```
DB_CONFIG = {
    "host": "SEU_HOST_AQUI",
    "port": 12345,
    "dbname": "defaultdb",
    "user": "SEU_USUARIO_AQUI",
    "password": "SUA_SENHA_AQUI",
    "sslmode": "require"
}
```

O professor irá informar os dados corretos do banco.

Explicação dos campos:

```
host      -> endereço do servidor do banco
port      -> porta de conexão
dbname    -> nome do banco de dados
user      -> usuário do banco
password  -> senha do banco
sslmode   -> modo de conexão segura
```

---

# 6. Testando a conexão com o banco

Abra o arquivo `main.py` e coloque este código:

```
import psycopg
from config import DB_CONFIG


def conectar():
    conexao = psycopg.connect(**DB_CONFIG)
    return conexao


def testar_conexao():
    try:
        conexao = conectar()
        print("Conexão realizada com sucesso!")
        conexao.close()
    except Exception as erro:
        print("Erro ao conectar no banco:")
        print(erro)


testar_conexao()
```

Agora execute o programa no terminal:

```
python main.py
```

Resultado esperado:

```
Conexão realizada com sucesso!
```

Se aparecer erro, verifique:

* se a internet está funcionando;
* se o host está correto;
* se a porta está correta;
* se o usuário está correto;
* se a senha está correta;
* se o banco está ativo.

---

# 7. Criando a tabela clientes

Agora vamos criar a primeira tabela do sistema.

Substitua o conteúdo do arquivo `main.py` por este código:

```
import psycopg
from config import DB_CONFIG


def conectar():
    conexao = psycopg.connect(**DB_CONFIG)
    return conexao


def criar_tabela_clientes():
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("""
        CREATE TABLE IF NOT EXISTS clientes (
            id SERIAL PRIMARY KEY,
            nome VARCHAR(255) NOT NULL
        );
    """)

    conexao.commit()
    cursor.close()
    conexao.close()

    print("Tabela clientes criada com sucesso.")


criar_tabela_clientes()
```

Execute:

```
python main.py
```

Resultado esperado:

```
Tabela clientes criada com sucesso.
```

---

# 8. Explicando o código da tabela clientes

Este comando cria a tabela:

```
CREATE TABLE IF NOT EXISTS clientes
```

Significa:

```
Crie a tabela clientes se ela ainda não existir.
```

Este campo cria um código automático:

```
id SERIAL PRIMARY KEY
```

Significa:

```
Cada cliente terá um ID único.
```

Este campo cria o nome do cliente:

```
nome VARCHAR(255) NOT NULL
```

Significa:

```
O nome será um texto obrigatório.
```

---

# 9. Criando todas as tabelas

Agora vamos criar todas as tabelas do sistema.

Substitua o conteúdo do arquivo `main.py` por este código completo:

```
import psycopg
from config import DB_CONFIG


def conectar():
    conexao = psycopg.connect(**DB_CONFIG)
    return conexao


def criar_tabela_clientes():
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("""
        CREATE TABLE IF NOT EXISTS clientes (
            id SERIAL PRIMARY KEY,
            nome VARCHAR(255) NOT NULL
        );
    """)

    conexao.commit()
    cursor.close()
    conexao.close()

    print("Tabela clientes criada com sucesso.")


def criar_tabela_produtos():
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("""
        CREATE TABLE IF NOT EXISTS produtos (
            id SERIAL PRIMARY KEY,
            nome VARCHAR(255) NOT NULL,
            valor_sugerido NUMERIC(10, 2) NOT NULL
        );
    """)

    conexao.commit()
    cursor.close()
    conexao.close()

    print("Tabela produtos criada com sucesso.")


def criar_tabela_vendas():
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("""
        CREATE TABLE IF NOT EXISTS vendas (
            id SERIAL PRIMARY KEY,
            cliente_id INTEGER NOT NULL,
            data_hora TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

            CONSTRAINT fk_clientes_id_vendas
                FOREIGN KEY (cliente_id)
                REFERENCES clientes(id)
        );
    """)

    conexao.commit()
    cursor.close()
    conexao.close()

    print("Tabela vendas criada com sucesso.")


def criar_tabela_vendas_produtos():
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("""
        CREATE TABLE IF NOT EXISTS vendas_produtos (
            id SERIAL PRIMARY KEY,
            produto_id INTEGER NOT NULL,
            venda_id INTEGER NOT NULL,
            preco NUMERIC(10, 2) NOT NULL,
            quantidade INTEGER NOT NULL,

            CONSTRAINT fk_produtos_id_vendas_produtos
                FOREIGN KEY (produto_id)
                REFERENCES produtos(id),

            CONSTRAINT fk_vendas_id_vendas_produtos
                FOREIGN KEY (venda_id)
                REFERENCES vendas(id)
        );
    """)

    conexao.commit()
    cursor.close()
    conexao.close()

    print("Tabela vendas_produtos criada com sucesso.")


def criar_todas_as_tabelas():
    criar_tabela_clientes()
    criar_tabela_produtos()
    criar_tabela_vendas()
    criar_tabela_vendas_produtos()

    print("Todas as tabelas foram criadas.")


criar_todas_as_tabelas()
```

Execute o programa:

```
python main.py
```

Resultado esperado:

```
Tabela clientes criada com sucesso.
Tabela produtos criada com sucesso.
Tabela vendas criada com sucesso.
Tabela vendas_produtos criada com sucesso.
Todas as tabelas foram criadas.
```

---

# 10. Entendendo as chaves estrangeiras

Observe este trecho:

```
FOREIGN KEY (cliente_id)
REFERENCES clientes(id)
```

Isso significa:

```
O campo cliente_id da tabela vendas aponta para o campo id da tabela clientes.
```

Exemplo:

```
clientes

id | nome
1  | Ana

vendas

id | cliente_id
1  | 1
```

Nesse exemplo, a venda pertence à cliente Ana.

---

# 11. Por que existe a tabela vendas_produtos?

Uma venda pode ter vários produtos.

Exemplo:

```
Venda 1:
- 2 coxinhas
- 1 refrigerante
- 1 suco
```

Se colocássemos os produtos diretamente na tabela `vendas`, ficaria difícil organizar.

Por isso usamos a tabela `vendas_produtos`.

Ela permite registrar vários produtos dentro da mesma venda.

---

# 12. Por que o preço aparece em vendas_produtos?

A tabela `produtos` tem o campo:

```
valor_sugerido
```

Mas a tabela `vendas_produtos` tem o campo:

```
preco
```

Isso acontece porque o preço pode mudar no momento da venda.

Exemplo:

```
Coxinha cadastrada com valor sugerido: R$ 6.50

Mas em uma promoção, ela pode ser vendida por: R$ 5.00
```

Por isso o sistema salva o preço usado naquela venda.

---

# 13. Conferindo se deu certo

Se tudo deu certo, o banco agora possui quatro tabelas:

```
clientes
produtos
vendas
vendas_produtos
```

Essas tabelas formam a estrutura inicial do sistema da lanchonete.

---

# 14. Exercícios

Responda no caderno ou em um arquivo de texto:

1. Para que serve a tabela `clientes`?
2. Para que serve a tabela `produtos`?
3. Para que serve a tabela `vendas`?
4. Para que serve a tabela `vendas_produtos`?
5. O que significa `PRIMARY KEY`?
6. O que significa `FOREIGN KEY`?
7. Por que a tabela `vendas` tem o campo `cliente_id`?
8. Por que a tabela `vendas_produtos` tem o campo `produto_id`?
9. Por que usamos `NUMERIC(10, 2)` para valores em dinheiro?
10. Qual é a diferença entre `valor_sugerido` e `preco`?

---

# 15. Desafio extra

Explique com suas palavras o que acontece neste exemplo:

```
clientes

id | nome
1  | Ana

produtos

id | nome          | valor_sugerido
1  | Coxinha       | 6.50
2  | Refrigerante  | 5.00

vendas

id | cliente_id
1  | 1

vendas_produtos

id | venda_id | produto_id | preco | quantidade
1  | 1        | 1          | 6.50  | 2
2  | 1        | 2          | 5.00  | 1
```

Pergunta:

```
Quem comprou?
Quais produtos foram comprados?
Qual foi o total da venda?
```

---

# 16. Resumo da aula

Nesta aula, aprendemos que:

* o Python pode se conectar a um banco de dados real;
* uma tabela organiza informações de um tipo;
* uma chave primária identifica cada registro;
* uma chave estrangeira liga uma tabela a outra;
* uma venda pode ter vários produtos;
* o banco da lanchonete precisa de várias tabelas para organizar bem os dados.



# Aula 2 - Cadastrando Clientes e Produtos com Python

## Continuação da Aula 1

Na aula anterior, criamos a estrutura do banco de dados da lanchonete.

Criamos quatro tabelas:

```
clientes
produtos
vendas
vendas_produtos
```

Nesta aula, vamos começar a colocar informações no banco.

Vamos criar um programa em Python que permite:

* cadastrar clientes;
* cadastrar produtos;
* listar clientes cadastrados;
* listar produtos cadastrados;
* usar um menu simples no terminal.

---

# 1. Objetivo da aula

Ao final desta aula, você deverá conseguir:

* inserir dados em uma tabela usando Python;
* consultar dados do banco usando Python;
* usar comandos SQL `INSERT` e `SELECT`;
* criar um menu simples no terminal;
* entender como o Python envia e recebe informações do banco.

---

# 2. Antes de começar

Verifique se você ainda tem a pasta criada na aula anterior:

```
lanchonete-python
```

Dentro dela, devem existir os arquivos:

```
config.py
main.py
```

O arquivo `config.py` deve conter os dados de conexão com o banco:

```
DB_CONFIG = {
    "host": "SEU_HOST_AQUI",
    "port": 12345,
    "dbname": "defaultdb",
    "user": "SEU_USUARIO_AQUI",
    "password": "SUA_SENHA_AQUI",
    "sslmode": "require"
}
```

---

# 3. O que vamos fazer hoje?

Na aula passada, o Python criou as tabelas.

Hoje vamos fazer o Python executar comandos como estes:

```
INSERT INTO clientes (nome)
VALUES ('Ana');
```

E também:

```
SELECT id, nome
FROM clientes;
```

Mas, em vez de escrever os dados direto no SQL, vamos pedir para o usuário digitar pelo terminal.

---

# 4. Começando o arquivo main.py

Abra o arquivo `main.py`.

Substitua o conteúdo dele por este código inicial:

```
import psycopg
from config import DB_CONFIG


def conectar():
    conexao = psycopg.connect(**DB_CONFIG)
    return conexao
```

Esse código importa a biblioteca do PostgreSQL e cria uma função para conectar no banco.

Sempre que precisarmos acessar o banco, vamos chamar:

```
conectar()
```

---

# 5. Criando a função para cadastrar clientes

Agora vamos criar uma função chamada `cadastrar_cliente`.

Adicione este código abaixo da função `conectar`:

```
def cadastrar_cliente():
    nome = input("Digite o nome do cliente: ")

    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("""
        INSERT INTO clientes (nome)
        VALUES (%s);
    """, (nome,))

    conexao.commit()
    cursor.close()
    conexao.close()

    print("Cliente cadastrado com sucesso.")
```

---

# 6. Entendendo o cadastro de clientes

Este trecho pede o nome do cliente:

```
nome = input("Digite o nome do cliente: ")
```

Este trecho abre a conexão com o banco:

```
conexao = conectar()
```

Este trecho cria um cursor:

```
cursor = conexao.cursor()
```

O cursor é usado para executar comandos SQL.

Este trecho insere o cliente no banco:

```
cursor.execute("""
    INSERT INTO clientes (nome)
    VALUES (%s);
""", (nome,))
```

O `%s` é um espaço reservado.
O valor digitado pelo usuário será colocado ali de forma segura.

Este trecho confirma a gravação no banco:

```
conexao.commit()
```

Sem o `commit`, o dado pode não ser salvo definitivamente.

Este trecho fecha o cursor e a conexão:

```
cursor.close()
conexao.close()
```

---

# 7. Testando o cadastro de clientes

No final do arquivo `main.py`, escreva:

```
cadastrar_cliente()
```

O arquivo ficará parecido com isto:

```
import psycopg
from config import DB_CONFIG


def conectar():
    conexao = psycopg.connect(**DB_CONFIG)
    return conexao


def cadastrar_cliente():
    nome = input("Digite o nome do cliente: ")

    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("""
        INSERT INTO clientes (nome)
        VALUES (%s);
    """, (nome,))

    conexao.commit()
    cursor.close()
    conexao.close()

    print("Cliente cadastrado com sucesso.")


cadastrar_cliente()
```

Execute no terminal:

```
python main.py
```

Digite um nome de cliente, por exemplo:

```
Ana
```

Resultado esperado:

```
Cliente cadastrado com sucesso.
```

Execute mais algumas vezes e cadastre outros clientes:

```
Bruno
Carlos
Mariana
```

---

# 8. Criando a função para listar clientes

Agora vamos criar uma função para mostrar os clientes cadastrados.

Apague a linha final:

```
cadastrar_cliente()
```

E adicione esta nova função:

```
def listar_clientes():
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("""
        SELECT id, nome
        FROM clientes
        ORDER BY id;
    """)

    clientes = cursor.fetchall()

    cursor.close()
    conexao.close()

    print("\n--- Clientes cadastrados ---")

    for cliente in clientes:
        print(f"{cliente[0]} - {cliente[1]}")
```

No final do arquivo, chame a função:

```
listar_clientes()
```

Execute:

```
python main.py
```

Resultado esperado:

```
--- Clientes cadastrados ---
1 - Ana
2 - Bruno
3 - Carlos
4 - Mariana
```

---

# 9. Entendendo a listagem de clientes

Este comando busca os clientes no banco:

```
SELECT id, nome
FROM clientes
ORDER BY id;
```

Ele significa:

```
Selecione o id e o nome da tabela clientes, ordenando pelo id.
```

Este trecho pega todos os resultados:

```
clientes = cursor.fetchall()
```

Este trecho percorre os clientes encontrados:

```
for cliente in clientes:
    print(f"{cliente[0]} - {cliente[1]}")
```

Cada `cliente` é uma linha retornada pelo banco.

Exemplo:

```
cliente[0] -> id
cliente[1] -> nome
```

---

# 10. Criando a função para cadastrar produtos

Agora vamos cadastrar produtos da lanchonete.

Adicione esta função no arquivo `main.py`:

```
def cadastrar_produto():
    nome = input("Digite o nome do produto: ")
    valor_sugerido = float(input("Digite o valor sugerido: "))

    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("""
        INSERT INTO produtos (nome, valor_sugerido)
        VALUES (%s, %s);
    """, (nome, valor_sugerido))

    conexao.commit()
    cursor.close()
    conexao.close()

    print("Produto cadastrado com sucesso.")
```

No final do arquivo, troque para:

```
cadastrar_produto()
```

Execute:

```
python main.py
```

Cadastre alguns produtos:

```
Coxinha
6.50

Refrigerante
5.00

Pastel
8.00

Suco
7.00

Pão de queijo
4.50
```

---

# 11. Atenção ao valor do produto

Quando o programa pedir o valor, use ponto em vez de vírgula.

Use assim:

```
6.50
```

Não use assim:

```
6,50
```

Em Python, números decimais usam ponto.

---

# 12. Criando a função para listar produtos

Agora vamos listar os produtos cadastrados.

Adicione esta função:

```
def listar_produtos():
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("""
        SELECT id, nome, valor_sugerido
        FROM produtos
        ORDER BY id;
    """)

    produtos = cursor.fetchall()

    cursor.close()
    conexao.close()

    print("\n--- Produtos cadastrados ---")

    for produto in produtos:
        print(f"{produto[0]} - {produto[1]} - R$ {produto[2]}")
```

No final do arquivo, chame:

```
listar_produtos()
```

Execute:

```
python main.py
```

Resultado esperado:

```
--- Produtos cadastrados ---
1 - Coxinha - R$ 6.50
2 - Refrigerante - R$ 5.00
3 - Pastel - R$ 8.00
4 - Suco - R$ 7.00
5 - Pão de queijo - R$ 4.50
```

---

# 13. Criando um menu

Agora vamos criar um menu para o usuário escolher o que deseja fazer.

Adicione esta função:

```
def menu():
    while True:
        print("\n=== Sistema da Lanchonete ===")
        print("1 - Cadastrar cliente")
        print("2 - Listar clientes")
        print("3 - Cadastrar produto")
        print("4 - Listar produtos")
        print("0 - Sair")

        opcao = input("Escolha uma opção: ")

        if opcao == "1":
            cadastrar_cliente()

        elif opcao == "2":
            listar_clientes()

        elif opcao == "3":
            cadastrar_produto()

        elif opcao == "4":
            listar_produtos()

        elif opcao == "0":
            print("Encerrando o sistema...")
            break

        else:
            print("Opção inválida.")
```

No final do arquivo, deixe apenas:

```
menu()
```

---

# 14. Código completo da Aula 2

Ao final da aula, o arquivo `main.py` deve ficar assim:

```
import psycopg
from config import DB_CONFIG


def conectar():
    conexao = psycopg.connect(**DB_CONFIG)
    return conexao


def cadastrar_cliente():
    nome = input("Digite o nome do cliente: ")

    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("""
        INSERT INTO clientes (nome)
        VALUES (%s);
    """, (nome,))

    conexao.commit()
    cursor.close()
    conexao.close()

    print("Cliente cadastrado com sucesso.")


def listar_clientes():
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("""
        SELECT id, nome
        FROM clientes
        ORDER BY id;
    """)

    clientes = cursor.fetchall()

    cursor.close()
    conexao.close()

    print("\n--- Clientes cadastrados ---")

    for cliente in clientes:
        print(f"{cliente[0]} - {cliente[1]}")


def cadastrar_produto():
    nome = input("Digite o nome do produto: ")
    valor_sugerido = float(input("Digite o valor sugerido: "))

    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("""
        INSERT INTO produtos (nome, valor_sugerido)
        VALUES (%s, %s);
    """, (nome, valor_sugerido))

    conexao.commit()
    cursor.close()
    conexao.close()

    print("Produto cadastrado com sucesso.")


def listar_produtos():
    conexao = conectar()
    cursor = conexao.cursor()

    cursor.execute("""
        SELECT id, nome, valor_sugerido
        FROM produtos
        ORDER BY id;
    """)

    produtos = cursor.fetchall()

    cursor.close()
    conexao.close()

    print("\n--- Produtos cadastrados ---")

    for produto in produtos:
        print(f"{produto[0]} - {produto[1]} - R$ {produto[2]}")


def menu():
    while True:
        print("\n=== Sistema da Lanchonete ===")
        print("1 - Cadastrar cliente")
        print("2 - Listar clientes")
        print("3 - Cadastrar produto")
        print("4 - Listar produtos")
        print("0 - Sair")

        opcao = input("Escolha uma opção: ")

        if opcao == "1":
            cadastrar_cliente()

        elif opcao == "2":
            listar_clientes()

        elif opcao == "3":
            cadastrar_produto()

        elif opcao == "4":
            listar_produtos()

        elif opcao == "0":
            print("Encerrando o sistema...")
            break

        else:
            print("Opção inválida.")


menu()
```

---

# 15. Executando o programa final

No terminal, execute:

```
python main.py
```

O menu deve aparecer:

```
=== Sistema da Lanchonete ===
1 - Cadastrar cliente
2 - Listar clientes
3 - Cadastrar produto
4 - Listar produtos
0 - Sair
Escolha uma opção:
```

Teste todas as opções.

---

# 16. Atividade prática

Cadastre pelo menos 3 clientes:

```
Ana
Bruno
Mariana
```

Cadastre pelo menos 5 produtos:

```
Coxinha - 6.50
Refrigerante - 5.00
Pastel - 8.00
Suco - 7.00
Pão de queijo - 4.50
```

Depois, use as opções de listagem para verificar se os dados foram salvos corretamente.

---

# 17. Perguntas para responder

Responda no caderno ou em um arquivo de texto:

1. Para que serve o comando `INSERT INTO`?
2. Para que serve o comando `SELECT`?
3. O que o comando `commit()` faz?
4. Por que usamos `%s` dentro do comando SQL?
5. O que a função `fetchall()` retorna?
6. Qual é a diferença entre cadastrar e listar?
7. Por que usamos um menu com `while True`?
8. O que acontece quando o usuário escolhe a opção `0`?
9. Por que o valor do produto precisa ser digitado com ponto?
10. Qual tabela guarda os nomes dos clientes?

---

# 18. Desafio extra

Adicione uma nova opção no menu:

```
5 - Buscar cliente pelo nome
```

Dica: você pode usar um comando parecido com este:

```
SELECT id, nome
FROM clientes
WHERE nome ILIKE %s;
```

O `ILIKE` permite buscar sem diferenciar letras maiúsculas e minúsculas.

Exemplo:

```
ana
```

Pode encontrar:

```
Ana
```

---

# 19. Resumo da aula

Nesta aula, aprendemos que:

* o Python pode inserir dados no banco;
* o comando `INSERT INTO` salva informações;
* o comando `SELECT` consulta informações;
* o menu permite escolher ações no sistema;
* clientes e produtos já podem ser cadastrados;
* os dados continuam salvos mesmo depois que o programa fecha.

Na próxima aula, vamos registrar uma venda escolhendo um cliente e adicionando produtos vendidos.

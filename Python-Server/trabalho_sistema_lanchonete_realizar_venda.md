# Trabalho — Sistema de Lanchonete: Realização de Venda

## Valor

Este trabalho valerá **1,0 ponto na média**.

---

## Contexto

Nas aulas anteriores, criamos a estrutura inicial de um sistema de lanchonete usando **Python** e **PostgreSQL**.

O sistema já possui as seguintes tabelas:

- `clientes`
- `produtos`
- `vendas`
- `vendas_produtos`

Também já foram trabalhadas funções para:

- conectar ao banco de dados usando `.env`;
- cadastrar clientes;
- listar e buscar clientes;
- cadastrar produtos;
- listar e buscar produtos;
- criar um menu no terminal.

Agora, o objetivo é avançar no sistema e permitir que uma venda seja realizada.

---

## Objetivo do trabalho

Você deverá implementar no sistema uma nova opção de menu para **realizar uma venda**.

Essa opção deverá chamar uma função chamada:

    processo_realizar_venda()

A função deverá controlar todo o processo de uma venda, desde a escolha do cliente até o registro dos produtos vendidos.

---

## O que deverá ser feito

### 1. Atualizar o menu principal

O menu do sistema deverá ter uma nova opção:

    5 - Realizar venda

Exemplo:

    === Sistema da Lanchonete ===
    1 - Cadastrar cliente
    2 - Listar ou buscar clientes
    3 - Cadastrar produto
    4 - Listar ou buscar produtos
    5 - Realizar venda
    0 - Sair

Quando o usuário escolher a opção `5`, o sistema deverá chamar a função:

    processo_realizar_venda()

---

## 2. Criar a função processo_realizar_venda()

A função `processo_realizar_venda()` deverá organizar as etapas da venda.

Ela deverá fazer, no mínimo, o seguinte processo:

### Etapa 1 — Escolher o cliente

O sistema deverá mostrar os clientes cadastrados e permitir que o usuário escolha o cliente da venda.

Exemplo:

    --- Clientes cadastrados ---
    1 - Ana
    2 - Bruno
    3 - Mariana

    Digite o ID do cliente: 1

O ID escolhido será usado para registrar a venda na tabela `vendas`.

---

### Etapa 2 — Criar a venda

Depois de escolher o cliente, o sistema deverá criar um registro na tabela `vendas`.

A tabela `vendas` guarda que uma venda aconteceu.

Exemplo de registro:

    id | cliente_id | data_hora
    1  | 1          | 2026-06-09 10:30:00

Importante:

A função que cria a venda deverá retornar o ID da venda criada, pois esse ID será usado para registrar os produtos vendidos.

---

### Etapa 3 — Escolher produtos para a venda

Depois de criar a venda, o sistema deverá permitir adicionar produtos a essa venda.

O sistema deverá mostrar os produtos cadastrados.

Exemplo:

    --- Produtos cadastrados ---
    1 - Coxinha - R$ 6.50
    2 - Refrigerante - R$ 5.00
    3 - Pastel - R$ 8.00

    Digite o ID do produto: 1
    Digite a quantidade: 2

Esse produto deverá ser salvo na tabela `vendas_produtos`.

---

### Etapa 4 — Permitir mais de um produto na mesma venda

Uma venda pode ter mais de um produto.

Depois de adicionar um produto, o sistema deverá perguntar se o usuário deseja adicionar outro produto.

Exemplo:

    Deseja adicionar outro produto? (s/n): s

Se o usuário responder `s`, o sistema deverá permitir escolher outro produto.

Se o usuário responder `n`, a venda deverá ser finalizada.

---

### Etapa 5 — Registrar os produtos vendidos

Cada produto escolhido deverá ser registrado na tabela `vendas_produtos`.

Essa tabela deve guardar:

- o ID da venda;
- o ID do produto;
- o preço do produto no momento da venda;
- a quantidade vendida.

Exemplo:

    venda_id | produto_id | preco | quantidade
    1        | 1          | 6.50  | 2
    1        | 2          | 5.00  | 1

---

### Etapa 6 — Mostrar o resumo da venda

Ao final da venda, o sistema deverá mostrar um resumo.

Exemplo:

    Venda realizada com sucesso!

    Cliente: Ana

    Produtos:
    2x Coxinha - R$ 6.50 cada - subtotal R$ 13.00
    1x Refrigerante - R$ 5.00 cada - subtotal R$ 5.00

    Total da venda: R$ 18.00

---

---

## Queries de exemplo

Antes de implementar a função em Python, é importante entender quais comandos SQL serão executados no banco de dados.

A venda acontece em duas partes:

1. primeiro, o sistema cria um registro na tabela `vendas`;
2. depois, o sistema registra os produtos vendidos na tabela `vendas_produtos`.

---

### 1. Criando uma venda

Exemplo de query para criar uma venda para o cliente de ID `1`:

    INSERT INTO vendas (cliente_id, data_hora)
    VALUES (1, NOW());

Essa query cria um novo registro na tabela `vendas`.

Exemplo:

    cliente_id = 1

Significa que a venda pertence ao cliente que possui o ID `1`.

O comando:

    NOW()

usa a data e a hora atuais do banco de dados.

---

### 2. Registrando produtos dentro da venda

Depois que a venda foi criada, é necessário registrar os produtos que fazem parte dela.

Exemplo:

    INSERT INTO vendas_produtos
        (venda_id, produto_id, quantidade, preco)
    VALUES
        (3, 1, 1, 5),
        (3, 4, 1, 7.5),
        (3, 5, 2, 4.3);

Nesse exemplo, os produtos estão sendo adicionados à venda de ID `3`.

Cada linha representa um produto vendido.

| venda_id | produto_id | quantidade | preco |
|---:|---:|---:|---:|
| 3 | 1 | 1 | 5.00 |
| 3 | 4 | 1 | 7.50 |
| 3 | 5 | 2 | 4.30 |

Interpretação:

- a venda `3` possui o produto `1`, com quantidade `1` e preço `5.00`;
- a venda `3` possui o produto `4`, com quantidade `1` e preço `7.50`;
- a venda `3` possui o produto `5`, com quantidade `2` e preço `4.30`.

---

### 3. Calculando o total da venda

Para calcular o total de uma venda, é necessário multiplicar o preço pela quantidade de cada item.

Exemplo de query:

    SELECT
        SUM(quantidade * preco) AS total
    FROM vendas_produtos
    WHERE venda_id = 3;

Essa query calcula o total da venda de ID `3`.

No exemplo anterior, o cálculo seria:

    1 x 5.00  = 5.00
    1 x 7.50  = 7.50
    2 x 4.30  = 8.60

    Total = 21.10

---

### 4. Buscando o resumo da venda

Para mostrar o resumo da venda, podemos buscar o cliente, os produtos, as quantidades, os preços e os subtotais.

Exemplo:

    SELECT
        vendas.id AS venda_id,
        clientes.nome AS cliente,
        produtos.nome AS produto,
        vendas_produtos.quantidade,
        vendas_produtos.preco,
        vendas_produtos.quantidade * vendas_produtos.preco AS subtotal
    FROM vendas
    INNER JOIN clientes
        ON clientes.id = vendas.cliente_id
    INNER JOIN vendas_produtos
        ON vendas_produtos.venda_id = vendas.id
    INNER JOIN produtos
        ON produtos.id = vendas_produtos.produto_id
    WHERE vendas.id = 3;

Resultado esperado:

    venda_id | cliente | produto       | quantidade | preco | subtotal
    3        | Ana     | Coxinha       | 1          | 5.00  | 5.00
    3        | Ana     | Refrigerante  | 1          | 7.50  | 7.50
    3        | Ana     | Pão de queijo | 2          | 4.30  | 8.60

---

### 5. Relação entre SQL e Python

No trabalho, essas queries deverão ser usadas dentro do Python com parâmetros.

Por exemplo, em vez de escrever diretamente:

    INSERT INTO vendas (cliente_id, data_hora)
    VALUES (1, NOW());

O ideal é fazer algo como:

    cursor.execute("""
        INSERT INTO vendas (cliente_id, data_hora)
        VALUES (%s, NOW())
        RETURNING id;
    """, (cliente_id,))

Assim, o valor do `cliente_id` vem da escolha feita pelo usuário no sistema.

O uso de:

    RETURNING id

é importante porque permite descobrir o ID da venda que acabou de ser criada.

Esse ID será usado para inserir os produtos na tabela `vendas_produtos`.

---

### 6. Exemplo de lógica esperada

A função `processo_realizar_venda()` deverá seguir uma lógica parecida com esta:

    1. mostrar os clientes cadastrados;
    2. pedir o ID do cliente;
    3. criar a venda na tabela vendas;
    4. guardar o ID da venda criada;
    5. mostrar os produtos cadastrados;
    6. pedir o ID do produto;
    7. pedir a quantidade;
    8. buscar o preço do produto;
    9. salvar o produto na tabela vendas_produtos;
    10. perguntar se deseja adicionar outro produto;
    11. repetir o processo se necessário;
    12. mostrar o resumo e o total da venda.


## Funções esperadas

Você pode organizar seu código da forma que preferir, mas o trabalho deverá ter obrigatoriamente a função:

    processo_realizar_venda()

Além dela, recomenda-se criar funções auxiliares, por exemplo:

    criar_venda(cliente_id)

    adicionar_produto_na_venda(venda_id, produto_id, preco, quantidade)

    buscar_cliente_por_id(cliente_id)

    buscar_produto_por_id(produto_id)

    calcular_total_venda(venda_id)

    mostrar_resumo_venda(venda_id)

Essas funções ajudam a deixar o código mais organizado.

---

## Regras importantes

O trabalho deverá seguir estas regras:

1. O sistema deve continuar usando o arquivo `.env` para a conexão com o banco.
2. O arquivo `.env` não deve ser enviado para o GitHub.
3. O arquivo `.gitignore` deve conter o `.env`.
4. O menu deve ter a opção para realizar venda.
5. A opção de venda deve chamar a função `processo_realizar_venda()`.
6. A venda deve ser salva na tabela `vendas`.
7. Os produtos da venda devem ser salvos na tabela `vendas_produtos`.
8. A venda deve permitir mais de um produto.
9. O sistema deve pedir a quantidade de cada produto.
10. Ao final, o sistema deve mostrar o total da venda.

---

## Entrega

O trabalho deverá ser entregue em um repositório no GitHub.

O repositório deve conter pelo menos:

    main.py
    .gitignore
    README.md

O arquivo `.env` não deve ser enviado.

No `README.md`, escreva:

- o nome do aluno ou da dupla;
- uma breve explicação do sistema;
- quais funcionalidades foram implementadas;
- como executar o programa;
- quais bibliotecas precisam ser instaladas.

Exemplo de instalação das bibliotecas:

    pip install psycopg[binary] python-dotenv

---

## Sugestão de estrutura do README.md

    # Sistema de Lanchonete

    ## Integrantes

    Nome do aluno ou dupla

    ## Descrição

    Este sistema permite cadastrar clientes, cadastrar produtos, listar registros e realizar vendas usando Python e PostgreSQL.

    ## Funcionalidades

    - Cadastrar cliente
    - Buscar clientes
    - Cadastrar produto
    - Buscar produtos
    - Realizar venda
    - Mostrar resumo da venda

    ## Como executar

    1. Instale as bibliotecas:

        pip install psycopg[binary] python-dotenv

    2. Crie um arquivo .env com os dados do banco.

    3. Execute o programa:

        python main.py

---

## Critérios de avaliação

O trabalho valerá **1,0 ponto**.

A avaliação será feita da seguinte forma:

| Critério | Valor |
|---|---:|
| Menu com a opção “Realizar venda” chamando `processo_realizar_venda()` | 0,15 |
| Escolha correta do cliente | 0,15 |
| Criação da venda na tabela `vendas` | 0,15 |
| Escolha de produtos e quantidades | 0,20 |
| Registro dos produtos na tabela `vendas_produtos` | 0,15 |
| Cálculo e exibição do total da venda | 0,10 |
| Organização do código e entrega no GitHub com README | 0,10 |

Total: **1,0 ponto**

---

## Entrega

O trabalho deverá estar disponível no seu próprio GitHub até o dia 15/06 às 23:59

---

## Observações

O professor fará em aula uma explicação das principais queries necessárias usando apenas o banco de dados.

A implementação completa em Python deverá ser feita pelos alunos e entregue no GitHub.

O objetivo não é apenas copiar código, mas entender como o sistema registra uma venda usando mais de uma tabela.

---

## Desafio extra

O desafio extra não é obrigatório, mas poderá ser considerado como melhoria do trabalho.

Sugestões:

- validar se o cliente escolhido existe;
- validar se o produto escolhido existe;
- impedir quantidade menor ou igual a zero;
- permitir cancelar uma venda antes de finalizar;
- mostrar o histórico de vendas realizadas;
- mostrar os itens de uma venda já cadastrada;
- formatar os valores em reais.

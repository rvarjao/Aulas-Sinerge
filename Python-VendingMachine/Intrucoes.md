# Aula — Máquina de Vendas Automática

Continuação da aula do **caixa eletrônico**

## Objetivo

Nesta aula, você vai criar um programa em Python que simula uma **máquina de vendas automática**.

A máquina deverá:

1. Mostrar uma lista de produtos.
2. Permitir que o usuário escolha um produto.
3. Receber o valor pago.
4. Verificar se o dinheiro é suficiente.
5. Calcular o troco.
6. Mostrar quais notas ou moedas serão usadas no troco.

---

# Parte 1 — Criando o menu de produtos

Comece criando um programa que apenas mostra os produtos disponíveis.

```python
print("=== Máquina de Vendas ===")
print("1 - Água - R$ 3,00")
print("2 - Refrigerante - R$ 5,00")
print("3 - Suco - R$ 6,00")
print("4 - Salgadinho - R$ 7,00")
print("5 - Chocolate - R$ 4,00")
```

Execute o programa e veja se o menu apareceu corretamente.

---

# Parte 2 — Lendo a escolha do usuário

Agora peça para o usuário digitar o código do produto.

```python
codigo = int(input("Digite o código do produto: "))
```

Depois, teste mostrando o código digitado:

```python
print("Código escolhido:", codigo)
```

Neste momento, o programa ainda não sabe qual produto foi escolhido. Ele apenas está lendo o número digitado.

---

# Parte 3 — Identificando o produto escolhido

Agora vamos criar duas variáveis:

```python
produto = ""
preco = 0
```

A variável `produto` vai guardar o nome do produto escolhido.
A variável `preco` vai guardar o preço do produto.

Agora use `if`, `elif` e `else` para identificar o produto.

```python
if codigo == 1:
    produto = "Água"
    preco = 3
elif codigo == 2:
    produto = "Refrigerante"
    preco = 5
elif codigo == 3:
    produto = "Suco"
    preco = 6
elif codigo == 4:
    produto = "Salgadinho"
    preco = 7
elif codigo == 5:
    produto = "Chocolate"
    preco = 4
else:
    print("Produto inválido")
```

Depois desse bloco, mostre o produto e o preço:

```python
print("Produto escolhido:", produto)
print("Preço: R$", preco)
```

Teste o programa digitando códigos diferentes.

---

# Parte 4 — Evitando continuar se o produto for inválido

Se o usuário digitar um código inválido, o preço continuará valendo `0`.

Por isso, vamos colocar o restante do programa dentro deste `if`:

```python
if preco > 0:
    print("Produto válido")
```

Agora coloque a parte do pagamento dentro desse bloco.

Exemplo:

```python
if preco > 0:
    valor_pago = float(input("Digite o valor pago: R$ "))
```

Assim, o programa só continua se o produto escolhido for válido.

---

# Parte 5 — Verificando se o dinheiro é suficiente

Agora compare o valor pago com o preço do produto.

```python
if valor_pago < preco:
    falta = preco - valor_pago
    print("Dinheiro insuficiente.")
    print("Faltam R$", falta)
elif valor_pago == preco:
    print("Compra realizada com sucesso.")
    print("Não há troco.")
else:
    troco = valor_pago - preco
    print("Compra realizada com sucesso.")
    print("Troco: R$", troco)
```

Teste três situações:

```text
Valor menor que o preço
Valor igual ao preço
Valor maior que o preço
```

Exemplo:

```text
Produto: Água
Preço: R$ 3,00
Valor pago: R$ 2,00
Resultado: falta dinheiro
```

```text
Produto: Água
Preço: R$ 3,00
Valor pago: R$ 3,00
Resultado: compra sem troco
```

```text
Produto: Água
Preço: R$ 3,00
Valor pago: R$ 10,00
Resultado: compra com troco
```

---

# Parte 6 — Código até aqui

Seu código deve estar parecido com este:

```python
print("=== Máquina de Vendas ===")
print("1 - Água - R$ 3,00")
print("2 - Refrigerante - R$ 5,00")
print("3 - Suco - R$ 6,00")
print("4 - Salgadinho - R$ 7,00")
print("5 - Chocolate - R$ 4,00")

codigo = int(input("Digite o código do produto: "))

produto = ""
preco = 0

if codigo == 1:
    produto = "Água"
    preco = 3
elif codigo == 2:
    produto = "Refrigerante"
    preco = 5
elif codigo == 3:
    produto = "Suco"
    preco = 6
elif codigo == 4:
    produto = "Salgadinho"
    preco = 7
elif codigo == 5:
    produto = "Chocolate"
    preco = 4
else:
    print("Produto inválido")

if preco > 0:
    print("Produto escolhido:", produto)
    print("Preço: R$", preco)

    valor_pago = float(input("Digite o valor pago: R$ "))

    if valor_pago < preco:
        falta = preco - valor_pago
        print("Dinheiro insuficiente.")
        print("Faltam R$", falta)

    elif valor_pago == preco:
        print("Compra realizada com sucesso.")
        print("Não há troco.")

    else:
        troco = valor_pago - preco
        print("Compra realizada com sucesso.")
        print("Troco: R$", troco)
```

---

# Parte 7 — Calculando o troco com notas e moedas

Agora vamos fazer algo parecido com a aula do **caixa eletrônico**.

A máquina deve informar como devolver o troco usando os valores:

```text
10, 5, 2 e 1
```

Imagine que o troco seja R$ 7,00.

A máquina poderia devolver:

```text
1 nota de R$ 5
1 moeda de R$ 2
```

---

# Parte 8 — Entendendo a lógica do troco

Use esta lista:

```python
valores = [10, 5, 2, 1]
```

Depois, use um `for` para testar cada valor:

```python
for valor in valores:
    quantidade = troco // valor
    troco = troco % valor

    if quantidade > 0:
        print(quantidade, "nota/moeda de R$", valor)
```

O operador `//` calcula quantas notas ou moedas cabem no troco.

Exemplo:

```python
7 // 5
```

Resultado:

```text
1
```

Porque uma nota de 5 cabe dentro de 7.

O operador `%` calcula o resto.

Exemplo:

```python
7 % 5
```

Resultado:

```text
2
```

Porque depois de tirar 5 de 7, sobra 2.

---

# Parte 9 — Inserindo essa lógica no programa

Na parte em que existe troco, substitua isto:

```python
print("Troco: R$", troco)
```

Por isto:

```python
print("Troco total: R$", troco)

troco_inteiro = int(troco)

valores = [10, 5, 2, 1]

print("Troco entregue:")

for valor in valores:
    quantidade = troco_inteiro // valor
    troco_inteiro = troco_inteiro % valor

    if quantidade > 0:
        print(quantidade, "nota/moeda de R$", valor)
```

---

# Parte 10 — Código final

```python
print("=== Máquina de Vendas ===")
print("1 - Água - R$ 3,00")
print("2 - Refrigerante - R$ 5,00")
print("3 - Suco - R$ 6,00")
print("4 - Salgadinho - R$ 7,00")
print("5 - Chocolate - R$ 4,00")

codigo = int(input("Digite o código do produto: "))

produto = ""
preco = 0

if codigo == 1:
    produto = "Água"
    preco = 3
elif codigo == 2:
    produto = "Refrigerante"
    preco = 5
elif codigo == 3:
    produto = "Suco"
    preco = 6
elif codigo == 4:
    produto = "Salgadinho"
    preco = 7
elif codigo == 5:
    produto = "Chocolate"
    preco = 4
else:
    print("Produto inválido")

if preco > 0:
    print("Produto escolhido:", produto)
    print("Preço: R$", preco)

    valor_pago = float(input("Digite o valor pago: R$ "))

    if valor_pago < preco:
        falta = preco - valor_pago
        print("Dinheiro insuficiente.")
        print("Faltam R$", falta)

    elif valor_pago == preco:
        print("Compra realizada com sucesso.")
        print("Não há troco.")

    else:
        troco = valor_pago - preco
        print("Compra realizada com sucesso.")
        print("Troco total: R$", troco)

        troco_inteiro = int(troco)

        valores = [10, 5, 2, 1]

        print("Troco entregue:")

        for valor in valores:
            quantidade = troco_inteiro // valor
            troco_inteiro = troco_inteiro % valor

            if quantidade > 0:
                print(quantidade, "nota/moeda de R$", valor)
```

---

# Parte 11 — Testes obrigatórios

Teste seu programa com os seguintes casos:

## Teste 1

```text
Produto: Água
Valor pago: R$ 2,00
```

Resultado esperado:

```text
Dinheiro insuficiente
Faltam R$ 1,00
```

---

## Teste 2

```text
Produto: Água
Valor pago: R$ 3,00
```

Resultado esperado:

```text
Compra realizada
Não há troco
```

---

## Teste 3

```text
Produto: Água
Valor pago: R$ 10,00
```

Resultado esperado:

```text
Compra realizada
Troco total: R$ 7,00
1 nota/moeda de R$ 5
1 nota/moeda de R$ 2
```

---

## Teste 4

```text
Produto: Chocolate
Valor pago: R$ 10,00
```

Resultado esperado:

```text
Troco total: R$ 6,00
1 nota/moeda de R$ 5
1 nota/moeda de R$ 1
```

---

## Teste 5

```text
Código do produto: 9
```

Resultado esperado:

```text
Produto inválido
```

---

# Desafio 1 — Quantidade de produtos

Agora modifique o programa para permitir que o usuário escolha a quantidade.

Depois de identificar o produto, pergunte:

```python
quantidade = int(input("Digite a quantidade desejada: "))
```

Depois calcule o total:

```python
total = preco * quantidade
```

Agora o programa deve comparar o valor pago com o `total`, e não mais apenas com o `preco`.

Exemplo:

```text
Produto: Água
Preço: R$ 3,00
Quantidade: 2
Total: R$ 6,00
```

---

# Desafio 2 — Máquina com repetição

Faça a máquina continuar funcionando até o usuário escolher sair.

Menu sugerido:

```text
1 - Comprar produto
2 - Sair
```

Estrutura inicial:

```python
opcao = 1

while opcao != 2:
    print("1 - Comprar produto")
    print("2 - Sair")

    opcao = int(input("Escolha uma opção: "))

    if opcao == 1:
        print("Aqui entra a lógica da compra")

    elif opcao == 2:
        print("Encerrando a máquina")

    else:
        print("Opção inválida")
```


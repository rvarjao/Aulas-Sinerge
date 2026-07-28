# Revisão de Python — Funções

## Objetivo

Nesta atividade, vamos revisar:

* criação de funções;
* parâmetros;
* retorno com `return`;
* entrada de dados com `input`;
* cálculos matemáticos.

Hoje construiremos um pequeno **sistema financeiro**.

---

# Exercício 1 — Desconto

## Passo 1 — Criar o arquivo

Crie um arquivo chamado:

```text
financeiro.py
```

## Passo 2 — Criar a função

Crie a função abaixo:

```python
def calcular_desconto(valor, percentual):
    desconto = valor * percentual / 100
    return desconto
```

A função recebe dois parâmetros:

* `valor`: valor original do produto;
* `percentual`: percentual de desconto.

Ao final, ela retorna o valor do desconto.

## Passo 3 — Solicitar os dados ao usuário

```python
valor = float(input("Digite o valor do produto: R$ "))
percentual = float(input("Digite o percentual de desconto: "))
```

## Passo 4 — Chamar a função

```python
desconto = calcular_desconto(valor, percentual)
```

## Passo 5 — Calcular o valor final

```python
valor_final = valor - desconto
```

## Passo 6 — Mostrar os resultados

```python
print(f"Valor original: R$ {valor:.2f}")
print(f"Valor do desconto: R$ {desconto:.2f}")
print(f"Valor final: R$ {valor_final:.2f}")
```

## Código completo

```python
def calcular_desconto(valor, percentual):
    desconto = valor * percentual / 100
    return desconto


valor = float(input("Digite o valor do produto: R$ "))
percentual = float(input("Digite o percentual de desconto: "))

desconto = calcular_desconto(valor, percentual)
valor_final = valor - desconto

print(f"Valor original: R$ {valor:.2f}")
print(f"Valor do desconto: R$ {desconto:.2f}")
print(f"Valor final: R$ {valor_final:.2f}")
```

## Teste

### Entrada

```text
Valor: 250
Desconto: 15
```

### Saída esperada

```text
Valor original: R$ 250.00
Valor do desconto: R$ 37.50
Valor final: R$ 212.50
```

---

# Exercício 2 — Juros Simples

Agora é sua vez!

Complete a função abaixo:

```python
def calcular_juros_simples(capital, taxa, tempo):
    pass
```

Depois, utilize essa função para:

1. ler o capital;
2. ler a taxa de juros, em porcentagem ao mês;
3. ler o tempo, em meses;
4. mostrar:

   * capital inicial;
   * juros;
   * montante final.

---

# Exercício 3 — Juros Compostos

Complete a função abaixo:

```python
def calcular_juros_compostos(capital, taxa, tempo):
    pass
```

Depois, utilize essa função para:

1. ler o capital;
2. ler a taxa de juros, em porcentagem ao mês;
3. ler o tempo, em meses;
4. mostrar:

   * capital inicial;
   * juros;
   * montante final.

---

# Desafio — Sistema financeiro

Crie um menu com as seguintes opções:

```text
SISTEMA FINANCEIRO

1 - Calcular desconto
2 - Juros simples
3 - Juros compostos
0 - Sair
```

Faça com que cada opção execute a função correspondente.

## Desafio extra

Pesquise na internet as fórmulas dos **juros simples** e dos **juros compostos** antes de implementar as funções.

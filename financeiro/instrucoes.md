Revisão de Python – Funções
Objetivo

Nesta atividade, vamos revisar:

criação de funções;
parâmetros;
retorno (return);
entrada de dados (input);
cálculos matemáticos.

Hoje construiremos um pequeno sistema financeiro.

Exercício 1 – Desconto
Passo 1

Crie um arquivo chamado:

financeiro.py
Passo 2

Crie a função abaixo:

def calcular_desconto(valor, percentual):
    desconto = valor * percentual / 100
    return desconto
Passo 3

Solicite os dados ao usuário.

valor = float(input("Digite o valor do produto: R$ "))
percentual = float(input("Digite o percentual de desconto: "))
Passo 4

Chame a função.

desconto = calcular_desconto(valor, percentual)
Passo 5

Calcule o valor final.

valor_final = valor - desconto
Passo 6

Mostre os resultados.

print(f"Valor original: R$ {valor:.2f}")
print(f"Valor do desconto: R$ {desconto:.2f}")
print(f"Valor final: R$ {valor_final:.2f}")
Código completo
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
Teste

Entrada:

Valor: 250
Desconto: 15

Saída esperada:

Valor original: R$ 250.00
Valor do desconto: R$ 37.50
Valor final: R$ 212.50
Exercício 2 – Juros Simples

Agora é sua vez!

Complete a função abaixo.

def calcular_juros_simples(capital, taxa, tempo):
    pass

Depois utilize essa função para:

ler o capital;
ler a taxa de juros (% ao mês);
ler o tempo (meses);
mostrar:
Capital inicial;
Juros;
Montante final.
Exercício 3 – Juros Compostos

Complete a função abaixo.

def calcular_juros_compostos(capital, taxa, tempo):
    pass

Depois utilize essa função para:

ler o capital;
ler a taxa de juros (% ao mês);
ler o tempo (meses);
mostrar:
Capital inicial;
Juros;
Montante final.
Desafio

Crie um menu:

SISTEMA FINANCEIRO

1 - Calcular desconto
2 - Juros simples
3 - Juros compostos
0 - Sair

Faça com que cada opção execute a função correspondente.

Desafio extra: pesquise na internet a fórmula dos juros simples e dos juros compostos antes de implementar as funções.

# Aula — Conversor de Unidades em Python

## Objetivo da atividade

Nesta atividade, você irá criar um programa em Python para realizar **conversões de unidades**.

O programa terá um menu inicial com quatro categorias:

1. Temperatura
2. Distância
3. Área
4. Tempo

Dentro de cada categoria, haverá um submenu com as conversões específicas. Cada opção do menu deverá chamar uma função diferente.

---

## O que você irá praticar

Durante esta atividade, você irá praticar:

* criação de funções;
* uso de `if`, `elif` e `else`;
* criação de menus;
* uso de `while`;
* entrada de dados com `input`;
* conversão de valores com `float`;
* organização do código em partes menores.

---

# Parte 1 — Menu inicial do conversor

Crie uma função chamada `menu_conversao_unidades()`.

Essa função será o menu inicial do programa.

```python
def menu_conversao_unidades():
    while True:
        print("\n=== CONVERSÃO DE UNIDADES ===")
        print("1 - Temperatura")
        print("2 - Distância")
        print("3 - Área")
        print("4 - Tempo")
        print("5 - Sair")

        opcao = input("Escolha uma opção: ")

        if opcao == "1":
            menu_temperatura()
        elif opcao == "2":
            menu_distancia()
        elif opcao == "3":
            menu_area()
        elif opcao == "4":
            menu_tempo()
        elif opcao == "5":
            print("Encerrando o programa...")
            break
        else:
            print("Opção inválida. Tente novamente.")
```

Atenção: esse menu não deve fazer cálculos diretamente.
Ele deve apenas chamar outras funções.

---

# Parte 2 — Menu de temperatura

Crie a função `menu_temperatura()`.

Ela deverá mostrar as opções:

1. Celsius para Fahrenheit
2. Fahrenheit para Celsius
3. Celsius para Kelvin
4. Kelvin para Celsius
5. Retornar ao menu de conversão de unidades

```python
def menu_temperatura():
    while True:
        print("\n=== TEMPERATURA ===")
        print("1 - Celsius para Fahrenheit")
        print("2 - Fahrenheit para Celsius")
        print("3 - Celsius para Kelvin")
        print("4 - Kelvin para Celsius")
        print("5 - Retornar")

        opcao = input("Escolha uma opção: ")

        if opcao == "1":
            celsius_para_fahrenheit()
        elif opcao == "2":
            fahrenheit_para_celsius()
        elif opcao == "3":
            celsius_para_kelvin()
        elif opcao == "4":
            kelvin_para_celsius()
        elif opcao == "5":
            break
        else:
            print("Opção inválida. Tente novamente.")
```

Fórmulas:

```text
F = C × 1.8 + 32
C = (F - 32) / 1.8
K = C + 273.15
C = K - 273.15
```

Exemplo de função pronta:

```python
def celsius_para_fahrenheit():
    celsius = float(input("Digite a temperatura em Celsius: "))
    fahrenheit = celsius * 1.8 + 32
    print("Resultado:", fahrenheit, "°F")
```

Agora implemente as demais funções:

```python
def fahrenheit_para_celsius():
    # implemente aqui
    pass


def celsius_para_kelvin():
    # implemente aqui
    pass


def kelvin_para_celsius():
    # implemente aqui
    pass
```

---

# Parte 3 — Menu de distância

Crie a função `menu_distancia()`.

Ela deverá mostrar as opções:

1. Metros para centímetros
2. Centímetros para metros
3. Quilômetros para metros
4. Metros para quilômetros
5. Retornar ao menu de conversão de unidades

```python
def menu_distancia():
    while True:
        print("\n=== DISTÂNCIA ===")
        print("1 - Metros para centímetros")
        print("2 - Centímetros para metros")
        print("3 - Quilômetros para metros")
        print("4 - Metros para quilômetros")
        print("5 - Retornar")

        opcao = input("Escolha uma opção: ")

        if opcao == "1":
            metros_para_centimetros()
        elif opcao == "2":
            centimetros_para_metros()
        elif opcao == "3":
            quilometros_para_metros()
        elif opcao == "4":
            metros_para_quilometros()
        elif opcao == "5":
            break
        else:
            print("Opção inválida. Tente novamente.")
```

Fórmulas:

```text
centímetros = metros × 100
metros = centímetros / 100
metros = quilômetros × 1000
quilômetros = metros / 1000
```

Funções que você deverá implementar:

```python
def metros_para_centimetros():
    # implemente aqui
    pass


def centimetros_para_metros():
    # implemente aqui
    pass


def quilometros_para_metros():
    # implemente aqui
    pass


def metros_para_quilometros():
    # implemente aqui
    pass
```

---

# Parte 4 — Menu de área

Crie a função `menu_area()`.

Ela deverá mostrar as opções:

1. Metros quadrados para centímetros quadrados
2. Centímetros quadrados para metros quadrados
3. Metros quadrados para quilômetros quadrados
4. Quilômetros quadrados para metros quadrados
5. Retornar ao menu de conversão de unidades

```python
def menu_area():
    while True:
        print("\n=== ÁREA ===")
        print("1 - Metros quadrados para centímetros quadrados")
        print("2 - Centímetros quadrados para metros quadrados")
        print("3 - Metros quadrados para quilômetros quadrados")
        print("4 - Quilômetros quadrados para metros quadrados")
        print("5 - Retornar")

        opcao = input("Escolha uma opção: ")

        if opcao == "1":
            metros_quadrados_para_centimetros_quadrados()
        elif opcao == "2":
            centimetros_quadrados_para_metros_quadrados()
        elif opcao == "3":
            metros_quadrados_para_quilometros_quadrados()
        elif opcao == "4":
            quilometros_quadrados_para_metros_quadrados()
        elif opcao == "5":
            break
        else:
            print("Opção inválida. Tente novamente.")
```

Atenção: conversão de área não é igual à conversão de distância.

```text
1 metro = 100 centímetros
1 metro quadrado = 10.000 centímetros quadrados
```

Fórmulas:

```text
cm² = m² × 10000
m² = cm² / 10000
km² = m² / 1000000
m² = km² × 1000000
```

Funções que você deverá implementar:

```python
def metros_quadrados_para_centimetros_quadrados():
    # implemente aqui
    pass


def centimetros_quadrados_para_metros_quadrados():
    # implemente aqui
    pass


def metros_quadrados_para_quilometros_quadrados():
    # implemente aqui
    pass


def quilometros_quadrados_para_metros_quadrados():
    # implemente aqui
    pass
```

---

# Parte 5 — Menu de tempo

Crie a função `menu_tempo()`.

Ela deverá mostrar as opções:

1. Horas para minutos
2. Minutos para horas
3. Minutos para segundos
4. Segundos para minutos
5. Dias para horas
6. Horas para dias
7. Retornar ao menu de conversão de unidades

```python
def menu_tempo():
    while True:
        print("\n=== TEMPO ===")
        print("1 - Horas para minutos")
        print("2 - Minutos para horas")
        print("3 - Minutos para segundos")
        print("4 - Segundos para minutos")
        print("5 - Dias para horas")
        print("6 - Horas para dias")
        print("7 - Retornar")

        opcao = input("Escolha uma opção: ")

        if opcao == "1":
            horas_para_minutos()
        elif opcao == "2":
            minutos_para_horas()
        elif opcao == "3":
            minutos_para_segundos()
        elif opcao == "4":
            segundos_para_minutos()
        elif opcao == "5":
            dias_para_horas()
        elif opcao == "6":
            horas_para_dias()
        elif opcao == "7":
            break
        else:
            print("Opção inválida. Tente novamente.")
```

Fórmulas:

```text
minutos = horas × 60
horas = minutos / 60
segundos = minutos × 60
minutos = segundos / 60
horas = dias × 24
dias = horas / 24
```

Funções que você deverá implementar:

```python
def horas_para_minutos():
    # implemente aqui
    pass


def minutos_para_horas():
    # implemente aqui
    pass


def minutos_para_segundos():
    # implemente aqui
    pass


def segundos_para_minutos():
    # implemente aqui
    pass


def dias_para_horas():
    # implemente aqui
    pass


def horas_para_dias():
    # implemente aqui
    pass
```

---

# Parte 6 — Iniciando o programa

No final do arquivo, chame a função principal do conversor:

```python
menu_conversao_unidades()
```

---

# Estrutura final esperada

Seu código deverá seguir esta estrutura:

```python
def menu_conversao_unidades():
    pass


def menu_temperatura():
    pass


def celsius_para_fahrenheit():
    pass


def fahrenheit_para_celsius():
    pass


def celsius_para_kelvin():
    pass


def kelvin_para_celsius():
    pass


def menu_distancia():
    pass


def metros_para_centimetros():
    pass


def centimetros_para_metros():
    pass


def quilometros_para_metros():
    pass


def metros_para_quilometros():
    pass


def menu_area():
    pass


def metros_quadrados_para_centimetros_quadrados():
    pass


def centimetros_quadrados_para_metros_quadrados():
    pass


def metros_quadrados_para_quilometros_quadrados():
    pass


def quilometros_quadrados_para_metros_quadrados():
    pass


def menu_tempo():
    pass


def horas_para_minutos():
    pass


def minutos_para_horas():
    pass


def minutos_para_segundos():
    pass


def segundos_para_minutos():
    pass


def dias_para_horas():
    pass


def horas_para_dias():
    pass


menu_conversao_unidades()
```

---

# Regras da atividade

1. O menu inicial deve mostrar as categorias de conversão.
2. O menu inicial não deve fazer cálculos diretamente.
3. Cada opção do menu deve chamar uma função.
4. Cada categoria deve ter seu próprio submenu.
5. Cada submenu deve ter a opção de retornar.
6. Cada função de conversão deve pedir um valor ao usuário.
7. Cada função de conversão deve calcular e mostrar o resultado.
8. O programa deve encerrar apenas quando o usuário escolher a opção `Sair`.
9. Use nomes de funções claros.
10. Teste cada conversão separadamente.

---

# Exemplo de funcionamento esperado

```text
=== CONVERSÃO DE UNIDADES ===
1 - Temperatura
2 - Distância
3 - Área
4 - Tempo
5 - Sair

Escolha uma opção: 1

=== TEMPERATURA ===
1 - Celsius para Fahrenheit
2 - Fahrenheit para Celsius
3 - Celsius para Kelvin
4 - Kelvin para Celsius
5 - Retornar

Escolha uma opção: 1
Digite a temperatura em Celsius: 30
Resultado: 86.0 °F
```

---

# Desafio extra

Depois que terminar a atividade, adicione pelo menos **duas novas conversões** ao programa.

Sugestões:

* quilogramas para gramas;
* gramas para quilogramas;
* km/h para m/s;
* m/s para km/h;
* reais para dólares usando uma cotação digitada pelo usuário.

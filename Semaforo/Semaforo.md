# Aula: Semáforo em Python

## Primeira simulação no contexto de robótica

Nesta aula, vamos começar uma transição importante: sair de programas que apenas calculam ou mostram mensagens e entrar no pensamento da **robótica**.

Antes de usar Arduino, LEDs, sensores e botões reais, vamos simular tudo em Python. A ideia é entender a lógica de funcionamento de um sistema automatizado.

Um semáforo é um ótimo exemplo porque ele trabalha com:

* sequência;
* tempo;
* repetição;
* tomada de decisão;
* entrada e saída de informações.

Na robótica, quase sempre temos essa estrutura:

```text
Entrada → Processamento → Saída
```

No nosso caso:

```text
Botão do pedestre → Código em Python → Mensagens do semáforo
```

Mais tarde, quando usarmos Arduino, as mensagens do terminal poderão virar LEDs de verdade.

---

# 1. Objetivo da aula

Ao final da aula, o aluno deverá conseguir:

* entender o semáforo como um sistema automatizado;
* criar uma sequência de funcionamento usando Python;
* usar `time.sleep()` para controlar o tempo;
* usar `while` para repetir o sistema;
* usar `input()` para simular um botão;
* perceber a relação entre programação e robótica.

---

# 2. Conversa inicial

Comece perguntando para a turma:

> Na aula do código Morse, usamos pontos e traços para transmitir mensagens.
> O semáforo também transmite mensagens? Quais?

Espere respostas como:

```text
Verde = pode passar
Amarelo = atenção
Vermelho = pare
```

Depois explique:

> O semáforo é uma forma de comunicação visual.
> Ele usa luzes, tempo e sequência para controlar o trânsito.
> Hoje vamos simular essa lógica usando Python.

---

# 3. Primeiro código: semáforo simples

Peça para os alunos criarem um arquivo chamado:

```text
semaforo.py
```

Depois, escrevam o código:

```python
import time

print("🟢 VERDE - carros podem passar")
time.sleep(3)

print("🟡 AMARELO - atenção")
time.sleep(1)

print("🔴 VERMELHO - pare")
time.sleep(3)
```

Explique cada parte:

```python
import time
```

Importa uma biblioteca que permite trabalhar com tempo.

```python
time.sleep(3)
```

Faz o programa esperar 3 segundos antes de continuar.

---

# 4. Teste do programa

Execute o programa e pergunte:

> O que aconteceu?
> O semáforo funcionou apenas uma vez ou ficou repetindo?

A resposta esperada é:

```text
Funcionou apenas uma vez.
```

Então explique:

> Um semáforo real não funciona apenas uma vez.
> Ele precisa repetir o ciclo o tempo todo.

---

# 5. Segundo código: semáforo repetindo

Agora vamos usar `while True`.

```python
import time

while True:
    print("🟢 VERDE - carros podem passar")
    time.sleep(3)

    print("🟡 AMARELO - atenção")
    time.sleep(1)

    print("🔴 VERMELHO - pare")
    time.sleep(3)

    print("--------------------------")
```

Explique:

```python
while True:
```

Significa:

```text
Enquanto for verdadeiro, repita para sempre.
```

Ou seja, o semáforo fica funcionando continuamente.

---

# 6. Ajustando os tempos

Agora peça para os alunos modificarem os tempos.

Exemplo:

```python
import time

while True:
    print("🟢 VERDE - carros podem passar")
    time.sleep(5)

    print("🟡 AMARELO - atenção")
    time.sleep(2)

    print("🔴 VERMELHO - pare")
    time.sleep(4)

    print("--------------------------")
```

Perguntas para discussão:

> O que acontece se o amarelo ficar rápido demais?
> O que acontece se o vermelho ficar muito tempo ligado?
> Quem decide o tempo de cada sinal em uma cidade real?

Essa parte ajuda os alunos a perceberem que programação não é só escrever código. Também envolve pensar em regras do mundo real.

---

# 7. Melhorando o código com função

Agora mostre que podemos evitar repetição criando uma função.

```python
import time

def mostrar_sinal(cor, mensagem, tempo):
    print(f"{cor} {mensagem}")
    time.sleep(tempo)

while True:
    mostrar_sinal("🟢", "VERDE - carros podem passar", 3)
    mostrar_sinal("🟡", "AMARELO - atenção", 1)
    mostrar_sinal("🔴", "VERMELHO - pare", 3)
    print("--------------------------")
```

Explique:

```python
def mostrar_sinal(cor, mensagem, tempo):
```

Cria uma função que recebe três informações:

```text
cor
mensagem
tempo
```

Assim, em vez de escrever várias vezes `print()` e `time.sleep()`, usamos uma função.

---

# 8. Ligação com robótica

Explique para os alunos:

> Em um robô ou sistema automatizado, o código normalmente controla alguma saída física.

No Python, estamos fazendo:

```python
print("🟢 VERDE")
```

No Arduino, futuramente, poderemos fazer algo parecido com:

```cpp
digitalWrite(ledVerde, HIGH);
```

Ou seja:

```text
Python agora: mostra texto na tela.
Arduino depois: acende um LED.
```

A lógica é parecida. O que muda é a saída.

---

# 9. Terceiro código: botão de pedestre simulado

Agora vamos adicionar uma entrada.

Explique:

> Um sistema robótico geralmente recebe informações do ambiente.
> Pode ser por botão, sensor de distância, sensor de luz, câmera ou teclado.

Como ainda estamos sem Arduino, vamos simular o botão usando `input()`.

```python
import time

while True:
    print("🟢 VERDE - carros podem passar")

    resposta = input("Algum pedestre apertou o botão? (s/n): ")

    if resposta == "s":
        print("Pedido recebido. Aguarde...")

        time.sleep(1)

        print("🟡 AMARELO - atenção")
        time.sleep(2)

        print("🔴 VERMELHO - carros parados")
        print("🚶 Pedestre pode atravessar")
        time.sleep(5)

        print("Voltando ao fluxo normal...")

    else:
        print("Nenhum pedestre aguardando. Mantendo fluxo dos carros.")

    print("--------------------------")
```

---

# 10. Explicação do código

Explique esta linha:

```python
resposta = input("Algum pedestre apertou o botão? (s/n): ")
```

Ela simula um botão.

Quando o aluno digita `s`, é como se o pedestre tivesse apertado o botão.

Explique também:

```python
if resposta == "s":
```

Significa:

```text
Se a resposta for "s", execute o processo de travessia.
```

E:

```python
else:
```

Significa:

```text
Caso contrário, continue no funcionamento normal.
```

---

# 11. Conceito principal da aula

Mostre no quadro:

```text
Entrada:
O usuário digita "s" ou "n"

Processamento:
O Python verifica a resposta

Saída:
O programa mostra o sinal verde, amarelo ou vermelho
```

Depois relacione com robótica:

```text
Entrada:
Botão físico

Processamento:
Arduino executa o código

Saída:
LEDs do semáforo acendem
```

---

# 12. Desafio 1: contagem para o pedestre

Peça para os alunos melhorarem o código colocando uma contagem regressiva.

Código de apoio:

```python
import time

for numero in range(5, 0, -1):
    print(f"🚶 Pedestre pode atravessar: {numero}")
    time.sleep(1)
```

Depois, eles devem encaixar isso no lugar do `time.sleep(5)`.

Código completo com o desafio resolvido:

```python
import time

while True:
    print("🟢 VERDE - carros podem passar")

    resposta = input("Algum pedestre apertou o botão? (s/n): ")

    if resposta == "s":
        print("Pedido recebido. Aguarde...")
        time.sleep(1)

        print("🟡 AMARELO - atenção")
        time.sleep(2)

        print("🔴 VERMELHO - carros parados")

        for numero in range(5, 0, -1):
            print(f"🚶 Pedestre pode atravessar: {numero}")
            time.sleep(1)

        print("Voltando ao fluxo normal...")

    else:
        print("Nenhum pedestre aguardando. Mantendo fluxo dos carros.")

    print("--------------------------")
```

---

# 13. Desafio 2: semáforo de duas ruas

Agora proponha uma versão mais avançada:

```text
Rua A: verde
Rua B: vermelho
```

Depois:

```text
Rua A: amarelo
Rua B: vermelho
```

Depois:

```text
Rua A: vermelho
Rua B: verde
```

Código inicial:

```python
import time

while True:
    print("Rua A: 🟢 VERDE")
    print("Rua B: 🔴 VERMELHO")
    time.sleep(3)

    print("Rua A: 🟡 AMARELO")
    print("Rua B: 🔴 VERMELHO")
    time.sleep(1)

    print("Rua A: 🔴 VERMELHO")
    print("Rua B: 🟢 VERDE")
    time.sleep(3)

    print("Rua A: 🔴 VERMELHO")
    print("Rua B: 🟡 AMARELO")
    time.sleep(1)

    print("--------------------------")
```

Pergunte:

> Por que as duas ruas não podem ficar verdes ao mesmo tempo?

Essa pergunta é importante para discutir segurança e lógica de controle.

---

# 14. Fechamento da aula

Finalize com esta ideia:

> Hoje nós não usamos Arduino, LEDs ou sensores reais.
> Mas já começamos a pensar como um sistema de robótica funciona.

Mostre a estrutura:

```text
Código Morse:
mensagem → pontos e traços → sinal

Semáforo:
estado → tempo → sinal

Robótica:
entrada → processamento → saída
```

E conclua:

> Na próxima etapa, poderemos trocar os textos do terminal por LEDs reais.
> O que hoje aparece como “VERDE” na tela poderá acender um LED verde no Arduino.

---

# 15. Atividade para entrega

Peça para os alunos entregarem um arquivo `semaforo.py` com pelo menos uma das opções:

## Opção 1 — Básica

Semáforo automático com verde, amarelo e vermelho.

## Opção 2 — Intermediária

Semáforo com botão de pedestre usando `input()`.

## Opção 3 — Avançada

Semáforo de duas ruas, garantindo que as duas nunca fiquem verdes ao mesmo tempo.

Critérios de avaliação:

```text
1. O código executa sem erro.
2. O semáforo segue uma sequência lógica.
3. O aluno usou tempo com time.sleep().
4. O aluno conseguiu usar repetição.
5. O aluno compreendeu a relação com robótica.
```

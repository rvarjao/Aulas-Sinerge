# Aula: Código Morse com Python — Parte 1

## Conversor de texto para código Morse

## 1. Tema da aula

Nesta aula, vamos criar um programa em Python para converter mensagens de texto em **código Morse**.

O objetivo é entender como um computador pode transformar uma informação em outra forma de representação.

Nesta primeira parte, não usaremos som, LED ou componentes eletrônicos. Trabalharemos apenas com texto, lógica e troca de mensagens entre colegas.

---

## 2. Objetivos da aula

Ao final da aula, você deverá ser capaz de:

* Entender o que é código Morse.
* Criar uma tabela de conversão em Python.
* Usar um dicionário para relacionar letras e códigos.
* Percorrer uma mensagem letra por letra.
* Converter texto em pontos e traços.
* Enviar uma mensagem codificada para um colega.
* Decodificar uma mensagem recebida.
* Verificar se a comunicação ocorreu corretamente.

---

## 3. O que é código Morse?

O código Morse é uma forma de comunicação que representa letras e números usando sinais curtos e longos.

Usaremos:

```text
.  ponto
-  traço
```

Exemplo:

```text
S = ...
O = ---
SOS = ... --- ...
```

O código Morse foi muito usado em sistemas de comunicação à distância. Nesta aula, vamos usar essa ideia para estudar lógica computacional.

---

## 4. A missão da aula

Imagine que você precisa enviar uma mensagem secreta para outro estudante.

Mas existe uma regra: a mensagem não pode ser enviada em texto normal. Ela precisa ser enviada em código Morse.

Exemplo:

```text
Mensagem original:
ROBO

Mensagem em Morse:
.-. --- -... ---
```

Depois, outro estudante deverá receber o código e tentar descobrir qual era a mensagem original.

---

## 5. Criando o arquivo Python

Crie um arquivo chamado:

```text
morse.py
```

---

## 6. Criando a tabela Morse

Digite o código abaixo no arquivo:

```python
codigo_morse = {
    "A": ".-",
    "B": "-...",
    "C": "-.-.",
    "D": "-..",
    "E": ".",
    "F": "..-.",
    "G": "--.",
    "H": "....",
    "I": "..",
    "J": ".---",
    "K": "-.-",
    "L": ".-..",
    "M": "--",
    "N": "-.",
    "O": "---",
    "P": ".--.",
    "Q": "--.-",
    "R": ".-.",
    "S": "...",
    "T": "-",
    "U": "..-",
    "V": "...-",
    "W": ".--",
    "X": "-..-",
    "Y": "-.--",
    "Z": "--..",
    "0": "-----",
    "1": ".----",
    "2": "..---",
    "3": "...--",
    "4": "....-",
    "5": ".....",
    "6": "-....",
    "7": "--...",
    "8": "---..",
    "9": "----."
}
```

Essa estrutura é chamada de **dicionário**.

Ela funciona assim:

```python
"A": ".-"
```

Isso significa que a letra `A` será representada pelo código `.-`.

---

## 7. Recebendo uma mensagem do usuário

Agora vamos pedir para o usuário digitar uma mensagem.

Abaixo da tabela, escreva:

```python
mensagem = input("Digite uma mensagem: ")
mensagem = mensagem.upper()

print(mensagem)
```

Execute o programa e teste com:

```text
sos
```

O programa deverá mostrar:

```text
SOS
```

Usamos `.upper()` para transformar o texto em letras maiúsculas, porque nossa tabela Morse está com letras maiúsculas.

---

## 8. Percorrendo a mensagem letra por letra

Agora vamos usar um laço `for` para passar por cada letra da mensagem.

```python
mensagem = input("Digite uma mensagem: ")
mensagem = mensagem.upper()

for letra in mensagem:
    print(letra)
```

Teste com:

```text
CASA
```

Resultado esperado:

```text
C
A
S
A
```

Neste momento, o programa ainda não converteu para Morse. Ele apenas separou a palavra em letras.

---

## 9. Convertendo cada letra para Morse

Agora vamos buscar cada letra dentro do dicionário `codigo_morse`.

```python
mensagem = input("Digite uma mensagem: ")
mensagem = mensagem.upper()

for letra in mensagem:
    codigo = codigo_morse[letra]
    print(letra, "=", codigo)
```

Teste com:

```text
SOS
```

Resultado esperado:

```text
S = ...
O = ---
S = ...
```

---

## 10. Montando a mensagem completa em Morse

Agora vamos juntar todos os códigos em uma única variável.

```python
mensagem = input("Digite uma mensagem: ")
mensagem = mensagem.upper()

mensagem_morse = ""

for letra in mensagem:
    codigo = codigo_morse[letra]
    mensagem_morse = mensagem_morse + codigo + " "

print("Mensagem em Morse:")
print(mensagem_morse)
```

Teste com:

```text
ROBO
```

Resultado esperado:

```text
Mensagem em Morse:
.-. --- -... ---
```

---

## 11. Tratando espaços entre palavras

Se digitarmos uma frase com espaço, o programa pode apresentar erro, pois o espaço não está na tabela.

Vamos resolver isso usando `/` para representar a separação entre palavras.

```python
mensagem = input("Digite uma mensagem: ")
mensagem = mensagem.upper()

mensagem_morse = ""

for letra in mensagem:
    if letra == " ":
        mensagem_morse = mensagem_morse + "/ "
    else:
        codigo = codigo_morse[letra]
        mensagem_morse = mensagem_morse + codigo + " "

print("Mensagem em Morse:")
print(mensagem_morse)
```

Teste com:

```text
OI TURMA
```

Resultado esperado:

```text
Mensagem em Morse:
--- .. / - ..- .-. -- .-
```

---

## 12. Evitando erro com caracteres desconhecidos

Se o usuário digitar acentos, vírgulas ou outros símbolos, o programa pode dar erro.

Vamos melhorar o código para tratar caracteres desconhecidos.

```python
mensagem = input("Digite uma mensagem: ")
mensagem = mensagem.upper()

mensagem_morse = ""

for letra in mensagem:
    if letra == " ":
        mensagem_morse = mensagem_morse + "/ "
    elif letra in codigo_morse:
        codigo = codigo_morse[letra]
        mensagem_morse = mensagem_morse + codigo + " "
    else:
        mensagem_morse = mensagem_morse + "? "

print("Mensagem em Morse:")
print(mensagem_morse)
```

Agora, se o programa encontrar um caractere que não conhece, ele colocará `?`.

Exemplo:

```text
Mensagem:
OLÁ

Resultado:
--- .-.. ?
```

---

## 13. Organizando o programa com função

Agora vamos organizar a conversão em uma função chamada `converter_para_morse`.

```python
def converter_para_morse(texto):
    texto = texto.upper()
    mensagem_morse = ""

    for letra in texto:
        if letra == " ":
            mensagem_morse = mensagem_morse + "/ "
        elif letra in codigo_morse:
            codigo = codigo_morse[letra]
            mensagem_morse = mensagem_morse + codigo + " "
        else:
            mensagem_morse = mensagem_morse + "? "

    return mensagem_morse
```

Depois, usamos a função assim:

```python
mensagem = input("Digite uma mensagem: ")
resultado = converter_para_morse(mensagem)

print("Mensagem em Morse:")
print(resultado)
```

---

## 14. Código completo da Aula 1

```python
codigo_morse = {
    "A": ".-",
    "B": "-...",
    "C": "-.-.",
    "D": "-..",
    "E": ".",
    "F": "..-.",
    "G": "--.",
    "H": "....",
    "I": "..",
    "J": ".---",
    "K": "-.-",
    "L": ".-..",
    "M": "--",
    "N": "-.",
    "O": "---",
    "P": ".--.",
    "Q": "--.-",
    "R": ".-.",
    "S": "...",
    "T": "-",
    "U": "..-",
    "V": "...-",
    "W": ".--",
    "X": "-..-",
    "Y": "-.--",
    "Z": "--..",
    "0": "-----",
    "1": ".----",
    "2": "..---",
    "3": "...--",
    "4": "....-",
    "5": ".....",
    "6": "-....",
    "7": "--...",
    "8": "---..",
    "9": "----."
}


def converter_para_morse(texto):
    texto = texto.upper()
    mensagem_morse = ""

    for letra in texto:
        if letra == " ":
            mensagem_morse = mensagem_morse + "/ "
        elif letra in codigo_morse:
            codigo = codigo_morse[letra]
            mensagem_morse = mensagem_morse + codigo + " "
        else:
            mensagem_morse = mensagem_morse + "? "

    return mensagem_morse


mensagem = input("Digite uma mensagem: ")
resultado = converter_para_morse(mensagem)

print("Mensagem em Morse:")
print(resultado)
```

---

# Atividade prática da Aula 1

## 15. Enviando uma mensagem secreta para um colega

Agora você deverá criar uma mensagem curta e convertê-la para código Morse.

A mensagem pode ser uma palavra ou frase simples.

Exemplos:

```text
ROBO
PYTHON
OI TURMA
AULA DE ROBOTICA
ESCOLA
```

Evite usar acentos, vírgulas ou pontuação.

Use apenas:

```text
letras
números
espaços
```

---

## 16. Passo a passo da atividade

### Etapa 1 — Escreva a mensagem original

Escolha uma mensagem.

Exemplo:

```text
AULA DE ROBO
```

---

### Etapa 2 — Converta usando o programa

Execute o programa e digite sua mensagem.

Exemplo de resultado:

```text
.- ..- .-.. .- / -.. . / .-. --- -... ---
```

---

### Etapa 3 — Envie apenas o código Morse por e-mail

Envie um e-mail para um colega contendo apenas:

* Seu nome.
* A mensagem em código Morse.
* Uma pergunta pedindo para ele tentar decodificar.

Não envie a mensagem original.

Modelo de e-mail:

```text
Assunto: Desafio de Código Morse

Olá!

Esta é minha mensagem em código Morse:

.- ..- .-.. .- / -.. . / .-. --- -... ---

Tente descobrir qual foi a mensagem original.

Depois me responda dizendo o que você entendeu.
```

---

### Etapa 4 — Receba o código de outro colega

Quando você receber uma mensagem em Morse, tente decodificar manualmente usando a tabela Morse.

Você também poderá criar uma função no Python para ajudar na decodificação, se quiser fazer o desafio extra.

---

### Etapa 5 — Verifique se a comunicação deu certo

Depois que o colega responder, compare:

```text
Mensagem original
Mensagem em Morse enviada
Mensagem decodificada pelo colega
```

Responda:

```text
A comunicação ocorreu corretamente?
Houve algum erro?
O erro foi na conversão, no envio ou na leitura?
Como poderíamos melhorar?
```

---

## 17. Registro da atividade

No final, cada estudante deve registrar:

```text
Minha mensagem original:
Mensagem em Morse enviada:
Colega que recebeu:
Mensagem que o colega entendeu:
Deu certo? Sim ou não?
O que poderia melhorar?
```

---

## 18. Perguntas para reflexão

Responda no caderno ou em um arquivo de texto:

1. O que o programa recebe como entrada?
2. O que o programa produz como saída?
3. Para que serve o dicionário `codigo_morse`?
4. Por que usamos o laço `for`?
5. Para que usamos o `if`?
6. O que acontece quando aparece um espaço na mensagem?
7. O que acontece quando aparece um caractere desconhecido?
8. O que poderia dar errado na comunicação por e-mail?
9. Como saber se a mensagem foi recebida corretamente?
10. Como essa atividade se relaciona com robótica?

---

# Desafio extra da Aula 1

## 19. Criando um decodificador de Morse

Agora tente criar uma função que faça o caminho contrário:

```text
Código Morse → Texto
```

Exemplo:

```text
Entrada:
... --- ...

Saída:
SOS
```

Dica: você precisará criar uma tabela invertida.

Exemplo:

```python
morse_para_texto = {
    "...": "S",
    "---": "O"
}
```

Uma forma automática de criar essa tabela é:

```python
morse_para_texto = {}

for letra in codigo_morse:
    codigo = codigo_morse[letra]
    morse_para_texto[codigo] = letra
```

Depois, você precisará separar a mensagem Morse em partes usando `.split()`.

Exemplo:

```python
mensagem_morse = "... --- ..."
partes = mensagem_morse.split()

print(partes)
```

Resultado:

```text
['...', '---', '...']
```

---

# Aula: Código Morse com Python — Parte 2

## Decodificação, som e preparação para robótica

## 1. Tema da aula

Na aula anterior, criamos um programa para converter texto em código Morse.

Nesta segunda aula, vamos avançar em duas direções:

1. Criar um programa para decodificar Morse de volta para texto.
2. Discutir como essa lógica pode virar uma atividade de robótica com som, LED ou buzzer.

A parte de som pode ser feita depois, caso os computadores permitam instalar bibliotecas.

---

## 2. Objetivos da Aula 2

Ao final desta aula, você deverá ser capaz de:

* Criar uma tabela Morse invertida.
* Converter código Morse em texto.
* Entender o processo de codificação e decodificação.
* Comparar mensagem enviada e mensagem recebida.
* Identificar erros de comunicação.
* Relacionar o projeto com robótica.
* Planejar uma versão com LED, buzzer ou botão.

---

## 3. Relembrando a Aula 1

Na Aula 1, fizemos isto:

```text
Texto → Código Morse
```

Exemplo:

```text
ROBO → .-. --- -... ---
```

Agora vamos fazer o contrário:

```text
Código Morse → Texto
```

Exemplo:

```text
.-. --- -... --- → ROBO
```

---

## 4. Criando a tabela invertida

Já temos esta tabela:

```python
codigo_morse = {
    "A": ".-",
    "B": "-...",
    "C": "-.-.",
    "D": "-..",
    "E": ".",
    "F": "..-.",
    "G": "--.",
    "H": "....",
    "I": "..",
    "J": ".---",
    "K": "-.-",
    "L": ".-..",
    "M": "--",
    "N": "-.",
    "O": "---",
    "P": ".--.",
    "Q": "--.-",
    "R": ".-.",
    "S": "...",
    "T": "-",
    "U": "..-",
    "V": "...-",
    "W": ".--",
    "X": "-..-",
    "Y": "-.--",
    "Z": "--..",
    "0": "-----",
    "1": ".----",
    "2": "..---",
    "3": "...--",
    "4": "....-",
    "5": ".....",
    "6": "-....",
    "7": "--...",
    "8": "---..",
    "9": "----."
}
```

Agora vamos criar uma nova tabela, invertendo chave e valor.

```python
morse_para_texto = {}

for letra in codigo_morse:
    codigo = codigo_morse[letra]
    morse_para_texto[codigo] = letra

print(morse_para_texto)
```

Na primeira tabela:

```text
A → .-
```

Na tabela invertida:

```text
.- → A
```

---

## 5. Separando uma mensagem Morse

Uma mensagem Morse usa espaços entre letras.

Exemplo:

```text
... --- ...
```

Podemos separar essa mensagem usando `.split()`.

```python
mensagem_morse = input("Digite a mensagem em Morse: ")

partes = mensagem_morse.split()

print(partes)
```

Teste com:

```text
... --- ...
```

Resultado esperado:

```text
['...', '---', '...']
```

---

## 6. Decodificando cada parte

Agora vamos converter cada código para uma letra.

```python
mensagem_morse = input("Digite a mensagem em Morse: ")

partes = mensagem_morse.split()

mensagem_texto = ""

for codigo in partes:
    letra = morse_para_texto[codigo]
    mensagem_texto = mensagem_texto + letra

print("Mensagem decodificada:")
print(mensagem_texto)
```

Teste com:

```text
... --- ...
```

Resultado esperado:

```text
Mensagem decodificada:
SOS
```

---

## 7. Tratando separação entre palavras

Na aula anterior, usamos `/` para separar palavras.

Exemplo:

```text
--- .. / - ..- .-. -- .-
```

Isso significa:

```text
OI TURMA
```

Vamos tratar o `/` como espaço.

```python
mensagem_morse = input("Digite a mensagem em Morse: ")

partes = mensagem_morse.split()

mensagem_texto = ""

for codigo in partes:
    if codigo == "/":
        mensagem_texto = mensagem_texto + " "
    elif codigo in morse_para_texto:
        letra = morse_para_texto[codigo]
        mensagem_texto = mensagem_texto + letra
    else:
        mensagem_texto = mensagem_texto + "?"

print("Mensagem decodificada:")
print(mensagem_texto)
```

---

## 8. Criando uma função para decodificar

Agora vamos organizar o código em uma função.

```python
def decodificar_morse(mensagem_morse):
    partes = mensagem_morse.split()
    mensagem_texto = ""

    for codigo in partes:
        if codigo == "/":
            mensagem_texto = mensagem_texto + " "
        elif codigo in morse_para_texto:
            letra = morse_para_texto[codigo]
            mensagem_texto = mensagem_texto + letra
        else:
            mensagem_texto = mensagem_texto + "?"

    return mensagem_texto
```

Agora podemos usar assim:

```python
mensagem_recebida = input("Digite a mensagem em Morse recebida: ")
resultado = decodificar_morse(mensagem_recebida)

print("Mensagem decodificada:")
print(resultado)
```

---

## 9. Código completo da Aula 2 sem som

```python
codigo_morse = {
    "A": ".-",
    "B": "-...",
    "C": "-.-.",
    "D": "-..",
    "E": ".",
    "F": "..-.",
    "G": "--.",
    "H": "....",
    "I": "..",
    "J": ".---",
    "K": "-.-",
    "L": ".-..",
    "M": "--",
    "N": "-.",
    "O": "---",
    "P": ".--.",
    "Q": "--.-",
    "R": ".-.",
    "S": "...",
    "T": "-",
    "U": "..-",
    "V": "...-",
    "W": ".--",
    "X": "-..-",
    "Y": "-.--",
    "Z": "--..",
    "0": "-----",
    "1": ".----",
    "2": "..---",
    "3": "...--",
    "4": "....-",
    "5": ".....",
    "6": "-....",
    "7": "--...",
    "8": "---..",
    "9": "----."
}


def converter_para_morse(texto):
    texto = texto.upper()
    mensagem_morse = ""

    for letra in texto:
        if letra == " ":
            mensagem_morse = mensagem_morse + "/ "
        elif letra in codigo_morse:
            codigo = codigo_morse[letra]
            mensagem_morse = mensagem_morse + codigo + " "
        else:
            mensagem_morse = mensagem_morse + "? "

    return mensagem_morse


morse_para_texto = {}

for letra in codigo_morse:
    codigo = codigo_morse[letra]
    morse_para_texto[codigo] = letra


def decodificar_morse(mensagem_morse):
    partes = mensagem_morse.split()
    mensagem_texto = ""

    for codigo in partes:
        if codigo == "/":
            mensagem_texto = mensagem_texto + " "
        elif codigo in morse_para_texto:
            letra = morse_para_texto[codigo]
            mensagem_texto = mensagem_texto + letra
        else:
            mensagem_texto = mensagem_texto + "?"

    return mensagem_texto


print("=== Conversor de Código Morse ===")
print("1 - Converter texto para Morse")
print("2 - Decodificar Morse para texto")

opcao = input("Escolha uma opção: ")

if opcao == "1":
    mensagem = input("Digite a mensagem original: ")
    resultado = converter_para_morse(mensagem)

    print("Mensagem em Morse:")
    print(resultado)

elif opcao == "2":
    mensagem = input("Digite a mensagem em Morse: ")
    resultado = decodificar_morse(mensagem)

    print("Mensagem decodificada:")
    print(resultado)

else:
    print("Opção inválida.")
```

---

# Atividade prática da Aula 2

## 10. Verificando as mensagens recebidas

Cada estudante deve pegar a mensagem Morse recebida por e-mail na aula anterior e tentar decodificar usando o programa.

Depois, deve responder ao colega dizendo qual mensagem entendeu.

Modelo de resposta:

```text
Olá!

Recebi sua mensagem em código Morse.

Mensagem que eu decodifiquei:
AULA DE ROBO

Deu certo?
```

---

## 11. Conferência entre remetente e receptor

Depois que o colega responder, compare:

```text
Mensagem original:
Mensagem Morse enviada:
Mensagem decodificada pelo colega:
```

Responda:

```text
A mensagem chegou corretamente?
Houve diferença entre a mensagem original e a mensagem recebida?
Se houve erro, onde ele pode ter acontecido?
```

Possíveis erros:

```text
Erro ao digitar a mensagem original
Erro na conversão
Erro ao copiar o código Morse
Erro ao enviar por e-mail
Erro ao decodificar
Erro por falta de espaço entre letras
Erro por uso de acentos ou símbolos
```

---

## 12. Discussão: o que isso tem a ver com robótica?

Na robótica, muitas vezes precisamos transformar uma informação em ação.

Nesta atividade:

```text
Texto → Código Morse
Código Morse → Texto
```

Em uma próxima versão, poderemos fazer:

```text
Texto → Código Morse → LED piscando
Texto → Código Morse → Buzzer tocando
Botão pressionado → Ponto ou traço → Texto
```

Isso mostra que a lógica criada no Python pode ser aproveitada depois em projetos físicos.

---

## 13. Planejamento para a próxima etapa com robótica

Pense em como o código poderia controlar componentes físicos.

### Com LED

```text
ponto = LED acende por pouco tempo
traço = LED acende por mais tempo
```

### Com buzzer

```text
ponto = som curto
traço = som longo
```

### Com botão

```text
pressionar rapidamente = ponto
pressionar por mais tempo = traço
```

---

## 14. Perguntas para reflexão

1. O que significa codificar uma mensagem?
2. O que significa decodificar uma mensagem?
3. O que acontece se esquecermos um espaço entre os códigos?
4. Por que usamos `/` para separar palavras?
5. Qual foi a maior dificuldade da atividade?
6. A comunicação por e-mail funcionou corretamente?
7. Como poderíamos evitar erros de cópia?
8. Como esse projeto poderia virar um projeto com Arduino?
9. Como um LED poderia representar pontos e traços?
10. Como um botão poderia ser usado para enviar uma mensagem?

---

# Sugestão de Aula 3 ou continuação prática

Em uma próxima aula, podemos criar uma versão com saída física ou sonora.

## Opção A — Sem instalar bibliotecas

Usar apenas texto no terminal:

```text
ponto = pisca curto
traço = pisca longo
```

O programa pode mostrar:

```text
PONTO
TRAÇO
PONTO
```

## Opção B — Com som no computador

Usar uma biblioteca de som para tocar beeps curtos e longos.

## Opção C — Com Arduino

Usar LED ou buzzer.

```text
Python ensinou a lógica.
Arduino executa a ação física.
```

---

# Conclusão

Nesta sequência de aulas, aprendemos que comunicação envolve:

```text
mensagem original
codificação
envio
recebimento
decodificação
verificação
```

Esse processo aparece em várias áreas da computação e da robótica.

Quando programamos um robô, também precisamos transformar informações em comandos claros para que a máquina consiga agir corretamente.

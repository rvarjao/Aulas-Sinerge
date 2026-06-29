# Atividade: Robô desenhista do campo de futebol

## Contexto

Você foi contratado para programar um robô que pinta automaticamente as linhas de um campo de futebol.

Esse robô não sabe o que é um campo. Ele apenas segue comandos.

Sua missão é completar o algoritmo para que o robô desenhe as linhas principais do campo.

---

## Objetivo da atividade

Criar um programa em Python que use comandos de movimento para desenhar um campo de futebol visto de cima.

Nesta atividade, você vai praticar:

* sequência de comandos;
* coordenadas no plano cartesiano;
* funções;
* decomposição de problemas;
* desenho com pontos, linhas e arcos;
* raciocínio lógico;
* proporção e escala.

---

## Medidas usadas na atividade

Vamos usar um campo com medidas próximas das usadas em competições profissionais:

```text
Comprimento: 105 metros
Largura: 68 metros
```

No programa, você vai trabalhar com **metros**.

A conversão para pixels será feita automaticamente pelo código.

```text
1 metro = 6 pixels
```

Portanto, quando você escrever:

```python
ir_para(10, 5)
```

o robô entende que deve ir para:

```text
x = 10 metros
y = 5 metros
```

Internamente, o programa converte isso para pixels.

---

## Plano cartesiano do campo

O centro do campo será a posição:

```text
(0, 0)
```

Como o campo tem 105 metros de comprimento e 68 metros de largura:

```text
Metade do comprimento: 52,5 metros
Metade da largura: 34 metros
```

Então os cantos do campo serão:

```text
Canto superior esquerdo:  (-52.5, 34)
Canto superior direito:   (52.5, 34)
Canto inferior direito:   (52.5, -34)
Canto inferior esquerdo:  (-52.5, -34)
```

Representação:

```text
(-52.5, 34) ---------------------- (52.5, 34)
      |                                |
      |                                |
      |                                |
(-52.5,-34) ---------------------- (52.5,-34)
```

Lembre-se:

```text
x controla esquerda e direita
y controla cima e baixo
```

---

## Medidas principais do campo

| Elemento                    |          Medida real |
| --------------------------- | -------------------: |
| Comprimento do campo        |                105 m |
| Largura do campo            |                 68 m |
| Grande área — profundidade  |               16,5 m |
| Grande área — largura       |              40,32 m |
| Pequena área — profundidade |                5,5 m |
| Pequena área — largura      |              18,32 m |
| Marca do pênalti            | 11 m da linha do gol |
| Círculo central             |       raio de 9,15 m |
| Meia-lua da área            |       raio de 9,15 m |
| Gol                         |    largura de 7,32 m |

---

## Pontos principais do campo

### Campo

```text
Esquerda: -52.5
Direita: 52.5
Topo: 34
Baixo: -34
```

---

### Linha do meio

A linha do meio fica em:

```text
x = 0
```

Ela vai de:

```text
(0, 34)
```

até:

```text
(0, -34)
```

---

### Círculo central

Centro:

```text
(0, 0)
```

Raio:

```text
9.15 metros
```

Para usar o comando `circulo(9.15)`, comece em:

```text
(0, -9.15)
```

---

### Grande área esquerda

A grande área tem:

```text
Profundidade: 16.5 m
Largura: 40.32 m
```

No lado esquerdo, ela vai de:

```text
x = -52.5 até x = -36
```

Como a largura é 40,32 m, metade é 20,16 m.

Pontos:

```text
(-52.5, 20.16)
(-36, 20.16)
(-36, -20.16)
(-52.5, -20.16)
```

---

### Grande área direita

Pontos:

```text
(52.5, 20.16)
(36, 20.16)
(36, -20.16)
(52.5, -20.16)
```

---

### Pequena área esquerda

A pequena área tem:

```text
Profundidade: 5.5 m
Largura: 18.32 m
```

No lado esquerdo, ela vai de:

```text
x = -52.5 até x = -47
```

Como a largura é 18,32 m, metade é 9,16 m.

Pontos:

```text
(-52.5, 9.16)
(-47, 9.16)
(-47, -9.16)
(-52.5, -9.16)
```

---

### Pequena área direita

Pontos:

```text
(52.5, 9.16)
(47, 9.16)
(47, -9.16)
(52.5, -9.16)
```

---

### Marcas do pênalti

A marca do pênalti fica a 11 metros da linha do gol.

Marca esquerda:

```text
(-41.5, 0)
```

Marca direita:

```text
(41.5, 0)
```

---

## Sobre a meia-lua da grande área

A meia-lua da grande área não é um semicírculo completo.

Ela é apenas uma parte de um círculo cujo centro é a marca do pênalti.

A meia-lua possui raio de:

```text
9.15 metros
```

Para a meia-lua esquerda, usamos:

```python
arco_centralizado(-41.5, 0, 9.15, -53, 53)
```

Para a meia-lua direita, usamos:

```python
arco_centralizado(41.5, 0, 9.15, 127, 233)
```

Os ângulos funcionam assim:

```text
0 graus   = direita
90 graus  = cima
180 graus = esquerda
270 graus = baixo
```

---

# Código-base

Copie o código abaixo e complete apenas as funções indicadas.

```python
import turtle
import math

# ==============================
# Configuração da tela
# ==============================

tela = turtle.Screen()
tela.title("Robô desenhista do campo de futebol")
tela.bgcolor("green")
tela.setup(width=900, height=650)

# ==============================
# Configuração do robô
# ==============================

robo = turtle.Turtle()
robo.shape("turtle")
robo.color("white")
robo.pensize(3)
robo.speed(4)

# ==============================
# Escala do desenho
# ==============================

# Nesta atividade:
# 1 metro no campo real será representado por 6 pixels na tela.
PIXELS_POR_METRO = 6

def metros_para_pixels(metros):
    return metros * PIXELS_POR_METRO

# ==============================
# Comandos do robô
# ==============================
# Atenção:
# Todas as funções abaixo recebem valores em METROS.
# A conversão para pixels acontece internamente.
# ==============================

def ir_para(x_metros, y_metros):
    x_pixels = metros_para_pixels(x_metros)
    y_pixels = metros_para_pixels(y_metros)

    robo.penup()
    robo.goto(x_pixels, y_pixels)

def caneta_baixar():
    robo.pendown()

def caneta_levantar():
    robo.penup()

def frente(distancia_metros):
    distancia_pixels = metros_para_pixels(distancia_metros)
    robo.forward(distancia_pixels)

def tras(distancia_metros):
    distancia_pixels = metros_para_pixels(distancia_metros)
    robo.backward(distancia_pixels)

def direita(graus):
    robo.right(graus)

def esquerda(graus):
    robo.left(graus)

def olhar_para(graus):
    robo.setheading(graus)

def circulo(raio_metros):
    raio_pixels = metros_para_pixels(raio_metros)
    robo.circle(raio_pixels)

def ponto(tamanho_metros=0.8):
    tamanho_pixels = metros_para_pixels(tamanho_metros)
    robo.dot(tamanho_pixels)

def arco_centralizado(x_metros, y_metros, raio_metros, angulo_inicial, angulo_final):
    """
    Desenha um arco de círculo.

    x_metros, y_metros: centro do círculo, em metros
    raio_metros: raio do círculo, em metros
    angulo_inicial: onde o arco começa
    angulo_final: onde o arco termina

    Ângulos:
    0 graus   = direita
    90 graus  = cima
    180 graus = esquerda
    270 graus = baixo
    """

    caneta_levantar()

    primeiro_ponto = True

    for angulo in range(angulo_inicial, angulo_final + 1):
        radianos = math.radians(angulo)

        ponto_x_metros = x_metros + raio_metros * math.cos(radianos)
        ponto_y_metros = y_metros + raio_metros * math.sin(radianos)

        ponto_x_pixels = metros_para_pixels(ponto_x_metros)
        ponto_y_pixels = metros_para_pixels(ponto_y_metros)

        if primeiro_ponto:
            robo.penup()
            robo.goto(ponto_x_pixels, ponto_y_pixels)
            robo.pendown()
            primeiro_ponto = False
        else:
            robo.goto(ponto_x_pixels, ponto_y_pixels)

    caneta_levantar()

# ==============================
# Funções que os alunos devem completar
# ==============================

def desenhar_contorno():
    # Complete aqui:
    # O campo vai de (-52.5, 34) até (52.5, -34)
    #
    # Pontos:
    # (-52.5, 34)
    # (52.5, 34)
    # (52.5, -34)
    # (-52.5, -34)
    pass


def desenhar_linha_do_meio():
    # Complete aqui:
    # A linha do meio fica em x = 0
    #
    # Vai de:
    # (0, 34)
    # até:
    # (0, -34)
    pass


def desenhar_circulo_central():
    # Complete aqui:
    # O centro do campo é (0, 0)
    # Raio do círculo central: 9.15 metros
    #
    # Dica:
    # para desenhar um círculo de raio 9.15 centralizado,
    # comece em (0, -9.15)
    pass


def desenhar_grande_area_esquerda():
    # Complete aqui:
    # Pontos sugeridos:
    # (-52.5, 20.16)
    # (-36, 20.16)
    # (-36, -20.16)
    # (-52.5, -20.16)
    pass


def desenhar_grande_area_direita():
    # Complete aqui:
    # Pontos sugeridos:
    # (52.5, 20.16)
    # (36, 20.16)
    # (36, -20.16)
    # (52.5, -20.16)
    pass


def desenhar_pequena_area_esquerda():
    # Complete aqui:
    # Pontos sugeridos:
    # (-52.5, 9.16)
    # (-47, 9.16)
    # (-47, -9.16)
    # (-52.5, -9.16)
    pass


def desenhar_pequena_area_direita():
    # Complete aqui:
    # Pontos sugeridos:
    # (52.5, 9.16)
    # (47, 9.16)
    # (47, -9.16)
    # (52.5, -9.16)
    pass


def desenhar_marcas_penalti():
    # Complete aqui:
    # Pênalti esquerdo: (-41.5, 0)
    # Pênalti direito:  (41.5, 0)
    pass


def desenhar_meia_lua_esquerda():
    # Complete aqui:
    # A meia-lua esquerda tem centro na marca do pênalti esquerdo.
    #
    # Centro: (-41.5, 0)
    # Raio: 9.15
    # Ângulo inicial: -53
    # Ângulo final: 53
    #
    # Dica:
    # arco_centralizado(-41.5, 0, 9.15, -53, 53)
    pass


def desenhar_meia_lua_direita():
    # Complete aqui:
    # A meia-lua direita tem centro na marca do pênalti direito.
    #
    # Centro: (41.5, 0)
    # Raio: 9.15
    # Ângulo inicial: 127
    # Ângulo final: 233
    #
    # Dica:
    # arco_centralizado(41.5, 0, 9.15, 127, 233)
    pass


def desenhar_gol_esquerdo():
    # Desafio extra:
    # O gol tem aproximadamente 7.32 metros de largura.
    # Vamos desenhar o gol para fora do campo.
    #
    # Pontos sugeridos:
    # (-52.5, 3.66)
    # (-57.5, 3.66)
    # (-57.5, -3.66)
    # (-52.5, -3.66)
    pass


def desenhar_gol_direito():
    # Desafio extra:
    # Pontos sugeridos:
    # (52.5, 3.66)
    # (57.5, 3.66)
    # (57.5, -3.66)
    # (52.5, -3.66)
    pass


# ==============================
# Código principal
# ==============================
# As chamadas já estão prontas.
# O robô vai executar as funções na ordem abaixo.
# O trabalho de vocês é completar cada função acima.
# ==============================

desenhar_contorno()
desenhar_linha_do_meio()
desenhar_circulo_central()

desenhar_grande_area_esquerda()
desenhar_grande_area_direita()

desenhar_pequena_area_esquerda()
desenhar_pequena_area_direita()

desenhar_marcas_penalti()

desenhar_meia_lua_esquerda()
desenhar_meia_lua_direita()

# Desafio extra:
desenhar_gol_esquerdo()
desenhar_gol_direito()

turtle.done()
```

---

# Dicas para resolver

## Contorno do campo

Use:

```python
ir_para(-52.5, 34)
caneta_baixar()
ir_para(52.5, 34)
ir_para(52.5, -34)
ir_para(-52.5, -34)
ir_para(-52.5, 34)
caneta_levantar()
```


---

# Perguntas para pensar

1. O robô entende o que é um campo de futebol?
2. O que acontece se uma coordenada estiver errada?
3. Por que usamos funções?
4. O que significa trabalhar com escala?
5. Por que o programa usa metros, mas a tela usa pixels?
6. Por que a meia-lua não é um semicírculo completo?
7. Quais partes do campo são simétricas?

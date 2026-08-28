# Projeto Interdisciplinar — Desenvolvimento de Sistemas + Ciências

## Objetivo

Vocês deverão criar a proposta de um sistema que una **desenvolvimento de software** com algum conceito de **Ciências da Natureza**.

O projeto pode utilizar conteúdos de:

- Física;
- Química;
- Biologia;
- ou uma combinação dessas áreas.

O sistema deverá possuir, obrigatoriamente:

- **Front-end** — interface utilizada pelo usuário;
- **Back-end** — regras e processamento do sistema;
- **Banco de dados** — armazenamento das informações;
- **Um conceito científico real** que faça parte do funcionamento do sistema.

O objetivo não é apenas criar um sistema "sobre Ciências". O conceito científico deve participar de alguma forma do funcionamento da aplicação.

---

# Etapa 1 — Conhecer um exemplo

Em sala, vamos conhecer o jogo **Corrida de Vetores**.

Nesse jogo, a posição de um veículo depende de sua velocidade e de sua aceleração.

Exemplo:

Velocidade atual:

`v = (3, 1)`

Aceleração escolhida:

`a = (-1, 1)`

Nova velocidade:

`v = (2, 2)`

O jogo utiliza, portanto, conceitos de:

- vetores;
- posição;
- velocidade;
- aceleração;
- movimento.

Percebam que não é apenas um jogo com aparência relacionada à Física.

**A Física faz parte da lógica do programa.**

Esse é o princípio que vocês deverão utilizar no projeto de vocês.

---

# Etapa 2 — Formar o grupo

Organizem-se nos grupos definidos para o projeto.

Todos os integrantes deverão participar de:

- pesquisa;
- planejamento;
- modelagem;
- desenvolvimento;
- apresentação.

É permitido dividir responsabilidades, mas todos devem compreender o funcionamento geral do projeto.

---

# Etapa 3 — Escolher uma área científica

Escolham inicialmente uma área:

### Física

Alguns exemplos:

- movimento;
- velocidade e aceleração;
- gravidade;
- lançamento de projéteis;
- eletricidade;
- consumo de energia;
- óptica;
- ondas;
- temperatura;
- pressão;
- astronomia.

### Química

Alguns exemplos:

- tabela periódica;
- reações químicas;
- pH;
- concentração;
- soluções;
- balanceamento de equações;
- propriedades dos elementos;
- misturas;
- estequiometria;
- gases.

### Biologia

Alguns exemplos:

- genética;
- ecologia;
- cadeia alimentar;
- evolução;
- anatomia;
- sistema circulatório;
- epidemias;
- reprodução;
- classificação dos seres vivos;
- população e ecossistemas.

Vocês não são obrigados a utilizar esses exemplos.

Podem pesquisar outros conteúdos.

---

# Etapa 4 — Pesquisar possibilidades

Antes de decidir o projeto, o grupo deverá pesquisar sistemas, jogos, simuladores ou aplicações que utilizem conceitos científicos.

Pesquisem perguntas como:

- Que fenômeno científico poderia ser simulado?
- Que problema poderia ser resolvido com um sistema?
- Que informações poderiam ser armazenadas?
- O usuário poderia fazer experimentos?
- Poderia existir um jogo?
- Poderia existir uma simulação?
- O sistema poderia fazer cálculos?
- Poderia comparar resultados?
- Poderia registrar experiências anteriores?

Anotem pelo menos **três ideias diferentes** antes de escolher a definitiva.

---

# Etapa 5 — Escolher o projeto

Depois da pesquisa, escolham uma das ideias.

A proposta deve responder claramente:

**O que nosso sistema fará?**

Tentem explicar em uma frase.

Exemplo:

> Desenvolver um simulador de lançamento de projéteis no qual o usuário informa velocidade e ângulo e pode comparar diferentes lançamentos salvos no sistema.

Outro exemplo:

> Criar um sistema de cultivo virtual no qual temperatura, água e luminosidade influenciam o desenvolvimento das plantas.

Outro exemplo:

> Criar um jogo de genética no qual o jogador realiza cruzamentos e observa as probabilidades das características dos descendentes.

---

# Etapa 6 — Identificar o conceito científico

Esta é uma das partes mais importantes.

Descrevam:

## Qual conceito científico será utilizado?

Exemplo:

`Movimento uniformemente variado.`

Depois expliquem:

## Como esse conceito influencia o sistema?

Não é suficiente escrever:

> Nosso sistema será sobre Física.

É necessário explicar a relação.

Por exemplo:

> A velocidade e a aceleração serão utilizadas para calcular a nova posição do veículo a cada rodada.

Ou:

> As leis de Mendel serão utilizadas para calcular a probabilidade de determinadas características aparecerem nos descendentes.

---

# Etapa 7 — Imaginar o usuário

Definam quem utilizaria o sistema.

Exemplos:

- estudantes;
- professores;
- jogadores;
- pesquisadores;
- agricultores;
- pacientes;
- profissionais;
- público geral.

Depois respondam:

**Por que essa pessoa utilizaria o sistema?**

---

# Etapa 8 — Definir as funcionalidades

Façam uma lista das principais funcionalidades.

Exemplo de um simulador:

1. Cadastrar usuário.
2. Fazer login.
3. Criar uma simulação.
4. Informar os valores iniciais.
5. Executar os cálculos.
6. Mostrar o resultado graficamente.
7. Salvar a simulação.
8. Consultar simulações anteriores.
9. Comparar dois experimentos.

Não tentem colocar dezenas de funcionalidades.

É melhor criar um projeto menor que funcione bem.

---

# Etapa 9 — Pensar no Front-end

Desenhem as principais telas.

Não é necessário programá-las neste momento.

Podem desenhar:

- no papel;
- no Figma;
- no Canva;
- em outra ferramenta de prototipação.

Identifiquem pelo menos:

### Tela inicial

O que o usuário verá?

### Tela principal do sistema

Onde acontecerá a simulação, experimento, jogo ou atividade?

### Tela de resultados

Como os resultados serão apresentados?

### Tela de histórico

O usuário poderá consultar atividades anteriores?

Vocês podem criar outras telas quando necessário.

---

# Etapa 10 — Pensar no Back-end

Agora pensem no que precisa acontecer "por trás" da interface.

Perguntem:

- Que cálculos serão realizados?
- Existem regras?
- Existem condições?
- Existem fórmulas?
- Existem pontuações?
- Existem decisões automáticas?
- O sistema precisa validar alguma coisa?

Exemplo:

O usuário informa:

`velocidade = 10 m/s`

`tempo = 5 s`

O back-end pode calcular:

`distância = velocidade × tempo`

Resultado:

`50 metros`

Nesse caso, a fórmula científica faz parte da regra do sistema.

---

# Etapa 11 — Pensar no Banco de Dados

Agora identifiquem quais informações precisam permanecer armazenadas.

Não salvamos no banco apenas dados de login.

O banco deverá fazer parte do sistema proposto.

Perguntem:

**O que seria interessante consultar novamente depois?**

Exemplo:

### Usuário

- id
- nome
- email
- senha

### Experimento

- id
- usuario_id
- data
- tipo
- parâmetros utilizados
- resultado

### Tentativa

- id
- experimento_id
- valor_inicial
- resultado
- pontuação

Não precisam utilizar exatamente essas tabelas.

Cada projeto terá seu próprio modelo.

---

# Etapa 12 — Fazer um modelo inicial do banco

Desenhem as entidades principais e seus relacionamentos.

Exemplo:

`USUÁRIO`

↓ possui

`SIMULAÇÃO`

↓ possui

`RESULTADO`

Tentem identificar:

- entidades;
- atributos;
- chaves;
- relacionamentos.

Neste momento o modelo ainda pode mudar durante o desenvolvimento.

---

# Etapa 13 — Mostrar o caminho dos dados

Escolham uma ação importante do usuário e expliquem todo o caminho dela.

Exemplo:

### Usuário realiza um experimento

1. Usuário informa os dados no **front-end**.
2. O front-end envia os dados para o **back-end**.
3. O back-end aplica a regra ou fórmula científica.
4. O sistema calcula o resultado.
5. Os dados são registrados no **banco de dados**.
6. O back-end devolve o resultado.
7. O front-end apresenta o resultado ao usuário.

Façam esse fluxo para pelo menos uma funcionalidade importante.

---

# Etapa 14 — Pesquisar o conteúdo científico

Vocês deverão estudar o conteúdo científico que utilizarão.

Não é permitido simplesmente pedir para uma IA fornecer uma fórmula e colocá-la no sistema sem compreender o que ela significa.

No relatório expliquem:

- qual fenômeno será utilizado;
- quais grandezas estão envolvidas;
- quais fórmulas ou regras serão utilizadas;
- significado de cada variável;
- unidade de medida, quando existir;
- pelo menos um exemplo calculado.

---

# Etapa 15 — Identificar dificuldades

O grupo deverá indicar pelo menos três possíveis dificuldades.

Por exemplo:

- realizar determinado cálculo;
- criar uma animação;
- desenhar gráficos;
- criar o banco;
- implementar autenticação;
- modelar uma simulação;
- encontrar dados científicos confiáveis.

Depois indiquem possíveis soluções.

---

# Etapa 16 — Definir o MVP

MVP significa **Produto Mínimo Viável**.

É a menor versão do projeto que já demonstra a ideia funcionando.

Perguntem:

> Se tivéssemos pouco tempo, qual seria a versão mínima necessária para provar que nossa ideia funciona?

Exemplo:

Para um simulador de lançamento de foguetes:

### MVP

- informar velocidade inicial;
- informar ângulo;
- calcular trajetória;
- mostrar resultado;
- salvar tentativa.

### Futuramente

- animação;
- vários planetas;
- vento;
- ranking;
- multiplayer;
- diferentes foguetes.

Separem claramente:

**O que é obrigatório para a primeira versão**

e

**O que seria uma melhoria futura.**

---

# Etapa 17 — Entregar a proposta do projeto

O primeiro relatório deverá possuir:

## 1. Nome provisório do projeto

Criem um nome para o sistema.

## 2. Integrantes

Nome dos integrantes do grupo.

## 3. Área científica

Física, Química, Biologia ou combinação delas.

## 4. Problema ou ideia

O que vocês pretendem criar?

## 5. Público-alvo

Quem utilizará o sistema?

## 6. Conceito científico

Qual conteúdo científico estará envolvido?

## 7. Funcionamento científico

Como esse conteúdo interfere no funcionamento do sistema?

## 8. Principais funcionalidades

Lista das funcionalidades planejadas.

## 9. Front-end

Descrição e desenhos das principais telas.

## 10. Back-end

Principais regras, cálculos e processamentos.

## 11. Banco de dados

Entidades e informações que precisarão ser armazenadas.

## 12. Modelo inicial do banco

Diagrama das entidades e relacionamentos.

## 13. Fluxo de uma funcionalidade

Mostrar:

`Usuário → Front-end → Back-end → Banco de dados → Resultado`

## 14. Pesquisa científica

Explicação do conteúdo científico utilizado.

## 15. MVP

O que será desenvolvido primeiro?

## 16. Melhorias futuras

O que poderia ser acrescentado posteriormente?

## 17. Referências

Sites, vídeos, artigos, livros ou outros materiais utilizados na pesquisa.

---

# Algumas ideias para inspiração

Vocês **não precisam escolher uma delas**.

### Física

- Corrida de vetores;
- simulador de lançamento de projéteis;
- simulador de sistema solar;
- simulador de queda livre;
- laboratório de circuitos elétricos;
- jogo utilizando gravidade;
- simulador de consumo de energia;
- sistema para acompanhar velocidade e movimento;
- simulador de colisões.

### Química

- simulador de pH;
- jogo da tabela periódica;
- sistema para montar moléculas;
- simulador de reações;
- balanceador de equações químicas;
- laboratório virtual;
- sistema de comparação de elementos químicos.

### Biologia

- simulador de genética;
- jogo de cadeia alimentar;
- simulador de crescimento populacional;
- ecossistema virtual;
- sistema de classificação de espécies;
- simulador de epidemias;
- jogo sobre funcionamento do corpo humano;
- simulador de seleção natural.

---

# Uma regra importante

Evitem projetos em que Ciências apareça apenas como conteúdo escrito.

Por exemplo:

> "Vamos fazer um site com textos sobre planetas."

Isso utiliza desenvolvimento e fala sobre Ciências, mas praticamente não integra as duas áreas.

É mais interessante fazer:

> "Vamos criar um sistema em que o usuário altera massa, velocidade e distância dos planetas e observa como isso interfere na simulação."

Ou:

> "Vamos criar um banco de espécies e simular como alterações no ambiente modificam uma população."

Procurem fazer com que o conceito científico **cause alguma coisa dentro do programa**.

---

# Pergunta final

Ao terminar a proposta, todo grupo deverá conseguir responder:

> **Se retirarmos o conceito de Física, Química ou Biologia, nosso sistema ainda funciona da mesma maneira?**

Se a resposta for **sim**, provavelmente a integração com Ciências ainda está muito superficial.

Se a resposta for **não**, vocês provavelmente estão no caminho certo.

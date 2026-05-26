# Atividade: Página de Máquina de Vendas

Nesta atividade, vocês deverão criar uma página web que simule uma **máquina de vendas**, como aquelas que vendem água, refrigerante, salgadinho, chocolate ou outros produtos.

A página deverá ser feita usando **HTML, CSS e JavaScript**.

Vocês podem desenvolver manualmente ou usar ferramentas de inteligência artificial para ajudar. Porém, existe uma regra muito importante:

**Vocês precisarão entender e explicar o código que entregarem.**

Durante a apresentação ou correção, o professor poderá fazer perguntas sobre o funcionamento da página, sobre partes específicas do código e sobre as escolhas feitas.

O objetivo não é apenas entregar uma página funcionando, mas demonstrar que vocês compreenderam a lógica utilizada.

---

## Objetivo da atividade

Criar uma página interativa que permita ao usuário:

1. Visualizar produtos disponíveis em uma máquina de vendas.
2. Escolher um produto.
3. Informar o valor pago.
4. Verificar se o valor é suficiente.
5. Calcular o troco, quando necessário.
6. Exibir uma mensagem final para o usuário.

---

## Requisitos obrigatórios

A página deve conter os seguintes elementos:

---

## 1. Estrutura em HTML

O arquivo HTML deve ter uma estrutura organizada, contendo pelo menos:

- título da página;
- lista ou cards dos produtos;
- nome dos produtos;
- preço dos produtos;
- campo para o usuário informar o dinheiro inserido;
- botão para comprar;
- área para exibir o resultado da compra.

Exemplo de produtos:

| Produto | Preço |
|---|---:|
| Água | R$ 3,00 |
| Refrigerante | R$ 6,00 |
| Suco | R$ 5,00 |
| Salgado | R$ 7,00 |
| Chocolate | R$ 4,00 |

Vocês podem usar esses produtos ou criar outros.

---

## 2. Estilo com CSS

A página deve ter uma aparência organizada e agradável.

O CSS deve incluir pelo menos:

- cores de fundo;
- estilo para os produtos;
- botões personalizados;
- espaçamento entre os elementos;
- destaque visual para o produto escolhido;
- uma área de resultado bem visível.

A página pode parecer:

- uma máquina de vendas real;
- um painel digital;
- uma vitrine de produtos;
- uma interface simples e organizada;
- uma versão criativa inventada pelo grupo.

---

## 3. Interatividade com JavaScript

O JavaScript deve permitir que a página funcione como uma máquina de vendas.

O sistema deve:

- identificar qual produto foi escolhido;
- guardar o preço do produto;
- ler o valor digitado pelo usuário;
- comparar o valor pago com o preço;
- mostrar mensagem de erro se o dinheiro for insuficiente;
- calcular o troco se o dinheiro for suficiente;
- exibir uma mensagem de compra realizada.

Exemplo de mensagem para compra realizada:

    Você escolheu: Refrigerante
    Preço: R$ 6,00
    Valor pago: R$ 10,00
    Compra realizada com sucesso.
    Troco: R$ 4,00

Exemplo de mensagem para dinheiro insuficiente:

    Dinheiro insuficiente.
    Faltam R$ 2,00 para comprar este produto.

---

## Requisitos de lógica

O código deve usar alguns dos seguintes conceitos:

- variáveis;
- funções;
- eventos de clique;
- estruturas condicionais, como `if`, `else if` e `else`;
- operações matemáticas;
- manipulação do HTML com JavaScript, como:
  - `getElementById`;
  - `querySelector`;
  - `innerHTML`;
  - `textContent`.

---

## Requisitos extras opcionais

Quem quiser melhorar o projeto pode adicionar:

- imagens dos produtos;
- som de compra realizada;
- cálculo do troco usando notas e moedas;
- botão para limpar a compra;
- animação ao selecionar produto;
- aviso quando nenhum produto for escolhido;
- controle de estoque;
- modo escuro;
- layout responsivo para celular;
- teclado numérico na tela;
- histórico de compras.

---

## Sobre o uso de inteligência artificial

O uso de inteligência artificial é permitido, mas com responsabilidade.

Vocês podem usar IA para:

- pedir ideias;
- corrigir erros;
- melhorar o visual;
- pedir explicações;
- gerar partes do código.

Porém, não basta copiar e colar sem entender.

Cada aluno deverá ser capaz de responder perguntas sobre o próprio projeto.

Exemplos de perguntas que poderão ser feitas:

- O que essa função faz?
- Onde o produto escolhido é armazenado?
- Como o preço é comparado com o valor pago?
- Onde o troco é calculado?
- O que acontece se o usuário digitar um valor menor que o preço?
- Qual parte do código altera a mensagem na tela?
- O que aconteceria se removêssemos esse `if`?
- Como você adicionaria um novo produto?
- Qual parte do código pertence ao HTML?
- Qual parte pertence ao CSS?
- Qual parte pertence ao JavaScript?

---

## Entrega

A atividade deverá ser entregue com os seguintes arquivos:

    index.html
    style.css
    script.js

Também será aceito entregar tudo em um único arquivo HTML, desde que o código esteja organizado e seja possível identificar claramente as partes de:

- HTML;
- CSS;
- JavaScript.

---

## Critérios de avaliação

| Critério | O que será observado |
|---|---|
| Funcionamento | A máquina permite escolher produto, pagar e receber resultado? |
| Lógica | O código compara valores e calcula o troco corretamente? |
| Organização | O HTML, CSS e JavaScript estão claros e bem separados? |
| Visual | A página está organizada e compreensível para o usuário? |
| Explicação | O aluno consegue explicar o próprio código? |
| Criatividade | O projeto tem identidade própria, melhorias ou personalização? |

---

## Desafio principal

Criem uma página que simule uma máquina de vendas e preparem-se para explicar como ela funciona.

O mais importante não é fazer o projeto mais bonito da turma, mas conseguir mostrar que vocês entenderam a lógica por trás da página.
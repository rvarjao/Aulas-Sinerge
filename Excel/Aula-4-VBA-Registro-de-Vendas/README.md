# Aula 4 — Registro de vendas com VBA e tabelas relacionadas

## Objetivo
Criar uma macro que registre pedidos do cardápio em duas tabelas relacionadas, usando como referência a atividade anterior de controle de estoque. **Não é necessário criar um formulário novo.** A interface do cardápio já será a origem dos dados.

## Arquivo
Utilize `Cardapio_atividade_vendas.xlsx`. Antes de programar, salve uma cópia como **.xlsm** para habilitar macros.

## Modelo relacional
- **vendas**: uma linha por pedido. Campos: `id_venda` (chave primária), `data_hora`, `forma_pagamento`, `valor_total`.
- **vendas_produtos**: uma linha por produto do pedido. Campos: `id_item` (chave primária), `id_venda` (chave estrangeira), `produto`, `quantidade`, `valor_unitario`, `subtotal`.

Uma venda pode ter vários itens, mas cada item pertence a uma única venda. O mesmo `id_venda` deve aparecer na venda e em todos os itens dela.

## Etapa 1 — Reconhecimento da planilha
1. Abra a aba **Interface Cliente** e identifique os produtos e as quantidades.
2. Observe os pastéis: colunas **A** (quantidade), **B** (preço), **C** (produto), linhas **9 a 19**.
3. Observe as bebidas: colunas **I** (quantidade), **J** (preço), **K** (produto), linhas **9 a 19**.
4. Localize as duas tabelas de destino e identifique a linha de cabeçalho.

**Pergunta:** por que não é adequado colocar todos os produtos de uma venda em uma única célula?

## Etapa 2 — Preparar a macro
1. Abra o editor com **Alt + F11**.
2. Insira um módulo e crie uma `Sub RegistrarVenda()`.
3. Declare variáveis para as três planilhas, última linha, próxima linha, identificadores, contador, quantidade, preço, subtotal e total.
4. Reaproveite a lógica da aula de estoque para localizar a última linha preenchida.

**Pista, não solução completa:**
```vb
ultimaLinha = wsVendas.Cells(wsVendas.Rows.Count, 1).End(xlUp).Row
```

## Etapa 3 — Validar o pedido
1. Verifique se existe pelo menos um produto com quantidade maior que zero.
2. Caso não exista, apresente uma mensagem e encerre a rotina sem gravar nada.
3. Calcule o total usando as quantidades e preços dos itens escolhidos.
4. Confira como a planilha representa valores monetários (número ou texto formatado).

**Desafio:** como evitar registrar um pedido vazio?

## Etapa 4 — Registrar o cabeçalho da venda
1. Encontre a próxima linha livre em `vendas`.
2. Gere um `id_venda` que ainda não exista.
3. Grave a data e hora atual, a forma de pagamento (conforme a interface ou critério definido em aula) e o total.
4. Guarde o `id_venda` em uma variável: ele será reutilizado em todos os itens.

**Pergunta:** qual é a diferença entre o número da linha e o ID da venda?

## Etapa 5 — Registrar os itens
1. Percorra as linhas dos pastéis com um laço `For`.
2. Para cada linha, use `If` para verificar se a quantidade é maior que zero.
3. Encontre a próxima linha livre em `vendas_produtos`.
4. Gere o `id_item`, copie o `id_venda`, nome do produto, quantidade e valor unitário.
5. Calcule `subtotal = quantidade * valor_unitario`.
6. Repita o procedimento para as bebidas.

**Desafio:** é possível evitar código duplicado criando uma `Sub` auxiliar ou passando os números das colunas como parâmetros?

## Etapa 6 — Finalização
1. Confirme se todos os itens foram gravados.
2. Somente depois da gravação, limpe as quantidades da interface.
3. Mostre uma mensagem com o ID da venda e o valor total.
4. Associe a macro a um botão na planilha.

**Atenção:** não limpe a interface se houver erro na gravação. Pense no que fazer se a venda for registrada, mas algum item falhar.

## Testes obrigatórios
- Uma venda com dois tipos de pastéis e uma bebida.
- Uma venda com apenas uma bebida.
- Tentativa de venda sem quantidades.
- Duas vendas consecutivas: verificar se os IDs não se repetem.
- Conferir se o total de cada venda é igual à soma dos subtotais dos itens com o mesmo `id_venda`.

## Entrega
Entregue a planilha **.xlsm**, com a macro funcionando, e um breve registro dos testes realizados. O código deve ser construído pelos alunos, usando a aula anterior como referência.

## Avaliação (10 pontos)
| Critério | Pontos |
|---|---:|
| Referências corretas às planilhas e próximas linhas | 2 |
| IDs e relacionamento entre tabelas | 2 |
| Uso de `For` e `If` | 2 |
| Gravação dos itens e cálculos | 2 |
| Validações, limpeza e testes | 2 |

## Versão no Google Sheets
- Podemos visualizar esse mesmo documento na versão do Google Sheets. Acesse pelo link: [Cardápio](https://docs.google.com/spreadsheets/d/1jAhigiklcQP9z9o3MzHIhsuBRd3lRq5o-533hr660ac/edit?usp=sharing)
- Para visualizar o código vá em Extensões -> App Scripts

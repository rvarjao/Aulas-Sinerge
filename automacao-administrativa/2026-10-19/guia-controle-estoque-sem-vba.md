# Atividade prática — Controle de estoque no Excel (sem VBA)

**Turma:** Automação Administrativa  
**Data:** 19/10/2026  
**Tempo previsto:** até 40 minutos

## O que você vai aprender

Nesta atividade, você vai usar o Excel para controlar o estoque de produtos. Ao final, sua planilha deverá calcular automaticamente o saldo com base nas **entradas** e **saídas**, além de indicar os produtos que precisam de reposição.

Você não precisará utilizar VBA ou macros.

## Antes de começar

Abra o arquivo `controle-estoque-sem-vba.xlsx` no Excel e localize as duas abas:

- **Produtos:** contém o cadastro, o estoque mínimo, o estoque atual e a situação de cada produto.
- **Movimentacoes:** registra a entrada ou a saída de cada produto.

**Importante:** não altere o estoque atual manualmente. Ele será calculado a partir dos registros de movimentação.

## Etapa 1 — Explore a planilha (3 minutos)

1. Na aba **Produtos**, observe os códigos dos produtos e os valores de estoque mínimo.
2. Na aba **Movimentacoes**, identifique as colunas **Código**, **Tipo** e **Quantidade**.
3. Verifique como os códigos relacionam cada movimentação a um produto.

## Etapa 2 — Calcule o estoque atual (12 minutos)

1. Acesse a aba **Produtos**.
2. Selecione a célula **D5**.
3. Digite a fórmula:

```excel
=SOMASES(Movimentacoes!$D$5:$D$30;Movimentacoes!$B$5:$B$30;A5;Movimentacoes!$C$5:$C$30;"Entrada")-SOMASES(Movimentacoes!$D$5:$D$30;Movimentacoes!$B$5:$B$30;A5;Movimentacoes!$C$5:$C$30;"Saída")
```

4. Pressione **Enter**.
5. Copie a fórmula de **D5 até D10**, usando a alça de preenchimento.

**Entenda o cálculo:** a função `SOMASES` soma as quantidades do produto indicado em `A5` que são do tipo **Entrada**. Depois, subtrai as quantidades do mesmo produto registradas como **Saída**.

Agora, faça a planilha informar se o estoque está adequado:

6. Na célula **E5**, digite:

```excel
=SE(D5<C5;"Abaixo do mínimo";"Estoque adequado")
```

7. Pressione **Enter** e copie a fórmula até **E10**.

**Observe:** a função `SE` compara o estoque atual (`D5`) com o estoque mínimo (`C5`).

## Etapa 3 — Destaque os produtos que precisam de reposição (5 minutos)

1. Selecione o intervalo **E5:E10**, na aba **Produtos**.
2. Acesse **Página Inicial → Formatação Condicional → Realçar Regras das Células → Texto que contém**.
3. Crie uma regra para o texto **Abaixo do mínimo** com preenchimento vermelho-claro.
4. Crie outra regra para o texto **Estoque adequado** com preenchimento verde-claro.

Confira se as situações estão destacadas com as cores corretas.

## Etapa 4 — Registre novas movimentações (12 minutos)

Acesse a aba **Movimentacoes** e preencha as próximas linhas vazias com os quatro registros abaixo.

| Situação | Código | Tipo | Quantidade |
| --- | ---: | --- | ---: |
| Chegaram canetas para reposição | 102 | Entrada | 20 |
| Foram usados cadernos em uma oficina | 101 | Saída | 22 |
| Chegaram marca-textos | 105 | Entrada | 10 |
| Foram entregues pastas | 106 | Saída | 9 |

Atenção:

- Use exatamente **Entrada** ou **Saída** na coluna **Tipo**.
- Registre cada operação em uma linha diferente.
- Não apague movimentações anteriores.
- Preencha as outras colunas existentes, como data, conforme o modelo da planilha.

Depois de registrar tudo, volte à aba **Produtos**. Verifique se os saldos e as situações mudaram automaticamente.

## Etapa 5 — Responda e confira seu trabalho (5 minutos)

Responda às perguntas abaixo no caderno ou no local indicado pelo professor:

1. Quais produtos ficaram abaixo do estoque mínimo após as novas movimentações?
2. Por que o estoque atual deve ser calculado pelas movimentações, em vez de digitado manualmente?
3. O que aconteceria com o saldo de um produto se uma movimentação de **Saída** fosse apagada?

### Checklist de conclusão

- [ ] Preenchi a fórmula do estoque atual em **D5:D10**.
- [ ] Preenchi a fórmula da situação em **E5:E10**.
- [ ] Configurei as duas regras de formatação condicional.
- [ ] Registrei as quatro movimentações propostas.
- [ ] Conferi a atualização automática dos saldos.
- [ ] Respondi às três perguntas.

**Ao finalizar:** salve seu arquivo do Excel e siga as orientações do professor para apresentar ou entregar a atividade.

> **Desafio extra (opcional):** pense em como a planilha poderia avisar que um produto está com estoque zerado, sem alterar manualmente os saldos.

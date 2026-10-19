# Aula rápida — Controle de estoque sem VBA

**Tempo de atividade no Excel: até 40 minutos.**

## Objetivo

Montar um controle de estoque que calcula o saldo de cada produto a partir do registro de entradas e saídas.

## Roteiro

### 1. Conhecer os dados — 3 min

Abra `controle-estoque-sem-vba.xlsx` e observe as abas **Produtos** e **Movimentacoes**. Toda alteração de estoque deve ser registrada em **Movimentacoes**.

### 2. Calcular o estoque atual — 12 min

Na aba **Produtos**, em `D5`, escreva a fórmula abaixo e copie-a até `D10`:

```excel
=SOMASES(Movimentacoes!$D$5:$D$30;Movimentacoes!$B$5:$B$30;A5;Movimentacoes!$C$5:$C$30;"Entrada")-SOMASES(Movimentacoes!$D$5:$D$30;Movimentacoes!$B$5:$B$30;A5;Movimentacoes!$C$5:$C$30;"Saída")
```

Em seguida, em `E5`, escreva e copie até `E10`:

```excel
=SE(D5<C5;"Abaixo do mínimo";"Estoque adequado")
```

### 3. Destacar produtos com pouco estoque — 5 min

Selecione `E5:E10` e aplique **Formatação Condicional → Realçar Regras das Células → Texto que contém**:

- `Abaixo do mínimo`: preenchimento vermelho-claro;
- `Estoque adequado`: preenchimento verde-claro.

### 4. Registrar movimentações — 12 min

Na aba **Movimentacoes**, registre as situações abaixo nas linhas vazias. Use apenas `Entrada` ou `Saída` na coluna Tipo.

| Situação | Código | Tipo | Quantidade |
| --- | ---: | --- | ---: |
| Chegaram canetas para reposição | 102 | Entrada | 20 |
| Foram usados cadernos em uma oficina | 101 | Saída | 22 |
| Chegaram marca-textos | 105 | Entrada | 10 |
| Foram entregues pastas | 106 | Saída | 9 |

Volte à aba **Produtos** e confira os saldos e as situações.

### 5. Fechamento — 5 min

Responda:

1. Quais produtos estão abaixo do mínimo?
2. Por que não devemos digitar diretamente o estoque atual?
3. O que aconteceria com o saldo se uma saída fosse apagada da aba Movimentacoes?

## Observação para o professor

Se o tempo estiver apertado, aplique somente a fórmula de estoque atual e deixe a coluna Situação como desafio ou demonstração final. Não é necessário criar tabelas, macros, gráficos ou filtros nesta aula.

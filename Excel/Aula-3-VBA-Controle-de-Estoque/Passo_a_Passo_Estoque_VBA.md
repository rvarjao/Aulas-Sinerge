# Aula — Controle de estoque por movimentações (Excel + VBA)

## Estrutura das três abas
1. **Lancamentos** (primeira aba): B4 código, B5 tipo (Entrada/Saída), B6 quantidade, B7 saldo disponível calculado.
2. **Produtos**: A código, B descrição, C mínimo, D estoque atual **calculado**, E situação.
3. **Movimentacoes**: A data, B código, C tipo, D quantidade. Toda entrada, inclusive estoque inicial, deve constar aqui.

## Regra central
**Nunca escreva no saldo da aba Produtos via VBA.** O saldo é derivado do histórico:

```excel
=SOMASES(Movimentacoes!$D$2:$D$1000;Movimentacoes!$B$2:$B$1000;A2;Movimentacoes!$C$2:$C$1000;"Entrada")-SOMASES(Movimentacoes!$D$2:$D$1000;Movimentacoes!$B$2:$B$1000;A2;Movimentacoes!$C$2:$C$1000;"Saída")
```
A planilha fornecida já contém a fórmula equivalente, armazenada no padrão interno do Excel.

## Aula 1: lançamentos guiados
1. Abra o arquivo e salve como **.xlsm**.
2. Observe que os três saldos iniciais resultam de movimentações de entrada, não de valores digitados em Produtos.
3. No editor VBA (Alt+F11), crie um módulo e uma macro `RegistrarMovimentacao`.
4. Leia código, tipo e quantidade das células B4, B5 e B6 da aba Lancamentos.
5. Procure o código na aba Produtos usando `For` e `If`. Se não existir, mostre `MsgBox` e encerre.
6. Verifique quantidade numérica, inteira e maior que zero. Para saída, compare com o saldo calculado na coluna D de Produtos.
7. Descubra a próxima linha livre de Movimentacoes usando `Cells(Rows.Count,1).End(xlUp).Row + 1`.
8. Grave **somente** data, código, tipo e quantidade na aba Movimentacoes.
9. Teste se o estoque em Produtos mudou automaticamente, sem atribuição VBA à coluna D.
10. Na aba Lancamentos, associe a macro a um botão de formulário chamado **Registrar movimentação**.

### Esqueleto para completar
```vb
Sub RegistrarMovimentacao()
    Dim codigo As Long, qtd As Long, tipo As String
    Dim linha As Long, ultima As Long, destino As Long
    Dim encontrada As Boolean
    ' TODO: ler e validar B4, B5, B6 da aba Lancamentos
    ' TODO: procurar código em Produtos
    ' TODO: se for Saída, validar qtd <= estoque atual
    ' TODO: gravar nova linha em Movimentacoes
    ' NÃO atualizar Produtos!D diretamente
End Sub
```

## Aula 2: testes e melhorias
- Entrada válida: uma linha nova e saldo maior.
- Saída válida: uma linha nova e saldo menor.
- Saída maior que estoque: nenhuma linha nova.
- Código inexistente ou quantidade zero/negativa: nenhuma linha nova.
- Desafio: limpar os campos após gravar, sem apagar fórmulas.
- Desafio extra: relatório de produtos abaixo do mínimo.

## Entrega
Entregar o arquivo **.xlsm** no **mesmo formulário usado na atividade anterior**, na nova questão criada pelo professor. Incluir uma breve descrição dos testes. Não criar formulário novo.

## Discussão
Por que o estoque é um dado derivado? Como reconstituir o saldo após uma falha? O que acontece se alguém editar ou apagar uma movimentação antiga?

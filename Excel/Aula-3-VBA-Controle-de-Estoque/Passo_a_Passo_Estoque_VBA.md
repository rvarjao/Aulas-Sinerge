# Aula prática — Controle de estoque com Excel e VBA

**Turma:** 1º ano · **Duração:** 2 aulas de 50 minutos

## Objetivo
Construir um sistema com duas abas relacionadas pelo código do produto:
- **Produtos:** Código, Produto, Estoque atual, Estoque mínimo.
- **Movimentacoes:** Data, Código produto, Tipo (Entrada/Saída), Quantidade.

Toda entrada ou saída deve atualizar o estoque e registrar uma linha em Movimentacoes.

## Preparação
1. Abra a planilha de controle de estoque no Excel desktop.
2. Salve como **Pasta de Trabalho Habilitada para Macro (.xlsm)**.
3. Ative a guia Desenvolvedor e pressione **Alt+F11**.
4. Selecione Inserir → Módulo.

## Aula 1 — Busca e entrada
1. Analise as tabelas e explique a relação entre Código e Código produto.
2. Crie uma macro com `InputBox` para solicitar o código.
3. Use `For ... Next` e `If ... Then` para localizar o produto na aba Produtos.
4. Solicite uma quantidade positiva e some ao estoque.
5. Encontre a próxima linha vazia da aba Movimentacoes e registre data, código, tipo Entrada e quantidade.
6. Teste código inexistente e quantidade zero/negativa.

### Exemplo de busca
```vb
Sub BuscarProduto()
    Dim codigo As Long, linha As Long, ultima As Long
    codigo = CLng(InputBox("Código do produto:"))
    ultima = Sheets("Produtos").Cells(Sheets("Produtos").Rows.Count, 1).End(xlUp).Row
    For linha = 2 To ultima
        If Sheets("Produtos").Cells(linha, 1).Value = codigo Then
            MsgBox Sheets("Produtos").Cells(linha, 2).Value
            Exit Sub
        End If
    Next linha
    MsgBox "Produto não encontrado."
End Sub
```

## Aula 2 — Saída, cadastro e testes
1. Implemente a saída de estoque, impedindo venda maior que o saldo.
2. Registre a saída na aba Movimentacoes.
3. Crie um botão para cada operação e associe a macro.
4. Desafio: cadastrar produto em nova linha, sem permitir código duplicado.
5. Desafio extra: destacar produtos abaixo do estoque mínimo.

## Testes obrigatórios
- Entrada válida aumenta o saldo e gera histórico.
- Saída válida diminui o saldo e gera histórico.
- Produto inexistente não altera as tabelas.
- Quantidade negativa ou zero é rejeitada.
- Saída maior que o saldo é rejeitada.
- Código duplicado não é cadastrado.

## Entrega
Use **o mesmo formulário da atividade anterior**, na nova questão disponibilizada pelo professor. Anexe a planilha final em **.xlsm** e descreva brevemente os testes realizados. Não envie por e-mail nem abra outro formulário.

## Discussão
Se o estoque atual fosse removido da tabela Produtos, seria possível reconstruí-lo pelo histórico? Quais dados iniciais seriam necessários?

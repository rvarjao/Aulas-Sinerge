# Aula 2 — VBA no Excel: registrar dados em tabelas relacionadas

## Missão da aula

Nesta aula, você vai construir uma automação para registrar **reservas de equipamentos do laboratório**. A ideia é a mesma de uma venda com produtos: uma solicitação pode ter vários itens.

Ao clicar em um botão, a macro deve pegar os dados da tela de lançamento e gravá-los em duas tabelas. Uma terceira tabela já existente funciona como catálogo:

| Tabela | O que guarda | Ligação |
|---|---|---|
| `tblSolicitacoes` | uma linha para cada reserva | possui o `ID_Solicitacao` |
| `tblItensSolicitacao` | uma linha para cada equipamento reservado | repete o mesmo `ID_Solicitacao` |
| `tblEquipamentos` | catálogo de códigos e nomes dos equipamentos | é consultada pelo `Codigo_Equipamento` |

Exemplo: a solicitação `RES-001` pode pedir um projetor e três notebooks. Ela aparece **uma vez** na primeira tabela e **duas vezes** na segunda.

```
RES-001 ─── Solicitação da turma 2A
   ├────── Projetor, quantidade 1
   └────── Notebook, quantidade 3
```

No final, as tabelas-resumo do `Dashboard` serão alimentadas pelos lançamentos. Os três cartões de indicador ficarão sem fórmula: essa será uma parte do desafio da turma.

## Arquivo inicial

Abra o arquivo `template_aula_2_vba_reservas_laboratorio.xlsx` e salve uma cópia como **Pasta de Trabalho Habilitada para Macro do Excel (`.xlsm`)** antes de inserir o código.

O arquivo tem cinco abas:

| Aba | Função |
|---|---|
| `Dashboard` | mostra indicadores e resumos calculados por fórmulas |
| `Tela_Lancamento` | é a tela que o usuário preenche |
| `Solicitacoes` | receberá os dados principais de cada reserva |
| `Itens_Solicitacao` | receberá cada equipamento da reserva |
| `Cadastros` | contém a `tblEquipamentos` e a lista de turmas |

As células amarelas na tela de lançamento são os campos de preenchimento.

## 1. Entenda a relação entre as duas tabelas

Na aba `Solicitacoes`, cada reserva terá estes dados:

| ID_Solicitacao | Data_Pedido | Professor | Turma | Data_Uso |
|---|---|---|---|---|
| RES-001 | 02/10/2026 | Ana Lima | 2A | 09/10/2026 |

Na aba `Itens_Solicitacao`, os itens usam o mesmo ID:

| ID_Solicitacao | Codigo_Equipamento | Equipamento | Quantidade | Observacao |
|---|---|---|---:|---|
| RES-001 | EQ-10 | Projetor | 1 | HDMI |
| RES-001 | EQ-03 | Notebook | 3 | Carregados |

O `ID_Solicitacao` é a chave que permite saber a quais dados principais cada item pertence.

## 2. Transforme as áreas de lançamentos em Tabelas do Excel

Vamos criar as duas tabelas que a macro usará.

1. Abra a aba `Solicitacoes`.
2. Selecione `A5:E5`, que contém os cabeçalhos.
3. Pressione `Ctrl + T`.
4. Marque **Minha tabela tem cabeçalhos** e confirme.
5. Na guia **Design da Tabela**, altere o nome da tabela para `tblSolicitacoes`.
6. Abra a aba `Itens_Solicitacao`.
7. Selecione `A5:E5`, pressione `Ctrl + T`, marque os cabeçalhos e confirme.
8. Renomeie essa tabela para `tblItensSolicitacao`.

> Os nomes precisam ser exatamente esses. O VBA usará os nomes para encontrar as tabelas, sem depender de uma linha específica.

Na aba `Cadastros`, a terceira tabela já está pronta: `tblEquipamentos`. Ela é o catálogo oficial de códigos e nomes. Por isso, não crie equipamentos manualmente em `Itens_Solicitacao`: informe o código e deixe o Excel buscar o nome no catálogo.

## 3. Crie as listas suspensas

Na aba `Cadastros`, existem os códigos da `tblEquipamentos` e a lista de turmas:

- Códigos dos equipamentos em `A6:A10`;
- Turmas em `D6:D10`.

Para que a lista funcione em outra aba, crie dois nomes:

1. Selecione `Cadastros!A6:A10`.
2. Clique na **Caixa de Nome**, à esquerda da barra de fórmulas.
3. Digite `listaCodigosEquipamentos` e pressione `Enter`.
4. Selecione `Cadastros!D6:D10`.
5. Na Caixa de Nome, digite `listaTurmas` e pressione `Enter`.

Agora aplique a validação de dados:

1. Abra `Tela_Lancamento` e selecione `B9`.
2. Vá em **Dados > Validação de Dados**.
3. Em **Permitir**, escolha **Lista**.
4. Em **Fonte**, escreva `=listaTurmas` e confirme.
5. Selecione `A13:A20`.
6. Repita o processo, mas use `=listaCodigosEquipamentos` como fonte.

Na célula `B13`, insira a fórmula abaixo e copie até `B20`. Ela mostra o nome correspondente ao código selecionado:

```excel
=SEERRO(PROCV(A13;tblEquipamentos;2;FALSO);"")
```

Teste as setas de lista suspensa antes de continuar. Depois, acrescente uma turma ou um equipamento à aba `Cadastros` e ajuste o intervalo dos nomes para incluir o novo dado.

## 4. Conheça o Dashboard dinâmico

As duas tabelas-resumo do Dashboard são Tabelas do Excel e usam fórmulas que buscam as categorias na aba `Cadastros`. Portanto, o Dashboard não repete manualmente os nomes das turmas e dos equipamentos.

Os cartões verdes foram deixados vazios de propósito. Em dupla ou grupo, criem as fórmulas para:

1. contar as solicitações registradas;
2. somar a quantidade de itens reservados;
3. contar as reservas cuja data de uso é hoje ou futura.

Use as abas `Solicitacoes` e `Itens_Solicitacao` como fonte. Teste cada fórmula depois de inserir novos lançamentos.

## 5. Prepare uma situação para testar

Na aba `Tela_Lancamento`, preencha:

| Campo | Valor de teste |
|---|---|
| B6 — ID da solicitação | `RES-001` |
| B7 — Data do pedido | `02/10/2026` |
| B8 — Professor responsável | `Ana Lima` |
| B9 — Turma | `2A` |
| B10 — Data de uso | `09/10/2026` |
| A13 | `EQ-10` |
| B13 | preenchido automaticamente como `Projetor` |
| C13 | `1` |
| D13 | `Usar cabo HDMI` |
| A14 | `EQ-03` |
| B14 | preenchido automaticamente como `Notebook` |
| C14 | `3` |
| D14 | `Carregados` |

Ainda não clique em nada. Primeiro vamos criar a macro.

## 6. Abra o editor VBA e crie o módulo

1. Pressione `Alt + F11`.
2. Clique em **Inserir > Módulo**.
3. No painel em branco, cole o código da próxima seção.

## 7. Crie a macro de lançamento

```vba
Option Explicit

Sub RegistrarSolicitacao()

    Dim wsTela As Worksheet
    Dim wsSolicitacoes As Worksheet
    Dim wsItens As Worksheet
    Dim tblSolicitacoes As ListObject
    Dim tblItens As ListObject
    Dim novaSolicitacao As ListRow
    Dim novoItem As ListRow
    Dim id As String
    Dim linha As Long
    Dim quantidadeItens As Long

    Set wsTela = Worksheets("Tela_Lancamento")
    Set wsSolicitacoes = Worksheets("Solicitacoes")
    Set wsItens = Worksheets("Itens_Solicitacao")
    Set tblSolicitacoes = wsSolicitacoes.ListObjects("tblSolicitacoes")
    Set tblItens = wsItens.ListObjects("tblItensSolicitacao")

    id = Trim(wsTela.Range("B6").Value)

    'Validação dos dados principais
    If id = "" Or wsTela.Range("B7").Value = "" Or _
       Trim(wsTela.Range("B8").Value) = "" Or _
       Trim(wsTela.Range("B9").Value) = "" Or _
       wsTela.Range("B10").Value = "" Then

        MsgBox "Preencha todos os dados da solicitação.", vbExclamation
        Exit Sub
    End If

    'Não permite repetir um ID já registrado
    If tblSolicitacoes.ListRows.Count > 0 Then
        If Application.WorksheetFunction.CountIf( _
            tblSolicitacoes.ListColumns("ID_Solicitacao").DataBodyRange, id) > 0 Then

            MsgBox "Esse ID já foi registrado. Escolha outro ID.", vbExclamation
            Exit Sub
        End If
    End If

    'Validação dos itens antes de gravar qualquer dado
    quantidadeItens = 0

    For linha = 13 To 20
        If Trim(wsTela.Cells(linha, "A").Value) <> "" Then

            If Trim(wsTela.Cells(linha, "B").Value) = "" Or _
               Not IsNumeric(wsTela.Cells(linha, "C").Value) Or _
               wsTela.Cells(linha, "C").Value <= 0 Then

                MsgBox "Confira o equipamento e a quantidade na linha " & linha & ".", vbExclamation
                Exit Sub
            End If

            quantidadeItens = quantidadeItens + 1
        End If
    Next linha

    If quantidadeItens = 0 Then
        MsgBox "Inclua pelo menos um equipamento.", vbExclamation
        Exit Sub
    End If

    'Grava uma linha na tabela principal
    Set novaSolicitacao = tblSolicitacoes.ListRows.Add

    With novaSolicitacao.Range
        .Cells(1, 1).Value = id
        .Cells(1, 2).Value = wsTela.Range("B7").Value
        .Cells(1, 3).Value = Trim(wsTela.Range("B8").Value)
        .Cells(1, 4).Value = Trim(wsTela.Range("B9").Value)
        .Cells(1, 5).Value = wsTela.Range("B10").Value
    End With

    'Grava uma linha para cada item preenchido
    For linha = 13 To 20
        If Trim(wsTela.Cells(linha, "A").Value) <> "" Then

            Set novoItem = tblItens.ListRows.Add

            With novoItem.Range
                .Cells(1, 1).Value = id
                .Cells(1, 2).Value = Trim(wsTela.Cells(linha, "A").Value)
                'O nome é buscado no catálogo tblEquipamentos pelo código.
                .Cells(1, 3).FormulaR1C1 = _
                    "=IFERROR(VLOOKUP(RC[-1],tblEquipamentos,2,FALSE),\"\")"
                .Cells(1, 4).Value = wsTela.Cells(linha, "C").Value
                .Cells(1, 5).Value = Trim(wsTela.Cells(linha, "D").Value)
            End With
        End If
    Next linha

    'Limpa a tela para o próximo lançamento
    wsTela.Range("B6:B10").ClearContents
    wsTela.Range("A13:A20").ClearContents
    wsTela.Range("C13:D20").ClearContents

    MsgBox "Solicitação " & id & " registrada com " & _
           quantidadeItens & " item(ns).", vbInformation

End Sub
```

## 8. Leia o código antes de executar

| Parte do código | Para que serve |
|---|---|
| `ListObject` | representa uma Tabela do Excel no VBA |
| `ListRows.Add` | cria uma nova linha no final de uma tabela |
| `For linha = 13 To 20` | percorre os possíveis itens na tela de lançamento |
| `If ... Then` | verifica se um dado está preenchido ou válido |
| `CountIf` | impede o uso do mesmo ID em duas solicitações |
| `Cells(1, 1)` | indica uma célula da nova linha criada na tabela |
| `ClearContents` | limpa os dados digitados, sem apagar a formatação |

Perceba que a macro grava primeiro a solicitação e depois todos os itens. O mesmo `id` é enviado para as duas tabelas, criando a relação entre elas. O código do equipamento também aponta para `tblEquipamentos`, que é a fonte única para o nome exibido.

## 9. Crie o botão

1. Volte para a aba `Tela_Lancamento`.
2. Abra a guia **Desenvolvedor > Inserir**.
3. Em **Controles de Formulário**, escolha **Botão**.
4. Desenhe o botão perto da indicação em cinza, na coluna F.
5. Na janela **Atribuir Macro**, selecione `RegistrarSolicitacao`.
6. Clique com o botão direito no botão, escolha **Editar Texto** e escreva `Registrar solicitação`.

> Se a guia Desenvolvedor não estiver visível: **Arquivo > Opções > Personalizar Faixa de Opções > marque Desenvolvedor**.

## 10. Execute o teste

1. Volte à `Tela_Lancamento` com os dados de teste preenchidos.
2. Clique em **Registrar solicitação**.
3. Confira a aba `Solicitacoes`: deve existir uma linha com `RES-001`.
4. Confira a aba `Itens_Solicitacao`: devem existir duas linhas com `RES-001`; os nomes dos equipamentos devem vir da tabela `tblEquipamentos`.
5. Abra o `Dashboard`: as tabelas-resumo devem ser recalculadas. Os cartões mostrarão resultados somente depois que seu grupo criar as fórmulas.

Resultado esperado após o teste:

| Indicador | Resultado esperado |
|---|---:|
| Solicitações da turma 2A | 1 |
| Projetor | 1 |
| Notebook | 3 |

## 11. Testes que seu grupo deve fazer

Teste a macro com as situações abaixo e explique o resultado.

1. Clicar no botão sem preencher o professor.
2. Digitar quantidade `0` ou texto em vez de número.
3. Tentar registrar novamente o ID `RES-001`.
4. Registrar uma nova solicitação com dois itens diferentes.
5. Registrar uma reserva sem preencher nenhum item.

## Desafios

Escolha pelo menos um:

1. Adicione um campo `Turno` à tela e à tabela `Solicitacoes`.
2. Crie as fórmulas dos três cartões do `Dashboard` e explique qual função foi usada em cada um.
3. Crie um gráfico de colunas no `Dashboard` usando “Itens por equipamento”.
4. Crie uma macro para localizar uma solicitação pelo ID e mostrar seus itens.
5. Impedir que a data de uso seja anterior à data do pedido.

## Entrega

Entregue o arquivo `.xlsm` com:

- o botão funcionando;
- as duas Tabelas do Excel criadas e nomeadas corretamente;
- pelo menos duas solicitações registradas, cada uma com mais de um item;
- as listas suspensas de turma e equipamento funcionando;
- as tabelas-resumo e os cartões do `Dashboard` atualizados;
- o código VBA comentado em pelo menos três partes.

Nunca habilite macros de arquivos desconhecidos. Use macros somente de fontes confiáveis.

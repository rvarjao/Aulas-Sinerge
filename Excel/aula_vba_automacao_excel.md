# Atividade: sua primeira automação com VBA no Excel

## Objetivo

Criar uma macro que lê um nome e um valor na planilha **Entrada**, transforma essas informações e gera um resumo automático na planilha **Resumo**.

Ao terminar, você saberá fazer o caminho básico de uma automação:

> ler uma célula → transformar um dado → escrever o resultado em outra célula

---

## 1. Prepare a planilha

Crie duas abas no mesmo arquivo do Excel:

- `Entrada`
- `Resumo`

Na aba **Entrada**, monte esta estrutura:

| Célula | Conteúdo |
|---|---|
| A1 | Cadastro simples |
| A2 | Nome |
| B2 | Digite seu nome |
| A3 | Valor |
| B3 | Digite um valor, por exemplo: 100 |

Na aba **Resumo**, deixe as células vazias por enquanto.

---

## 2. Salve o arquivo corretamente

1. Clique em **Arquivo > Salvar como**.
2. Em tipo de arquivo, escolha **Pasta de Trabalho Habilitada para Macro do Excel**.
3. Salve com a extensão `.xlsm`.

> Atenção: nunca habilite macros de arquivos desconhecidos. Uma macro é código e precisa vir de uma fonte confiável.

---

## 3. Abra o editor VBA

1. Pressione `Alt + F11`.
2. No menu superior, clique em **Inserir > Módulo**.
3. Uma área em branco para escrever o código será aberta.

---

## 4. Crie a macro

Copie este código para o módulo:

```vba
Sub GerarResumo()

    Dim nome As String
    Dim valor As Double

    nome = Trim(Worksheets("Entrada").Range("B2").Value)
    valor = Worksheets("Entrada").Range("B3").Value

    Worksheets("Resumo").Range("A2").Value = "Nome"
    Worksheets("Resumo").Range("B2").Value = UCase(nome)

    Worksheets("Resumo").Range("A3").Value = "Valor com desconto de 10%"
    Worksheets("Resumo").Range("B3").Value = valor * 0.9

    Worksheets("Resumo").Range("A5").Value = _
        "Resumo gerado em: " & Format(Now, "dd/mm/yyyy hh:mm")

End Sub
```

---

## 5. Execute e teste

1. Volte para a aba **Entrada** e altere o nome e o valor em `B2` e `B3`.
2. Abra novamente o editor com `Alt + F11`.
3. Clique em qualquer parte do código.
4. Pressione `F5` ou clique no botão verde de executar.
5. Volte para a aba **Resumo** e confira o resultado.

Teste, por exemplo:

- Nome: `  maria da silva  `
- Valor: `100`

O nome deve aparecer como `MARIA DA SILVA` e o valor final como `90`.

---

## 6. Entendendo o código

| Trecho | O que faz |
|---|---|
| `Range("B2").Value` | Lê ou escreve o conteúdo da célula B2. |
| `Worksheets("Entrada")` | Indica em qual aba a célula está. |
| `Trim(nome)` | Remove espaços extras antes e depois do texto. |
| `UCase(nome)` | Converte o texto para letras maiúsculas. |
| `valor * 0.9` | Calcula o valor com 10% de desconto. |
| `Now` | Obtém a data e a hora atuais. |
| `Dim` | Cria uma variável para guardar uma informação. |

---

## 7. Coloque um botão na planilha (opcional)

1. Abra a guia **Desenvolvedor**. Se ela não aparecer, avise o professor.
2. Clique em **Inserir > Botão (Controle de Formulário)**.
3. Desenhe o botão na aba **Entrada**.
4. Quando o Excel pedir uma macro, escolha `GerarResumo`.
5. Troque o texto do botão para **Gerar resumo**.

Agora não é necessário abrir o editor para executar a automação.

---

## Desafio

Adapte a macro para o mini sistema que você está desenvolvendo.

Escolha uma opção ou crie outra ideia:

1. Calcular a média de duas notas e informar se o aluno foi aprovado.
2. Informar o valor total de um produto usando quantidade × valor unitário.
3. Aplicar um desconto ou acréscimo em uma venda.
4. Pegar dados de cadastro e gerar uma ficha em outra planilha.

Seu desafio precisa ter pelo menos:

- duas células de entrada;
- uma transformação ou cálculo;
- um resultado em outra célula ou outra aba.

## Entrega

Salve o arquivo `.xlsm` com a macro funcionando e mostre ao professor o seu botão ou a execução pelo editor VBA.

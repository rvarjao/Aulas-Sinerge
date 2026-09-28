# Atividade — Tabela Dinâmica e Gráficos no Excel

Nesta atividade, vamos trabalhar com uma base de vendas já organizada e pronta para análise.

O objetivo não será limpar ou corrigir os dados.

O foco será aprender a:

- importar um arquivo CSV;
- transformar os dados em tabela;
- criar Tabelas Dinâmicas;
- analisar informações de forma resumida;
- criar gráficos comuns a partir dos dados;
- interpretar tendências;
- adicionar uma linha de tendência a um gráfico.

---

## Arquivo da atividade

Utilize o arquivo:

```text
vendas_adm_tabela_dinamica.csv
```

A base representa vendas realizadas por uma empresa durante o primeiro semestre de 2026.

Ela possui as seguintes colunas:

- ID da venda;
- data;
- vendedor;
- produto;
- categoria;
- quantidade;
- valor unitário;
- faturamento;
- cidade;
- forma de pagamento.

---

## Situação-problema

Você trabalha no setor administrativo de uma empresa.

A gerência recebeu uma base contendo todas as vendas realizadas durante o primeiro semestre de 2026.

Porém, analisar centenas de linhas individualmente não é uma forma eficiente de entender o desempenho da empresa.

Sua tarefa será transformar esses dados em informações mais fáceis de interpretar.

Ao final da atividade, você deverá conseguir responder perguntas como:

- quais categorias geraram mais faturamento?
- quais vendedores tiveram melhor desempenho?
- quais produtos venderam mais?
- quais cidades possuem maior volume de vendas?
- como o faturamento evoluiu durante o semestre?
- existe uma tendência de crescimento ou queda nas vendas?

---

# 1. Importar o arquivo CSV

Abra o Excel.

Depois, importe o arquivo:

```text
vendas_adm_tabela_dinamica.csv
```

Dependendo da versão do Excel, você poderá utilizar:

```text
Dados → De Texto/CSV
```

ou simplesmente abrir o arquivo diretamente.

Verifique se as colunas foram carregadas corretamente.

---

# 2. Transformar os dados em Tabela

Selecione os dados importados.

Depois utilize:

```text
Inserir → Tabela
```

ou o atalho:

```text
Ctrl + T
```

Confirme que a opção:

```text
Minha tabela tem cabeçalhos
```

está marcada.

A partir deste momento, os dados estarão organizados como uma Tabela do Excel.

---

# 3. Criar a primeira Tabela Dinâmica

Clique em qualquer célula da tabela.

Depois acesse:

```text
Inserir → Tabela Dinâmica
```

Crie a Tabela Dinâmica em uma nova planilha.

---

## Análise 1 — Faturamento por categoria

Configure a Tabela Dinâmica utilizando:

```text
Linhas:
Categoria
```

```text
Valores:
Soma de Faturamento
```

Observe os resultados.

### Responda

1. Qual categoria teve o maior faturamento?

2. Qual categoria teve o menor faturamento?

3. Existe uma diferença significativa entre as categorias?

---

# 4. Análise por vendedor

Crie uma nova Tabela Dinâmica.

Utilize:

```text
Linhas:
Vendedor
```

```text
Valores:
Soma de Faturamento
```

Ordene os valores do maior para o menor.

### Responda

1. Qual vendedor apresentou maior faturamento?

2. Qual apresentou menor faturamento?

3. Qual a diferença aproximada entre eles?

---

# 5. Quantidade vendida por produto

Crie outra Tabela Dinâmica.

Utilize:

```text
Linhas:
Produto
```

```text
Valores:
Soma de Quantidade
```

### Responda

1. Qual produto teve maior quantidade vendida?

2. O produto mais vendido em quantidade também é o que mais gera faturamento?

3. Por que quantidade vendida e faturamento podem apresentar resultados diferentes?

---

# 6. Vendas por cidade

Crie uma Tabela Dinâmica utilizando:

```text
Linhas:
Cidade
```

```text
Valores:
Soma de Faturamento
```

Ordene os valores do maior para o menor.

### Responda

1. Qual cidade apresentou maior faturamento?

2. Qual apresentou menor faturamento?

---

# 7. Forma de pagamento

Crie uma Tabela Dinâmica utilizando:

```text
Linhas:
Forma_Pagamento
```

```text
Valores:
Soma de Faturamento
```

Observe como as vendas estão distribuídas entre as diferentes formas de pagamento.

### Responda

Qual forma de pagamento representa o maior volume financeiro?

---

# 8. Criar gráficos

Agora vamos utilizar gráficos comuns do Excel para representar algumas das análises.

Não é necessário utilizar Gráfico Dinâmico.

Você poderá utilizar os resultados das Tabelas Dinâmicas como fonte dos gráficos.

---

## Gráfico 1 — Faturamento por categoria

Utilize os dados da análise:

```text
Faturamento por Categoria
```

Crie um:

```text
Gráfico de Colunas
```

O gráfico deve possuir:

- título;
- nome das categorias;
- valores de faturamento;
- organização visual adequada.

Sugestão de título:

```text
Faturamento por Categoria
```

---

# 9. Gráfico de desempenho dos vendedores

Utilize a Tabela Dinâmica com o faturamento por vendedor.

Crie um:

```text
Gráfico de Barras
```

Sugestão de título:

```text
Faturamento por Vendedor
```

Observe como esse formato facilita a comparação entre diferentes vendedores.

---

# 10. Evolução das vendas durante o semestre

Agora vamos analisar o comportamento das vendas ao longo do tempo.

Crie uma nova Tabela Dinâmica.

Utilize:

```text
Linhas:
Data
```

```text
Valores:
Soma de Faturamento
```

Agrupe as datas por:

```text
Meses
```

O resultado deverá apresentar o faturamento de:

```text
Janeiro
Fevereiro
Março
Abril
Maio
Junho
```

---

# 11. Criar gráfico de linha

Utilize os dados de faturamento mensal.

Crie um:

```text
Gráfico de Linha
```

Sugestão de título:

```text
Evolução do Faturamento no Primeiro Semestre
```

O eixo horizontal deverá representar os meses.

O eixo vertical deverá representar o faturamento.

---

# 12. Adicionar uma linha de tendência

Clique sobre a linha do gráfico.

Depois procure a opção:

```text
Adicionar Linha de Tendência
```

Escolha inicialmente:

```text
Linear
```

Observe a nova linha adicionada ao gráfico.

---

## Para que serve uma linha de tendência?

A linha de tendência ajuda a visualizar o comportamento geral dos dados.

Ela não representa exatamente os valores de cada mês.

Seu objetivo é mostrar uma direção geral.

Por exemplo:

```text
↗ tendência de crescimento
```

```text
↘ tendência de queda
```

ou

```text
→ comportamento relativamente estável
```

---

## Responda

1. A linha de tendência indica crescimento ou queda no faturamento?

2. Essa tendência significa que o próximo mês obrigatoriamente terá o mesmo comportamento?

3. Por que uma tendência deve ser utilizada com cuidado em análises administrativas?

---

# 13. Comparar gráfico e tabela

Observe a Tabela Dinâmica e o gráfico de linha.

Responda:

1. Qual deles permite visualizar os valores exatos com maior facilidade?

2. Qual deles permite perceber a evolução ao longo do tempo mais rapidamente?

3. Em uma apresentação para gestores, em quais situações você utilizaria uma tabela?

4. Em quais situações utilizaria um gráfico?

---

# 14. Desafio

Escolha uma informação diferente daquelas utilizadas anteriormente.

Pode ser, por exemplo:

- quantidade vendida por categoria;
- faturamento por cidade;
- faturamento por forma de pagamento;
- quantidade vendida por vendedor;
- faturamento por produto.

Crie:

1. uma Tabela Dinâmica;
2. um gráfico adequado;
3. um título para o gráfico;
4. uma conclusão de uma ou duas frases sobre o resultado.

---

# Checklist da atividade

Antes de concluir, verifique se você realizou:

- [ ] importação do arquivo CSV;
- [ ] criação da Tabela do Excel;
- [ ] Tabela Dinâmica por categoria;
- [ ] Tabela Dinâmica por vendedor;
- [ ] Tabela Dinâmica por produto;
- [ ] Tabela Dinâmica por cidade;
- [ ] análise por forma de pagamento;
- [ ] gráfico de colunas;
- [ ] gráfico de barras;
- [ ] análise mensal de faturamento;
- [ ] gráfico de linha;
- [ ] linha de tendência;
- [ ] respostas das questões;
- [ ] desafio final.

---

# Conclusão

Tabelas Dinâmicas são utilizadas para resumir grandes quantidades de dados rapidamente.

Os gráficos ajudam a transformar esses resultados em informações visuais.

Cada tipo de gráfico possui uma finalidade diferente:

```text
Colunas → comparar valores
```

```text
Barras → comparar categorias
```

```text
Linha → visualizar evolução no tempo
```

A linha de tendência permite observar a direção geral dos dados e pode ajudar na análise e no planejamento.

Porém, uma tendência não representa uma previsão garantida.

Os resultados sempre devem ser interpretados considerando o contexto da empresa e outras informações disponíveis.


# Envio da planilha

A planilha finalizada deve ser enviada pelo formulário do Google disponível em:
[28/09/2026 - Tabela Dinâmica e Gráficos no Excel](https://docs.google.com/forms/d/e/1FAIpQLScaveQzqz19mYTerVdNVShzEifzeEfLm2Au4PdXDQ4N7wy-hA/viewform?usp=publish-editor)


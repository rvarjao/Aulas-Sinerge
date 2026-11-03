# Atividade Avaliativa — Onde vou morar?

**Turma:** 1º ano — Administração  
**Ferramenta:** Google Sheets  
**Tema:** Pesquisa imobiliária, planejamento financeiro e pensamento analítico  
**Modalidade:** Individual ou em grupo, conforme orientação do professor  
**Entrega:** Link para a planilha do Google Sheets, com permissão de visualização  
**Programação:** Não é permitido utilizar VBA ou Google Apps Script.

## 1. Situação-problema

Você começou a trabalhar e pretende sair da casa da família. Agora precisa decidir **onde morar** e **como organizar suas despesas**. Há duas possibilidades:

- **Morar sozinho(a):** você paga integralmente aluguel, condomínio, IPTU e demais custos da moradia.
- **Dividir a moradia com amigos:** você divide despesas comuns entre os moradores, mas precisa considerar se o imóvel oferece espaço adequado para todos.

Sua tarefa é pesquisar imóveis **reais** para aluguel, organizar e comparar os dados no Google Sheets e recomendar a opção mais adequada. A decisão deverá ser sustentada por fórmulas, indicadores, gráficos e argumentos baseados nos dados.

**Pergunta central:** vale mais a pena morar sozinho(a) ou compartilhar um imóvel com amigos? Em qual imóvel, bairro e cidade?

## 2. Premissas do orçamento

Considere os seguintes dados fictícios, que deverão ficar registrados em células editáveis da planilha:

| Parâmetro | Valor inicial |
|---|---:|
| Salário líquido mensal de cada pessoa | R$ 3.500,00 |
| Percentual máximo de renda destinado à moradia | 30% |
| Número de moradores — cenário individual | 1 |
| Número de moradores — cenário compartilhado | 2 ou 3 (escolha e justifique) |

O limite inicial recomendado para moradia é **R$ 1.050,00 por pessoa por mês** (30% de R$ 3.500,00). Trata-se de um critério de análise da atividade, não de uma regra universal.

**Importante:** no cenário compartilhado, considere que cada amigo recebe o mesmo salário fictício. Custos compartilháveis podem ser divididos igualmente, mas as despesas individuais devem continuar individuais. A planilha deverá permitir modificar a quantidade de moradores e recalcular os valores automaticamente.

## 3. Etapa 1 — Pesquise 10 imóveis reais

Encontre **no mínimo 10 imóveis para alugar**, distribuídos por **pelo menos 3 bairros diferentes**. Você pode pesquisar em Curitiba e em municípios da região metropolitana.

Pesquise imóveis de diferentes tamanhos, incluindo alternativas adequadas para **morar sozinho(a)** e para **dividir com amigos**. Não basta escolher dez imóveis incompatíveis com um dos cenários.

Na aba **Imóveis**, registre no mínimo:

1. Identificação ou nome do imóvel;
2. Bairro;
3. Cidade;
4. Tipo (kitnet, apartamento, casa etc.);
5. Número de quartos;
6. Área em m²;
7. Aluguel mensal;
8. Condomínio mensal;
9. IPTU (valor e periodicidade: mensal ou anual);
10. Outras despesas mensais informadas no anúncio;
11. Distância aproximada até um ponto de referência comum (escola ou trabalho, por exemplo);
12. Link do anúncio;
13. Data em que o anúncio foi consultado;
14. Quantidade de moradores considerada adequada para o imóvel (1, 2 ou 3) e justificativa breve.

**Atenção:** utilize anúncios reais e informe as fontes. Não invente valores ausentes. Diferencie claramente **R$ 0,00** (sem cobrança) de **não informado**. Se uma informação não estiver disponível, indique essa ausência e mencione a limitação na análise. Padronize o IPTU para custo mensal antes de calcular os totais.

## 4. Etapa 2 — Construa a planilha

Crie **quatro abas**:

### Aba 1 — Orçamento

Registre o salário líquido, o percentual máximo da renda para moradia, o limite financeiro calculado e a quantidade de moradores do cenário compartilhado. Deixe as premissas identificadas para que possam ser alteradas sem editar as fórmulas.

### Aba 2 — Imóveis

Organize os dez imóveis em uma tabela: **uma linha por imóvel e uma coluna por informação**. Utilize títulos, filtros, formatação monetária, formato numérico, bordas ou cores discretas e padronização de dados.

Acrescente colunas calculadas para:

- Custo total mensal do imóvel (aluguel + condomínio + IPTU mensalizado + outras despesas comuns conhecidas);
- Valor do aluguel por m²;
- Custo mensal **por pessoa** ao morar sozinho(a);
- Custo mensal **por pessoa** ao dividir o imóvel com 2 ou 3 moradores;
- Percentual da renda comprometida em cada cenário;
- Diferença entre o custo por pessoa e o limite do orçamento;
- Classificação automática: **Dentro do orçamento** ou **Acima do orçamento**;
- Indicação de adequação: o imóvel possui quartos e condições razoáveis para o número de moradores previsto?

**Regra para a divisão:** distribua igualmente entre os moradores os custos comuns identificados. Se houver despesas pessoais não compartilhadas, não as divida. O cenário compartilhado só poderá ser recomendado para imóveis adequados ao número de pessoas escolhido.

### Aba 3 — Análise

Construa um resumo automático com:

- Menor e maior custo mensal total;
- Média do custo mensal dos dez imóveis;
- Menor aluguel por m²;
- Quantidade de imóveis dentro do orçamento para morar sozinho(a);
- Quantidade de imóveis dentro do orçamento por pessoa no cenário compartilhado;
- Comparação de custo por bairro ou cidade;
- Pelo menos **dois gráficos**, sendo um deles uma comparação entre morar sozinho(a) e dividir moradia.

Os gráficos devem ter títulos, rótulos legíveis e unidades quando necessário. **Não digite manualmente resultados que podem ser obtidos por fórmulas.**

### Aba 4 — Conclusão

Responda às perguntas com base nos dados calculados:

1. Qual imóvel tem o aluguel mais barato? Ele também tem o menor custo mensal total?
2. Qual apresenta o menor custo por metro quadrado?
3. Quantos imóveis cabem no orçamento para **morar sozinho(a)**?
4. Quantos cabem no orçamento **dividindo com amigos**?
5. Qual é a economia mensal por pessoa ao compartilhar o imóvel escolhido, em comparação com morar sozinho(a) nele?
6. Quais vantagens e desvantagens existem em dividir a moradia (privacidade, localização, tamanho, despesas e convivência)?
7. Qual imóvel e qual forma de moradia você escolheria? Justifique com **pelo menos três critérios**, incluindo valores calculados.
8. Quais dados não encontrados ou condições dos anúncios poderiam alterar sua decisão?

## 5. Fórmulas e recursos obrigatórios

A planilha deverá demonstrar o uso dos conteúdos estudados:

| Recurso | Aplicação esperada |
|---|---|
| Operações `+`, `-`, `*` e `/` | Somar despesas, calcular custo por pessoa e preço por m² |
| Referências relativas e absolutas (`$`) | Aplicar o mesmo salário e limite às diferentes linhas |
| `SE` | Classificar o imóvel conforme orçamento |
| `MÍNIMO` e `MÁXIMO` | Identificar menores e maiores valores |
| `MÉDIA` | Calcular a média de custos |
| `CONT.SE` ou `CONT.SES` | Contar imóveis dentro do orçamento ou em determinados bairros |
| Filtros e ordenação | Comparar regiões, tipos e preços |
| Formatação condicional | Destacar imóveis dentro e fora do orçamento |
| Gráficos | Comunicar os resultados da comparação |

**Observação:** o Google Sheets pode apresentar nomes e separadores de funções diferentes conforme as configurações de idioma da planilha. As fórmulas devem funcionar no arquivo entregue.

## 6. Teste da planilha

Depois de completar a pesquisa e a análise, realize estes testes:

1. Altere o salário de R$ 3.500,00 para **R$ 4.000,00**. Verifique se o limite, os percentuais e as classificações são atualizados.
2. Altere o número de moradores compartilhando o imóvel de **2 para 3** (ou de 3 para 2). Verifique se o custo por pessoa e os indicadores mudam automaticamente.
3. Restaure os valores iniciais e confira se os gráficos continuam corretos.

**Atenção:** um imóvel que fica mais barato com três moradores não é necessariamente adequado para três pessoas. O número de quartos e as condições de uso devem entrar na decisão.

## 7. Critérios de avaliação

| Critério | Peso |
|---|---:|
| Pesquisa de 10 imóveis reais e qualidade dos dados e fontes | 20% |
| Organização, tabelas, formatos e filtros | 15% |
| Fórmulas, referências e atualização automática dos cálculos | 30% |
| Comparação dos dois cenários, indicadores e gráficos | 20% |
| Conclusão fundamentada e pensamento analítico | 15% |
| **Total** | **100%** |

## 8. Regras e entrega

- Use **Google Sheets**; não entregue apenas imagens ou capturas de tela da planilha.
- Utilize **pelo menos 10 anúncios reais** e **3 bairros diferentes**.
- Compare obrigatoriamente **morar sozinho(a)** e **morar com amigos**.
- Utilize **fórmulas nas células** para os cálculos, não apenas resultados digitados.
- Não use **VBA, Google Apps Script** ou qualquer outro código de automação.
- Inclua os links e a data de consulta dos anúncios. Lembre-se de que os preços podem mudar.
- Organize os dados para que outra pessoa compreenda a análise sem precisar de explicações orais.
- Compartilhe o **link da planilha** com permissão de visualização, conforme orientação do professor.

**Objetivo final:** demonstrar que uma planilha pode funcionar como uma ferramenta para investigar dados, comparar alternativas, simular cenários e tomar decisões justificadas.

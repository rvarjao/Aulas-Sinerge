Power Query com o Top 10 da Netflix

## Contexto

Na aula anterior, importamos um arquivo CSV no Excel. Nesta atividade, vamos trabalhar com uma situação recorrente: toda semana, uma equipe recebe um novo arquivo com o ranking global de filmes da Netflix.

O objetivo é criar uma consulta que registre as etapas de preparação dos dados. Quando chegar o arquivo da semana seguinte, não será necessário repetir o tratamento: bastará substituir o CSV e atualizar a consulta.

## Dados utilizados

Os arquivos contêm dados reais do ranking **Global — Movies | English** publicado pela Netflix:

- arquivo inicial: semana encerrada em **30/08/2026**;
- arquivo de atualização: semana encerrada em **06/09/2026**.

Campos presentes no arquivo bruto:

| Campo | Significado |
| --- | --- |
| `week_ending` | Data final da semana analisada |
| `rank` | Posição do filme no ranking |
| `title` | Título do filme |
| `views` | Visualizações informadas pela Netflix |
| `runtime` | Duração no formato horas:minutos |
| `hours_viewed` | Total de horas assistidas |
| `territory` | Abrangência do ranking |
| `category` | Categoria analisada |
| `source_batch` | Identificador técnico do lote de importação |

Fonte: [Netflix Tudum — Top 10](https://www.netflix.com/tudum/top10). Dados consultados em 13/09/2026.

## Objetivos de aprendizagem

Ao final da atividade, você deverá ser capaz de:

- importar um CSV pelo Power Query;
- reconhecer as etapas aplicadas de uma consulta;
- renomear, remover e reorganizar colunas;
- definir tipos de dados;
- dividir uma coluna e criar uma coluna calculada;
- carregar o resultado em uma tabela do Excel;
- atualizar a tabela quando o arquivo de origem for substituído.

## Arquivos da atividade

```text
dados/
├── semana-inicial/
│   └── netflix_top10.csv
└── semana-atualizacao/
    └── netflix_top10.csv
```

Comece usando somente o arquivo da pasta `semana-inicial`. A pasta `semana-atualizacao` será usada no final.

## Parte 1 — Importar o CSV

1. Abra uma pasta de trabalho vazia no Excel.
2. Acesse **Dados → Obter Dados → De Arquivo → De Texto/CSV**.
3. Selecione `dados/semana-inicial/netflix_top10.csv`.
4. Na janela de pré-visualização, confirme:
   - origem do arquivo: **UTF-8**;
   - delimitador: **vírgula**;
   - detecção de tipos: pode permanecer automática neste primeiro momento.
5. Clique em **Transformar Dados**.

## Parte 2 — Conhecer o Editor do Power Query

Antes de transformar os dados, localize:

- o painel **Consultas**, à esquerda;
- a pré-visualização da tabela, no centro;
- o painel **Configurações da Consulta**, à direita;
- a seção **Etapas Aplicadas**.

Renomeie a consulta para `Top 10 Netflix`.

Observe que cada transformação feita a partir de agora aparecerá como uma nova etapa. Para compreender esse funcionamento, clique nas etapas anteriores e depois retorne à última etapa.

## Parte 3 — Limpar e organizar os dados

### 3.1 Renomear as colunas

Renomeie as colunas conforme a tabela:

| Nome original | Novo nome |
| --- | --- |
| `week_ending` | `data_final_semana` |
| `rank` | `ranking` |
| `title` | `titulo` |
| `views` | `visualizacoes` |
| `runtime` | `duracao` |
| `hours_viewed` | `horas_assistidas` |
| `territory` | `territorio` |
| `category` | `categoria` |

### 3.2 Remover uma coluna técnica

Selecione a coluna `source_batch` e use **Página Inicial → Remover Colunas**.

Essa coluna identifica o lote de origem, mas não é necessária para a análise.

### 3.3 Definir os tipos de dados

Configure os tipos abaixo:

| Coluna | Tipo |
| --- | --- |
| `data_final_semana` | Data |
| `ranking` | Número inteiro |
| `titulo` | Texto |
| `visualizacoes` | Número inteiro |
| `duracao` | Texto |
| `horas_assistidas` | Número inteiro |
| `territorio` | Texto |
| `categoria` | Texto |

Confira se nenhuma etapa apresenta **Erro** após a conversão.

### 3.4 Transformar a duração em minutos

1. Selecione a coluna `duracao`.
2. Acesse **Transformar → Dividir Coluna → Por Delimitador**.
3. Use `:` como delimitador e divida em duas colunas.
4. Renomeie as novas colunas para:
   - `duracao_horas`;
   - `duracao_minutos_parte`.
5. Defina as duas colunas como **Número inteiro**.
6. Acesse **Adicionar Coluna → Coluna Personalizada**.
7. Crie a coluna `duracao_minutos` com a fórmula:

```powerquery
[duracao_horas] * 60 + [duracao_minutos_parte]
```

8. Defina `duracao_minutos` como **Número inteiro**.
9. Remova `duracao_horas` e `duracao_minutos_parte`.

## Parte 4 — Finalizar e carregar

1. Organize as colunas nesta ordem:

```text
data_final_semana
ranking
titulo
visualizacoes
duracao_minutos
horas_assistidas
territorio
categoria
```

2. Ordene `ranking` do menor para o maior.
3. Acesse **Página Inicial → Fechar e Carregar**.
4. Confirme que o Excel criou uma tabela com dez filmes.
5. Formate `visualizacoes` e `horas_assistidas` com separador de milhares.

## Parte 5 — Atualizar a consulta

Agora vamos simular a chegada do ranking da semana seguinte.

1. Salve a pasta de trabalho do Excel.
2. Na pasta `semana-inicial`, renomeie o arquivo atual para `netflix_top10_backup.csv`.
3. Copie `dados/semana-atualizacao/netflix_top10.csv` para a pasta `semana-inicial`.
4. Volte ao Excel.
5. Acesse **Dados → Atualizar Tudo**.

O Power Query deverá executar novamente todas as etapas aplicadas, agora sobre o novo conteúdo.

## Verificação do resultado

Depois da atualização, confira:

- a data final da semana mudou de `30/08/2026` para `06/09/2026`;
- o primeiro lugar mudou de **Grand Theft Auto VI: An Extended Look** para **The Whisper Man**;
- **The Whisper Man** passou de 23.200.000 para 33.400.000 visualizações;
- a tabela continua com dez registros e a duração permanece em minutos.

Se a atualização não funcionar, abra **Dados → Consultas e Conexões**, edite a consulta e confira a primeira etapa, chamada normalmente de **Fonte**. O caminho deve continuar apontando para `semana-inicial/netflix_top10.csv`.

## Questões para responder

1. Qual é a função do painel **Etapas Aplicadas**?
2. Por que foi possível atualizar a tabela sem repetir manualmente as transformações?
3. Quais filmes permaneceram no Top 10 nas duas semanas?
4. Qual foi a diferença de visualizações de **The Whisper Man** entre uma semana e outra?
5. O que aconteceria se o arquivo atualizado tivesse uma coluna com nome diferente?

## Desafio opcional

Adicione uma coluna personalizada chamada `horas_por_milhao_de_visualizacoes`:

```powerquery
[horas_assistidas] / ([visualizacoes] / 1000000)
```

Depois, formate a coluna como número decimal e observe como a duração de cada filme influencia o total de horas assistidas.

## Próxima aula sugerida

Na próxima etapa, mantenha os dois CSVs sem substituir nenhum arquivo e use **Dados → Obter Dados → De Arquivo → De Pasta**. O Power Query poderá combinar várias semanas em uma única tabela, permitindo comparar a evolução dos filmes ao longo do tempo.

## Observação para o professor

Tempo sugerido: **50 a 60 minutos**.

- 10 min: retomada da importação de CSV e apresentação do problema recorrente;
- 10 min: interface do Editor do Power Query;
- 20 min: transformações;
- 10 min: carregamento e atualização;
- tempo restante: verificação e questões.

Os valores de ranking, visualizações, duração e horas assistidas foram mantidos conforme a publicação oficial. Os nomes técnicos das colunas e o campo `source_batch` foram preparados para fins didáticos.

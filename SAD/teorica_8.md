# Sistemas de Apoio à Decisão

## Aula Teórica 8

Uma das abordagens mais comuns no desenvolvimento de sistemas de apoio à decisão é a **Modelação Dimensional**, especialmente útil para criar **Data Warehouses**.

### O que é Modelação Dimensional?

A **Modelação Dimensional** é uma técnica de design de bases de dados voltada para a análise de dados, que visa facilitar o acesso a informações relevantes de uma maneira intuitiva e fácil de consultar. Esse tipo de modelagem organiza os dados em um formato que torna a análise mais rápida e eficaz, frequentemente por meio de **esquemas estrela** (Star Schema) ou **esquemas floco de neve** (Snowflake Schema).

### Elementos da Modelação Dimensional

A modelação dimensional baseia-se em duas estruturas principais:

- **Tabela de Fatos**: Contém dados quantitativos, como vendas, lucros ou quantidades, representando eventos ou transações. É chamada de "fato" porque esses dados representam fatos ou ocorrências específicas que queremos analisar.

- **Tabela de Dimensões**: Contém dados qualitativos ou descritivos, como **data**, **produto**, **cliente** e **local**. As dimensões permitem a análise dos fatos sob diferentes perspectivas, como a análise de vendas por período de tempo, localização ou categoria de produto.

### ETL - Extração, Transformação e Carga

Para que a modelação dimensional seja eficiente, é essencial ter um processo de **ETL (Extract, Transform, Load)** robusto.

### Benefícios da Modelação Dimensional em Sistemas de Apoio à Decisão

A modelação dimensional facilita a criação de relatórios e dashboards intuitivos e interativos. Seus principais benefícios incluem:

- **Acesso rápido aos dados**: A estrutura otimizada para consulta permite respostas rápidas a consultas analíticas complexas.
- **Simplicidade**: O design intuitivo facilita o entendimento do modelo por usuários de negócios, sem necessidade de profundo conhecimento técnico.
- **Flexibilidade de análise**: Permite que os dados sejam analisados em diferentes perspectivas e níveis de granularidade.

### Estruturas de Modelação Dimensional

**Esquema Estrela (Star Schema)**:

- **Estrutura**: Uma tabela de fatos central com dados quantitativos (ex: vendas) conectada a várias tabelas de dimensões (ex: produto, cliente, data), que são desnormalizadas.
- **Vantagem**: Simples e rápido para consultas, pois há menos junções entre tabelas.
- **Desvantagem**: Alta redundância nas dimensões, ocupando mais espaço de armazenamento.

**Esquema Floco de Neve (Snowflake Schema)**:

- **Estrutura**: Similar ao Esquema Estrela, mas com tabelas de dimensões normalizadas, dividindo-as em várias subdimensões (ex: a dimensão “Produto” pode ter uma subdimensão “Categoria”).
- **Vantagem**: Menor redundância de dados e economia de espaço.
- **Desvantagem**: Mais complexo e com mais junções, o que pode reduzir a performance das consultas.

**Esquema Constelação (Constellation Schema)**:

- **Estrutura**: Várias tabelas de fatos compartilham dimensões comuns, formando uma rede (ou constelação) de tabelas (ex: uma tabela de fatos de vendas e outra de inventário compartilhando dimensões como produto e data).
- **Vantagem**: Permite a análise de múltiplos processos de negócio.
- **Desvantagem**: Complexo de implementar e consultar, devido ao aumento de tabelas e relacionamentos.

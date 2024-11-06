# Sistemas de Apoio à Decisão

## Introdução aos SAD

### Introdução

- **Processo de decisão**
  - Organizações dependem da utilização eficaz de informações para apoiar a tomada de decisões.
  - A maioria dos sistemas informáticos não atende plenamente às necessidades de informação dos tomadores de decisão.
  - É necessário criar um ambiente apropriado para armazenamento e gerenciamento eficiente dos dados produzidos nas operações diárias das organizações.
  - O processo de tomada de decisão envolve a escolha de uma opção entre várias alternativas, seguindo etapas estabelecidas que levam à resolução de um problema.
  - Esse processo inclui várias etapas, como:
    - Recrutamento de pessoal
    - Gestão de avaliações de desempenho
  - **Etapas do processo de decisão**
    - Análise e identificação da situação
    - Desenvolvimento de alternativas
    - Comparação das alternativas
    - Classificação dos riscos de cada alternativa
    - Escolha da melhor alternativa
    - Execução e avaliação dos resultados

### Sistemas de Apoio à Decisão

- **Conceito**
  - Um sistema de apoio à decisão (SAD) é um sistema complexo que possibilita:
    - Acesso às bases de dados da organização
    - Modelagem de problemas
    - Realização de simulações
    - Interface amigável para o usuário
  - Auxilia executivos e gestores no processo de tomada de decisão.

- **Características**
  - Projetados para resolver problemas complexos e pouco estruturados.
  - Integram modelos e técnicas analíticas com funções de processamento de dados tradicionais, como acesso e recuperação de informações.
  - Devem ser interativos, fáceis de usar e possuir uma interface amigável.

- **Principais características dos SADs**
  - Otimização na entrada de dados
  - Estruturas de dados complexas
  - Dados distribuídos por múltiplos sistemas, com possíveis inconsistências entre eles
  - Baixo volume de dados por transação

- **Modelo lógico de dados**
  - O Modelo Entidade-Relacionamento (ER):
    - Reduz a redundância dos dados
    - Facilita a entrada de dados
    - Cria várias tabelas que, visualmente, podem parecer similares no diagrama
    - É complexo e pode ser de difícil compreensão devido ao tamanho e detalhamento dos diagramas

### Análise de Dados em Sistemas Operacionais: Evolução

- Os departamentos de informática geram relatórios, que são entregues após um certo tempo.
- Com o surgimento dos computadores pessoais, os tomadores de decisão passaram a poder analisar dados diretamente.
- Introdução dos _Data Warehouses_.

### Análise de Dados em Sistemas Operacionais: Problemas

- Esforços duplicados
- Dados podem não ser extraídos simultaneamente
- Algoritmos divergentes
- Atributos podem ter significados distintos
- Falta de regras que assegurem a qualidade dos dados

### Sistemas Analíticos

#### Data Warehouses

> “A Data Warehouse is a subject-oriented, integrated, time-variant, non-volatile collection of data in support of management’s decision-making process.” – Bill Inmon

> “The Data Warehouse is not just data, but also a set of tools to query, analyze, and present information.” – Ralph Kimball

- **Características dos Data Warehouses**
  - Armazenamento de grandes volumes de dados
  - Foco em finalidades específicas
  - Integração e consistência dos dados
  - Dados organizados por dependência temporal
  - Dados não voláteis
  - Estruturas otimizadas para consultas

#### Características dos Data Warehouses (DWs)

- **Foco em finalidades específicas**
  - As bases de dados operacionais são orientadas a processos e funções específicas, como operações de levantamento e depósito.
  - _Data Warehouses_ são organizados para atender a principais objetivos da empresa, como informações sobre clientes, produtos, ou produtividade.
  - Excluem informações irrelevantes para o processo de decisão.

- **Integração e consistência**
  - Nas bases de dados operacionais, dados semelhantes podem ser armazenados em formatos diferentes.
  - É necessária uma integração para dar consistência aos dados extraídos das bases operacionais antes de serem armazenados no _Data Warehouse_.
  - Consistência pode incluir:
    - Padrões para atribuição de nomes
    - Medidas uniformes para variáveis
    - Definições físicas consistentes dos atributos
  - Consistência garante que duas pessoas recebam a mesma informação ao fazerem o mesmo pedido em momentos distintos.

- **Dependência temporal dos dados**
  - Um _Data Warehouse_ é explicitamente organizado como uma série temporal.
    - Dados são coletados e armazenados ao longo do tempo.
  - Estruturas de chave incluem informações temporais.
  - Permite análise do passado para previsões futuras.

- **Não volatilidade**
  - Dados no _Data Warehouse_ não são alterados após o carregamento inicial.
  - Uma vez carregados, os dados só podem ser consultados.

- **Estruturas otimizadas para consulta**
  - Dados são organizados de modo a otimizar a velocidade das consultas, frequentemente utilizando desnormalização do modelo físico.

#### Comparação: Bases de Dados Operacionais vs. Data Warehouses

- **Bases de Dados Operacionais**
  - Objetivos operacionais
  - Acesso de leitura/escrita
  - Acesso por transações pré-definidas
  - Consultas de poucos registros por vez
  - Dados atualizados em tempo real
  - Estrutura otimizada para atualizações frequentes
  - _Event-driven_: processos geram dados

- **Data Warehouses**
  - Registro histórico
  - Acesso apenas de leitura
  - Acesso por consultas _ad-hoc_ e relatórios
  - Envolvem muitos registros em cada acesso
  - Carregamento periódico de novos dados
  - Estrutura otimizada para consultas complexas
  - _Data-driven_: dados geram respostas e perguntas

## OLAP e Data Warehousing

### Data Warehouse

- **Definição**: “Um Data Warehouse é uma coleção de dados orientada por assunto, integrada, variante no tempo e não volátil, usada para suportar a tomada de decisão gerencial.”
  - Trata-se de uma base de dados separada das bases de dados operacionais
  - Fornece uma plataforma robusta com dados históricos consolidados para análise

### Data Warehousing

- **O que é _Data Warehousing_?**
  - Primeiramente, é um processo
    - Um processo é uma sequência organizada de atividades, executadas de forma sistemática, por pessoas com responsabilidades definidas
  - _Data Warehousing_ é o processo de construção e uso de _Data Warehouses_

### OLAP

- **O que é OLAP?**
  - OLAP (_OnLine Analytical Processing_) é um termo introduzido em 1993 por Edgar Codd em um “white paper”
  - Refere-se ao processo interativo de criação, análise e relatórios a partir de dados
  - Permite a análise em tempo real de grandes volumes de dados para suporte à decisão
  - Os dados são manipulados como se estivessem armazenados em um _array_ multidimensional, com estruturas de armazenamento multidimensionais (cubos de dados)
  - O OLAP oferece uma agregação de dados em inúmeras formas, viabilizando diversos agrupamentos

- **Exemplo: Armazém**

  | Fornecedor | Produto | Quantidade |
  | ---------- | ------- | ---------- |
  | F1         | P1      | 300        |
  | F1         | P2      | 200        |
  | F2         | P1      | 300        |
  | F2         | P2      | 400        |
  | F3         | P2      | 200        |
  | F4         | P2      | 200        |

  - Análises possíveis:
    - Quantidade total em estoque
    - Quantidade total por fornecedor
    - Quantidade total por produto
    - Quantidade total por fornecedor e produto
  - Necessário realizar 4 consultas – uma solução com limitações

### Cubo de Dados

- **O que é um cubo de dados?**
  - Estrutura que armazena dados de forma multidimensional, facilitando e agilizando a análise
  - Quando possui mais de três dimensões, é chamado de _hipercubo_

- **Exemplo**: Implementações 2D e 3D com dados de quantidade vendida

- **Variáveis no Cubo de Dados**
  - Variáveis independentes (dimensões): Data, Loja, Produto
  - Variável dependente: Quantidade vendida, armazenada nas células do cubo

- **Conceito de _Cuboid_**
  - _n-D Cuboid_: Nível mais baixo de agregação, chamado de _base cuboid_
  - _0-D Cuboid_: Nível mais alto de agregação, chamado de _apex cuboid_
  - Um grafo de _cuboids_ forma o cubo de dados completo

### Operações OLAP

- **Operações Comuns em Cubo de Dados**
  - _Drilling_, _Rolling_, _Slicing_, _Dicing_, _Pivoting_
  - Realizadas instantaneamente em cubos de dados, enquanto podem ser demoradas em bases relacionais

- **_Drill-Down_ e _Roll-Up_**
  - _Drill-Down_: Aumenta o nível de detalhe, descendo de um nível superior a um nível mais granular
  - _Roll-Up_: Reduz o nível de detalhe, agregando informações em níveis superiores

- **_Slicing_**
  - Consiste em “cortar” o cubo ao longo de uma ou mais dimensões, fixando valores específicos em uma dimensão

- **_Dicing_**
  - Define um subcubo ao limitar valores em uma ou mais dimensões, permitindo focar em dimensões relevantes

- **_Pivoting_**
  - Permite rotacionar o cubo para visualização de diferentes perspectivas, facilitando a visualização em 2D

- **Outras Operações OLAP**
  - _Drill-Through_: Permite explorar detalhes fora do cubo, ao nível dos registros
  - _Drill-Across_: Consultas que cruzam dados de diferentes _data marts_
  - _Ranking_ e _Filtering_: Permitem ordenação e aplicação de filtros nos dados

### Integração OLAP e SQL

- **Dados no Mundo Real**
  - Dados são geralmente armazenados em bases relacionais; é possível representar _n_ dimensões em tabelas 2D?
  - OLAP pode ser combinado com SQL usando extensões como CUBE e ROLLUP

- **ROLLUP**
  - Calcula um caminho através do grafo de cubóides, gerando agregações em ordens definidas no GROUP BY

- **CUBE**
  - Calcula o grafo completo de cubóides, sem importância para a ordem de agrupamento

### Modelos de Armazenamento OLAP: ROLAP, MOLAP e HOLAP

- **ROLAP (_Relational OLAP_)**
  - OLAP sobre bancos de dados relacionais, com alta escalabilidade, utilizando extensões SQL

- **MOLAP (_Multidimensional OLAP_)**
  - OLAP sobre bancos de dados multidimensionais, oferece processamento rápido, mas com menor capacidade de armazenamento devido à esparsidão dos dados

- **HOLAP (_Hybrid OLAP_)**
  - Combinação de ROLAP e MOLAP, oferecendo rapidez e economia de espaço

### Comparação OLTP vs. OLAP

|                   | OLTP            | OLAP                   |
| ----------------- | --------------- | ---------------------- |
| Objetivo chave    | Disponibilidade | Performance            |
| Tamanho comum     | Mega a GB       | Giga a Tera/Petabyte   |
| Granularidade     | Atômico         | Atômico e agregado     |
| Origem dos dados  | Interna         | Interna e externa      |
| Atualizações      | Em tempo real   | Batch                  |
| Período dos dados | Atual           | Histórico              |
| Consultas         | Pré-definidas   | Pré-definidas e ad hoc |
| Atividade         | Operacional     | Analítica              |
| Utilizadores      | Muitos          | Poucos                 |
| Modelo de dados   | Normalizado     | Desnormalizado         |

## Processo de Data Warehousing

### Metodologias

#### _Corporate Warehouse_

- **Fonte**: _Building the Data Warehouse_ de B. Inmon, 1990.
- **Descrição**: Estrutura que coleta dados de várias fontes heterogêneas em uma base de dados central, detalhada e temporal.
- **Características**:
  - Abordagem _top-down_.
  - Dados estruturados.
  - Metodologia _Corporate Information Factory_ (2002).
  - Modelo de Dados Empresarial (complexo).
  - Integração via modelo de dados corporativo.
  - _Data marts_ são agregados.

#### _Dimensional Design_

- **Fonte**: _The Data Warehouse Toolkit_ de R. Kimball, 1996.
- **Descrição**: Estrutura que organiza diferentes bases de dados (_data marts_) conforme os processos de negócio.
- **Características**:
  - Abordagem _bottom-up_.
  - Dados estruturados.
  - Metodologia _Business Dimensional Lifecycle_ (2002).
  - Modelo dimensional.
  - Integração via dimensões conformes.
  - _Data marts_ ao nível atômico.
  - Adotado nesta unidade curricular.

#### Outras Metodologias

- **_Data Vault_**: Criado por Daniel Linstedt (2000), com uma abordagem híbrida (normalização e modelagem dimensional) que oferece resiliência e escalabilidade.
- **_Data Lake_**: James Dixon (2011), repositório para grandes quantidades de dados em formato natural.
- **_Data Lakehouse_**: Desenvolvido pela Databricks (2020), combina características de _data lakes_ e _data warehouses_.

### Arquitetura do Data Warehouse

#### Sistemas Fonte

- Sistemas que registram operações críticas do negócio.
- **Características**:
  - Alta disponibilidade.
  - Poucos registros por consulta.
  - Pouca retenção de dados históricos.
  - Consultas extensas podem impactar a performance.

#### Área de Tratamento de Dados (_Data Staging Area_)

- **Processo de Extração**: Selecione e copie os dados da fonte para a área de tratamento (_data staging_).
  - Exportação e extração de dados.
  - Diferenciação entre extração inicial e incremental.

- **Processo de Transformação**: Inclui verificação de qualidade e transformação de dados.
  - Limpeza de dados e eliminação de campos desnecessários.
  - Combinação de dados de diferentes fontes.

- **Processo de Carregamento**: Após a transformação, os dados são carregados no data warehouse em massa (_bulk loading_) e indexados para consultas mais rápidas.

### Data Marts e Metadados

#### Data Marts

- Subconjunto lógico de um data warehouse, relacionado a processos específicos de negócio.
- **Integração**: A união de _data marts_ conformes compõe o _data warehouse_.

#### Metadados

- Descrevem os dados do data warehouse, incluindo:
  - Estrutura, formato, e relações com dados das fontes originais.
  - Origem e responsáveis pelos dados.

### Utilizadores Finais

#### Aplicações Cliente

- Ferramentas analíticas para consultas e análise de dados no data warehouse.
  - **Exigências**: Facilidade de uso e suporte a consultas _ad hoc_ com visualização em tabelas, gráficos e _dashboards_.

#### Aplicações para Análise de Dados

- Ferramentas que oferecem modelos preditivos, de agrupamento e classificação, incluindo _data mining_.

### Construção do Data Warehouse

#### Metodologia de Ralph Kimball

- **Etapas Principais**:
  1. Identificar objetivos.
  2. Definir infraestrutura.
  3. Analisar dados das fontes.
  4. Modelar dados do _data warehouse_.
  5. Definir regras de mapeamento.
  6. Extrair, integrar e purificar dados.
  7. Testar, otimizar e avaliar a eficácia.

#### Etapas Detalhadas

1. **Objetivos**: Compreender o processo de negócio e os objetivos da empresa, incluindo usuários e uso da informação.
2. **Infraestrutura**: Organizar equipe, ferramentas e métodos de trabalho para execução do projeto.
3. **Modelo de Dados das Fontes**: Identificar dados fonte com ferramentas de _reverse engineering_, considerando fontes externas.
4. **Modelo de Dados do Data Warehouse**: Desenvolver o modelo de negócio, identificar processos e granularidade de dados.
5. **Mapeamento de Dados**: Definir regras para integração e limpeza dos dados, documentando o processo.
6. **Extração e Integração**: Implementar ferramentas para garantir a qualidade do mapeamento.
7. **Otimização e Avaliação**: Testar ferramentas de exploração de dados, aprimorar consultas e administrar o _data warehouse_.

## Extração de Dados

### Introdução

**Processo ETL**:

- O processo ETL (Extração, Transformação e Carregamento) permite a migração dos dados dos sistemas fonte para o Data Warehouse, aplicando as transformações necessárias em termos de formato e conteúdo.
- Não se trata apenas de uma justaposição de três processos (Extração, Transformação e Carregamento); há uma interdependência entre eles, embora possam ser analisados separadamente para fins pedagógicos.
- O ETL é frequentemente apontado como um dos maiores desafios dos Data Warehouses, representando cerca de 70% dos custos de construção e manutenção.
- A área de Tratamento de Dados (DSA) é responsável por esses processos, funcionando como uma "cozinha de dados" em uma analogia com um restaurante.

### Processo de Extração

**Objetivo**:

- A extração de dados consiste em identificar, selecionar e copiar os dados dos sistemas fonte para a área de tratamento de dados (DSA).
- Há duas abordagens principais:
  - **Exportação de dados**: Converte os dados em um arquivo para leitura posterior na DSA.
  - **Extração direta**: Utiliza código específico para transferir diretamente os dados para a DSA.

- A cooperação dos sistemas fonte é essencial para o processo de extração, que pode ser dividido em:
  - **Primeira extração**: Cópia inicial de todos os dados.
  - **Extrações incrementais**: Inclui apenas dados novos ou modificados.

**Análise dos Sistemas Fonte**:

- Analisar o Diagrama de Entidade-Relacionamento (DER) dos sistemas fonte, caso exista. Em sua ausência, realizar engenharia reversa da base de dados operacional usando ferramentas de ETL.
- Consultar as descrições das tabelas e colunas da base de dados (mesmo que desatualizadas) e verificar alterações junto do responsável pela base de dados.

**Análise de Conteúdo dos Dados**:

- Identificar e corrigir anomalias, como:
  - Valores nulos em chaves estrangeiras e colunas críticas.
  - Formatação inconsistente de datas (ex.: "10-10-2024", "2024/10", "10 de outubro de 2024").

**Extração de Dados de Diferentes Fontes**:

- O processo deve integrar dados de fontes variadas, como bases de dados operacionais, arquivos CSV, XML, JSON, registros de web logs e ERPs.
- Situações de integração são comuns, como em fusões empresariais.

**Extração de Dados Dinâmicos**:

- Técnicas de Captura de Alterações de Dados (CDC) permitem identificar modificações em dados.
- O planejamento para capturar dados que mudam deve ser feito antes do primeiro carregamento.

### Técnicas de CDC

**_Timestamps_**:

- Algumas bases de dados permitem registrar a data/hora de alteração de cada registro, facilitando a detecção de mudanças.
- Essa técnica suporta extrações incrementais de maneira integrada.

**_Triggers_**:

- Simulam a atualização de registros com _timestamps_. Cada registro inserido ou modificado é marcado com a data/hora da alteração.
- Para implementar:
  - Adicionar uma coluna de data e hora nas tabelas do sistema fonte.
  - Criar _triggers_ para disparar a atualização a cada INSERT/UPDATE.
  - Criar tabelas correspondentes na DSA e registrar a data do último registro extraído.

**Partições**:

- Dividir as tabelas em partições temporais, como uma partição por dia, para suportar extrações incrementais.

**Processo de Eliminação**:

- Em cada extração, copia-se todos os dados fonte para a DSA. O sistema retém uma cópia da extração anterior para comparação.
- Essa técnica é adequada para arquivos como CSV e JSON e pode ser usada quando técnicas incrementais não são viáveis.
- Para implementar:
  - Criar duas tabelas na DSA (_table_new_ e _table_old_).
  - A extração atual é armazenada em _table_new_, enquanto _table_old_ armazena os dados da extração anterior.

**Etapas Típicas do Algoritmo do Processo de Eliminação**:

1. Limpar a _table_old_.
2. Copiar os dados da _table_new_ para a _table_old_.
3. Limpar a _table_new_.
4. Extrair novos dados da fonte para a _table_new_.

## Transformação de Dados

### Introdução

**Processo ETL**:

- O processo ETL (Extração, Transformação e Carga) permite migrar dados dos sistemas fonte para o _Data Warehouse_, realizando as transformações necessárias para que os dados fiquem no formato e conteúdo adequado para análise.
- Na _Data Staging Area_ (DSA), são executados processos que extraem, transformam e carregam dados de diversas fontes para alimentar o _Data Warehouse_ de maneira consistente e precisa.

### Processo de Transformação

**Introdução**:

- Diferente do processo de extração, que é principalmente uma movimentação e formatação dos dados, o processo de transformação visa modificar e preparar os dados para análise.
- Após a extração, a transformação é essencial para garantir a limpeza e conformidade dos dados.
- As principais atividades no processo de transformação incluem:
  - Verificação da qualidade dos dados
  - Aplicação das transformações necessárias

- Existem várias abordagens para transformar dados de fontes diferentes, incluindo:
  - Limpeza de dados
  - Remoção de campos irrelevantes
  - Integração de dados de fontes diversas

- Durante a transformação, são gerados metadados que registram o processo e permitem monitorar a qualidade e as alterações feitas nos dados desde a extração até a entrega ao usuário final.

### Qualidade dos Dados

**Introdução**:

- A qualidade dos dados deve ser garantida em cada etapa do processo ETL:
  - E -> TL (Extração para Transformação e Carga)
  - ET -> L (Transformação para Carga)
- Sempre que possível, os problemas de qualidade devem ser corrigidos nos sistemas fonte, pois as correções realizadas na DSA são temporárias e podem resultar em inconsistências se não forem propagadas para a origem.
- Dados de baixa qualidade podem comprometer a eficiência do _Data Warehouse_.

- Os critérios de qualidade dos dados incluem:
  - Correção: os dados representam uma versão oficial e confiável.
  - Clareza: o significado dos dados é inequívoco e compreensível.
  - Consistência: a representação dos dados segue uma convenção única.
  - Completude: todos os campos esperados têm dados preenchidos, e o número de registros é o adequado.

- As atividades para garantir a qualidade dos dados envolvem:
  - Detecção, registro e análise de erros.

**Correção**:

- A correção garante que os valores dos dados estejam alinhados com uma versão oficial, mas atenção: um dado "correto" não necessariamente representa a verdade, pois pode haver limitações nos sistemas fonte.

**Clareza**:

- A clareza assegura que cada dado possui um único significado, reduzindo ambiguidade e facilitando a interpretação correta dos dados.

**Consistência**:

- A consistência significa manter uma representação uniforme dos dados, essencial para a confiabilidade e a precisão das análises.

**Completude**:

- Para garantir a completude, os valores esperados nos campos devem estar preenchidos e a quantidade de registros deve ser a correta.

### Gestão de Erros

**Atitudes perante o erro**:

- Há diferentes opções ao lidar com erros:
  - Ignorá-los
  - Interromper o processo
  - Corrigir erros
- A escolha da ação deve ser informada e baseada no impacto da decisão no processo.

- O controle de qualidade inclui _checkpoints_ e relatórios, conhecidos como _screens_, onde são registrados todos os erros identificados.

**Deteção de Erros**:

- Para assegurar a qualidade, são realizados testes de qualidade abrangentes, acompanhados de metadados sobre as fontes de dados.
- _Screens_ são responsáveis por aplicar critérios de qualidade e realizar testes como:
  - Verificar se as colunas estão preenchidas.
  - Confirmar se os valores extraídos e o total de registros correspondem ao esperado.

**Registo de Erros**:

- Os erros são registrados detalhadamente em infraestruturas específicas:
  - Registro individual e agrupado dos erros.
- Arquivos de _Log_ são mantidos para cada execução do ETL.
- O _Transformation Error Logger_ (TEL) armazena o histórico de erros, permitindo análises posteriores e decisões mais informadas.

**Análise de Erros**:

- Realiza-se uma análise estatística dos erros, avaliando aspectos como:
  - Evolução da qualidade dos dados.
  - Identificação das fontes com mais problemas.
  - _Screens_ que demandam mais tempo.
  - Avaliação de _screens_ que talvez já não sejam necessários.

### Conflitos e Prioridades

- A qualidade dos dados é definida pela exaustividade, transparência, velocidade e correção.
- Os conflitos mais comuns são:
  - Exaustividade vs. Rapidez: maior quantidade de dados pode reduzir a velocidade de processamento.
  - Correção vs. Transparência: ênfase na transparência pode exigir reengenharia excessiva, enquanto correções extensivas podem criar dependências no ETL e gerar novos problemas.

### Limpeza de Dados

**Dados “sujos”**:

- Os dados sujos incluem:
  - Valores incorretos, dados ausentes, duplicações, significados ambíguos, dados contraditórios e dados que violam regras de integridade (referencial, temporal, etc.).
- O processo de limpeza resolve esses problemas aplicando correções e padronizações automáticas e, quando necessário, manuais.

### Transformação de Dados

**Integração de dados**:

- É a combinação de dados de vários sistemas fonte para estruturar o _Data Warehouse_ de forma mais simples e consolidada.
- Durante a integração, podem surgir dificuldades como a falta de chaves primárias ou dados ausentes.

**Conformidade**:

- A conformidade lida com:
  - Dados que deveriam estar relacionados, mas não estão devido à ausência de chaves unívocas.
  - Dados que foram relacionados erroneamente.

**Tipos de transformações**:

- As transformações podem ser ao nível do registro (seleção, junção e agregação) ou do campo (transformações de um para um ou muitos para um).

**Correção de erros**:

- A correção ideal é feita nos sistemas fonte. Corrigir erros temporariamente nas transformações pode ser ineficaz e problemático.

### Mapa Lógico de Dados

**Definição do Mapa**:

- Um mapa lógico de dados detalha as relações entre as fontes de dados e os destinos no _Data Warehouse_, servindo como guia para o fluxo de dados e assegurando uma implementação precisa do ETL.

**Estrutura do Mapa**:

- O mapa lógico é geralmente estruturado em tabelas e inclui:
  - Origem: base de dados, tabela, coluna, tipo de dado.
  - Transformação: descrição detalhada do processo de manipulação.
  - Destino: tabela e coluna de destino, tipo de dados e, no caso de tabelas de dimensão, o tipo de alteração (SCD 1, 2 ou 3).

## Carregamento de Dados

### Introdução

**Processo ETL**:

- Facilita a migração de dados dos sistemas de origem para o _Data Warehouse_, aplicando as transformações necessárias para padronizar formato e conteúdo.
- A Área de Tratamento de Dados (_Data Staging Area - DSA_) reúne processos de extração, transformação e carga (_ETL_) para preparar os dados antes de sua inclusão no _Data Warehouse_.

### Processo de Carregamento

**Visão Geral**:

- Após a transformação, os dados são carregados na base de dados (_BD_) do _Data Warehouse_, frequentemente em grandes volumes (_bulk loading_).
- A ordem de carregamento é fundamental:
  - Primeiro, as tabelas de **minidimensões**
  - Seguidas pelas **tabelas de dimensões**
  - Por fim, as **tabelas de fatos**
- Criação de chaves primárias específicas para o _Data Warehouse_, independentes das chaves dos sistemas de origem.
- Inclusão de registros especiais para exceções, evitando interrupções no carregamento.
- Construção de agregados para otimizar consultas, seguida de indexação dos dados carregados.

**Carregamento das Tabelas**:

- É uma fase crítica; falhas podem exigir complexos processos de recuperação.
- Otimizações como criação de índices, agregados e particionamento de tabelas melhoram o desempenho, mas tendem a retardar o carregamento.

**Carregamento Inicial**:

- Consiste em disponibilizar, pela primeira vez, os dados extraídos e validados no _Data Warehouse_.
- Geralmente, o carregamento inicial é bem-sucedido, sendo ideal reduzir ao máximo a janela de carregamento.

**Carregamentos Periódicos**:

- Após o carregamento inicial, realizam-se carregamentos periódicos, como atualizações de dimensões e agregados.
- Desafios incluem estimar a duração do carregamento e considerar seu impacto na integridade do _Data Warehouse_ em caso de interrupções.

### Técnicas SCD

**Preservação de Histórico**:

- Para manter o histórico dos dados, utilizam-se técnicas de **Slowly Changing Dimensions (SCD)**, adequadas para tratar mudanças nos atributos das dimensões ao longo do tempo.
- Principais tipos de SCD:
  - **SCD0**: Mantém os dados inalterados.
  - **SCD1**: Substitui valores diretamente, útil para corrigir erros.
  - **SCD2**: Cria novos registros para preservar versões históricas.
  - **SCD3**: Adiciona colunas para armazenar o valor anterior, limitado ao valor atual e uma alteração.
  - **SCD4 e SCD6**: Variantes avançadas para diferentes necessidades de preservação de histórico.

### Processo ETL

**Etapas Principais**:

- **Planejamento**:
  - Estabelecer um plano de ETL completo (_end-to-end_), incluindo o Mapa Lógico de Dados e a infraestrutura da DSA.
  - Selecionar ferramentas de ETL e elaborar um plano detalhado considerando fontes de dados, transformações e especificidades de cada tabela de destino.

- **Carregamento de Dimensões**:
  - Executar planos ETL para dimensões estáticas e dinâmicas.
  - Tratar dimensões geradas manualmente e outros casos especiais.

- **Carregamento de Fatos**:
  - Implementar e testar o ETL para tabelas de fatos, incluindo processos de carregamento periódico.

- **Automatização do Processo**:
  - Utilizar ferramentas avançadas para escalonar e automatizar execuções de ETL.

**Infraestrutura da DSA**:

- Pode variar de uma conta no servidor do _Data Warehouse_ a máquinas dedicadas.
- A escolha depende do volume de dados e da complexidade das transformações necessárias.

**Carregamento Inicial**:

- Realizado diretamente da DSA para o _Data Warehouse_, com alguns cuidados, como:
  - Desativar _logging_.
  - Ordenar os dados pela chave primária.
  - Agregar dados durante o carregamento, se necessário.

**Carregamentos Periódicos**:

- Definir estratégia para identificar novos dados, incluindo novas transações e atualizações.
- Identificar:
  - Novos registros para dimensões.
  - Atualizações de atributos de dimensões e tratamentos adequados.
  - Inclusão de novos fatos ou medidas numéricas.

**Administração**:

- Desenvolver e manter ferramentas de extração de dados.
- Garantir a qualidade dos dados após cada extração.
- Construir e manter agregados e realizar backups e recuperações em caso de falhas no _Data Warehouse_.

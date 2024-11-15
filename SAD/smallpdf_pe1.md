# Sistemas de Apoio à Decisão

## Etapas do Processo de Tomada de Decisão

1. **Análise e Identificação da Situação**: Compreender o problema ou a oportunidade que requer uma decisão.
2. **Desenvolvimento de Alternativas**: Criar diferentes opções ou soluções possíveis para o problema identificado.
3. **Comparação de Alternativas**: Avaliar as opções com base em critérios relevantes, como custo, viabilidade e impacto.
4. **Classificação dos Riscos**: Analisar os riscos associados a cada alternativa.
5. **Escolha da Melhor Alternativa**: Selecionar a opção que melhor atende aos objetivos e minimiza os riscos.
6. **Execução e Avaliação**: Implementar a decisão e monitorar os resultados para avaliar a eficácia da escolha.

## Características dos Data Warehouses

1. **Armazenamento de Grandes Quantidades de Dados**: Projetados para armazenar grandes volumes de dados históricos de diversas fontes.
2. **Integração e Consistência**: Integram dados de diferentes bases operacionais, garantindo consistência e uniformidade.
3. **Dados Dependentes do Tempo**: Mantêm informações temporais, permitindo análises históricas e previsões futuras.
4. **Não Volatilidade**: Os dados, uma vez carregados, não são alterados, apenas consultados.
5. **Estruturas de Dados Otimizadas para Consulta**: Projetados para facilitar consultas complexas e rápidas, frequentemente utilizando desnormalização.

## Concebidos Sobretudo para a Produção de Reports Estáticos

Os **Data Warehouses** são concebidos principalmente para a produção de **reports estáticos**, que são relatórios fixos e pré-definidos que apresentam dados de forma estruturada. Esses relatórios são utilizados para análise de desempenho, monitoramento de KPIs e suporte à tomada de decisão, permitindo que os utilizadores finais acessem informações consolidadas de maneira eficiente. Além disso, eles facilitam a geração de relatórios periódicos e a visualização de dados históricos.

## Operações Necessárias para a Construção de um Data Warehouse por Ordem

1. **Definição do Modelo de Negócio**: Compreender os objetivos e requisitos do negócio.
2. **Identificação de Processos de Negócio**: Determinar quais processos serão suportados pelo Data Warehouse.
3. **Coleta e Análise de Dados Disponíveis**: Identificar as fontes de dados e os dados que serão utilizados.
4. **Desenvolvimento do Processo ETL**: Extrair, transformar e carregar os dados para o Data Warehouse.
5. **Carregamento Inicial dos Dados**: Transferir os dados preparados para as tabelas do Data Warehouse.
6. **Definição de Estruturas de Dados**: Criar tabelas de dimensões e tabelas de fatos.
7. **Implementação de Ferramentas de Acesso e Análise**: Configurar ferramentas para consulta e geração de relatórios.
8. **Testes e Validação**: Garantir que o Data Warehouse funcione corretamente e atenda aos requisitos.
9. **Manutenção e Atualização Contínua**: Monitorar e atualizar o sistema conforme necessário.

## Preferência dos Data Scientists entre Data Lake e Data Warehouse

Os **Data Scientists** geralmente preferem a **arquitetura Data Lake** devido à sua capacidade de armazenar dados em seu formato bruto, incluindo dados estruturados, semiestruturados e não estruturados. Isso permite uma maior flexibilidade na análise de dados e na aplicação de técnicas de **Data Science** e **Machine Learning**, já que os dados podem ser acessados e processados em tempo real. Além disso, os Data Lakes suportam uma abordagem ad hoc, que é frequentemente necessária para experimentação e exploração de dados.

## Diferenças entre Conformidade, Correção, Consistência, Coerência, Certeza e Completude

- **Conformidade**: Refere-se à aderência dos dados a padrões ou regras predefinidos, como formatos e tipos de dados esperados.

- **Correção**: Diz respeito à precisão dos dados, ou seja, se os valores refletem a realidade ou uma versão oficial correta.

- **Consistência**: Envolve a uniformidade dos dados em diferentes fontes ou sistemas, garantindo que informações idênticas sejam apresentadas da mesma forma.

- **Coerência**: Relaciona-se à lógica interna dos dados, assegurando que as informações sejam logicamente compatíveis e não contraditórias.

- **Certeza**: Refere-se ao nível de confiança que se tem na precisão e na veracidade dos dados, muitas vezes influenciado pela qualidade das fontes.

- **Completude**: Refere-se à presença de todos os dados necessários, assegurando que não faltem informações essenciais em um conjunto de dados.

## Documentos Chave na Etapa de Transformação de um Data Warehouse

Os documentos chave usados pelos arquitetos de um Data Warehouse durante a implementação dos métodos da etapa de transformação incluem:

1. **Requisitos do negócio**: Fornecem a base para entender as necessidades e objetivos do projeto.
2. **Mapa Lógico de Dados**: Descreve os relacionamentos entre as fontes de dados e os campos no Data Warehouse, essencial para a transformação.
3. **Modelos Lógicos das fontes de dados**: Ajudam a entender a estrutura e a qualidade dos dados que serão transformados.

As outras opções, como casos de uso, mapa local da arquitetura e lista de pesquisas ad-hoc, podem ser úteis, mas não são consideradas documentos chave especificamente para a etapa de transformação.

## Opções Corretas Relativamente ao Processo de Carregamento de Dados

1. **São carregados muitos registos de uma só vez**: **Correta** (o carregamento em massa é uma prática comum).
2. **As técnicas SCD permitem lidar com as alterações nas dimensões**: **Correta** (as técnicas SCD são essenciais para gerenciar mudanças nas dimensões).
3. **As tabelas de dimensão são carregadas antes da tabela de factos**: **Correta** (normalmente, as dimensões são carregadas primeiro para garantir a integridade referencial).
4. **As estruturas de otimização podem atrasar o carregamento**: **Correta** (otimizações como índices e agregações podem impactar o tempo de carregamento).

As opções "A tabela de factos é carregada antes das tabelas de dimensão" e "Nos carregamentos periódicos, os problemas com atualizações nas dimensões não se colocam" são **incorretas**.

## Mecanismos de Otimização que Podem Prejudicar a Rapidez da Etapa de Carregamento de Dados

1. **Particionamento de tabelas**: Pode aumentar a complexidade do carregamento, afetando a velocidade.
2. **Agregados**: A construção de agregados pode demandar tempo adicional durante o carregamento.
3. **Índices**: A criação ou atualização de índices pode retardar o processo de carregamento.

As opções "Logs do sistema operativo", "Views" e "Desagregados" não são mecanismos que, em geral, prejudicam a rapidez da etapa de carregamento de dados.

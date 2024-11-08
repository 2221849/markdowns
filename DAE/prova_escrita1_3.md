# Desenvolvimento de Aplicações Empresariais

## Padrões de Acesso a Dados e ORM (Object-Relational Mapping)

### Entidades de Negócio: Como Representar?

- **Como representar uma entidade de negócio** (por exemplo, cliente)?
- **Como representar coleções de entidades de negócio** (por exemplo, carteira de clientes)?
- **Como representar objetos complexos** com hierarquias ou redes (por exemplo, plano de produção)?
- Dados (estrutura) ou objetos (dados & comportamento)?
- Estrutura semelhante à BD ou mais adequada à representação conceptual?

### Alternativas para Representar uma Entidade

1. **Custom Classes**
2. **Text-based format** (ficheiros de texto, XML, JSON...)
3. **DataSet** (.NET)
4. **ResultSet** (JDBC)

### Alternativas para Representar Hierarquias e Coleções de Entidades

1. **Custom Classes**
2. **Text-based format** (ficheiros de texto, XML, JSON...)
3. **DataSet** (.NET)
4. **ResultSet** (JDBC)
5. **Suporte da Plataforma** (ex. IList / List)

### Custom Classes

- **Vantagens**:
  - Integração natural no programa orientado a objetos (OO);
  - Suporte a tipos de dados definidos;
  - Acesso explícito aos campos;
  - Aproveitamento do conhecimento prévio dos programadores.
- **Desvantagens**:
  - Exige mais esforço de desenvolvimento;
  - Ligação mais complexa a controlos na interface de utilizador (UI);
  - Necessidade de mapeamento com SGBD relacional.

### Text-based format (XML, JSON...)

- **Vantagens**:
  - Fácil de exportar;
  - Suporte abrangente em diferentes plataformas;
  - Suporte natural para coleções e hierarquias;
  - Standard de facto com possibilidade de validação através de esquemas;
  - Suporte em alguns SGBDs para gerar XML com comandos SELECT.
- **Desvantagens**:
  - Manipulação de dados via API (ex., DOM);
  - Conversão necessária devido a tratamento em formato de texto;
  - Lento;
  - Acesso aos campos não é explícito;
  - Integração limitada com UI.

### DataSet (.NET)

- **Vantagens**:
  - Pouco ou nenhum desenvolvimento adicional necessário;
  - Estrutura similar ao modelo relacional;
  - Integração eficiente com UI;
  - Permite representar coleções complexas e hierarquias (usando DataRelation).
- **Desvantagens**:
  - Restrito à plataforma .NET;
  - Manipulação de dados via API;
  - Acesso aos campos não é explícito (se não forem tipados).

### ResultSet (JDBC)

- **Vantagens**:
  - Pouco ou nenhum desenvolvimento adicional necessário;
  - Modelo relacional simplificado (semelhante a uma tabela);
  - Permite coleções lineares de um único tipo.
- **Desvantagens**:
  - Restrito à plataforma Java;
  - Suporte apenas para uma tabela (coleções simples);
  - Manipulação de dados via API;
  - Acesso aos campos não é explícito.

### IList / List

- **Vantagens**:
  - Sem necessidade de desenvolvimento adicional para representar coleções;
  - Algoritmos standard disponíveis (ex., ordenação);
  - Adequado para coleções lineares.
- **Desvantagens**:
  - Não fortemente tipado (a menos que se utilizem genéricos);
  - Representação de hierarquias é complexa.

### Classificação dos Padrões de Acesso a Dados e ORM

1. **Padrões Arquiteturais de Acesso a Dados**:
   - Table Data Gateway
   - Active Record
   - Data Mapper

2. **Padrões Comportamentais de ORM**:
   - Unit of Work
   - Identity Map
   - Lazy Load

3. **Padrões Estruturais de ORM**:
   - Identity Field
   - Foreign Key Mapping
   - Association Table Mapping
   - Serializable LOB
   - Single Table Inheritance
   - Class Table Inheritance
   - Concrete Table Inheritance

### Padrões Arquiteturais de Acesso a Dados

#### Table Data Gateway

- Um objeto que atua como um intermediário (Gateway) entre a aplicação e uma tabela da base de dados, tratando todos os registos dessa tabela.
- **Características**:
  - Ideal para utilizar em conjunto com o padrão Table Module;
  - Usa métodos _finder_ para buscar dados e métodos CRUD para operações de manipulação;
  - Sem estado persistente.

#### Table Module

- Um único objeto que gere a lógica de negócio para todos os registos de uma tabela ou vista na base de dados.
- **Características**:
  - Uma instância para todos os registos da tabela;
  - Implementa lógica associada a uma tabela através de métodos específicos;
  - Atribui um equilíbrio entre simplicidade e manutenção.

#### Active Record

- Um objeto que encapsula um registo numa tabela, providenciando acesso aos dados e incluindo lógica de domínio sobre esses dados.
- **Características**:
  - Estrutura e métodos orientados à lógica de domínio;
  - Beneficia da geração de código para CRUD.

#### Data Mapper

- Uma camada que move dados entre objetos e uma base de dados, mantendo ambos independentes.
- **Características**:
  - Ideal para Domain Models complexos;
  - Permite independência entre o esquema de objetos e o esquema relacional.

### Padrões Comportamentais de ORM

#### Unit of Work

- Mantém uma lista de alterações feitas durante uma transação de negócio, coordenando a gravação dos dados e a resolução de problemas de concorrência.
- **Motivação**:
  - Minimiza chamadas desnecessárias à base de dados, consolidando alterações;
  - Realiza um _commit_ ordenado, verificando consistência e gravando todas as modificações.

#### Identity Map

- Assegura que cada objeto é carregado uma única vez, evitando duplicações ao manter todos os objetos carregados num mapa de referência.
- **Características**:
  - Usado pelos métodos _finder_;
  - Implementado geralmente como um Singleton.

#### Lazy Load

- Um objeto que só contém os dados necessários para uma primeira interação, mas que sabe como obter dados adicionais conforme necessário.
- **Características**:
  - Apenas carrega dados quando são necessários, otimizando desempenho;
  - Implementado via técnicas como:
    - **Lazy Initialization**: Carrega atributos apenas quando acedidos.
    - **Virtual Proxy**: Cria um proxy que carrega o objeto real ao ser acedido.
    - **Value Holder**: Encapsula o objeto real, carregando-o ao primeiro acesso.
    - **Ghost**: Objeto parcialmente carregado, completando-se na primeira interação.

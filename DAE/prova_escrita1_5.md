# Desenvolvimento de Aplicações Empresariais

## Padrões de Lógica de Negócio

### Padrões de Lógica de Negócio

- **Transaction Script** [PoEAA] (orientado aos procedimentos)
- **Domain Model** [PoEAA] (orientado aos objetos)
- **Table Module** [PoEAA] (orientado à tabela)
- **Service Layer** [PoEAA] (orientado aos serviços)

### Transaction Script

- Organiza a lógica de negócio em procedimentos, onde cada procedimento trata de uma única requisição da camada de apresentação.
- **Exemplo:**
  - `calculateRecognitions(contractNumber: long): void`
  - `recognizedRevenue(contractNumber: long, asOf: Date): Money`

**Características:**

- A lógica de negócio organiza-se em transações de negócio com o utilizador.
- Não interfere com outras transações; visa recolher dados, consultar a BD, calcular e guardar resultados.
- Principal vantagem é a simplicidade, adequado para lógicas de negócio pouco complexas.
- Funciona bem com o padrão **Table Data Gateway**.
- Pode originar código duplicado e complicações em lógicas de negócio complexas.
- Idealmente, **Transaction Scripts** ficam separados dos componentes de apresentação e acesso a dados.

### Domain Model

- Modelo orientado a objetos que representa o domínio e incorpora comportamento e dados.

- **Exemplo de Estrutura de Classes:**
  - `Contract`: `calculateRecognitions`, `recognizedRevenue(date)`
  - `Product`: `calculateRecognitions(contract)`
  - `RecognizedStrategy`: estratégias de reconhecimento de receita.

**Características:**

- Paradigma OO, com hierarquia de classes que representa o domínio do problema.
- Cada entidade contém métodos de negócio.
- Suporta conceitos OO avançados (ex.: **Strategy**).
- Pode ser complexo para situações simples e difícil de gerir em grandes dimensões.
- Flexível na evolução e manutenção após uma compreensão sólida do modelo.
- Dificuldades em integração com bases de dados relacionais.
- Pouco eficiente para operações em lote (ex.: aumentar preços de todos os produtos).

### Table Module

- Uma única instância que gere a lógica de negócio para todas as linhas de uma tabela ou vista da BD.

- **Exemplo de Estrutura de Classes:**
  - `Contract`: `calculateRecognitions(ID)`
  - `Product`: `getProductType(ID)`
  - `RevenueRecognition`: `insert(ID, amount, date)`, `recognizedRevenue(contractID, date)`

**Características:**

- Estrutura com vários componentes (um por tabela).
- Métodos associados a cada tabela.
- Uma instância partilhada para todos os registos.
- Ideal para uso com **RecordSets**.
- Não guarda estado das entidades; o estado é passado entre camadas através de **RecordSet**.
- Bom equilíbrio entre decomposição de código/lógica e facilidade de manutenção.

### Service Layer

- Define a fronteira de uma aplicação com uma camada de serviços que estabelece operações disponíveis e coordena respostas da aplicação.

- **Exemplo de Estrutura:**
  - `RecognitionService`
  - Camadas de **User Interfaces**, **Domain Model** e **Data Source Layer**.

**Características:**

- Ideal para aplicações que requerem múltiplas interfaces para acesso a dados e lógica.
- Serve de fachada para a aplicação empresarial, disponibilizando operações de interface à lógica de negócio encapsulada.
- Coordena transações entre clientes e a aplicação, e as respetivas respostas.
- Suporta interação com diversos tipos de clientes (web, mobile, etc.) e integração com outras aplicações.

#### Exemplos de Serviços

- `ApplicationService`: `getEmailGateway()`, `getIntegrationGateway()`
- `RecognitionService`: `calculateRevenueRecognitions(contractNumber: long)`, `recognizedRevenue(contractNumber: long, asOf: Date)`

### Combinações entre Padrões de Lógica de Negócio e Acesso a Dados

- **Transaction Script + Table Data Gateway**
- **Table Module + Table Data Gateway**
- **Table Module + Table Data Gateway + Custom Classes**
- **Domain Model + Active Record**
- **Domain Model + Data Mapper**

### Estrutura de Packages

1. **Table Module + Table Data Gateway**
   - Pacotes: `BLL (Business Logic Layer)`, `DAL (Data Access Layer)`, `UI (User Interface)`
   - Utilizam **RecordSet** para comunicação entre camadas.

2. **Table Module + Table Data Gateway + Custom Classes**
   - Pacotes: `BLL`, `DAL`, `UI`, `Entities`
   - Classes apenas com atributos.

3. **Domain Model + Active Record**
   - Pacotes: `BLL + DAL`, `UI`

4. **Domain Model + Data Mapper**
   - Pacotes: `BLL`, `DAL`, `UI`

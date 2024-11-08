# Desenvolvimento de Aplicações Empresariais

## Arquitetura de software & modelo 3 camadas

### Definição

> A set of...design elements that have a particular form.
> Perry, D.E. & Wolf, A.L. “Foundations for the Study of Software Architecture.” Software Engineering notes, ACM SIGSOFT 17, 4 (October 1992): 40-52.

> A level of design concerned with issues beyond the algorithms and data structures of the computation;

> Designing and specifying the overall system structure emerges as a new kind of problem. Structural issues include gross organization and global control structure; protocols for communication, synchronization, and data access; assignment of functionality to design elements; physical distribution; composition of design elements; scaling and performance; and selection among design alternatives.
> Garlan, D. & Shaw, M. “An Introduction to Software Architecture,” in Advances in Software Engineering and Knowledge Engineering, vol. I. River Edge, NJ: World Scientific Publishing Company, 1993.

> The structure of the components of a program/system, their interrelationships, and principles and guidelines governing their design and evolution over time.
> Garlan, David & Perry, Dewayne. “Introduction to the Special Issue on Software Architecture.” IEEE Transactions on Software Engineering 21, 4 (April, 1995).

> The set of significant decisions about the organization of a software system, the selection of the structural elements and their interfaces by which the system is composed, together with their behavior as specified in the collaborations among those elements, the composition of these structural and behavioral elements into progressively larger subsystems, and the architectural style that guides this organization – these elements and their interfaces, their collaboration, and their composition
> Booch, Rumbaugh, and Jacobson. “The UML Modeling Language User Guide,” Addison-Wesley, 1999

> The fundamental organization of a system, embodied in its components, their relationships to each other and the environment, and the principles governing its design and evolution.
> ANSI/IEEE Std 1471-2000, Recommended Practice for Architectural Description of Software-Intensive Systems

> The architecture of any automated services that support and implement functional requirements, including the interfaces to the business and other applications.
> It describes the structure of an application and how that structure implements the functional requirements of the organization. Whilst there should ideally be one application architecture in an organization, there are typically many different application architectures.
> Microsoft Architecture Overview, <https://msdn.microsoft.com/en-us/library/ms978007.aspx>

> The software architecture of a program or computing system is the structure or structures of the system, which comprise software elements, the externally visible properties of those elements, and the relationships among them.
> By "externally visible" properties, we are referring to those assumptions other components can make of a component, such as its provided services, performance characteristics, fault handling, shared resource usage, and so on.
> The intent of this definition is that a software architecture must abstract away some information from the system (otherwise there is no point looking at the architecture, we are simply viewing the entire system) and yet provide enough information to be a basis for analysis, decision making, and hence risk reduction.
> Software Architecture in Practice (2nd edition), Bass, Clements, Kazman; Addison-Wesley (2003)

### Resumo

- Organização de alto nível e estrutura (relações) de componentes do sistema
- Princípios (regras) de desenho
- Decisões fundamentais (difíceis de alterar posteriormente)
- Fundação para o desenvolvimento e evolução do sistema
- Suporta e implementa funções de negócio
- Deve permitir a evolução do sistema (Estrutura, Requisitos, Funcionalidades)
- Existem várias arquiteturas (ou vistas) no sistema

### Para que serve?

- Perspectiva organizacional
  - Comunicação do desenho de alto nível
  - Fornece contexto ao sistema
  - Alocação de trabalho
- Perspectiva técnica
  - Cumprir requisitos e objetivos
  - Potencia flexibilidade
  - Potencia redução de custos de manutenção e evolução
  - Aumenta a reutilização e integração com sistemas legacy e componentes de terceiros

É difícil dizer se uma arquitetura de aplicação é correta ou errada. Uma arquitetura resulta de um conjunto de compromissos e concessões entre várias forças e do contexto específico.

### O que não é uma arquitetura de software

- Modelo de dados;
- Arquitetura física onde o sistema vai executar;
- Detalhes de desenho/implementação.

### Regras de ouro de uma boa arquitetura de software

- Elementos isolados (componentes)
- Responsabilidades bem definidas
- Comunicam através de interfaces bem definidas
- Diminuir as dependências entre elementos
  - Programar para a interface e não para a implementação
- Tentar antecipar a mudança/evolução
  - Por exemplo, através de parametrização e carregamento dinâmico de componentes
- Ligações assíncronas sempre que possível
  - Por exemplo, Message Queueing

### Exemplos de padrões arquiteturais

**Microkernel**:
A arquitetura de microkernel consiste em dois tipos de componentes de arquitetura: um sistema central e módulos plug-in. A lógica da aplicação é dividida entre módulos plug-in independentes e o sistema central básico, oferecendo extensibilidade, flexibilidade e isolamento das funcionalidades da aplicação e lógica de processamento personalizada.

**Microservices**:
A arquitetura de microserviços é um estilo de desenvolvimento de software onde uma aplicação é estruturada como uma coleção de serviços pequenos, independentes e autônomos. Cada serviço é responsável por uma função específica e se comunica com outros através de interfaces bem definidas. Essa arquitetura é particularmente útil para aplicações que necessitam de alta escalabilidade, resiliência e facilidade de manutenção, além de permitir a utilização de diferentes tecnologias e frameworks.

**Space-based**:
A arquitetura baseada em espaço é projetada para fornecer alta escalabilidade, especialmente em sistemas que precisam de grandes volumes de dados e cargas variáveis. O padrão space-based é uma abordagem de computação distribuída que utiliza uma estrutura de memória compartilhada para distribuir dados e processamento. Isso permite que a aplicação escale horizontalmente, distribuindo carga de forma eficiente.

**Event-driven**:
O padrão de arquitetura orientada a eventos é um padrão popular de arquitetura assíncrona distribuída utilizado para produzir aplicações altamente escaláveis. Também é altamente adaptável e pode ser usado tanto para pequenas aplicações quanto para grandes e complexas. A arquitetura orientada a eventos é composta por componentes de processamento de eventos desacoplados e de propósito único que recebem e processam eventos de forma assíncrona.

A arquitetura orientada a eventos possui duas topologias principais: o mediador e o corretor.

**Pipeline**:
O padrão de arquitetura pipeline organiza o sistema como uma série de etapas ou transformações de dados. Cada etapa realiza uma operação no dado que passa por ela, podendo passar por diversas etapas até ser processado ou exibido ao usuário. É útil em sistemas que processam grandes volumes de dados sequenciais ou que envolvem processamento de dados em tempo real, como em sistemas de streaming ou de análise de dados.

**Layered**:
Como mencionado, a arquitetura em camadas é uma das abordagens mais tradicionais, dividindo a aplicação em camadas lógicas que se separam claramente por responsabilidades, como apresentação, lógica de negócios e persistência. Este modelo favorece a reutilização, a manutenção e a escalabilidade do sistema, permitindo que cada camada seja modificada independentemente, desde que as interfaces entre elas permaneçam consistentes. A separação de responsabilidades também facilita a especialização das equipes de desenvolvimento, com cada equipe focando em uma camada específica.

### Arquitetura de 3 Camadas vs. Arquitetura em Múltiplas Camadas (N-Tier)

Embora o conceito de camadas se refira à organização lógica dos componentes dentro da aplicação, a arquitetura de múltiplas camadas (ou n-tier) se refere à distribuição física dessas camadas. Com **n-tiers**, cada camada pode estar em servidores diferentes, facilitando a escalabilidade e a distribuição de carga.

- **n-layer** não implica necessariamente **n-tier**.
- **n-tier** não implica **n-layer**.

O uso de múltiplos tiers (camadas físicas) permite uma maior flexibilidade na distribuição do sistema e na alocação de recursos. Esse modelo é particularmente útil em sistemas empresariais que exigem alta disponibilidade, resiliência e capacidade de escalar conforme a demanda.

### **Importância dos Padrões Arquiteturais no Desenvolvimento de Aplicações Empresariais**

A adoção de um padrão arquitetural adequado para o desenvolvimento de aplicações empresariais é um passo fundamental para garantir que o sistema seja escalável, flexível e de fácil manutenção. No entanto, essa escolha precisa ser feita com base no tipo de aplicação, na complexidade do negócio e na necessidade de integração com outros sistemas.

- **Complexidade da aplicação**: Para sistemas simples, pode não ser necessário adotar um padrão arquitetural complexo. No entanto, para sistemas empresariais mais complexos, que envolvem múltiplas interações e grandes volumes de dados, a escolha de um padrão arquitetural é crucial.
- **Integração com sistemas legados**: Muitas vezes, uma aplicação empresarial precisa se integrar com sistemas legados que já existem na organização. A escolha do padrão arquitetural correto pode facilitar essa integração, utilizando técnicas como proxies ou adaptações para que o novo sistema se comunique adequadamente com os legados.
- **Requisitos de escalabilidade**: Em sistemas empresariais, a capacidade de escalar horizontalmente e lidar com grandes volumes de dados é frequentemente

 uma necessidade. Arquiteturas como microserviços e arquiteturas orientadas a eventos são ideais para esses requisitos, pois permitem que o sistema cresça sem comprometer o desempenho.

### **Conclusão: Como Tirar Partido da Experiência e Boas Práticas de Outros**

Para garantir o sucesso no desenvolvimento de aplicações empresariais, é fundamental que os desenvolvedores e arquitetos de sistemas aproveitem os padrões e boas práticas estabelecidos por especialistas na área. Isso envolve não apenas a adoção de arquiteturas já comprovadas, mas também a adaptação de tais arquiteturas para atender às necessidades específicas da organização. Os padrões de software, quando aplicados corretamente, ajudam a mitigar riscos, reduzir custos e garantir que a aplicação seja capaz de evoluir conforme as mudanças nas necessidades do negócio.

A utilização de padrões de software permite que a organização construa soluções mais robustas, escaláveis e fáceis de manter, além de facilitar a integração com outros sistemas e reduzir a complexidade geral do sistema.

## Padrões de Aplicações Empresariais

### Definição de Padrão

> Cada padrão descreve um problema que ocorre repetidamente no nosso ambiente e, em seguida, descreve o núcleo da solução para esse problema de uma forma que pode ser reutilizada muitas vezes sem que a solução seja exatamente a mesma. — Christopher Alexander

### Padrão de Desenho de Software: Definição

> Um padrão de design nomeia, abstrai e identifica os aspetos essenciais de uma estrutura de design comum que é útil para criar um design orientado a objetos reutilizável. — *Design Patterns: Elements of Reusable Object-Oriented Software*, Gamma et al. (Gang of Four)

### O que **não é** um padrão

Um padrão não é uma solução mágica que resolve todos os problemas de uma aplicação ou empresa.

### Padrão de Software

- Um padrão é um conjunto de *boas práticas*;
- Representa uma solução para um problema recorrente num contexto específico;
- Ajuda a evitar "reinventar a roda";
- Facilita a comunicação ao criar um vocabulário comum;
- Padrões são descobertos, não inventados;
- “Patterns are half-baked” — Martin Fowler

### Vantagens dos Padrões de Software

- Facilita a comunicação;
- Fornece uma solução comprovada;
- Aumenta a reutilização em larga escala;
- Captura o conhecimento dos especialistas e os *trade-offs* envolvidos;
- Geralmente são independentes de:
  - Tecnologia;
  - Linguagem de programação;
  - Filosofia (open source, etc.).

### Desvantagens dos Padrões de Software

- Não permite reutilização direta de código;
- Muitas vezes são simplificações excessivas;
- A equipa pode sofrer de *overload* de padrões;
- São validados através de experiência e discussão, em vez de testes automatizados;
- A integração de padrões no processo de desenvolvimento exige colaboração humana intensiva.

### Descrição de um Padrão de Software (Gamma et al., 1995)

- **name**: Contribui para o vocabulário de padrões;
- **synopsis**: Breve descrição do problema que o padrão resolve;
- **forces**: Requisitos, considerações ou condições necessárias;
- **solution**: Essência da solução;
- **counter forces**: Razões para não usar o padrão;
- **related patterns**: Alternativas de design possíveis.

### Catálogos de Padrões de Software

- GoF Design Patterns (.NET): [DoFactory](https://www.dofactory.com/net/design-patterns)
- GoF Design Patterns (Java): [DZone](https://dzone.com/articles/gof-design-patterns-using-java-part-1)
- *Patterns of Enterprise Application Architecture*: [Martin Fowler](http://martinfowler.com/eaaCatalog/)
- *Java EE Patterns*: [Packt Publishing](https://www.packtpub.com/product/java-ee-8-design-patterns-and-best-practices/978178883062)
- .NET Application Architecture Guides: [Microsoft](https://dotnet.microsoft.com/learn/dotnet/architecture-guides)
- *Patterns of Enterprise Application Integration*: [Enterprise Integration Patterns](http://www.enterpriseintegrationpatterns.com/)
- The Server Side: [The Server Side](https://www.theserverside.com/)

### Siglas

- **GoF**: Gang of Four
- **PoEAA**: Patterns of Enterprise Application Architecture
- **CRUD**: Create, Read, Update, Delete

### Aplicação Empresarial (Revisitado)

- Funcionalidade crítica para a empresa;
- Gerencia grandes volumes de dados persistentes;
- Suporta acessos simultâneos e concorrentes;
- Inclui um grande número de interfaces gráficas;
- Necessita de integração com outras aplicações;
- Enfrenta dissonâncias conceptuais em conceitos comuns entre departamentos e unidades;
- Regras de negócio complexas e, às vezes, não intuitivas.

### Arquiteturas por Camadas

- Podem incluir mais de três camadas;
- Algumas plataformas definem um modelo padrão de camadas:
  - Java EE
  - .NET

### Modelo de 3 Camadas

- **Presentation Logic**
- **Business Logic**
- **Data Access Logic**

> *Layer* ≠ *Tier*

### Arquitetura Modelo (Java EE)

Um modelo de cinco camadas para separação lógica de responsabilidades:

1. **Client Tier**: Interação com o utilizador, apresentação da interface, dispositivos (aplicações, applets, GUIs).
2. **Presentation Tier**: Gestão de sessão, criação de conteúdo, formatação e entrega (JSP, Servlets, etc.).
3. **Business Tier**: Lógica de negócios, transações, dados e serviços (EJBs e outros objetos de negócio).
4. **Integration Tier**: Conectores para sistemas legados e externos (JMS, JDBC, adaptadores de recursos).
5. **Resource Tier**: Dados, serviços externos e sistemas legados (bases de dados e outros recursos).

### E então?

- Que questões surgem para cada camada?
- Quais padrões são recomendados para cada camada em aplicações empresariais?
- Nas próximas secções, discutiremos padrões para:
  - Entidades de negócio;
  - Lógica de negócio;
  - Acesso a dados;
  - Lógica de apresentação;
  - Concorrência na base de dados.

### Reflexão

**Questões**:

- Como dividir a aplicação?
- Como representar as entidades de negócio?
- Como implementar a lógica de negócio?
- Como persistir entidades de negócio?
- Como garantir a consistência dos dados?
- Como tratar a interação com o utilizador?
- Como lidar com a distribuição física da aplicação?

**Como Dividir a Aplicação**:

- Que camadas implementar?
- Como dividir a aplicação em projetos/componentes?
  - Quais projetos?
  - Que componentes em cada projeto?
  - Que interface para cada componente?
- Manter ou não o estado nos componentes?
- Que tipo de interface usar nos componentes de DAL?
  - CRUD ou lógica de negócio?

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
  - Usa métodos *finder* para buscar dados e métodos CRUD para operações de manipulação;
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
  - Realiza um *commit* ordenado, verificando consistência e gravando todas as modificações.

#### Identity Map

- Assegura que cada objeto é carregado uma única vez, evitando duplicações ao manter todos os objetos carregados num mapa de referência.
- **Características**:
  - Usado pelos métodos *finder*;
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

### Padrões Estruturais de ORM (Object-Relational Mapping)

- **Identity Field**
- **Foreign Key Mapping**
- **Association Table Mapping**
- **Serializable LOB**
- **Single Table Inheritance**
- **Class Table Inheritance**
- **Concrete Table Inheritance**

### Motivação

Diferenças de representação entre objetos e tabelas em banco de dados:

- **Associações entre objetos**: mantidas em memória, permitindo coleções de referências (e.g., Fatura e suas linhas).
- **Relacionamentos entre tabelas**: dependem de chaves estrangeiras; todas as linhas relacionadas devem conter a chave da entidade associada.

### Identity Field

Campo que armazena o ID da base de dados no objeto, permitindo a correspondência entre um objeto em memória e uma linha do banco de dados.

- **Chaves**: podem ser significativas (e.g., NIF) ou não (e.g., GUID), e podem ser simples, compostas, únicas na tabela ou na base de dados.

### Foreign Key Mapping

Mapeia uma associação entre objetos para uma chave estrangeira entre tabelas.

- **Tipos de Mapeamento**:
  - Campo de valor único
  - Campo de coleção

- **Abordagens de sincronização**:
  - Delete e insert
  - Adicionar uma referência inversa
  - Realizar um "diff" na coleção

### Association Table Mapping

Salva uma associação como uma tabela com chaves estrangeiras que ligam as tabelas associadas. Ideal para associações "N para N".

- **Etapas para carregamento de dados**:
  1. Encontrar registros associados ao empregado na tabela-associação.
  2. Carregar cada habilidade dos registros encontrados.

### Serialized LOB

Salva um grafo de objetos ao serializá-los em um único objeto grande (LOB) e armazená-lo em um campo de banco de dados.

- **Formas de Serialização**:
  - **Binário (BLOB)**: simples e rápido, mas problemático em caso de mudanças na classe.
  - **Texto (CLOB)**: permite leitura direta no banco de dados, mas ocupa mais espaço e pode ser mais lento.

### Mapeamento de Heranças

Como bancos de dados relacionais não possuem padrão SQL para herança, três abordagens são usadas:

#### Single Table Inheritance

Representa uma hierarquia de classes como uma única tabela.

- **Vantagens**:
  - Única tabela, sem necessidade de `JOINs`.
  - Refatorações na hierarquia de classes não afetam a estrutura da tabela.

- **Desvantagens**:
  - Tabela única pode ficar grande e impactar o desempenho.
  - Conflitos de nomes entre atributos diferentes.

#### Class Table Inheritance

Cada classe da hierarquia possui sua própria tabela.

- **Vantagens**:
  - Tabelas mais compreensíveis e sem desperdício de espaço.
  - Relação direta entre classes e tabelas.

- **Desvantagens**:
  - Requer múltiplas consultas e `JOINs` para carregar um objeto.
  - Refatorações afetam tabelas relacionadas.
  - Tabelas de superclasses podem se tornar gargalos.

#### Concrete Table Inheritance

Cada classe concreta possui uma tabela.

- **Vantagens**:
  - Cada tabela possui todos os dados relevantes.
  - Evita `JOINs`, reduzindo a carga de acesso.

- **Desvantagens**:
  - Não permite relações para classes abstratas.
  - Alterações em atributos de superclasses exigem mudanças em todas as tabelas das classes concretas.

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

## Padrões de concorrência

### Concorrência

- Múltiplos processos ou *threads* acedem aos mesmos dados num mesmo intervalo de tempo.
- Essencial em aplicações empresariais e servidores aplicacionais.
- Utilizam-se frequentemente *transaction managers*, mas:
  - Algumas interações com o sistema não podem ser limitadas a uma única transação com a BD.
  - É necessário controlo de transações para dados manipulados por múltiplas transações com a BD.

### Problemas de Concorrência

**Problemas de Corretidão**:

- **Lost updates (atualizações perdidas):** ocorrem quando mais de um agente atualiza o mesmo recurso simultaneamente, levando a perdas de dados.
- **Inconsistent reads (leituras inconsistentes):** ocorrem quando duas leituras de uma informação são corretas em momentos diferentes, mas não simultâneas.

**Problemas de Convivência**:

- Quantidade de atividade concorrente permitida.
- Equilíbrio entre corretidão e necessidade de concorrência.
- Mecanismos de controlo de concorrência introduzem novos problemas (embora menos graves).

### Contextos de Execução

- ***Request*:** um pedido externo ao qual o software responde.
- ***Session*:** conjunto de interações entre cliente e servidor ao longo do tempo (pode incluir um ou múltiplos *requests*).
- ***Process*:** contexto de execução isolado, manipulando dados de forma independente.
- ***Thread*:** contexto de execução leve dentro de um processo, que permite múltiplos *requests* com memória partilhada, podendo causar problemas de concorrência.

**Subcategorias**:

- **Transaction:** agrupa vários *requests* num único contexto de execução:
  - **System transaction:** para a BD.
  - **Business transaction:** para o utilizador.

### Soluções para Concorrência

**Isolamento e Imutabilidade**:

- **Isolamento:** Particionar dados para serem acedidos por um único contexto de execução, reduzindo erros de corretidão.
- **Imutabilidade:** Dados apenas para leitura ou quase sempre imutáveis, permitindo cópias para evitar conflitos.

**Controlo de Concorrência**:

- **Optimistic Locking:** Permite acesso simultâneo aos dados, detetando conflitos no momento de submissão das alterações.
- **Pessimistic Locking:** Bloqueia o acesso aos dados, permitindo uso exclusivo a um único contexto de execução.

### Problemas de *Optimistic* e *Pessimistic Locks*

- *Optimistic locks:* utilizam versionamento para resolver *lost updates* e *inconsistent reads*.
- *Pessimistic locks:* usam *read* e *write locks* para evitar *inconsistent reads* e incluem mecanismos de deteção e *timeouts* para resolver *deadlocks*.

### Transações

**Propriedades ACID**:

- **Atomicidade:** Todos os passos numa sequência de ações devem concluir com sucesso ou gerar um *rollback*.
- **Consistência:** Recursos devem estar consistentes no início e no fim da transação.
- **Isolamento:** Resultados de uma transação não devem ser visíveis para outras transações até ao sucesso da operação.
- **Durabilidade:** Resultados de uma transação devem ser permanentes.

**Tipos de Transações**:

- **Request transaction:** começa e termina com um *request*.
- **Long transaction:** inclui vários *requests*.
- **Late transaction:** iniciada o mais tarde possível.

**Níveis de Isolamento**:

- **Serializable:** nível mais forte, impede *inconsistent reads*.
- **Repeatable read:** permite *phantoms*.
- **Read committed:** permite *phantoms* e *unrepeatable reads*.
- **Read uncommitted:** permite *phantoms*, *unrepeatable reads* e *dirty reads*.

### Padrões de Concorrência

**Optimistic Offline Lock**:

- Deteta conflitos entre transações empresariais concorrentes e realiza *rollback* em caso de conflito.
- Utiliza versionamento, comparando versões dos dados entre a sessão e a BD antes de atualizar.

**Pessimistic Offline Lock**:

- Impede conflitos, permitindo acesso exclusivo aos dados a uma única *business transaction* de cada vez.
- Utiliza *locks* exclusivos de leitura/escrita conforme necessário.

**Coarse-Grained Lock**:

- Utiliza um *lock* único para múltiplos objetos relacionados.
- Evita o carregamento de todos os objetos para bloqueio individual.
- Implementado através de *shared locks* ou *root locks* para facilitar o bloqueio em grupo.

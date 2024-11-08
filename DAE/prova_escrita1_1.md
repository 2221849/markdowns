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

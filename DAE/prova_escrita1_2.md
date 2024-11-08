# Desenvolvimento de Aplicações Empresariais

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

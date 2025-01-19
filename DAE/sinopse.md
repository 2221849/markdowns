# Desenvolvimento de Aplicações Empresariais

## Questões

- Como dividir a aplicação?
- Como representar as entidades de negócio?
- Como representar a lógica de negócio?
- Como persistir as entidades de negócio?
- Como garantir a consistência dos dados da base de dados?
- Como tratar a interação com o utilizador?
- Como resolver questões relacionadas com a distribuição física da aplicação?

### Como dividir a aplicação?

- Que camadas implementar?
- Como dividir a aplicação em projetos/componentes?
  - Que projetos?
  - Que componentes em cada projeto?
  - Que interface em cada componente?
- Manter ou não o estado nos componentes?
- Que tipo de interface colocar nos componentes de DAL (Data Acess Layer)?
  - CRUD ou negócio?

### Como representar entidades de negócio?

- Custom, XML, DataSet, ResultSet, ...
- Para a plataforma de destino em causa existe algum modelo mais comum? Ou que seja melhor suportado?
- Como passar estas classes entre camadas (eventualmente remotas)?
- Table Module é muito adequado quando a plataforma suporta Record Sets nas várias camadas (especialmente UI)
- Domain Model é mais complexo mas mais flexível (paradigma OO puro)
- Lógica simples a complexa e bom suporte na plataforma para recordsets -> **Table Module**
- Lógica muito complexa -> **Domain Model**

### Como persistir as entidades de negócio?

- Table Module -> com o **Table Data Gateway**
- Domain Model muito similar à estrutra da DB -> **Active Record**
- Domain Model complexo -> **Data Mapper**
- Garantir que os dados em memória são só atualizados num sítio -> **Identity Map**
- Garantir ligação entre objetos de domínio (memória) e entidades da BD -> **Identity Field**
- Evitar carregar para a memória toda a BD -> **Lazy Load**
- Abstrair o formato de dados da BD?
- Desenvolver classes próprias ou usar o modelo relacional?
- Como mapear o formato relacional na BD para as classes da linguagem?

### Notas e Questões sobre SQL

- Código SQL apenas nas camadas de acesso a dados

- Não esquecer que existem views no SQL ...
  - Facilita a construção e compreensão de strings de SQL no código
  - Permite reutilização de lógica
- Lógica de negócio no SQL?
  - Programadores estão à vontade com SQL?
  - Eficiência e Performance
  - Stored Procedures ou SQL Dinâmico?
  - Usar stored procedures:
    - Apenas para as operações CRUD?
    - Implementar lógica de negócio?

## Outras questões

- Gerir complexidade do projeto (nº de classes/métodos)
- Interoperabilidade de plataformas
- Integração de aplicações
- Multi-canal
- Segurança, autenticação e autorização
- Suporte para múltiplas BDs

## Bibliografia

- Microsoft Application Architecture Guide, 2nd Edition. Microsoft Press.
  - [http://msdn.microsoft.com/en-us/library/dd673617.aspx](http://msdn.microsoft.com/en-us/library/dd673617.aspx)
- Design patterns : elements of reusable object-oriented software. Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides.
  - [GoF]
- Patterns of Enterprise Application Architecture. Martin Fowler. Adisson-Wesley.
  - [PoEAA]

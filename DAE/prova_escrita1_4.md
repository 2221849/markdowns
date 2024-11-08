# Desenvolvimento de Aplicações Empresariais

## Padrões de Acesso a Dados e ORM (Object-Relational Mapping)

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

# Desenvolvimento de Aplicações Empresariais

## Enunciado do Projeto

### Objetivo

O objetivo deste projeto é implementar e testar uma aplicação empresarial de monitorização de embalagens inteligentes (isto é, equipadas com sensores e conectividade sem fios).

### Cenário

A loja online XYZ vende uma grande variedade de produtos que vão desde produtos alimentares, tais como gelados, a produtos eletrónicos, como aparelhos de televisão. Para aumentar a qualidade de serviço e melhorar seus processos, a empresa necessita de uma aplicação – **Aplicação de Monitorização** – que permita recolher as informações de sensores de monitorização integrados nas embalagens de alguns produtos ou encomendas.

Esses sensores podem monitorizar temperatura, pressão atmosférica, aceleração e/ou posicionamento global, enviando informações a intervalos regulares através de redes sem fios desde o momento da ativação até à desativação ou esgotamento da bateria.

Além de receber informações desses sensores, a aplicação precisará comunicar com outros sistemas da empresa, incluindo:

- **Sistema de Logística** (utilizado pelos armazéns para preparar, embalar e despachar encomendas).
- **Sistema de Gestão Operacional** (onde gestores acompanham o estado das encomendas).
- **Sistema de Apoio ao Cliente** (onde os clientes acompanham as encomendas em trânsito).

A **Aplicação de Monitorização** será relevante apenas após as encomendas estarem prontas para expedição, um processo iniciado pelo **Sistema de Logística**.

### Exemplo de Cenário

1. Maria Silva compra dois televisores (modelos ABC e BCE) e duas dúzias de gelados XPTO.
2. No Armazém #1, os gelados são colocados numa caixa isotérmica equipada com um sensor de temperatura. O sensor é ativado e associado à encomenda no **Sistema de Logística**.
3. No Armazém #2, os televisores são preparados, cada um com sensores de posicionamento global e de aceleração, que são ativados e associados à encomenda.
4. Desde a ativação, os sensores enviam dados à **Aplicação de Monitorização**, permitindo ao Gestor e ao Cliente consultar informações, como a última temperatura registada ou impactos detectados nos produtos.

### Requisitos Tecnológicos

- **RT1.** O sistema deverá ser auto-contido, composto por:
  - Aplicação backend (foco do projeto) e motor de base de dados.
  - Aplicação frontend para simular sistemas externos e testar funcionalidades do backend.

- **RT2.** O backend deverá ser desenvolvido com **Jakarta Enterprise Edition**, seguindo o modelo **REST Service**.

- **RT3.** O frontend pode utilizar tecnologias como **Vue.JS/NUXT** para consumir serviços REST.

- **RT4.** O banco de dados deverá ser relacional com licença GPL ou LGPL, preferencialmente **PostgreSQL**.

- **RT5.** Adotar padrões arquiteturais que promovam a modularidade, como **MVC**, **ORM**, **lazy loading**, etc.

### Grupos: Regras

1. Os grupos devem ter 4 estudantes.
2. A classificação será igual para todos os membros do grupo.
3. A apresentação final poderá incluir perguntas individuais, impactando a nota do grupo.

### Entrega Intermédia (Primeira Entrega)

1. Especificação da **API REST** em formato PDF.
2. Nome do arquivo: `DAE-2024-25-API-Projeto-#####-#####-#####-#####.pdf`, com os números dos estudantes.
3. Entrega no repositório Moodle até à data agendada.
4. Cada endpoint da API deverá ser especificado, seguindo exemplos fornecidos.

### Entrega Final

1. Arquivo ZIP, RAR ou 7Z contendo:
   - Projeto Java (backend).
   - Projeto Vue.JS/NUXT (frontend).
   - Especificação final da API REST, se diferente da entrega intermédia.

2. Nome do arquivo: `DAE-2024-25-Projeto-#####-#####-#####-#####`.
3. Entrega no repositório Moodle até à data agendada.

### Avaliação

- **25%** - Entrega Intermédia (Especificação da API).
- **75%** - Entrega Final (Implementação do Projeto):
  - **85%** - Funcionalidades implementadas (backend e frontend).
  - **15%** - Extras implementados.

### Notas Importantes

1. Configurações de tipos de produtos, embalagens e sensores são "compile time" e não são funcionalidades obrigatórias, mas podem ser considerados extras.
2. Extras podem incluir importação de dados via CSV/Excel/API, frontend responsivo, notificações por e-mail, entre outros.
3. A entrega final do projeto requer apresentação e defesa das escolhas feitas na análise, design e implementação, além de uma demonstração das funcionalidades.

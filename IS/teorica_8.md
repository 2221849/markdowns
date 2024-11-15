# Integração de Sistemas

## Aula Teórica 8

### Facilitar a Operabilidade na Integração de Sistemas

À medida que sistemas e tecnologias evoluem, surgem continuamente novas necessidades e padrões. Mesmo com a existência de padrões de integração, a integração direta entre sistemas (ou "integração a baixo nível") pode tornar-se onerosa e inflexível, dificultando a interoperabilidade entre sistemas heterogêneos.

### Padrões de Arquitetura para Integração

Existem diferentes abordagens de arquitetura para facilitar a comunicação entre sistemas:

1. **Ponto-a-Ponto Sincrono**:
   - Ideal para cenários simples com poucos sistemas.
   - Facilita a comunicação direta entre pares de sistemas.
   - Requer um esforço maior de desenvolvimento para cada novo sistema integrado, já que novas conexões devem ser manualmente configuradas.

2. **Hub-and-Spoke**:
   - Abordagem mais centralizada onde um hub serve como intermediário entre sistemas.
   - Reduz a complexidade das conexões individuais, mas aumenta o peso do hub, exigindo mais recursos e esforço dos desenvolvedores para gerenciar o sistema central.

3. **Enterprise Service Bus (ESB)**:
   - Melhor solução para empresas com ambientes complexos e grande número de sistemas.
   - Arquitetura orientada a serviços, permitindo um ambiente de integração padronizado, escalável e reutilizável.
   - Pode ser oneroso e complicado, mas oferece flexibilidade e robustez.
   - Necessário parametrizar o ESB e configurar os sistemas para que possam “falar” entre si, utilizando protocolos de comunicação suportados pelo ESB.

### O Papel do ESB

O ESB funciona como um mecanismo de “cola” que une diversos aplicativos, serviços, arquivos e portas de entrada e saída (I/O ports), garantindo a comunicação entre eles. Em um ESB, mensagens entre sistemas podem ser normalizadas, facilitando o intercâmbio de dados em diferentes formatos.

Exemplo de implementação de ESB: **Apache Camel** - utiliza normalizadores para uniformizar mensagens em diferentes formatos e oferece um conjunto de conectores.

### Node-RED como Ferramenta de Integração

O **Node-RED** é uma ferramenta visual para desenvolvimento de integrações, desenvolvida pela IBM em 2013. A plataforma é baseada em navegador, de código aberto, escrita em JavaScript e voltada para automação e integração por meio de fluxos.

#### Elementos de um Flow no Node-RED

No Node-RED, os fluxos (flows) são compostos por diferentes etapas interconectadas. Os conectores, também chamados de “nós” (nodes), são divididos em três tipos principais:

1. **Input Nodes**: Capturam dados do usuário ou de outros sistemas para iniciar o fluxo.
2. **Output Nodes**: Enviam dados processados para fora do fluxo, seja para outros sistemas, bancos de dados ou APIs.
3. **Function Nodes**: Permitem desenvolver lógica personalizada ou conectores inexistentes na biblioteca nativa.

#### Benefícios do Node-RED

- Permite criar fluxos visuais de integração com rapidez.
- A interface simplifica a compreensão e o design do fluxo.
- Suporta diversos conectores e protocolos, facilitando a integração com sistemas heterogêneos.
- Uma vez desenhado o fluxo, é necessário fazer o **deploy** para que ele entre em operação.

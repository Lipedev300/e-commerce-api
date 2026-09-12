# Tropa das lojas

 O Tropa das Lojas compreende um sistema agregador de lojas e um e-commerce, destinado principalmente para pequenos vendedores que desejem expandir suas vendas e gerenciar melhor seu trabalho. Além disso, o projeto é voltado para clientes que desejem maior facilidade para encontrar produtos mais perto de onde estão.
O sistema é inclusive focado em acessibilidade para pessoas com deficiência, incluindo compatibilidade com leitores de tela. Isso possibilita que usuários cegos e com deficiência visual tanto sejam vendedores buscando aumentar suas vendas, como clientes buscando encontrar seus produtos mais perto de onde estão.

# Requisitos.

## Requisitos funcionais.

RF01 - Cadastro de Vendedores e Lojas: O sistema deve permitir que vendedores cadastrem seus perfis e suas respectivas lojas, informando dados de localização, categorias de produtos comercializados e endereço de atendimento.
RF02 - Perfil e Interesses do Cliente: O cliente deve poder cadastrar seu perfil informando suas preferências e interesses de produtos, permitindo que a plataforma sugira lojas compatíveis.
RF03 - Busca Geolocalizada e por Produtos: O sistema deve permitir a busca por produtos avulsos e listar lojas próximas à localização do cliente que possuem o item em estoque.
RF04 - Gestão de Estoque por Loja: O sistema deve manter o controle rigoroso de estoque por estabelecimento, impedindo a finalização de pedidos caso a quantidade solicitada exceda a disponibilidade.
RF05 - Fluxo de Pedidos e Aprovação: O cliente deve poder criar um pedido consolidado, que será enviado ao vendedor para análise e aprovação prévia.
RF06 - Pagamento via PIX: O sistema deve integrar o fluxo de pagamento via PIX após a aprovação do pedido pelo vendedor.
RF07 - Chat com Suporte a Mensagens de Áudio: O sistema deve disponibilizar um canal de comunicação interno (chat) entre cliente e vendedor pós-pedido, com suporte ao envio e reprodução de mensagens de áudio para acessibilidade.
RF08 - Gestão de Entrega: O chat e o sistema de pedidos devem permitir alinhar a modalidade de entrega (retirada local ou envio pelos Correios/transportadora).

## Requisitos Não Funcionais.

RNF01 - Acessibilidade (WCAG / Leitores de Tela): O front-end mobile deve ser totalmente compatível com leitores de tela (como NVDA/TalkBack/VoiceOver), garantindo navegação fluida para usuários com deficiência visual.
RNF02 - Arquitetura de monolito modular + app mobile: O projeto deve ser desacoplado em dois repositórios independentes (Back-end em Django Ninja e Front-end em React Native / Expo Router).
RNF03 - Documentação Automática da API: O back-end deve expor documentação interativa utilizando o Swagger/OpenAPI gerado pelo Django Ninja.
RNF04 - Ambiente Isolado via Docker: O banco de dados e os serviços de suporte devem ser executados em containers Docker para garantir portabilidade entre desenvolvimento e produção.

# Modelagem de dados (principais entidades):
 
 1. User (Usuário): Representa qualquer pessoa cadastrada no sistema.
Atributos:

id: Chave primária (UUID ou AutoField).
full_name: String (Nome completo).
email: String (Único, usado para login).
phone: String (Telefone/WhatsApp, ex: com DDI e DDD).
role: Enum / Choice ('client' ou 'vendor').
interests: Relacionamento Many-to-Many com a entidade Category (aplicável apenas se o usuário for um cliente).
Store (loja): cas o usuário seja um vendedor, este é o relacionamento one-to-one com a tabela de lojas, trazendo o id da loja específica do vendedor.

Store (Loja):
id: Chave primária (UUID).
vendor: Chave estrangeira (1/1) vinculada ao User.
name: String (Nome comercial).
description: String (Descrição do negócio).
categories: Relacionamento Many-to-Many com Category.
cep: String.
street: String (Preenchido via API).
number: String (Informado pelo lojista).
complement: String (Opcional).
neighborhood: String (Preenchido via API).
city: String (Preenchido via API).
state: String (Preenchido via API).
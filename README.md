# Rocketseat DDD challenge
This is a challenge proposed by Rocketseat to create a simple DDD application using Node.js and TypeScript. Check out [this link](https://efficient-sloth-d85.notion.site/Atividade-Mapeando-o-dom-nio-38963358ffd74289b824ff73b187165d) for more information about the challenge.

## Key points given by the domain expert (in pt-br)

Geral:
- [x] Precisamos de uma solução que nos permita *rastrear* cada **produto** individualmente
- [x] *definir quantidades mínimas* de **estoque**
- [x] *receber alertas* quando estivermos ficando sem um determinado **produto**
- [x] *visualizar* o histórico de **vendas** e **estoque** para ajudar a tomarmos decisões futuras de compra

Rasteamento:
- [x] *atribuir* um **número de identificação único** a cada **produto**
  - para podermos *rastrear* facilmente suas movimentações em nosso **estoque**
- [x] adicionar **informações extras**, como **tamanho** e **cor**
  - para tornar o rastreamento ainda mais preciso

Quantidades mínimas de estoque:
- [x] *definir* um *limite mínimo* para cada **produto**
  - [x] de forma que pudéssemos receber um *alerta* quando o estoque estiver chegando próximo ao fim
  - Isso nos ajudaria a garantir que nunca fiquemos sem um produto popular e também nos permitiria fazer pedidos mais eficientes.

Receber alertas:
- [x] receber alertas por e-mail e também por meio de uma notificação em nosso sistema de gerenciamento de estoque

Histórico de vendas e estoque:
- [x] ver quantos **produtos** vendemos em um determinado período
- [x] qual foi o lucro gerado por **produto**
- [x] quais **produtos** estão vendendo melhor em cada período
- [x] observar as *tendências* de estoque ao longo do tempo

Outras funcionalidades:
- [x] *criar e gerenciar* **ordens de compra** automaticamente
  - com base nas quantidades mínimas de estoque definidas e nas tendências de vendas
- [x] integrar o sistema com nossos fornecedores
  - para que pudéssemos receber atualizações automáticas sobre os prazos de entrega de novas remessas

## Domain model

Products
- id (number, unique)
- name
- size
- color
- minimum quantity
- Stock (Aggregate)

Stocks 
- Product (Aggregate)
- quantity

Sales
- Product
- date
- quantity
- price

Orders
- Product
- date
- arriveAt
- quantity
- price

## Use cases

### Warehouse

Products
- Create
- Define minimum quantity
- Calculate profit
- Get Best Sellers
- Update (name, size, color, quantity)

Sales
- Register
- List (from product and period)
- Get tendance

Orders
- Register
- List (from product and period)
- Change arrival date

### Notifications

- Send alert (e-mail and system in controller)
- Read alert

## Events
- Product below minimum quantity
  - Send alert
  - Registe order
- Register sale
  - Send alert
- Register order
  - Send alert
- Arrival order
  - Change ArriveAt date
  - Send alert

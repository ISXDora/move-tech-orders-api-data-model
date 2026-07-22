## Entidades 

* Docs: https://dbml.dbdiagram.io/docs 

### Schema DBML

```dbml
Table orders {
  id string [primary key , default: 'uuid_generate_v4()'] // Identificador único gerado com uuidv4
  customer string [not null] // Nome do cliente não pode ser nulo
  status string [default: "open"] // Status do pedido, inicia por padrão como open
  created_at datetime [not null, default: `now()`] // Registra data e hora no momento da criação do registro
}

Table items {
  id string [primary key, default: 'uuid_generate_v4()'] // Identificador único gerado com uuidv4 
  order_id string [not null, ref: > orders.id] // Foreign key referência orders.id na tabela orders
  sku string [not null] // Código sku não pode ser nulo
  description string [not null] // Descrição do item do pedido e não pode ser nulo
  quantity integer [not null] // Quantidade do item para o pedido
}

// Relacionamento 1:N (one-to-many) 
// Um pedido pode ter vários itens e quando um pedido é deletado os itens associados também serão deletados juntos.
Ref: orders.id < items.order_id [delete: cascade]

Records orders(id, customer, status) {
  0, 'Aldenira', 'open'
}

Records items(id, order_id, sku, description, quantity) {
  0, 0, 'ABC123', 'Arroz', 2
  1, 0, 'ABC321', 'Ovos', 12
}
```

### Diagrama 
<iframe width="560" height="315" src='https://dbdiagram.io/e/6a601f06067336e1dec767a1/6a601f12067336e1dec7681a'> </iframe>
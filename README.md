# external-api-docs


### Buscar dados do usuário


##### Request
```shell
curl --location 'https://pagar.taon.app/api/bots/user/<id>' \
--header 'Api-Key: <Api key>'
```
##### Response

```jsonc
{
    "id": "", // id do usuário
    "name": "", // Nome completo so usuário
    "nickname": "", // Nome como chamamos o usuário
    "email": "", // email do usuário
    "cpf": "", // cpf
    "balance": 999.99, // saldo do usuário
    "mgm_code": "", // código MGM do usuário
    "product_main_count": 1, // quantidade de produtos comprados historicamente do usuário (mais relevante é o valor 0 que significa que nunca comprou)
    "last_main_product_id": "", // id do último produto comprado (pode estar disponível para renovação)
    "available_products": [ // Produtos disponíveis para compra
        { // Entidade 'Produto'
            "id": "", // id do produto
            "amount": 45.9, // preço do produto
            "display_info": {
                "icon": "", // ícone do produto no formato https://static.taon.app/icon_<name>.png
                "bg": "", // image bg do produto no formato https://static.taon.app/bg_<name>.png
                "display_name": "", // nome comercial do produto
                "features": [
                    {
                        "icon": "", // icone feature no formato https://static.taon.app/icon_<name>.png
                        "label": "" // nome da feature
                    }                    
                ],
                "attr": [
                    {
                        "icon": "", // icone atributos no formato https://static.taon.app/icon_<name>.png
                        "label": "" // nome do atributo
                    }
                ]
            },
            "free_items_count": 2, // número de produtos grátis que esse produto suporta
            "product_type": "", // tipo do produto (main | mcp-app | mcp-gb)
            "available_subproducts": [
                {} // Entidade 'Produto'
            ],
            "purchased_subproducts": [
                {} // Entidade 'Produto'
            ]
        }
    ],
    "purchased_products": [ // Produtos ativos do usuário
        {} // Entidade 'Produto'
    ],   
    "created_at": "", // Data de cadastro do usuário (UTC)
    "phone_number": "(11) 98656-0599", // Número da linha associada ao usuário
}
```




##### Gerar link de pagamento para compra de produtos
```shell
curl --location 'https://pagar.taon.app/api/bots/pix' \
--header 'Api-Key: <Api key>' \
--header 'Content-Type: application/json' \
--data '{
    "user_id": "<user id>",
    "product_id": "<product id>",
    "extra_free_items": [
        "<product id>",
        "<product id>"
    ],
    "extra_paid_products_ids": [
        "<product id>",
        "<product id>"
    ],
    "bypass_product_availability": false // [opcional] Ignora as regras de tags se for true 
}'
```

#####

```jsonc
{
    "pay_id": "91c5151a", // id de pagamento pix para usar em https://pagar.taon.app/p/<id>
    "amount": 11, // valor gerado do pix - Pode ser diferente da soma do pedido baseado em saldo remanescente do usuário
    "payment_type": "pix", // meio de pagamento (será 'wallet' caso o usuário tenha saldo para cobrir o total do pedido ou 'pix' caso o saldo seja insuficiente ou zero)
    "pix_data": {
        "expiration_date": "", // data de expiração do pix
        "qr_code": "" // código QR para pagamento do pix copia e cola
    },
    "products_transaction_id": "" // id do pedido de compra
}
```

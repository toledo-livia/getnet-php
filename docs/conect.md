#Info

## Usage

```php
use getnet-php\lib\GetNet;

    LIVE;
    END_POINT_HOMOLOGATION;
    END_POINT_PRODUCTION;
    API_VERSION;
    AUTH;

$getnet = new GetNet();

### Get Client
$response = $getnet_request->getClientId();

### Get Client Secret
$response = $getnet_request->getClientSecret();

### Get URL
$response = $getnet_request->full_api_url();

### Get URL Authenticate
$response = $getnet_request->api_url_authenticate();

```
#Request

## Usage

```php
use getnet-php\lib\GetNet_Request;

$getnet_request = new GetNet_Request($path, $method,$live = GetNet::LIVE);
    $path

### GET 
```

### Create and Authorize Payment
```php
$array = [
        "amount"    => 100,
        "currency"  => "BRL",
        "order"     => [
            "order_id" => "6d2e4380-d8a3-4ccb-9138-c289182818a3"
        ],
        "customer" => [
            "customer_id"     => "customer_21081826",
            "first_name"      => "João",
            "last_name"       => "da Silva",
            "name"            => "João da Silva",
            "email"           => "customer@email.com.br",
            "document_type"   => "CPF",
            "document_number" => "12345678912",
            "phone_number"    => "5551999887766",
            "billing_address" => [
                "street"      => "Av. Brasil",
                "number"      => "1000",
                "complement"  => "Sala 1",
                "district"    => "São Geraldo",
                "city"        => "Porto Alegre",
                "state"       => "RS",
                "country"     => "Brasil",
                "postal_code" => "90230060"
            ]
        ],
        "device" => [
            "ip_address" => "127.0.0.1",
        ],
        "shippings" => [
            [
                "first_name"      => "João",
                "name"            => "João da Silva",
                "email"           => "customer@email.com.br",
                "phone_number"    => "5551999887766",
                "shipping_amount" => 3000,
                "address" => [
                    "street"      => "Av. Brasil",
                    "number"      => "1000",
                    "complement"  => "Sala 1",
                    "district"    => "São Geraldo",
                    "city"        => "Porto Alegre",
                    "state"       => "RS",
                    "country"     => "Brasil",
                    "postal_code" => "90230060"
                ]
            ]
        ],
        "credit" => [
            "delayed"             => false,
            "authenticated"       => false,
            "pre_authorization"   => false,
            "save_card_data"      => false,
            "transaction_type"    => "FULL",
            "number_installments" => 1,
            "soft_descriptor"     => "LOJA*TESTE*COMPRA-123",
            "dynamic_mcc"         => 1799,
            "card" => [
                "number_token"     => "dfe05208b105578c070f806c80abd3af09e246827d29b866cf4ce16c205849977c9496cbf0d0234f42339937f327747075f68763537b90b31389e01231d4d13c",
                "cardholder_name"  => "JOAO DA SILVA",
                "security_code"    => "123",
                "brand"            => "Mastercard",
                "expiration_month" => "12",
                "expiration_year"  => "20"
            ]
        ]
    ];


    $authenticate = [
        'client_id'     => 'eb153ef1-4e41-4898-92d4-ee407e47b199',
        'client_secret' => 'fcf1e007-5cf9-4fda-830d-e51f9de0b9e6'
    ];

    $authorization = new GetNet_Token($authenticate);
    $authorization->authorize();



    // var_dump($array);
    // GetNet::setClientId();
    // GetNet::setClientSecret();
    // var_dump(GetNet::getSellerId());
    // echo'<pre>';
    // var_dump(new GetNet_Transaction($array));

```
## Errors
### 4xx errors
#### Field validation error
```php

// payment without amount
$decode = [
    "externalId" => "23524234322523-32523",
    "capture" => true,
    "amount" => null,
    "interest" => 0,
    "creditCard" => [
        "installments" => 1,
        "number" => "4111.1111.1111.1111",
        "holder" => "John Doe",
        "expiration" => "12/2020",
        "cvv" => "123",
        "brand" => "visa"
    ],
    "customer" => [
        "externalId" => "1234",
        "name" => "John Doe",
        "document" => "112.452.662-12",
        "address" => [
            "street" => "Rua Joaquim Floriano",
            "number" => "820",
            "complement" => "20 andar",
            "zipcode" => "04534-003",
            "city" => "São Paulo",
            "state" => "SP",
            "country" => "BR"
        ]
    ],
    "items" => [
        [
            "externalId" => "123",
            "type" => "ticket",
            "name" => "My VIP ticket",
            "unitPrice" => 100,
            "quantity" => 1
        ]
    ]
];

    throw GetNet_Exception::buildWithFullMessage($decode);
*/
```
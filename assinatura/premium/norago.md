---
layout: default
title: Streaming
parent: Assinatura Premium
nav_order: 1
nav_enabled: true
---

# {{ page.title }}

[Documentação NoraGo](https://setplex.com/developers/overview.html)

## API do Meio

| **USUÁRIO:** meioapi        | **TOKEN:** xxx
| **URL:** https://meio.norago.tv/        | **networkID:** 36294d9f-171b-4b83-9d31-cb1065d5cdaf

## Função python de request
Função recebe endpoint e um array. No array precisa passar as informações de login e token.

Retorna um json

```python
def norago_request(endpoint,data):
    headers = {"Content-Type": "application/json"}
    r = requests.post("https://meio.norago.tv"+endpoint, headers=headers,json=data)
    return json.loads(r.text) 
```

## Listar subscriptions (PLANOS)
```python
data = {"auth": {"token": token,"login": "meioapi"}}
norago_request("/apex/v2/subscriptions/get",data)
```

## Listar todos os subscribers (ASSINANTES)
```python
data = {"auth": {"token": token,"login": "meioapi"}, "pageRequest": {"page": 0,"number": 100}, "networkId": "36294d9f-171b-4b83-9d31-cb1065d5cdaf"}
norago_request("/apex/v2/networks/subscribers/get",data)
```

## Listar dados de um subscriber

{: .obs }
accountNumber e lastName são Obrigatórios.
É possivel pegar o expirationTime, currentSubscriptionStatus


```python
data = {"auth": {"token": token,"login": "meioapi","accountNumber":"MO534335", "lastName": "Lamata"}}
norago_request("/apex/v2/subscribers/get",data)
```
## Atualizar prox_vencimento de um subscriber
```python
data = {"auth": {"token": token,"login": "meioapi","accountNumber":"MO534335", "lastName": "Lamata"}, "activeUntil": "2024-08-21T08:00:00Z"}
norago_request("/apex/v2/subscribers/subscription/update",data)
```

## Search Subscribers
```python
data = {"auth": {"token": token,"login": "meioapi"}, "email": email}
norago_request("/apex/v2/subscribers/search",data)
```

## Criar subscriber E subscription na mesma chamada
```python
data = {"auth": {
	"token": token,
	"login": "meioapi"
	}, 
	"subscriber": {
		"password": "123456", 
		"firstName": "Nome", 
		"lastName": "Sobrenome", 
		"email": "email@gmail.com", 
		"phone": "999999999999999", 
		"zipCode": "-",
		"address": "-",
		"city": "-",
		"country": "BR",
		"timeZone": "America/Sao_Paulo"
	},
	"subscription": {
		"subscriptionId":"WHYZYKEGY"
	},
	"deviceCount": 3, 
	"approvalRequired": "false",
	"paymentSystemType":"EXTERNAL_PAYMENTS", 
	"externalPaymentSystemType": "PAYPAL_EXPRESS", 
	"transactionId": "123456777"
}
norago_request("/apex/v2/payments/doSingle",data)
```
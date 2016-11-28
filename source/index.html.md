---
title: Referência para a API do BrucerBanner

toc_footers:
  - <a href='https://bitbucket.org/oqv/bruce_banner_sinatra'>Projeto no Bitbucket</a>
  - <a href='https://h-banners.oqvestir.com.br/api/v2/site_page'>Staging V2</a>
  - <a href='https://h-banners.oqvestir.com.br/api/v3/site_page'>Staging V3</a>
  - <a href="https://brucebanner.oqvestir.com.br/api/v2/site_page">Production V2</a>
  - <a href="https://brucebanner.oqvestir.com.br/api/v3/site_page">Production V3</a>

includes:
  - errors

search: true
---

# Introdução

Essa API é utilizada para retornar os dados de SEO das páginas do site
e também seus respectivos banners.


# V2

Todos os resultados referentes à banners são ordenados pela data de ativação do mesmo.

## Listar Todas as Páginas

Esse endpoint traz todos os banners de todos os sources de uma vez.

### HTTP Request

`GET https://h-banners.oqvestir.com.br/api/v2/`

<aside class="notice">
  Nenhum parâmetro é necessário, caso queira resultados filtrados, ver parâmetros disponíveis a baixo.
</aside>

### Parâmetros aceitos
Parâmetro | Valores Aceitos | Descrição
--------- | --------------- | -----------
url | string | URL da página que deseja trazer as informações. Ex: /novidades
source_kind | app_iphone, app_android, mobile, desktop | Para qual dispositivo esse banner será servido.


<aside class="warning">
  `source_kind` que não estiver na lista de valores aceitos, fará busca direta pelo banner para achar a página.
  Isso é custoso para o sistema e deve ser evitado. Usar a API v1 caso queira esse efeito.
</aside>

> Exemplo de retorno quando acha somente BANNER ou o BANNER não possui páginas associadas:

```json
{
  "id":null,
  "url":null,
  "desc":null,
  "title":null,
  "inserted_at":null,
  "updated_at":null,
  "banners":[
    {
    "id":339,
    "title":"20160920_desk_homeSmall1_outlet",
    "image_url":"https://d3k9vhbixcdyc5.cloudfront.net/original_20160815_home-p_outlet.jpg?63641534517",
    "link_url":"https://www.oqvestir.com.br/outlet",
    "description":"20160920_desk_homeSmall1_outlet",
    "active":true,
    "activation_date":"2016-09-20T00:04:00.000Z",
    "expiration_date":"2021-01-01T00:00:00.000Z",
    "source_kind":"desktop-home_small",
    "inserted_at":"2016-09-19T20:01:57.000Z",
    "updated_at":"2016-09-19T20:01:57.000Z",
    "site_page_id":null,
    "ga_event":null,
    "ga_ctr":null,
    "page_position":null,
    "short_description":null
    }
  ]
}
```

> Exemplo de retorno quando busca pelo source_kind=app_iphone

```json
{
  "id": null,
  "url": null,
  "desc": null,
  "title": null,
  "inserted_at": null,
  "updated_at": null,
  "banners": [
    {
      "id": 320,
      "title": "Sale Reebok! Até 40% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160712_828x634_sale-reebok.jpg?14683595797",
      "link_url": "https://www.oqvestir.com.br/reebok",
      "description": "Sale Reebok! Até 40% OFF",
      "active": true,
      "activation_date": "2016-07-12T22:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-11T14:52:51.000Z",
      "updated_at": "2016-07-12T21:39:39.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 319,
      "title": "Tommy Hilfiger com até 40% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160712_828x634_sale-tommy.jpg?14683595796",
      "link_url": "https://www.oqvestir.com.br/tommy-hilfiger",
      "description": "Tommy Hilfiger com até 40% OFF",
      "active": true,
      "activation_date": "2016-07-12T18:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-11T14:52:23.000Z",
      "updated_at": "2016-07-12T21:39:39.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 318,
      "title": "New in 7 For All Mankind!",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160712_828x634_7forallmankind.jpg?14683595796",
      "link_url": "https://www.oqvestir.com.br/7-for-all-mankind",
      "description": "New in 7 For All Mankind!",
      "active": true,
      "activation_date": "2016-07-12T13:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-11T14:51:55.000Z",
      "updated_at": "2016-07-12T21:39:39.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    }
  ]
}
```
> Exemplo de resultado quando acha uma página pela url, mas não tem banner.

```json
{
  "id": 1,
  "url": "/novidades",
  "desc": "Olha essa descrição.",
  "title": "Pagina legal e cheia de novidades!",
  "inserted_at": "2016-10-03T19:28:09.000Z",
  "updated_at": "2016-10-03T19:28:09.000Z",
  "banners": []
}
```

> Exemplo de resultado quando acha uma página pela URL e com BANNER.

```json
  {
  "id": 1,
  "url": "/novidades",
  "desc": "Olha essa descrição.",
  "title": "Pagina legal e cheia de novidades!",
  "inserted_at": "2016-10-03T19:28:09.000Z",
  "updated_at": "2016-10-03T19:28:09.000Z",
  "banners": [
    {
      "id": 275,
      "title": "Confira as novidades do verão 17",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160707_828x634_nov-verao.jpg?14683595778",
      "link_url": "https://www.oqvestir.com.br/novidades",
      "description": "Confira as novidades do verão 17",
      "active": true,
      "activation_date": "2016-07-07T13:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-06T20:20:50.000Z",
      "updated_at": "2016-07-12T21:39:37.000Z",
      "site_page_id": 1,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    }
  ]
}
```

## OnBoarding Páginado

Esse endpoint traz os banners páginados de acordo com os paramêtros. Não inclui informações das página do site.

### HTTP Request

`GET https://h-banners.oqvestir.com.br/api/v2/paginate`

<aside class="notice">
   É OBRIGATÓRIO informar a página que você necessita, mesmo que seja a primeira.
</aside>

### Parâmetros aceitos
Parâmetro | Valores Aceitos | Descrição
--------- | --------------- | -----------
page | integer | Número da página que você quer. Ex:. 1
source_kind | app_iphone, app_android, mobile, desktop | Para qual dispositivo esse banner será servido.


> Exemplo de retorno BANNERS páginados para ONBOARDING nos. Parâmetros usados: page=1&source_kind=app_iphone

```json
{
  "banners": [
    {
      "id": 320,
      "title": "Sale Reebok! Até 40% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160712_828x634_sale-reebok.jpg?14683595797",
      "link_url": "https://www.oqvestir.com.br/reebok",
      "description": "Sale Reebok! Até 40% OFF",
      "active": true,
      "activation_date": "2016-07-12T22:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-11T14:52:51.000Z",
      "updated_at": "2016-07-12T21:39:39.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 319,
      "title": "Tommy Hilfiger com até 40% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160712_828x634_sale-tommy.jpg?14683595796",
      "link_url": "https://www.oqvestir.com.br/tommy-hilfiger",
      "description": "Tommy Hilfiger com até 40% OFF",
      "active": true,
      "activation_date": "2016-07-12T18:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-11T14:52:23.000Z",
      "updated_at": "2016-07-12T21:39:39.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 318,
      "title": "New in 7 For All Mankind!",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160712_828x634_7forallmankind.jpg?14683595796",
      "link_url": "https://www.oqvestir.com.br/7-for-all-mankind",
      "description": "New in 7 For All Mankind!",
      "active": true,
      "activation_date": "2016-07-12T13:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-11T14:51:55.000Z",
      "updated_at": "2016-07-12T21:39:39.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 295,
      "title": "On sale! Lolitta até 30% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160711_828x634_lolitta.jpg?14683595787",
      "link_url": "https://www.oqvestir.com.br/lolitta",
      "description": "On sale! Lolitta até 30% OFF",
      "active": true,
      "activation_date": "2016-07-11T22:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-08T11:51:45.000Z",
      "updated_at": "2016-07-12T21:39:38.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 294,
      "title": "Isolda com até 50% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160711_828x634_isolda.jpg?14683595786",
      "link_url": "https://www.oqvestir.com.br/isolda",
      "description": "Isolda com até 50% OFF",
      "active": true,
      "activation_date": "2016-07-11T18:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-08T11:51:18.000Z",
      "updated_at": "2016-07-12T21:39:38.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 293,
      "title": "Sale Bobstore até 60% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160711_828x634_bobstore.jpg?14683595786",
      "link_url": "https://www.oqvestir.com.br/bobstore",
      "description": "Sale Bobstore até 60% OFF",
      "active": true,
      "activation_date": "2016-07-11T13:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-08T11:50:55.000Z",
      "updated_at": "2016-07-12T21:39:38.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 284,
      "title": "Peças-chave jeans! Até 70% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160710_828x634_sale-jeans.jpg?14683595782",
      "link_url": "https://www.oqvestir.com.br/roupas/jeans?session=343&page=2",
      "description": "Peças-chave jeans! Até 70% OFF",
      "active": true,
      "activation_date": "2016-07-10T22:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-07T18:27:47.000Z",
      "updated_at": "2016-07-12T21:39:38.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 283,
      "title": "Camisas on sale! Até 80% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160710_828x634_sale-camisas.jpg?14683595782",
      "link_url": "https://www.oqvestir.com.br/roupas/blusas-camisa?session=192&page=2",
      "description": "Camisas on sale! Até 80% OFF",
      "active": true,
      "activation_date": "2016-07-10T18:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-07T18:27:22.000Z",
      "updated_at": "2016-07-12T21:39:38.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 282,
      "title": "New in acessórios!",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160710_828x634_acessorios.jpg?14683595781",
      "link_url": "https://www.oqvestir.com.br/acessorios",
      "description": "New in acessórios!",
      "active": true,
      "activation_date": "2016-07-10T13:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-07T18:26:37.000Z",
      "updated_at": "2016-07-12T21:39:38.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 281,
      "title": "J.Chermann com até 50% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160708_828x634_j-chermann.jpg?14683595781",
      "link_url": "https://www.oqvestir.com.br/j-chermann",
      "description": "J.Chermann com até 50% OFF",
      "active": true,
      "activation_date": "2016-07-08T22:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-07T17:46:28.000Z",
      "updated_at": "2016-07-12T21:39:38.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    }
  ],
  "pages": 7,
  "current_page": 1
}
```

## Expiração de CACHE

Expira um ou mais tipos de CACHE para a API de banners.

### HTTP Request

`GET https://h-banners.oqvestir.com.br/api/v2/expire`

<aside class="warning">
    Caso nenhum parâmetro seja passado, TODO o cache será eliminado.
</aside>

### Parâmetros aceitos
Parâmetro | Valores Aceitos | Descrição
--------- | --------------- | -----------
urlpage | string | URL da página. Ex: /novidades
source_kind | app_iphone, app_android, mobile, desktop | Para qual dispositivo esse banner será servido.


> Exemplo de retorno quando o cache é limpo.

```json
{
  "message": "Cache expirado"
}
```

# V3

Todas as chamadas feitas para a versão devem conter o HEADER `Accept-Platform`.
Sem esse header qualquer chamada realizada para a V3 será considerada uma `BAD REQUEST` com o código `422`.
Todos os resultados referentes à banners são ordenados pela data de ativação do mesmo.

## Listar Todas as Páginas

Esse endpoint traz todos os banners de todos os sources de uma vez.

### HTTP Request

`GET https://h-banners.oqvestir.com.br/api/v3/`

<aside class="notice">
  HEADER Accept-Platform é obrigatório.
  Nenhum parâmetro é necessário, caso queira resultados filtrados, ver parâmetros disponíveis a baixo.
</aside>

### Parâmetros aceitos
Parâmetro | Valores Aceitos | Descrição
--------- | --------------- | -----------
url | string | URL da página que deseja trazer as informações. Ex: /novidades
source_kind | app_iphone, app_android, mobile, desktop | Para qual dispositivo esse banner será servido.


<aside class="warning">
  `source_kind` que não estiver na lista de valores aceitos, fará busca direta pelo banner para achar a página.
  Isso é custoso para o sistema e deve ser evitado. Usar a API v1 caso queira esse efeito.
</aside>

> Exemplo de retorno quando acha somente BANNER ou o BANNER não possui páginas associadas:

```json
{
  "id":null,
  "url":null,
  "desc":null,
  "title":null,
  "inserted_at":null,
  "updated_at":null,
  "banners":[
    {
    "id":339,
    "title":"20160920_desk_homeSmall1_outlet",
    "image_url":"https://d3k9vhbixcdyc5.cloudfront.net/original_20160815_home-p_outlet.jpg?63641534517",
    "link_url":"https://www.oqvestir.com.br/outlet",
    "description":"20160920_desk_homeSmall1_outlet",
    "active":true,
    "activation_date":"2016-09-20T00:04:00.000Z",
    "expiration_date":"2021-01-01T00:00:00.000Z",
    "source_kind":"desktop-home_small",
    "inserted_at":"2016-09-19T20:01:57.000Z",
    "updated_at":"2016-09-19T20:01:57.000Z",
    "site_page_id":null,
    "ga_event":null,
    "ga_ctr":null,
    "page_position":null,
    "short_description":null
    }
  ]
}
```

> Exemplo de retorno quando busca pelo source_kind=app_iphone

```json
{
  "id": null,
  "url": null,
  "desc": null,
  "title": null,
  "inserted_at": null,
  "updated_at": null,
  "banners": [
    {
      "id": 320,
      "title": "Sale Reebok! Até 40% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160712_828x634_sale-reebok.jpg?14683595797",
      "link_url": "https://www.oqvestir.com.br/reebok",
      "description": "Sale Reebok! Até 40% OFF",
      "active": true,
      "activation_date": "2016-07-12T22:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-11T14:52:51.000Z",
      "updated_at": "2016-07-12T21:39:39.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 319,
      "title": "Tommy Hilfiger com até 40% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160712_828x634_sale-tommy.jpg?14683595796",
      "link_url": "https://www.oqvestir.com.br/tommy-hilfiger",
      "description": "Tommy Hilfiger com até 40% OFF",
      "active": true,
      "activation_date": "2016-07-12T18:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-11T14:52:23.000Z",
      "updated_at": "2016-07-12T21:39:39.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 318,
      "title": "New in 7 For All Mankind!",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160712_828x634_7forallmankind.jpg?14683595796",
      "link_url": "https://www.oqvestir.com.br/7-for-all-mankind",
      "description": "New in 7 For All Mankind!",
      "active": true,
      "activation_date": "2016-07-12T13:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-11T14:51:55.000Z",
      "updated_at": "2016-07-12T21:39:39.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    }
  ]
}
```
> Exemplo de resultado quando acha uma página pela url, mas não tem banner.

```json
{
  "id": 1,
  "url": "/novidades",
  "desc": "Olha essa descrição.",
  "title": "Pagina legal e cheia de novidades!",
  "inserted_at": "2016-10-03T19:28:09.000Z",
  "updated_at": "2016-10-03T19:28:09.000Z",
  "banners": []
}
```

> Exemplo de resultado quando acha uma página pela URL e com BANNER.

```json
  {
  "id": 1,
  "url": "/novidades",
  "desc": "Olha essa descrição.",
  "title": "Pagina legal e cheia de novidades!",
  "inserted_at": "2016-10-03T19:28:09.000Z",
  "updated_at": "2016-10-03T19:28:09.000Z",
  "banners": [
    {
      "id": 275,
      "title": "Confira as novidades do verão 17",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160707_828x634_nov-verao.jpg?14683595778",
      "link_url": "https://www.oqvestir.com.br/novidades",
      "description": "Confira as novidades do verão 17",
      "active": true,
      "activation_date": "2016-07-07T13:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-06T20:20:50.000Z",
      "updated_at": "2016-07-12T21:39:37.000Z",
      "site_page_id": 1,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    }
  ]
}
```

## OnBoarding Páginado

Esse endpoint traz os banners páginados de acordo com os paramêtros. Não inclui informações das páginas do site.

### HTTP Request

`GET https://h-banners.oqvestir.com.br/api/v2/paginate`

<aside class="notice">
  HEADER Accept-Platform é obrigatório.
   É OBRIGATÓRIO informar a página que você necessita, mesmo que seja a primeira.
</aside>

### Parâmetros aceitos
Parâmetro | Valores Aceitos | Descrição
--------- | --------------- | -----------
page | integer | Número da página que você quer. Ex:. 1
source_kind | app_iphone, app_android, mobile, desktop | Para qual dispositivo esse banner será servido.


> Exemplo de retorno BANNERS páginados para ONBOARDING nos. Parâmetros usados: page=1&source_kind=app_iphone

```json
{
  "banners": [
    {
      "id": 320,
      "title": "Sale Reebok! Até 40% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160712_828x634_sale-reebok.jpg?14683595797",
      "link_url": "https://www.oqvestir.com.br/reebok",
      "description": "Sale Reebok! Até 40% OFF",
      "active": true,
      "activation_date": "2016-07-12T22:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-11T14:52:51.000Z",
      "updated_at": "2016-07-12T21:39:39.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 319,
      "title": "Tommy Hilfiger com até 40% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160712_828x634_sale-tommy.jpg?14683595796",
      "link_url": "https://www.oqvestir.com.br/tommy-hilfiger",
      "description": "Tommy Hilfiger com até 40% OFF",
      "active": true,
      "activation_date": "2016-07-12T18:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-11T14:52:23.000Z",
      "updated_at": "2016-07-12T21:39:39.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 318,
      "title": "New in 7 For All Mankind!",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160712_828x634_7forallmankind.jpg?14683595796",
      "link_url": "https://www.oqvestir.com.br/7-for-all-mankind",
      "description": "New in 7 For All Mankind!",
      "active": true,
      "activation_date": "2016-07-12T13:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-11T14:51:55.000Z",
      "updated_at": "2016-07-12T21:39:39.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 295,
      "title": "On sale! Lolitta até 30% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160711_828x634_lolitta.jpg?14683595787",
      "link_url": "https://www.oqvestir.com.br/lolitta",
      "description": "On sale! Lolitta até 30% OFF",
      "active": true,
      "activation_date": "2016-07-11T22:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-08T11:51:45.000Z",
      "updated_at": "2016-07-12T21:39:38.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 294,
      "title": "Isolda com até 50% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160711_828x634_isolda.jpg?14683595786",
      "link_url": "https://www.oqvestir.com.br/isolda",
      "description": "Isolda com até 50% OFF",
      "active": true,
      "activation_date": "2016-07-11T18:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-08T11:51:18.000Z",
      "updated_at": "2016-07-12T21:39:38.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 293,
      "title": "Sale Bobstore até 60% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160711_828x634_bobstore.jpg?14683595786",
      "link_url": "https://www.oqvestir.com.br/bobstore",
      "description": "Sale Bobstore até 60% OFF",
      "active": true,
      "activation_date": "2016-07-11T13:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-08T11:50:55.000Z",
      "updated_at": "2016-07-12T21:39:38.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 284,
      "title": "Peças-chave jeans! Até 70% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160710_828x634_sale-jeans.jpg?14683595782",
      "link_url": "https://www.oqvestir.com.br/roupas/jeans?session=343&page=2",
      "description": "Peças-chave jeans! Até 70% OFF",
      "active": true,
      "activation_date": "2016-07-10T22:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-07T18:27:47.000Z",
      "updated_at": "2016-07-12T21:39:38.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 283,
      "title": "Camisas on sale! Até 80% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160710_828x634_sale-camisas.jpg?14683595782",
      "link_url": "https://www.oqvestir.com.br/roupas/blusas-camisa?session=192&page=2",
      "description": "Camisas on sale! Até 80% OFF",
      "active": true,
      "activation_date": "2016-07-10T18:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-07T18:27:22.000Z",
      "updated_at": "2016-07-12T21:39:38.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 282,
      "title": "New in acessórios!",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160710_828x634_acessorios.jpg?14683595781",
      "link_url": "https://www.oqvestir.com.br/acessorios",
      "description": "New in acessórios!",
      "active": true,
      "activation_date": "2016-07-10T13:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-07T18:26:37.000Z",
      "updated_at": "2016-07-12T21:39:38.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    },
    {
      "id": 281,
      "title": "J.Chermann com até 50% OFF",
      "image_url": "https://d3k9vhbixcdyc5.cloudfront.net/original_20160708_828x634_j-chermann.jpg?14683595781",
      "link_url": "https://www.oqvestir.com.br/j-chermann",
      "description": "J.Chermann com até 50% OFF",
      "active": true,
      "activation_date": "2016-07-08T22:00:00.000Z",
      "expiration_date": "2116-05-20T23:00:00.000Z",
      "source_kind": "app_iphone",
      "inserted_at": "2016-07-07T17:46:28.000Z",
      "updated_at": "2016-07-12T21:39:38.000Z",
      "site_page_id": null,
      "ga_event": null,
      "ga_ctr": null,
      "page_position": null,
      "short_description": null
    }
  ],
  "pages": 7,
  "current_page": 1
}
```

## Expiração de CACHE

Expira um ou mais tipos de CACHE para a API de banners.

### HTTP Request

`GET https://h-banners.oqvestir.com.br/api/v2/expire`

<aside class="warning">
    HEADER Accept-Platform é obrigatório.
    Caso nenhum parâmetro seja passado, TODO o cache será eliminado.
</aside>

### Parâmetros aceitos
Parâmetro | Valores Aceitos | Descrição
--------- | --------------- | -----------
urlpage | string | URL da página. Ex: /novidades
source_kind | app_iphone, app_android, mobile, desktop | Para qual dispositivo esse banner será servido.


> Exemplo de retorno quando o cache é limpo.

```json
{
  "message": "Cache expirado"
}
```
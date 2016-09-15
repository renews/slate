---
title: Referência para a API do BrucerBanner

toc_footers:
  - <a href='https://bitbucket.org/oqv/bruce_banner_sinatra'>Projeto no Bitbucket</a>
  - <a href='#'>API Staging - http://h-banners.oqvestir.com.br..oqvestir.com.br/api/v2</a>

includes:
  - errors

search: true
---

# Introdução

Essa API é utilizada para retornar os dados de SEO das páginas do site
e também seus respectivos banners.


# Páginas do Site

## Listar Todas as Páginas

Esse endpoint traz todos os banners de todos os sources de uma vez.

### HTTP Request

`GET http://h-brucebanner.oqvestir.com.br/api/v2/`

<aside class="notice">
  Nenhum parâmetro é necessário, caso queira resultados filtrados, ver parâmetros disponíveis a baixo.
</aside>

### Parâmetros aceitos
Parâmetro | Valores Aceitos | Descrição
--------- | --------------- | -----------
url | string | URL da página que deseja trazer as informações. Ex: /novidades
source_kind | app_iphone, app_android, mobile, desktop | Para qual dispositivo esse banner será servido.
page_position | string | Em qual lugar da página esse banner deve aparecer.

<aside class="warning">
  `source_kind` que não estiver na lista de valores aceitos, fará busca direta pelo banner para achar a página.
  Isso é custoso para o sistema e deve ser evitado. Usar a API v1 caso queira esse efeito.
</aside>

> Estrutura do JSON retornado:

```json
  {
    "site_pages": [
      {
        "id":1,
        "url":"/novidades",
        "title":"Compre ROUPAS das melhores Marcas no OQVestir! blusas, vestidos, saias, calças, lingerie e muito mais. Aproveite!",
        "description":"Lançamentos no OQVestir: roupas, acessórios, sapatos, moda praia, fitness da atual coleção da marca! Frete grátis, troca fácil e pagamento em até 10x sem juros. Aproveite...",
        "inserted_at":"26.9",
        "updated_at":"9.9",
        "banners":[]
      },
      {
        "id":2,
        "url":"/animale/roupas",
        "title":"ROUPAS - Compre blusas, vestidos, saias, calças, lingerie e mais | OQVestir",
        "description":"Compre ROUPAS das melhores Marcas no OQVestir! blusas, vestidos, saias, calças, lingerie e muito mais. Aproveite!",
        "inserted_at":"26.9",
        "updated_at":"9.9",
        "banners":[
          {
            "id": 12313,
            "title": "Título do Banner",
            "image_url": "banner_de_roupas_da_animale.jpg?63641184930",
            "link_url":"https://www.oqvestir.com.br/qualquercoisa",
            "description":"Descrição do banner",
            "active":1,
            "activation_date":"2016-05-25 03:00:00",
            "expiration_date":"2021-01-01 00:00:00",
            "source_kind":"app_iphone",
            "page_position":"posicao_na_pagina",
            "inserted_at":"2016-05-25 03:00:00",
            "updated_at":"2016-05-25 03:00:00",
            "site_page_id": 2,
            "ga_event":"evento_GA",
            "ga_ctr":"GA CTR",
            "page_position":"posicao_na_pagina",
            "short_description":"descriçãozinha"
          },
          {
            "id": 1313,
            "title": "Título do Banner",
            "image_url": "o_arquivo.jpg?63641184930",
            "link_url":"https://www.oqvestir.com.br/qualquercoisa",
            "description":"Descrição do banner",
            "active":0,
            "activation_date":"2016-05-25 03:00:00",
            "expiration_date":"2021-01-01 00:00:00",
            "source_kind":"desktop",
            "page_position":"posicao_na_pagina",
            "inserted_at":"2016-05-25 03:00:00",
            "updated_at":"2016-05-25 03:00:00"
            "updated_at":"2016-05-25 03:00:00",
            "site_page_id": 2,
            "ga_event":"evento_GA",
            "ga_ctr":"GA CTR",
            "page_position":"posicao_na_pagina",
            "short_description":"descriçãozinha"
          }
        ]
      }
    ]
  }
```

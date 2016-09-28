# API

`https://tekislauta.fi/api`

## Päätepisteet

* `GET /boards/:board/:page tai null` Palauttaa 10 lankaa per sivu. (Jos sivu on null, niin palautus on ensimmäinen sivu)
* `POST /boards` Luo uuden laudan.
* `GET /boards/:board/posts/:id` Palauttaa jonkin julkaisun.
* `POST /:board/posts` Lisää uuden vastauksen.

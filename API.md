# API

`https://tekislauta.fi/api`

## Päätepisteet

* `GET /:board/:page tai null` Palauttaa 10 lankaa per sivu. (Jos sivu on null, niin palautus on ensimmäinen sivu)
* `GET /:board/threads/:thread_id` Palauttaa langan.
* `POST /:board/threads/` Lisää uuden langan.
* `GET /:board/threads/:thread_id/posts/:post_id` Palauttaa kommentin.
* `POST /:board/threads/:thread_id/posts` Lisää uuden kommentin.
Сервер задаёт правила через заголовки `access-control-*`. Например: // TODO зачем?

- `Access-Control-Allow-Methods: GET, POST` — сервер принимает только `GET`- и `POST`-запросы. Если будет отправлен `PUT`- или `DELETE`-запрос, сервер не ответит, а браузер просто заблокирует отправку.

- `Access-Control-Allow-Headers: content-type, x-my-header` — если мы отправим кастомный заголовок (например, `x-my-other-header`), возникнет такая же ошибка, как и в предыдущем случае.

- `Access-Control-Allow-Credentials: true` — разрешает присылать cookies.
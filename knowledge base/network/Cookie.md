Куки (cookies) — небольшой фрагмент данных, отправленный веб-сервером и хранимый на компьютере пользователя. Веб-клиент всякий раз при попытке открыть страницу соответствующего сайта пересылает этот фрагмент данных веб-серверу в виде HTTP-запроса.

Куки — это просто заголовки, но браузеры договорились, как с ними работать, и обязательно это делают. Если браузер встречает в ответе заголовки `cookie` — он сохраняет их к себе в память. И, соответственно, если при запросе к домену браузер видит, что у него есть куки для этого домена, — он подставит их в запрос. В браузере из JavaScript можно получить значение куки через `document.cookie`, но только если кука не `httponly`.
  
Некоторые особенности куки:

- куки ставятся на конкретный домен,
- браузер должен хранить как минимум 4096 байт cookies,
- имена нечувствительны к регистру.
  
Сервер устанавливает клиенту куки в ответе на запрос через специальный заголовок `Set-Cookie: name=value`. Далее браузер должен отправлять серверу куку через заголовок `Cookie: name=value`.

## Где применяются

Где применяются куки:

- аутентификация пользователей,
- хранение настроек пользователей,
- сессия пользователя,
- сбор различной статистики,
- и многое другое.

# Security

Важные атрибуты — `secure` и `httponly`

## `httponly`

Атрибут `httponly` делает куки доступными только по HTTP-запросам. Доступ через JavaScript при этом к этим кукам запрещён — это очень важно. 

Кука может быть «паспортом» пользователя в приложении, потому желательно не допускать кражу таких данных либо делать так, чтобы кража была бесполезной.

Атрибут `httponly` усложняет задачу злоумышленникам. Да и в наше время куки очень редко нужны фронтенд-разработчикам — хватает других инструментов. Клиент не должен работать с куками.

## `secure`

Атрибут `secure` говорит браузеру, что куку можно установить только при защищённом HTTPS-соединении. Если запрос приходит от HTTP, то браузер просто не поставит данную куку.

# Lifetime

Cookie lifetime can be set with two way:
- use `Expires` parameter: `Set-Cookie: token=123abc; Expires=Tue, 01 Jan 2030 00:00:00 -0000`
- use `MAX_AGE` parameter:  `Set-Cookie: token=123abc; MAX_AGE=120

Different browsers use different ways to check the cookie's lifetime. So it's better use both of them to let the browser choose supported parameter.

# Scope

There is two parameters to handle cookie's scope: `domain` and `path`.

If you do not set `domain` then it will be equal to the server's host like `test.example.com`. But if you set to equals to `example.com` so the cookie can be used in subdomains like `test-1.example.com`.

If you do not set `path` then the cookie can be used in every endpoint of the supported domains. But if you set to something like `/api` the the cookie will only be used for the endpoints starting with `/api`. 

Example:
````
Set-Cookie: token=123abc; expires=Thu, 05 Aug 2021 18:45:00 -0000; max_age=120; domain=example.com; path=/api
````


https://learn.javascript.ru/script-async-defer
https://habr.com/ru/companies/avito/articles/710674/
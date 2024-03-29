## Что такое CRLF-инъекция?

При CRLF-инъекции злоумышленник вставляет символы возврата каретки и ввода строки (`\r, \n`) в пользовательский ввод, чтобы обмануть сервер, веб-приложение или пользователя, заставив его думать, что один объект завершился, а другой начался.


## CRLF-инъекции в логи

  
Представьте себе файл с логами в панели администратора с шаблоном выходного потока _IP — Время – Путь_, как показано ниже:

```
123.123.123.123 - 08:15 - /index.php?page=home
```

Если злоумышленник может сделать инъекцию CRLF-символов в HTTP-запрос, он может изменить выходной поток и фальсифицировать логи. Он может изменить ответ веб-приложения на что-нибудь подобное:

```
/index.php?page=home&%0d%0a127.0.0.1 - 08:15 - /index.php?page=home&restrictedaction=edit
```

Здесь %0d и %0a – закодированные URL символы CR и LF. Таким образом после того, как злоумышленник вставит эти символы, а приложение выведет их, логи будут выглядеть следующим образом:

```
123.123.123.123 - 08:15 - /index.php?page=home&
127.0.0.1 - 08:15 - /index.php?page=home&restrictedaction=edit
```

Таким образом, используя CRLF-инъекции, злоумышленник может подделать записи в логах, чтобы замести следы. Злоумышленник буквально делает hijacking страницы и изменяет ответ. Например, представим сценарий, в котором у злоумышленника есть пароль администратора и выполняется параметр _restrictedaction_, который может использовать только администратор.

Проблема заключается в том, что если администратор заметит, что неизвестный IP использует параметр _restrictedaction_, то поймет, что что-то не так. Однако пока это выглядит так, будто команда была выдана localhost (и, потому, вероятно, кем-то, кто имеет доступ к серверу, например, администратором), это не будет выглядеть подозрительно.

Часть запроса, начинающаяся с %0d%0a будет обработана сервером как один параметр. После этого появится еще один & с параметром _restrictedaction_, который будет воспринят сервером, как еще один параметр. По сути, это будет тот же самый запрос, что и:

```
/index.php?page=home&restrictedaction=edit
```


## HTTP Response Splitting

Поскольку заголовок HTTP-ответа и его тело разделены символами CRLF, злоумышленник может попытаться внедрить их. Комбинация CRLFCRLF скажет браузеру, что заголовок заканчивается и начинается тело. Значит теперь он может записывать данные в тело ответа туда, где лежит HTML-код. Это может привести к уязвимости межсайтового скриптинга.

##### Пример HTTP Response Splitting, приводящего к XSS

Представьте, что приложение устанавливает собственный заголовок, например:

```
X-Your-Name: Bob
```

Значение заголовка задается с помощью GET-параметра «name». Если нет кодировки URL-адреса и значение просто содержится в заголовке, то злоумышленник может вставить вышеупомянутую комбинацию CRLFCRLF, чтобы сообщить браузеру о начале тела запроса. Так он может вставить данные, например, полезную нагрузку XSS:

```
?name=Bob%0d%0a%0d%0a<script>alert(document.domain)</script>
```


## HTTP Header Splitting


##### Пример инъекции в HTTP-заголовок для извлечения конфиденциальных данных

Отправим запрос:

```
GET /path?redirect=home%0D%0ASet-Cookie:%20login%3Dadmin HTTP/1.1 
```

Зная, что весь путь будет подставлен в `Location`, подставим свои заголовки, которые считаем нужными. На выходе получим запрос:

```
HTTP/1.1 302\r\n
Location: /home\r\n
Set-Cookie: login=admin\r\n
```

#####  Как предотвратить CRLF/HTTP-инъекции заголовков в веб-приложениях

- Лучший метод предотвращения – это не использовать ввод данных пользователем непосредственно в заголовок ответа. 
- Если это невозможно, вы всегда должны использовать функцию для кодирования специальных символов CRLF. 
- Еще одна хорошая практика безопасности – это обновление языка программирования до версии, которая не позволяет делать инъекции CR и LF внутри функций, которые устанавливают HTTP-заголовки.


https://habr.com/ru/companies/otus/articles/512226/
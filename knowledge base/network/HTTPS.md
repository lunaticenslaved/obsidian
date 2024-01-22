# Что это такое

SSL (Secure Socket Layer) — протокол шифрования данных, которыми обмениваются клиент и сервер, — стал наиболее распространённым методом защиты в Интернете.

Цифровой сертификат — файл, который уникальным образом идентифицирует серверы. Обычно цифровой сертификат **подписывается и заверяется специализированными центрами**. Их называют **центрами сертификации** или удостоверяющими центрами.

По сути, **SSL-сертификат — цифровая подпись вашего сайта, подтверждающая его подлинность**. Использование сертификата позволяет защитить как владельца сайта, так и его клиентов. **SSL-сертификат даёт возможность владельцу применить к своему сайту технологию SSL-шифрования**.

Таким образом, назначение SSL-сертификата — обеспечить безопасное соединение между сервером и браузером пользователя, надёжно защитить данные от перехвата и подмены. 

**Сертификат используется для шифрования данных и идентификации сайта при установлении защищённого соединения HTTPS.**

Информация передаётся в зашифрованном виде, и **расшифровать её можно только с помощью специального ключа, являющегося частью сертификата**. Тем самым гарантируется сохранность данных.

# Как работает HTTPS

![[Pasted image 20231203114626.png]]

1. Пользователь заходит на защищённый сайт;
2. Выполняется проверка DNS и определение IP-адреса хоста веб-сайта;
3. Запись веб-сайта найдена, переход на веб-сервер хоста;
4. Запрос безопасного SSL-соединения с хоста веб-сайта;
5. Хост отвечает валидным SSL-сертификатом;
6. Устанавливается защищённое соединение, передаваемые данные шифруются.
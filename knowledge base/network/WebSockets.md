Протокол WebSocket («веб-сокет»), описанный в спецификации RFC 6455, обеспечивает возможность обмена данными между браузером и сервером через постоянное соединение.

Данные передаются в обоих направлениях в виде «пакетов», без разрыва соединения и дополнительных HTTP-запросов.

#### Основные преимущества веб-сокетов:

- возможность отправки с сервера на клиент,
- нет оверхэда на открытие соединения, так как сообщения проходят через одно TCP-соединение,
- хорошая поддержка браузерами,
- очень простой API.

#### WebSockets часто используют для реализации:

- онлайн (real-time) игр,
- чатов и веб-мессенджеров,
- push-уведомлений и других уведомлений от сервера.
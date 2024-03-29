Можно сказать, что технология RPC (Remote Procedure Call) — одна из основоположников всего общения между удалёнными процессами.

**Основная идея RPC в том, что клиент и сервер имеют договорённость о транспортном протоколе, формате сообщений и способе сериализации передаваемых данных и с помощью этого общаются.**

Поверх RPC существует много других протоколов, два из которых — JSON-RPC и gRPC

Любой RPC, в отличие от REST, не ограничивает вас в терминологии и не стесняет рамками — вы вольны придумывать модели и действия с ними так, как вам удобно.

## JSON-RPC

Этот протокол стандартизировал только формат сообщений между клиентом и сервером, коды ответов HTTP и больше ничего. Лаконично, удобно, гибко.

## gRPC

Это фреймворк, который помогает агрегировать весь бэкенд в общий способ описания методов и ответов. Иногда в проектах используют микросервисную архитектуру или просто зоопарк технологий, но gRPC всё это агрегирует

Для архитекторов, фронтенд-разработчиков или техлидов всё будет выглядеть одинаково — есть API для работы с сервисом. Этот сервис в свою очередь может дробиться на подсервисы, то есть микросервисы. Каждый будет описан специальной структурой в proto-файлах.

Он поможет удобно спроектировать систему и раскидать методы на микросервисы. Этот инструмент хорошо подходит для написания микросервисной архитектуры.
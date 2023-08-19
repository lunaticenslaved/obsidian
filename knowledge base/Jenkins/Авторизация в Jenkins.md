Настраивается через раздел Manage Jenkins / Security. Новые пользователи создаются через Manage Jenkins / Users.

## [](https://github.com/lunaticenslaved/studying/blob/main/jenkins/authentication.md#%D0%BE%D1%82%D0%BB%D0%B8%D1%87%D0%B8%D1%8F-%D0%B0%D0%B2%D1%82%D0%BE%D1%80%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D0%B8-%D0%B8-%D0%B0%D1%83%D1%82%D0%B5%D0%BD%D1%82%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D0%B8)Отличия авторизации и аутентификации

- Аутентификация - процесс проверки пользователя. Отвечает на вопрос - как проверять?
- Авторизация - процесс распознания прав для пользователя. Отвечает на вопрос - какие права выдавать?

## [](https://github.com/lunaticenslaved/studying/blob/main/jenkins/authentication.md#%D0%B0%D1%83%D1%82%D0%B5%D0%BD%D1%82%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D1%8F)Аутентификация

Есть несколько типов аутентификации:

- Jenkins OWN database - БД, которая хранится в Jenkins
- LDAP - ? TODO: learn more
- Unix User / Group Database - аутентификация через пользователей на мастер машине

## [](https://github.com/lunaticenslaved/studying/blob/main/jenkins/authentication.md#%D0%B0%D0%B2%D1%82%D0%BE%D1%80%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F)Авторизация

Есть несколько типов авторизации:

- anyone can do anything
- legacy mode - ? TODO: learn more
- logged-in user can do anything
- matrix-based security - создаются группы пользователей и для групп настраиваются права. Подходит если один проект и много пользователей.
- project-based matrix authorization strategy TODO: learn more

### [](https://github.com/lunaticenslaved/studying/blob/main/jenkins/authentication.md#role-based-authorization-strategy)Role-based authorization strategy

Можно реализовать role-based authorization strategy через одноименный плагин.

Тогда каждой группе пользователей будут выдаваться права только на определенную папку. Это подходит, если много проектов крутится на одном Jenkins и нужно направить людей не только по типам пользователя внутри проекта, но и по проекту.

После установки плагина нужно изменить тип авторизации на Role-Based Strategy и настраивать права пользователей через Manage Jenkins / Manage And Assign Roles.

Можно создавать роли на айтемы (папки пайплайны и т.д.). Там будет задаваться поле паттерн, по которому Jenkins будет понимать, что в папку с таким названием пользователь может получить доступ.

Можно так же настраивать права доступа к агентам.
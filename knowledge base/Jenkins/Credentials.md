Типы:

- Username with password - сдандартно
- GitHub App - // TODO
- SSH Username with private key
- Secret file - можно загрузить файл и использовать его в пайплайне
- Secret text - // TODO
- Certificate - можно загрузить файл сертификата и использовать

Область видимости:

- Global - для всех креденшлы, что используются в пайплайне, рекомендуется использовать глобал
- System - для подключения нод

ID для ключам должно быть осмыслено. Лучше создавать их по определенной схеме: projectId-env-destination (myProject-dev-sonar)

Все credentials записаны в файле jenkins_home/credentials.xml. Данные хранятся в зашифрованном виде, однако их можно расшифровать через секретный интерфейс http//:jenkins.ru/script, через который можно выполнять groovy скрипты:

```
println(hudson.util.Secret.decrypt("wow"));
```
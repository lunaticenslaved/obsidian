`agent` - лейблы, определяющие более спицифичного слэйва

`stages` - описывается стадии

`steps` - описывает шаги стадии

`sh` - шаг, который выполняет переданную `shell`-команду. Например, `sh 'make publish'`

`junit` - ещё один этап шага (как `sh`), который собирает репорты тестов

Jenkinsfile (Declarative Pipeline):

```
pipeline { 
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') { 
            steps { 
                sh 'make' 
            }
        }
        stage('Test'){
            steps {
                sh 'make check'
                junit 'reports/**/*.xml' 
            }
        }
        stage('Deploy') {
            steps {
                sh 'make publish'
            }
        }
    }
}
```

Описать пайплайн можно через:

- Blue Ocean
- the classic UI
- in SCM с `Jenkinsfile` (предпочтительно)

Можно выполнять какие-то шаги параллельно на линуксе или на винде. Например, запускать тесты на двух ОС одновременоо.
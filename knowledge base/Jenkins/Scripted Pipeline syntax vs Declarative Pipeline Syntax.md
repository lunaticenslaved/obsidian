Оба способа описания пайплайна - это `DSL (Domain Specific Language)`

Одну и ту же работу можно описать через эти два вида синтакса.

Совет для начала: начать с декларативного синтакса. Если начнутся какие-то проблемы, то использовать `shared libraries`. И только когда и через shared `libs` не получиться решить все проблемы, то использовать `scripted syntax`.

## [](https://github.com/lunaticenslaved/studying/blob/main/jenkins/pipeline-syntax.md#declarative-pipeline-syntax)Declarative Pipeline Syntax

Записывается как:

```
pipeline { stages { stage('Build') {} }  }
```

## [](https://github.com/lunaticenslaved/studying/blob/main/jenkins/pipeline-syntax.md#scripted-pipeline-syntax)Scripted Pipeline Syntax

Записывается как описано ниже. Частично использует `Groovy Syntax` (Язык `Groovy`).

```
{ stage('Build') {}  }
```
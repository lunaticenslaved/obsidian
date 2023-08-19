
![](https://lh5.googleusercontent.com/2T5dZBs5cG7omLmTEWzE24KaD4bZCT5ZsGVWUt3Yk7eohm56DFrAm9frVISGG53ylz9UDTS87KJlORe2huSaJq-Iyvfa2yCPPkYFG17sKzRG-AzQ_QURQh3Wbbaxgxj3_CIV0DurrJSw1f-8OZjYZgk)


#### Добавление пользователя

```
git config --global user.name "Stas Basov"
git config --global user.email stasbasov@yandex.ru
```


#### Создание локального репозитория

```
git init
```


#### Проверить статус репозитория

```
git status
```


#### Добавить изменения в репозитории

```
git add -A - все файлы
```


#### Зафиксировать изменения

```
git commit -m "мой первый коммит"
```


#### Посмотреть историю коммитов

```
git log
```


#### Посмотреть разницу двух коммитов

```
git diff <hash1> <hash2>
```


#### Посмотреть список веток

```
git branch
```


#### Создать новую ветку

```
git branch <branch_name>
```


#### Создать ветку из удаленной

```
git branch <new_branch_name> <remote_name>/<remote_branch_name>
```


#### Переключиться на ветку

```
git checkout <branch_name>
```


#### Слить код из ветки в другой веткой (Merge)

```
git checkout master # переходим в основную ветку
git merge testing # переносим код из ветки testing в основную
```


#### Залить изменения на удаленный репозиторий

```
git push -u origin master
```

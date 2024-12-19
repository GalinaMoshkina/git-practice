# Лабораторная работа 5
## Задание 1 - Автоматизация проверки формата файлов при коммите

Предположим, у вас есть задача автоматизировать проверку формата файлов при коммите с использованием Git Hooks.

  Перед каждым коммитом необходимо автоматически проверять, чтобы все .txt файлы в репозитории соответствовали определенному формату.

  Создайте bash-скрипт, который будет выполнять проверку того, что коммитится файл формата .txt и в файле присутствует какой-то текст (например, в конце файла есть подпись автора, неважно как она выглядит, главное чтобы была какая-нибудь проверка содержимого файла). Далее поместите этот скрипт в нужную папку и проверьте, что перед каждым коммитом проходит проверка, например, добавьте вывод о результате проверки в консоль. За этот функционал отвечает Git Hooks, там сказазно как автоматизировать такую проверку.

### Решение 
1. Создаем репозиторий с помощью `git clone <url репозитория>` 
2.  Переходим в папку репозитория с помощью `cd lab5`
3.  Проверяем наличие папки `.git/hooks/ с помощью команды ls -la .git/hooks/ ![image](https://github.com/user-attachments/assets/82323e88-19ba-4936-9317-49d57e5c31a7) 

4.  Заходим в папку `.git/hooks/` с помощью `cd` и создаем файл `pre-commit`.
5.  Вписываем туда код: ![Снимок экрана от 2024-12-18 20-48-02](https://github.com/user-attachments/assets/4075d760-681a-47db-88e8-a6c479052cdd) 
6. Сделаем файл исполняемым с помощью команды `chmod +x pre-commit`

7.  Создаем файл в /home/user/lab5 22example.txt (без автора) с помощью команды `touch`, с помощью команды `gedit` изменяем файл. 

![image](https://github.com/user-attachments/assets/6432f7ce-81ce-4afc-9651-80ce0886693a) 
8. Попробуем сделать коммит и отправить в репозиторий файл 22example.txt 
```
git add task_1_1.txt
git commit -m "Добавлен корректный текстовый файл"
git push origin main
```
На скриншоте вместо "Добавлен корректный текстовый файл" будет "любой" 
![image](https://github.com/user-attachments/assets/f8cbe4f7-5f07-4adb-8885-964e36128378)



## Задание 2 - Использование Git Flow в проекте
 
Предположим, у вас есть задача на создание новой функциональности для вашего проекта с использованием Git Flow. Давайте рассмотрим конкретный пример. В примере важен не сам проект и его код (его тут вообще как такового нет), а принцип работы Git Flow.

### Решение 
1. Устанавливаем git-flow: 

```
sudo apt-get install git-flow
```

2. В корне репозитория выполняем инициализацию Git Flow.

```
git flow init
```

3. Создаем ветку для новой функциональности, которая называется "task-management":

```
git flow feature start task-management
```

4. Внесите изменения в код для добавления функционала управления задачами (например, в файл task_manager.py): ![image](https://github.com/user-attachments/assets/e9899b27-6706-4fee-8ee4-12ab2d847fa6) 


```
def create_task(title, description):
    # Логика создания задачи
    print(f"Создана новая задача: {title}")
```

Выполняем коммит изменения по мере разработки: ![image](https://github.com/user-attachments/assets/f301b80e-7c52-45ef-97ac-d8f48bc7ba7a) 


```
git add task_manager.py
git commit -m "Добавлен функционал управления задачами"


```

5. После завершения разработки функции завершаем фичу и объединяем ее с основной веткой: ![image](https://github.com/user-attachments/assets/b18799a2-4aff-43c7-b62a-4fdb0dd48da3) 


```
git flow feature finish task-management

```

Git Flow автоматически переключится на ветку develop и выполнит слияние. Если есть конфликты, их нужно разрешить.

6. Переключаемся на ветку "develop" и начинаем создание релиза: ![image](https://github.com/user-attachments/assets/8693fb63-4cef-4f74-98da-60c1e2f71d37) 


```
git checkout develop
git flow release start v1.0.0
```

7. Внесите изменения, связанные с релизом (например, обновите версию в файле version.txt):

```
echo "v1.0.0" > version.txt
git add version.txt
git commit -m "Обновлена версия для релиза v1.0.0"

```

8. Завершите релиз и объедините его с ветками "develop" и "main": ![image](https://github.com/user-attachments/assets/8abd8c7c-ce43-4d95-98f3-c182e9616acc) 


```
git flow release finish v1.0.0
```

9. Если в процессе использования выявлена критическая ошибка, создайте hotfix (у нас конечно же ошибки никакой не возникнет, но hotfix все равно создаем): ![image](https://github.com/user-attachments/assets/8b2c42b8-b983-443c-b9f8-a53a6e11f17f) 


```
git flow hotfix start hotfix-1.0.1
```

10. Внесите изменения для исправления ошибки и коммитите: ![image](https://github.com/user-attachments/assets/3f367967-cd35-4300-b738-0e3ba82df333) 


```
# Исправление ошибки
git add file_with_error.py
git commit -m "Исправлена критическая ошибка"
```

11. Завершите hotfix и объедините его с ветками "develop" и "main": ![image](https://github.com/user-attachments/assets/2a053ce7-3f46-4780-b6bf-6bd2d7412562) 


```
git flow hotfix finish hotfix-1.0.1
```

12. Завершение работы и отправка изменений на удаленный репозиторий. Отправьте изменения на удаленный репозиторий: ![image](https://github.com/user-attachments/assets/5a625646-ec16-4ec9-9203-34fc3bff60cf) 


```
git push origin develop
git push origin main

```
### Как успешно сдать работу?

Создать свой репозиторий из шаблона этого. Как это делается - "Use this template" -> "Create a new repository" и сделайте его public. 

Находясь уже в своем репозитории - создайте новый файл формата .md и там оформляйте отчет. В отчете опишите все шаги которые вы делали, чтобы получить финальный результат работы.

Что вам нужно знать, чтобы успешно защитить работу:

Основные команды Git, как возникают и как решать конфликты, Git Hooks, Git Flow. 

## Ресурсы

1. [Git Documentation](https://git-scm.com/doc)
2. [Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials)
3. [Pro Git Book](https://git-scm.com/book/en/v2)
4. [Markdown Guidelines](https://docs.github.com/ru/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

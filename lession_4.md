# Домашнее задание к занятию 10 «Jenkins»

## Подготовка к выполнению

1. Создать два VM: для jenkins-master и jenkins-agent.
2. Установить Jenkins при помощи playbook.
3. Запустить и проверить работоспособность.
4. Сделать первоначальную настройку.

  ![screen](https://github.com/MaximovAA/school/blob/main/9.1install.jpg)  
  ![screen](https://github.com/MaximovAA/school/blob/main/9.1start.jpg)  
  
  ![screen](https://github.com/MaximovAA/school/blob/main/9.1agent.jpg)  
  ![screen](https://github.com/MaximovAA/school/blob/main/9.1agent2.jpg)
## Основная часть

1. Сделать Freestyle Job, который будет запускать `molecule test` из любого вашего репозитория с ролью.
2. Сделать Declarative Pipeline Job, который будет запускать `molecule test` из любого вашего репозитория с ролью.
3. Перенести Declarative Pipeline в репозиторий в файл `Jenkinsfile`.
4. Создать Multibranch Pipeline на запуск `Jenkinsfile` из репозитория.
5. Создать Scripted Pipeline, наполнить его скриптом из [pipeline](./pipeline).
6. Внести необходимые изменения, чтобы Pipeline запускал `ansible-playbook` без флагов `--check --diff`, если не установлен параметр при запуске джобы (prod_run = True). По умолчанию параметр имеет значение False и запускает прогон с флагами `--check --diff`.
7. Проверить работоспособность, исправить ошибки, исправленный Pipeline вложить в репозиторий в файл `ScriptedJenkinsfile`.
8. Отправить ссылку на репозиторий с ролью и Declarative Pipeline и Scripted Pipeline.
9. Сопроводите процесс настройки скриншотами для каждого пункта задания!!
    [Jenkinsfile](https://github.com/MaximovAA/school/blob/main/Jenkinsfile)
   [ScriptedJenkinsfile](https://github.com/MaximovAA/school/blob/main/ScriptedJenkinsfile)
```
Molecule test упорно не хочет выполняться на агенте, заменив его на любую команду баш или ансибл можно сделать все джобы "зелеными" но оставил как есть.

pipeline {
    agent {
        label 'ansible'
    }
    stages {
        stage (first) {
            steps {
                sh 'echo "molecule"'
            }
        }
        stage (second) {
            steps {
                sh "molecule test"
            }
        }
    }
}
```

  ![screen](https://github.com/MaximovAA/school/blob/main/9.1freestyle1.jpg)  
  ![screen](https://github.com/MaximovAA/school/blob/main/9.1freestyle2.jpg)  
  ![screen](https://github.com/MaximovAA/school/blob/main/9.1declarative.jpg)  
  ![screen](https://github.com/MaximovAA/school/blob/main/9.1DeclarativeSCM.jpg)  
  ![screen](https://github.com/MaximovAA/school/blob/main/9.1DeclarativeSCM2.jpg)  
  ![screen](https://github.com/MaximovAA/school/blob/main/9.1parametrs.jpg)  
  ![screen](https://github.com/MaximovAA/school/blob/main/9.1prode_run1.jpg)  
  ![screen](https://github.com/MaximovAA/school/blob/main/9.1ansible.jpg)  
  ![screen](https://github.com/MaximovAA/school/blob/main/9.1ansible2.jpg)
## Необязательная часть

1. Создать скрипт на groovy, который будет собирать все Job, завершившиеся хотя бы раз неуспешно. Добавить скрипт в репозиторий с решением и названием `AllJobFailure.groovy`.
2. Создать Scripted Pipeline так, чтобы он мог сначала запустить через Yandex Cloud CLI необходимое количество инстансов, прописать их в инвентори плейбука и после этого запускать плейбук. Мы должны при нажатии кнопки получить готовую к использованию систему.

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---

# Настройка репозитория

1. Создаем [основные ветки](../../rules/repository/RU.md) - `main` и `develop`.

2. Если ваш тарифный план GitHub или GitLab позволяет защищать ветки, и `main` и `develop` необходимо защитить. Включить защиту можно в настройках репозитория:

**GitHub:** `Settings` -> `Branches` -> `Branch protection rules`

**GitLab:** `Settings` -> `Repository` -> `Protected branches`

Здесь же необходимо включить условие, что Pull Request можно вмержить только после аппрува хотя бы одним членом команды.

> _Зачем это нужно?_ Мы защищаем критически важные ветки от неосторожных коммитов (например, по невнимательности), а также от случайных вмерживаний PR'ов.

3. Устанавливаем ветку `develop` в качестве дефолтной:

**GitHub:** `Settings` -> `Branches` -> `Default branch`

**GitLab:** `Settings` -> `Repository` -> `Default branch`

> _Зачем это нужно?_ Так мы будем уверены, что разработчик по невнимательности не ответвился от `main`.

4. Разрешаем CI:

**GitHub:** `Settings` -> `Actions` -> `Actions permissions`

**GitLab:** `Settings` -> `CI/CD` -> `General pipelines`

> _Зачем это нужно?_ В [следующем разделе](../project/RU.md) мы настроим автоматический запуск тестов при открытии нового PR.

5. Добавляем подробный README в соответствии с [правилами](../../rules/readme/RU.md).

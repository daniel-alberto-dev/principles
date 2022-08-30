# Настройка проекта

## 1. Инициализируем проект

1.1. В корне репозитория выполняем команду:

```sh
yarn init
```

> _Примечание._ В процессе инициализации не забываем установить флаг `private` в `true`, если репозиторий должен быть приватным. Это предотвратит случайную публикацию кода в `npm`.

1.2. В начало `/package.json` руками дописываем ссылку на [homepage](https://classic.yarnpkg.com/en/docs/package-json/#toc-homepage):

```json
"homepage": "https://your-site.com"
```

1.3. Также в конец `/package.json` дописываем информацию о [среде выполнения](https://classic.yarnpkg.com/en/docs/package-json/#toc-engines). В настоящий момент мы везде используем `node.js` 14 и `yarn` 1.22.

```json
"engines": {
  "node": "14.*",
  "yarn": "1.22.*"
}
```

1.4. Если проект по какой-то причине не предназначен для запуска из под Windows (например, это ios-приложение на `react-native`), добавляем в `/package.json` [ограничение по ОС](https://classic.yarnpkg.com/en/docs/package-json/#toc-os):

```json
"os": ["!win32"]
```

1.5. В корне репозитория создаем файл [.gitignore](https://git-scm.com/docs/gitignore) для игнорирования временных файлов. В него добавляем первое правило - директорию `node_modules`.

## 2. Настраиваем `prettier` на прекоммит-хук

> _Зачем это нужно?_ Мы считаем что [prettier](https://prettier.io/) - лучшее, что подарила разработчикам индустрия (не считая Internet Explorer, конечно 😉). Наш принцип - автоматизировать то, что можно автоматизировать, и `prettier` отлично с этим справляется, снимая с плеч разработчиков контроль за форматированием кода.

2.1. Устанавливаем зависимости:

```sh
yarn add --dev prettier husky pretty-quick
```

> **Важно.** Мы никогда не ставим зависимости глобально. _Почему:_ разные проекты могут требовать разные версии зависимостей, в этом случае их менеджмент превращается в хаос.

2.2. Инициализируем [husky](https://github.com/typicode/husky):

```sh
npx husky-init
yarn husky set .husky/pre-commit "npx pretty-quick --staged"
```

2.3. Защищаем хук от поломок, добавив в `package.json` реинициализацию husky при каждом обновлении зависимостей:

```diff
"scripts": {
-  "prepare": "husky install",
+  "postinstall": "husky install",
  ...
```

2.4. В `/package.json` добавляем команду для запуска `prettier` из `CI`:

```diff
"scripts": {
+  "prettier": "prettier --check .",
  "postinstall": "husky install",
  ...
```

> _Хозяйке на заметку._ Теперь мы также можем простой командой локально проверять форматирование (`yarn run prettier`) или даже автоматически исправлять проблемы в коде (`yarn run prettier -w`).

2.5. В корень репозитория добавляем конфиг `prettier` - файл `.prettierrc`:

```json
{
  "trailingComma": "es5",
  "singleQuote": true
}
```

2.6. Рядом кладем файл `.prettierignore` - в него со временем будем добавлять директории и файлы, которые не требуется форматировать (например, продакшн-бандлы).

## 3. Настраиваем редактор

Кладем файл [settings.json](../../.vscode/settings.json) в директорию `/.vscode`.

## 4. Настраиваем запуск `prettier` при открытии PR

4.1. **GitHub**: Кладем файл [validate_code.yml](./yml/validate_code.yml) в директорию `/.github/workflows`.

4.2. **GitLab**: Кладем файл [.gitlab-ci.yml](./yml/.gitlab-ci.yml) в корень репозитория.

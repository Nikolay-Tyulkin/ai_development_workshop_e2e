# Урок 1. Настройка агентной среды разработки в opencode

![Готовимся к агентной разработке](https://media.tenor.com/_aPzXVrVveIAAAAd/%D0%B0%D1%80%D0%BD%D0%BE%D0%BB%D1%8C%D0%B4-%D1%88%D0%B2%D0%B0%D1%80%D1%86%D0%B5%D0%BD%D0%B5%D0%B3%D0%B3%D0%B5%D1%80.gif)

## Назначение урока

На первом этапе мы еще не пишем приложение. Сначала собираем рабочую среду для агентной разработки: правила, агенты, навыки и конфигурацию opencode, чтобы дальше агент не импровизировал, а работал в понятных границах.

В этом уроке мы настраиваем opencode строго по его документации:

- проектные правила: `AGENTS.md` в корне проекта;
- проектная конфигурация: `opencode.json` в корне проекта;
- агенты: `.opencode/agents/<name>.md`;
- навыки: `.opencode/skills/<name>/SKILL.md`;
- описание внешних инструментов: `TOOLS.md`.

В `ASSETS` лежит готовый набор файлов. Его можно целиком скопировать в новый проект и сразу открыть проект в opencode.

## Результат урока

К концу урока в рабочем проекте должна появиться такая структура:

```text
project-root/
  AGENTS.md
  TOOLS.md
  opencode.json
  .opencode/
    agents/
      product-analyst.md
      architect.md
      frontend-engineer.md
      backend-engineer.md
      ai-integration-engineer.md
      qa-engineer.md
      devops-engineer.md
      technical-writer.md
    skills/
      product-spec/
        SKILL.md
      implementation-plan/
        SKILL.md
      quality-gate/
        SKILL.md
```

Дополнительно в `ASSETS` оставлен `SKILLS.md` как человекочитаемый индекс навыков. Работает в opencode не сам `SKILLS.md`, а файлы `SKILL.md` внутри `.opencode/skills/<name>/`.


## Шаг 1. Создать рабочий проект

Создайте пустую папку будущего проекта или откройте уже существующий проект, где дальше будет жить `TaskerAI`.

```powershell
mkdir TaskerAI
cd TaskerAI
git init
```

Linux/macOS:

```bash
mkdir TaskerAI
cd TaskerAI
git init
```

На этом этапе специально не создаем `frontend`, `backend`, базу данных, Docker-файлы и тесты. Первый урок нужен только для агентной среды.

## Шаг 2. Скопировать ASSETS целиком

Скопируйте все содержимое папки `Course/01-agent-environment/ASSETS` в корень рабочего проекта.

Пример для PowerShell из корня курса:

```powershell
Copy-Item -Recurse -Force .\Course\01-agent-environment\ASSETS\* .\TaskerAI\
```

Пример для Linux/macOS из корня курса:

```bash
cp -R ./Course/01-agent-environment/ASSETS/. ./TaskerAI/
```

После копирования в проекте должны появиться:

```text
AGENTS.md
TOOLS.md
SKILLS.md
opencode.json
.opencode/agents/*.md
.opencode/skills/*/SKILL.md
```

`SKILLS.md` можно оставить в проекте как справочный индекс. Он не заменяет официальную структуру skills и не должен использоваться вместо `.opencode/skills/<name>/SKILL.md`.

## Шаг 3. Проверить `AGENTS.md`

`AGENTS.md` - это правила игры для opencode. Файл лежит в корне проекта и объясняет агенту:

- контекст курса и продукта;
- ограничения перед началом разработки;
- правила работы с изменениями пользователя;
- требования к frontend, backend, AI-интеграции, тестам, Docker и документации;
- формат финального отчета агента.

Самые важные правила:
- агент не начинает реализацию без технического задания;
- агент не создает крупную структуру проекта без согласованного плана;
- агент не удаляет файлы и не откатывает чужие изменения без явного разрешения;
- секреты не хранятся в коде;
- после изменений агент сообщает, что изменено и какие проверки выполнены.

## Шаг 4. Проверить `opencode.json`

`opencode.json` - проектная конфигурация opencode. Она должна быть в корне проекта и содержать схему:

```json
{
  "$schema": "https://opencode.ai/config.json"
}
```

В готовом наборе `ASSETS` конфигурация делает три вещи:

- подключает `AGENTS.md`, `TOOLS.md` и `SKILLS.md` как проектные инструкции через `instructions`;
- задает безопасные разрешения для `edit`, `bash` и `webfetch`;
- оставляет `build` основным агентом по умолчанию, а специализированных агентов хранит отдельными Markdown-файлами в `.opencode/agents`.

Если вы изменили `opencode.json`, перезапустите opencode. Конфигурация загружается при старте сессии и не обязана применяться к уже открытому сеансу.

## Шаг 5. Проверить Agents

По документации opencode проектные агенты размещаются в `.opencode/agents/`. Каждый агент - это Markdown-файл с YAML-заголовком.

Пример формы агента:

```markdown
---
description: Prepares product requirements and acceptance criteria for the course project.
mode: subagent
permission:
  edit: deny
  bash: deny
---

You are a product analyst for this project.
```

Имя файла становится именем агента. Например, `.opencode/agents/product-analyst.md` создает агента `product-analyst`.

В готовом наборе есть агенты:

- `product-analyst` - требования, MVP, пользовательские сценарии;
- `architect` - архитектура и план реализации;
- `frontend-engineer` - React, TypeScript, UI-состояния и адаптивность;
- `backend-engineer` - FastAPI, API, модели данных и ошибки;
- `ai-integration-engineer` - AI API, промпты, мокирование и секреты;
- `qa-engineer` - тест-план, unit/API/E2E-проверки;
- `devops-engineer` - Docker, Compose и окружение;
- `technical-writer` - README, changelog и документация.

Субагента можно вызвать вручную через `@`:

```text
@architect подготовь план реализации MVP. Код пока не создавай.
```

Основные агенты opencode `build` и `plan` остаются встроенными. Используйте `plan` для анализа и планирования без изменений, `build` - когда нужно реально менять файлы.

## Шаг 6. Проверить Skills

По документации opencode skill - это не один общий `SKILLS.md`. Каждый навык должен лежать в отдельной папке:

```text
.opencode/skills/<skill-name>/SKILL.md
```

Каждый `SKILL.md` должен начинаться с YAML-заголовка. Обязательные поля:

- `name`;
- `description`.

Имя навыка должно совпадать с именем папки, быть в нижнем регистре и использовать дефисы.

Пример формы навыка:

```markdown
---
name: product-spec
description: Use when preparing or refining the product specification, MVP scope, user scenarios, and acceptance criteria.
---

## What to do

Write the product specification before implementation starts.
```

В готовом наборе есть навыки:

- `product-spec` - подготовка технического задания и критериев приемки;
- `implementation-plan` - декомпозиция работ перед разработкой;
- `quality-gate` - проверка результата перед завершением задачи.

opencode показывает доступные навыки агенту через инструмент `skill`. Агент загружает навык только когда он нужен по описанию.

## Шаг 7. Проверить инструменты

opencode умеет работать с файлами, искать по проекту и запускать команды через терминал. Но сами системные команды не появляются магически: Git, Node.js, Python и Docker должны быть установлены отдельно.

Проверьте инструменты:

```powershell
git --version
node --version
npm --version
python --version
docker --version
docker compose version
```

Linux/macOS:

```bash
git --version
node --version
npm --version
python3 --version
docker --version
docker compose version
```

Минимум для перехода ко второму уроку:

- opencode установлен и открывает проект;
- Git установлен;
- Node.js и npm установлены;
- Python установлен;
- понятно, доступен ли Docker сейчас или его установка отложена до Docker-этапа.

Playwright обычно устанавливается позже внутри frontend-проекта, а не на первом уроке.

## Шаг 8. Запустить opencode в проекте

Откройте рабочий проект и запустите opencode:

```powershell
opencode web
```

Linux/macOS:

```bash
opencode web
```

После изменения `opencode.json`, `.opencode/agents/*` или `.opencode/skills/*/SKILL.md` перезапустите opencode, чтобы новая конфигурация точно загрузилась.

## Шаг 9. Проверить агентную среду промптами

Проверка правил:

```text
Прочитай AGENTS.md, TOOLS.md и SKILLS.md. Ничего не меняй. Кратко объясни:
1. какую роль ты выполняешь в этом проекте;
2. какие действия тебе запрещены без разрешения;
3. какие проверки ты должен выполнять после изменений;
4. как ты должен сообщать результат работы;
5. какие инструменты доступны через opencode, а какие должны быть установлены отдельно.
```

Проверка агента планирования:

```text
@architect подготовь план вопросов для технического задания приложения TaskerAI. Не создавай код и не создавай структуру приложения.
```

Проверка навыка ТЗ:

```text
Подготовь структуру технического задания для приложения TaskerAI. Если нужен навык product-spec, используй его. Код пока не создавай.
```

Проверка quality gate:

```text
Опиши, как ты будешь проверять готовность будущей функции перед финальным ответом. Если нужен навык quality-gate, используй его. Ничего не меняй.
```

## Критерии готовности урока

Урок можно считать закрытым, если на все пункты ниже получается ответить "да":

- в проекте есть `AGENTS.md`;
- в проекте есть `opencode.json` со схемой `https://opencode.ai/config.json`;
- агенты лежат в `.opencode/agents/*.md`;
- навыки лежат в `.opencode/skills/<name>/SKILL.md`;
- каждый `SKILL.md` содержит `name` и `description`;
- правила запрещают старт разработки без ТЗ;
- правила запрещают удалять файлы и откатывать чужие изменения без разрешения;
- понятно, какие инструменты установлены, а какие будут добавлены позже;
- opencode запускается в проекте после копирования файлов.

## Итог урока

После первого урока у нас есть готовая агентная среда opencode: проектные правила, безопасная конфигурация, специализированные субагенты и переиспользуемые навыки. На следующем уроке эта среда будет использоваться для подготовки технического задания и плана реализации приложения.

## Следующий урок

Переходите к [уроку 2: техническое задание и план реализации](../02-specification-and-planning/README.md).

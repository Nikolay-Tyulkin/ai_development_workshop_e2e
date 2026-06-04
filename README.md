# Агентная End2End-разработка приложения с ИИ

Короткий практический воркшоп по разработке учебного веб-приложения с помощью ИИ-агента в opencode. Участники проходят полный цикл: настройка агентной среды, подготовка требований, реализация MVP, тестирование, Docker-запуск и оформление проекта.

## Что должно получиться

К концу курса должен быть готов учебный проект `task-manager-ai` - веб-приложение "Менеджер задач с ИИ".

В приложении должны быть:

- создание, редактирование и удаление задач;
- статусы задач и базовая фильтрация;
- ИИ-функции в мок-режиме или через внешний API;
- frontend и backend;
- базовые автотесты;
- E2E-проверки через Playwright;
- запуск через Docker Compose;
- README, changelog и рабочие инструкции для сопровождения проекта.

## Требования

Перед началом нужны базовые навыки работы с терминалом, Git и редактором кода. Также нужно установить инструменты:

- Git: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
- Node.js и npm: https://nodejs.org/en/download
- Python: https://www.python.org/downloads/
- Docker Desktop: https://docs.docker.com/desktop/
- opencode: https://opencode.ai/docs
- Playwright: https://playwright.dev/docs/intro

Playwright можно установить позже, на уроке тестирования и Docker. Docker нужен для финальной проверки запуска проекта в контейнерах.

## Материалы курса

Основные материалы лежат в папке `Course`:

| Урок | Тема | Результат |
| --- | --- | --- |
| [01](Course/01-agent-environment/README.md) | Настройка агентной среды | `AGENTS.md`, `TOOLS.md`, `opencode.json`, агенты и skills |
| [02](Course/02-specification-and-planning/README.md) | Требования и план | `PROJECT_SPEC.md`, `IMPLEMENTATION_PLAN.md`, `ACCEPTANCE_CRITERIA.md` |
| [03](Course/03-application-development/README.md) | Разработка MVP | Рабочий frontend/backend и базовые тесты |
| [04](Course/04-testing-and-docker/README.md) | Тестирование и Docker | Playwright, E2E-тесты, Docker Compose |

В каждом уроке есть пошаговая инструкция и папка `ASSETS` с примерами артефактов.

## Как проходить

1. Откройте урок `Course/01-agent-environment/README.md`.
2. Создайте рабочий проект `task-manager-ai`.
3. Следуйте урокам по порядку и переносите нужные файлы из `ASSETS`.
4. После каждого урока проверяйте, что получился указанный результат.

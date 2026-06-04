# Course

Материалы курса "Агентная End2End-разработка приложения TaskerAI".

## Структура

```text
Course/
  01-agent-environment/
  02-specification-and-planning/
  03-application-development/
  04-testing-and-docker/
  05-maintenance-versioning-docs/  # в разработке
```

Каждый модуль содержит сам урок в `README.md`. В первых модулях папка `ASSETS` содержит готовые примеры выходных артефактов; в практических модулях 3-4 все нужные шаги описаны прямо в README.

## Первый модуль

Первый модуль находится в папке `01-agent-environment` и посвящен настройке рабочих файлов агентной разработки: `AGENTS.md`, `SKILLS.md` и `TOOLS.md`.

## Второй модуль

Второй модуль находится в папке `02-specification-and-planning` и посвящен подготовке технического задания, плана реализации и критериев приемки для `TaskerAI`: `PROJECT_SPEC.md`, `IMPLEMENTATION_PLAN.md` и `ACCEPTANCE_CRITERIA.md`.

## Третий модуль

Третий модуль находится в папке `03-application-development` и посвящен пошаговой реализации MVP приложения по плану: backend API, frontend-интерфейс, локальное хранение данных, AI-функции в мок-режиме, базовые backend-автотесты и базовые frontend-автотесты без Playwright.

## Четвертый модуль

Четвертый модуль находится в папке `04-testing-and-docker` и посвящен установке Playwright, E2E-проверкам, расширению тестового покрытия и Docker-запуску приложения.

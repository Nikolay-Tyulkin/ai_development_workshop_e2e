# Course

Материалы курса "Агентная End2End-разработка приложения TaskerAI".

## Структура

```text
Course/
  01-agent-environment/
  02-specification-and-planning/
  03-application-development/
  04-testing-and-docker/
  05-maintenance-versioning-docs/
```

Каждый модуль содержит сам урок в `README.md`. Если в модуле есть папка `ASSETS`, она содержит готовые примеры выходных артефактов или настроек, которые можно использовать как шаблон.

## Первый модуль

Первый модуль находится в папке `01-agent-environment` и посвящен настройке рабочих файлов агентной разработки: `AGENTS.md`, `SKILLS.md`, `opencode.json`, agents и skills.

## Второй модуль

Второй модуль находится в папке `02-specification-and-planning` и посвящен подготовке технического задания, плана реализации и критериев приемки для `TaskerAI`: `PROJECT_SPEC.md`, `IMPLEMENTATION_PLAN.md` и `ACCEPTANCE_CRITERIA.md`.

## Третий модуль

Третий модуль находится в папке `03-application-development` и посвящен пошаговой реализации MVP приложения по плану: backend API, frontend-интерфейс, локальное хранение данных, AI-функции в мок-режиме, базовые backend-автотесты и базовые frontend-автотесты без Playwright.

## Четвертый модуль

Четвертый модуль находится в папке `04-testing-and-docker` и посвящен установке Playwright, E2E-проверкам, расширению тестового покрытия и Docker-запуску приложения.

## Пятый модуль

Пятый модуль находится в папке `05-maintenance-versioning-docs` и посвящен сопровождению проекта после MVP: SemVer, changelog, feature branch, артефактам новой фичи, разработке канбан-доски и внесению изменений обратно в основную ветку.

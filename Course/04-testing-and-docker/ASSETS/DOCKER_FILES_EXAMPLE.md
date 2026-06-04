# DOCKER_FILES_EXAMPLE: урок 4

## 1. Назначение файла

Этот файл содержит пример Docker-настройки для учебного приложения `TaskerAI`. Используйте его как шаблон, а не как обязательный готовый код: фактические пути, команды и порты нужно сверить с реальным проектом.

Пример рассчитан на структуру:

```text
project-root/
  docker-compose.yml
  backend/
    Dockerfile
    requirements.txt
    app/
  frontend/
    Dockerfile
    package.json
    src/
```

## 2. Backend Dockerfile

Пример для FastAPI:

```dockerfile
FROM python:3.12-slim

WORKDIR /app

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY app ./app

EXPOSE 8000

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
```

Если в проекте `main.py` лежит не в `app/main.py`, команду `CMD` нужно изменить под фактический импорт.

## 3. Frontend Dockerfile

Пример для Vite + React:

```dockerfile
FROM node:22-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build

FROM nginx:1.27-alpine

COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

Если frontend должен проксировать API через nginx, добавьте отдельный `nginx.conf`. Для учебного MVP часто проще передавать публичный URL backend через переменную окружения на этапе сборки или использовать относительный `/api` при настроенном reverse proxy.

## 4. docker-compose.yml

Пример с backend и frontend:

```yaml
services:
  backend:
    build:
      context: ./backend
    environment:
      AI_MOCK_MODE: "true"
      DATABASE_URL: "sqlite:////data/app.db"
    volumes:
      - backend-data:/data
    ports:
      - "8000:8000"

  frontend:
    build:
      context: ./frontend
    depends_on:
      - backend
    ports:
      - "3000:80"

volumes:
  backend-data:
```

Если frontend обращается к backend из браузера, помните: браузер пользователя не видит Docker service name `backend`. Для браузера обычно нужен URL вроде `http://localhost:8000` или reverse proxy на том же домене.

## 5. .env.example

Пример безопасного `.env.example`:

```text
AI_MOCK_MODE=true
AI_API_KEY=
DATABASE_URL=sqlite:///./app.db
```

Правила:

- не добавлять реальные ключи;
- не коммитить `.env` с секретами;
- не передавать AI API key во frontend;
- для тестов использовать мок-режим.

## 6. Команды проверки

Сборка:

```powershell
docker compose build
```

Linux/macOS:

```bash
docker compose build
```

Запуск:

```powershell
docker compose up
```

Linux/macOS:

```bash
docker compose up
```

Остановка:

```powershell
docker compose down
```

Linux/macOS:

```bash
docker compose down
```

Остановка с удалением volume, если нужно очистить учебные данные:

```powershell
docker compose down -v
```

Linux/macOS:

```bash
docker compose down -v
```

## 7. Частые проблемы

- Frontend не видит backend: проверьте URL API в браузере и CORS-настройки backend.
- Backend в Docker не видит базу: проверьте `DATABASE_URL` и volume.
- Vite-переменные не применились: проверьте, на каком этапе они читаются, во время build или runtime.
- AI-тесты требуют ключ: включите мок-режим и проверьте, что тесты не читают реальный секрет.
- Docker build медленно повторяет установку зависимостей: проверьте порядок `COPY package*.json` и `COPY requirements.txt`.

## 8. Критерии готовности Docker-настройки

- `docker compose build` проходит без ошибок;
- `docker compose up` поднимает backend и frontend;
- frontend открывается в браузере;
- frontend может вызвать backend API;
- AI-функции работают в мок-режиме;
- данные не теряются неожиданно при перезапуске, если это требуется проектом;
- README содержит фактические команды запуска;
- секреты не попали в Dockerfile, compose и `.env.example`.

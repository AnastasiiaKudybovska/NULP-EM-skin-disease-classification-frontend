# Skin Insight AI — фронтенд

React-інтерфейс для класифікації зображень шкіри, перегляду XAI-пояснень та історії.

## Запуск усього PoC через Docker Compose

Потрібні Docker і Docker Compose. Бекенд має лежати поруч із цим каталогом під назвою `NULP-EM-skin-disease-classification-backend`: Compose збирає його з `../NULP-EM-skin-disease-classification-backend`.

Покладіть файл моделі в `../NULP-EM-skin-disease-classification-backend/app/classification_models/resnet_model.h5` до збирання. Він не входить до репозиторію й потрібен для старту API.

З каталогу фронтенду виконайте:

```bash
docker compose up --build
```

Відкрийте <http://localhost:3000>. API доступне на <http://localhost:8000>, його документація — на <http://localhost:8000/docs>. Compose запускає фронтенд, API та MongoDB. Перший запуск може бути довгим через ML-залежності; API використовує образ `linux/amd64`, тому на Apple Silicon працює через емуляцію. Фронтенд запускається сервером розробки Create React App; після змін коду для цього сценарію повторно виконайте `docker compose up --build`.

Для локального PoC Compose задає `SECRET_KEY` за замовчуванням. Власне значення можна передати так:

```bash
SECRET_KEY=your-local-secret docker compose up --build
```

Зупинити стек: `docker compose down`. Видалити також дані MongoDB: `docker compose down -v`. Не запускайте паралельно Compose з каталогу бекенду: обидва використовують порт `8000`.

## Локальний запуск без Docker

Після запуску API задайте адресу бекенду для Create React App і встановіть залежності:

```bash
npm ci --legacy-peer-deps
REACT_APP_API_BASE_URL=http://localhost:8000 npm start
```

Фронтенд буде доступний на <http://localhost:3000>.

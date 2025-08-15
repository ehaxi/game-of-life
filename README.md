# game-of-life

```
game-of-life-advanced/
│
├── docs/                         — документация, схемы архитектуры  
│
├── server/                       — Golang back-end
│   ├── cmd/
│   │   └── server/               — точка входа сервера
│   ├── internal/
│   │   ├── api/                  — REST/gRPC API
│   │   ├── service/              — бизнес-логика сервера (состояния, правила игры, очереди)
│   │   ├── storage/              — слой хранения (in-memory, Redis, SQL/Pg)
│   │   └── utils/                
│   └── go.mod                    
│
├── engine/                       — ядро логики игры (C# library)
│   ├── GameOfLife.Core/          — основные правила, состояния, обновление клеток
│   └── GameOfLife.API/           — публичный API для фронтов
│
├── web/                          — Web-интерфейс (SPA)
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   └── services/             — работа с API
│   ├── package.json
│   └── vite.config.ts
│
├── desktop_app/                  — десктопное приложение (Unity/Avalonia/.NET MAUI)
│   └── AdvancedLife.App/
│
├── mobile_app/ (по желанию)      — если захотите мобильную версию
│
└── deploy/
    ├── Dockerfile.server
    ├── docker-compose.yml
    └── k8s/
```

## 🟢 **Этап 1** - Подготовка
- Определить фичи MVP (минимально жизнеспособной версии)
- Выбрать стек технологий:
  - C# (движок), Go (сервер), React/Vue (Web), Avalonia/Maui (Desktop)
- Составить API контракт между engine ↔ server ↔ client
- Настроить репозиторий: `main`, `dev`, `feature/*`, `docs/*`

## ⚙️ **Этап 2** — Реализация ядра игры 
- Создать ядро (`GameOfLife.Core`) на C#
- Реализовать:
  - структуру поля
  - состояние клетки
  - обработку поколений
  - возможность задавать параметры правил (расширяемость)
- Написать unit-тесты для логики
- CLI-интерфейс для ручного запуска и дебага

## 🔌 **Этап 3** — Сервер (Go)
- Настроить базовую структуру Go-проекта
- Реализовать:
  - REST/gRPC API:
    - создать/получить мир
    - перейти к следующему поколению
  - Вызовы engine как отдельного CLI/микросервиса
- Добавить хранение состояния:
  - In-memory → Redis/PostgreSQL
- Написать Dockerfile

## 🌐 **Этап 4** — Web-клиент 
- Инициализировать фронт (Vite + React/Vue + TypeScript)
- Создать UI:
  - отображение поля (canvas/grid)
  - запуск/паузу симуляции
  - кнопки Next / Random / Reset
- Подключение к API сервера
- Реализовать WebSocket для live-обновлений (опционально)

## 💻 **Этап 5** — Desktop client 
- Выбрать технологию: Avalonia / .NET MAUI / Unity
- Переиспользовать библиотеку GameOfLife.Core
- Создать UI аналогично web-версии
- Добавить запуск симуляции офлайн и онлайн (подключение к серверу)

## 📦 **Этап 6** — DevOps & автоматизация
- Написать docker-compose (server + redis + web)
- Настроить CI / CD:
  - сборка image’ов
  - автозапуск тестов
- Автоматические выкатывания в dev/prod окружения
- Добавить генерацию релизов

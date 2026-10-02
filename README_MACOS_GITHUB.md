# SleepGuard — автоматическая сборка DMG для macOS

В проект уже добавлен GitHub Actions workflow. Он собирает настоящий macOS `.app`, упаковывает Qt-зависимости и создаёт `.dmg` без установки Qt на вашем Mac.

## Что собирается

Workflow делает две сборки:

- **Apple Silicon / arm64** — M1, M2, M3, M4 и новее;
- **Intel / x86_64** — Intel Mac.

Используется официальный macOS runner GitHub Actions и Qt 6. В Qt есть `macdeployqt`, который предназначен для создания self-contained macOS bundle и умеет создавать `.dmg`.

## Один раз: создать GitHub repository

1. Откройте GitHub и создайте новый repository, например `SleepGuard`.
2. Загрузите в него весь проект.
3. Убедитесь, что файл находится по пути:

   `.github/workflows/build-macos-dmg.yml`

## Запуск сборки

В GitHub:

1. Откройте repository.
2. Нажмите **Actions**.
3. Выберите **Build SleepGuard macOS DMG**.
4. Нажмите **Run workflow**.
5. Дождитесь зелёного статуса.
6. Откройте завершившийся запуск.
7. Внизу страницы **Artifacts** скачайте нужную сборку:
   - `SleepGuard-macOS-arm64` — Apple Silicon;
   - `SleepGuard-macOS-x86_64` — Intel.

В скачанном архиве будет:

`SleepGuard-arm64.dmg`

или

`SleepGuard-x86_64.dmg`

## Автоматически по тегу

Если создать tag вида:

`v0.1.0`

workflow также запустится автоматически.

## Важно: подпись Apple

Сейчас workflow делает **неподписанный для распространения** DMG. Для личного использования этого достаточно, но macOS может показать предупреждение Gatekeeper.

Для публичной раздачи понадобится Apple Developer signing и notarization. Это можно добавить позже через GitHub Secrets, не меняя саму архитектуру сборки.

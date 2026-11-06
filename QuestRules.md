# QuestRules — документ разделён на целевые инструкции

**Точка входа: [AGENTS.md](AGENTS.md).** Начиная с версии 0.50 спецификация больше не
лежит одним файлом — она разбита по темам, чтобы ИИ и человек читали только нужное.

Этот файл оставлен как указатель: старые ссылки вида «QuestRules.md §4.1» продолжают
работать и приводят сюда.

Набор описывает только разбор книги в пакет: вход — текст, выход — файлы. Проигрывание
пакетов ведётся отдельным проектом интерфейса.

| Было | Стало |
|---|---|
| §0.1–0.4 — о документе, пайплайн, режим конвертации | [AGENTS.md](AGENTS.md) |
| §0.5 — `review.md`, коды `C_*` | [docs/review.md](docs/review.md) |
| §1 — принципы формата | [AGENTS.md](AGENTS.md) |
| §2 — структура пакета, `game.yaml`, брифы | [docs/manifest.md](docs/manifest.md), [docs/illustrations.md](docs/illustrations.md), [docs/soundtrack.md](docs/soundtrack.md) |
| §2.2 — аннотированный `story.md` | [docs/story.md](docs/story.md) |
| §2.3 — `storyGraph.md` | [docs/story-graph.md](docs/story-graph.md) |
| §3 — сцена | [docs/story.md](docs/story.md) |
| §4 — переходы, варианты, броски | [docs/story.md](docs/story.md) |
| §5 — условия | [docs/manifest.md](docs/manifest.md) |
| §6 — эффекты | [docs/manifest.md](docs/manifest.md) |
| §7 — предметы | [docs/items.md](docs/items.md) |
| §8 — статусы и флаги | [docs/stats.md](docs/stats.md) |
| §9.1–9.2 — изображения | [docs/illustrations.md](docs/illustrations.md) |
| §9.3–9.5 — музыка | [docs/soundtrack.md](docs/soundtrack.md) |
| §10 — тема оформления | [docs/manifest.md](docs/manifest.md) |
| §11 — валидатор | [docs/manifest.md](docs/manifest.md) |
| §12 — правила оформления контента | [AGENTS.md](AGENTS.md) |
| §13 — реестр TBD | [AGENTS.md](AGENTS.md) |
| §15 / приложение А — эталонный пакет | [docs/manifest.md](docs/manifest.md), [docs/story.md](docs/story.md), [docs/items.md](docs/items.md), [docs/stats.md](docs/stats.md) |
| А.8 — пошаговая конвертация | [docs/conversion.md](docs/conversion.md) |

Если ссылка ведёт на конкретный раздел (`§4.5`, `А.8`), ищи его в файле-приёмнике из
таблицы: нумерация разделов сохранена.

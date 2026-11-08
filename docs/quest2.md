# Quest/2 — контракт пакета

> Часть инструкции QuestRules, версия набора 0.67.
> Точка входа — [AGENTS.md](../AGENTS.md).
>
> Полная нормативная схема: `MVP/engine_docs/QUEST2_SCHEMA.md`; машинная:
> `MVP/engine_docs/quest2.schema.json`.

## 1. Статус

- Quest/2 — новый формальный контракт пакета.
- Адаптер `quest/1 → quest/2` **не делается**.
- Существующие книги остаются `quest/1` до отдельного решения человека.
- Исходники книг лежат в `games/<id>/` и используются для сверки.
- 3.6 (build-time нормализация) отложен.

## 2. Отличие от quest/1

`quest/1` — набор файлов с неявными правилами: движок сам решает, что значит
`checks`, `combat`, `next.roll`, `shop`, `on_enter.goto`.

`quest/2` — явная модель:

- `profile` и `features`;
- `entry` — типизированные эффекты;
- `condition` — AST, не произвольная строка;
- `interaction` — один объект с `type`;
- `outcomes` — явные исходы;
- `combat.mode` — `pool | contest | rpg`;
- `start_items`, `visible`, `ui.counter`, `codebook`;
- обязательный `text` сцены;
- `after` — follow-up после `gamble`/`shop`;
- `combat.outcomes.defeat` необязателен: без него используется общий экран смерти.

## 3. Минимальный пакет

```yaml
format: quest/2
id: example
title: "Пример"
profile: storybook
start: "1"
scenes:
  "1":
    title: "Начало"
    interaction:
      type: choices
      options:
        - label: "Идти"
          to: "2"
  "2":
    title: "Конец"
    ending: true
```

## 4. Эффекты

```yaml
entry:
  - grant: { item: sword, count: 1 }
    once: true
  - consume: { item: medkit, count: 1 }
  - modify: { stat: hp, delta: -2 }
  - set_flag: met_guard
  - learn_code: map
  - redirect: death
```

Действия: `grant`, `consume`, `drop`, `modify`, `set_flag`, `clear_flag`,
`learn_code`, `drop_best_weapon`, `roll`, `redirect`.

## 5. Интеракции

- `choices` — варианты с `to`, `if`, `effects`;
- `continue` — линейный переход;
- `check` — `mode: stat|skill`, `formula`, `outcomes.success/failure`,
  `morale_cost`;
- `combat` — `mode`, `enemies`, `options`, `outcomes.victory/defeat`;
- `gamble` — `stat`, `stake`, `win`, `push`, `outcomes`;
- `shop` — `offers`, `title`, `currency`, `outcomes.continue`;
- `roll` — `formula`, диапазоны `outcomes`;
- `codebook` — панель известных кодов.

## 6. Валидация

JSON Schema проверяет форму. Семантический валидатор проверяет ссылки, формулы,
исходящие переходы, диапазоны, коды, `start_items` и достижимость.

```bash
python3 scripts/quest2_validate.py path/to/book.yaml
python3 scripts/quest2_graph.py path/to/book.yaml --json
python3 scripts/quest2_simulate.py path/to/book.yaml --runs 500 --seed 42
```

## 7. Конвертация

Все 11 существующих книг переведены в `games/<id>/quest2.yaml`:
0 `E_*`, предупреждения о недостижимости соответствуют прежним данным.
Старые `game.yaml`/`story.md` удалены; ассеты и PDF/TXT-исходники сохранены.

Существующие книги не переводятся автоматически. План и порядок —
`MVP/engine_docs/CONVERSION_PLAN.md`; перед изменением конкретной книги пакет
сверяется с исходником в её каталоге.

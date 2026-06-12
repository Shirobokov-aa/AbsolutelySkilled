# AbsolutelySkilled — установка и использование

Набор из 4 скиллов (инструкций) для AI-агентов. Ставятся через [skills CLI](https://github.com/vercel-labs/skills).

**Важно:** скиллы работают с AI-агентом, не с редактором. VS Code сам по себе скиллы не читает — нужен Copilot, Cline, Continue и т.д.

---

## Скиллы

### absolute-work
Полный цикл разработки: обсуждение → спецификация → задачи на доске → код с тестами → проверка. Ждёт твоё «ок» между фазами. Доска: `.absolute-work/board.md`.

**Промпты:**
```
absolute-work this: добавь OAuth через Google в этот проект
```
```
absolute-work: разбей этот тикет на задачи и начни с плана
```

### absolute-ui
Правила для красивого UI: отступы, цвета, типографика, тёмная тема, доступность. Без «AI-slop».

**Промпты:**
```
absolute-ui: сделай лендинг профессиональнее, стиль минималистичный
```
```
absolute-ui: стилизуй форму регистрации — кнопки, поля, ошибки, мобильная версия
```

### absolute-simplify
Упрощает код без смены поведения. Работает по git-изменениям или указанным файлам, гоняет тесты.

**Промпты:**
```
absolute-simplify
```
```
absolute-simplify src/utils/auth.ts — убери вложенность и дубли
```

### absolute-documentations
Документация по Diátaxis: tutorial, how-to, reference, explanation. Пишет, улучшает, аудирует. Сверяется с кодом.

**Промпты:**
```
absolute-documentations: напиши README для этой фичи
```
```
absolute-documentations: улучши docs/api.md — сейчас смешаны tutorial и reference
```

---

## Установка

### Только в проект (рекомендуется)

```bash
cd /path/to/your-project

# все 4 скилла
npx skills add AbsolutelySkilled/AbsolutelySkilled -a cursor -y

# выборочно
npx skills add AbsolutelySkilled/AbsolutelySkilled \
  --skill absolute-work --skill absolute-ui \
  -a cursor -y
```

| Область | Флаг | Куда |
|---------|------|------|
| Проект | без `-g` | `.agents/skills/` |
| Глобально | `-g` | `~/.cursor/skills/` |

### Cursor + VS Code сразу

Одна папка `.agents/skills/` для Cursor и Copilot/Cline:

```bash
cd /path/to/your-project

npx skills add AbsolutelySkilled/AbsolutelySkilled \
  -a cursor -a github-copilot -y
```

| Агент в VS Code | Флаг `--agent` | Папка |
|-----------------|----------------|-------|
| GitHub Copilot | `github-copilot` | `.agents/skills/` |
| Cline | `cline` | `.agents/skills/` |
| Continue | `continue` | `.continue/skills/` |
| Roo Code | `roo` | `.roo/skills/` |

Continue и Roo — отдельные папки, добавь `-a continue` или `-a roo` к команде.

### Флаги

| Флаг | Значение |
|------|----------|
| `-y` / `--yes` | Без вопросов в терминале |
| `-g` / `--global` | На все проекты |
| `-a` / `--agent` | Целевой агент (`cursor`, `github-copilot`, …) |
| `--skill` | Конкретный скилл (без флага — все) |

### Удалить глобальную установку

```bash
npx skills remove --global \
  absolute-work absolute-ui absolute-simplify absolute-documentations \
  -a cursor -y
```

### Обновить

```bash
npx skills update
npx skills list
```

---

## Использование

1. Открой проект, где установлены скиллы.
2. В чате агента (Cursor Agent, Copilot Agent и т.д.) напиши задачу и **назови скилл** в начале или в тексте.
3. Агент подхватывает скилл по `description` в `SKILL.md` — отдельная кнопка не нужна.

**Типичный порядок:** `absolute-work` (фича) → `absolute-ui` (интерфейс) → `absolute-simplify` (чистка) → `absolute-documentations` (доки).

`.agents/skills/` можно закоммитить в git — команда получит те же скиллы.

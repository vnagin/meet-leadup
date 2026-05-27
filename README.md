# meet.leadup.guru

Страница записи на AI-диагностику LeadUp AI.

## Страницы

| URL | Файл |
|-----|------|
| `meet.leadup.guru/diagnostics/` | `diagnostics/index.html` |

---

## Настройка DNS (для Владимира)

Добавьте одну CNAME-запись в настройках DNS-зоны `leadup.guru`:

| Тип | Хост | Значение | TTL |
|-----|------|----------|-----|
| `CNAME` | `meet` | `vnagin.github.io` | `3600` |

> **Где это делать:** в панели вашего DNS-провайдера (Cloudflare, reg.ru, namecheap и т.п.) → DNS → добавить запись.

После добавления записи страница станет доступна по адресу `https://meet.leadup.guru/diagnostics/` в течение 5–30 минут (после propagation DNS + выпуска SSL-сертификата GitHub Pages).

---

## Обновление контента

Все изменения делаются в файле `diagnostics/index.html`. Основные места:

- **Заголовок (h1)** — строка с тегом `<h1>`
- **Подзаголовок (lead)** — параграф с классом `class="lead"`
- **Статистика (hero)** — блоки `.stat-cell` в секции `.stats-grid`
- **Пункты agenda** — `<li>` внутри `.sb-card ul`
- **HubSpot embed** — атрибут `data-src` у `.meetings-iframe-container`
  - Текущий URL: `https://explore.leadup.guru/meetings/naginvlad/ai-diagnostics?embed=true`

После редактирования — сохраните файл, сделайте `git commit` и `git push`. GitHub Pages обновится автоматически в течение 1–2 минут.

```bash
git add -A
git commit -m "Update content"
git push
```

---

## Структура репо

```
meet-leadup/
├── CNAME                   # Кастомный домен
├── README.md               # Этот файл
└── diagnostics/
    └── index.html          # Страница диагностики
```

---

*Создано LeadUp AI. Вопросы — @neurosborka или hello@leadup.guru*

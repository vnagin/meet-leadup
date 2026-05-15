# meet-leadup

Лендинг с HubSpot Meetings iframe для записи на 40-мин AI-диагностику с CEO LeadUp AI. Развёрнут как статический сайт через GitHub Pages.

- **Live:** [https://meet.leadup.guru/diagnostics/](https://meet.leadup.guru/diagnostics/)
- **Темплейт:** dark, на токенах LeadUp v3 (D2 Cold Technical · C3 Electric Teal · TS1 Geist).
- **HubSpot embed:** скедулер `naginvlad/ai-diagnostics` через `https://static.hsappstatic.net/MeetingsEmbed/ex/MeetingsEmbedCode.js`.

## Структура

```
.
├── CNAME                  # meet.leadup.guru — для GitHub Pages
├── index.html             # редирект на /diagnostics/
├── diagnostics/
│   ├── index.html         # сама страница лендинга
│   └── logo-leadup.png    # лого (whitened через CSS-фильтр)
└── README.md
```

## Деплой (GitHub Pages)

1. Repo: `vnagin/meet-leadup` (private, GitHub Pro).
2. **Settings → Pages:** Source = `main` branch, folder = `/ (root)`.
3. **Custom domain:** `meet.leadup.guru` (берётся из файла `CNAME` автоматически).
4. **Enforce HTTPS:** включить после того, как GitHub выпустит сертификат (обычно 5–30 мин после привязки домена).

## DNS-настройка (для Владимира)

В DNS-зоне `leadup.guru` (Cloudflare / тот же провайдер, что и `explore.leadup.guru`) добавить запись:

```
Type:   CNAME
Name:   meet
Value:  vnagin.github.io
TTL:    Auto (или 3600)
Proxy:  DNS only (если Cloudflare — серая тучка, не оранжевая)
```

После того, как DNS пропагируется (обычно 5–15 минут), зайди в **GitHub → repo settings → Pages**, поставь галку «Enforce HTTPS» — GitHub выпустит сертификат Let's Encrypt автоматически.

Проверить:
```bash
dig meet.leadup.guru CNAME +short
# → vnagin.github.io.
curl -I https://meet.leadup.guru/diagnostics/
# → HTTP/2 200
```

## Как обновлять контент

Любая правка идёт через PR в `main`. После merge GitHub Pages автоматически пересобирает сайт за ~1 минуту.

- **Тексты, заголовки, sidebar:** `diagnostics/index.html`.
- **Логотип:** замените `diagnostics/logo-leadup.png` (PNG с прозрачным фоном; высота отрисовки — 24px).
- **HubSpot embed URL:** строка с `data-src="https://explore.leadup.guru/meetings/naginvlad/ai-diagnostics?embed=true"` в `diagnostics/index.html`.

## Бренд / дизайн

Канонические токены и UI-Kit (для следующих страниц на этом субдомене):

- `vault/company/brand/colors_and_type.css`
- `vault/company/brand/ui_kits/b2b-booking/index.html`

Цвета на странице используют только CSS-переменные из `:root` (см. начало `diagnostics/index.html`); хардкод hex-значений — вне `:root` запрещён.

## Зачем эта страница

Use case — участники интенсива «Hermes Agent — AI-ассистент руководителя» (21 мая 2026, cohort `intensive-hermes-2105`) переходят сюда, чтобы забронировать 40-мин разбор кейса с CEO. Встречи попадают в HubSpot CRM, помогает к ним готовиться Саша (sales).

Страница `/diagnostics/` родовая — копию обновляем под текущий cohort, новых страниц не плодим. Источник правды для текста и meta-тегов: `vault/projects/content-media/deliverables/intensive-hermes-agent/landing-copy.md`.

Связанные тикеты: LEA-506 (зонтик), LEA-507 (вёрстка), LEA-508 (HubSpot scheduler), LEA-1887 (cohort hermes-2105 update).

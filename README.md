# 🌮 Amira & Karan's Taco Tracker

A tiny couples' taco counter — *because every taco counts 💕*. Ported off Lovable to a
single static page hosted on GitHub Pages.

**Live site:** https://karakotaram.github.io/taco-counter/

## How it works

- **One file, no build step.** Everything lives in [`index.html`](index.html) — markup, styles,
  and a small ES-module script. GitHub Pages serves it directly.
- **Cross-device sync** is preserved via the original [Supabase](https://supabase.com) backend.
  The browser talks to Supabase directly using the public **anon** key (safe to expose — access is
  governed by Row Level Security), and realtime subscriptions keep every device in sync.

### Data model (Supabase)

| Table          | Columns                          | Notes                                            |
| -------------- | -------------------------------- | ------------------------------------------------ |
| `taco_counter` | `id`, `count`, `updated_at`      | Single row holding the running total.            |
| `taco_log`     | `id`, `added_at`                 | Append-only log of additions (delete is blocked by RLS). |

- **+1** increments `taco_counter.count` and inserts a `taco_log` row.
- **−1** decrements `taco_counter.count` only (the log is append-only).

## Local development

It's a static file — just open it, or serve the folder:

```bash
python3 -m http.server 8000   # then visit http://localhost:8000
```

## Deploying

Pushing to `main` auto-publishes via GitHub Pages (configured to serve the repo root).
The `.nojekyll` file tells Pages to serve files as-is without Jekyll processing.

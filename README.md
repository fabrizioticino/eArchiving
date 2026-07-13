# eArchiving — Conservazione a norma

Portale statico per la raccolta ragionata del materiale normativo sulla
**conservazione dei documenti informatici**. Perimetro **Italia + Unione
Europea**, organizzato in due parti:

- **Temi** — 12 aree tematiche (governance, processi, infrastruttura) del
  sistema di conservazione, ciascuna collegata alle fonti pertinenti.
- **Biblioteca normativa** — il corpus delle fonti (leggi, decreti, Linee
  guida AgID, circolari, regolamenti UE, standard ISO/ETSI), ricercabile e
  filtrabile per area, tipo e stato di vigenza.

> Materiale a fini informativi — non costituisce consulenza legale o fiscale.
> Verificare sempre la versione vigente sulle fonti ufficiali (AgID,
> Normattiva, EUR-Lex).

## 📁 Struttura del progetto

```
eArchiving/
├── index.html              ← la pagina del portale
├── data/
│   ├── temi.json            ← le 12 aree tematiche
│   ├── fonti.json           ← la biblioteca normativa
│   └── meta.json            ← timestamp ultimo aggiornamento
└── .github/workflows/
    └── deploy.yml            ← deploy automatico su GitHub Pages
```

## 🚀 Pubblicazione (GitHub Pages)

1. Su GitHub: **Settings → Pages → Build and deployment → Source: GitHub Actions**.
2. Ad ogni `push` su `master`, il workflow `deploy.yml` pubblica il sito.
3. L'URL pubblico compare in **Settings → Pages** (tipo
   `https://fabrizioticino.github.io/eArchiving/`).

## 🛠️ Aggiungere o aggiornare una fonte

Modifica `data/fonti.json` — un array di oggetti. Campi principali:

| Campo | Descrizione |
|---|---|
| `id` | Slug univoco (usato negli URL `#fonte-<id>`) |
| `short` | Nome breve mostrato sulla card |
| `title` | Titolo esteso |
| `type` | Tipo (Decreto legislativo, Linee guida, Regolamento UE, Standard…) |
| `issuer` | Ente emittente |
| `jurisdiction` | `IT`, `UE` o `INT` |
| `date` / `date_iso` | Data / vigenza |
| `status` | `vigente`, `superato` o `abrogato` |
| `summary` | Sintesi mostrata in apertura del dettaglio |
| `key_points` | Elenco puntato di articoli/aspetti chiave |
| `temi` | Array di `id` dei temi collegati (vedi `temi.json`) |
| `url` | Link alla fonte ufficiale |

Per i temi, modifica `data/temi.json`. Il collegamento tema ↔ fonte è
bidirezionale e si basa sull'array `temi` di ciascuna fonte.

## 🎨 Design

Stesso linguaggio editoriale del tracker
[einvoicing](https://github.com/fabrizioticino/einvoicing-tracker):
caratteri Fraunces / IBM Plex Mono / Inter, texture "carta", accento rosso.
Nessuna dipendenza, nessun build step — HTML/CSS/JS statico.

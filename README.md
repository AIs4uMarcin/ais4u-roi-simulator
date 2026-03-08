# ROI Simulator — AIsolution4.you

Symulator ROI dla AIsolution4.you. Spersonalizowana prognoza finansowa oparta na 66 udokumentowanych case studies.

## Stack

- **React 18** (CDN, UMD)
- **Recharts** (CDN, UMD) — wykresy cashflow
- **Babel Standalone** (CDN) — transpilacja JSX w przeglądarce (pre-prod)
- **Google Fonts** — DM Serif Display + Plus Jakarta Sans
- **Hosting** — GitHub Pages (statyczna strona)

## Deployment

### Automatyczny (GitHub Actions)

1. Utwórz repo na GitHubie
2. Push tego folderu do `main`
3. W repo → Settings → Pages → Source: **GitHub Actions**
4. GitHub automatycznie zbuduje i opublikuje

### Manualny

1. W repo → Settings → Pages → Source: **Deploy from a branch** → `main` / `/ (root)`
2. Strona dostępna pod: `https://TWOJ-USER.github.io/REPO-NAME/`

## Struktura

```
index.html          — Cała aplikacja (React SPA, ~95KB)
.nojekyll           — Wyłącza Jekyll processing
.github/workflows/  — Auto-deploy na push do main
```

## Dane referencyjne (embedded)

| Tabela | Rekordów | Opis |
|--------|----------|------|
| BENCH[] | 66 | Benchmarki KPI (Forrester, PMC, McKinsey, Gartner) |
| MSUM{} | 10 | Module summary (conservative/median/optimistic) |
| AUDIT_COST[] | 6 | Koszt audytu wg przychodu |
| IMPL_COST[] | 6 | Koszt I pakietu wg przychodu |
| MONTHLY_FEE[] | 5 | Miesięczne fee wg przychodu |
| REV_CEILING{} | 5×6 | Max wzrost wg oceny audytu × sektor |
| SIZE_CEILING[] | 5 | Dampener wielkości firmy |
| SRC_W{} | 9 | Wagi wiarygodności źródeł |
| PL_M{} | 6 | Mnożniki rynku polskiego |
| CDB[] | 20 | Baza audytowa Wielkopolska (demo) |

### @DB_MIGRATION

Na produkcji tabele zostaną przeniesione do bazy danych / API.
Getter functions (`getAuditCost`, `getImplPackageCost`, `getMonthlyFee`, `getRevenueCeiling`) to warstwa abstrakcji — zmiana implementacji gettera, reszta kodu bez zmian.

## Model biznesowy (3 fazy)

1. **Audyt** (jednorazowy) — 10K–200K PLN
2. **I Pakiet wdrożeniowy** (jednorazowy) — 40K–480K PLN
3. **Miesięczne fee** (od osiągnięcia KPI) + **Success fee 15%** (cap 2.5× annual)

## Produkcja (TODO)

- [ ] Vite build (zamiast Babel standalone)
- [ ] Backend API (tabele referencyjne)
- [ ] Twilio SMS 2FA
- [ ] Email verification
- [ ] jsPDF export raportu
- [ ] Strefa klienta (dashboard post-audit)

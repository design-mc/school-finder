# School Finder Portal - Przewodnik Wdrożeniowy

> **WAŻNE**: NIGDY nie używaj plików z folderu `-Trash`. Folder ten zawiera przestarzałe lub odrzucone dokumenty, które nie powinny być wykorzystywane w implementacji.

## 1. Przygotowanie do Wdrożenia

### 1.1. Wymagania
- Konto Vercel
- Konto GitHub
- Konto PlanetScale (lub AWS dla DynamoDB)
- Konto Google Cloud Platform (dla Google Maps API)
- Konto Apify
- Konto Stripe (dla płatności)

### 1.2. Zmienne Środowiskowe
Przygotuj następujące zmienne środowiskowe:

```
# Uwierzytelnianie
NEXTAUTH_URL=https://twoja-domena.com
NEXTAUTH_SECRET=twoj-tajny-klucz
GOOGLE_CLIENT_ID=twoj-google-client-id
GOOGLE_CLIENT_SECRET=twoj-google-client-secret
GITHUB_ID=twoj-github-id
GITHUB_SECRET=twoj-github-secret

# Baza danych
DATABASE_URL=twoj-url-do-bazy-danych

# API
APIFY_API_TOKEN=twoj-token-apify
GOOGLE_MAPS_API_KEY=twoj-klucz-google-maps

# Płatności
STRIPE_SECRET_KEY=twoj-tajny-klucz-stripe
STRIPE_WEBHOOK_SECRET=twoj-tajny-klucz-webhook-stripe
STRIPE_PRICE_ID=twoj-id-ceny-premium
```

## 2. Wdrożenie na Vercel

### 2.1. Połączenie z Repozytorium
1. Zaloguj się do Vercel i kliknij "New Project"
2. Połącz z repozytorium GitHub zawierającym kod projektu
3. Skonfiguruj projekt:
   - Framework Preset: Next.js
   - Root Directory: ./
   - Build Command: `npm run build`
   - Output Directory: .next

### 2.2. Konfiguracja Zmiennych Środowiskowych
1. W panelu projektu przejdź do zakładki "Settings" > "Environment Variables"
2. Dodaj wszystkie zmienne środowiskowe wymienione w sekcji 1.2

### 2.3. Konfiguracja Domeny
1. W panelu projektu przejdź do zakładki "Domains"
2. Dodaj własną domenę lub użyj domeny Vercel

## 3. Konfiguracja Bazy Danych

### 3.1. PlanetScale
1. Utwórz nową bazę danych w PlanetScale
2. Połącz bazę danych z projektem używając zmiennej środowiskowej `DATABASE_URL`
3. Uruchom migracje Prisma: `npx prisma migrate deploy`

### 3.2. DynamoDB (alternatywnie)
1. Utwórz tabele w AWS DynamoDB
2. Skonfiguruj dostęp AWS w zmiennych środowiskowych

## 4. Konfiguracja Zadań Cron

### 4.1. Vercel Cron Jobs
1. W pliku `vercel.json` dodaj konfigurację zadań cron:

```json
{
  "crons": [
    {
      "path": "/api/cron/update-school-data",
      "schedule": "0 1 * * *"
    },
    {
      "path": "/api/cron/sentiment-analysis",
      "schedule": "0 2 * * *"
    }
  ]
}
```

## 5. Monitorowanie i Utrzymanie

### 5.1. Logi i Alerty
1. Skonfiguruj Vercel Analytics do monitorowania wydajności
2. Ustaw alerty dla błędów i problemów z wydajnością

### 5.2. Kopie Zapasowe
1. Skonfiguruj regularne kopie zapasowe bazy danych
2. Ustaw procedury odzyskiwania danych

### 5.3. Aktualizacje
1. Regularnie aktualizuj zależności
2. Testuj aktualizacje w środowisku deweloperskim przed wdrożeniem
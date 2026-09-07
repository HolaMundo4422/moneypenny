# MoneyPenny

> A simple, mobile-first personal expense tracker built as a Progressive
> Web App (PWA), with Google Sheets as the data store.

MoneyPenny is a lightweight expense tracking application designed for
fast daily expense recording from desktop or mobile devices.

## Features

-   Mobile-first expense entry
-   Installable Progressive Web App (PWA)
-   Expense history with month navigation
-   Filtering by expense source: Ariq, Najwa, Together
-   Categories: Food, Transport, Groceries, Utilities, Health,
    Entertainment, Shopping, Education, Other
-   Payment methods: Cash, Debit, QRIS
-   Google Sheets integration
-   Offline expense queue using IndexedDB
-   Automatic synchronization when connectivity returns
-   Offline fallback page
-   Service Worker caching
-   Passcode-based authentication
-   Google Sheets serial-date handling

## Technology Stack

  Layer             Technology
  ----------------- ----------------------
  Framework         React Router v7
  Language          TypeScript
  Styling           Tailwind CSS v4
  UI                React
  Data Store        Google Sheets API v4
  Validation        Zod
  Offline Storage   IndexedDB
  PWA               Service Worker
  Hosting           Vercel
  Package Manager   npm

## Project Structure

``` text
MoneyPenny/
├── app/
│   ├── routes/
│   │   ├── _index.tsx
│   │   ├── history.tsx
│   │   ├── login.tsx
│   │   ├── offline.tsx
│   │   └── api.sync.tsx
│   ├── lib/
│   │   ├── sheets.server.ts
│   │   ├── auth.server.ts
│   │   ├── cookies.server.ts
│   │   ├── month.server.ts
│   │   ├── logger.server.ts
│   │   ├── constants.ts
│   │   ├── validation.ts
│   │   ├── offline-queue.ts
│   │   ├── sync.ts
│   │   └── types.ts
│   └── components/
│       ├── expense-form.tsx
│       ├── expense-card.tsx
│       ├── month-selector.tsx
│       └── ...
├── public/
│   ├── manifest.webmanifest
│   ├── sw.js
│   ├── icon-192.png
│   ├── icon-512.png
│   └── apple-touch-icon.png
├── .env.example
├── package.json
├── tsconfig.json
├── vite.config.ts
└── react-router.config.ts
```

## Google Sheets Structure

MoneyPenny uses Google Sheets as its primary data store.

  Column   Field            Description
  -------- ---------------- ----------------------------
  A        Timestamp        Server-generated timestamp
  B        Item             Expense description
  C        Category         Expense category
  D        Amount           Expense amount in IDR
  E        Payment Method   Cash, Debit, or QRIS
  F        Date             Expense date
  G        Source           Ariq, Najwa, or Together

Monthly sheets use the `YYYY-MM` naming convention, for example
`2026-09`.

The Date column should be formatted as a date in Google Sheets.
MoneyPenny also handles Google Sheets serial date values so historical
entries remain readable in the application.

## Environment Variables

Create a local `.env` file containing:

``` env
GOOGLE_SERVICE_ACCOUNT_EMAIL=
GOOGLE_PRIVATE_KEY=
GOOGLE_SPREADSHEET_ID=
AUTH_PASSCODE=
SESSION_SECRET=
```

Never commit `.env` or private credentials to Git.

## Local Development

Requirements:

-   Node.js 20 or newer
-   npm
-   Google Cloud project
-   Google Sheets API enabled
-   Google service account
-   Google Spreadsheet

Clone the repository:

``` bash
git clone https://github.com/HolaMundo4422/moneypenny.git
cd moneypenny
```

Install dependencies:

``` bash
npm install
```

Start the development server:

``` bash
npm run dev
```

The application normally runs at:

``` text
http://localhost:5173
```

## Available Scripts

``` bash
npm run dev
npm run build
npm run start
npm run typecheck
```

-   `npm run dev` --- start development server
-   `npm run build` --- create a production build
-   `npm run start` --- start the production server locally
-   `npm run typecheck` --- run TypeScript type checking

## Offline Support

When online, expenses are sent to the server and stored in Google
Sheets.

When offline, MoneyPenny stores pending expenses locally in IndexedDB.
The Service Worker and client-side synchronization mechanisms can
synchronize pending entries when connectivity returns.

## Deployment

MoneyPenny is deployed with Vercel.

``` text
Local Changes
    ↓
Git Commit
    ↓
Git Push
    ↓
GitHub
    ↓
Vercel
    ↓
MoneyPenny Production
```

## PWA

PWA configuration:

``` text
public/manifest.webmanifest
```

Icons:

``` text
public/icon-192.png
public/icon-512.png
public/apple-touch-icon.png
```

Service Worker:

``` text
public/sw.js
```

## Security

Sensitive configuration must remain in environment variables.

Do not commit:

``` text
.env
```

or Google service account credentials.

The Google service account should only have the permissions required by
the MoneyPenny spreadsheet.

## License

This project is licensed under the MIT License.

See the `LICENSE` file for details.

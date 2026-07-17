# ackerblog

> Another simple blog implementation :v

![TypeScript](https://img.shields.io/badge/TypeScript-4.5-3178C6?logo=typescript&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-12-000000?logo=next.js&logoColor=white)
![React](https://img.shields.io/badge/React-17-61DAFB?logo=react&logoColor=black)
![Contentful](https://img.shields.io/badge/Contentful-CMS-2478CC?logo=contentful&logoColor=white)

A simple blog built with **Next.js**, **TypeScript**, and **React**, using [**Contentful**](https://www.contentful.com/) as a headless CMS for content. The project is configured for one-click deployment to **Netlify**.

> **Project status:** early-stage scaffold. The Contentful client is wired up and ready to use, while the homepage currently renders the default Next.js starter page. See [Roadmap](#roadmap) for what's next.

## Tech Stack

| Layer      | Technology                                             |
| ---------- | ------------------------------------------------------ |
| Framework  | [Next.js](https://nextjs.org/) 12                      |
| Language   | [TypeScript](https://www.typescriptlang.org/) 4.5      |
| UI         | [React](https://react.dev/) 17 + React DOM             |
| Content    | [Contentful](https://www.contentful.com/) SDK (`contentful` v9) |
| Styling    | CSS Modules + global CSS                               |
| Deployment | [Netlify](https://www.netlify.com/) (`@netlify/plugin-nextjs`) |
| Tooling    | ESLint (`eslint-config-next`) + Prettier               |

## Features

- **Next.js + TypeScript** application scaffold with strict React mode enabled.
- **Contentful integration** — a preconfigured Contentful client (`src/services/contentful.ts`) that authenticates via environment variables, ready to fetch blog content.
- **API routes** — Next.js API routes under `pages/api` (includes a sample `hello` endpoint).
- **CSS Modules** for component-level styling plus a global stylesheet.
- **Netlify-ready** — includes a `netlify.toml` with the official Next.js runtime plugin for zero-config deployment.
- **CI linting** — a GitHub Actions workflow runs ESLint and Prettier on every push and pull request to `main`.

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (v16+ recommended)
- [Yarn](https://yarnpkg.com/)
- A [Contentful](https://www.contentful.com/) account and space (for content)

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/AckerCoder/ackerblog.git
   cd ackerblog
   ```

2. Install dependencies:

   ```bash
   yarn install
   ```

3. Create a `.env` file at the project root and copy in the contents of `.env.example`:

   ```bash
   cp .env.example .env
   ```

4. Fill in your Contentful credentials in `.env`:

   ```env
   CONTENTFUL_SPACE_ID=your_space_id
   CONTENTFUL_ACCESS_TOKEN=your_access_token
   ```

### Running the app

Start the development server:

```bash
yarn dev
```

Then open [http://localhost:3000](http://localhost:3000) in your browser.

## Available Scripts

| Command      | Description                                        |
| ------------ | -------------------------------------------------- |
| `yarn dev`   | Start the development server on `localhost:3000`.  |
| `yarn build` | Create an optimized production build.              |
| `yarn start` | Run the production server (requires a build).      |
| `yarn lint`  | Run ESLint via `next lint`.                        |

## Fetching content from Contentful

Content is accessed through the shared Contentful client:

```ts
import { client } from "../src/services/contentful";

// Example: fetch entries from your space
const entries = await client.getEntries();
```

The client reads its credentials from the `CONTENTFUL_SPACE_ID` and `CONTENTFUL_ACCESS_TOKEN` environment variables, so make sure your `.env` file is populated before making requests.

## Project Structure

```
ackerblog/
├── pages/
│   ├── _app.tsx              # Custom App component (global CSS)
│   ├── index.tsx             # Home page
│   └── api/
│       └── hello.ts          # Sample API route
├── src/
│   └── services/
│       └── contentful.ts     # Configured Contentful client
├── styles/
│   ├── globals.css           # Global styles
│   └── Home.module.css       # Home page CSS module
├── public/                   # Static assets
├── .github/
│   └── workflows/main.yml    # ESLint + Prettier CI
├── .env.example              # Environment variable template
├── netlify.toml              # Netlify deployment config
└── next.config.js            # Next.js configuration
```

## Deployment

The project is preconfigured for **Netlify**. The included `netlify.toml` registers the official `@netlify/plugin-nextjs` runtime, so connecting the repository in the Netlify dashboard is enough to build and deploy it.

Remember to set the `CONTENTFUL_SPACE_ID` and `CONTENTFUL_ACCESS_TOKEN` environment variables in your Netlify site settings.

## Roadmap

- Render a blog post list on the homepage from Contentful entries.
- Add individual post detail pages.
- Introduce a content model for posts (title, body, author, date).

## License

No license file is currently included in this repository.

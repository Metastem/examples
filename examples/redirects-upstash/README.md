# Edge Redirects with Upstash

This demo features a list of redirects, both hardcoded and coming from Redis ([Upstash](https://upstash.com/)), that get evaluated at the edge.

The demo has a total of 10,000 redirects, 1,000 of which are hardcoded on a JSON file, and 9,000 added to Redis.

## Demo

https://edge-functions-api-rate-limit.vercel.app/

### One-Click Deploy

Deploy the example using [Vercel](https://vercel.com?utm_source=github&utm_medium=readme):

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fvercel-customer-feedback%2Fedge-functions%2Ftree%2Fmain%2Fexamples%2Fapi-rate-limit&env=UPSTASH_REST_API_DOMAIN,UPSTASH_REST_API_TOKEN&project-name=api-rate-limit&repo-name=api-rate-limit)

## Getting Started

You'll need to have an account with [Upstash](https://upstash.com/). Once that's done, copy the `.env.example` file in this directory to `.env.local` (which will be ignored by Git):

```bash
cp .env.example .env.local
```

Then open `.env.local` and set the environment variables to match the REST API and Edge API of your database. It should look like this:

```bash
# Upstash REST API
UPSTASH_REST_API_DOMAIN = "us1-shiny-firefly-12345.upstash.io"
UPSTASH_REST_API_TOKEN = "your-api-token"

# Upstash Edge API
UPSTASH_EDGE_API_DOMAIN = "us1-shiny-firefly-12345.edge-a.upstash.io"
UPSTASH_EDGE_API_TOKEN = "your-edge-token"
```

We use the REST API to setup the redirects in Upstash ([source](scripts/upstash.js)), if you prefer not to do that then set `POPULATE_REDIS` to `false` in `.env`.

We use the Edge API to have the lowest latency possible when fetching a redirect, it's also possible to only use the REST API by replacing `upstashEdge` with `upstashRest` in [lib/redirects.ts](lib/redirects.ts).

Next, run Next.js in development mode:

```bash
npm install
npm run dev

# or

yarn
yarn dev
```
# --- Build stage ---
FROM node:22-alpine AS builder

WORKDIR /app

COPY package.json package-lock.json ./
# --legacy-peer-deps: vite-plugin-vuetify@1.0.2 declares a peer range (vite 2-4)
# older than the vite version Nuxt 3.21 actually bundles; the pair works fine in
# practice, but strict peer resolution (and therefore `npm ci`) rejects it.
RUN npm install --no-audit --no-fund --legacy-peer-deps

COPY . .
RUN npm run build

# --- Production stage ---
FROM node:22-alpine AS runner

ENV NODE_ENV=production
ENV PORT=3001
ENV HOST=0.0.0.0

WORKDIR /app

RUN addgroup -S nuxt && adduser -S nuxt -G nuxt
COPY --from=builder --chown=nuxt:nuxt /app/.output ./.output
USER nuxt

EXPOSE 3001

CMD ["node", ".output/server/index.mjs"]

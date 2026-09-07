# --- Build stage ---
FROM node:22-alpine AS builder

WORKDIR /app

# node:22-alpine bundles npm 10, whose optional-dependency resolver picks the
# wrong libc variant for Nuxt's native oxc bindings on musl (alpine); npm 12
# fixes that detection, so pin it here rather than relying on the base image.
RUN npm install -g npm@12

COPY package.json package-lock.json ./
# --dangerously-allow-all-scripts: npm 12 blocks install scripts for packages
# not on an allowlist by default; this build stage is discarded after `.output`
# is copied out, so there is no persistence risk in letting them run.
RUN npm ci --no-audit --no-fund --dangerously-allow-all-scripts

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

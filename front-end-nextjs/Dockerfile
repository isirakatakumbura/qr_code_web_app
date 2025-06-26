FROM node:18-alpine AS base

WORKDIR /app

COPY package.json yarn.lock* package-lock.json* ./

RUN \
    if [ -f yarn.lock ]; then \
        yarn install --frozen-lockfile; \
    elif [ -f package-lock.json ]; then \
        npm ci; \
    elif [ -f pnpm-lock.yaml ]; then corepack enable pnpm && pnpm I --frozen-lockfile; \
    else echo "lock file not found, skipping install" && exit 1; \
    fi

COPY . .

RUN npm run build

EXPOSE 3000

CMD ["npm", "start"]
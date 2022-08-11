# Build the nextjs site
FROM node:16 AS builder

# Install git
RUN apt-get -y update
RUN apt-get -y install git

WORKDIR /birklehof-materialausgabe
ENV NEXT_TELEMETRY_DISABLED 1

# Download the code from github and copy the config file

RUN git clone --depth=1 -b main https://github.com/C0mput3r5c13nt15t/birklehof-materialausgabe.git .
COPY .env.local .env.local

RUN yarn install
RUN yarn build

# Deploy the nextjs site
FROM node:16 AS deployment

WORKDIR /birklehof-materialausgabe
ENV NODE_ENV production
ENV NEXT_TELEMETRY_DISABLED 1

# Don't run production as root
RUN addgroup --system --gid 1001 nodejs
RUN adduser --system --uid 1001 nextjs
USER nextjs

# COPY --from=builder /birklehof-materialausgabe/public ./public
COPY --from=builder /birklehof-materialausgabe/next.config.js .
COPY --from=builder /birklehof-materialausgabe/package.json .

# Automatically leverage output traces to reduce image size
# https://nextjs.org/docs/advanced-features/output-file-tracing
COPY --from=builder --chown=nextjs:nodejs /birklehof-materialausgabe/.next/standalone ./
COPY --from=builder --chown=nextjs:nodejs /birklehof-materialausgabe/.next/static ./.next/static

COPY .env.local .env.local

CMD node server.js


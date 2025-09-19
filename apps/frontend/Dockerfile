FROM node:18-alpine

WORKDIR /app

# Install curl for health checks
RUN apk add --no-cache curl

COPY package*.json ./
RUN npm install

COPY . .

# Set environment variables for stable dev mode
ENV NODE_ENV=development
ENV NEXT_TELEMETRY_DISABLED=1
ENV CHOKIDAR_USEPOLLING=true
ENV WATCHPACK_POLLING=true

EXPOSE 3000

# Health check to ensure the container stays running
HEALTHCHECK --interval=30s --timeout=10s --start-period=30s --retries=3 \
    CMD curl -f http://localhost:3000 || exit 1

# Use a more stable command for dev mode
CMD ["npm", "run", "dev", "--", "--hostname", "0.0.0.0", "--port", "3000"]

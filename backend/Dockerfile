# Multi-stage build for production-ready Node.js backend

# Stage 1: Build dependencies
FROM node:18-alpine AS dependencies
WORKDIR /app

# Copy package files
COPY package.json package-lock.json* ./

# Install production dependencies only
RUN npm ci --only=production && npm cache clean --force

# Stage 2: Production image
FROM node:18-alpine AS production

# Set working directory
WORKDIR /app

# Set production environment
ENV NODE_ENV=production

# Copy dependencies from build stage
COPY --from=dependencies /app/node_modules ./node_modules

# Copy application source code
COPY package.json package-lock.json* ./
COPY server.js ./
COPY app ./app

# Expose port 8080
EXPOSE 8080

# Default command to start the server
CMD ["node", "server.js"]


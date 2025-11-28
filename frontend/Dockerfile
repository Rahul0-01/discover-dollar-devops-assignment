# Multi-stage build for production-ready Angular frontend

# Stage 1: Build the Angular application
FROM node:18-alpine AS builder

WORKDIR /app

# Copy package files
COPY package.json package-lock.json ./

# Install dependencies
# Use npm ci for faster, reliable, reproducible builds if package-lock.json exists
RUN npm ci

# Copy the rest of the source code
COPY . .

# Build the Angular application for production
# Using ng build with production configuration
RUN npm run build -- --configuration production

# Stage 2: Serve with Nginx
FROM nginx:alpine

# Copy custom Nginx configuration for Angular SPA
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copy built Angular application from builder stage
COPY --from=builder /app/dist/angular-15-crud /usr/share/nginx/html

# Expose port 8081
EXPOSE 8081

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]


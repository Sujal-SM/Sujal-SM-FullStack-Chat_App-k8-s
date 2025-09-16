# Stage 1: Build
FROM node:18-alpine AS builder

# Set working directory
WORKDIR /app

# Install dependencies
COPY package*.json ./

RUN npm ci --only=production

# Copy source code
COPY . .

#2nd stage build
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Create a non-root user to run the application
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Copy application files and dependencies from the builder stage
COPY --from=builder /app ./
COPY --from=builder /app/node_modules ./node_modules

# Expose application port
EXPOSE 5001

# Set environment variables
ENV NODE_ENV=production

# Switch to non-root user
USER appuser

# Start the application
CMD [ "npm","start" ]


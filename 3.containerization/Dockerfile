# Using LTS version
FROM node:22-alpine AS builder

WORKDIR /usr/src/app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm ci

# Copy the source
COPY . .

# Run build
RUN npm run build


# Final production image
FROM node:22-alpine

# Set timezone
RUN apk add --no-cache tzdata
ENV TZ=America/Sao_Paulo

# Set production environment
ENV NODE_ENV=production

WORKDIR /usr/src/app

# Change ownership of directory
RUN chown node:node .
USER node


# Copy package files
COPY package*.json ./

# Install production-only dependencies
RUN npm ci

# Copy build artifacts from builder
COPY --from=builder /usr/src/app/dist ./

# Expose microservice port
EXPOSE 3000

# Start command
CMD ["npm", "start"]
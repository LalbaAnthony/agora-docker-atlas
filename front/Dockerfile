FROM node:18-alpine as build-stage

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm ci

# Copy the rest of the application
COPY . .

# Build the application for production (if needed for production)
RUN npm run build

# Production stage
FROM node:18-alpine

WORKDIR /app

# Copy from build stage
COPY --from=build-stage /app ./

# Set environment variables
ENV HOST=0.0.0.0
ENV PORT=3000
ENV NODE_ENV=development

# Expose the port the app will run on
EXPOSE 3000

# Start the application in development mode for hot reload
CMD [ "npm", "run", "dev" ]
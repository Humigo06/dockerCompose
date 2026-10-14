# Stage 1: Build the React application
FROM node:18-alpine as builder

# Set working directory inside container
WORKDIR /app

# Copy package files first (for better caching)
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy application code
COPY . .

# Build the production application
RUN npm run build

# Stage 2: Serve with nginx
FROM nginx:alpine

# Copy built files from previous stage
COPY --from=0 /app/dist /usr/share/nginx/html

# Expose the port
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
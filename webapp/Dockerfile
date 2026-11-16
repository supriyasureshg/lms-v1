```dockerfile
# Docker file for React app created using Vite
FROM node:20 AS build

# Create app directory
WORKDIR /app

# Install app dependencies
COPY package*.json ./
RUN npm install

# Build app
COPY . .
RUN npm run build

# Nginx server using non-root user
FROM nginxinc/nginx-unprivileged:alpine

# Copy React build files
COPY --from=build /app/dist /usr/share/nginx/html

# Copy Nginx configuration for SPA routing
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose unprivileged Nginx port
EXPOSE 8080

# Start Nginx in foreground
CMD ["nginx", "-g", "daemon off;"]
```

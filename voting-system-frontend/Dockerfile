# Use an official Node.js runtime as a parent image
FROM node:14

# Set the working directory
WORKDIR /usr/src/app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the app for production
RUN npm run build

# Use an official Nginx image to serve the frontend
FROM nginx:1.19-alpine

# Copy the build output to replace the default Nginx static assets
COPY --from=0 /usr/src/app/build /usr/share/nginx/html

# Expose port 100
EXPOSE 100

# Update Nginx configuration to listen on port 100
RUN echo 'server { listen 100; location / { root /usr/share/nginx/html; index index.html index.htm; try_files $uri $uri/ /index.html =404; } }' > /etc/nginx/conf.d/default.conf

# Command to run Nginx
CMD ["nginx", "-g", "daemon off;"]
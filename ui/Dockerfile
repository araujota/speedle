# Stage 1: Build the React app
FROM node:14 AS build

# Set the working directory
WORKDIR /urs/src/ui

# Copy package.json and package-lock.json
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the React app
RUN npm run build

# Stage 2: Serve the app with nginx
FROM nginx:alpine

# Copy the build output to the nginx html directory
COPY --from=build /ui/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf

# Copy custom nginx configuration if needed
# COPY nginx.conf /etc/nginx/nginx.conf

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]

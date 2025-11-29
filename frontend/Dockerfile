# 1) build
FROM node:18-alpine as build-stage
WORKDIR /app
COPY package*.json ./

# FIX: use install instead of npm ci
RUN npm install --legacy-peer-deps

COPY . .
RUN npm run build -- --configuration production

# 2) serve with nginx
FROM nginx:stable-alpine

# Remove default nginx welcome page
RUN rm -rf /usr/share/nginx/html/*

COPY --from=build-stage /app/dist/angular-15-crud/ /usr/share/nginx/html/
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

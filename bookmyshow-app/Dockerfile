# ---------- Build Stage ----------
FROM node:18 AS build
WORKDIR /app

# Set OpenSSL legacy provider for older React scripts
ENV NODE_OPTIONS=--openssl-legacy-provider
ENV CI=false

COPY package*.json ./
RUN npm install --legacy-peer-deps

COPY . .
RUN npm run build

# ---------- Production Stage ----------
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

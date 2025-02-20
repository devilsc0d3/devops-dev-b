
FROM node:lts-alpine AS build

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

ARG VITE_API_URL
ENV VITE_API_URL=${VITE_API_URL}

RUN npm run build

# Étape 2 : Serveur Nginx pour les fichiers statiques
FROM nginx:alpine

# Copier les fichiers build dans le dossier de Nginx
COPY --from=build /app/dist /usr/share/nginx/html

# Exposer le port 80
EXPOSE 80

# Lancer Nginx
CMD ["nginx", "-g", "daemon off;"]

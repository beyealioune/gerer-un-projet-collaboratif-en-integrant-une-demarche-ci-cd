# Stage 1: Build
FROM node:latest as build

# Définir le répertoire de travail
WORKDIR /usr/local/app

# Copier les fichiers de package et installer les dépendances
COPY package*.json ./
RUN npm install -g @angular/cli
RUN npm install

# Copier le reste du code source et construire le projet
COPY ./ ./
RUN npm run build --prod

# Stage 2: Serve
FROM nginx:latest as production

# Copier la configuration nginx
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copier les fichiers construits à partir du stage précédent
COPY --from=build /usr/local/app/dist/bobapp /usr/share/nginx/html

# Exposer le port 80
EXPOSE 80

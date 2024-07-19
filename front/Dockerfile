# Étape 1 : Construction
FROM node:21 AS build

# Définir le répertoire de travail
WORKDIR /usr/local/app

# Copier les fichiers package.json et yarn.lock
COPY package.json yarn.lock ./

# Installer les dépendances
RUN yarn install

# Copier le reste du code source de l'application
COPY ./ ./

# Installer Angular CLI globalement
RUN yarn global add @angular/cli

# Construire l'application
RUN yarn build

# Étape 2 : Production
FROM nginx:latest AS production

# Copier la configuration personnalisée de Nginx
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copier les fichiers construits depuis l'étape de construction
COPY --from=build /usr/local/app/dist/bobapp /usr/share/nginx/html

# Exposer le port 80
EXPOSE 80

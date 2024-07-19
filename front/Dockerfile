# Étape de build
FROM node:latest as build

# Définir le répertoire de travail
WORKDIR /usr/local/app

# Copier les fichiers de package
COPY package.json package-lock.json ./

# Installer les dépendances
RUN yarn

# Installer Angular CLI globalement
RUN npm install -g @angular/cli

# Copier tous les fichiers du projet dans le conteneur
COPY ./ ./

# Exécuter la commande de build
RUN npx ng build

# Étape de production
FROM nginx:latest as production

# Copier la configuration NGINX personnalisée
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copier les fichiers de build de l'étape précédente
COPY --from=build /usr/local/app/dist/bobapp /usr/share/nginx/html

# Exposer le port 80
EXPOSE 80

# Commande par défaut pour lancer NGINX
CMD ["nginx", "-g", "daemon off;"]

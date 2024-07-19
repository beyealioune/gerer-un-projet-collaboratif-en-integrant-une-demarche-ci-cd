# Étape de build
FROM node:latest as build

# Définir le répertoire de travail
WORKDIR /usr/local/app

# Copier les fichiers package.json et package-lock.json séparément
COPY package.json package-lock.json ./

# Installer les dépendances en mode développement
RUN NODE_ENV=development npm install

# Installer Angular CLI localement
RUN npm install @angular/cli@latest

# Copier le reste des fichiers du projet
COPY . .

# Exécuter la commande de build
RUN npx ng build --prod

# Étape de production
FROM nginx:latest as production

# Copier le fichier de configuration Nginx personnalisé
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copier les fichiers construits depuis l'étape de build vers le répertoire Nginx
COPY --from=build /usr/local/app/dist/bobapp /usr/share/nginx/html

# Exposer le port 80 pour le service Nginx
EXPOSE 80

# Démarrer Nginx
CMD ["nginx", "-g", "daemon off;"]

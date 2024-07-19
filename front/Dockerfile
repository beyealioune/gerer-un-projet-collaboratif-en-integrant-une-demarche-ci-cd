# Utiliser une image Node.js officielle comme image parente
FROM node:16

# Définir le répertoire de travail
WORKDIR /app

# Copier package.json et package-lock.json dans le conteneur
COPY package*.json ./

# Installer les dépendances
RUN npm install

# Copier le reste du code de l'application
COPY . .

# Construire l'application
RUN npm run build

# Exposer le port (si nécessaire)
EXPOSE 3000

# Commande pour exécuter l'application
CMD ["npm", "start"]

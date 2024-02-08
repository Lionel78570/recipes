# Utilisez une image Node.js stable comme base
FROM node:14

# Définissez le répertoire de travail à l'intérieur du conteneur
WORKDIR /usr/src/app

# Copiez le package.json et le package-lock.json dans le répertoire de travail
COPY package*.json ./

# Installez les dépendances
RUN npm install

# Copiez le reste des fichiers dans le répertoire de travail
COPY . .

# Exposez le port sur lequel l'application fonctionne
EXPOSE 1337

# Commande de démarrage de l'application
CMD ["npm", "start"]

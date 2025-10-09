🎨 Frontend – Angular
🧩 Installation locale

Pour développer ou tester localement le front-end :

cd front
npm install
npm start


L’application sera accessible sur http://localhost:4200
.

⚙️ CI – GitHub Actions (Intégration Continue)
📄 Fichier : .github/workflows/ci-front.yml

Le workflow CI Frontend Angular s’exécute à chaque push sur une branche feature-branch et effectue :

Installation des dépendances Node.js

Exécution des tests unitaires avec Karma en mode headless Chrome
→ Génération d’un rapport de couverture (coverage/bobapp/lcov.info)

Build Angular de production (dist/)

Upload des artefacts :

frontend-coverage → pour SonarCloud

frontend-dist → pour le déploiement

Analyse SonarCloud dédiée au front :

Projet SonarCloud : mako2727_frontend-app

Organisation : mako2727

Token : SONAR_TOKEN_FRONT

👉 Pour déclencher le CD, assurez-vous que les KPI sur SonarCloud sont respectés, puis réalisez le merge de la branche feature vers main.

🚀 CD – GitHub Actions (Déploiement Continu)
📄 Fichier : .github/workflows/cd-front.yml

Le workflow CD Frontend Angular s’exécute à chaque push sur la branche main et effectue :

Installation et build Angular (production)

npx ng build --configuration production


Connexion à Docker Hub via DOCKERHUB_USERNAME et DOCKERHUB_TOKEN

Build de l’image Docker du front

Contexte : front/

Dockerfile : front/Dockerfile

Push vers Docker Hub

monapp-frontend:latest

monapp-frontend:${{ github.sha }} (tag unique par commit)

📊 KPI à surveiller sur SonarCloud
Indicateur	Objectif	Outil
Couverture de tests	≥ 80 %	Karma + lcov
Bugs	Niveau A	SonarCloud
Vulnérabilités	Niveau A	SonarCloud
Code Smells	< 50	SonarCloud
Temps moyen du pipeline	≤ 5 min	GitHub Actions

🐳 Image Docker Frontend
Élément	Valeur
Nom sur Docker Hub	${{ secrets.DOCKERHUB_USERNAME }}/monapp-frontend
Tags	latest, ${{ github.sha }}
Contexte	front/
Fichier Dockerfile	front/Dockerfile



🎨 Backend – Spring Boot
🧩 Installation locale

Pour développer ou tester localement le back-end :

cd back
mvn clean install
mvn spring-boot:run


L’API sera accessible sur http://localhost:8080.

⚙️ CI – GitHub Actions (Intégration Continue)
📄 Fichier : .github/workflows/ci-back.yml

Le workflow CI Backend Spring Boot s’exécute à chaque push sur une branche feature-branch et effectue :

Installation et setup Java 11 (Temurin)

Exécution des tests unitaires avec Maven + Jacoco → génération du coverage XML (target/site/jacoco/jacoco.xml)

Analyse SonarCloud dédiée au back :

Projet SonarCloud : mako2727_backend-app

Organisation : mako2727

Token : SONAR_TOKEN_BACK

Artefacts uploadés :

backend-classes → pour SonarCloud

backend-coverage → pour SonarCloud

👉 Pour déclencher le CD, assurez-vous que les KPI sur SonarCloud sont respectés, puis réalisez le merge de la branche feature vers main.

🚀 CD – GitHub Actions (Déploiement Continu)
📄 Fichier : .github/workflows/cd-back.yml

Le workflow CD Backend Spring Boot s’exécute à chaque push sur la branche main et effectue :

Build Maven projet (skip tests)

mvn clean package -DskipTests


Connexion à Docker Hub via DOCKERHUB_USERNAME et DOCKERHUB_TOKEN

Build de l’image Docker du back :

Contexte : back/

Dockerfile : back/Dockerfile

Push vers Docker Hub :

monapp-backend:latest

monapp-backend:${{ github.sha }} (tag unique par commit)

📊 KPI à surveiller sur SonarCloud

Indicateur	Objectif	Outil
Couverture de tests	≥ 80 %	Jacoco XML
Bugs	Niveau A	SonarCloud
Vulnérabilités	Niveau A	SonarCloud
Code Smells	< 50	SonarCloud
Temps moyen du pipeline	≤ 5 min	GitHub Actions

🐳 Image Docker Backend

Élément	Valeur
Nom sur Docker Hub	${{ secrets.DOCKERHUB_USERNAME }}/monapp-backend
Tags	latest, ${{ github.sha }}
Contexte	back/
Fichier Dockerfile	back/Dockerfile
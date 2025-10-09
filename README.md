# 🚀 Projet Fullstack — Angular & Spring Boot

---

## 🎨 FRONT-END (Angular)

### ⚙️ Installation locale
```bash
cd front
npm install
npm run start


⚡ CI — Intégration Continue (GitHub Actions)

À chaque push sur une branche, le workflow CI Frontend :

Installe les dépendances (npm ci)

Exécute les tests unitaires avec Karma

Génère le rapport de couverture de code (front/coverage/bobapp/lcov.info)

Upload l’artefact de couverture pour le job global SonarCloud

Compile l’application Angular (npm run build -- --prod)

Objectif : garantir que le front-end est stable, testé et compilable avant toute livraison.


🚀 CD — Déploiement Continu (Docker Hub)

Le workflow CD Frontend :

Construit l’image Docker à partir du Dockerfile dans front/

Se connecte à Docker Hub

Push l’image avec deux tags :

mako2727/monapp-frontend:latest
mako2727/monapp-frontend:<commit-sha>


Objectif : disposer d’images Docker versionnées et prêtes pour le déploiement.


📊 KPIs SonarCloud — Front
Indicateur	Objectif	Source
Couverture de tests	≥ 80 %	Rapport Karma / lcov
Bugs & Vulnérabilités	Niveau A	Analyse SonarCloud
Duplications	≤ 3 %	SonarCloud
Code Smells	≤ 10	SonarCloud



⚙️ BACK-END (Spring Boot)
⚙️ Installation locale
cd back
mvn clean install
mvn spring-boot:run

⚡ CI — Intégration Continue (GitHub Actions)

À chaque push sur une branche, le workflow CI Backend :

Configure l’environnement Java (Temurin 11)

Exécute les tests (mvn clean verify)

Génère un rapport de couverture Jacoco (back/target/site/jacoco/jacoco.xml)

Upload l’artefact pour SonarCloud

Prépare les classes compilées (target/classes) pour l’analyse

Objectif : assurer une couverture suffisante et détecter les régressions sur l’API.


🚀 CD — Déploiement Continu (Docker Hub)

Le pipeline CD Backend :

Construit l’image Docker depuis back/Dockerfile

Se connecte à Docker Hub

Push l’image avec deux tags :

mako2727/monapp-backend:latest
mako2727/monapp-backend:<commit-sha>


Objectif : garantir une disponibilité continue de l’API sous forme d’image versionnée.

📊 KPIs SonarCloud — Back
Indicateur	Objectif	Source
Couverture de tests	≥ 80 %	Jacoco XML
Bugs & Vulnérabilités	Niveau A	SonarCloud
Duplications	≤ 3 %	SonarCloud
Code Smells	≤ 15	SonarCloud


🐳 Image Docker — Back
Nom de l’image	Description
mako2727/monapp-backend:latest	Image courante du back-end
mako2727/monapp-backend:<commit-sha>	Version spécifique liée au commit Git


🔑 Secrets GitHub Actions
DOCKERHUB_TOKEN
DOCKERHUB_USERNAME
SONAR_TOKEN_BACK
SONAR_TOKEN_FRONT
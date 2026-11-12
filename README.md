# tp11
# Product API – Projet multi-backend avec Docker

## 1. Présentation du projet

Ce projet consiste à développer et déployer trois API REST permettant de gérer des produits avec trois technologies différentes :

- **Spring Boot** (Java)
- **Express.js** (Node.js)
- **Laravel** (PHP)

Les trois applications utilisent une base de données MySQL et sont conteneurisées avec Docker.

## 2. Architecture du projet

| Service | Technologie | Port local |
|---|---|---|
| Spring API | Spring Boot | 8081 |
| Express API | Express.js | 8082 |
| Laravel API | Laravel + Nginx | 8083 |
| MySQL | MySQL 8 | 3306 |

Les applications communiquent avec MySQL à travers le réseau Docker Compose.

## 3. Dépôts GitHub

- Spring Boot : https://github.com/YASSBELAB/tp3
- Express.js : https://github.com/YASSBELAB/tp6
- Laravel : https://github.com/YASSBELAB/tp8

## 4. Prérequis

Installer les outils suivants :

- Docker Desktop
- Docker Compose
- Git
- Postman
- Newman (pour exécuter les tests automatiquement)

Vérifier les installations :

```bash
docker --version
docker compose version
git --version
newman --version
```

## 5. Build des applications

Depuis le dossier contenant `docker-compose.yml`, exécuter :

```bash
docker compose build
```

Cette commande construit les images Docker des trois backends.

Pour construire et démarrer tous les services :

```bash
docker compose up --build -d
```

## 6. Vérification des conteneurs

Afficher les conteneurs actifs :

```bash
docker compose ps
```

Consulter les logs :

```bash
docker compose logs
```

Consulter les logs d'un service particulier :

```bash
docker compose logs spring-api
docker compose logs express-api
docker compose logs laravel-php
docker compose logs mysql
```

## 7. Tests des API

Les API sont accessibles aux adresses suivantes :

- Spring Boot : http://localhost:8081
- Express.js : http://localhost:8082
- Laravel : http://localhost:8083

Les endpoints principaux permettent de réaliser les opérations CRUD :

| Méthode | Opération |
|---|---|
| GET | Récupérer les produits |
| GET | Récupérer un produit par son ID |
| POST | Ajouter un produit |
| PUT | Modifier un produit |
| DELETE | Supprimer un produit |

Les API utilisent une authentification Bearer Token.

Dans Postman, configurer l'en-tête :

```http
Authorization: Bearer {{API_KEY}}
```

La variable `API_KEY` doit être définie dans l'environnement Postman.

## 8. Tests automatisés avec Newman

Exécuter les collections Postman avec Newman.

Exemple pour Spring Boot :

```bash
newman run "Product API – Spring Boot.postman_collection.json" -e "envtp3.postman_environment.json"
```

Exemple pour Express.js :

```bash
newman run "Product API – Express.postman_collection.json" -e "dev.postman_environment.json"
```

Exemple pour Laravel :

```bash
newman run "Product API – Laravel.postman_collection.json" -e "dev.postman_environment.json"
```

Générer un rapport HTML :

```bash
newman run "Product API – Spring Boot.postman_collection.json" -e "envtp3.postman_environment.json" --reporters cli,html --reporter-html-export report.html
```

La même commande peut être utilisée pour les deux autres backends en adaptant les noms des fichiers.

## 9. Documentation OpenAPI

Chaque backend possède un fichier `openapi.yaml` décrivant :

- Les endpoints disponibles.
- Les méthodes HTTP.
- Les paramètres des requêtes.
- Les formats des réponses.
- Les schémas des produits.
- Le mécanisme d'authentification Bearer.

Les fichiers peuvent être importés dans Postman via **Import → Raw Text** ou en sélectionnant directement les fichiers YAML.

## 10. Déploiement

Pour démarrer les applications :

```bash
docker compose up -d
```

Pour arrêter les applications :

```bash
docker compose down
```

Pour reconstruire les images après modification du code :

```bash
docker compose up --build -d
```

Pour arrêter les services et supprimer également les volumes de données :

```bash
docker compose down -v
```

Attention : cette dernière commande supprime les données persistées dans les volumes Docker.

## 11. Optimisation Docker

Le Dockerfile Laravel utilise une approche multi-stage afin de :

- Séparer l'installation des dépendances de l'image finale.
- Exclure les dépendances de développement.
- Utiliser une image PHP-FPM Alpine.
- Utiliser Nginx pour servir les fichiers publics.
- Réduire la taille des images Docker.

Un fichier `.dockerignore` permet également d'exclure les fichiers inutiles du contexte de build.

## 12. Conclusion

Ce projet permet de comparer trois technologies backend différentes dans une architecture conteneurisée.

Docker Compose facilite le lancement et la gestion des services, tandis que Postman et Newman permettent de tester les API. OpenAPI fournit une documentation standardisée pour les endpoints et leur authentification.



API REST Node.js/Express de gestion de produits avec authentification JWT et documentation interactive Swagger.



<img width="1217" height="656" alt="Screenshot 2026-11-12 010647" src="https://github.com/user-attachments/assets/503f8399-fa70-4072-9227-fa56e20b7dd6" />


API REST Java avec Spring Boot pour la gestion complète des produits (CRUD, recherche et pagination), documentée via Swagger UI.

<img width="1226" height="623" alt="Screenshot 2026-11-12 010909" src="https://github.com/user-attachments/assets/5f9f3ff5-b818-41fb-8e6a-6e29e6bf22ac" />


API RESTful Laravel pour un système e-commerce (produits, catégories, clients, commandes) sécurisée par tokens Sanctum et documentée via Swagger UI


<img width="1259" height="639" alt="Screenshot 2026-11-12 011053" src="https://github.com/user-attachments/assets/dfa06b5c-cc13-4c55-be6f-00bf80c56206" />


Collection Postman organisée pour tester l'API Spring Boot de gestion des produits (endpoints CRUD, recherche et pagination)


<img width="333" height="146" alt="Screenshot 2026-11-12 011134" src="https://github.com/user-attachments/assets/80b8aefe-395d-46d9-ad0c-c567bba98b47" />



Collection Postman de l'API Laravel de gestion des produits, structurée avec des dossiers pour l'authentification et les requêtes produits (liste, création, affichage)


<img width="322" height="137" alt="Screenshot 2026-11-12 011155" src="https://github.com/user-attachments/assets/358f6166-0395-46cd-a045-8a2060898537" />


Collection Postman de l'API Node.js/Express (Product API – Express), organisée en dossiers pour General, Auth et Products.





<img width="335" height="126" alt="Screenshot 2026-11-12 011215" src="https://github.com/user-attachments/assets/bb5448c8-1a50-4e80-bbc6-415f7893643d" />



Liste des environnements de configuration Postman pour les différents projets (avec l'environnement actif tp11 sélectionné).


<img width="325" height="271" alt="Screenshot 2026-11-12 011308" src="https://github.com/user-attachments/assets/a623422f-950a-4d3d-9375-1c2f5485c706" />



Interface de Docker Desktop affichant un conteneur en cours d'exécution nommé tp_docker.   


<img width="1275" height="633" alt="Screenshot 2026-11-12 011334" src="https://github.com/user-attachments/assets/7b5fbb5a-40ca-4d49-be3f-491e9f9e0000" />

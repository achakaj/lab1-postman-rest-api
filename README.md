# Lab 1 : Conception et test d'une API REST avec HTTP et Postman

Cours **Développement Backend avec Java, Node.js et PHP** - Master IAIDDWM, FST Marrakech.
Auteur : Abdellah Achakaj.

## Description

Collection Postman qui teste l'API de démonstration [DummyJSON](https://dummyjson.com) :
requêtes GET / POST / PUT / PATCH / DELETE, authentification par jeton (chaînage login -> `/auth/me`)
et cas d'erreur (400, 401, 404). Chaque requête contient une description et des tests JavaScript
(statut, `Content-Type` JSON, champs du body, temps de réponse < 500 ms).
La collection est exécutable en ligne de commande avec Newman, qui génère un rapport HTML.

## Structure du dépôt

```
lab1-postman-rest-api/
├── postman/
│   ├── lab1-collection.postman_collection.json   # collection (format v2.1)
│   └── lab1-env.postman_environment.json         # variables d'environnement
├── rapport/
│   ├── rapport-lab1.md                           # rapport (source)
│   ├── rapport-lab1.pdf                          # rapport PDF
│   └── captures/                                 # captures d'écran Postman
├── newman/
│   └── newman-report.html                        # rapport d'exécution Newman
├── README.md
└── .gitignore
```

Dossiers de la collection : `01 - GET`, `02 - POST`, `03 - PUT vs PATCH`, `04 - DELETE`,
`05 - Chaînage`, `06 - Erreurs` (17 requêtes). Toutes les URLs utilisent `{{baseUrl}}`.

## Import dans Postman

1. Ouvrir Postman, cliquer sur **Import**.
2. Glisser `postman/lab1-collection.postman_collection.json` et `postman/lab1-env.postman_environment.json`.
3. Sélectionner l'environnement **Lab 1 - Environnement** (en haut à droite).
4. Lancer la collection avec **Run collection** (ou requête par requête, dans l'ordre : le dossier 05 stocke `accessToken` pour `/auth/me`).

Variables d'environnement : `baseUrl`, `productId`, `userId`, `accessToken` (vide au départ), `username`, `password`
(identifiants publics de démonstration de DummyJSON, aucun secret réel).

## Lancement avec Newman

```bash
npm install -g newman newman-reporter-htmlextra

newman run postman/lab1-collection.postman_collection.json \
  -e postman/lab1-env.postman_environment.json \
  -r cli,htmlextra \
  --reporter-htmlextra-export newman/newman-report.html
```

Résultat de référence : 17 requêtes, 78 assertions, 0 échec.

> Le seuil de 500 ms dépend de la latence réseau vers l'API publique : une exécution lente peut
> faire échouer ponctuellement un test de temps de réponse. Relancer dans ce cas.

## Livrables

- `postman/lab1-collection.postman_collection.json` : collection Postman
- `postman/lab1-env.postman_environment.json` : environnement
- `rapport/rapport-lab1.pdf` et `rapport/rapport-lab1.md` : rapport avec captures d'écran Postman (dossier `rapport/captures/`)
- `newman/newman-report.html` : rapport Newman
- `README.md`, `.gitignore`

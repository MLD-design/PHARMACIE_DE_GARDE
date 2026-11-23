# [S0-5] Choix Techniques — Plateforme de Gestion des Pharmacies de Garde

**Auteurs (Binôme XP) :** Mouhamadou Lamine Diouf (Pilote) & Aissatou SOW (Copilote)  
**Projet :** Plateforme de gestion et de recherche des pharmacies de garde  
**Sprint :** Sprint 0 — Conception & Modélisation  

---

## 1. Critères de Décision Technique

Les choix technologiques sont évalués selon cinq critères adaptés au contexte du projet :
* **Légèreté et accessibilité mobile :** Rapidité de chargement sur connexion mobile (3G/4G) pour les citoyens en recherche d'une pharmacie de garde.
* **Fiabilité et sécurité :** Protection des accès professionnels (pharmaciens et administrateurs) et intégrité des plannings de garde.
* **Géolocalisation :** Capacité à rechercher les officines à proximité et à afficher une carte interactive.
* **Testabilité (XP / TDD) :** Facilité d'écriture de tests unitaires et d'intégration automatisés.
* **Maîtrise par l'équipe :** Technologies déjà pratiquées par l'équipe pour limiter les risques techniques dès le Sprint 1.

---

## 2. Choix Techniques Retenus

| Domaine | Options envisagées | Choix retenu | Justification |
| :--- | :--- | :--- | :--- |
| **Frontend** | React (Vite), Vue.js, Angular | **React + Vite + Tailwind CSS** | Bundle léger, réactivité sur mobile et découpage clair en composants réutilisables. |
| **Backend** | Spring Boot, Express.js, Django | **Spring Boot (Java)** | Structure claire, typage fort, sécurité intégrée et écosystème de test mature (JUnit / Mockito). |
| **Base de données** | MySQL, PostgreSQL | **MySQL** | Modèle relationnel adapté aux données structurées (pharmacies, gardes, utilisateurs, zones) et maîtrisé par l'équipe. |
| **Cartographie** | Leaflet + OpenStreetMap, Google Maps | **Leaflet + OpenStreetMap** | Solution gratuite, sans quota payant et légère pour l'affichage de cartes et marqueurs. |
| **Authentification** | JWT, Sessions serveur | **JWT + BCrypt** | Authentification sans état (*stateless*) adaptée aux API REST et au hachage sécurisé des mots de passe. |
| **CI/CD & Conteneurs** | Docker + GitHub Actions | **Docker + GitHub Actions** | Environnement reproductible sur chaque poste et exécution automatique des tests à chaque push. |

---

## 3. Décisions Techniques Clés (ADR)

* **ADR-01 — Authentification par JWT :** Protège les opérations de gestion (création/validation des gardes, mise à jour des officines) tout en laissant la consultation publique libre.
* **ADR-02 — OpenStreetMap / Leaflet :** Évite les coûts d'API cartographique payante tout en couvrant l'affichage des pharmacies et de la position de l'utilisateur.
* **ADR-03 — Gestion des créneaux de garde par dates/heures (`date_debut`, `date_fin`) :** Permet de gérer les gardes de nuit ou de week-end qui s'étendent sur plusieurs jours sans ambiguïté.


# 03 — Architecture & Choix Techniques (PharmaGarde)

Ce dossier regroupe les décisions architecturales et les choix technologiques retenus pour la plateforme de gestion et de recherche des pharmacies de garde (**PharmaGarde**).

---

## Documents disponibles

| Livrable | Fichier | Statut | Description |
| :--- | :--- | :--- | :--- |
| **[S0-5] Choix Techniques** | [`S0-5_architecture_choix_techniques.md`](S0-5_architecture_choix_techniques.md) | Validé (Revue XP) | Justification de la stack technique (React/Vite, Spring Boot, MySQL, Leaflet/OSM, JWT) et décisions d'architecture (ADR). |

---

## Vue d'ensemble de la Stack Technique

* **Frontend :** React + Vite + Tailwind CSS + Leaflet (OpenStreetMap)
* **Backend :** Spring Boot (API RESTful sécurisée)
* **Base de données :** MySQL
* **Sécurité :** Authentification *stateless* via JWT et hachage BCrypt
* **DevOps / CI-CD :** Docker & GitHub Actions

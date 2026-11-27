# Product Backlog, Definition of Done et Stratégie de Tests
**Projet :** Plateforme de gestion des pharmacies de garde  
**Méthodologie :** Scrumban + Extreme Programming (XP)  
**Livrable :** Tâche S0-8 (Sprint 0)  

---

## 1. Product Backlog (MVP)

Le *Product Backlog* recense l'ensemble des fonctionnalités attendues pour la plateforme, priorisées selon la méthode **MoSCoW** et estimées en **Story Points** (suite de Fibonacci).

| ID | Rôle | User Story | Priorité | Estimation | Critères d'acceptation principaux |
| :--- | :--- | :--- | :---: | :---: | :--- |
| **US-01** | Citoyen | En tant que citoyen, je veux rechercher les pharmacies de garde ouvertes autour de ma position ou par quartier/ville afin de trouver rapidement un point de vente accessible. | Must | 5 | - Recherche par géolocalisation ou par zone<br>- Affichage de la liste triée par proximité<br>- Statut « De garde » clairement indiqué |
| **US-02** | Citoyen | En tant que citoyen, je veux visualiser les pharmacies de garde sur une carte interactive et consulter leurs détails (adresse, téléphone, horaires, itinéraire) afin de m'y rendre facilement. | Must | 5 | - Marqueurs distincts sur la carte<br>- Fiche détaillée complète au clic<br>- Bouton d'appel direct et lien vers l'itinéraire |
| **US-03** | Citoyen | En tant que citoyen, je veux signaler une anomalie (pharmacie fermée alors qu'elle est affichée de garde, numéro erroné) afin de maintenir des informations fiables. | Should | 3 | - Formulaire de signalement simple (motif + commentaire)<br>- Enregistrement horodaté en base<br>- Confirmation de prise en compte |
| **US-04** | Pharmacien | En tant que pharmacien, je veux m'authentifier sur mon espace sécurisé afin de gérer les informations de mon officine. | Must | 3 | - Connexion sécurisée (email/mot de passe)<br>- Contrôle d'accès par rôle (`PHARMACIEN`)<br>- Gestion des erreurs d'authentification |
| **US-05** | Pharmacien | En tant que pharmacien, je veux déclarer et mettre à jour les périodes de garde de ma pharmacie (dates, horaires, disponibilité) afin d'informer les citoyens en temps réel. | Must | 5 | - Création, modification et suppression d'un créneau de garde<br>- Vérification de non-chevauchement des dates<br>- Mise à jour immédiate côté citoyen |
| **US-06** | Pharmacien | En tant que pharmacien, je veux mettre à jour la fiche de mon officine (adresse, coordonnées GPS, téléphone, statut d'ouverture) afin de garantir l'exactitude des données. | Should | 3 | - Formulaire d'édition pré-rempli<br>- Validation des champs obligatoires et coordonnées GPS |
| **US-07** | Administrateur | En tant qu'administrateur, je veux valider ou suspendre les comptes pharmacies afin d'éviter toute création de fausse officine sur la plateforme. | Must | 3 | - Liste des inscriptions en attente<br>- Actions d'approbation ou de rejet<br>- Seules les pharmacies validées sont visibles publiquement |
| **US-08** | Administrateur | En tant qu'administrateur, je veux consulter et traiter les signalements envoyés par les citoyens afin de corriger les informations erronées. | Should | 3 | - Tableau de bord des signalements (Nouveau, En cours, Résolu)<br>- Possibilité de masquer temporairement une garde erronée |
| **US-09** | Administrateur | En tant qu'administrateur, je veux importer ou planifier un calendrier officiel des tours de garde afin de faciliter la mise à jour globale. | Could | 5 | - Import structuré (CSV/JSON) ou saisie par lot<br>- Rapport des lignes importées ou en erreur |

---

## 2. Definition of Done (DoD)

Une User Story ou tâche technique est considérée comme **Done** (terminée) uniquement lorsque l'ensemble des conditions suivantes est respecté :

### 2.1. Critères fonctionnels
* **Critères d'acceptation validés :** Toutes les conditions décrites dans l'issue GitHub sont implémentées et vérifiées.
* **Conformité métier et UX :** L'interface respecte les maquettes validées et s'adapte aux écrans mobiles et ordinateurs (responsive).
* **Zéro bug bloquant :** Aucune anomalie critique ou majeure n'est ouverte sur le périmètre de la tâche.

### 2.2. Critères techniques (Pratiques XP)
* **Respect des conventions :** Le code suit les conventions de nommage, de structure et de formatage établies dans le dépôt (`S0-7`).
* **Tests automatisés passants :** Les tests unitaires et d'intégration couvrant la fonctionnalité sont écrits et exécutés avec succès (taux de réussite de 100 %).
* **Pipeline CI au vert :** La compilation, l'analyse statique et les tests passent sans erreur dans GitHub Actions.
* **Revue de code (*Code Review*) :** La Pull Request a été relue et approuvée par au moins un autre membre de l'équipe avant sa fusion (*merge*).

### 2.3. Critères documentaires et gestion de flux (Scrumban)
* **Documentation à jour :** Les diagrammes UML, la documentation d'API ou les guides techniques impactés sont mis à jour dans `/docs`.
* **Traçabilité GitHub :** L'issue correspondante est liée à la Pull Request fusionnée (`Closes #numéro`) et déplacée dans la colonne **Done** du tableau Kanban.

---

## 3. Stratégie de Tests

La qualité logicielle repose sur une validation continue à chaque étape du développement, inspirée de la pyramide des tests et des pratiques d'Extreme Programming.

### 3.1. Niveaux de tests

| Niveau | Objectif | Périmètre couvert | Outils / Méthode | Déclenchement |
| :--- | :--- | :--- | :--- | :--- |
| **Tests unitaires** | Valider la logique métier isolée sans dépendances externes. | Calcul des pharmacies actuellement de garde, calcul de distance géographique, validation des créneaux horaires, contrôle des rôles. | Framework unitaire de la stack (ex. JUnit / Jest / Pytest), approche TDD sur les règles critiques. | En local avant commit et automatiquement dans le pipeline CI. |
| **Tests d'intégration** | Vérifier la communication entre les composants internes et externes. | Endpoints de l'API REST, requêtes et contraintes de la base de données (*Pharmacie*, *Garde*, *Utilisateur*, *Signalement*), appels au service de cartographie. | Tests d'API automatisés avec base de test isolée (vérification des codes HTTP, formats JSON et sécurité JWT/session). | À chaque création ou mise à jour d'une Pull Request via CI. |
| **Tests fonctionnels (E2E)** | Valider les parcours utilisateurs complets de bout en bout. | 1. Recherche et localisation d'une pharmacie de garde (Citoyen)<br>2. Connexion et publication d'une garde (Pharmacien)<br>3. Validation d'un compte et traitement d'un signalement (Admin) | Cahier de recette exécuté sur l'environnement de préproduction + scénarios automatisés sur les flux critiques. | Avant chaque **Sprint Review**. |
| **Tests non fonctionnels** | S'assurer de la sécurité, de la compatibilité et des performances de base. | Protection des routes privées (anti-élévation de privilèges), validation des entrées utilisateurs (XSS/SQLi), affichage mobile/desktop. | Audit manuel des permissions, tests multi-résolutions navigateur. | Lors de la revue de fonctionnalité et avant livraison finale. |

### 3.2. Gestion des anomalies (Workflow Scrumban)
1. **Enregistrement :** Tout défaut détecté est créé sous forme d'issue GitHub avec le label `bug` et une sévérité (`Critique`, `Majeure`, `Mineure`).
2. **Priorisation :** Les anomalies `Critiques` ou `Majeures` sont traitées en priorité avant toute nouvelle tâche, dans le respect de la limite **WIP** du tableau Kanban.
3. **Non-régression :** Chaque correction d'anomalie s'accompagne d'un test automatisé reproduisant le défaut initial afin d'empêcher toute régression future.

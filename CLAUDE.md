# FM22 Role Analyzer — projet d'apprentissage

## Mode de travail (important)
- Objectif : **apprendre Java** et ses fonctionnalités en construisant un vrai projet.
- Je construis pas à pas. Ne m'écris pas le code à ma place.
- Donne-moi l'objectif de l'étape, des indices (classes/méthodes à regarder), puis relis mon code.
- Ne montre une solution complète que si je la demande explicitement.
- Réponses concises et directes, en français.

## Gestion de projet
- Le projet est découpé en **versions** (une par phase), chaque version en **user stories** : voir `docs/BACKLOG.md`.
- Une story = une branche `feature/US-xx-nom`, des commits courts (Conventional Commits : `feat:`, `fix:`, `test:`, `refactor:`, `docs:`, `chore:`), puis une revue avant le merge sur `main`.
- On ne commence pas une story tant que la précédente n'est pas « Done ».
- **Definition of Done** : les critères d'acceptation sont remplis, `mvn test` passe, le code est relu, la branche est mergée, le backlog et la section Avancement sont mis à jour.
- Tests écrits **au fil de l'eau** (dès la première logique testable), pas à la fin.

## Contexte
- Jeu : Football Manager 2022, **en français**. Données d'entrée : export HTML du jeu
  (vue d'effectif ou de recherche → Ctrl+A → Ctrl+P → "page web").
- Je contrôle les colonnes : la vue d'export est **imposée** (liste de colonnes figée et documentée),
  et elle inclut **UID** dès le départ (identité stable du joueur pour les phases suivantes).
- En-têtes en français abrégés (« Acc », « Vit »…) → table de correspondance abréviation → attribut.
- Stack : Java 21, Maven, Jsoup (parsing HTML), Jackson (JSON), JUnit 5.
  Plus tard : JPA/Hibernate (H2 puis PostgreSQL), Spring Boot.

## Architecture (à respecter dès le début, pour migrer vers Spring sans réécriture)
- `model` : Player (distinction joueur de champ / gardien), Role, Duty (enum), Attribute, Slot (postes)
- `io` : lecture de l'export HTML et du fichier des rôles (JSON)
- `scoring` : calculs purs, aucune dépendance à Jsoup ni aux fichiers
- `App` : orchestration uniquement

## Modèle de score
- Un rôle est défini par un couple **(rôle, devoir)**, ex. « Milieu relayeur / Soutien ».
- Chaque couple a des attributs clés et préférables (écran tactique du jeu).
- Score = moyenne pondérée (clés ×3, préférables ×2) + **poids « méta » configurables**
  (ex. Vitesse, Accélération), ramenée sur 100.
- La familiarité au poste n'entre pas dans le score : elle sert de contrainte ou de pénalité au moment de l'affectation du XI.
- v1 : joueurs **parfaitement connus** uniquement (son propre effectif), sans indice de confiance.
  Les plages « 12-15 » (milieu de la plage) et « - » (absent) arrivent avec le recrutement (v2).
- Le fichier des rôles démarre avec environ 5 couples, puis on l'élargit.

## Feuille de route (ordre : v1 → v2 → v3 → v4)
- **v1 — Analyseur de rôles (CLI)** : en cours, détail dans le backlog.
- **v2 — Recrutement Moneyball** : valeur, salaire, âge, plages de scouting, indice qualité/prix,
  postes faibles du XI → recrues. Question ouverte : comment évaluer un jeune sans son potentiel ?
- **v3 — Suivi de progression** : JPA/Hibernate, Snapshot (export + date en jeu saisie), requêtes d'évolution.
- **v4 — Dashboard web** : Spring Boot, API REST, front simple.

## Avancement
- Version : v1
- Story en cours : US-00

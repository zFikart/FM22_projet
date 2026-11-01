# Backlog

Statuts : `TODO` · `EN COURS` · `DONE`

## v1 — Analyseur de rôles (CLI)

**Objectif de la version :** à partir de l'export de mon effectif, l'outil me donne le classement des joueurs pour un rôle, puis le meilleur XI pour ma tactique.

### US-00 — Mise en place du projet · `TODO`
En tant que développeur, je veux un projet Maven versionné, pour travailler proprement dès le départ.
- [ ] Dépôt Git initialisé, `.gitignore` Java/Maven/IDE
- [ ] `pom.xml` Java 21 avec Jsoup, Jackson et JUnit 5
- [ ] Packages `model`, `io`, `scoring`, plus une classe `App`
- [ ] `mvn test` passe (même sans aucun test)
- [ ] `README.md` minimal : ce que fait l'outil, comment le lancer
- [ ] Vue d'export FM documentée dans `docs/EXPORT.md` (liste des colonnes, dont UID)

### US-01 — Lire l'export HTML · `TODO`
En tant qu'utilisateur, je veux donner le chemin d'un export à l'outil, pour qu'il le lise.
- [ ] Le fichier HTML est lu avec Jsoup, et les en-têtes du tableau sont affichés
- [ ] Un message clair s'affiche si le fichier est absent ou ne contient pas de tableau

### US-02 — Transformer les lignes en joueurs · `TODO`
En tant qu'utilisateur, je veux que chaque ligne devienne un joueur, pour pouvoir l'analyser.
- [ ] Table de correspondance entre abréviations FR et attributs
- [ ] `Player` contient l'UID, le nom, la position brute et les attributs ; les gardiens sont distingués des joueurs de champ
- [ ] Une ligne invalide est signalée sans faire planter l'outil
- [ ] Tests : parsing d'une ligne de champ, d'une ligne de gardien, d'une ligne invalide

### US-03 — Charger les rôles · `TODO`
En tant qu'utilisateur, je veux définir les rôles dans un JSON, pour les modifier sans recompiler.
- [ ] `roles.json` : environ 5 couples (rôle, devoir) avec leurs attributs clés et préférables
- [ ] Poids méta configurables dans le JSON
- [ ] Erreur explicite si un attribut inconnu est cité
- [ ] Tests : chargement valide, attribut inconnu

### US-04 — Calculer le score · `TODO`
En tant qu'utilisateur, je veux le score /100 d'un joueur pour un rôle.
- [ ] Calcul de la moyenne pondérée (×3, ×2, plus les poids méta), ramenée sur 100
- [ ] Le package `scoring` ne dépend ni de Jsoup ni des fichiers
- [ ] Tests : cas calculés à la main (joueur à 20 partout = 100, etc.)

### US-05 — Classement en ligne de commande · `TODO`
En tant qu'utilisateur, je veux le top N de mon effectif pour un rôle donné.
- [ ] Commande du type `--export fichier.html --role "Milieu relayeur" --duty SOUTIEN --top 5`
- [ ] Affichage sous forme de tableau lisible (rang, nom, score)
- [ ] Message clair si le rôle ou le devoir est inconnu

### US-06 — Interpréter les positions · `TODO`
En tant qu'utilisateur, je veux que l'outil comprenne « D (DGC), MD, M/MO (G) ».
- [ ] La chaîne de position est transformée en un ensemble de `Slot`
- [ ] Tests sur au moins 6 formats réels tirés de mes exports

### US-07 — Meilleur XI · `TODO`
En tant qu'utilisateur, je veux le meilleur XI pour une tactique, avec un joueur par poste.
- [ ] Tactique décrite en JSON : 11 slots, chacun avec un (rôle, devoir)
- [ ] Affectation optimale par l'algorithme hongrois, avec contrainte ou pénalité si le poste n'est pas familier
- [ ] Tests : petit cas (3×3) vérifiable à la main

## v2 — Recrutement Moneyball
*(stories à écrire au lancement de la version)*

## v3 — Suivi de progression
*(stories à écrire au lancement de la version)*

## v4 — Dashboard web
*(stories à écrire au lancement de la version)*

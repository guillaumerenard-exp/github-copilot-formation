# FlowRange — Waves de référence

> Document formateur — résultat attendu de l'exercice "Specs to Waves"

---

## Rappel : qu'est-ce qu'une Wave ?

Une **wave** est un mini sprint autonome et livrable. Elle regroupe un ensemble cohérent de features qui forment une valeur utilisateur complète. À la fin de chaque wave, l'application doit être **déployable et démo-able**.

Règles d'une bonne wave :
- Livrable seule (pas de dépendance sur une wave future)
- Visuellement perceptible par un utilisateur final
- Réalisable en 2-4h de vibe coding
- Nominée avec un nom évocateur, pas juste un numéro

---

## Wave 1 — "The Board" *(démo live, ~30 min)*

**Objectif** : Un utilisateur peut créer des tâches et les organiser visuellement sur un kanban.

### Features incluses
- Affichage d'un board kanban avec 3 colonnes fixes : **To Do**, **In Progress**, **Done**
- Création d'une tâche (titre, description optionnelle, couleur/priorité)
- Affichage des tâches sous forme de cartes dans leur colonne
- **Drag & drop** d'une carte entre les colonnes
- Suppression d'une tâche
- Persistence des données (in-memory ou SQLite selon le temps)

### Ce qui est explicitement hors scope
- Assignation à un utilisateur
- Dates d'échéance
- Multiple boards / projets
- Authentification

### Stack technique
- **Backend** : C# Minimal API — endpoints REST (`GET /tasks`, `POST /tasks`, `PATCH /tasks/{id}`, `DELETE /tasks/{id}`)
- **Frontend** : Vue.js 3 (Composition API) — composant `KanbanBoard`, `KanbanColumn`, `TaskCard`
- **Drag & drop** : `vue-draggable-plus` ou native HTML5 DnD

### Résultat attendu en fin de Wave 1
Un board kanban fonctionnel, coloré, avec drag & drop. Visuellement proche d'un Trello simplifié.

---

## Wave 2 — "The Dashboard" *(live si temps — sinon participant)*

**Objectif** : Un utilisateur peut avoir une vue synthétique de l'état de son projet.

### Features incluses
- Page dashboard avec compteurs par statut (nb de tâches To Do / In Progress / Done)
- Graphique de répartition (donut chart ou bar chart)
- Liste des tâches récemment modifiées
- Temps total estimé vs temps passé (si Wave 3 faite) OU champs "estimation en heures" sur chaque tâche

### Ce qui est hors scope
- Filtres par date ou par utilisateur
- Export PDF/CSV
- Comparaison entre projets

### Stack technique
- **Backend** : endpoint `GET /dashboard/stats` qui agrège les données
- **Frontend** : composant `DashboardView` avec `Chart.js` ou `vue-chartjs`

---

## Wave 3 — "The Timer" *(participants autonomes)*

**Objectif** : Un utilisateur peut mesurer le temps passé sur chaque tâche.

### Features incluses
- Bouton Start/Stop sur chaque carte
- Affichage du temps écoulé en temps réel (format HH:MM:SS)
- Historique des sessions de travail par tâche
- Temps total cumulé visible sur la carte

### Stack technique
- **Backend** : `POST /tasks/{id}/timer/start`, `POST /tasks/{id}/timer/stop`, `GET /tasks/{id}/sessions`
- **Frontend** : composant `TimerButton` avec un interval JS

---

## Wave 4 — "The Team" *(participants autonomes)*

**Objectif** : Gérer une équipe et assigner les tâches.

### Features incluses
- CRUD membres (nom, avatar/initiales, couleur)
- Assignation d'une tâche à un ou plusieurs membres
- Filtre du board par membre assigné
- Vue "par membre" sur le dashboard

---

## Wave 5 — "The Projects" *(participants autonomes)*

**Objectif** : Gérer plusieurs projets distincts avec leur propre board.

### Features incluses
- CRUD projets (nom, description, couleur, dates)
- Navigation entre projets
- Boards et timers isolés par projet
- Dashboard global multi-projets

---

## Prompts de challenge pour "Specs to Waves"

Ces prompts sont à utiliser pendant l'exercice pour pousser les participants à approfondir leurs specs avec Copilot :

```
1. "Quels cas limites as-tu ignorés dans ces specs ? Liste-les et propose comment les gérer."

2. "Quelles ambiguïtés vois-tu dans cette wave ? Pose-moi 5 questions pour clarifier."

3. "En tant que développeur qui doit implémenter cette wave, quelles informations te manquent ?"

4. "Identifie les dépendances techniques entre les waves. Y a-t-il des risques d'ordre ?"

5. "Cette wave est-elle trop grosse pour 2-4h de développement ? Comment la découper ?"

6. "Génère les critères d'acceptation (Given/When/Then) pour chaque feature de cette wave."
```

---

## Ordre de dépendance des Waves

```
Wave 1 (Board)
    └── Wave 2 (Dashboard)     ← nécessite des données de Wave 1
    └── Wave 3 (Timer)         ← s'ajoute sur les cartes de Wave 1
        └── Wave 2 (enrichi)   ← si Wave 3 faite, le dashboard est plus riche
Wave 4 (Team)                  ← indépendante, peut se faire après Wave 1
Wave 5 (Projects)              ← regroupe tout, à faire en dernier
```

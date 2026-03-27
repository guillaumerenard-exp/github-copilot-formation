# FlowRange — Guide animateur

> Document interne — ne pas distribuer aux participants.

---

## Vue d'ensemble de la session (2h)

| Segment | Durée | Activité | Fichier/Ressource |
|---|---|---|---|
| Intro | 5-10 min | Objectif de la session, annonce du sujet FlowRange | Slides intro |
| GitHub Copilot, c'est quoi ? | 5-10 min | Présentation des modes : Chat, Edit, Agent | Slides Copilot |
| Présentation du pitch | 5-10 min | Distribuer `pitch.md`, lecture commentée | `pitch.md` |
| Specs to Waves | 15 min | Exercice avec Copilot : pitch → specs → waves | `waves-reference.md` |
| Specs techniques | 15 min | Configurer `copilot-instructions.md` | `copilot-instructions.md` |
| Implémentation Wave 1 | 30 min | Live coding : Kanban board | Live + branches fallback |
| Tests & améliorations | 30 min | Participants continuent, formateur démo Wave 2 | Libre |
| **TOTAL** | **~2h** | | |

---

## Segment 1 — Introduction (5-10 min)

**Objectif** : Poser le contexte, créer l'envie.

**Script** :
- Annoncer que d'ici 2h, on va construire ensemble une application web complète de gestion de projet
- Montrer le pitch de FlowRange — *"C'est le brief que vous allez donner à GitHub Copilot"*
- L'objectif n'est pas d'apprendre à coder, c'est d'apprendre à **déléguer le code à l'IA**

**Point d'accroche** : *"Qui utilise Trello ? Qui utilise Toggl ? On va en construire une version en 30 minutes."*

---

## Segment 2 — GitHub Copilot, c'est quoi ? (5-10 min)

**Points clés à couvrir** :

1. **Copilot inline** : complétion de code dans l'éditeur — `Tab` pour accepter, `Alt+]` pour voir d'autres suggestions
2. **Copilot Chat** (`Ctrl+Alt+I`) : conversation libre, poser des questions, expliquer du code
3. **Copilot Edit** : modifier plusieurs fichiers en une instruction
4. **Copilot Agent** (`#agent`) : mode autonome qui lit le projet et enchaîne les actions — c'est ça le vibe coding

**Raccourcis à afficher** :
```
Ctrl+I           → Copilot inline edit (dans l'éditeur)
Ctrl+Alt+I       → Ouvrir Copilot Chat
Tab              → Accepter suggestion inline
Esc              → Refuser suggestion inline
Alt + ]          → Suggestion suivante
```

**Ne pas s'attarder** — juste planter les bases. Les participants vont expérimenter immédiatement.

---

## Segment 3 — Présentation du Pitch (5-10 min)

**Action** : Distribuez (ou partagez à l'écran) le fichier `pitch.md`.

**Lecture commentée** — s'arrêter sur :
- *"Ce que FlowRange permet"* → pointer les analogies avec Trello / Monday / Toggl
- *"Ce que FlowRange n'est PAS"* → insister : délimiter le scope c'est aussi important que définir les features
- *"À vous de jouer"* → transition vers l'exercice Specs to Waves

**Question à poser à la salle** : *"Qu'est-ce qui manque dans ce pitch ? Qu'est-ce que vous voudriez savoir avant de coder ?"* — laisser 2 min de réponses, puis dire *"C'est exactement ce qu'on va demander à Copilot."*

---

## Segment 4 — Specs to Waves (15 min)

**Exercice participatif** : chaque participant sur son poste avec Copilot ouvert.

### Instructions à donner

1. Ouvrir VS Code, créer un fichier `specs.md`
2. Coller le contenu du pitch dedans
3. Dans Copilot Chat (mode Agent), saisir :
   ```
   Tu es un product owner expert. À partir de ce pitch, génère des specs fonctionnelles détaillées 
   pour FlowRange. Pour chaque feature, décris le comportement attendu, les cas nominaux et les 
   cas limites. Puis découpe ces specs en waves (mini sprints autonomes et livrables).
   ```
4. Lire le résultat, puis poser l'un des **prompts de challenge** de `waves-reference.md`

### Rôle de l'animateur pendant l'exercice
- Circuler dans la salle
- Pointer les specs trop vagues → *"Demande à Copilot de clarifier ça"*
- Pointer les waves trop grosses → *"Tu penses vraiment qu'on peut faire ça en 2h ?"*
- **Ne pas corriger** les specs — laisser Copilot travailler

### Débriefing (3 min)
- Demander à 1-2 participants de montrer leur résultat
- Comparer avec la référence dans `waves-reference.md`
- Expliquer qu'il n'y a pas de bonne réponse — l'exercice montre que **Copilot peut être votre PO**

---

## Segment 5 — Specs techniques (15 min)

**Objectif** : montrer comment guider Copilot sur les décisions d'architecture via `copilot-instructions.md`.

### Déroulé

1. Ouvrir `copilot-instructions.md` dans VS Code — **lire ensemble** les sections principales
2. Expliquer les 3 types de règles :
   - **Ce qu'on veut** (stack, conventions, nommage)
   - **Ce qu'on ne veut pas** (pas d'auth, pas de librairies exotiques)
   - **Le contexte** (structure de dossiers, modèle de données)
3. Demo : modifier une règle en direct et montrer que Copilot s'adapte instantanément

**Message clé** : *"Ce fichier c'est votre contrat avec l'IA. Plus il est précis, moins vous passerez de temps à corriger le code généré."*

**Point d'attention** : certains seniors vont vouloir débattre de l'architecture. Cadrer : *"Pour ce projet de démo, on a choisi la simplicité. En vrai projet, vous adaptez ces règles à vos standards."*

---

## Segment 6 — Implémentation Wave 1 (30 min)

**Mode** : live coding, tous suivent sur leur poste.

### Séquence recommandée

**T+00 — Scaffolding (5 min)**
```bash
# Backend
dotnet new web -n FlowRange.Api
cd FlowRange.Api

# Frontend
npm create vue@latest flowrange-frontend
# Choisir : TypeScript ✓, Vue Router ✓, Pinia ✓
```

**T+05 — Prompt de génération du backend (8 min)**

Dans Copilot Chat (mode Agent), depuis le dossier `FlowRange.Api` :
```
En suivant les instructions de copilot-instructions.md, génère l'implémentation complète 
de la Wave 1 côté backend :
- Le modèle Task avec les propriétés définies dans les specs
- Le FlowRangeDbContext en InMemory
- Les endpoints Minimal API : GET /tasks, POST /tasks, PATCH /tasks/{id}/status, DELETE /tasks/{id}
- La configuration CORS pour localhost:5173
- Des données de seed pour avoir 3-4 tâches au démarrage
```

*Moment WOW #1 : Copilot génère tous les fichiers en une fois.*

**T+13 — Prompt de génération du frontend (10 min)**
```
En suivant les instructions de copilot-instructions.md, génère les composants Vue.js pour 
la Wave 1 :
- KanbanBoard.vue : affiche 3 colonnes (To Do, In Progress, Done)
- KanbanColumn.vue : affiche les cartes de son statut, accepte le drop
- TaskCard.vue : affiche titre, priorité, bouton supprimer
- Implémente le drag & drop natif HTML5 entre les colonnes
- Le store Pinia pour gérer l'état des tâches
- Les appels API dans services/api.ts
```

*Moment WOW #2 : Le board kanban apparaît en quelques secondes.*

**T+23 — Corrections et ajustements (5 min)**

Laisser les participants tester sur leurs postes. Points courants à corriger :
- CORS non configuré → montrer comment demander à Copilot de corriger
- API URL incorrecte → adapter `api.ts`

*Moment WOW #3 : "Copilot, ce composant ne se met pas à jour après un drag & drop, corrige ça" → fix en 10 secondes.*

**T+28 — Demo finale (2 min)**

Montrer l'app qui tourne : créer une tâche, la déplacer entre les colonnes, la supprimer.

### Branches de fallback (si ça plante)

Préparer des branches git avec le code à chaque étape :
```
git checkout wave1/step1-backend    # Backend seul
git checkout wave1/step2-frontend   # Frontend seul
git checkout wave1/complete         # Wave 1 complète
```

---

## Segment 7 — Tests & améliorations (30 min)

**Mode** : participants en autonomie, animateur disponible.

### Activités suggérées pour les participants

**Niveau standard** :
- Ajouter un champ "priorité" sur les cartes avec un indicateur coloré
- Ajouter un formulaire de création de tâche plus complet
- Améliorer le style (couleurs, animations)

**Pour les seniors (challenge)** :
- *"Refactorise le store Pinia avec Copilot pour gérer les erreurs réseau"*
- *"Commence la Wave 2 : génère les stats pour le dashboard"*
- *"Demande à Copilot d'ajouter de la validation côté backend et côté formulaire"*

### Si le temps le permet
Démarrer la Wave 2 ensemble : dashboard avec compteurs par statut.

---

## Points de vigilance

| Risque | Signal | Action |
|---|---|---|
| Participant bloqué sur le setup | Pas de réponse Copilot | Vérifier licence, passer au poste du formateur |
| Segment Specs to Waves trop long | +5 min après T+15 | Couper le débriefing, passer directement aux specs techniques |
| Backend ne démarre pas | Erreur `dotnet run` | Utiliser branche fallback `wave1/step1-backend` |
| Frontend ne se connecte pas | Erreur CORS ou 404 | Montrer la correction CORS en live — c'est pédagogique |
| Participants avancent trop vite | Ils ont fini Wave 1 avant T+30 | Proposer le challenge senior ci-dessus |

---

## Timing serré ? Coupes possibles

Si en retard de plus de 10 min :
1. Réduire "Specs to Waves" à 10 min (skip le débriefing)
2. Faire le scaffolding en avance (repo déjà initialisé)
3. Réduire "Specs techniques" à 5 min (lecture rapide sans démo)

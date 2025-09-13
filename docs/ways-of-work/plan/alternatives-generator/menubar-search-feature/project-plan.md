# Plan de projet — AltGenie : Menubar Search Feature

## 1. Vue d'ensemble du projet

Feature Summary

L'initiative "Menubar Search Feature" (AltGenie) fournit une interface macOS discrète dans la barre des menus qui permet à l'utilisateur de rechercher rapidement des alternatives à une application/service/site. Le résultat est une liste structurée d'alternatives (nom, description courte, URL) générée par un service backend qui interroge un modèle IA.

Business value

- Réduire le temps nécessaire pour découvrir des outils alternatifs.
- Augmenter l'engagement des utilisateurs macOS en proposant une expérience native et non intrusive.
- Permettre des choix plus éclairés (coût, vie privée, open-source).

Success criteria (KPI)

- Temps de réponse perçu < 5s pour 90% des requêtes.
- Taux d'ouverture des URLs proposées > 20% sur résultats affichés.
- Pourcentage d'utilisateurs satisfaits (NPS léger) > 70% lors du test utilisateur initial.
- Fiabilité : <1% de plantages liés au flux de recherche.

Key milestones (sans dates)

- M0: Repository + CI initialisés
- M1: Menubar icon et popover UI basique
- M2: Intégration backend IA (endpoint /alternatives)
- M3: Affichage des résultats + interactions (ouvrir URL, copier)
- M4: Tests unitaires & widget tests
- M5: Packaging macOS & docs de déploiement

Risk assessment

- Dépendance critique à l'API IA (coût, latence, disponibilité). Mitigation : caching, fallback message, quota/rate-limiting côté backend.
- Exactitude des URLs renvoyées par l'IA. Mitigation : validation côté backend (optionnel : enrichment via SerpAPI).
- Comportement natif macOS (permissions, positionnement du popover). Mitigation : tests sur macOS ciblés, platform-channel si nécessaire.
- Confidentialité des requêtes. Mitigation : ne pas stocker PII, chiffrer en transit, stocker clés côté backend.

## 2. Hiérarchie des éléments de travail

```mermaid
graph TD
  A[Epic: AltGenie (Alternatives Generator)] --> B[Feature: Menubar Search]
  B --> C[Story 1: UI - Menubar icon & popover]
  B --> D[Story 2: UX - Search input & loading states]
  B --> E[Enabler 1: Backend API /alternatives]
  B --> F[Enabler 2: AI prompt engineering & parsing]

  C --> G[Task: Add system_tray / menubar integration]
  C --> H[Task: Create popover layout (macos_ui)]
  C --> I[Test: UI snapshots (light/dark)]

  D --> J[Task: Implement input handling & validation]
  D --> K[Task: Loading indicator & empty/error states]
  D --> L[Test: Widget tests for states]

  E --> M[Task: FastAPI endpoint + caching]
  E --> N[Task: Secrets management + rate limiting]

  F --> O[Task: Prompt templates + response parser]
  F --> P[Task: URL validation / optional search enrichment]
```

## 3. Détail des issues GitHub (templates adaptés)

### Epic issue (exemple)

Titre: Epic: AltGenie — Alternatives Generator

Corps (résumé):
- But: Permettre aux utilisateurs macOS de découvrir rapidement des alternatives.
- Success metrics: (liste KPI ci-dessus)
- Acceptance criteria:
  - [ ] Menubar app montrée et popover fonctionnel
  - [ ] Backend /alternatives répond avec format structuré JSON
  - [ ] Résultats affichés et interaction URL/copie fonctionnelles

Labels recommandés: `epic`, `priority-high`, `value-high`

---

### Feature issue (exemple)

Titre: Feature: Menubar Search

Corps (résumé):
- Description: Interface menubar + popover qui permet de lancer une requête et voir des alternatives.
- User stories:
  - [ ] #<story-UI> - UI - Menubar icon & popover
  - [ ] #<story-UX> - UX - Search input & loading states
- Technical enablers:
  - [ ] #<enabler-backend> - Backend API /alternatives
  - [ ] #<enabler-prompt> - Prompt engineering & parser
- Acceptance criteria:
  - [ ] Le popover se positionne sous l'icône
  - [ ] Les résultats contiennent `name`, `description`, `url` et s'ouvrent dans le navigateur

Labels recommandés: `feature`, `priority-high`, `frontend`, `backend`

---

### User story example

Titre: User Story: UI - Menubar icon & popover

Story statement:
As a macOS user, I want to open AltGenie from the menubar so I can search alternatives without leaving my workflow.

Acceptance criteria:
- [ ] L'icône apparaît dans la menubar
- [ ] Cliquer bascule le popover
- [ ] Le popover se ferme au clic extérieur ou Esc

Technical tasks:
- [ ] Add `system_tray` integration
- [ ] Build popover widget with `macos_ui`

Tests:
- [ ] Snapshot tests light/dark

## 4. Priorisation & estimation

Priority / Value matrix (recommandée)

- P0: blocking (ex: backend endpoint ou secrets manquants)
- P1: core user-facing (menubar UI, search mechanics)
- P2: important non-blocking (caching, enrichment)
- P3: nice-to-have (analytics, telemetry)

Estimation guidelines

- Story points: 1/2/3/5/8 (Fibonacci)
- T-shirt for feature: S/M (selon découpage)

## 5. Plan de sprints (template)

Sprint length: 2 semaines (recommandé)

Sprint 1 (exemple)
- Objectif: Mener à bien M1 + M2 (menubar + backend minimal)
- Stories candidates:
  - UI - Menubar icon & popover (3 pts)
  - Backend /alternatives (5 pts)
  - Input handling & loading (2 pts)
- Buffer: 20% pour bugs

## 6. Configuration du board GitHub (recommandé)

Colonnes: Backlog, Sprint Ready, In Progress, In Review, Testing, Done
Champs personnalisés: Priority (P0..P3), Value (High/Medium/Low), Component (Frontend/Backend), Estimate, Sprint

## 7. Automatisation proposition (workflow GitHub Actions)

- Workflow `create-feature-issues.yml` (dispatch manuel) qui prend `feature_name` et `epic_issue` et crée un ticket Feature lié à l'Epic. (Implémentation recommandée via `actions/github-script`)

## 8. Annexes & références

Principaux fichiers sources (spécs consultées):
- `Specs/PRD.md`
- `Specs/Architecture.md`
- `Specs/Design_Prompt.md`
- `Specs/Dev_Plan.md`

---

## Notes finales

Fichier généré automatiquement à partir des spécifications PRD/Architecture/Design/Dev_Plan. Prochaine étape recommandée: créer l'Epic GitHub correspondant et lancer le workflow d'automatisation (ou me dire si vous voulez que je le crée pour vous).
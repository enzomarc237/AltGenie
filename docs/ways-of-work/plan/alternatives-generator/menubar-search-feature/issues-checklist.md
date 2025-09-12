# Issues Checklist — AltGenie : Menubar Search Feature

Cette checklist suit la structure recommandée par le prompt de planification et facilite la création d'issues GitHub complètes et traçables.

## Pré-création (conditions préalables)

- [ ] PRD, Architecture, Design Prompt et Dev Plan disponibles (vérifié)
- [ ] Epic GitHub créé pour "AltGenie" (ou planifier sa création)
- [ ] Project board et champs personnalisés configurés (Priority, Value, Component, Estimate)
- [ ] Équipe et capacité évaluées pour le sprint initial

## Epic level

- [ ] Créer l'issue Epic: `Epic: AltGenie — Alternatives Generator`
  - Inclure description, success metrics, acceptance criteria
  - Appliquer labels: `epic`, `priority-high`, `value-high`
  - Assigner milestone (release cible)
  - Lier au project board

## Feature level — `Feature: Menubar Search`

- [ ] Créer l'issue Feature
  - Description courte + user stories list
  - Lier à l'Epic
  - Estimer en t-shirt size
  - Labels: `feature`, `frontend`, `backend`, `priority-high`

## Stories & Enablers (à créer pour la Feature)

UI / UX

- [ ] Story: UI - Menubar icon & popover
  - Tasks:
    - [ ] `system_tray` integration
    - [ ] Popover widget (`macos_ui`) implementation
    - [ ] Snapshot tests (light/dark)

- [ ] Story: UX - Search input & states
  - Tasks:
    - [ ] Input validation (no empty queries)
    - [ ] Loading indicator & message
    - [ ] Empty / error state design & actions

Backend / AI

- [ ] Enabler: Backend API `/alternatives`
  - Tasks:
    - [ ] FastAPI endpoint POST /alternatives
    - [ ] Secrets management (env, secrets manager)
    - [ ] Rate limiting and basic abuse protection
    - [ ] Caching strategy (Redis or DB)

- [ ] Enabler: Prompt engineering & parser
  - Tasks:
    - [ ] Prompt templates for structured JSON output
    - [ ] Parser resilient aux variations (fallbacks)
    - [ ] URL validation + optional enrichment (SerpAPI)

Testing

- [ ] Tests: Unit tests for `AiService.fetchAlternatives` (success, parse error, network failure)
- [ ] Tests: Widget tests for AlternativesGeneratorView (loading/success/error)
- [ ] E2E: Verify click-to-open-URL behaviour on macOS runner (manual or automated)

## Acceptance criteria per story

- [ ] Chaque story contient des critères d'acceptation clairs et testables
- [ ] Chaque story référence les tasks techniques et tests associés
- [ ] Étiquette `Definition of Done` documentée (tests verts, revue approuvée, docs mises à jour)

## Dépendances & ordre recommandé

1. Backend `/alternatives` (Enabler) —> nécessaire pour tester le flux complet
2. UI Popover + Input (Story) —> permet de déclencher requêtes locales/mock
3. Prompt engineering & parser (Enabler) —> améliore qualité des résultats
4. Tests unitaires & widget tests —> valider fiabilité

## Labels recommandés (liste rapide)

- `epic`, `feature`, `user-story`, `enabler`, `task`, `test`
- `priority-critical`, `priority-high`, `priority-medium`, `priority-low`
- `value-high`, `value-medium`, `value-low`
- `component-frontend`, `component-backend`, `component-infra`, `component-testing`

## Checklist de fermeture d'une Feature

- [ ] Tous les user stories associés sont `Done`
- [ ] Tests unitaires & widget tests passés
- [ ] Intégration backend vérifiée en staging
- [ ] Documentation (README / project-plan) mise à jour
- [ ] Release notes prêtes / Milestone mise à jour

## Suggestions pour automatisation (optionnel)

- Utiliser un workflow `workflow_dispatch` pour créer les issues Feature/Stories automatiquement à partir de la `project-plan.md` (inputs: `feature_name`, `epic_issue`).
- Ajouter une étape `actions/github-script` qui parse un petit JSON ou frontmatter dans `project-plan.md` pour générer issues préremplies.

---

Faites-moi savoir si vous voulez que je :
- crée directement l'Epic et les issues dans ce dépôt (je peux générer un script ou un workflow GH Actions),
- ajoute le workflow d'automatisation pour la création d'issues,
- ou que j'ajuste les templates (langue, labels, fields) selon vos conventions.

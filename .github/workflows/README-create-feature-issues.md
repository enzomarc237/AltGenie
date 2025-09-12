# Create Feature & Stories Workflow — Guide d'utilisation

Ce document explique comment utiliser le workflow GitHub Actions `create-feature-issues.yml` (présent dans `.github/workflows`) pour créer automatiquement une issue Feature et des issues enfants (user stories, enablers) liées.

## But

Permettre à un responsable produit ou chef de projet de créer rapidement une issue Feature pré-remplie et quatre issues enfants recommandées (UI, UX, Backend, Prompt) à partir d'un dispatch manuel.

## Entrées du workflow

- `feature_name` (required) : Titre de la Feature (ex. "Menubar Search").
- `epic_issue` (required) : Numéro de l'issue Epic parent (sans le #). Ex : `12`.
- `feature_description` (optional) : Brève description de la feature.
- `labels` (optional) : Labels à appliquer aux issues créées (séparés par des virgules). Ex : `feature,frontend,priority-high`.

## Permissions nécessaires

Le workflow utilise le token GitHub fourni par la plateforme (`GITHUB_TOKEN`) avec la permission `issues: write` définie dans le fichier workflow. Assurez-vous dans les paramètres du repo que :

- Actions a l'autorisation d'utiliser `GITHUB_TOKEN` avec accès en écriture aux issues.

Si vous déclenchez le workflow depuis la CLI (`gh`), la CLI utilisera vos propres identifiants GitHub (votre token personnel). Dans ce cas, assurez-vous que ce compte a les droits pour créer des issues.

## Déclencher depuis l'interface GitHub (UI)

1. Aller sur l'onglet `Actions` du dépôt.
2. Dans la liste des workflows, sélectionner `Create Feature & Stories Issues`.
3. Cliquer sur `Run workflow`.
4. Remplir les champs `feature_name` et `epic_issue` (les autres sont optionnels).
5. Cliquer sur `Run workflow` pour lancer.

Après exécution, ouvrez les logs du job `Create Feature and Child Issues` pour voir les numéros des issues créées (ils sont affichés dans la sortie du script).

## Déclencher depuis la CLI GitHub (optionnel)

Exemple avec la GitHub CLI `gh` :

```bash
gh workflow run create-feature-issues.yml \
  -f feature_name="Menubar Search" \
  -f epic_issue="12" \
  -f feature_description="Popover menubar UI + search to get AI-generated alternatives" \
  -f labels="feature,frontend,priority-high"
```

Note : la commande ci-dessus utilise votre session `gh` (vos identifiants) pour déclencher le workflow.

## Résultats et suivi

- Le workflow crée une issue Feature et quatre issues enfants (UI, UX, Backend, Prompt) par défaut.
- Les numéros créés sont imprimés dans les logs du job. Le workflow définit aussi des outputs `feature_issue` et `created_issues` (tableau JSON) si vous souhaitez chaîner d'autres workflows.

## Personnalisation

- Vous pouvez modifier la liste des issues enfants et leurs templates dans le fichier `.github/workflows/create-feature-issues.yml`.
- Pour changer les labels et conventions, éditez la variable `labels` passée en entrée ou adaptez les labels par défaut dans le script.

## Sécurité & bonnes pratiques

- Évitez d'envoyer des secrets sensibles comme corps d'issue. Le workflow n'utilise pas d'API keys externes.
- Si vous préférez que la création d'issues soit limitée, restreignez l'accès à l'exécution du workflow aux membres de l'équipe via les règles du repo.

---

Si vous voulez, je peux :

- ajouter un petit script `scripts/generate_issues.py` pour personnaliser plus finement le contenu avant création,
- ou créer une version qui lit un frontmatter YAML/JSON dans `project-plan.md` pour générer issues plus détaillées.

Indiquez votre préférence et je l'ajoute.

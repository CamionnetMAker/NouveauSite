# Camion Net — Preview v2 (GitHub Pages)

Preview publique du site Camion Net v2 avant intégration dans Wix.

**URL en ligne :** https://camionnetmaker.github.io/lavagecamions-preview/

## Structure

- 28 pages HTML organisées en dossiers selon les URLs Wix cibles.
- Chaque lien interne pointe vers les slugs locaux pour navigation fluide dans la preview.
- Les liens "Espace membres" et "Réservation Rungis" (booking-calendar) pointent vers le site live (Wix actuel) — non rejoués dans la preview.

## Comment déployer

1. Créer un nouveau repo GitHub nommé **`lavagecamions-preview`** (ou adapter `REPO_PREFIX` dans `build_github_preview.py`).
2. Pousser ce dossier à la racine du repo.
3. Settings -> Pages -> Deploy from branch -> `main` / root.
4. Attendre 1–2 minutes. Le site est accessible à https://<ton-user>.github.io/lavagecamions-preview/

## Regénérer

Depuis le dossier parent (qui contient `pages_wix/` et `build_github_preview.py`) :

```
python3 build_github_preview.py
```

Pour changer l'URL de déploiement, modifier `REPO_PREFIX` en tête du script.

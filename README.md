# Camion Net — Site preview v2 sur GitHub Pages

**Objectif :** parcourir le site Camion Net v2 intégralement avant de déployer dans Wix.

**URL de preview après déploiement :**
https://camionnetmaker.github.io/NouveauSite/

---

## 1. Déploiement GitHub Pages

### Étape 1 — créer le repo

1. Aller sur https://github.com/new (connecté en tant que **CamionnetMAker**).
2. Repository name : **`NouveauSite`** (respecter la casse exacte).
3. Public (GitHub Pages gratuit ne marche qu'en public).
4. Ne pas cocher "Add README".
5. Create repository.

### Étape 2 — pousser le contenu

**Méthode A — interface web GitHub (sans ligne de commande) :**

1. Dézipper `camionnet-github-preview.zip` localement.
2. Sur la page du repo vide GitHub, cliquer "uploading an existing file".
3. Glisser-déposer **tout le contenu dézippé** (pas le dossier parent, son contenu direct : `index.html`, `404.html`, `robots.txt`, `README.md`, et les 27 sous-dossiers).
4. Commit message : `Initial preview site`.
5. Commit changes.

**Méthode B — en ligne de commande :**

```bash
unzip camionnet-github-preview.zip -d NouveauSite
cd NouveauSite
git init
git add -A
git commit -m "Initial preview site"
git branch -M main
git remote add origin https://github.com/CamionnetMAker/NouveauSite.git
git push -u origin main
```

### Étape 3 — activer Pages

1. Sur le repo : **Settings** → **Pages** (menu de gauche).
2. Source : **Deploy from a branch**.
3. Branch : **main** / **/ (root)** → Save.
4. Attendre 1 à 2 minutes.
5. La bannière affiche : "Your site is live at https://camionnetmaker.github.io/NouveauSite/".

### Étape 4 — tester

Ouvrir https://camionnetmaker.github.io/NouveauSite/ et vérifier :
- L'accueil s'affiche correctement.
- Le menu fonctionne (cliquer "Services → Centre Rungis" → charge la page Rungis locale de la preview).
- Les 28 pages sont accessibles en naviguant via le menu.
- Les boutons "Espace membres" et "Réservation Rungis" ouvrent le site Wix live (comportement voulu).

---

## 2. Structure du dossier

Chaque URL Wix cible est reproduite en dossier local avec un `index.html` dedans. 28 pages au total :

- `index.html` (accueil, à la racine)
- 27 sous-dossiers, un par page cible (ex : `lavage-camionnette/index.html`, accessible à `.../NouveauSite/lavage-camionnette/`)
- `404.html` (page d'erreur, redirige vers l'accueil)
- `robots.txt` (bloque l'indexation Google pour éviter tout duplicate content avec le site Wix de production)

---

## 3. Différences vs. version Wix finale

| Élément | Version GitHub Pages (preview) | Version Wix (production) |
|---------|--------------------------------|--------------------------|
| Liens internes | Chemins locaux (`/NouveauSite/…`) | URLs absolues (`https://www.lavagecamions.com/…`) |
| Structure | Un dossier par page, `index.html` dedans | Un fichier HTML collé par page dans un composant Wix |
| Liens externes (espace membres, booking-calendar) | Pointent vers le site Wix live | Identiques |

C'est la version Wix (ZIP `camionnet-wix-v2-integration.zip`) qui doit être déployée en production. Cette preview sert uniquement à **valider le rendu** avant intégration.

---

## 4. Indexation Google

Le fichier `robots.txt` inclut la directive suivante, qui empêche Google d'indexer la preview :

```
User-agent: *
Disallow: /
```

Aucun risque de duplicate content avec le site Wix de production.

---

## 5. Régénérer avec un autre prefix

Si tu renommes le repo, relancer le build avec le nouveau prefix :

```bash
python3 build_github_preview.py /NouveauNom
```

Le script est dans `pages_wix/_source/` du ZIP Wix, ou dans ce dossier si tu l'as gardé.

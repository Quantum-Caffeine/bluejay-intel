# BlueJay Intel — Site vitrine

Page statique unique (HTML + CSS + un peu de JS), **aucune dépendance**, prête à publier.

## Fichiers

| Fichier | Rôle |
|---|---|
| `index.html` | La page complète (styles et script intégrés → 1 seule requête) |
| `favicon.svg` | Icône (geai bleu) |
| `.nojekyll` | Empêche GitHub Pages d'appliquer Jekyll |

## Modifier le contenu

Tout est dans `index.html`, en français :

- **Textes des projets** : recherchez `corviPi` et `aPiary` (balises `<p class="desc">`).
- **Nuances de couleur** : variables dans `:root` en haut du `<style>` (`--blue`, `--cyan`, `--bg`…).
- **Lien GitHub** : recherchez `github.com/Quantum-Caffeine` (4 occurrences).
- **Meta description / partage** : balises `<title>`, `<meta name="description">`, `og:*` en haut du fichier.

## Astuce : agrandir les logos

Les logos sont des SVG inline : **copiez le contenu de `<defs>` … `</svg>`** de `favicon.svg` et
remplacez-le à l'intérieur des balises `<svg class="mark">` (en-tête) et des SVG de projet.
L'attribut `id="g1"` doit rester unique : renommez-le (`g1`, `g2`, `g3`) si vous dupliquez.

## Tester en local

```bash
# simple : ouvrir le fichier
xdg-open index.html

# ou avec un serveur local (comme sur hébergement)
python3 -m http.server 8000   # puis http://localhost:8000
```

---

# Hébergement gratuit

## Option 1 — GitHub Pages (en ligne ✔)

Le dépôt **`Quantum-Caffeine/bluejay-intel`** est public et publié depuis la branche `main` (racine).

- Site : **https://quantum-caffeine.github.io/bluejay-intel/**
- Publier une mise à jour :

```bash
cd /run/media/jeromev/PartageBTRFS/BlueJayIntel
git add -A
git commit -m "site: mise à jour"
git push
```

- Vérifier l'état de publication :

```bash
gh api repos/Quantum-Caffeine/bluejay-intel/pages --jq '.html_url, .status'
```

- Modifier la source de publication : **Settings → Pages** du dépôt.

### Domaine personnalisé (ex. bluejayintel.com)

1. Achetez le domaine (≈10–15 $/an, seul coût — l'hébergement reste gratuit).
2. Chez le registrar, créez ces enregistrements **A** vers GitHub Pages :
   `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   puis un **CNAME** `www` → `quantum-caffeine.github.io`.
3. Ajoutez un fichier `CNAME` contenant `bluejayintel.com` à la racine du dépôt, puis `git push`.
4. Settings → Pages → Custom domain → cochez **Enforce HTTPS** (après propagation).

> Remarque : le compte GitHub `QuantumCaffeine` (sans tiret, celui qui apparaît dans
> l'historique de ce document) n'est **pas** celui utilisé ici. Le compte actif pour
> GitHub Pages est `Quantum-Caffeine`, et les liens du site pointent vers lui.

## Option 2 — Cloudflare Pages

Gratuit, HTTPS, CDN, déploiement par glisser-déposer ou via Git, **sans limite de bande passante** pratique.

- Sans Git : [dash.cloudflare.com](https://dash.cloudflare.com) → **Workers & Pages → Create → Pages → Upload assets** → glissez le dossier (sans `node_modules`) → nom du projet `bluejay-intel` → Deploy.
- URL : `https://bluejay-intel.pages.dev`.
- Domaine personnalisé : gratuit lui aussi si le domaine est géré par Cloudflare.

## Option 3 — Netlify

Gratuit, HTTPS automatique, très simple : [app.netlify.com/drop](https://app.netlify.com/drop) →
glissez le dossier → URL `https://bluejay-intel.netlify.app`. Possibilité de relier le dépôt GitHub pour
chaque `git push` redéploie automatiquement.

## Comparatif rapide

| Service | Bande passante | Domaine perso | Sans Git | Points forts |
|---|---|---|---|---|
| GitHub Pages | ~100 GB/mois (souple) | ✔ | ✘ (nécessite Git) | Vous avez déjà le compte |
| Cloudflare Pages | illimitée (raisonnable) | ✔ (gratuit) | ✔ (upload) | Très rapide, DNS gratuit |
| Netlify | 100 GB/mois | ✔ | ✔ (drag & drop) | Déploiement en 30 s |

## Si vous préférez un seul dépôt « entreprise »

Vous pouvez transformer ce dossier en dépôt monorepo :

```
BlueJayIntel/
├── site/            # -> contenu de ce dossier
├── corvipi/         # futur projet
└── apiary/          # futur projet
```

Puis dans GitHub Pages, choisissez la source **GitHub Actions** et un workflow
qui publie le dossier `site/` (ou le plus simple : gardez `index.html` à la racine du dépôt du site).

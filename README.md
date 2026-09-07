# Boccard – Carte de vœux 2019

Page de vœux du groupe Boccard : une page unique qui lit une vidéo de vœux en
plein écran, puis, à la fin de la lecture, affiche un encart renvoyant vers les
réseaux sociaux de l'entreprise. La langue (français ou anglais) et la
définition de la vidéo (360p ou 720p) sont choisies automatiquement.

**Année de réalisation / livraison : 2018** (diffusion pour les vœux 2019).

## Contenu

- `index.html` — page unique : structure HTML, texte, liens réseaux sociaux et
  script inline (lecture des paramètres d'URL, choix de langue et de définition,
  injection des `<source>` vidéo, transition vers l'encart de partage).
- `css/screen.css` — feuille de styles compilée (compressée) depuis
  `lib/compass/sass/screen.scss`.
- `css/ie.css`, `css/print.css` — feuilles compilées, vides (aucune règle
  définie dans les sources correspondantes).
- `lib/compass/config.rb` — configuration Compass (chemins, sortie compressée,
  assets relatifs).
- `lib/compass/sass/` — sources Sass : `screen.scss`, `ie.scss`, `print.scss`.
- `lib/compass/.sass-cache/` — cache de compilation Compass (généré).
- `images/` — logo Boccard, décors « étoiles » haut et bas, icônes réseaux
  sociaux (Facebook, LinkedIn, Twitter, YouTube), vignette de la vidéo
  (`vignette.png`).
- `videos/` — vidéo de vœux déclinée en 2 définitions (`360`, `720`), 2 langues
  (`fr`, `en`) et 3 formats (`.mp4`, `.webm`, `.ogv`), soit `video-<def>-<lang>.<ext>`.

## Stack technique

- Site statique, une seule page HTML, sans framework ni gestionnaire de paquets.
- JavaScript vanilla, écrit en clair dans `index.html` (pas de dépendance JS).
  La récupération des paramètres GET reprend un snippet de creativejuiz.fr
  (crédité en commentaire dans le code).
- Styles écrits en Sass et compilés avec Compass, sortie `:compressed`,
  `relative_assets = true` (cache-busting par timestamp sur les URLs d'images).
- Vidéo HTML5 native (`<video>` avec `<source>` mp4 / webm / ogv), image de
  substitution `poster`.
- Sélection de langue via le paramètre d'URL `?l=en` (défaut : `fr`) ;
  sélection de la définition selon `window.innerWidth` (≥ 1024 px → `720`,
  sinon `360`).

## Développement

Prérequis : Ruby avec les gems `compass` et `compass-core`
(`gem install compass`).

```sh
cd lib/compass
compass compile        # compile une fois vers ../../css
compass watch          # recompile à chaque modification des .scss
```

Servir la racine du projet avec n'importe quel serveur statique, par exemple :

```sh
python3 -m http.server 8000
```

Notes de configuration : dans `lib/compass/config.rb`, `http_path = "/"`
correspond à un déploiement à la racine du domaine ; à adapter si le site est
servi depuis un sous-dossier. Les chemins `css_dir`, `images_dir` et
`sass_dir` sont relatifs à `lib/compass/`.

## Crédits

- **Développement** — Olivier Charvoz
- **Commanditaire** — Boccard
- **Agence** — Big Company
- Snippet de récupération des paramètres GET :
  <https://www.creativejuiz.fr/blog/javascript/recuperer-parametres-get-url-javascript>

Copyright © 2018 Boccard. Tous droits réservés.

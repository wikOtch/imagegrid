# imagegrid

Particle **Image Grid** amélioré pour les templates Gantry 5 (testé avec RocketTheme Phoenix sous Joomla).
Improved **Image Grid** particle for Gantry 5 templates (tested with RocketTheme Phoenix on Joomla).

[Français](#français) · [English](#english)

---

## Français

### Améliorations

Ce particle reprend l'Image Grid d'origine (grille de 2 à 5 colonnes, légendes, visionneuse Lightcase) et ajoute :

- **Texte alternatif par image** : un champ *Alternative Text* remplit l'attribut `alt` de l'image. Le même texte sert de titre à l'image agrandie : il s'affiche comme titre dans la visionneuse Lightcase et en infobulle au survol de l'image agrandie. Les miniatures de la grille n'ont pas d'attribut `title`, donc pas d'infobulle. Si le champ est vide, la légende est utilisée. Les balises HTML éventuelles sont retirées.
- **Tags par image** : un champ *Tags* reçoit une liste de tags séparés par des virgules (ex. `mixage, documentaire`). Les tags ne tiennent pas compte des majuscules.
- **Filtre par tag** (option *Tag Filter*, activée par défaut) : une rangée de boutons au-dessus de la grille, « Tous » puis un bouton par tag, triés par ordre alphabétique. Un clic n'affiche que les images portant ce tag.
- **Recherche par tag** (option *Tag Search*, désactivée par défaut) : un champ de recherche filtre les images pendant la frappe, sans tenir compte des accents (« ete » trouve « été »).
- **Message « aucun résultat »** affiché quand aucune image ne correspond.
- **Fiche film** : pour chaque image, des champs *Film Title*, *Year*, *Director*, *Production* et *Festival* (un festival par ligne). Quand on clique sur une affiche, la fiche s'affiche avec l'image agrandie : **à côté de l'affiche** sur ordinateur et tablette, **sous l'affiche** sur mobile. Seuls les champs remplis apparaissent. Une image sans aucun champ film s'ouvre comme avant. Les libellés affichés (« Année », « Réalisateur », « Production », « Festival ») se changent dans les réglages du particle (*Year Label*, etc.). Le titre du film n'est pas répété s'il est identique au texte alternatif, qui reste le titre de l'image agrandie.
- **Album Lightcase cohérent** : quand un nom d'album est défini, les images masquées par le filtre sont retirées de la navigation de la visionneuse.
- **Accessibilité** : les boutons indiquent le filtre actif (`aria-pressed`) et le champ de recherche a un libellé.
- Les textes du bouton « Tous », du champ de recherche et du message sont modifiables dans les réglages du particle.

Le filtre est un petit script JavaScript sans dépendance, écrit dans le code du particle uniquement si au moins une image a un tag. Sans tags, le particle s'affiche comme l'original.

**Pourquoi à côté de l'image et pas dans un popup** : une affiche est verticale, il reste donc de la place à sa droite sur un écran d'ordinateur. La fiche se lit en même temps que l'affiche, sans clic de plus et sans rien cacher. Un second popup aurait recouvert l'affiche et demandé un clic pour le fermer. La fiche suit la navigation de l'album (flèches, clavier) et le filtre par tag.

**Sécurité** : les textes de la fiche sont échappés à l'affichage (une balise saisie apparaît comme du texte), puis copiés tels quels dans la visionneuse, sans être réinterprétés comme du HTML.

**Cache Joomla** : les scripts sont écrits dans le HTML du particle, et Lightcase est rechargé s'il manque, pour que le filtre et la visionneuse fonctionnent aussi quand la page sort du cache Joomla. Quand le module est affiché dans un article avec `{loadmoduleid}`, Joomla garde l'article en cache : après une modification des images, des textes ou des tags, videz le cache (Système → Vider le cache) pour voir les changements tout de suite.

### Fichiers

| Fichier | Rôle |
| --- | --- |
| `imagegrid.yaml` | Définition du particle et de ses champs dans l'administration Gantry |
| `imagegrid.html.twig` | Rendu HTML, script de filtrage et fiche film dans la visionneuse |
| `_imagegrid.scss` | Styles de la grille, des boutons de filtre, du champ de recherche et de la fiche film |

### Installation

Remplacez `nom_du_template` par le nom de votre template Gantry (par exemple `rt_phoenix`).

> Ces fichiers s'ajoutent ou remplacent ceux d'origine du template : faites-en une copie de sauvegarde avant, et pensez à les recopier après une mise à jour du template.

1. Copiez `imagegrid.html.twig` et `imagegrid.yaml` dans le dossier `particles` du template :
   ```
   templates/nom_du_template/particles/imagegrid.html.twig
   templates/nom_du_template/particles/imagegrid.yaml
   ```
2. Copiez `_imagegrid.scss` dans le dossier `scss/nom_du_template/particles` du template :
   ```
   templates/nom_du_template/scss/nom_du_template/particles/_imagegrid.scss
   ```
3. Videz le cache Gantry (administration Gantry → bouton *Clear Cache*) pour recompiler le CSS, puis le cache Joomla (Système → Vider le cache).

### Utilisation

1. Ajoutez le particle **Image Grid** dans une mise en page Gantry, ou créez un module Joomla de type **Gantry 5 Particle** et choisissez *Image Grid*.
2. Pour chaque image, renseignez l'image, la légende, le **texte alternatif**, les **tags** et, pour une affiche, la **fiche film** (titre, année, réalisateur, production, festivals).
3. Activez ou non *Tag Filter* et *Tag Search*, et adaptez les textes si besoin.

**Afficher le module dans un article Joomla** avec `{loadmoduleid 698}` (remplacez 698 par l'ID du module) : depuis Joomla 4, le module doit être autorisé sur la page de l'article, sinon rien ne s'affiche. Vérifiez :
- *Affectation des menus* : « Sur toutes les pages », ou l'élément de menu de l'article coché ;
- *Langue* : « Toutes » ou la langue de la page ;
- *Statut* : publié, et *Accès* : public.

---

## English

### Improvements

This particle builds on the original Image Grid (2 to 5 column grid, captions, Lightcase lightbox) and adds:

- **Per-image alternative text**: an *Alternative Text* field fills the image `alt` attribute. The same text is used as the title of the enlarged image: it shows as the title in the Lightcase lightbox and as a tooltip when hovering the enlarged image. The grid thumbnails have no `title` attribute, so no tooltip. When the field is empty, the caption is used. Any HTML tags are stripped.
- **Per-image tags**: a *Tags* field takes a comma-separated list of tags (e.g. `mixing, documentary`). Tags are case-insensitive.
- **Tag filter** (*Tag Filter* option, on by default): a row of buttons above the grid, "All" then one button per tag, sorted alphabetically. Clicking a button shows only the images with that tag.
- **Tag search** (*Tag Search* option, off by default): a search field filters the images as you type, ignoring accents ("ete" matches "été").
- **"No result" message** shown when no image matches.
- **Film details**: per image, *Film Title*, *Year*, *Director*, *Production* and *Festival* (one festival per line) fields. Clicking a poster shows the details with the enlarged image: **next to the poster** on desktop and tablet, **under the poster** on mobile. Only filled fields are shown, and an image without film fields opens as before. The displayed labels ("Année", "Réalisateur", "Production", "Festival") can be changed in the particle settings (*Year Label*, etc.). The film title is not repeated when it matches the alternative text, which stays the title of the enlarged image.
- **Consistent Lightcase album**: when an album name is set, images hidden by the filter are removed from the lightbox navigation.
- **Accessibility**: the buttons expose the active filter (`aria-pressed`) and the search field has a label.
- The "All" button, search placeholder and message texts can be changed in the particle settings.

The filter is a small dependency-free JavaScript, written into the particle output only when at least one image has a tag. Without tags, the particle renders like the original.

**Security**: the film details are escaped on output (typed tags show as text), then copied as-is into the lightbox, never parsed again as HTML.

**Joomla cache**: the scripts are written into the particle HTML, and Lightcase is loaded again when missing, so the filter and the lightbox also work when the page comes from the Joomla cache. When the module is shown in an article with `{loadmoduleid}`, Joomla caches the article: after changing the images, texts or tags, clear the cache (System → Clear Cache) to see the changes right away.

### Files

| File | Purpose |
| --- | --- |
| `imagegrid.yaml` | Particle definition and its fields in the Gantry admin |
| `imagegrid.html.twig` | HTML output, filter script and film details in the lightbox |
| `_imagegrid.scss` | Styles for the grid, filter buttons, search field and film details |

### Installation

Replace `template_name` with the name of your Gantry template (for example `rt_phoenix`).

> These files replace the template's original ones: back them up first, and copy them again after a template update.

1. Copy `imagegrid.html.twig` and `imagegrid.yaml` into the template's `particles` folder:
   ```
   templates/template_name/particles/imagegrid.html.twig
   templates/template_name/particles/imagegrid.yaml
   ```
2. Copy `_imagegrid.scss` into the template's `scss/template_name/particles` folder:
   ```
   templates/template_name/scss/template_name/particles/_imagegrid.scss
   ```
3. Clear the Gantry cache (Gantry admin → *Clear Cache* button) to recompile the CSS, then the Joomla cache (System → Clear Cache).

### Usage

1. Add the **Image Grid** particle to a Gantry layout, or create a Joomla module of type **Gantry 5 Particle** and pick *Image Grid*.
2. For each image, set the image, caption, **alternative text**, **tags** and, for a poster, the **film details** (title, year, director, production, festivals).
3. Turn *Tag Filter* and *Tag Search* on or off, and adjust the texts if needed.

**Showing the module in a Joomla article** with `{loadmoduleid 698}` (replace 698 with the module ID): since Joomla 4, the module must be allowed on the article's page, otherwise nothing is shown. Check:
- *Menu Assignment*: "On all pages", or the article's menu item selected;
- *Language*: "All" or the page language;
- *Status*: published, and *Access*: public.

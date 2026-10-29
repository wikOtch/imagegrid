# imagegrid

Particle **Image Grid** amélioré pour les templates Gantry 5 (testé avec RocketTheme Phoenix sous Joomla).
Improved **Image Grid** particle for Gantry 5 templates (tested with RocketTheme Phoenix on Joomla).

[Français](#français) · [English](#english)

---

## Français

### Améliorations

Ce particle reprend l'Image Grid d'origine (grille de 2 à 5 colonnes, légendes, visionneuse Lightcase) et ajoute :

- **Texte alternatif par image** : un champ *Alternative Text* remplit l'attribut `alt` de l'image. Le même texte sert d'attribut `title` sur l'image et sur le lien : il s'affiche en infobulle au survol et comme titre dans la visionneuse Lightcase. Si le champ est vide, la légende est utilisée.
- **Tags par image** : un champ *Tags* reçoit une liste de tags séparés par des virgules (ex. `mixage, documentaire`). Les tags ne tiennent pas compte des majuscules.
- **Filtre par tag** (option *Tag Filter*, activée par défaut) : une rangée de boutons au-dessus de la grille, « Tous » puis un bouton par tag, triés par ordre alphabétique. Un clic n'affiche que les images portant ce tag.
- **Recherche par tag** (option *Tag Search*, désactivée par défaut) : un champ de recherche filtre les images pendant la frappe, sans tenir compte des accents (« ete » trouve « été »).
- **Message « aucun résultat »** affiché quand aucune image ne correspond.
- **Album Lightcase cohérent** : quand un nom d'album est défini, les images masquées par le filtre sont retirées de la navigation de la visionneuse.
- **Accessibilité** : les boutons indiquent le filtre actif (`aria-pressed`) et le champ de recherche a un libellé.
- Les textes du bouton « Tous », du champ de recherche et du message sont modifiables dans les réglages du particle.

Le filtre est un petit script JavaScript sans dépendance, chargé en pied de page uniquement si au moins une image a un tag. Sans tags, le particle s'affiche comme l'original.

### Fichiers

| Fichier | Rôle |
| --- | --- |
| `imagegrid.yaml` | Définition du particle et de ses champs dans l'administration Gantry |
| `imagegrid.html.twig` | Rendu HTML et script de filtrage |
| `_imagegrid.scss` | Styles de la grille, des boutons de filtre et du champ de recherche |

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
2. Pour chaque image, renseignez l'image, la légende, le **texte alternatif** et les **tags**.
3. Activez ou non *Tag Filter* et *Tag Search*, et adaptez les textes si besoin.

**Afficher le module dans un article Joomla** avec `{loadmoduleid 698}` (remplacez 698 par l'ID du module) : depuis Joomla 4, le module doit être autorisé sur la page de l'article, sinon rien ne s'affiche. Vérifiez :
- *Affectation des menus* : « Sur toutes les pages », ou l'élément de menu de l'article coché ;
- *Langue* : « Toutes » ou la langue de la page ;
- *Statut* : publié, et *Accès* : public.

---

## English

### Improvements

This particle builds on the original Image Grid (2 to 5 column grid, captions, Lightcase lightbox) and adds:

- **Per-image alternative text**: an *Alternative Text* field fills the image `alt` attribute. The same text is used as the `title` attribute on the image and on the link, so it shows as a tooltip on hover and as the title in the Lightcase lightbox. When the field is empty, the caption is used.
- **Per-image tags**: a *Tags* field takes a comma-separated list of tags (e.g. `mixing, documentary`). Tags are case-insensitive.
- **Tag filter** (*Tag Filter* option, on by default): a row of buttons above the grid, "All" then one button per tag, sorted alphabetically. Clicking a button shows only the images with that tag.
- **Tag search** (*Tag Search* option, off by default): a search field filters the images as you type, ignoring accents ("ete" matches "été").
- **"No result" message** shown when no image matches.
- **Consistent Lightcase album**: when an album name is set, images hidden by the filter are removed from the lightbox navigation.
- **Accessibility**: the buttons expose the active filter (`aria-pressed`) and the search field has a label.
- The "All" button, search placeholder and message texts can be changed in the particle settings.

The filter is a small dependency-free JavaScript, loaded in the footer only when at least one image has a tag. Without tags, the particle renders like the original.

### Files

| File | Purpose |
| --- | --- |
| `imagegrid.yaml` | Particle definition and its fields in the Gantry admin |
| `imagegrid.html.twig` | HTML output and filter script |
| `_imagegrid.scss` | Styles for the grid, filter buttons and search field |

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
2. For each image, set the image, caption, **alternative text** and **tags**.
3. Turn *Tag Filter* and *Tag Search* on or off, and adjust the texts if needed.

**Showing the module in a Joomla article** with `{loadmoduleid 698}` (replace 698 with the module ID): since Joomla 4, the module must be allowed on the article's page, otherwise nothing is shown. Check:
- *Menu Assignment*: "On all pages", or the article's menu item selected;
- *Language*: "All" or the page language;
- *Status*: published, and *Access*: public.

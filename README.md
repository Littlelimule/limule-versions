# limule-versions

Fichiers lus par LimuleLib sur chaque serveur, au démarrage puis toutes les 6 h
(`raw.githubusercontent.com/Littlelimule/limule-versions/main/...`). Garder ce dépôt **public** :
un dépôt privé renvoie 404 sans jeton.

Un texte est soit une chaîne, soit une table par langue (`{ "fr": "...", "en": "..." }`) ; l'anglais sert de
repli quand la langue du joueur manque.

## versions.json

```json
{
  "schema": 1,
  "store": "https://ma-boutique.example",
  "products": {
    "limule":     { "name": "LimuleLib", "version": "3.1.0", "date": "2026-10-01",
                    "url": "https://...", "notes": { "fr": ["..."], "en": ["..."] } },
    "limdiscord": { "name": "Discord Suite", "version": "2.1.0", "url": "https://...",
                    "catalog": true, "desc": { "fr": "Une phrase.", "en": "One sentence." } }
  }
}
```

- La clé d'un produit est l'id de l'addon (`Limule.Addon({ id = ... })`), ou son champ `product` s'il en a un.
  `limule` = la lib.
- `version` plus récente que celle installée : la mise à jour apparaît dans le menu (page Mises à jour,
  pastille), en console serveur, et en notification aux admins qui se connectent (une fois par version).
- `url` : bouton « Télécharger » ; `notes` : liste de points ; `date` : `AAAA-MM-JJ`.
- `catalog: true` + `desc` : l'addon est proposé dans la vitrine « Découvrir plus d'addons » des serveurs
  qui ne l'ont pas. `store` : lien du bouton de cette vitrine.

## news.json

```json
{
  "schema": 1,
  "items": [
    {
      "id": "2026-10-01-lib-3-1",
      "kind": "lib",
      "tag": { "fr": "Nouveau", "en": "New" },
      "title": { "fr": "LimuleLib 3.1", "en": "LimuleLib 3.1" },
      "text": { "fr": "Une phrase, deux lignes au plus.", "en": "One sentence, two lines at most." },
      "points": { "fr": ["Point 1", "Point 2"], "en": ["Point 1", "Point 2"] },
      "action": { "fr": "Voir les notes", "en": "See the notes" },
      "url": "https://...",
      "from": "2026-10-01",
      "until": "2026-10-31",
      "minLib": "3.0",
      "ifAddon": "limdiscord",
      "ifMissing": "limpresence"
    }
  ]
}
```

- `id` : unique et stable (un admin qui ferme l'annonce ne la revoit pas avant la réouverture du menu).
- `kind` : `lib` (vitrine verte) ou `addon` (bleue).
- Facultatifs : `src` (texte à côté de l'étiquette, ex. le nom de l'addon), `points` (liste à droite), `action` + `url` (bouton), `from` / `until` (dates incluses),
  `minLib` / `maxLib` (versions de la lib), `ifAddon` (seulement si cet addon est chargé),
  `ifMissing` (seulement s'il n'est pas installé).
- 8 annonces au plus sont gardées.

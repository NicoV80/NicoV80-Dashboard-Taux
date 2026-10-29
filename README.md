# Courbes des taux · taux.siftlab.net

Site statique, sans étape de compilation, publié par Cloudflare comme le site nickel.

```
wrangler.jsonc      configuration Cloudflare (nom du projet : dashboard-taux)
public/index.html   interface : 5 onglets, charte Nickel Monitor, aucune dépendance externe hors police Carlito
public/data.js      toutes les données de taux, seul fichier à modifier pour une mise à jour
```

Pour un aperçu local : ouvrir `public/index.html` dans un navigateur.

## Mise en ligne (une seule fois)

1. **GitHub** : créer le dépôt privé `NicoV80/Dashboard-Taux`, puis cliquer sur « uploading an existing file » et y glisser `wrangler.jsonc`, `README.md` et le dossier `public`. Valider avec « Commit changes ».
2. **Cloudflare** : aller dans Workers & Pages, puis Create application, puis Import a repository.
   - Choisir `NicoV80/Dashboard-Taux`.
   - Nom du projet : `dashboard-taux`, identique au champ `name` de `wrangler.jsonc`.
   - Build command : laisser vide.
   - Deploy command : `npx wrangler deploy`, la valeur par défaut.
   - Cliquer sur Deploy.
3. **Domaine** : dans le projet `dashboard-taux`, ouvrir Settings, puis Domains & Routes, puis Add, puis Custom domain. Saisir `taux.siftlab.net`.
4. **Lien retour** : ajouter dans le bandeau du site nickel un lien vers `https://taux.siftlab.net/`. Le site des taux pointe déjà vers `https://nickel.siftlab.net/`.

## Mise à jour des données

Modifier `public/data.js` et l'envoyer sur GitHub. Cloudflare republie automatiquement.

- Indices 0 à 12 : fins de mois d'octobre 2025 à septembre 2026, puis le dernier point disponible.
- `swef` et `swuf` : `o` pour une valeur observée, `e` pour une valeur estimée, par maturité (2, 5, 10, 30 ans).
- `meta.asOfLabel` : la date affichée dans le bandeau.

Les textes de lecture et la chronologie sont rédigés dans `index.html`. Ils doivent être relus à chaque mise à jour importante.

## Points d'attention

- **Diffusion publique.** Les données de la Fed de New York, du Trésor américain, de la Banque de France, de la Bundesbank et de la BCE sont publiques. L'Euribor (EMMI) et les taux de swap (BlueGamma, Investing.com, PCBB) peuvent être soumis à des conditions de rediffusion : il faut les vérifier avant d'ouvrir le site au public.
- **Accès restreint.** Pour réserver l'accès, utiliser Cloudflare Zero Trust, puis Access, puis Applications. Ajouter `taux.siftlab.net` avec une règle sur les adresses e-mail autorisées (gratuit jusqu'à 50 utilisateurs).
- **Usage.** Outil d'aide à la décision, pas un conseil en investissement.

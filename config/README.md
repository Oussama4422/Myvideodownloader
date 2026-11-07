# Configuration distante — My Video Downloader

L'application lit un fichier JSON pour savoir **quels liens de pub afficher** et **s'il existe une nouvelle version**.
Elle le recharge à chaque démarrage et à chaque fois que le téléphone retrouve Internet.

## Où l'app cherche le fichier

1. `https://videodownloader.my/api/app-config.json` (le site, quand il sera prêt)
2. sinon `https://raw.githubusercontent.com/Oussama4422/Myvideodownloader/main/config/app-config.json` (dans le dépôt **public** `Oussama4422/Myvideodownloader`, celui des releases)

Tant que le site n'existe pas, il suffit de modifier `config/app-config.json` dans le dépôt public `Myvideodownloader` sur GitHub : les téléphones prennent la nouvelle valeur dès qu'ils sont en ligne.
Le fichier `config/app-config.json` du code source n'est qu'un modèle.
Si aucun fichier n'est trouvé, l'app fonctionne normalement : pas de pub, mise à jour vérifiée directement sur les *releases* GitHub.

## Champs

### `ads` — pubs sur le bouton Télécharger

| Champ | Rôle |
|---|---|
| `enabled` | `true` pour activer les pubs, `false` pour les couper partout. |
| `frequency` | Une pub tous les N appuis sur « Télécharger » (`1` = à chaque fois, `3` = un appui sur trois). |
| `directLinks` | Liens directs Adsterra / Monetag (ou autre). Ils s'ouvrent dans le navigateur **pendant que le téléchargement démarre**. Laissez `url` vide pour désactiver une entrée. |
| `directLinks[].weight` | Poids relatif : `2` = affiché deux fois plus souvent qu'un lien de poids `1`. |
| `unity.gameId` | Game ID Unity Ads (tableau de bord Unity → Monetization). Vide = Unity désactivé. |
| `unity.placementId` | Identifiant du placement interstitiel (par défaut `Interstitial_Android`). |
| `unity.testMode` | `true` pendant les essais, `false` en production. |

Les liens et Unity tournent à tour de rôle selon leur poids. **Le téléchargement n'est jamais bloqué par une pub.**

### `update` — mises à jour

| Champ | Rôle |
|---|---|
| `latestVersionCode` | Numéro de version : `majeur × 10000 + mineur × 100 + correctif` (v1.2.3 → `10203`). |
| `latestVersionName` | Version affichée, ex. `1.2.3`. |
| `changelog` | Notes de version par code langue (`en`, `fr`, `ar`…). L'anglais sert par défaut. |
| `apk` | Lien direct de l'APK par type de processeur. L'app choisit celui du téléphone, sinon `universal`. |

Les liens d'APK pointent vers les *releases* GitHub :
`https://github.com/Oussama4422/Myvideodownloader/releases/download/vX.Y.Z/MyVideoDownloader-vX.Y.Z-<abi>.apk`
Ces liens directs ne fonctionnent que si le dépôt (ou ses releases) est **public**.

### `links`

`website` et `fdm` : adresses ouvertes par le menu (Site web, FDM) et par le bouton Windows.

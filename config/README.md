# Configuration distante — My Video Downloader

L'application lit un fichier JSON pour savoir **s'il existe une nouvelle version**. Elle le recharge à chaque
démarrage et à chaque fois que le téléphone retrouve Internet.

## Où l'app cherche le fichier

1. `https://videodownloader.my/api/app-config.json` — généré par l'administration du site
   (**Mise à jour (APK)** : version, 4 liens directs, 4 empreintes SHA-256, nouveautés par langue).
2. sinon `https://raw.githubusercontent.com/Oussama4422/Myvideodownloader/main/config/app-config.json` (ce fichier).

Tant que le site n'est pas en ligne, ce fichier sert de source : pensez à le mettre à jour à chaque release.
Si aucun fichier n'est trouvé, l'app vérifie directement la dernière *release* GitHub (et son `SHA256SUMS.txt`).

## Champs (`schemaVersion` 2)

### `update`

| Champ | Rôle |
|---|---|
| `latestVersionCode` | `majeur × 10000 + mineur × 100 + correctif` (v1.2.3 → `10203`), identique au versionCode de l'APK. |
| `latestVersionName` | Version affichée, ex. `1.2.3`. |
| `released` | Date de publication (`AAAA-MM-JJ`). |
| `changelog` | Nouveautés par code langue (`en`, `fr`, `ar`, `zh`, `ja`, `he`, `hi`, `ko`, `it`, `pt`, `es`, `de`, `ru`). L'anglais sert par défaut. |
| `apk` | Lien direct de l'APK par architecture (`arm64-v8a`, `armeabi-v7a`, `x86_64`, `universal`). L'app choisit celle du téléphone, sinon `universal`. |
| `sha256` | Empreinte SHA-256 de chaque APK (affichée sur la page de téléchargement du site et dans `SHA256SUMS.txt`). |
| `size` | Taille en octets (affichage). |

Les liens pointent vers les *releases* GitHub :
`https://github.com/Oussama4422/Myvideodownloader/releases/download/vX.Y.Z/MyVideoDownloader-vX.Y.Z-<abi>.apk`
Les empreintes sont dans le fichier `SHA256SUMS.txt` joint à chaque release.

### `links`

`website` et `fdm` : adresses ouvertes par le menu (Site web, FDM) et par le bouton Windows.

Quand une version plus récente est publiée, l'application affiche « Mise à jour disponible » avec les nouveautés ;
le bouton **Mettre à jour** ouvre le lien de l'APK de son architecture et Android l'installe par-dessus la version
actuelle. Depuis la version 1.1.1, l'application n'installe plus elle-même de paquets (c'est ce qui la faisait classer
« dangereuse » par Google Play Protect) et ne contient aucune publicité.

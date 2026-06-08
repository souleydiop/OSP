# FibreOps — Gestion Incidents Coupure Fibre Optique

Application PWA (Progressive Web App) pour la gestion et simulation des incidents de coupure fibre optique sur réseau télécom.

## Fonctionnalités

- **Upload multi-fichiers KMZ/KML** — Tracés fibre optique affichés sur carte
- **Base BTS en KMZ** — Import des sites BTS avec affichage/masquage par toggle
- **Upload fichiers .sor** — Analyse automatique des mesures OTDR (événements, pertes, réflexions)
- **Simulation de coupure** — Choisir un tronçon, saisir la distance en km, simuler l'impact
- **Visualisation carte** — Point de coupure, segment en rouge, BTS impactées colorées
- **Analyse des dégradations** — Métriques réseau, table BTS impactées, export CSV
- **Fonds de carte** — OSM, Satellite, Dark, Topo

## Structure

```
fibre-incident-manager/
├── index.html      # Application principale (SPA)
├── manifest.json   # PWA manifest
├── sw.js           # Service Worker (offline)
└── README.md
```

## Déploiement GitHub Pages

1. Créer un repo GitHub : `fibreops` (ou nom au choix)
2. Uploader les 3 fichiers : `index.html`, `manifest.json`, `sw.js`
3. Aller dans Settings → Pages → Source: `main` branch → Save
4. L'app sera accessible sur : `https://<username>.github.io/fibreops/`

## Génération APK via PWABuilder

1. Aller sur **https://www.pwabuilder.com**
2. Entrer l'URL GitHub Pages de l'app
3. Cliquer **Start** → laisser l'analyse s'effectuer
4. Section **Android** → cliquer **Package for store**
5. Choisir **Generate** → télécharger le `.apk` signé
6. Installer directement sur Android (activer "sources inconnues")

> Pour publier sur Google Play Store, utiliser l'option **TWA (Trusted Web Activity)** de PWABuilder.

## Format des fichiers

### KMZ / KML — Fibre & BTS
- Fibre : `LineString` ou `MultiLineString` avec `name` dans les propriétés
- BTS : `Point` avec `name` = identifiant du site (ex: `THIES_001`)

### Fichiers .sor
- Format standard **Bellcore SR-4731** (OTDR)
- Compatible : EXFO, JDSU, Anritsu, Viavi, Yokogawa
- L'application lit : longueur, longueur d'onde, IOR, événements (épissures, connecteurs, coupures, réflexions)

## Stack technique

- **Leaflet.js** 1.9.4 — Cartographie
- **leaflet-omnivore** — Lecture KMZ/KML
- **Vanilla JS / CSS** — Aucun framework, léger et rapide
- **PWA** — Service Worker + manifest pour installation offline

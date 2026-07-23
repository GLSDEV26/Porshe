# Macan 95B — Analyse d'achat

Application web (PWA) d'aide à la décision pour l'achat d'un **Porsche Macan phase 1 (2014-2018)** :
estimation de valeur marché, marge de négociation chiffrée, coût réel d'entrée, financement
et checklist d'inspection.

Pensée pour être utilisée **sur le téléphone, chez le vendeur** : installable en plein écran,
fonctionne hors connexion, sauvegarde l'analyse en cours.

## Fonctions

| Onglet | Contenu |
|---|---|
| **Voiture** | Version, année, kilométrage, prix demandé, type de vendeur, qualité du suivi |
| **Verdict** | Jauge prix vs marché, valeur estimée, nuage de points des 25 comparables |
| **Négo** | 12 leviers chiffrés (dont 2 critiques), stratégie d'offre en 3 paliers |
| **Budget** | Carte grise, financement jusqu'à 120 mois, coût de possession annuel |
| **Check** | 13 points d'inspection spécifiques au 95B, avec progression |

## Le modèle d'estimation

Valeur de référence par version à 100 000 km / millésime 2016, puis :

- **−150 €** par tranche de 1 000 km au-delà de 100 000 (**+130 €** en dessous)
- **±2 300 €** par année de millésime
- coefficient de suivi d'entretien : 0,86 (aucun justificatif) à 1,04 (réseau Porsche)

Bases de référence : GTS 45 000 € · Turbo 43 500 € · S essence 38 500 € · S Diesel 33 500 € · 2.0 31 000 €.

Calibré sur 25 annonces leboncoin relevées en **juillet 2026**. Ce sont des prix demandés,
pas des prix de transaction. **C'est une estimation indicative, pas une cote officielle** :
à recouper avec l'Argus et La Centrale avant toute offre ferme.

## Installation sur iPhone

1. Ouvrir l'URL dans **Safari** (pas Chrome — l'installation PWA ne marche que depuis Safari sur iOS)
2. Bouton **Partager** → **Sur l'écran d'accueil**
3. L'app s'ouvre en plein écran, sans barre d'adresse, et fonctionne hors connexion

## Développement

Aucune dépendance, aucun build. Trois fichiers : `index.html`, `manifest.webmanifest`, `sw.js`.

```bash
python3 -m http.server 8080
# puis http://localhost:8080
```

Le service worker met l'app en cache. Après une modification, incrémenter `CACHE` dans `sw.js`
pour forcer la mise à jour côté client.

## Données

Les saisies sont stockées **en local sur l'appareil** (`localStorage`). Rien n'est envoyé nulle part :
pas de serveur, pas d'analytics, pas de dépendance externe hors les polices Google.

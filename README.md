# IGBEGA X — Formulaire de Restitution Stratégique Q1 2026

<div align="center">

![IGBEGA X](https://img.shields.io/badge/IGBEGA%20X-Restitution%20Q1%202026-1B8FE3?style=for-the-badge&logo=discord&logoColor=white)
![HTML](https://img.shields.io/badge/HTML5-Single%20File-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![Formspree](https://img.shields.io/badge/Formspree-Email%20Integration-FF5733?style=for-the-badge)
![Mobile First](https://img.shields.io/badge/Design-Mobile%20First-3DC9F5?style=for-the-badge)

**Formulaire web multi-étapes pour la restitution trimestrielle des Leads de pôle de la communauté Igbega X.**

[Aperçu](#aperçu) · [Fonctionnalités](#fonctionnalités) · [Installation](#installation) · [Configuration](#configuration) · [Structure](#structure-du-projet) · [Personnalisation](#personnalisation)

</div>

---

## Aperçu

Ce projet est une **application web statique** (fichier HTML unique, sans dépendances externes ni serveur) permettant aux Leads de pôle d'Igbega X de soumettre leur bilan trimestriel de façon structurée et professionnelle.

Les réponses sont transmises automatiquement par email au Lead Général via **Formspree**.

```
Soumission formulaire  →  25 Mai 2026
Séance de présentation →  31 Mai 2026 (Discord)
```

---

## Fonctionnalités

### Interface
- **Cover / Hero** — page d'accueil avec logo, dates clés et accès rapide au formulaire
- **Formulaire multi-étapes** — 5 étapes avec barre de progression interactive
- **Récapitulatif complet** — relecture de toutes les réponses avant envoi (étape 6)
- **Validation en temps réel** — champs obligatoires vérifiés à chaque étape
- **Écran de succès** — confirmation animée après soumission

### Technique
- **Zéro dépendance** — aucun framework JS, aucun build, un seul fichier `.html`
- **Mobile First** — responsive, conçu d'abord pour smartphone
- **Icônes SVG inline** — aucun chargement externe d'icônes
- **Logo embarqué** — image encodée en base64 directement dans le HTML
- **Police Google Fonts** — `Plus Jakarta Sans` (chargement CDN unique)

### Formulaire — 5 étapes
| Étape | Contenu |
|-------|---------|
| **1 — Identité** | Nom complet, pôle dirigé, email, nombre de membres |
| **2 — Plan & Activités** | Plan d'action initial (Mars 2026), activités réalisées |
| **3 — Résultats & KPIs** | Résultats obtenus, niveau d'atteinte, estimation %, KPIs |
| **4 — Difficultés & Q2** | Difficultés rencontrées, perspectives et ajustements Q2 |
| **5 — Modalités** | Durée de présentation, format Discord, éléments couverts, commentaires |

### Pôles disponibles
- Formation et Recherche
- Projets et Innovation
- Communication et Branding
- Partenariats et Relations Extérieures
- Administration et Organisation

---

## Installation

### Option 1 — Utilisation directe (recommandée)

Aucune installation requise. Il suffit d'ouvrir le fichier dans un navigateur :

```bash
# Cloner le dépôt
git clone https://github.com/ShegouB/restitution_igbegaX.git

# Ouvrir le fichier
open index.html
# ou double-cliquer sur le fichier
```

### Option 2 — Hébergement statique

Le fichier peut être déployé sur n'importe quel hébergeur statique :

**GitHub Pages**
```bash
# Depuis la racine du repo
git add index.html
git commit -m "deploy: formulaire restitution Q1"
git push origin main
# Activer GitHub Pages dans Settings > Pages > main / root
```

**Autres hébergeurs compatibles**
- [Netlify Drop](https://app.netlify.com/drop) — glisser-déposer le fichier
- [Vercel](https://vercel.com) — via CLI ou interface web
- [Cloudflare Pages](https://pages.cloudflare.com) — déploiement en 1 clic

---

## Configuration

### Formspree (envoi d'email)

Les soumissions du formulaire sont envoyées via [Formspree](https://formspree.io). Pour configurer votre propre endpoint :

**1. Créer un compte Formspree**
```
https://formspree.io/register
```

**2. Créer un nouveau formulaire**
- Aller dans "New Form"
- Renseigner l'email de réception
- Copier le Form ID généré (ex: `xkoydzeq`)

**3. Mettre à jour le fichier HTML**

Rechercher la ligne suivante dans `index.html` :
```javascript
const res = await fetch('https://formspree.io/f/xxxxxxx', {
```

Remplacer `xxxxxxx` par votre propre Form ID :
```javascript
const res = await fetch('https://formspree.io/f/VOTRE_FORM_ID', {
```

**4. Configuration actuelle**
```
Endpoint  : https://formspree.io/f/xkoydzeq
Email     : xxxxxxx@gmail.com
Sujet     : [IGBEGA X] Restitution Q1 2026
```

> **Note :** Le plan gratuit Formspree est limité à **50 soumissions/mois**. Pour une communauté avec 5 pôles, cela est largement suffisant.

---

## Structure du projet

```
restitution_igbegaX/
│
├── index.html       # Fichier principal (tout-en-un)
├── README.md               # Cette documentation
│
└── assets/                 # (optionnel si logo externalisé)
    └── logo.png
```

### Architecture interne du fichier HTML

```
index.html
├── <head>
│   ├── Meta tags + viewport
│   ├── Google Fonts (Plus Jakarta Sans)
│   └── <style> — CSS complet (~400 lignes)
│
├── <body>
│   ├── .topbar              — Barre de navigation fixe
│   ├── .hero                — Page de couverture
│   ├── .form-section
│   │   ├── .prog-wrap       — Barre de progression (étapes 1–6)
│   │   ├── .form-wrap
│   │   │   ├── #step1       — Identité
│   │   │   ├── #step2       — Plan & Activités
│   │   │   ├── #step3       — Résultats & KPIs
│   │   │   ├── #step4       — Difficultés & Q2
│   │   │   ├── #step5       — Modalités
│   │   │   ├── #recapBlock  — Récapitulatif dynamique
│   │   │   └── #subBlock    — Bouton d'envoi
│   └── #success             — Écran de confirmation
│
└── <script> — Logique JS (~120 lignes)
    ├── Navigation multi-étapes
    ├── Validation par étape
    ├── Construction du récapitulatif
    └── Soumission Formspree (async/await)
```

---

## Personnalisation

### Modifier les dates

Rechercher et remplacer dans le HTML :

```html
<!-- Date limite de soumission -->
<div class="dn">25</div>
<div class="dm">Mai 2026</div>

<!-- Date de la séance -->
<div class="dn">31</div>
<div class="dm">Mai 2026</div>
```

### Modifier les pôles

Dans la section `#step1`, mettre à jour les `<option>` :

```html
<select name="pole" required>
  <option value="" disabled selected>Sélectionner</option>
  <option>Formation et Recherche</option>
  <option>Projets et Innovation</option>
  <option>Communication et Branding</option>
  <option>Partenariats et Relations Extérieures</option>
  <option>Administration et Organisation</option>
</select>
```

### Modifier la palette de couleurs

Les couleurs sont définies dans les variables CSS en haut du `<style>` :

```css
:root {
  --bg: #05080F;         /* Fond principal */
  --blue: #1B8FE3;       /* Couleur primaire */
  --cyan: #3DC9F5;       /* Couleur secondaire */
  --grad: linear-gradient(135deg, #1B8FE3, #3DC9F5); /* Dégradé */
  --text: #EEF2FF;       /* Texte principal */
  --text2: #A8B4D0;      /* Texte secondaire */
  --text3: #5A6880;      /* Texte tertiaire */
}
```

### Remplacer le logo

Le logo est actuellement embarqué en **base64** directement dans le HTML. Pour le remplacer :

**Option A — Remplacer par une URL externe**
```html
<!-- Rechercher toutes les occurrences de : -->
<img src="data:image/jpeg;base64,/9j/4AAQ..." alt="IGBEGA X"/>

<!-- Remplacer par : -->
<img src="https://votre-domaine.com/logo.png" alt="IGBEGA X"/>
```

**Option B — Générer un nouveau base64**
```bash
# Encoder votre logo en base64
base64 -w 0 votre-logo.png > logo_b64.txt

# Construire la data URI
echo "data:image/png;base64,$(cat logo_b64.txt)"
```

### Modifier le sujet de l'email

```javascript
// Dans le <form>
<input type="hidden" name="_subject" value="[IGBEGA X] Restitution Q1 2026"/>
```

---

## Données collectées

Voici les champs transmis à chaque soumission :

| Champ | Type | Obligatoire |
|-------|------|:-----------:|
| `nom_complet` | Texte | ✅ |
| `pole` | Sélection | ✅ |
| `email` | Email | ✅ |
| `nb_membres` | Nombre | ❌ |
| `plan_action` | Textarea (600 car.) | ✅ |
| `activites` | Textarea (600 car.) | ✅ |
| `resultats` | Textarea (600 car.) | ✅ |
| `niveau_atteinte` | Sélection | ✅ |
| `pct` | Nombre (0–100) | ❌ |
| `kpis` | Textarea (500 car.) | ✅ |
| `difficultes` | Textarea (500 car.) | ❌ |
| `perspectives` | Textarea (600 car.) | ✅ |
| `duree` | Sélection | ✅ |
| `format` | Sélection | ❌ |
| `elements_presentation` | Texte (cases cochées) | ❌ |
| `commentaires` | Textarea (300 car.) | ❌ |

---

## Stack technique

| Technologie | Usage |
|-------------|-------|
| **HTML5** | Structure et sémantique |
| **CSS3** | Styles, animations, responsive (variables CSS, Grid, Flexbox) |
| **JavaScript ES6+** | Navigation, validation, fetch API |
| **Formspree** | Backend email serverless |
| **Google Fonts** | Typographie (`Plus Jakarta Sans`) |
| **SVG inline** | Icônes sans dépendances |

---

## Compatibilité navigateurs

| Navigateur | Support |
|------------|:-------:|
| Chrome 90+ | ✅ |
| Firefox 88+ | ✅ |
| Safari 14+ | ✅ |
| Edge 90+ | ✅ |
| Mobile Chrome | ✅ |
| Mobile Safari | ✅ |

> `backdrop-filter` (effet de flou sur la topbar) peut ne pas fonctionner sur certaines versions de Firefox. Le fallback est un fond opaque.

---

## Contribuer

Les contributions sont les bienvenues pour améliorer ce formulaire.

```bash
# Fork le projet
# Créer une branche feature
git checkout -b feat/ma-amelioration

# Commiter les changements
git commit -m "feat: description de l'amélioration"

# Pousser et ouvrir une Pull Request
git push origin feat/ma-amelioration
```

### Conventions de commit

```
feat:     Nouvelle fonctionnalité
fix:      Correction de bug
style:    Modification de design/CSS
docs:     Mise à jour documentation
chore:    Maintenance générale
```

---

## Licence

Ce projet est la propriété de la communauté **Igbega X**.  
Usage réservé aux membres et Leads de la communauté.

---

<div align="center">

Développé pour **Igbega X** · Lead Général · Q1 2026

![Made with](https://img.shields.io/badge/Made%20with-HTML%20%2B%20CSS%20%2B%20JS-1B8FE3?style=flat-square)
![Formspree](https://img.shields.io/badge/Powered%20by-Formspree-FF5733?style=flat-square)

</div>

# CLAUDE.md — Ccentre AI
> Fichier de contexte projet pour Claude. À lire en début de chaque nouvelle session.
> Dernière mise à jour : Mars 2026

---

## 🏢 Contexte Métier

**Ccentre AI** est une agence d'automatisation d'appels téléphoniques 100% IA, disponible 24/7, ciblant les entreprises B2B au Paraguay et en Amérique Latine.

- **Modèle** : SaaS B2B — abonnement mensuel
- **Positionnement** : "Tu empresa, siempre disponible."
- **Marché cible** : PMEs paraguayennes — immobilier, cliniques, agences marketing, e-commerce, éducation, restauration, finance
- **Langue du site** : Espagnol (es-PY)
- **Siège** : Asunción, Paraguay
- **Email** : hola@ccentre.ai
- **Associé principal** : Santiago Lacarrubba (compte Calendly : `ccentrepy`)
- **Développeur/Owner GitHub** : kemaspues

### Plans tarifaires
| Plan | Prix | Appels/mois |
|------|------|-------------|
| Starter | $500 USD/mois | 500 |
| Business | $1,500 USD/mois | 5,000 |
| Enterprise | Sur devis | Illimité |

### Technologies IA utilisées (affichées sur le site)
OpenAI · ElevenLabs · Vapi · Twilio · Google

---

## 🗂️ Architecture du Projet

```
ccentre-ai/
├── index.html          ← Landing page (renommé depuis ccentre-ai-v6.html)
├── dashboard.html      ← Dashboard client
└── CLAUDE.md           ← Ce fichier
```

**Hébergement** : GitHub Pages
- **Repo** : `github.com/kemaspues/ccentre-ai-v6.html`
- **Landing** : `https://kemaspues.github.io/ccentre-ai-v6.html/`
- **Dashboard** : `https://kemaspues.github.io/ccentre-ai-v6.html/dashboard.html`

**Référence** (ancien site de l'associé) : `https://ccentreai.github.io/#`

### Principe d'architecture
- **Zéro backend** : tout est en HTML/CSS/JS vanilla standalone
- **Zéro build tool** : pas de npm, webpack, ni framework
- **Single file** : chaque page = 1 fichier HTML autonome (CSS + JS inline)
- **Déploiement** : upload manuel sur GitHub Pages via l'interface web

---

## 🛠️ Stack Technique

### Landing Page (`index.html`)
| Élément | Valeur |
|---------|--------|
| Format | HTML5 standalone (CSS + JS inline) |
| Taille | ~53 KB, ~1000 lignes |
| Fonts | Bricolage Grotesque (titres) + Geist (body) via Google Fonts |
| Lib externe | Calendly Widget JS (`assets.calendly.com`) |
| Animations | Canvas API (flickering grid + ripple circles) |
| Calendrier | Calendly embed (`calendly.com/ccentrepy/30min`) |

### Dashboard (`dashboard.html`)
| Élément | Valeur |
|---------|--------|
| Format | HTML5 standalone (CSS + JS inline) |
| Taille | ~65 KB, ~938 lignes |
| Fonts | Bricolage Grotesque + Geist via Google Fonts |
| Charts | Chart.js `4.4.1` via cdnjs.cloudflare.com |
| Données | Fictives (démo) — générées en JS au runtime |

---

## 🎨 Design System

### Couleurs — Mode Sombre (défaut)
```css
:root {
  /* Verts */
  --g: #25D366;          /* Vert principal (WhatsApp green) */
  --gd: #1aab52;         /* Vert foncé */
  --gdim: rgba(37,211,102,.10);   /* Vert transparent */
  --gborder: rgba(37,211,102,.20);

  /* Fonds */
  --bg: #050906;         /* Fond page */
  --bg2: #080e09;        /* Fond alternatif */
  --s: #0c1510;          /* Surface */
  --s2: #101a13;         /* Surface 2 */
  --s3: #142018;         /* Surface 3 */

  /* Textes */
  --t: #edf7f0;          /* Texte principal */
  --t2: #a8cdb6;         /* Texte secondaire */
  --t3: #7aaa8a;         /* Texte muted */

  /* Bordures */
  --b: rgba(255,255,255,.06);
  --b2: rgba(255,255,255,.11);
}
```

### Couleurs — Mode Clair
```css
html.light {
  --g: #1aab52;          /* Vert adapté au fond clair */
  --bg: #f4f7f5;
  --bg2: #eef2f0;
  --s: #ffffff;
  --s2: #f0f4f2;
  --s3: #e8ede9;
  --t: #0d1a0f;
  --t2: #3a6647;
  --t3: #5a7a62;
  --b: rgba(0,0,0,.07);
  --b2: rgba(0,0,0,.12);
}
```

### Typographie
- **Titres / Display** : `Bricolage Grotesque` — weights 300, 400, 500, 700, 800
- **Body / UI** : `Geist` — weights 300, 400, 500, 600, 700
- **Sizing** : `clamp()` pour les titres hero (responsive automatique)

### Identité visuelle (Logo)
Le logo est un **SVG inline** composé de :
1. Lettre **"C"** verte (`#25D366`) — Bricolage Grotesque 900
2. **Waveform** (5 barres rectangulaires blanches de hauteurs variables)
3. Texte **"CENTRE"** blanc — Bricolage Grotesque 800, letter-spacing 1.5
4. Badge **"AI"** — rectangle vert `#25D366`, texte noir

```html
<svg viewBox="0 0 172 40" fill="none">
  <text x="0" y="30" font-family="Bricolage Grotesque" font-weight="900" fill="#25D366">C</text>
  <!-- 5 barres waveform blanches -->
  <text x="33" y="30" font-family="Bricolage Grotesque" font-weight="800" fill="#fff">CENTRE</text>
  <rect x="130" y="12" width="30" height="18" rx="5" fill="#25D366"/>
  <text x="145" y="25" fill="#000" text-anchor="middle">AI</text>
</svg>
```

---

## 📄 Structure Landing Page (`index.html`)

### Navigation
```
Logo | Servicios | Proceso | Precios | Contacto | [🌙/☀️] [Área de clientes]
```
- `Área de clientes` → `dashboard.html` (liseré vert `border: 2px solid #25D366`)
- Toggle dark/light : icônes SVG lune/soleil, border vert permanent

### Sections (dans l'ordre)
| ID | Classe | Contenu |
|----|--------|---------|
| — | `.he` | Hero : tagline + CTAs + waveform animée |
| — | `.logos` | Bande technos : OpenAI, ElevenLabs, Vapi, Twilio, Google |
| `#features` | `.fv2` | 6 features cards (Voice Agent AI, Recopilación, Agenda, Voz clonada, Follow-up, Reportes) |
| `#how` | `.how` | 3 étapes : Onboarding → Entrenamiento → Integración |
| `#infographic` | `.apple` | Infographie Apple-style : stats 0%, 5s, +40%, 48h, 24/7 |
| `#pricing` | `.pricing` | 3 plans : Starter / Business (hot) / Enterprise |
| — | `.testi` | 2 témoignages |
| `#contact` | `.fcta` | CTA final + Calendly widget embed |
| — | `footer` | Liens + copyright |

### Tagline (IMMUABLE — ne jamais changer sans accord explicite)
```
Ligne 1 : "Tu empresa,"          ← blanc
Ligne 2 : "siempre disponible."  ← vert (#25D366)
```

### Hero subtitle
```
"Implementamos agentes de voz con inteligencia artificial que atienden,
califican y convierten a tus clientes — las 24 horas, sin intervención humana."
```

### CTAs Hero
- Bouton principal : `Agendar una demo` → `#contact`
- Bouton secondaire : `Ver servicios →` → `#features`

### Calendly
- **URL** : `https://calendly.com/ccentrepy/30min`
- **Paramètres dark** : `?locale=es&hide_event_type_details=1&hide_gdpr_banner=1&background_color=0c1510&text_color=dff0e1&primary_color=25D366`
- **Paramètres light** : `background_color=f4f7f5&text_color=0d1a0f&primary_color=1aab52`
- Le widget recharge dynamiquement via `updateCalendly()` au toggle de thème

---

## 📊 Structure Dashboard (`dashboard.html`)

### Login
- Page de login plein écran (`z-index: 9999`) avec canvas flickering vert
- N'importe quel email + mot de passe fonctionne (démo)
- Après login : `loginPage.style.pointerEvents = 'none'` IMMÉDIATEMENT, puis `display:none` après 400ms fade

### Sidebar (260px fixe)
```
Logo SVG
├── [Principal]
│   ├── Resumen
│   ├── Llamadas
│   ├── Agente IA
│   └── Reportes
├── [Sistema]
│   ├── Integraciones
│   └── Configuración
├── Plan activo (Business)
├── ← Volver al sitio web  (→ index.html)
├── Cerrar sesión (rouge)  (→ confirm + redirect index.html)
└── Avatar RetailPro Paraguay
```

### Sections dashboard
| ID | Contenu |
|----|---------|
| `sec-resumen` | 4 métriques + chart ligne 7 jours + feed dernières llamadas |
| `sec-llamadas` | Table 87 appels fictifs + filtres + export CSV + modal transcription |
| `sec-agente` | Fiche Agente Sofía + waveform + stats + scripts |
| `sec-reportes` | 3 charts Chart.js (bar + donut + line) + KPIs |
| `sec-integraciones` | Salesforce/HubSpot/Pipedrive + Webhook URL + API Key |
| `sec-configuracion` | Datos empresa + horarios + notificaciones + plan + danger zone |

### Navigation entre sections
```javascript
function navigate(page, el) {
  // Cache toutes les sections, affiche sec-{page}
  // Retire .active de tous les nav-items, ajoute sur el
  // Si reportes : setTimeout(initReportCharts, 100)
  // Si llamadas : renderCalls()
}
```
**IMPORTANT** : Les nav-items ont à la fois `onclick="navigate(...)"` ET un `addEventListener` ajouté via `DOMContentLoaded` pour double protection.

### Charts (Chart.js 4.4.1)
- `chartInstances` : objet global qui stocke les instances
- `destroyCharts()` : détruit toutes les instances avant réinit
- `getChartColors()` : retourne `{txt, grid}` selon `isDark`
- `initResumenChart()` : chart ligne (section Resumen)
- `initReportCharts()` : 3 charts (bar + donut + line, section Reportes)
- Init au chargement via `DOMContentLoaded` avec `setTimeout(initResumenChart, 150)`

### Toggle thème dashboard
```javascript
// IIFE dans le second script — expose window.toggleTheme et window.isDark
(function(){
  var dark = localStorage.getItem('dash-t') !== 'l';
  // Applique html.light ou non
  // Met à jour window.isDark (utilisé par getChartColors)
  // Synchronise isDark du script Opus : try{ isDark=dark; }catch(e){}
  window.toggleTheme = function(){ ... };
})();
```
- Clé localStorage : `'dash-t'` (valeurs : `'d'` = dark, `'l'` = light)

---

## 🔧 Conventions de Code

### CSS
- **Variables CSS** : toutes préfixées `--` et définies dans `:root`
- **Nommage** : kebab-case court (`--g`, `--bg`, `--t2`) pour les variables fréquentes
- **Sélecteurs** : classes courtes et descriptives (`.he`, `.bp`, `.bg2`, `.ncta`)
- **Light mode** : via classe `html.light` (jamais `body.light`)
- **Responsive** : `clamp()` pour les tailles de titres, media queries à la fin du CSS
- **Minification** : CSS minifié inline pour les propriétés répétitives
- **Transitions** : `all .2s` ou `all .25s cubic-bezier(.4,0,.2,1)`

### JavaScript
- **Vanilla JS uniquement** — zéro framework (pas de React, Vue, etc.)
- **Fonctions globales** pour les `onclick` HTML inline
- **IIFE** `(function(){...})()` pour les blocs autonomes (flickering canvas, toggle thème)
- **`window.X`** pour exposer des fonctions depuis une IIFE vers le scope global
- **`var`** dans les scripts anciens (Opus), **`const`/`let`** dans les nouveaux
- **Pas de modules ES** (compatibilité maximale)
- **Ordre critique** : les fonctions utilisées dans `DOMContentLoaded` doivent être définies AVANT dans le même script

### HTML
- **Langue** : `<html lang="es">`
- **Sections sémantiques** : `<section>`, `<nav>`, `<aside>`, `<header>`, `<footer>`
- **IDs de navigation** : `#features`, `#how`, `#pricing`, `#contact`
- **IDs sections dashboard** : `sec-{nom}` (ex: `sec-resumen`, `sec-llamadas`)
- **Icônes** : SVG inline (pas d'icon fonts)

### Nommage des classes CSS (Landing)
| Préfixe | Usage |
|---------|-------|
| `.he` | Hero section |
| `.bp` | Bouton primaire vert |
| `.bg2` | Bouton secondaire outline |
| `.ncta` | Nav CTA button |
| `.atile-*` | Infographie tiles |
| `.pcard` | Pricing card |
| `.fv2-*` | Features v2 cards |
| `.hstep-*` | How-to steps |
| `.fcta` | Final CTA section |

### Nommage des classes CSS (Dashboard)
| Préfixe | Usage |
|---------|-------|
| `.metric-card` | Carte de métrique |
| `.nav-item` | Item de navigation sidebar |
| `.section` | Section de contenu (cachée par défaut) |
| `.section.active` | Section visible |
| `.card` | Carte de contenu générique |
| `.btn-primary` | Bouton vert principal |
| `.btn-outline` | Bouton outline |
| `.status-badge` | Badge de statut (exitosa/sin-respuesta/transferida) |

---

## 🚀 Commandes de Déploiement

### Workflow standard
```
1. Modifier le fichier localement (Claude génère le HTML)
2. Télécharger le fichier depuis Claude
3. Renommer :
   - Landing page → index.html
   - Dashboard    → dashboard.html
4. Aller sur github.com/kemaspues/ccentre-ai-v6.html
5. Add file → Upload files → glisser les fichiers
6. Commit directly to main → Confirm
7. Attendre 1-2 min → GitHub Pages se déploie automatiquement
8. Vider le cache navigateur : Cmd+Shift+R (Mac) / Ctrl+Shift+R (Windows)
```

### URLs de production
```
Landing  : https://kemaspues.github.io/ccentre-ai-v6.html/
Dashboard: https://kemaspues.github.io/ccentre-ai-v6.html/dashboard.html
```

### Vérification déploiement
Sur GitHub → colonne droite → **Deployments** → `github-pages` avec ✅ vert

---

## ⚠️ Règles Critiques pour Toute Modification Future

### ✅ À TOUJOURS FAIRE
1. **Lire les fichiers avant de modifier** — ne jamais supposer le contenu actuel
2. **Vérifier les accolades JS** : `opens == closes` (diff doit être 0) après chaque modification
3. **Tester la structure HTML** : `<script>` ouverts = `</script>` fermés, jamais de script imbriqué
4. **Préserver la tagline** : "Tu empresa, siempre disponible." — IMMUABLE sans accord explicite
5. **Mode dark = défaut** — toujours tester en dark en premier
6. **loginPage** : toujours ajouter `pointerEvents='none'` immédiatement lors du hide
7. **isDark synchronisation** : `window.isDark = dark` + `try{ isDark=dark; }catch(e){}`

### ❌ À NE JAMAIS FAIRE
1. **Ne jamais modifier** la tagline sans demande explicite de Raphael
2. **Ne jamais utiliser** `document.body.classList` pour le thème (utiliser `html.light`)
3. **Ne jamais supprimer** `overflow-y:auto` sur `.sidebar-nav` (casse la navigation)
4. **Ne jamais imbriquer** un `<script>` dans un autre `<script>`
5. **Ne jamais ajouter** `window.load` pour les inits de charts (utiliser `DOMContentLoaded`)
6. **Ne jamais supprimer** le double listener (onclick + addEventListener) des nav-items
7. **Ne jamais changer** les clés localStorage (`'t'` pour landing, `'dash-t'` pour dashboard)
8. **Ne jamais modifier** le logo SVG sans recréer tous les éléments (C + waveform + CENTRE + AI badge)

### 🐛 Bugs connus et leurs causes
| Bug | Cause | Fix |
|-----|-------|-----|
| Onglets sidebar inactifs | Accolade JS manquante → tout le JS plante | Vérifier `{` == `}` |
| Graphiques vides | `initResumenChart()` appelé avant DOMContentLoaded | Utiliser `setTimeout` 150ms |
| Toggle thème cassé | `document.body.classList` au lieu de `html.classList` | Toujours cibler `html` |
| LoginPage bloque les clics | `display:none` appliqué avec délai | `pointerEvents:none` immédiat |
| Calendly en anglais | Langue du compte Calendly, pas l'URL | Changer dans Settings Calendly |

---

## 📦 Fichiers Livrables Générés

Tous générés dans `/mnt/user-data/outputs/` :
| Fichier | Description |
|---------|-------------|
| `ccentre-ai-v6.html` | Landing page (→ renommer en `index.html`) |
| `dashboard.html` | Dashboard client |
| `pitch-deck-ccentre.md` | Pitch deck 10 slides B2B |
| `scripts-ventas-ccentre.md` | Scripts de vente (demo 30min + cold call) |
| `emails-followup-ccentre.md` | Séquence 3 emails post-demo |
| `politica-privacidad-ccentre.md` | CGU + Politique de confidentialité (droit paraguayen) |

---

## 🔗 Liens Utiles

| Service | URL | Notes |
|---------|-----|-------|
| GitHub repo | `github.com/kemaspues/ccentre-ai-v6.html` | Hébergement |
| Calendly | `calendly.com/ccentrepy` | Compte Santiago |
| Ancien site référence | `ccentreai.github.io` | Textes originaux |
| Chart.js CDN | `cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js` | Dashboard |
| Google Fonts | Bricolage Grotesque + Geist | Typography |

---

## 👥 Équipe

| Personne | Rôle | Notes |
|----------|------|-------|
| Raphael | Entrepreneur français, développeur du projet | Basé à Asunción, Paraguay |
| Santiago Lacarrubba | Associé | Compte Calendly + GitHub ccentreai |

---

*Ce fichier est généré automatiquement par Claude et doit être mis à jour à chaque évolution majeure du projet.*

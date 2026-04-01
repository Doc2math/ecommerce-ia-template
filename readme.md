# 🛒 E-commerce IA — Documentation Complète

## Description du projet

Ce projet est une plateforme e-commerce moderne et intelligente, construite avec les meilleures technologies actuelles. Elle combine un backend robuste (Medusa.js) et un frontend performant (Next.js) avec une couche d'intelligence artificielle intégrée.

### Ce que c'est

Un site e-commerce **complet et fonctionnel** que tu peux adapter pour chaque client en changeant un seul fichier de configuration. Il inclut :

- Une boutique en ligne complète (produits, panier, commandes)
- Un chatbot IA intégré (assistant shopping)
- Un système de recommandations personnalisées
- Plusieurs thèmes visuels interchangeables
- Un dashboard admin pour gérer les produits et commandes
- Un système de paiement via Stripe

### Architecture

```
projet/
├── backend/         → Medusa.js v2 (API, base de données, paiement)
└── frontend/        → Next.js 15 (interface client)
    ├── themes/
    │   ├── default/     → Thème élégant (mode, luxe)
    │   └── dynamique/   → Thème sombre (sport, streetwear)
    └── config/
        └── client.ts    → ★ Fichier de configuration client
```

### Technologies utilisées

| Technologie | Rôle | Version |
|---|---|---|
| Medusa.js | Backend e-commerce | v2 |
| Next.js | Frontend React | v15 |
| PostgreSQL | Base de données | v16 |
| Zustand | Gestion du panier | v4 |
| TypeScript | Langage | v5 |
| Stripe | Paiement en ligne | — |
| Claude API | Chatbot IA | Sonnet |

### Fonctionnalités incluses

**Site client**
- Header sticky avec navigation et panier
- Barre IA active (indicateur en temps réel)
- Hero personnalisable avec badge produit recommandé
- Grille de produits avec tags (IA, Nouveau, Solde)
- Ajout au panier avec animation
- Panier latéral avec barre de livraison offerte
- Section newsletter avec confirmation
- Chatbot IA conversationnel
- Footer complet avec liens

**Dashboard admin (Medusa)**
- Gestion des produits et variantes
- Gestion des commandes
- Gestion des clients
- Gestion des stocks
- Configuration des prix et promotions
- Gestion des livraisons

**Système de thèmes**
- Thème Default : élégant, tons crème, typographie serif
- Thème Dynamique : sombre, orange, streetwear
- Changement de thème en modifiant 2 lignes de code

---

## Prérequis

Avant d'installer le projet, assure-toi d'avoir ces logiciels installés sur ton ordinateur :

- **Node.js** v20 ou supérieur → https://nodejs.org
- **PostgreSQL** v14 ou supérieur → https://postgresql.org
- **Git** → https://git-scm.com
- **VS Code** (recommandé) → https://code.visualstudio.com

Pour vérifier que tout est installé, ouvre un terminal et tape :
```bash
node --version    # doit afficher v20.x.x ou supérieur
npm --version     # doit afficher 10.x.x ou supérieur
psql --version    # doit afficher psql 14.x ou supérieur
```

---

## Installation

### Étape 1 — Créer le dossier du projet

```bash
mkdir mon-ecommerce
cd mon-ecommerce
```

### Étape 2 — Installer le backend Medusa

```bash
npx create-medusa-app@latest backend --no-browser
```

Répondre aux questions :
- Would you like to install the Next.js Starter? → **No**
- Postgres username → **postgres**
- Postgres password → **ton mot de passe PostgreSQL**
- Database name → **postgres**

Attendre 5 à 15 minutes que l'installation se termine.

### Étape 3 — Créer le compte admin Medusa

```bash
cd backend
npx medusa user --email admin@monsite.com --password MonMotDePasse123
```

### Étape 4 — Démarrer le backend

```bash
npm run dev
```

Le backend est disponible sur : `http://localhost:9000`
Le dashboard admin sur : `http://localhost:9000/app`

> Laisser ce terminal ouvert et ouvrir un nouveau terminal pour la suite.

### Étape 5 — Installer le frontend Next.js

Dans un nouveau terminal, depuis le dossier `mon-ecommerce` :

```bash
npx create-next-app@latest frontend --typescript --tailwind --app --no-git
```

Répondre aux questions :
- Which linter? → **ESLint**
- React Compiler? → **No**
- src/ directory? → **No**
- Import alias? → **Yes**
- Alias configuration? → **@/*** (Entrée)

### Étape 6 — Installer les dépendances supplémentaires

```bash
cd frontend
npm install zustand
```

### Étape 7 — Configurer les variables d'environnement

```bash
# Dans le dossier frontend
echo NEXT_PUBLIC_MEDUSA_URL=http://localhost:9000 > .env.local
```

Récupérer la clé API Medusa :
1. Aller sur `http://localhost:9000/app`
2. Se connecter avec les identifiants créés à l'étape 3
3. Cliquer sur **Settings** → **API Keys** → **Create API Key**
4. Choisir **Publishable**, donner un nom, cliquer **Create**
5. Copier la clé (commence par `pk_...`)

```bash
echo NEXT_PUBLIC_MEDUSA_PK=pk_ta_cle_ici >> .env.local
```

### Étape 8 — Créer la structure des fichiers

Créer les dossiers suivants dans `frontend/` :
```
config/
store/
themes/
themes/default/
themes/dynamique/
components/
components/layout/
components/cart/
components/ai/
components/sections/
```

### Étape 9 — Créer les fichiers de configuration

**`config/client.ts`** — Variables du client (couleurs, textes, polices)

**`store/cart.ts`** — Gestion du panier (Zustand)

**`themes/default/`** — Thème élégant :
- `Header.tsx`
- `Hero.tsx`
- `ProductGrid.tsx`
- `Newsletter.tsx`
- `Footer.tsx`

**`themes/dynamique/`** — Thème streetwear :
- `Header.tsx`
- `Hero.tsx`
- `ProductGrid.tsx`
- `Newsletter.tsx`
- `Footer.tsx`

**`components/cart/CartDrawer.tsx`** — Panier latéral

**`components/ai/ChatBot.tsx`** — Assistant IA

**`app/layout.tsx`** — Layout principal

**`app/page.tsx`** — Page d'accueil

**`app/globals.css`** — Styles globaux

### Étape 10 — Démarrer le frontend

```bash
cd frontend
npm run dev
```

Le site est disponible sur : `http://localhost:3000`

---

## Adapter le projet pour un nouveau client

### Étape 1 — Copier le projet

```bash
cp -r mon-ecommerce nouveau-client
cd nouveau-client
```

### Étape 2 — Modifier le fichier de configuration

Ouvrir `frontend/config/client.ts` et changer :

```typescript
export const CLIENT = {
  name:     "NOM DE LA BOUTIQUE",    // ← Changer
  tagline:  "Slogan du client",       // ← Changer

  colors: {
    primary:   "#2c5f3a",   // ← Couleur principale
    secondary: "#c8973a",   // ← Couleur secondaire
    promo:     "#c0392b",   // ← Couleur promotions
  },

  fonts: {
    display:    "Cormorant Garamond",  // ← Police titres
    body:       "DM Sans",             // ← Police texte
    displayUrl: "...",                 // ← URL Google Fonts
  },

  // ... autres paramètres
}
```

### Étape 3 — Changer le thème (optionnel)

Dans `app/layout.tsx` et `app/page.tsx`, changer `default` par `dynamique` :

```tsx
// Thème élégant
import Header from "@/themes/default/Header"

// Thème streetwear
import Header from "@/themes/dynamique/Header"
```

### Étape 4 — Créer une nouvelle base de données

```bash
cd backend
# Modifier DATABASE_URL dans .env avec un nouveau nom de BDD
npx medusa db:create
npx medusa db:migrate
```

### Étape 5 — Saisir les produits

1. Aller sur `http://localhost:9000/app`
2. **Products** → **Create Product**
3. Remplir titre, description, prix, images
4. Publier le produit

---

## Thèmes disponibles

### Default — Élégant / Mode
- Fond crème (#faf8f4)
- Typographie : Cormorant Garamond (titres) + DM Sans (texte)
- Style : luxe, intemporel, mode féminine
- Idéal pour : boutiques mode, accessoires, maison

### Dynamique — Sport / Streetwear
- Fond noir (#0a0a0a)
- Typographie : Bebas Neue (titres) + système (texte)
- Style : urbain, énergique, jeune
- Idéal pour : sport, sneakers, streetwear, gaming

---

## Structure des fichiers finale

```
mon-ecommerce/
│
├── backend/                          → Medusa.js
│   ├── src/
│   │   └── api/store/ai/chat/
│   │       └── route.ts              → API chatbot Claude
│   ├── medusa-config.ts              → Configuration Medusa
│   └── .env                          → Variables d'environnement
│
└── frontend/                         → Next.js
    ├── app/
    │   ├── layout.tsx                → Layout principal
    │   ├── page.tsx                  → Page d'accueil
    │   └── globals.css               → Styles globaux
    │
    ├── config/
    │   └── client.ts                 → ★ Config client (à modifier)
    │
    ├── store/
    │   └── cart.ts                   → Gestion panier Zustand
    │
    ├── themes/
    │   ├── default/                  → Thème élégant
    │   │   ├── Header.tsx
    │   │   ├── Hero.tsx
    │   │   ├── ProductGrid.tsx
    │   │   ├── Newsletter.tsx
    │   │   └── Footer.tsx
    │   └── dynamique/                → Thème streetwear
    │       ├── Header.tsx
    │       ├── Hero.tsx
    │       ├── ProductGrid.tsx
    │       ├── Newsletter.tsx
    │       └── Footer.tsx
    │
    ├── components/
    │   ├── cart/
    │   │   └── CartDrawer.tsx        → Panier latéral
    │   └── ai/
    │       └── ChatBot.tsx           → Assistant IA
    │
    └── .env.local                    → Variables d'environnement
```

---

## Commandes utiles

```bash
# Démarrer le backend
cd backend && npm run dev

# Démarrer le frontend
cd frontend && npm run dev

# Créer un admin Medusa
cd backend && npx medusa user --email email@example.com --password MotDePasse

# Builder le frontend pour la production
cd frontend && npm run build

# Démarrer en production
cd frontend && npm run start
```

---

## URLs importantes

| URL | Description |
|---|---|
| `http://localhost:3000` | Site client |
| `http://localhost:9000/app` | Dashboard admin Medusa |
| `http://localhost:9000/store/products` | API produits |

---

## Prochaines étapes

- [ ] Connecter les vrais produits Medusa au frontend
- [ ] Configurer Stripe pour les paiements réels
- [ ] Créer la page fiche produit
- [ ] Créer la page checkout
- [ ] Connecter le chatbot à Claude API
- [ ] Déployer sur Vercel (frontend) et Railway (backend)

---

*Documentation v1.0 — Projet E-commerce IA*
*Stack : Medusa.js v2 + Next.js 15 + PostgreSQL + Claude API*
Etat du projet:
Ce que on a maintenant :

✅ Un backend Medusa qui tourne sur ton PC
✅ Un frontend Next.js avec 2 thèmes (default + dynamique)
✅ Un panier fonctionnel, un chatbot, une newsletter
✅ Un fichier client.ts pour personnaliser rapidement
✅ Une documentation Word complète

Ce qui reste à faire:

Saisir les vrais produits dans Medusa
Connecter les produits au site (remplacer les emojis par de vraies photos)
Activer le vrai chatbot Claude API
Configurer Stripe pour les paiements réels
Déployer en ligne (Vercel + Railway)
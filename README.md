# LaLoCarte 🗺️

> **La plateforme vivante du territoire local.**  
> Producteurs, événements, paniers, disponibilités — en un seul fil, pour tout le monde, maintenu par la communauté.

[![Licence AGPL-3.0](https://img.shields.io/badge/licence-AGPL--3.0-red.svg)](LICENSE)
[![Open Source](https://img.shields.io/badge/open--source-oui-black.svg)]()
[![Contributions bienvenues](https://img.shields.io/badge/contributions-bienvenues-FF3B00.svg)](CONTRIBUTING.md)
[![Gratuit](https://img.shields.io/badge/gratuit-toujours-black.svg)]()

---

```
██╗      █████╗ ██╗      ██████╗  ██████╗ █████╗ ██████╗ ████████╗███████╗
██║     ██╔══██╗██║     ██╔═══██╗██╔════╝██╔══██╗██╔══██╗╚══██╔══╝██╔════╝
██║     ███████║██║     ██║   ██║██║     ███████║██████╔╝   ██║   █████╗  
██║     ██╔══██║██║     ██║   ██║██║     ██╔══██║██╔══██╗   ██║   ██╔══╝  
███████╗██║  ██║███████╗╚██████╔╝╚██████╗██║  ██║██║  ██║   ██║   ███████╗
╚══════╝╚═╝  ╚═╝╚══════╝ ╚═════╝  ╚═════╝╚═╝  ╚═╝╚═╝  ╚═╝   ╚═╝   ╚══════╝
```

---

## ✊ Pourquoi LaLoCarte existe

Il n'existe pas aujourd'hui de lieu numérique unique pour savoir :

- que Marie-Claire, à 2 km, a **des œufs frais disponibles ce matin**
- que le GAEC Les Coteaux **ouvre les inscriptions aux paniers** cette semaine
- que la **fête du village** a lieu samedi prochain place de l'église
- que la boulangerie Lefèvre fait un **atelier pain** vendredi soir

Ces informations existent. Elles sont dans des groupes Facebook fermés, des affiches papier, des SMS de voisins, des sites de mairie mal tenus.

**LaLoCarte centralise tout ça. Gratuitement. Sans algorithme. Sans publicité. Pour tout le monde.**

---

## 🗺️ Ce que fait LaLoCarte

### Pour les habitants
- Un **feed local** avec tout ce qui se passe près de chez soi
- Une **carte interactive** des producteurs et événements autour de moi
- Des **notifications personnalisées** : je m'abonne à mes producteurs préférés, je reçois une alerte quand un stock est disponible
- Un **agenda de la vie locale** : fêtes, marchés, vide-greniers, concerts, ateliers

### Pour les producteurs (de 6 poules à 10 employés)
- Un **profil producteur gratuit** visible sur la carte
- Publication de **disponibilités en temps réel** : "2 douzaines d'œufs", "8 pots de miel restants"
- Gestion des **paniers hebdomadaires** avec liste d'attente
- Notification automatique envoyée aux abonnés à chaque publication
- Aucune commission, aucun intermédiaire

### Pour les mairies & associations
- Page **commune dédiée** avec agenda officiel
- **Widget intégrable** sur le site de la mairie
- Administration simplifiée des événements locaux
- Instance **auto-hébergeable** sur les serveurs de la collectivité

---

## 📱 Les écrans principaux

| Écran | Description |
|---|---|
| **Feed** | Fil d'actualité local — dispo, événements, nouveaux producteurs |
| **Carte** | Vue map avec pins producteurs + événements |
| **Producteur** | Profil, stocks, paniers, historique |
| **Événement** | Fiche détaillée, partage, ajout calendrier |
| **Notifications** | Centre de gestion des alertes personnalisées |
| **Ajouter** | Publication en 60 secondes — event ou dispo |

---

## 🛠️ Stack technique

LaLoCarte est conçu pour être léger, auto-hébergeable et maintenable par une petite équipe.

```
Frontend Web      → Next.js 14 (App Router)
App Mobile        → React Native (Expo)
Base de données   → PostgreSQL + PostGIS (données géo)
Backend           → Supabase (auth, realtime, storage)
Notifications     → Supabase Realtime + Web Push API
Carte             → MapLibre GL JS (open source, pas de clé Google Maps)
Hébergement       → Vercel (web) + Fly.io (API) — auto-hébergeable
PWA               → Offline-first, installable sur mobile
```

### Pourquoi ces choix ?
- **PostGIS** : requêtes géographiques natives ("événements dans un rayon de 5 km")
- **Supabase** : open source, auto-hébergeable, realtime pour les notifications
- **MapLibre** : 100% open source, aucune dépendance à Google Maps ou Mapbox payant
- **Expo** : une seule codebase pour iOS et Android

---

## 🚀 Lancer LaLoCarte en local

### Prérequis

- Node.js ≥ 18
- PostgreSQL ≥ 15 avec extension PostGIS
- Un compte Supabase (ou instance self-hosted)

### Installation

```bash
# Cloner le repo
git clone https://github.com/lalocarte/lalocarte.git
cd lalocarte

# Installer les dépendances
npm install

# Copier les variables d'environnement
cp .env.example .env.local
# → Remplir SUPABASE_URL, SUPABASE_ANON_KEY, DATABASE_URL

# Initialiser la base de données
npm run db:migrate

# Lancer en développement
npm run dev
```

L'app tourne sur `http://localhost:3000`.

### Lancer l'app mobile (Expo)

```bash
cd mobile
npm install
npx expo start
```

Scanne le QR code avec Expo Go sur ton téléphone.

---

## 📁 Structure du projet

```
lalocarte/
├── app/                  # Next.js App Router
│   ├── (feed)/           # Page d'accueil — feed local
│   ├── carte/            # Vue carte interactive
│   ├── producteurs/      # Profils producteurs
│   ├── evenements/       # Événements locaux
│   └── api/              # API Routes
├── mobile/               # React Native (Expo)
│   ├── screens/
│   └── components/
├── lib/
│   ├── supabase.ts       # Client Supabase
│   ├── geo.ts            # Utilitaires géographiques
│   └── notifications.ts  # Système de notifications
├── supabase/
│   ├── migrations/       # Migrations SQL
│   └── functions/        # Edge Functions
└── public/
```

---

## 🗺️ Roadmap

### v0.1 — MVP (mois 1–2)
- [x] Design system brutaliste + identité LaLoCarte
- [ ] Profil producteur (inscription, photo, localisation)
- [ ] Publication d'une disponibilité
- [ ] Feed local basique (liste)
- [ ] Carte avec pins producteurs

### v0.2 — Notifications (mois 3)
- [ ] Système d'abonnement producteur
- [ ] Notifications Web Push
- [ ] Notifications in-app (realtime)
- [ ] Préférences de notification par catégorie

### v0.3 — Événements (mois 4)
- [ ] Ajout d'un événement par n'importe qui
- [ ] Modération communautaire
- [ ] Agenda par commune
- [ ] Partage d'événement (lien + image générée)

### v0.4 — Paniers (mois 5–6)
- [ ] Système de paniers hebdomadaires
- [ ] Liste d'attente
- [ ] Récapitulatif retrait (lieu, horaire, contact)
- [ ] Historique côté producteur

### v1.0 — App mobile (mois 6+)
- [ ] React Native / Expo
- [ ] Notifications push mobiles
- [ ] Mode hors-ligne (PWA first)
- [ ] Widget mairie intégrable

---

## 🤝 Contribuer

LaLoCarte est un projet communautaire. Toute contribution est la bienvenue — code, design, documentation, traduction, tests terrain.

### Première contribution

1. Fork le repo
2. Crée une branche : `git checkout -b feature/ma-fonctionnalite`
3. Commit : `git commit -m 'feat: ajout de la fonctionnalité X'`
4. Push : `git push origin feature/ma-fonctionnalite`
5. Ouvre une Pull Request

### Types de contributions recherchées

| Type | Description |
|---|---|
| 🐛 **Bug fix** | Corriger un problème existant |
| ✨ **Feature** | Ajouter une fonctionnalité de la roadmap |
| 📖 **Docs** | Améliorer la documentation |
| 🎨 **Design** | Maquettes, icônes, composants UI |
| 🌍 **Terrain** | Tester avec de vrais producteurs locaux |
| 🏛️ **Mairies** | Aider à l'intégration dans une commune |

### Convention de commits

Nous utilisons [Conventional Commits](https://www.conventionalcommits.org/) :

```
feat: nouvelle fonctionnalité
fix: correction de bug
docs: documentation
style: formatage (pas de logique)
refactor: refactoring sans nouvelle feature
test: ajout de tests
chore: tâches de maintenance
```

Consulte [CONTRIBUTING.md](CONTRIBUTING.md) pour plus de détails.

---

## 💬 Communauté

- **Discussions GitHub** → pour les idées, questions, retours
- **Issues** → pour les bugs et demandes de fonctionnalités
- **Discord** → `discord.gg/lalocarte` *(à venir)*

---

## 🏛️ Auto-hébergement pour les mairies

LaLoCarte peut être déployé par une collectivité sur ses propres serveurs. Les données restent sur l'infrastructure de la commune, sous son contrôle.

```bash
# Docker Compose (recommandé)
docker compose up -d

# Variables d'environnement requises
DATABASE_URL=postgresql://...
SUPABASE_URL=https://...
NEXT_PUBLIC_MAP_STYLE=https://...  # Tuiles OpenStreetMap ou IGN
```

Un guide complet d'installation pour les collectivités est disponible dans [docs/auto-hebergement.md](docs/auto-hebergement.md).

---

## ⚖️ Licence

LaLoCarte est distribué sous licence **AGPL-3.0**.

Cela signifie :
- ✅ Utilisation gratuite, y compris commerciale
- ✅ Modification et distribution libres
- ✅ Usage privé et public
- ⚠️ Toute modification distribuée doit rester open source sous AGPL-3.0
- ⚠️ Si vous déployez LaLoCarte comme service réseau, le code source modifié doit être rendu public

Cette licence garantit que LaLoCarte reste un bien commun numérique, pour toujours.

---

## 💛 Remerciements

LaLoCarte est né d'une conviction simple : **le lien entre voisins ne devrait pas appartenir à une plateforme privée**.

Merci à tous ceux qui contribuent — développeurs, designers, producteurs qui testent, habitants qui remontent des retours, mairies qui font confiance au projet.

---

<p align="center">
  <strong>LaLoCarte — fait avec ♥ par la communauté, pour les territoires</strong><br>
  <a href="https://lalocarte.fr">lalocarte.fr</a> · 
  <a href="https://github.com/lalocarte/lalocarte">GitHub</a> · 
  Licence AGPL-3.0
</p>

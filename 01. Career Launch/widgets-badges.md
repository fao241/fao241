# Widgets & badges — README de profil

> **Règle n°1 : privilégier ce qui est hébergé chez toi.** Les widgets servis par une instance publique tierce (Vercel/Heroku) tombent régulièrement en panne, se mettent en pause, ou imposent des limites de requêtes → ton profil affiche une image cassée.
> **Préférer :** badges statiques (`shields.io`, `skillicons`) et outils passant par une **GitHub Action** (le SVG est généré et stocké dans ton dépôt → rien ne casse).

**Légende :**
- ✅ **Fiable** — statique ou généré par Action dans ton dépôt.
- ⚠️ **Instance publique tierce** — peut tomber en panne / être mise en pause ; privilégier l'Action ou le self-host.

---

## 1. Bannière / header

- ✅ *alternative stable :* une **image de bannière** versionnée dans le dépôt (créée une fois, jamais cassée).
- ⚠️ **capsule-render** (bannière dégradée, styles `waving`, `rect`, `egg`…) — https://github.com/kyechan99/capsule-render
- ⚠️ **readme-SVG** (bannières animées : typing, glitch, matrix…) — https://github.com/readme-SVG/readme-SVG-typing-generator

## 2. Texte animé

- ⚠️ **readme-typing-svg** — https://github.com/DenverCoder1/readme-typing-svg
  - Domaine **actuel** : `readme-typing-svg.demolab.com` (les anciens `herokuapp.com` / `vercel.app` ne sont plus à utiliser).

## 3. Badges & icônes

- ✅ **shields.io** — badges paramétrables, styles `flat`, `for-the-badge`… — https://shields.io
- ✅ **skillicons.dev** — grille de technos en une URL — https://skillicons.dev
- ✅ **simple-icons** — SVG de marques — https://github.com/simple-icons/simple-icons
- ✅ **devicon** — logos de langages/outils — https://github.com/devicons/devicon

## 4. Stats GitHub

- ✅ **github-profile-summary-cards** — généré par **Action** (SVG stocké dans le dépôt) — https://github.com/vn7n24fzkq/github-profile-summary-cards
- ⚠️ **github-readme-stats** (Anuraghazra) — l'instance publique `github-readme-stats.vercel.app` est *best-effort* et souvent en panne ; utiliser l'**Action** ou self-host — https://github.com/anuraghazra/github-readme-stats
- ⚠️ **github-readme-streak-stats** — domaine **actuel** : `streak-stats.demolab.com` — https://github.com/DenverCoder1/github-readme-streak-stats
- ⚠️ **github-readme-activity-graph** — instance publique tierce — https://github.com/Ashutosh00710/github-readme-activity-graph
- ⚠️ **github-profile-trophy** — **instance publique hors service** (Vercel a suspendu le service) ; nécessite un self-host — https://github.com/ryo-ma/github-profile-trophy

## 5. Animations (toutes via GitHub Action → ✅ fiable)

- **Platane/snk** — serpent qui parcourt le graphe de contributions — https://github.com/Platane/snk
- **github-profile-3d-contrib** — graphe de contributions 3D — https://github.com/yoshi389111/github-profile-3d-contrib
- **pacman-contribution-graph** — Pac-Man sur le graphe — https://github.com/abozanona/pacman-contribution-graph
- **recent-activity** (Readme-Workflows) — activité récente dans le README — https://github.com/Readme-Workflows/recent-activity
- **blog-post-workflow** — dernier article de blog — https://github.com/gautamkrishnar/blog-post-workflow

## 6. Extras

- **github-profile-views-counter** — compteur de visites — https://github.com/antonkomarev/github-profile-views-counter
- **spotify-github-profile** — morceau en cours — https://github.com/kittinan/spotify-github-profile

## 7. Générateurs / éditeurs visuels

- **github-profile-readme-generator** — https://github.com/rahuldkjain/github-profile-readme-generator
- **GitAscii** — éditeur visuel de widgets — https://github.com/Igorcbraz/GitAscii

---

## À éviter

- Les URLs **`*.herokuapp.com`** (offre gratuite Heroku arrêtée) → ne fonctionnent plus.
- Les instances publiques **surchargées** comme widget principal de ton profil : préfère une version **Action** ou **self-host**.

## Syntaxe (rappel, un seul exemple)

Un badge cliquable = une image dans un lien :
```
[![alt](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
```

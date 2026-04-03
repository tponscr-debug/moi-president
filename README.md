# MOI PRÉSIDENT 🇫🇷

> Deviens Président de la République française du jour au lendemain. Dirige le pays. Chaque décision a des conséquences réelles — chiffrées, sourcées, implacables.

## Concept

Un jeu de simulation présidentielle basé sur l'actualité française en temps réel. L'IA scrape les vraies news, calcule les conséquences de tes décisions à partir d'études publiques sérieuses (INSEE, OCDE, Eurostat, data.gouv.fr), et te les renvoie le lendemain. Pas d'opinions. Des faits.

**Le gameplay en une phrase :** chaque matin, tu reçois ton briefing présidentiel sur Telegram. Tu réponds dans la journée. Le lendemain, tu vis les conséquences.

## Fonctionnement

### Le cycle quotidien
1. **3h00** — cron job : scrape les actualités, rafraîchit les données macro, génère le dossier du jour via Gemini
2. **7h30** — message Telegram : *"Monsieur le Président, votre briefing du [date] est prêt"*
3. **Dans la journée** — tu ouvres le dashboard web, consultes ton dossier (2-4 décisions), réponds
4. **Le lendemain** — les conséquences arrivent dans le briefing suivant, chiffrées et sourcées

### Actions disponibles
- Prendre des **décisions politiques** sur les événements du jour
- **Changer un ministre** (coût politique, risque médiatique)
- **Communiquer** — déclaration, conférence de presse (impact popularité)
- **Allouer le budget** entre ministères
- **Répondre à une crise** (événement exceptionnel)

### Indicateurs gérés
| Domaine | KPIs |
|---------|------|
| Popularité | Cote de confiance par camp politique |
| Économie | Croissance, dette, chômage, pouvoir d'achat |
| Social | Inégalités, santé, éducation |
| Sécurité | Criminalité, terrorisme, défense |
| International | Diplomatie, Europe, conflits |
| Environnement | CO2, politiques climatiques |
| Finances | Budget, déficit, dépenses par ministère |

## Architecture

```
Backend (FastAPI / Python)          Frontend (Next.js)
├── game_engine.py                  ├── /dashboard     — KPIs + graphiques
├── rag_engine.py                   ├── /decisions     — historique + sources
├── gemini_client.py (BYOK)        ├── /gouvernement  — ministres
├── news_scraper.py                 ├── /config        — clé Gemini + Telegram
├── telegram_bot.py                 └── /onboarding   — cérémonie de nomination
└── indicators.py

Vector DB : Qdrant (local)
Sources : data.gouv.fr · INSEE · OCDE · Eurostat · Presse FR (RSS)
DB joueur : SQLite → Postgres (si multi-joueurs)
Deploy : Hetzner Main (77.42.31.88)
```

## Principes

- **100% sourcé** — chaque conséquence cite l'étude qui la justifie
- **BYOK** — le joueur apporte sa propre clé API Gemini, le jeu est gratuit
- **Slow gaming** — un dossier par jour, pas de session imposée
- **Objectif** — aucune orientation politique dans le moteur, seulement des données publiques

## Stack

- **Backend** : Python 3.12 · FastAPI · LangChain · sentence-transformers
- **Vector DB** : Qdrant
- **LLM** : Gemini (BYOK)
- **Frontend** : Next.js 14 · TypeScript · Tailwind
- **Canal de jeu** : Telegram Bot
- **Déploiement** : Hetzner (nginx · systemd)

## Status

🟡 En cours de design — brainstorming validé, implémentation à venir.

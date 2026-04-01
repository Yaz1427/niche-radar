# 🎯 NicheRadar

**NicheRadar** est un outil local de veille marché et de recherche de niches e-commerce, construit avec Python et Streamlit.

Il agrège des données publiques provenant de **Google Trends**, **Reddit**, **Amazon Best Sellers** et **AliExpress** pour scorer automatiquement les niches et identifier les opportunités émergentes avant qu'elles ne saturent.

---

## ✨ Fonctionnalités

- 📊 **Moteur de NicheScore** — score pondéré combinant croissance, buzz Reddit, vélocité Amazon et opportunité géographique
- 📈 **Prévisions de tendances** — forecasting via Facebook Prophet avec intervalles de confiance
- 🌍 **Carte des opportunités géo** — détection du lag US → EU/MENA pour identifier les niches émergentes
- 🔔 **Watchlist & Alertes** — surveillance automatique hebdomadaire de mots-clés
- 🕐 **Cache intelligent** — TTL par source, fallback automatique si API hors ligne
- ⚠️ **Fiabilité transparente** — chaque métrique affiche son score de confiance et sa significativité statistique

---

## 🛠️ Stack technique

| Composant | Technologie |
|---|---|
| Interface | Streamlit + Plotly |
| Tendances Google | pytrends |
| Reddit | PRAW (read-only) |
| Amazon | requests + BeautifulSoup |
| Prévisions | Facebook Prophet |
| NLP | scikit-learn (TF-IDF) |
| Stockage | SQLite (local) |
| Stats | scipy, numpy |

---

## 🚀 Installation

```bash
git clone https://github.com/Yaz1427/niche-radar.git
cd niche-radar
pip install -r requirements.txt
```

### Configuration Reddit (PRAW)

1. Crée une application sur [reddit.com/prefs/apps](https://www.reddit.com/prefs/apps) (type : **script**)
2. Copie le fichier d'exemple et remplis tes credentials :

```bash
cp .env.example .env
```

```env
REDDIT_CLIENT_ID=your_client_id
REDDIT_CLIENT_SECRET=your_client_secret
REDDIT_USER_AGENT=NicheRadar/1.0 by u/your_username
REDDIT_USERNAME=your_username
REDDIT_PASSWORD=your_password
```

### Lancement

```bash
streamlit run app.py

# Mode démo (sans connexion API) :
streamlit run app.py -- --demo
```

---

## 📁 Structure du projet

```
niche-radar/
├── app.py                      # Point d'entrée Streamlit
├── collectors/
│   ├── google_trends.py        # Wrapper pytrends
│   ├── reddit_collector.py     # Collecteur Reddit (read-only via PRAW)
│   ├── amazon_scraper.py       # Best Sellers Amazon
│   └── aliexpress.py           # Tendances AliExpress
├── analysis/
│   ├── scorer.py               # Calcul du NicheScore
│   ├── forecaster.py           # Prévisions Prophet
│   ├── validator.py            # Validation & fiabilité des données
│   └── geo_analyzer.py         # Analyse géographique
├── storage/
│   └── database.py             # Cache SQLite + watchlist
├── pages/
│   ├── dashboard.py
│   ├── keyword_explorer.py
│   ├── product_trends.py
│   ├── geo_analysis.py
│   └── watchlist.py
├── utils/
│   ├── retry.py                # Retry + backoff exponentiel
│   ├── normalizer.py           # Normalisation, z-score, déduplication
│   └── logger.py
├── .env.example
├── requirements.txt
└── README.md
```

---

## ⚖️ Usage & Éthique

- L'application fonctionne **entièrement en local** sur la machine de l'utilisateur
- L'accès Reddit est **strictement en lecture seule** via l'API officielle PRAW
- Aucune donnée Reddit n'est redistribuée, revendue ou exposée publiquement
- Les appels API sont limités en fréquence et mis en cache localement pour minimiser la charge serveur
- Aucun post, vote, commentaire ou interaction n'est effectué sur Reddit

---

## 📄 Licence

MIT License — usage personnel uniquement.

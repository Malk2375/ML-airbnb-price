# 🏠 Prédiction du prix Airbnb à Paris

> **IPSSI M1 · M102 · Projet final**
> Équipe : [Votre prénom] & [Prénom camarade]

---

## 🎯 Problème métier

Une plateforme de location courte durée veut aider ses hôtes parisiens à **fixer le bon prix de nuitée**.
Un prix trop bas → manque à gagner. Trop haut → l'annonce ne se loue pas.

Notre modèle prédit le prix optimal d'une nuitée à partir des caractéristiques du logement (quartier, type, capacité, équipements, etc.).

---

## 📦 Dataset

- **Source** : [Inside Airbnb — Paris](https://insideairbnb.com/get-the-data/)
- **Fichier** : `listings.csv.gz` (version détaillée, ~75 colonnes)
- **Volume** : ~70 000 logements parisiens
- **Cible** : `price` (nuitée en €)

> ⚠️ Le fichier CSV n'est pas versionné (trop lourd). Voir section "Installation" pour le télécharger.

---

## 🛠️ Stack technique

| Outil | Usage |
|---|---|
| Python 3.11 | Langage |
| pandas / numpy | Manipulation données |
| scikit-learn | Pipeline, modèles, évaluation |
| matplotlib / seaborn | Visualisation |
| joblib | Sérialisation du modèle |

---

## 🚀 Installation

### Avec Anaconda (Jupyter Notebook)
```bash
git clone https://github.com/Malk2375/ML-airbnb-price.git
cd ML-airbnb-price

# Créer l'environnement
conda create -n airbnb python=3.11 -y
conda activate airbnb
pip install -r requirements.txt

# Télécharger le dataset
# → https://insideairbnb.com/get-the-data/ → Paris → listings.csv.gz
# → Décompresser dans data/listings.csv

# Lancer Jupyter
jupyter notebook
# ou
python -m jupyter notebook
```

### Avec uv
```bash
uv venv
uv pip install -r requirements.txt
```

---

## ▶️ Exécution

Ouvrir et exécuter dans l'ordre :

```
notebooks/AirbnbParis.ipynb
```

**Cellule démo** (dernière cellule du notebook) :
```python
# Prédire le prix pour un nouveau logement
sample = {
    "neighbourhood_cleansed": "Montmartre",
    "room_type": "Entire home/apt",
    "accommodates": 4,
    "bedrooms": 2,
    "has_wifi": True,
    "has_balcony": True,
    # ...
}
model.predict(pd.DataFrame([sample]))
```

---

## 📊 Résultats

| Modèle | R² (CV 5-fold) | MAE (€) |
|---|---|---|
| LinearRegression (baseline) | - | - |
| Ridge | - | - |
| RandomForestRegressor | - | - |

> *Tableau à compléter après entraînement*

---

## ⚠️ Limites assumées

- Le dataset est un snapshot à une date donnée → les prix saisonniers ne sont pas capturés
- Les photos et le texte de l'annonce ne sont pas exploités (NLP possible en perspective)
- Les outliers de prix (> 1 000 €/nuit) sont filtrés → le modèle n'est pas fiable sur ce segment

## 🔭 Perspectives

- Intégrer la saisonnalité (prix par mois)
- Feature engineering sur le texte (`description`, `name`)
- Déploiement via API FastAPI (Bonus A)

---

## 📁 Structure du projet

```
ML-airbnb-price/
├── data/               ← (gitignored) listings.csv ici
├── notebooks/
│   └── AirbnbParis.ipynb
├── outputs/
│   ├── model.joblib
│   └── metrics.json
├── decisions.md        ← journal de décisions
├── requirements.txt
├── README.md
└── .gitignore
```

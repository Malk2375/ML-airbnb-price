# 📓 Journal de décisions techniques

> Conformément aux conseils du projet : noter les choix techniques au fil de l'eau.
> Ce fichier sera la matière première du README et de la soutenance.

---

## 🗓️ Jeudi 22 mai — Démarrage

### Décision 1 — Sujet : Airbnb Paris (Sujet 1)
**Contexte** : Sujet imposé n°1.
**Décision** : Accepté.

---

### Décision 2 — Dataset : `listings.csv.gz` version détaillée
**Contexte** : Inside Airbnb propose deux versions : résumé (~16 col) et détaillée (~75 col).
**Décision** : Version détaillée pour accéder aux amenities, host_response_rate, reviews.
**Risque assumé** : Plus de colonnes = plus de nettoyage, mais beaucoup plus de signal.

---

### Décision 3 — Cible : `log1p(price)` via `TransformedTargetRegressor`
**Contexte** : La distribution de `price` est skewed à droite (queue longue sur les prix élevés).
**Décision** : Appliquer `log1p` sur la cible via `TransformedTargetRegressor(regressor=..., func=np.log1p, inverse_func=np.expm1)`.
**Pourquoi** : Réduit le poids des outliers, stabilise la variance → améliore R² et MAE.

---

## Template pour les décisions suivantes

### Décision N — [Titre]
**Contexte** : ...
**Options envisagées** : ...
**Décision retenue** : ...
**Pourquoi** : ...
**Résultat observé** : ...

---

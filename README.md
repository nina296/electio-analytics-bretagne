# Electio-Analytics Bretagne

Preuve de concept (POC) de prévision des tendances électorales à partir d'indicateurs socio-économiques publics, réalisée dans le cadre de la MSPR TPRE813 — Big Data et Analyse de données (Bloc 3, Certification RNCP 35584).

## Contexte

Electio-Analytics est une start-up fictive de conseil stratégique en campagnes électorales. Ce projet construit une preuve de concept permettant de prédire le groupe politique arrivé en tête dans une commune bretonne, à partir de son profil socio-économique et de son historique électoral.

**Périmètre** : région Bretagne (Côtes-d'Armor, Finistère, Ille-et-Vilaine, Morbihan), environ 1 200 communes.

**Résultat clé** : modèle de classification (Régression Logistique) atteignant 78,9 % d'accuracy sur des communes jamais vues à l'entraînement, soit 30 points au-dessus d'une prédiction triviale.

## Pipeline

1. **ETL** (`notebooks/ETL.ipynb`) : collecte de 13 fichiers sources publics (résultats électoraux 2017/2022, démographie, emploi, éducation, revenus, criminalité, entreprises, vie associative), nettoyage et fusion en `dataset_bretagne.csv` (2 440 lignes : 1 233 communes en 2017 + 1 207 en 2022).
2. **Base SQL** (`notebooks/SQL.ipynb`) : structuration en base SQLite normalisée (`electio_analytics.db`, 4 tables : `commune`, `indicateurs`, `resultat_electoral`, `groupe_politique`).
3. **Analyse exploratoire** (`notebooks/Analyse_exploratoire.ipynb`) : cartes, matrice de corrélation, distributions — identification des indicateurs les plus discriminants.
4. **Modélisation** (`notebooks/modele_ml.ipynb`) : mise au format large (`dataset_final.csv`, 1 207 communes), comparaison de 5 modèles de classification (Random Forest, Gradient Boosting, Régression Logistique, KNN, SVM), sélection du modèle final, production de scénarios prédictifs (probabilités, cartes de chaleur, courbes temporelles, projection à 1/2/3 ans).

## Sources de données

- [Résultats électoraux — data.gouv.fr](https://www.data.gouv.fr/fr/pages/donnees-des-elections/)
- [Données de sécurité — data.gouv.fr](https://www.data.gouv.fr/fr/pages/donnees-securite/)
- [Données emploi — data.gouv.fr](https://www.data.gouv.fr/datasets/search?q=emploi)
- [INSEE — base communale](https://www.insee.fr)

Les fichiers bruts ne sont pas versionnés sur ce dépôt (voir `.gitignore`) ; ils sont téléchargeables depuis les liens ci-dessus.

## Reproduire le pipeline

```bash
pip install pandas numpy matplotlib seaborn geopandas scikit-learn jupyter
```

Exécuter les notebooks dans l'ordre : `ETL.ipynb` → `SQL.ipynb` → `Analyse_exploratoire.ipynb` → `modele_ml.ipynb`.

## Livrables

| Livrable | Emplacement |
|---|---|
| Dossier de synthèse | `reports/Dossier_synthese_Electio_Analytics.docx` |
| Jeu de données nettoyé et normalisé | `data/processed/electio_analytics.db` |
| Code commenté | `notebooks/` |
| Support de soutenance | `reports/` |

## Équipe

[Noms des membres de l'équipe]

## Licence

Projet pédagogique réalisé dans le cadre de la certification RNCP 35584 — EPSI.
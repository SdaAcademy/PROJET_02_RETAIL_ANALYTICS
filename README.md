# PROJET 02 — RETAIL SALES ANALYTICS
## Mission professionnelle : diagnostiquer les ventes d'un retailer électronique (2019)

**Rôle :** Data Analyst Junior, équipe Commerciale & BI  
**Environnement :** MySQL / Railway — base `retail_db`, table brute `raw_sales`  
**Outils :** DBeaver ou MySQL Workbench, SQL, Excel/Power BI  
**Données :** 186 850 lignes attendues dans `retail_db.raw_sales`.

## 1. Brief de la Direction

L'entreprise vend des produits électroniques. La Direction Commerciale souhaite comprendre la performance 2019, mais les fichiers reçus sont des exports opérationnels imparfaits. Votre mission est de transformer la table brute en analyse défendable, puis de proposer des décisions concrètes.

Vous avez accès à la table `retail_db.raw_sales` en lecture seule. Les données brutes doivent être conservées telles quelles. Vous ne devez pas créer de tables, corriger la source ni modifier la base partagée. Les transformations et analyses doivent être réalisées dans vos scripts SQL locaux, vues temporaires si autorisées, ou outils analytiques externes.

## 2. Source et colonnes

- `raw_id` : identifiant technique de chargement ;
- `order_id` : identifiant de commande sous forme texte ;
- `product` : libellé du produit ;
- `quantity_ordered` : quantité sous forme texte ;
- `price_each` : prix unitaire sous forme texte ;
- `order_date` : date/heure sous forme texte ;
- `purchase_address` : adresse d'achat ;
- `source_file` : fichier source ;
- `loaded_at` : horodatage du chargement.

Les anomalies sont intentionnelles : lignes vides, en-têtes répétés, champs numériques invalides, dates mal formées et doublons possibles. L'adresse est une localisation de transaction, pas un identifiant client fiable.

## 3. Missions

### Mission 01 — Comprendre les données
- vérifier la volumétrie ;
- examiner un échantillon ;
- documenter le grain ;
- décrire chaque champ et son type source ;
- identifier les risques d'analyse.

### Mission 02 — Data Quality & règles d'éligibilité
Mesurer :
- lignes vides ou identifiants manquants ;
- répétitions de l'en-tête ;
- valeurs non numériques dans quantité/prix ;
- dates invalides ;
- prix ou quantités nuls/négatifs ;
- doublons exacts et doublons métier potentiels ;
- part des lignes exclues par chaque règle.

Définissez une règle `ELIGIBLE / EXCLUDED` explicite. Ne supprimez jamais les anomalies de la table partagée. Documentez le nombre de lignes retenues et exclues.

### Mission 03 — Construire un jeu analytique propre
Sans modifier la base :
- proposez une transformation SQL reproductible qui normalise les textes, convertit quantité/prix/date, exclut les lignes invalides et retire les doublons selon une règle justifiée ;
- définissez le grain de l'analyse : une ligne de produit dans une commande ;
- créez un script local `02_cleaning_logic.sql` avec des CTE lisibles ;
- justifiez chaque règle et son impact.

### Mission 04 — KPI commerciaux
Calculez :
- chiffre d'affaires (quantité × prix unitaire) ;
- quantité vendue ;
- nombre de commandes distinctes ;
- prix unitaire moyen, en distinguant moyenne simple et moyenne pondérée si utile ;
- panier moyen (CA / commandes), en explicitant la définition ;
- chiffre d'affaires et volume par mois, produit et ville ;
- contribution (%) de chaque mois et produit au total ;
- top/bottom produits et saisonnalité.

### Mission 05 — Analyse de la ville et de l'adresse
- extrayez la ville à partir de l'adresse en documentant les hypothèses ;
- contrôlez les adresses incomplètes ;
- classez les villes selon CA et volume ;
- ne prétendez pas identifier des clients uniques à partir de l'adresse ;
- proposez les données supplémentaires qu'il faudrait collecter pour analyser les clients.

### Mission 06 — Recommandations de Direction
À partir des résultats, proposez :
- 5 à 8 insights, chacun avec une mesure vérifiable ;
- 5 recommandations hiérarchisées ;
- les risques d'interprétation et les données manquantes ;
- un dashboard Excel ou Power BI.

## 4. Livrables obligatoires

1. `01_data_quality_audit.sql`
2. `02_cleaning_logic.sql`
3. `03_kpi_sales.sql`
4. `04_product_analysis.sql`
5. `05_monthly_city_analysis.sql`
6. `06_executive_summary.md`
7. `07_recommendations.md`
8. `dashboard/` (capture ou fichier si autorisé)
9. `README.md` décrivant les règles, le grain et les limites.

## 5. Évaluation — 100 points

| Critère | Points |
|---|---:|
| Data Quality et quantification des exclusions | 20 |
| Logique de nettoyage, typage et dédoublonnage | 20 |
| SQL : CTE, fonctions, agrégations et lisibilité | 25 |
| KPI et interprétation commerciale | 15 |
| Dashboard, synthèse et recommandations | 15 |
| GitHub, traçabilité et sécurité | 5 |

## 6. Contraintes professionnelles

- Ne jamais modifier la table `raw_sales`.
- Ne pas compter les lignes d'en-tête comme des ventes.
- Ne pas additionner un prix unitaire comme s'il s'agissait d'un chiffre d'affaires.
- Définir explicitement le traitement des doublons.
- Ne pas utiliser `COUNT(*)` comme nombre de commandes : une commande peut contenir plusieurs produits.
- Ne pas traiter l'adresse comme un identifiant client.
- Ne pas annoncer un insight sans requête, résultat ou visualisation permettant de le vérifier.

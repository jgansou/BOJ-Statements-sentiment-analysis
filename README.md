# BOJ-Statements-sentiment-analysis

## Motivations
Dans le monde en rapide évolution de la finance et de l'économie, l'accès à des informations actualisées et pertinentes est crucial pour les traders, gérants, les analystes et les investisseurs. Les déclarations des banques centrales jouent un rôle significatif dans la modélisation des attentes du marché et l'orientation des décisions économiques à l'échelle mondiale. Cependant, le volume considérable de données et la fréquence des publications peuvent rendre difficile l'analyse rapide et efficace de ces informations précieuses.

L'impact de la Banque du Japon (BOJ) sur les marchés financiers est notable, particulièrement via sa politique de contrôle de la courbe des taux. Cette stratégie régule les taux d'intérêt à court et à long terme. Cela souligne l'importance des politiques des banques centrales, comme celle de la BOJ, qui façonnent les marchés financiers en influençant les taux d'intérêt et les prévisions d'inflation.


Le projet présent vise à développer une solution automatisée qui peut non seulement collecter les déclarations (statements) de la BOJ à partir de leur site Web mais aussi analyser le sentiment inhérent à ces textes. En utilisant des techniques de web scraping avancées et d'analyse de sentiments, ce projet aspire à transformer un flux continu de données en insights actionnables, offrant ainsi un avantage stratégique.

Nous utilisons deux méthodes pour mesurer les sentiments dans les déclarations de la BOJ. La première repose sur le dictionnaire empirique d'analyse de sentiment de Loughran-McDonalds (voir *Loughran, Tim and McDonald, Bill, When is a Liability not a Liability? Textual Analysis, Dictionaries, and 10-Ks (March 4, 2010). Journal of Finance, Forthcoming, Available at SSRN: https://ssrn.com/abstract=1331573*). L'article de Tim Loughran et Bill McDonald, "When is a Liability not a Liability? Textual Analysis, Dictionaries, and 10-Ks", propose une méthode novatrice pour l'analyse des sentiments dans les rapports financiers, remettant en question les dictionnaires généraux et plaidant pour un dictionnaire adapté au contexte financier qui reflète mieux la complexité et la spécificité du langage de la finance.

 La deuxième méthode utilise des méthodes d'apprentissage supervisé notamment le `TfidfVectorizer` pour la conversion de texte en caractéristiques numériques et `ElasticNet`, une régression régularisée qui combine les pénalités L1 et L2, pour la prédiction des sentiments dans les textes (voir *Hui Zou, Trevor Hastie, Addendum: Regularization and Variable Selection Via the Elastic Net, Journal of the Royal Statistical Society Series B: Statistical Methodology, Volume 67, Issue 5, November 2005, Page 768, https://doi.org/10.1111/j.1467-9868.2005.00527.x*).

Nous reprenons essentiellement les codes vus en cours notamment ceux des notebooks `47_Central_bank_sentiment` et `Text_processing` (voir Sylvain Champonnois, https://github.com/schampon/skfin).

## Données utilisées

Les données utilisées pour le projet sont les statements de la BOJ de 1999 à 2024. Les données sont disponibles sur le site de la BOJ: https://www.boj.or.jp/en/mopo/mpmdeci/state_all/index.htm.

Il s'agit de données textuelles stockées soit dans des pdfs, soit sur le site. Pour récupérer les données.

La récupération des déclarations de la Banque du Japon a été effectuée grâce à un processus méticuleux. Tout d'abord, la fonction `get_boj_statements_urls` a été utilisée pour rassembler les URL des documents depuis le site de la BOJ, remontant à 1999. Cette fonction a parcouru les pages des archives annuelles, extrayant les liens vers les déclarations monétaires, tout en associant chaque document à sa date de publication.

Ensuite, pour nettoyer le contenu textuel extrait des fichiers HTML, la fonction `clean_html_text` a été déployée, éliminant les sections de référence non pertinentes pour l'analyse.

Pour les documents en format PDF, la fonction `extract_text_from_pdf` a été mise en place pour extraire le texte.

Finalement, la fonction `get_texts_from_urls` a consolidé le processus en extrayant le contenu textuel à partir des URLs rassemblées, produisant une base de données organisée avec les dates de publication et les textes associés. Cet ensemble de données a ensuite servi de fondement à l'analyse subséquente.

Ces fonctions s'inspirent essentiellement des fonctions utilisées dans le cours pour la récupération des données.

##  Conclusion

L'étude a montré que l'analyse de sentiment peut fournir des informations précieuses sur la perception du marché. Les techniques de traitement de texte telles que TF-IDF couplées avec des modèles de régression Elastic Net ont permis d'identifier des mots clés significatifs qui ont un impact positif ou négatif sur les rendements du marché. De plus, l'application de l'analyse en composantes principales (PCA) a aidé à détecter des regroupements temporels dans les données, suggérant des périodes distinctes de l'économie japonaise et de la politique monétaire.

Les résultats visuels, à travers les graphiques de sentiment et les marqueurs sur le Nikkei 225, illustrent comment le sentiment extrait des communications de la BOJ est un indicateur potentiel des réactions du marché.

## Limites de l'étude
Bien que l'étude ait apporté des éclairages intéressants, il existe plusieurs limites à prendre en compte :

 **Biais de Sélection** : La sélection de l'indice Nikkei 225 comme seul indicateur des réactions du marché peut introduire un biais. Il aurait été plus intéressant peut-être choisir le jpy pour de meilleurs résultats.

**Complexité du Langage** : Les dictionnaires de sentiment, même spécialisés comme celui de Loughran-McDonald, peuvent ne pas saisir entièrement la complexité et la subtilité du langage financier. Les nuances contextuelles peuvent être perdues dans l'analyse automatisée.


**Limitations Techniques** : Les modèles de machine learning utilisés sont aussi bons que les données sur lesquelles ils sont entraînés. Les erreurs de données, le surajustement et la généralisation des modèles sont des problèmes courants qui peuvent affecter les résultats. Par ailleurs, notre analyse manque de test statistique des différentes hypothèses et conclusions tirées.

## Bibliographie

- *Loughran, Tim and McDonald, Bill, When is a Liability not a Liability? Textual Analysis, Dictionaries, and 10-Ks (March 4, 2010). Journal of Finance, Forthcoming, Available at SSRN: https://ssrn.com/abstract=1331573*). L'article de Tim Loughran et Bill McDonald, "When is a Liability not a Liability? Textual Analysis, Dictionaries, and 10-Ks"*
- *Hui Zou, Trevor Hastie, Addendum: Regularization and Variable Selection Via the Elastic Net, Journal of the Royal Statistical Society Series B: Statistical Methodology, Volume 67, Issue 5, November 2005, Page 768, https://doi.org/10.1111/j.1467-9868.2005.00527.x*
- Sylvain Champonnois, https://github.com/schampon/skfin

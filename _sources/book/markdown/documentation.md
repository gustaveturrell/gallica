# Les enjeux dans le développement d'un jeux de donnée autour des fonds numérisés de la Bibliothèque Nationale de France

## Contextualisation  

Dans le cadre de l'appel à projet émis par la Bibliothèque Nationale de France (*BnF*) et s'inscrivant dans le projet [France Relance 2030](https://www.economie.gouv.fr/france-2030), il est demandé aux prestataires de mettre en place une solution de fouille d'images autour des documents présents sur [Gallica Images](https://gallica.bnf.fr/). Aujourd'hui il est possible d'indexer des images sur Gallica Images grâce aux métadonnées qui leur sont associées. Ces métadonnées sont issues des archives dont elles proviennent, elles sont donc purement descriptives. Chaque métadonnée concerne un document et ce document peut être associé à plusieurs images. Dans le cas, par exemple, d'une collection de photographies sur pellicule, l'ensemble des images partagent la même métadonnée, ce qui nous donne des informations sur l'ensemble de collection mais pas à l’échelle des images.
Tout l'enjeu de cet appel à projet est d'incorporer des briques d'intelligence artificielle à l'infrastructure déjà préexistante afin de développer une nouvelle chaîne de traitement automatique des documents, basée sur une approche de segmentations et de classifications. L'objectif est d'extraire de nouvelles métadonnées pour l'image en complément de celle déjà présente, afin de permettre une meilleure exposition des documents, leurs croisement et la fouille d'images.


```{figure} assets/research-gallica.png
:width: 500px
:align: center
Recherche avancée aujourd'hui sur [Gallica Images](https://gallica.bnf.fr/services/engine/search/advancedSearch/)

```

```{note}
*Il est à noté que le prestaire est libre de proposer les technologies qui lui semble en adéquation avec l'enjeux exposé précédemment.*
```

Mon stage s'inscrit dans la phase de sélection des prestataires. Pour évaluer les modèles des différents prestataires, il est essentiel de faire un inventaire le plus factuel possible des données qu’ils devront automatiser, notamment à des fins d'évaluation autour d'un ensemble de mesures de la qualité. Cet inventaire et ces mesures de qualité prendront la forme d'un jeu de données, qui se voudra représentatif sur le nombre et le type de documents présents sur Gallica Images.


L'organisation du marché est découpé de la façon suivante :

1. **Tranche ferme** : Développement, paramétrage et mise en place d'une version initiale du système d'identification et d'indexation des illustrations, initialisation sur la collection Images (estampes, dessins et photographies, *1.4 millions de pages* environ) dont une prestation de livraison.
2. **Tranche optionnelle 1** : Développement complémentaire - Monographies imprimées avec traitements associés d'un échantillon de tests de *20 000 pages* de la collection dont une prestation de livraison.
3. **Tranche optionnelle 2** : Développement complémentaire - Périodiques avec traitements associés d'un échantillon de test de *20 000 pages* de la collection dont une prestation de livraison.
4. **Tranche optionnelle 3** : Développement complémentaire - Manuscrit avec traitements associés d'un échantillon de tests de *20 000 pages* de la collection dont une prestation de livraison.
5. **Tranche optionnelle 4** : Développement complémentaire - Documents spécialisés (partition musicales, cartes et plans, monnaies) avec traitements associés d'un échantillon de tests de *20 000 pages* de la collection dont une prestation de livraison

Ce premier jeu de données s'articulera donc avec la tranche ferme, autour de trois types de documents : **les estampes, le dessin et la photographie**.

## Création du jeu de donnée

Comme évoqué précédemment, la création d'un jeu de données permettra à la BnF de mettre à disposition un ensemble de documents ainsi que leurs métadonnées aux différents prestataires. Afin qu'ils puissent évaluer conjointement la qualité des modèles de segmentations et de classifications. Le jeu de données mettra à disposition deux grands types de données.

- Des données structurées et riches sémantiquement à travers les métadonnées associées à chaque document :

```{code-block} python
{'title': ['Vallée du Gave - Vue prise du Parc à Pau / J. A.'], 
'creator': ['J. A.. Fonction indéterminée'], 
'subject': ['Photographie stéréoscopique -- 19e siècle', 'Gave de Pau, Vallée du (France) -- 19e siècle -- Photographies'], 
'description': ['Appartient à l’ensemble documentaire : PrnS001'], 
'relation': ['Notice du catalogue : http://catalogue.bnf.fr/ark:/12148/cb449506875'], 
'identifier': ['http://gallica.bnf.fr/ark:/12148/btv1b10584517b'], 'rights': ['domaine public'], 
'type': ['image fixe', 'photographie'], 
'language': ['Sans contenu linguistique'], 
'date': ['18??'], 
'format': ['photographie stéréoscopique, 16,8 x 8,5 cm', 'image/jpeg', 'Nombre total de vues :  1'], 'source': ['Archives et bibliothèques Pau Béarn Pyrénées, PHA152 (469)']}
```

***

- Des données semi-structurées et faibles sémantiquement à travers l'image car, au-delà de la structure de celle-ci (hauteur, largeur, nombre de canaux (couleurs, noir et blanc)), il est difficile d'obtenir des informations sémantiques pertinentes sans l'aide d'un modèle d’apprentissage automatique.

```{figure} assets/btv1b105845b.jpeg
:width: 500px
:align: center
Exemple de donnée semi-structurée et faible sémantiquement
btv1b10584517b | Vallée du Gave - Vue prise du Parc à Pau / J. A | Archives et bibliothèques Pau Béarn Pyrénées

```

***

La classification et l'extraction d'informations s'effectueront donc à travers ces deux types de données qui pourront s'entre alimenter une fois la collection moissonnée. C'est-à-dire classifier de futur document ne présentant aucune métadonnée ou bien entre-croiser la recherche de documents suite à la segmentation et classification des images. Le prestataire disposant d'une liberté dans le choix des technologies et des modèles d'apprentissage automatique choisit, il est évident que certaines métriques seront amenées à être développées lors de la phase de sélection.

En revanche, nous devons  procéder à une analyse la plus fine possible sur les documents et les métadonnées présents dans Gallica Images (notamment les estampes, photographies, et dessins). Garantir une population représentative, afin d’amoindrir les biais qui se traduirait par des erreurs de classification, et de favoriser la généralisation des modèles qui se traduirait par la capacité d'extrapoler les résultats d'un échantillon de population sur son ensemble.


## Acquisition et analyse des données

Le service Gallica dispose de divers protocoles qui permettent l'exploitation et l'extraction de leurs ressources numériques. Une [API](https://fr.wikipedia.org/wiki/Interface_de_programmation) (Application Programming Interface) non standardisée et un protocole [OAI-PMH](https://www.bnf.fr/fr/protocole-oai-pmh) (Open Archives Initiative - Protocol for Metadata Harvesting) qui permet de récupérer les métadonnées des documents (donc d'images) présentes sur Gallica Images
Afin de contextualiser la procédure de téléversement de ces métadonnées, il est important de rappeler qu'à travers le protocole OAI-PMH, la Bibliothèque Nationale de France offre la possibilité à d'autre partenaires de téléverser leurs données à des fins de préservation et de mise à disposition de leurs infrastructures. En effet, certaines institutions ne possèdent pas les équipements nécessaires pour numériser leurs documents, ni les ressources infrastructurelles pour héberger leurs documents et faire face au trafic que cela générerait. Cette initiative prend la forme du concept « marque blanche ».


Les documents présents dans l'entrepôt sont donc issus de sources éparses qui s'accompagnent de différentes échelles de granularité. La Bibliothèque Nationale de France met à disposition un [Guide d'interopérabilité OAI-PMH](https://multimedia-ext.bnf.fr/pdf/Guide_oaipmh.pdf) pour un référencement des documents numériques dans Gallica pour que les institutions qui décident de téléverser leurs ressources calquent leurs métadonnées sur ce référentiel. Dans la pratique cela fonctionne, mais la plupart du temps les métadonnées ne sont pas corrélées entre les différentes institutions. Il est donc parfois difficile d'analyser de façon formelle certains documents par le fait que les métadonnées sont mal formatées ou non renseignées.
Il a donc fallu collecter dans l'entrepôt OAINUM, l'ensemble des métadonnées qui traitent de document relatif aux dessins, estampes, photographies afin d'effectuer leurs exploration et analyses. Pour créer une population représentative, nous nous sommes penchés sur les caractéristiques suivantes:

1. Indication sur le type de document
2. Indication sur la techniques du document
3. Indication sur la fonction du document
4. Indication sur la date du document
5. Indication sur la colorimétrie du document
6. Indication sur la présente de texte
7. Indication sur le nombre de vues


Après l'analyse et l'exploration de ces caractéristiques, plusieurs constat sont établis. Premièrement, il est difficile d'obtenir des informations pertinentes pour l'ensemble de la population notamment car ces indications étaient majoritairement absentes. Deuxièmement, l'application de listes d'autorités et de manipulations des informations soulève une question de véracité de l'information qui en a été extraite car elle n'a pas été réalisée conjointement avec des experts du domaine. Et pour finir, on observe un effet de sédimentation qui s'applique par la temporalité des informations qui ont été télévisées. Sur des mêmes périodes on observe beaucoup d'erreurs de formatage communes, qui s'accompagnent parfois par un changement de granularité, notamment à travers différents référentiels qui sont actualisés ou mis à jour sans réactualisation des anciennes métadonnées.

Lors de la fouille et l'analyse des métadonnées, les projections ont été réalisées sur un jeu de données comportant **30 000 documents** (et non d'images) par rapport à une population totale de **468 494 documents**.

Nous retrouvons majoritairement des types de documents associés à la photographie qui sont environ 5 fois plus présents que les dessins et environ 2 fois plus présents que les estampes, en notant que 11.07% des documents ne sont associés à aucun type de documents. Il est également intéressant et forcé de constater que des documents peuvent être associés à plusieurs types de documents à la fois. Cela s'explique par le lien étroit qu'il existe entre ces trois types de documents : une estampe repose préalablement sur du dessin et des procédés photographiques repose parfois sur de l'estampe comme la photomécanique


| type de document | pourcentage | nombre de documents | projection sur le jeu de donnée |
| ---------------- | ----------- | ------------------ | ------------------------------- |
| dessin           | 11.67%      | 54408              | 3483                            |
| estampe          | 23.49%      | 7047               | 7047                            |
| photographie     | 53.83%      | 252212             | 16149                           |
| non assigné  | 11.07%  | 51837          | 3321                        |

Nous avons créé plusieurs listes d'autorités afin de récupérer des informations complémentaires concernant : les techniques, les fonctions, les dates, le nombre d'images présentes par documents. L'objectif étant de dresser des sous populations pour les estampes, les photographies et les dessins.

Chaque à étape de cette chaîne de traitement (de l'acquisition à l'exploration) est détaillé dans le [pipeline de collecte des données](../notebooks/pipeline.ipynb)

## Etablissement du *«ground truth»*

Dans le contexte de la réalisation d'un jeu de données pour la classification et la segmentation, le «*ground truth*» fait référence aux annotations ou aux étiquettes correctes associées à chaque exemple de données. Il s'agit de la référence ou de la vérité absolue utilisée pour évaluer la performance des modèles d'apprentissage automatique.

Dans le cas de la classification, le ground truth indique la classe réelle à laquelle chaque exemple de données appartient. Par exemple, si vous construisez un jeu de données pour classifier des images en chats et chiens, le ground truth désignerait l'étiquette correcte (chat ou chien) pour chaque image. 

Pour la segmentation, le ground truth consiste en une carte d'étiquetage qui définit les différentes régions ou les contours d'intérêt dans une image. Chaque pixel de l'image est étiqueté selon la classe à laquelle il appartient.

```{figure} assets/bbox.png
:width: 500px
:align: center
Exemple de *«bouding-box»* présent dans le jeu de donnée
```

Ces deux méthodes peuvent-être jointes à travers une *«bouding-box»*. La bounding box est généralement utilisée pour localiser et encadrer les objets dans une image. Elle est définie par les coordonnées des quatre coins qui englobent l'objet d'intérêt.

Pour créer le *«ground truth»* d'une *«bouding-box»*, des annotateurs humains examinent l'image et dessinent manuellement une boîte englobante autour de chaque objet d'intérêt. Les coordonnées de cette boîte englobante sont enregistrées pour chaque objet étiqueté. Ces annotations servent de référence pour entraîner et évaluer les modèles de détection d'objets.

Le ground truth est généralement créé manuellement par des annotateurs humains ou peut être obtenu à partir de sources fiables. Les annotateurs examinent les données d'entrée et attribuent les étiquettes appropriées en se basant sur des instructions spécifiques ou des critères préétablis. L'exactitude du ground truth est essentielle pour évaluer la qualité des modèles de classification ou de segmentation, car il sert de référence pour calculer les métriques de performance telles que la précision, le rappel, le F-score, etc.

Il est important de noter que la création d'un ground truth précis et de haute qualité peut être un processus complexe et sujet à des erreurs. Par conséquent, il est souvent recommandé d'avoir plusieurs annotateurs pour évaluer et résoudre les éventuelles divergences ou incertitudes.

Chaque à étape dans la création du *«ground truth»* est détaillé dans le [Guide de pratique pour Label Studio](../notebooks/labelstudio.ipynb)

## Définition des métriques

Dans le cadre du jeu de données produit qui comprend des bounding boxes et des métadonnées, plusieurs métriques peuvent être utilisées pour évaluer la performance d'un modèle de détection d'objets. Voici quelques-unes des métriques couramment utilisées :

```{figure} assets/metrics.png
:width: 500px
:align: center
Les différentes *metrics*
```

1. Intersection over Union (IoU) : L'IoU mesure le degré de chevauchement entre la prédiction de la *«bouding-box»* et du *«ground truth»*. Il est calculé en divisant l'aire de l'intersection entre les deux boîtes par l'aire de leur union. Un IoU élevé indique une correspondance étroite entre la prédiction et le ground truth.

2. Précision (Precision) : La précision évalue la proportion des prédictions de bounding boxes correctes parmi toutes les prédictions positives effectuées par le modèle. Elle mesure la capacité du modèle à ne pas prédire de fausses détections.

3. Rappel (Recall) : Le rappel mesure la proportion des vérités terrain correctement détectées parmi toutes les instances réelles présentes dans le jeu de données. Il évalue la capacité du modèle à identifier tous les objets d'intérêt.

4. F1-score : Le F1-score est une métrique qui combine la précision et le rappel en une seule valeur. Il fournit une mesure globale de la performance du modèle en tenant compte à la fois des vrais positifs, des faux positifs et des faux négatifs.

5. Moyenne des précisions moyennes (Average Precision, AP) : L'AP est utilisée pour évaluer la précision d'un modèle de détection d'objets sur plusieurs seuils de confiance. Elle calcule la précision moyenne pour chaque seuil et les moyenne ensuite. L'AP est souvent calculée pour différents niveaux de rappel (mAP), ce qui permet d'obtenir une évaluation plus complète de la performance du modèle.

Ces métriques sont largement utilisées dans l'évaluation des modèles de détection d'objets avec des du *«bounding-box»* et aident à quantifier la précision, le rappel et la performance globale du modèle.
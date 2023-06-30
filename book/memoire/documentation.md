##  Les enjeux dans le développement d'un jeux de donnée autour des fonds numérisés de la Bibliothèque Nationale de France (BnF)

### Contextualisation  

Dans le cadre de l'appel à projet émis par la BnF et s'inscrivant dans le projet France Relance 2030, il seras demandé au prestataire de mettre en place une solution de fouille de d'image autour des documents présents sur Gallica Images.  L'ensemble de ces documents reposent aujourd'hui sur de l'indexation sémantique, se basant autours des métadonnées qui leurs sont associées. 

Tout l'enjeux de cette appel à projet est d'incorporer des briques d'intelligence artificielle à l'infrastructure déjà préexistante afin de développer une nouvelle chaîne de traitement automatique des documents basé sur une approche de segmentation et de classification. L'enjeux étant de venir extraire de nouvelles métadonnées en complément de celle déjà présente, cela permettras une meilleur exposition des documents, le croisement et la fouille des collections présente sur Gallica Images. Il est à noté que le prestaire est libre de proposer les technologies qui lui semble en adéquation avec l'enjeux exposé précédemment.

Afin d'évaluer les modèles différents prestataires , il est essentielle de faire un inventaire le plus factuel des données que le prestaire devras automatiser sur la base du modèle qu'il aura développé, notamment à des fins d'évaluation autour d'un ensemble de mesure de la qualité. 

L'organisation du marché est découper de la façon suivante:

- **Tranche ferme**: Développement, paramétrage est mise en place d'une version initiale du système d'identification et d'indexation des illustrations, initialisation sur la collection Images (estampes, dessin et photographies, 1,4 millions de page environ) dont une prestation de livraison.
- **Tranche optionnelle 1**: *Développement complémentaire* - Monographies imprimées avec traitement associée d'un échantillon de test de 20 000 pages de la collection dont une prestation de livraison 
- **Tranche optionnelle 2**: *Développement complémentaire* - Périodiques avec traitement associée d'un échantillon de test de 20 000 pages de la collection dont une prestation de livraison
- **Tranche optionnelle 3**: *Développement complémentaire* - Manuscrit avec traitement associée d'un échantillon de test de 20 000 pages de la collection dont une prestation de livraison
- **Tranche optionnelle 4**: *Développement complémentaire* - Document spécialisés (partition musicales, cartes et plans, monnaies) avec traitement associé d'un échantillon de test de 20 000 pages de la collection dont une prestation de livraison

 Ce premier jeu de donnée s'articuleras donc en corrélation avec la tranche ferme autour de trois de type de documents: les estampes, le dessin et la photographies.

### Création du jeu de donnée

La création d'un jeu de donnée comme évoquer précédemment permettra  à la BnF de mettre à disposition un ensemble de document ainsi que leurs métadonnée aux différents prestataire afin qu'ils évaluent conjointement la qualité des modèles de segmentation et de classification. La première étape étant de définir la qualité recherchée pour définir ensuite les métriques.

Le jeu de donnée mettra à disposition deux grands type de donnée: 

- **Des données structurées et riche sémantiquement** à travers des métadonnées présentant différent aspect du document comme le titre, la date, l'auteur, de type de document, la description, le sujet..) 
- **Des données semi-structurées et faible sémantiquement**  à travers l'image, car au delà de la structure de celle-ci hauteur, largeur, nombre de canaux (couleurs, noir et blanc) il est difficile et d'obtenir des informations sémantique pertinente sans l'aide d'un modèle apprentissage automatique.

La classification et l'extraction d'information s'effectueras donc à travers ces deux types de donnée qui pourront s'entre alimenter une fois la collection moissonnée. C'est à dire classifier de futur document ne présentant aucune métadonnée ou bien entre croisé la recherche de document suite à la segmentation et classification des images. Le prestaire disposant d'une liberté dans le choix des technologies et des modèles d'apprentissage automatique choisit, il évident que certaines métriques seront amenée à être développement lors de la phase de sélection. 

Nous devons en revanche procéder à une analyse la plus fine possible sur les documents et les métadonnées présent dans la collection Images et d'établir une population représentative. Pour amoindrir les biais qui se traduirait par des erreurs de classification, et de favoriser la généralisation des modèles qui se traduirait par la capacité d'extrapoler les résultats d'un échantillons de population sur son ensemble.

#### Acquisition

Le service Gallica dispose de divers protocole qui permettent l'exploitation et l'extraction de leurs ressources numériques. Une **API** (Application Programming Interface) non standardisé et un protocole **OAI-PMH** (Open Archives Initiative - Protocol for Metadata Harvesting) qui permet permet de récupérer les métadonnées et qui offre la possibilité à d'autre institution de téléverser leurs données. 

DOCUMENTATION.



#### Constitution et exploration

Une fois la collecte des métadonnées effectuées, l'exploration et l'analyse de celle-ci fut effectuer sur l'ensembles du sets afin d'obtenir un premier recensement de chaque populations qu'il s'agissent d'estampe, de dessin ou de photographie.

 Afin de contextualisation la procédure de téléversement de ces métadonnées, il est important de rappeler qu'à travers le protocole OAI, la BnF offre la possibilité à d'autre partenaires la possibilité de téléverser leurs données à des fins de préservation et de mise à disposition de leurs infrastructures. Les documents présent dans l'entrepôt sont donc issue de source éparse qui s'accompagne de différente échelle de granularité. La  BnF dispose de plusieurs référentiel dans la constitution et la description des ressources dont elle est pourvu, référentiel qui ne sont la plupart du temps pas corréler avec les divers partenaires. Il est donc parfois difficile d'analyser de façon formelle certain document par le fait  que les métadonnées sont mal formatter ou non renseignées.

Il a était donc nécessaire de mettre en place une chaîne de traitement afin de disposée d'information pertinente sur l'ensemble des documents autours de trois grandes caractéristique qui nous semble nécessaire donc la création d'un population représentative:

- **Indication sur le type de document**
- **Indication sur la techniques du document**
- **Indication sur la fonction du document**
- **Indication sur la date du document**
- **Indication sur la colorimétrie du document**
- **Indication sur la présente de texte**
- **Indication sur le nombre de vues**

<u>Après application de cette première chaîne de traitement plusieurs constat</u>

1. Il est difficile d'obtenir des informations pertinentes pour l'ensemble la population notamment car ces indications était majoritairement absente.
2. L'application de liste d'autorité et de manipulation des informations soulève une question de véracité de l'information qui en a était extraire car elle n'a pas était réaliser conjointement avec des experts du domaines. 
3. On observe un effet de sédimentation qu'il s'applique par la temporalité des informations qui ont été téléverser, sur des mêmes périodes on observe beaucoup d'erreur et formatage commun, qui s'accompagne parfois par un changement granularité notamment à travers différent référentiels qui sont actualisé ou mise à jour sans réactualisation  des anciens documents.

Les résultats présent ci-dessous présente les indications sur lesquels nous nous sommes attardées c'est à dire: le type de document, les techniques associées, leurs fonction et temporalité ainsi que le nombre vues pour chaque document. Les projections ont été réaliser sur un jeu de donnée comportant ==30 000 documents== (et non d'image) et sur une population de ==468 494 documents==.

Nous retrouvons majoritairement des types de documents associées à la photographies qui sont environs 5 fois plus présente que les dessins et environ 2 fois plus présente que les estampes, en notant que ==11.07%== des documents ne sont associées à aucun type de document. Il est également intéressant et forcer de constater que des documents peuvent être associées à plusieurs de type de document à fois. Ce s'explique par par le liens étroit qu'il existe entre ces trois types de document, une estampes repose préalablement sur du dessins et des procédés photographiques repose parfois sur de l'estampe comme la photomécanique.

| type de document | pourcentage | nombre de document | projection sur le jeu de donnée |
| ---------------- | ----------- | ------------------ | ------------------------------- |
| dessin           | 11.67%      | 54408              | 3483                            |
| estampe          | 23.49%      | 7047               | 7047                            |
| photographie     | 53.83%      | 252212             | 16149                           |
| ==non assigné==  | ==11.07%==  | ==51837==          | ==3321==                        |

Ce tableau présente un classement des 30 premières techniques récolter après la chaîne traitement, ==52.77%== des documents ne sont associées à aucune techniques. La lithographie qui représente seulement ==10.76%==est la deuxième technique majoritaire. 

| techniques         | pourcentage | nombre de document | vues       | projection (nb) | projection (vues) |
| :----------------- | :---------- | :----------------- | :--------- | :-------------- | :---------------- |
| ==non assigné==    | ==52.77==   | ==280981==         | ==747058== | ==15833==       | ==42095.98==      |
| lithographie       | 10.76       | 57333              | 160788     | 3231            | 9061.2            |
| papier albuminé    | 7.46        | 39749              | 83293      | 2240            | 4693.86           |
| négatif            | 4.48        | 23884              | 57112      | 1346            | 3218.59           |
| plume              | 2.89        | 15404              | 25306      | 868             | 1425.97           |
| aquarelle          | 2.38        | 12682              | 54041      | 715             | 3046.78           |
| burin              | 1.97        | 10538              | 35467      | 594             | 1999.18           |
| gravure sur bois   | 1.95        | 10402              | 70572      | 586             | 3975.7            |
| gélatinobromure    | 1.81        | 9683               | 20204      | 546             | 1139.25           |
| mine de plomb      | 1.29        | 6905               | 13637      | 389             | 768.25            |
| gélatino-bromure   | 1.09        | 5815               | 6920       | 328             | 390.33            |
| xylographie        | 1.08        | 5772               | 6850       | 325             | 385.7             |
| photomécanique     | 0.96        | 5148               | 20546      | 290             | 1157.41           |
| gouache            | 0.83        | 4462               | 24837      | 251             | 1397.15           |
| taille-douce       | 0.76        | 4099               | 14849      | 231             | 836.82            |
| lavis d'encre      | 0.66        | 3516               | 8380       | 198             | 471.91            |
| pointe-sèche       | 0.58        | 3113               | 3375       | 175             | 189.73            |
| contretype         | 0.53        | 2826               | 2873       | 159             | 161.64            |
| diapositive        | 0.52        | 2817               | 128183     | 159             | 7235.04           |
| rehauts            | 0.44        | 2380               | 8475       | 134             | 477.16            |
| aquatinte          | 0.37        | 1991               | 3930       | 112             | 221.07            |
| stéréoscopique     | 0.33        | 1780               | 6574       | 100             | 369.33            |
| pointillé          | 0.33        | 1770               | 5996       | 100             | 338.76            |
| verre au collodion | 0.24        | 1303               | 16952      | 73              | 949.73            |
| pierre noire       | 0.20        | 1116               | 1523       | 63              | 85.98             |
| au pointillé       | 0.20        | 1098               | 4145       | 62              | 234.05            |
| camaïeu            | 0.19        | 1044               | 1311       | 59              | 74.09             |
| au pochoir         | 0.19        | 1034               | 58396      | 58              | 3275.6            |
| sur bois           | 0.19        | 1026               | 72636      | 58              | 4106.13           |
| fusain             | 0.19        | 1022               | 1474       | 58              | 83.65             |

Ce tableau présente un classement des 30 premières fonction récoler après la chaîne de traitement, avec ==65.4%== des documents qui ne sont associées à aucune fonction. L'image de presse est la deuxième technique majoritaire avec ==24.14%==.

| fonction            | pourcentage | nombre de document | vues       | projection (nb) | projection (vues) |
| :------------------ | :---------- | :----------------- | :--------- | :-------------- | :---------------- |
| ==non assigné==     | ==65.34==   | ==309286==         | ==996266== | ==19605==       | ==63151.24==      |
| image de presse     | 24.14       | 114291             | 145458     | 7245            | 9220.7            |
| affiche             | 2.73        | 12939              | 14149      | 820             | 896.68            |
| carte postale       | 2.27        | 10760              | 20099      | 682             | 1273.93           |
| illustration        | 2.14        | 10169              | 58372      | 645             | 3702.42           |
| carte à jouer       | 0.41        | 1957               | 110553     | 124             | 7004.89           |
| dessin de presse    | 0.34        | 1640               | 2296       | 104             | 145.6             |
| maquette de costume | 0.32        | 1549               | 2013       | 98              | 127.36            |
| croquis             | 0.21        | 1007               | 12101      | 64              | 769.08            |
| vue stéréoscopique  | 0.21        | 997                | 4870       | 63              | 307.73            |
| frontispice         | 0.17        | 838                | 2239       | 53              | 141.61            |
| modèle              | 0.17        | 808                | 10620      | 51              | 670.32            |
| vue d'optique       | 0.15        | 743                | 752        | 47              | 47.57             |
| almanach            | 0.14        | 669                | 1834       | 42              | 115.14            |
| calendrier          | 0.11        | 541                | 752        | 34              | 47.26             |
| carte de visite     | 0.11        | 534                | 13244      | 34              | 843.25            |
| image de mode       | 0.10        | 495                | 640        | 31              | 40.08             |
| couverture          | 0.09        | 429                | 926        | 27              | 58.28             |
| partition           | 0.08        | 405                | 991        | 26              | 63.62             |
| éventail            | 0.08        | 390                | 567        | 25              | 36.35             |
| coupe transversale  | 0.07        | 377                | 470        | 24              | 29.92             |
| cartouche           | 0.07        | 347                | 379        | 22              | 24.03             |
| enveloppe           | 0.05        | 273                | 17301      | 17              | 1077.35           |
| coupe longitudinale | 0.05        | 264                | 323        | 17              | 20.8              |
| tarot               | 0.04        | 214                | 16811      | 14              | 1099.79           |
| maquette de décor   | 0.03        | 159                | 927        | 10              | 58.3              |
| prospectus          | 0.02        | 137                | 503        | 9               | 33.04             |
| image publicitaire  | 0.02        | 128                | 529        | 8               | 33.06             |
| timbre              | 0.02        | 110                | 203        | 7               | 12.92             |
| assignat            | 0.02        | 110                | 444        | 7               | 28.25             |



Ce tableau présente des tranches 100 ans allant de 0 à 1900 jusqu'à nos jours associées au nombre de document. Les documents sont majoritairement compris entre 1800 à nos jours.

| date                   | 0    | 100  | 200  | 300  | 400  | 500  | 600  | 700  | 800  | 900  | 1000 | 1100 | 1200 | 1300 | 1400 | 1500 | 1600 | 1700  | 1800   | 1900   |
| :--------------------- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :---- | :----- | :----- |
| **nombre de document** | 5    | 4    | 5    | 3    | 3    | 0    | 0    | 0    | 21   | 1    | 468  | 38   | 28   | 261  | 596  | 3498 | 9183 | 25334 | 102099 | 207447 |
| **pourcentage**        | 0.0  | 0.0  | 0.0  | 0.0  | 0.0  | 0.0  | 0.0  | 0.0  | 0.01 | 0.0  | 0.13 | 0.01 | 0.01 | 0.07 | 0.17 | 1.0  | 2.63 | 7.26  | 29.26  | 59.44  |

Ce tableau présente la répartition des vues (et donc d'image) par documents et leurs pourcentage.

| vues      | documents | pourcentage |
| :-------- | :-------- | :---------- |
| 1 - 9     | 441562    | 96.762897   |
| 10 - 19   | 3152      | 0.690722    |
| 20 - 49   | 5562      | 1.218844    |
| 50 - 99   | 3688      | 0.808180    |
| 100 - 499 | 2315      | 0.507304    |
| +500      | 55        | 0.012053    |



#### Format 

Après la constitution du jeux de donnée, il a était nécessaire de publier ces données à travers un format adéquate pour la distribution auprès des prestataires mais aussi pour leurs diffusions sur différentes plateformes comme Hugging Face, Kaggle ou Data.gouv.fr. Ce format doit prendre en l'incorporation des métadonnées associées aux documents comme détaillées précédemment, des boîte englobantes (bounding box), des étiquettes de classification mais également des annotations textuelles. Il faut souligner que les images ne seront présente sous aucun format d'image mais disponible à travers l'API IIIF de la BnF via leurs ARK, qui permet l'exposition des images et de leurs manipulation (recadrage, redimensionnage, colorimétrie..).  Il est donc impératif que le format harmonise l'ensemble de ces données avec une finesse donc la hiérarchisation de celle-ci.

Trois critères de sélection:

- **Accessibilité et partage**
- **Hiérarchisation des données**
- **Incorporation de coordonnées cartésienne et textuelles**

Il existe de type de format standard et de référence dans la communauté scientifique pour les tâches tâches de vision par ordinateur dans l'organisation de données complexes, le format XML comme les jeux de données PascalVOC ou bien le format JSON comme COCO (Common Object in Context) pour ne cité qu'eux. Ils offrent tout les deux des caractéristique différent dans la hiérarchisation des données:

- **Le format XML**: 
  -  Langage de balisage il permet de transférer des données mais aussi un traitement de calcul pour formatter des objets et documents. 
  - Il est autodescriptif habituellement il possède un lien qui revoit à son schéma, cela permet auto validation des champs
  - Un transfert de donnée plus lent du fait du fait de sa complexité ce qui le rend plus difficile à lire pour un utilisateurs également notamment par sa structure arborescente.
- **Le format JSON**
  - Un format de donnée il permet de transférer des données mais n'offre aucun traitement de calcul pour formatter des objets ou documents. 
  - Il n'est pas autodescriptif et ne dispose pas nativement de schéma pour auto validation des champs.
  - Un transfert de donnée plus rapide du fait de structure clé-valeur, facile à lire grâce à sa syntaxe minimale 

Le première constatation est que le format XML offre une structure de donnée trop complexe, à des fins accessibilité en direction des chercheurs et utilisateurs n'ayant aucune connaissance annexe vis à vis du jeu de donnée. Il est nécessaire d'opter pour un format qui favorise la compréhension de l'ensemble des données et la structure clé-valeur semble la plus aisée (à noté que le format JSON n'offre pas la possibilité incorporer des commentaires). Il est également important de faire le parallèle avec l'API IIIF qui expose des données aux formats JSON.

Le format JSON semble donc le plus adéquate.




# Analyse de la Segmentation Client : Réduction de Dimensionnalité et Comparaison des Algorithmes de Regroupement

##Objectif : 

Développer un modèle de segmentation de la clientèle pour améliorer les processus de prise de décision dans le secteur du commerce de détail. 

L'objectif est de transformer les données transactionnelles en un ensemble axé sur le client grâce à la création de nouvelles caractéristiques, facilitant la segmentation des clients en groupes distincts via des algorithmes de regroupement (dont on effectuera la comparaison) et permettant une meilleure compréhension des profils et préférences des différents groupes de clients

>Develop a customer segmentation model to enhance decision-making processes in the retail sector. Our aim is to transform transactional data into customer-focused datasets by creating new features, facilitating customer segmentation into distinct groups using clustering algorithms. This approach will provide deeper insights into the profiles and preferences of different customer segments.

##Dataset :

Ce projet utilise des données provenant d'une boutique en ligne de cosmétiques collectées par le projet Open CDP ! [données ici](https://www.kaggle.com/datasets/mkechinov/ecommerce-events-history-in-cosmetics-shop?select=2019-Dec.csv)


Cet ensemble de fichiers couvrent 5 mois (oct 2019 - fév 2020) totalisant environ 4 millions de lignes par fichier. Seuls les événements *cart* et *purchase* ont été sélectionnés pour analyser ces comportements avant d'être combinés en un fichier unique.


##Voici les différents notebooks : 

Ce repo présente un ensemble de 4 Jupyter Notebooks démontrant le processus pour la segmentation de la clientèle:

•	[1-clean_transform_FE](https://github.com/SafaeLh/client-segmentation/blob/main/1-clean_transform_FE.ipynb) : une analyse préliminaire pour comprendre la structure et les types de colonnes de données est effectuée dans ce fichier. Suivi d’un nettoyage et transformation de données (traitements des valeurs manquantes, gestion de doublons, vérifications des colonnes). Enfin, afin de créer un ensemble complet de données centrées sur le client pour le regroupement, les fonctionnalités basées sur le client ont été créés (Caractéristiques RFM, comportementales, saisonnalité et tendances)


•	[2-data_preprocessing](https://github.com/SafaeLh/client-segmentation/blob/main/2-data_preprocessing.ipynb) : un travail de preprocessing est fait sur notre nouvelle base de données axées sur le client (détection et traitement des valeurs aberrantes, analyse de corrélation, mise à l’échelle des différentes caractéristiques, réduction de la dimensionnalité avec PCA et kernelPCA)


•	[3-clustering](https://github.com/SafaeLh/client-segmentation/blob/main/3-clustering.ipynb) : le regroupement a été fait sur 3 données pour comparaison (les données originales, les données transformées avec PCA et les données transformées en utilisant le KERNEL). Dans cette étude deux algorithmes sont comparés : K-means clustering, the Gaussian mixture model (GMM). Pour l’examen de la qualité des différents algorithmes 3 mesures sont calculées (Score de silhouette, Score Calinski Harabasz, Score de Davies Bouldin)


> Bien que GMM ait un meilleur Silhouette Score, K-means a eu des scores Calinski Harabasz et Davies Bouldin plus favorables après l'application de PCA. En général, ces scores suggèrent que K-means offre des clusters plus distincts et moins dispersés que GMM. Ainsi, **K-means semble globalement fournir de meilleurs résultats de clustering par rapport à GMM dans ce cas particulier**.


•	[4-clusters_analysis](https://github.com/SafaeLh/client-segmentation/blob/main/4-clusters_analysis.ipynb) : Dans cette section, l’analyser les caractéristiques de chaque cluster identifié par l'algorithme K-means sur les données réduites avec PCA afin de comprendre les comportements et les préférences distincts des différents segments de clientèle et de dresser le profil de chaque groupe afin d'identifier les traits clés qui définissent les clients de chaque groupe.


##Output : 
 ![newplot](https://github.com/user-attachments/assets/242f82c3-430f-4b4c-9b31-d4720ec2e156)


**Analyse globale**

- *Cluster 0: "Gros dépensiers occasionnels"*

Les clients du cluster 0 montrent une faible activité d'achat en termes de nombre d'achats et de diversité des produits, mais lorsqu'ils achètent, ils dépensent des sommes importantes. Leur engagement dans les activités de la plateforme est modéré. Ils font des achats relativement fréquemment, avec une préférence pour les jours en début de semaine et en dehors des heures de pointe. Leur comportement d'achat est très décidé, avec de faibles fréquences et taux de retrait des articles du panier. Malgré un faible nombre d'achats, leurs dépenses mensuelles sont relativement élevées et stables, avec une tendance à la hausse. Ce groupe pourrait bénéficier de stratégies visant à augmenter la fréquence de leurs achats tout en maintenant ou augmentant le montant moyen dépensé par achat.

- *Cluster 1: "Acheteurs modérés irréguliers"*

Les clients de ce cluster sont très engagés, participant à de nombreux événements et interagissant fréquemment. Cependant, cet engagement ne se traduit pas par des achats fréquents ou de grande valeur. Ils dépensent peu en général et montrent une préférence pour des produits spécifiques avec une faible diversité dans leurs achats. Bien qu'ils aient tendance à acheter à des moments spécifiques, ils hésitent peu avant de finaliser leurs achats. La tendance des dépenses est légèrement à la hausse, suggérant un potentiel d'augmentation des dépenses futures avec des stratégies de réengagement appropriées.

- *Cluster 2 : "Acheteurs fréquents et diversifiés"*

Les clients de ce cluster sont extrêmement engagés, participant à de nombreux événements et effectuant fréquemment des achats. Ils achètent une grande variété de produits et dépensent globalement plus que la moyenne, bien que le montant moyen par achat soit légèrement inférieur à la moyenne. Leur fréquence d'achat est élevée, et ils montrent une certaine hésitation avant de finaliser leurs achats, comme en témoignent les fréquences et les taux de retrait d'articles élevés. Leurs dépenses mensuelles sont élevées et relativement stables, avec une tendance marquée à la hausse, ce qui suggère un potentiel de croissance continue de leurs dépenses.

- *Cluster 3 : "Acheteurs Engagés mais Hésitants et Décroissants"*

Les clients de ce cluster montrent un engagement élevé en termes de participation à des événements, mais leur activité d'achat récente est très faible, avec des périodes longues entre les achats. Quand ils achètent, ils dépensent de manière significative et achètent une variété de produits, mais leurs habitudes d'achat sont très irrégulières. Leur tendance de dépenses est fortement négative, ce qui indique qu'ils réduisent progressivement leurs dépenses. Ils montrent une préférence pour des horaires atypiques pour faire leurs achats et ont une forte propension à retirer des articles de leurs paniers avant de finaliser les achats. Ces clients pourraient nécessiter des stratégies spécifiques pour réengager et stabiliser leurs comportements d'achat.

- *Cluster 4 : "Acheteurs modérés réguliers"*

Les clients du cluster 4 montrent un bon engagement avec une participation active à de nombreux événements, mais leur nombre d'achats et leurs dépenses totales sont faibles. Ils achètent une petite variété de produits et dépensent peu en moyenne par achat. Malgré cela, ils font des achats plus fréquemment, mais avec des montants faibles, et montrent une préférence pour les achats en fin de semaine et pendant les heures de pointe. Leur comportement d'achat est assez décidé avec une faible fréquence et un taux de retrait des articles. Les dépenses mensuelles sont faibles et stables, avec une légère tendance à la hausse. Ce groupe pourrait bénéficier de stratégies incitatives pour augmenter leur panier moyen et diversifier leurs achats.




 



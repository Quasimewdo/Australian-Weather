# Librairies utilisées

Assurez-vous bien de disposer des packages suivants:

- tidyr               #Gérer les dataframes
- dplyr               #Gérer les dataframes
- lubridate           #Gérer les dates
- FactoMineR
- MASS
- cluster
- pROC
- klaR
- rpart
- rpart.plot
- randomForest
- ISLR
- DMwR

S'il vous en manque, il vous suffit d'effectuer la commande install.package("nom_du_package_a_installer")

# Australian-Weather

Nous avons à disposition des données de la météo de l'Australie.   

Avant de pouvoir l'utiliser, nous allons effectuer des mises en structure en fonction des différents type d'analyse. Mais en général, nous avons éliminé les variables qui contiennent que des NA (Evaporation, Sunshine, Cloud9am, Cloud3pm). Puis nous avons effectué un trie en fonction de la date et de la ville : nous avons extrait 2300 lignes par ville de l'année 2010 à 2017.  


## Analyser les directions de rafale du vent de 25 villes

### ACP : 

Axe 1: ENE / N  
Axe 2: SW / SE  
Axe 3: NE / SE  
Axe 4: NNW / W  
Axe 5: N / NE  

### AFC : 

- Il y a des régions dont les résultats sont proches des résultats nationaux : des points qui sont proches du centre de gravité, par exemple : Mildura.  
- Il y a des régions qui se ressemblent : des points bleus confondus, par exemple : WaggaWagga et PerthAirport.  
- Townsville a surtout des vents qui viennent du ENE.  
- Cairns a peu de vent qui vient du WSW.  
- Hobart a surtout du vent qui vient de Nord-West.

## Effectuer une classification des 2300 jours du Sydney

Ici, nous nous intéressons pas aux états des vents, donc nous avons éliminés ces variables.  
Après avoir extrait les 2300 lignes du Sydney, nous avons aussi supprimé les variables Location, et Year.  
Nous avons ajouté une variable AvgTemp pour faciliter l'analyse des résultats.  

### ACP : 

Axe 1 indique importance de la température.  
Axe 2 indique importance de la pression contre d'humidité.  

### Classification non supervisée (CAH, kmeans) : 
Les individus sont classés en fonction de la température, l'humidité et la pression : 

- Classe 1 : Température moyenne élevée
- Classe 2 : Température moyenne faible
- Classe 3 : Température moyenne-moyenne, Humidité faible, Pression élevée
- Classe 4 : Température moyenne-moyenne, Humidité forte, Pression faible


## Classification supervisée : Prédire la météo du lendemain, plus particulièrement s'il va pleuvoir pour Sydney

### Première analyse : Jeu de données non équilibré

lda légèrement meilleure que qda : taux de réussite environ égal à 75%

Le modèle prédit "No" la plupart du temps -> taux d'erreur de No est petit, mais de Yes est très grand.  

### Jeu de données ré-équilibré

Taux d'erreur de Yes diminue mais reste non négligeable.  


La météo reste difficile à prédire, le taux de réussite est à 75%, ce qui est pas mal pour un modèle simple.

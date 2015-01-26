ABD - TP 02
===========

Auteurs
-------

- BERNARD Thomas
- SAINT-OMER Anne-Sophie

Exercice 1
----------

Caractéristiques du disque :
- 512 octets par secteur
- 50 secteurs par piste
- 2000 pistes par surface
- 5 plateaux
- Vitesse de rotation de 5400 rpm (rotations par minute)
- Temps de positionnement moyen de 10ms

#### Question 2

#### Question 3

#### Question 4

#### Question 5

#### Question 6

Exercice 2
----------

Exercice 3
----------

Données :  

Relation R(K,A,B,C) avec :  
- K : clé primaire, avec valeurs entières dans l'intervalle (1, 100000)  
- A : attribut, avec valeurs entières distribuées uniforméments dans l'intervalle (1, 1000)  

Relation mémorisée avec une structure de fichier tas (heap file) avec les valeurs de K et A non ordonnées en pages de taille Dp = 1024 octets  
Nombre d'enregistrements (record) sur le disque Ne = 100000  
Taille d'un enregistrement (record) Lr = 100 Ko  

#### Expression 1

```sql
SELECT ∗
FROM R
WHERE Attribut = 50;
```

#### Expression 2

```sql
SELECT ∗
FROM R
WHERE Attribut BETWEEN 50 AND 100;
```

#### Expression 3

```sql
SELECT ∗
FROM R
WHERE Attribut = 50 ORDER BY Attribut;
```

#### Expression 4

```sql
INSERT INTO R values ();
```

#### Expression 5

```sql
DELETE
FROM R
WHERE Attribut = 50;
```

Exercice 4
----------

Soit le fichier `⟨[20,1],[25,2],[30,3],[40,5],[60,6],[12,15],[21,17],[50,45]⟩`.  
Tri externe sur ce fichier avec 3 buffers disponibles et 2 enregistrements sur chaque bloc :

1. Tri de la mémoire principale  

Les 2 premiers enregistrements sont lus, triés et écrits dans Tb1.  

```
Tb1:	1 	20
Tb2:
Tb3:
```

Les 2 enregistrements suivants sont lus, triés et écrits dans Tb2.  

```
Tb1:	1 	20
Tb2:	2 	25
Tb3:
```

Les 2 enregistrements suivants sont lus, triés et écrits dans Tb3.  

```
Tb1:	1 	20
Tb2:	2 	25
Tb3:	3	30
```

Les 2 enregistrements suivants sont lus, triés et ajoutés à Tb1.  

```
Tb1:	1 	20 	|	5 	40
Tb2:	2 	25
Tb3:	3	30
```

Les 2 enregistrements suivants sont lus, triés et ajoutés à Tb2.  

```
Tb1:	1 	20 	|	5 	40
Tb2:	2 	25	|	6 	60
Tb3:	3	30
```

Les 2 enregistrements suivants sont lus, triés et ajoutés à Tb3.  

```
Tb1:	1 	20 	|	5 	40
Tb2:	2 	25	|	6 	60
Tb3:	3	30	|	12 	15
```

Les 2 enregistrements suivants sont lus, triés et ajoutés à Tb1.

```
Tb1:	1 	20 	|	5 	40	|	17	21
Tb2:	2 	25	|	6 	60
Tb3:	3	30	|	12 	15
```

Les 2 derniers enregistrements sont lus, triés et ajoutés à Tb2.

```
Tb1:	1 	20 	|	5 	40	|	17	21
Tb2:	2 	25	|	6 	60	|	45	50
Tb3:	3	30	|	12 	15
```


Exercice 5
----------

#### Question 1

#### Question 2

#### Question 3

#### Question 4

#### Question 5

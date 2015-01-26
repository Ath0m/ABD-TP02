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

Exercice 5
----------

#### Question 1

#### Question 2

#### Question 3

#### Question 4

#### Question 5

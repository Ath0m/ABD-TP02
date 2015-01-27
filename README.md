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

Enregistrement de taille fixe :

- Avantages :
	- Simple à implémenter
	- Une fois la base créée, il suffit de respecter la taille imposée aux enregistrements et aucune modification n'est nécesaire.

- Inconvénient :
	- Un nouvel enregistrement plus grand ne peut pas être inséré dans la table.

Enregistrement de taille variable :

- Avantage :
	- On ne se soucie pas de la taille d'un nouvel enregistrement.

- Inconvénient :
	- Compliqué à implémenter.

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

**1. Tri de la mémoire principale**  

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

**2.	Fusion**  

Construction d'un tas avec les premiers enregistrements de chaque buffer.

```
Tas:	1 	2 	3

Tb1:	1 	20 	|	5 	40	|	17	21
Tb2:	2 	25	|	6 	60	|	45	50
Tb3:	3	30	|	12 	15
```

Le plus petit élément du tas est est retiré et ajouté à Ta1.  
Ici, le plus petit élément est 1. Il appartenait à Tb1, donc on ajoute au tas l'élément suivant de Tb1.

```
Tas:	20 	2 	3

Tb1:	 	20 	|	5 	40	|	17	21
Tb2:	2 	25	|	6 	60	|	45	50
Tb3:	3	30	|	12 	15

Ta1:	1
```

On itére de nouveau, avec le nouvel élément le plus petit du tas.

```
Tas:	20 	25 	3

Tb1:	 	20 	|	5 	40	|	17	21
Tb2:	 	25	|	6 	60	|	45	50
Tb3:	3	30	|	12 	15

Ta1:	1 	2
```

On itére sur les enregistrements suivants.

```
Tas:	20 	25 	30

Tb1:	 	20 	|	5 	40	|	17	21
Tb2:	 	25	|	6 	60	|	45	50
Tb3:		30	|	12 	15

Ta1:	1 	2 	3
```

```
Tas:	 	25 	30

Tb1:	 	 	|	5 	40	|	17	21
Tb2:	 	25	|	6 	60	|	45	50
Tb3:		30	|	12 	15

Ta1:	1 	2 	3 	20
```

```
Tas:	 	 	30

Tb1:	 	 	|	5 	40	|	17	21
Tb2:	 		|	6 	60	|	45	50
Tb3:		30	|	12 	15

Ta1:	1 	2 	3 	20 	25
```

```
Tas:	 	 	

Tb1:	 	 	|	5 	40	|	17	21
Tb2:	 		|	6 	60	|	45	50
Tb3:			|	12 	15

Ta1:	1 	2 	3 	20 	25 	30
```

On reconstruit le tas, et on ajoute les enregistrements suivants à Ta2.

```
Tas:	5 	6 	12

Tb1:	 	 	|	5 	40	|	17	21
Tb2:	 		|	6 	60	|	45	50
Tb3:			|	12 	15

Ta1:	1 	2 	3 	20 	25 	30
Ta2:	
```

```
Tas:	40 	6 	12

Tb1:	 	 	|	 	40	|	17	21
Tb2:	 		|	6 	60	|	45	50
Tb3:			|	12 	15

Ta1:	1 	2 	3 	20 	25 	30
Ta2:	5
```

```
Tas:	40 	60 	12

Tb1:	 	 	|	 	40	|	17	21
Tb2:	 		|	 	60	|	45	50
Tb3:			|	12 	15

Ta1:	1 	2 	3 	20 	25 	30
Ta2:	5 	6
```

```
Tas:	40 	60 	15

Tb1:	 	 	|	 	40	|	17	21
Tb2:	 		|	 	60	|	45	50
Tb3:			|	 	15

Ta1:	1 	2 	3 	20 	25 	30
Ta2:	5 	6 	12
```

```
Tas:	40 	60 	

Tb1:	 	 	|	 	40	|	17	21
Tb2:	 		|	 	60	|	45	50
Tb3:			|	 	

Ta1:	1 	2 	3 	20 	25 	30
Ta2:	5 	6 	12 	15
```

```
Tas:	 	60 	

Tb1:	 	 	|	 		|	17	21
Tb2:	 		|	 	60	|	45	50
Tb3:			|	 	

Ta1:	1 	2 	3 	20 	25 	30
Ta2:	5 	6 	12 	15 	40
```

```
Tas:	 	 	

Tb1:	 	 	|	 		|	17	21
Tb2:	 		|	 		|	45	50
Tb3:			|	 	

Ta1:	1 	2 	3 	20 	25 	30
Ta2:	5 	6 	12 	15 	40 	60
```

On reconstruit le tas, et on ajoute les derniers enregistrements à Ta1.

```
Tas:	17 	45

Tb1:	 	 	|	 		|	17	21
Tb2:	 		|	 		|	45	50
Tb3:			|	 	

Ta1:	1 	2 	3 	20 	25 	30
Ta2:	5 	6 	12 	15 	40 	60
```

```
Tas:	21 	45

Tb1:	 	 	|	 		|		21
Tb2:	 		|	 		|	45	50
Tb3:			|	 	

Ta1:	1 	2 	3 	20 	25 	30 	|	17
Ta2:	5 	6 	12 	15 	40 	60
```

```
Tas:	 	45

Tb1:	 	 	|	 		|		
Tb2:	 		|	 		|	45	50
Tb3:			|	 	

Ta1:	1 	2 	3 	20 	25 	30 	|	17	21
Ta2:	5 	6 	12 	15 	40 	60
```

```
Tas:	 	50

Tb1:	 	 	|	 		|		
Tb2:	 		|	 		|		50
Tb3:			|	 	

Ta1:	1 	2 	3 	20 	25 	30 	|	17	21	45
Ta2:	5 	6 	12 	15 	40 	60
```

```
Tas:	 	

Tb1:	 	 	|	 		|		
Tb2:	 		|	 		|		
Tb3:			|	 	

Ta1:	1 	2 	3 	20 	25 	30 	|	17	21	45	50
Ta2:	5 	6 	12 	15 	40 	60
```

```
Ta1:	1 	2 	3 	20 	25 	30 	|	17	21	45	50
Ta2:	5 	6 	12 	15 	40 	60
```

**3. Tri**  

En utilisant un tas avec les deux premiers enregistrements de `Ta1` et `Ta2`, et en suivant le même principe de tri, on obtient :  

```
Tb1:	1 	2 	3 	5 	6	12 	15 	20 	25 	30 	40 	60
Tb2:	17 	21 	45 	50
Tb3:
``` 

**4. Tri**  

Même opération de tri pour obtenir le fichier final.

```
Ta1:	1 	2 	3 	5 	6 	12 	15 	17 	20 	21 	25 	30 	40 	45 	50 	60
``` 

Exercice 5
----------

#### Question 1

#### Question 2

#### Question 3

#### Question 4

#### Question 5

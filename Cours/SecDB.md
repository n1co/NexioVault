
1: 
```sql
SELECT COUNT(*)  FROM eleves  JOIN adresses  ON eleves.adresse = adresses.id_adresse  WHERE adresses.numero=14 AND adresses.rue='avenue du general de gaulle';
```

2:
```sql
SELECT COUNT(id) FROM eleves INNER JOIN adresses ON adresse = id_adresse WHERE ville = "paris";
```

3:
```sql
SELECT CONCAT(numero, " ", rue, ", ", ville) AS "Adresse de JL" FROM eleves INNER JOIN adresses ON adresse = id_adresse WHERE prenom = "jean-luc" AND nom = "vlan";
```

4:
```sql
SELECT prenom,nom FROM eleves,adresses WHERE adresse = id_adresse AND prenom LIKE "jean%";
```

5:
```sql
SELECT nom,prenom,numero,rue FROM eleves,adresses WHERE eleves.adresse = adresses.id_adresse AND nom = "parker" AND prenom = "peter";
```

6:
```sql
SELECT CONCAT(prenom, " ", UPPER(nom)) AS "Gens avec Marie" FROM eleves INNER JOIN adresses ON adresse = id_adresse WHERE eleves.adresse = (SELECT adresse FROM eleves WHERE prenom = "marie" AND nom = "gole") AND prenom != "marie" AND nom != "gole";
```

7:
```sql
SELECT prenom, nom, age FROM eleves WHERE age = (SELECT MAX(age) FROM eleves);
```

8:
```sql
SELECT COUNT(age) AS "Semi vieux" FROM eleves WHERE age BETWEEN 31 and 39;
```

9:
```sql
SELECT prenom,nom AS "Vieux" FROM eleves WHERE age > 50;
```

10:
```sql
SELECT mail FROM eleves WHERE age < 20;
```




```shell
mysql -u username -p database_name < file.sql
```

MDP ZIP: OUI

User VM: localadm / localadm


```sql
CREATE DATABASE *databasename*;
```

```sql
CREATE TABLE Persons (  
    PersonID int NOT NULL,  
    LastName varchar(255),  
    FirstName varchar(255),  
    Address varchar(255),  
    City varchar(255)  
);
```


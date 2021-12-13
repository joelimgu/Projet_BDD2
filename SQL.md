
# Tables
## Doctorants table
```sql
CREATE table Doctorant (
    id_doctorant serial,
    date_debut_de_these date,
    date_de_soutenance date,
    PRIMARY KEY (id_doctorant),
    CONSTRAINT fk_personnel
       FOREIGN KEY(id_doctorant)
           REFERENCES personnel(id_personnel)
);
```
## Scientifique Table 
``` sql 
CREATE TABLE scientifique(ID_Scientifique INT PRIMARY KEY, 
                          grade VARCHAR(2), 
                          CONSTRAINT fk_scientifique 
                            FOREIGN KEY(ID_Scientifique) 
                                REFERENCES Personnel(ID_Personnel) ON DELETE CASCADE);
```
## President table 
``` sql 
CREATE TABLE President(ID_President INT PRIMARY KEY,  
                       Constraint fk_president 
                            FOREIGN KEY (ID_president) 
                                REFERENCES scientifique(id_scientifique) ON DELETE CASCADE);
```
## Chercheur table 
```sql
CREATE TABLE Chercheur( 
    id_chercheur INT, 
    CONSTRAINT fk_chercheur 
        FOREIGN KEY(ID_Chercheur) 
        REFERENCES Scientifique(id_scientifique) ON DELETE CASCADE, 
    PRIMARY KEY(ID_Chercheur)
);
```

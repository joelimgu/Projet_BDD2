
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
## Chercheur table 
```sql
CREATE TABLE Chercheur( 
    id_chercheur INT, 
    CONSTRAINT fk_chercheur 
        FOREIGN KEY(id_chercheur) 
        REFERENCES Scientifique(id_scientifique) ON DELETE CASCADE ON UPDATE CASCADE, 
    PRIMARY KEY(id_chercheur)
);
```

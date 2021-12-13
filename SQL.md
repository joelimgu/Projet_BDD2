
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
## Scientifique table 
```sql
CREATE TABLE scientifique(
        ID_Scientifique INT PRIMARY KEY, 
        grade VARCHAR(2), 
        CONSTRAINT fk_scientifique 
            FOREIGN KEY(ID_Scientifique) 
                REFERENCES Personnel(ID_Personnel) ON DELETE CASCADE
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

## Porteur table
```sql
CREATE TABLE PORTEUR(
    id_porteur INT PRIMARY KEY,
    CONSTRAINT fk_porteur 
        FOREIGN KEY(ID_PORTEUR) 
            REFERENCES scientifique(id_scientifique) ON DELETE CASCADE ON UPDATE CASADE
);
```


# Tables

## Doctorants table
```sql
CREATE table if not exists Doctorant (
     id_doctorant serial,
     date_debut_de_these date,
     date_de_soutenance date,
     PRIMARY KEY (id_doctorant),
     CONSTRAINT fk_personnel
         FOREIGN KEY(id_doctorant)
             REFERENCES personnel(id_personnel)
             on delete cascade
             on update cascade
);
```
CREATE TABLE Chercheur( 
    id_chercheur INT, 
    CONSTRAINT fk_chercheur 
        FOREIGN KEY(ID_Chercheur) 
        REFERENCES Scientifique(id_scientifique) ON DELETE CASCADE, 
    PRIMARY KEY(ID_Chercheur)
);

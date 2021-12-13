
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
        FOREIGN KEY(ID_Chercheur) 
        REFERENCES Scientifique(id_scientifique) ON DELETE CASCADE, 
    PRIMARY KEY(ID_Chercheur)
);
```

## Chercheur Enseignant
```sql
CREATE table if not exists chercheur_enseignant (
     id_chercheur_ens serial not null,
     echelon varchar(255) not null,
     PRIMARY KEY (id_chercheur_ens),
     CONSTRAINT fk_personnel
         FOREIGN KEY (id_chercheur_ens)
             REFERENCES personnel(id_personnel)
             on delete cascade
             on update cascade
);
```


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
## Projet de recherche table 
```sql
CREATE TABLE Projet_De_Recherche(
    ID_Projet SERIAL PRIMARY KEY, 
    Titre TEXT NOT NULL, 
    Acronyme TEXT , 
    An_début DATE NOT NULL, 
    Durée INT , 
    Coût_Global INT , 
    Budget INT NOT NULL, 
    ID_Porteur INT NOT NULL, 
    CONSTRAINT FK_PORTEUR 
        FOREIGN KEY (ID_PORTEUR)   
            REFERENCES porteur(Id_Porteur)
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

## Encadrant
```sql
CREATE TABLE Encadrant(
    id_encadrant INT PRIMARY KEY, 
    CONSTRAINT fk_encadrant 
        FOREIGN KEY(ID_Encadrant) 
            REFERENCES Scientifique(ID_Scientifique) ON DELETE CASCADE ON UPDATE CASCADE
);


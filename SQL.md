
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

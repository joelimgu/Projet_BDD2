
# Tables
## Congres
```sql
create table congres
(
    id_congres     serial
        primary key,
    nb_participant integer    not null,
    classe         varchar(15) not null,
    date_debut     date       not null,
    date_fin       date       not null
);
```

## Etablissement
```sql
create table etablissement
(
    id_etablissement serial
        primary key,
    nom              text not null,
    adresse          text not null,
    acronyme         varchar(10)
);
```
## Jpo
```sql
create table jpo
(
    id_jpo     serial
        primary key,
    date_debut date not null,
    date_fin   date not null
);
```
## Laboratoires_externes
```sql
create table laboratoires_externes
(
    id_labo serial
        primary key,
    nom     text not null,
    pays    text not null
);
```
## Personnel
```sql
create table personnel
(
    id_personnel        serial
        primary key,
    nom                 text not null,
    prenom              text not null,
    date_de_naissance   date not null,
    adresse             text not null,
    date_de_recrutement date not null
);
```
## President
```sql
create table president
(
    id_president integer not null
        primary key
        constraint fk_president
        references scientifique
        on delete cascade
);
```

## Publications
```sql
create table publications
(
    id_publication          serial
        primary key,
    titre                   text       not null,
    annee_de_publication    date       not null,
    nom_de_la_conférence    text       not null,
    classe_de_la_conférence varchar(2) not null,
    nb_de_pages             integer    not null
);
```

## Doctorants table
```sql
CREATE table if not exists Doctorant (
    id_doctorant integer not null,
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
## Scientifique table 
```sql
CREATE TABLE scientifique(
        ID_Scientifique INT PRIMARY KEY, 
        grade VARCHAR(2), 
        CONSTRAINT fk_scientifique 
            FOREIGN KEY(ID_Scientifique) 
                REFERENCES Personnel(ID_Personnel) ON DELETE CASCADE ON UPDATE CASCADE
            );
```
## President table 
```sql
    CREATE TABLE President(
    ID_President INT PRIMARY KEY,  
    Constraint fk_president 
        FOREIGN KEY (ID_president) 
           REFERENCES scientifique(id_scientifique) ON DELETE CASCADE);
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
            REFERENCES porteur(Id_Porteur) ON DELETE CASCADE ON UPDATE CASCADE
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
    id_chercheur_ens integer not null,
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
```

## Partenaire
```sql
CREATE table if not exists partenaire (
    id_partenaire integer not null,
    nom varchar(255),
    pays varchar(255),
    PRIMARY KEY (id_partenaire)
);
```

## Auteurs Externes Table
```sql
CREATE TABLE Auteurs_Externes(
    ID_Auteur SERIAL PRIMARY KEY,
    Nom VARCHAR(255) NOT NULL,
    Prenom VARCHAR(255) NOT NULL,
    Adresse_Mail VARCHAR(255) NOT NULL,
    ID_Labo INT,
    CONSTRAINT fk_auteur_externe
        FOREIGN KEY(ID_Labo)
        REFERENCES Laboratoires_externes(ID_Labo) ON DELETE CASCADE ON UPDATE CASCADE
);
```
## Publications-Personnel Table
```sql
CREATE TABLE Publications_R_Personnel(
    ID_Publication INT NOT NULL, 
    ID_Personnel INT NOT NULL, 
    PRIMARY KEY (ID_Publication,ID_Personnel), 
    CONSTRAINT fk_Publication 
        FOREIGN KEY(ID_Publication) 
            REFERENCES Publications(ID_Publication)ON DELETE CASCADE ON UPDATE CASCADE, 
    CONSTRAINT fk_Personnel 
        FOREIGN KEY(ID_Personnel) 
            REFERENCES Personnel(ID_Personnel) ON DELETE CASCADE ON UPDATE CASCADE
);
```

## Doctorant-Encadrant Table
```sql
CREATE TABLE Doctorant_R_Encadrant(
    ID_Doctorant INT, 
    ID_Encadrant INT,
    CONSTRAINT fk_Doctorant 
        FOREIGN KEY(ID_Doctorant) 
            REFERENCES Doctorant(ID_Doctorant) ON DELETE CASCADE ON UPDATE CASCADE, 
    CONSTRAINT fk_Encadrant 
        FOREIGN KEY(ID_Encadrant)   
            REFERENCES Encadrant(ID_Encadrant) ON DELETE CASCADE ON UPDATE CASCADE, 
    PRIMARY KEY(ID_Doctorant,ID_Encadrant)
);
```

## Auteurs_externes_R_publications
```sql
CREATE table if not exists auteurs_externes_R_publications (
    id_publication serial not null,
    id_auteur serial not null,
    PRIMARY KEY (id_publication, id_auteur),
    CONSTRAINT fk_publication
      FOREIGN KEY (id_publication)
        REFERENCES publications(id_publication)
          on delete cascade
          on update cascade,
   CONSTRAINT fk_auteur
       FOREIGN KEY (id_auteur)
            REFERENCES auteurs_externes(id_auteur)
           on delete cascade
           on update cascade
);
```
## Projet_de_recherche_R_scientifique
```sql
CREATE table if not exists projet_de_recherche_R_scientifique (
    id_projet_de_recherche int not null,
    id_scientifique int not null,
    PRIMARY KEY (id_projet_de_recherche, id_scientifique),
    CONSTRAINT fk_projet_de_recherche
      FOREIGN KEY (id_projet_de_recherche)
        REFERENCES projet_de_recherche(id_projet)
          on delete cascade
          on update cascade,
   CONSTRAINT fk_scientifique
       FOREIGN KEY (id_scientifique)
            REFERENCES scientifique(id_scientifique)
           on delete cascade
           on update cascade
);
```
## Projet_de_Recherche_R_Partenaires Table
```sql
CREATE TABLE Projet_de_Recherche_R_Partenaires(
    ID_Projet INT,
    ID_Partenaire INT,
    CONSTRAINT fk_projet 
        FOREIGN KEY(ID_Projet) 
            REFERENCES Projet_de_Recherche(ID_Projet) ON UPDATE CASCADE ON DELETE CASCADE,
    CONSTRAINT fk_partenaire 
        FOREIGN KEY(ID_Partenaire) 
            REFERENCES Partenaire(ID_Partenaire) ON UPDATE CASCADE ON DELETE CASCADE,
    PRIMARY KEY(ID_Projet,ID_Partenaire)
);
```


# Requests
### 1. 
Le nom et le grade des encadrants du doctorant dont l'identifiant est 1
```sql
select nom, grade from doctorant_r_encadrant
join scientifique on id_scientifique = id_encadrant
join personnel on id_personnel = id_encadrant
where id_doctorant = 1;
```
### 2.
Le nom et le pays des auteurs collaborateurs (auteurs externes) du chercheur "Jean Azi" de 2016 à 2020
```sql
select ae.nom, ae.prenom, le.pays from personnel as per
join publications_r_personnel prp on per.id_personnel = prp.id_personnel
right join publications pub on pub.id_publication = prp.id_publication
right join auteurs_externes_r_publications aerp on pub.id_publication = aerp.id_publication
join auteurs_externes ae on ae.id_auteur = aerp.id_auteur
join laboratoires_externes le on ae.id_labo = le.id_labo
where per.nom = 'Azi' 
  and per.prenom = 'Jean' 
  and annee_de_publication >= '2016-01-01' 
  and annee_de_publication <= '2020-01-01';
```

### 3.
Le nombre de collaborateurs total du chercheur dont l'ID est 18
```sql
select count(ae.nom) from personnel as per
join publications_r_personnel prp on per.id_personnel = prp.id_personnel
right join publications pub on pub.id_publication = prp.id_publication
right join auteurs_externes_r_publications aerp on pub.id_publication = aerp.id_publication
join auteurs_externes ae on ae.id_auteur = aerp.id_auteur
where per.id_personnel = 18;
```

### 4.
Le nombre de pays avec lesquels le LAAS a collaboré dans le cadre de
publications de rang A (i.e., des articles publiés dans des conférences
de classe A)
```sql
select count(DISTINCT pays) from publications
right join auteurs_externes_r_publications aerp on publications.id_publication = aerp.id_publication
join auteurs_externes ae on aerp.id_auteur = ae.id_auteur
join laboratoires_externes le on ae.id_labo = le.id_labo
where publications.classe_de_la_conférence = 'A';
```

### 5.
Pour les doctorants, on souhaiterait récupérer le nombre de leurs publications. On veut retourner l'identifiant des 
doctorants accompagné du nombre de leur publication.
```sql
select id_doctorant, nom, prenom, count(*) as nombre_de_publications from doctorant
join personnel per on Doctorant.id_doctorant = per.id_personnel
join publications_r_personnel pubrper on id_doctorant = pubrper.id_personnel
join publications pub on pub.id_publication = pubrper.id_publication
group by id_doctorant, nom, prenom
```

### 6.
Le nombre de doctorants du laboratoire ayant soutenu
```sql
select count(*) from doctorant
where date_de_soutenance is not null;
```

### 7.
Le nom et le prénom des chercheurs qui n’ont jamais encadré
```sql
select nom, prenom from chercheur
join personnel per on id_chercheur = per.id_personnel
where id_chercheur not in (select * from encadrant);
```

### 8.
Le nom et le prénom des chercheurs qui n’ont jamais publié ni encadré
```sql
select nom, prenom from chercheur
join personnel on id_personnel = id_chercheur
where id_chercheur not in (select * from encadrant)
and id_chercheur not in (select id_personnel from publications_r_personnel);
```

### 9.
Le nom et prénom des chercheurs qui encadrent mais n’ont pas de doctorants ayant déjà soutenu
⚠ Ce ne montre pas les encadrants qui n'ont pas de doctorant, mais cela ne devrait pas arriver.
```sql
select nom, prenom from encadrant
join doctorant_r_encadrant dre on encadrant.id_encadrant = dre.id_encadrant
join Doctorant D on dre.id_doctorant = D.id_doctorant
join personnel P on encadrant.id_encadrant = P.id_personnel
where date_de_soutenance is null;
```

### 10.
L'identifiant,le nom et le prénom des doctorants avec un encadrant
```sql
select id_doctorant,nom,prenom, count(*) from doctorant_r_encadrant
join Personnel on id_personnel=id_doctorant
group by id_doctorant,nom,prenom
having count(distinct id_encadrant)=1;
```
### 15.
L'identifiant,le nom et le prénom des doctorants avec un encadrant
```sql
SELECT prp.id_personnel FROM publications pu
Natural Join publications_r_personnel prp
where prp.id_personnel in (select id_chercheur from chercheur) and pu.classe_de_la_conférence='A';
```


### 15.
L'identifiant,le nom et le prénom des doctorants avec un encadrant
```sql
SELECT count(Distinct id_chercheur_ens) FROM chercheur_enseignant
GROUP BY (id_etablissement)
```
### 16.
Le pays avec lequel le laboratoire a plus de publications
```sql
SELECT pays, count(*) nombre_publication 
FROM Laboratoires_externes 
JOIN Auteurs_Externes on Auteurs_Externes.ID_Labo = Laboratoires_Externes.ID_Labo 
JOIN Auteurs_Externes_R_Publications on Auteurs_Externes_R_publications.id_auteur = auteurs_externes.id_auteur 
GROUP BY pays
ORDER BY nombre_publication DESC LIMIT 1;
```

### 17.
Les scientifiques qui ont un seul projet
```sql
SELECT Nom,prenom,scientifique.id_scientifique, count(*) Nombre_Projet 
FROM personnel 
JOIN Scientifique on Scientifique.id_scientifique = personnel.id_personnel 
JOIN Projet_de_recherche_R_scientifique on Projet_de_recherche_R_scientifique.id_scientifique = scientifique.id_scientifique 
GROUP BY Nom, prenom, scientifique.id_scientifique
HAVING count(*) = 1; 
```

### 18.
Les scientifiques qui auraient participé à tous les projets
```sql
SELECT Nom,prenom,scientifique.id_scientifique, count(*) Nombre_Projet 
FROM personnel 
JOIN Scientifique on Scientifique.id_scientifique = personnel.id_personnel 
JOIN Projet_de_recherche_R_scientifique on Projet_de_recherche_R_scientifique.id_scientifique = scientifique.id_scientifique 
GROUP BY Nom, prenom, scientifique.id_scientifique
HAVING count(*) = (
	SELECT count(*) 
	FROM PROJET_de_Recherche
); 
```

### 19.
Les établissements d'enseignements ayant plus de 50 enseignants-chercheurs appartenant au LAAS
```sql
SELECT nom, count(*) nb_chercheur 
FROM Etablissement 
JOIN Chercheur_enseignant on Chercheur_enseignant.id_etablissement=Etablissement.Id_Etablissement 
GROUP BY nom 
HAVING count(*)>50;
```

### 20.
Les scientifiques qui ont le plus de projets 
```sql

```

### .21
Les pays qui sont impliqués dans tous les projets 
```sql
SELECT pays, count(*) nb_projet_diff 
FROM  (
	     SELECT pays, id_projet 
	     From Partenaire 
	     JOIN projet_de_recherche_R_partenaires on projet_de_recherche_R_partenaires.id_partenaire = partenaire.id_partenaire 
	    GROUP BY pays,id_projet) as Proj 
GROUP BY pays HAVING count(*) = ( 
 	SELECT count(*) 
	 FROM PROJET_de_Recherche
);
```

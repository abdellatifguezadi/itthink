# ITThink Database

## Contexte

**ITThink** est une plateforme qui met en relation des utilisateurs, des freelances et des projets. Ce projet vise à concevoir une base de données relationnelle efficace pour gérer ces entités et leurs relations.

## Schéma de la Base de Données

Les principales tables sont :

- **Utilisateurs** : Contient les informations des utilisateurs (ID, nom, email, etc.).
- **Catégories** : Contient les catégories des projets.
- **Sous-Catégories** : Contient les sous-catégories liées aux catégories.
- **Projets** : Contient les projets soumis par les utilisateurs.
- **Freelances** : Contient les freelances et leurs compétences.
- **Offres** : Contient les offres faites par les freelances pour les projets.
- **Témoignages** : Contient les témoignages laissés par les utilisateurs.

### Relations principales :

- Un utilisateur peut avoir plusieurs projets.
- Un projet appartient à une catégorie et à une sous-catégorie.
- Un freelance peut proposer plusieurs offres pour des projets.

## Scripts SQL

### Création de la Base et des Tables

```sql
CREATE DATABASE ITThink;

USE ITThink;

CREATE TABLE Utilisateurs (
    id_utilisateur INT AUTO_INCREMENT PRIMARY KEY,
    nom_utilisateur VARCHAR(255),
    email VARCHAR(255) UNIQUE,
    mot_de_passe VARCHAR(255)
);

CREATE TABLE Categories (
    id_categorie INT AUTO_INCREMENT PRIMARY KEY,
    nom_categorie VARCHAR(255)
);

CREATE TABLE SousCategories (
    id_sous_categorie INT AUTO_INCREMENT PRIMARY KEY,
    nom_sous_categorie VARCHAR(255),
    id_categorie INT,
    FOREIGN KEY (id_categorie) REFERENCES Categories(id_categorie)
);

CREATE TABLE Projets (
    id_projet INT AUTO_INCREMENT PRIMARY KEY,
    titre_projet VARCHAR(255),
    description TEXT,
    id_utilisateur INT,
    id_categorie INT,
    id_sous_categorie INT,
    FOREIGN KEY (id_utilisateur) REFERENCES Utilisateurs(id_utilisateur),
    FOREIGN KEY (id_categorie) REFERENCES Categories(id_categorie),
    FOREIGN KEY (id_sous_categorie) REFERENCES SousCategories(id_sous_categorie)
);

CREATE TABLE Freelances (
    id_freelance INT AUTO_INCREMENT PRIMARY KEY,
    nom_freelance VARCHAR(255),
    competences TEXT,
    id_utilisateur INT,
    FOREIGN KEY (id_utilisateur) REFERENCES Utilisateurs(id_utilisateur)
);

CREATE TABLE Offres (
    id_offre INT AUTO_INCREMENT PRIMARY KEY,
    montant DECIMAL(10, 2),
    delai INT,
    id_freelance INT,
    id_projet INT,
    FOREIGN KEY (id_freelance) REFERENCES Freelances(id_freelance),
    FOREIGN KEY (id_projet) REFERENCES Projets(id_projet)
);

CREATE TABLE Temoignages (
    id_temoignage INT AUTO_INCREMENT PRIMARY KEY,
    commentaire TEXT,
    id_utilisateur INT,
    FOREIGN KEY (id_utilisateur) REFERENCES Utilisateurs(id_utilisateur)
);


### Explication du contenu :

- **Contexte** : Présente le but de la base de données et les entités principales.
- **Schéma de la base de données** : Détaille les tables principales et leurs relations.
- **Scripts SQL** : Comprend les requêtes pour créer les tables, ainsi que des exemples d'opérations courantes (insertion, mise à jour, suppression).
- **Installation** : Instructions pour cloner le projet et importer le fichier SQL.
- **Auteurs** et **License** : Sections pour indiquer l'auteur du projet et la licence associée.




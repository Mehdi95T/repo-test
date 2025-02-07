# ConformiTrain

## 1. Présentation du projet
ConformiTrain est une application de bureau développée en JavaFX, conçue pour aider les entreprises ferroviaires à gérer la conformité et les inspections de sécurité des trains. L'objectif est de remplacer le suivi papier des inspections par une solution numérique efficace, réduisant ainsi les erreurs et améliorant le respect des normes de sécurité.

## 2. Technologies utilisées
- **Langage** : Java
- **Framework** : JavaFX
- **Base de données** : SQL (hébergée en ligne)
- **Gestion du code** : Git (GitHub/GitLab)
- **Outils de planification** : Trello

## 3. Rôles des utilisateurs
- **Administrateurs** : Gèrent les comptes des managers et inspecteurs.
- **Managers** : Assignent les mises en conformité aux inspecteurs, valident et corrigent les inspections.
- **Inspecteurs** : Réalisent les inspections et complètent les formulaires numériques.

## 4. Fonctionnalités principales
- **Gestion des utilisateurs** : Création, suppression et modification des comptes (admin).
- **Assignation des mises en conformité** : Les managers peuvent assigner des tâches aux inspecteurs.
- **Formulaires d'inspection interactifs** : Les inspecteurs complètent les inspections via l'application.
- **Validation et correction des inspections** : Les managers vérifient et valident les inspections.
- **Génération et stockage des rapports PDF** : Une fois validée, chaque inspection est exportée et stockée en PDF.
- **Système de notifications** :
  - Un inspecteur est notifié lorsqu'une mise en conformité lui est assignée.
  - Un manager est alerté quand une mise en conformité approche de l'expiration.

## 5. Diagramme de cas d'utilisation
![Diagramme Cas d'Utilisation](cas_utilisation.png)

## 6. Diagramme de classes
![Diagramme de Classes](diagramme_classes.png)

## 7. Modèle relationnel de la base de données

### Tables principales
```sql
CREATE TABLE Utilisateur (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(50),
    prenom VARCHAR(50),
    email VARCHAR(100) UNIQUE,
    mot_de_passe VARCHAR(255),
    role ENUM('Admin', 'Manager', 'Inspecteur')
);

CREATE TABLE MiseEnConformite (
    id INT PRIMARY KEY AUTO_INCREMENT,
    titre VARCHAR(255),
    description TEXT,
    date_limite DATE,
    statut ENUM('A faire', 'En cours', 'Validée'),
    id_manager INT,
    FOREIGN KEY (id_manager) REFERENCES Utilisateur(id)
);

CREATE TABLE Inspection (
    id INT PRIMARY KEY AUTO_INCREMENT,
    id_inspecteur INT,
    id_conformite INT,
    date_inspection DATE,
    statut ENUM('En attente', 'Corrigé', 'Validé'),
    pdf_stocke VARCHAR(255),
    FOREIGN KEY (id_inspecteur) REFERENCES Utilisateur(id),
    FOREIGN KEY (id_conformite) REFERENCES MiseEnConformite(id)
);

CREATE TABLE Notification (
    id INT PRIMARY KEY AUTO_INCREMENT,
    id_utilisateur INT,
    message TEXT,
    date_envoi TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    est_lu BOOLEAN DEFAULT FALSE,
    FOREIGN KEY (id_utilisateur) REFERENCES Utilisateur(id)
);
```

## 8. Organisation du code
```
- src/
  - dao/         # Gestion de la BDD
  - modele/      # Modèles (Classes métier)
  - service/     # Logique métier
  - vue/         # Interface utilisateur JavaFX
```

## 9. Planification et Diagramme de Gantt
![Diagramme de Gantt](gantt.png)

### Étapes principales
1. **Conception** : Diagrammes UML, Modèle de base de données.
2. **Développement Backend** : DAO, services, gestion des utilisateurs.
3. **Développement Frontend** : Interfaces en JavaFX.
4. **Implémentation des fonctionnalités** : Notifications, PDF, authentification.
5. **Tests et validation**.
6. **Finalisation et documentation**.

## 10. Dépôt GitHub
Le code source est disponible ici : [Lien GitHub](https://github.com/Mehdi95T/ConformiTrain_JavaFX)

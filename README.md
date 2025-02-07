# ConformiTrain

## 1. Présentation de l'équipe
Nous sommes une équipe composée de trois personnes:
- **Mehdi Tarchoul**
- **Mathys Sousa**
- **Mouhamad Fall**

Nous collaborons pour développer une application innovante destinée à améliorer la sécurité des trains.

## 2. Contexte
L'application est développée pour une entreprise spécialisée dans la gestion de la sécurité ferroviaire, qui rencontre des difficultés dans la gestion des inspections de sécurité de ses trains. Actuellement, les techniciens utilisent des fiches papier pour consigner les résultats des inspections, ce qui entraîne des erreurs et des retards dans la mise à jour des informations critiques. Ces problèmes compromettent la conformité aux réglementations et, par conséquent, la sécurité des passagers.

## 3. Solutions proposées
Pour répondre aux besoins identifiés, nous avons conçu **ConformiTrain**, une application qui permet de gérer efficacement les inspections de sécurité des trains.

### Fonctionnalités de ConformiTrain
- **Remplissage de formulaires** : Les inspecteurs peuvent facilement remplir des formulaires d’inspection directement dans l'application, facilitant ainsi la saisie des données.
- **Récupération de formulaires avec affectation de conformité** : L'application permet aux inspecteurs de récupérer les formulaires précédemment complétés et de les associer à des états de conformité.
- **Affectation des dates de mise en conformité** : Les manageurs vont pouvoir placer les rendez-vous conformités pour chaque inspecteur.
- **Vérification des dates de péremption de la conformité** : Les utilisateurs peuvent suivre les dates de péremption des conformités afin de garantir que toutes les inspections sont à jour et conformes aux normes de sécurité.

## 4. Technologies utilisées
- **Langage** : Java
- **Framework** : JavaFX
- **Base de données** : SQL (hébergée en ligne)
- **Gestion du code** : Git (GitHub/GitLab)
- **Outils de planification** : Trello

## 5. Rôles des utilisateurs
- **Administrateurs** : Gèrent les comptes des managers et inspecteurs.
- **Managers** : Assignent les mises en conformité aux inspecteurs, valident et corrigent les inspections.
- **Inspecteurs** : Réalisent les inspections et complètent les formulaires numériques.

## 6. Fonctionnalités principales
- **Gestion des utilisateurs** : Création, suppression et modification des comptes (admin).
- **Assignation des mises en conformité** : Les managers peuvent assigner des tâches aux inspecteurs.
- **Formulaires d'inspection interactifs** : Les inspecteurs complètent les inspections via l'application.
- **Validation et correction des inspections** : Les managers vérifient et valident les inspections.
- **Génération et stockage des rapports PDF** : Une fois validée, chaque inspection est exportée et stockée en PDF.
- **Système de notifications** :
  - Un inspecteur est notifié lorsqu'une mise en conformité lui est assignée.
  - Un manager est alerté quand une mise en conformité approche de l'expiration.

## 7. Exemple de maquette de l'application
### Vue Connexion
![conformitrain maquette 1](conformitrain%20img/Conformitrain%20maquette%20(1).png)

### Vue Manageurs pour les formulaires de mise en conformité non validés encore
![conformitrain maquette](conformitrain%20img/Conformitrain%20maquette%20(4).png)

### Vue Manageurs pour les formulaires de mise en conformité qui on été validés
![conformitrain maquette](conformitrain%20img/Conformitrain%20maquette%20(5).png)

### Vue Inspecteur
![conformitrain maquette 2](conformitrain%20img/Conformitrain%20maquette(2).png)    

### Vue Formulaire
![conformitrain maquette 3](conformitrain%20img/Conformitrain%20maquette(3).png)    

## 8. User Case
![Diagramme User Case](user_case.png)

## 9. Diagramme de classes
![Diagramme de Classes](diagramme%20classe.png)

## 10. Modèle relationnel de la base de données

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

## 11. Organisation du code
```
- src/
  - dao/         # Gestion de la BDD
  - modele/      # Modèles (Classes métier)
  - service/     # Logique métier
  - vue/         # Interface utilisateur JavaFX
```

## 12. Planification et Diagramme de Gantt
![Diagramme de Gantt](gantt.png)

### Étapes principales
1. **Conception** : Diagrammes UML, Modèle de base de données.
2. **Développement Backend** : DAO, services, gestion des utilisateurs.
3. **Développement Frontend** : Interfaces en JavaFX.
4. **Implémentation des fonctionnalités** : Notifications, PDF, authentification.
5. **Tests et validation**.
6. **Finalisation et documentation**.

## 13. Dépôt GitHub
Le code source est disponible ici : [Lien GitHub](https://github.com/Mehdi95T/ConformiTrain_JavaFX)

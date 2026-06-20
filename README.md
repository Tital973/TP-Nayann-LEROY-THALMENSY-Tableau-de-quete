# Tableau des Quêtes RPG

Projet réalisé dans le cadre du TP Vue.js de développement Web.

# Présentation

Cette application est un gestionnaire de quêtes inspiré des jeux de rôle .

Elle permet de créer, modifier, supprimer et suivre l'avancement de différentes quêtes à travers plusieurs colonnes représentant leur état.

Le projet a été développé avec Vue.js afin de mettre en pratique :

- Les composants
- Les props
- Les emits
- Les directives Vue
- Les propriétés calculées (computed)
- Les watchers
- La persistance des données avec localStorage

# Thème choisi

J'ai choisi le thème RPG car il permet de rendre le projet plus ludique tout en conservant les mêmes fonctionnalités qu'un gestionnaire de tâches classique.

Chaque tâche est représentée par une quête possédant :

- un titre
- une description
- une difficulté
- une récompense
- un statut
# Fonctionnalités implémentées :

## Gestion des quêtes

- Ajout d'une nouvelle quête
- Modification d'une quête existante
- Suppression d'une quête
- Validation du titre obligatoire

## Gestion des statuts

Chaque quête peut avoir l'un des statuts suivants :

- Disponible
- En cours
- Terminée
- Échouée

Les quêtes peuvent être déplacées entre les colonnes grâce aux boutons d'action.

## Affichage dynamique

- Génération des colonnes avec `v-for`
- Génération des cartes avec `v-for`
- Affichage conditionnel avec `v-if`
- Badge spécial lorsque la quête est terminée
- Bouton Supprimer masqué pour les quêtes terminées

## Difficulté
Chaque quête possède un niveau de difficulté :

- Facile
- Moyenne
- Difficile

La couleur de la carte change selon la difficulté.

## Persistance des données

Les quêtes sont automatiquement sauvegardées dans le navigateur grâce au `localStorage`.
Les données sont restaurées automatiquement lors du rechargement de la page.

## Statistiques

Une propriété calculée (`computed`) permet d'afficher le nombre total de quêtes terminées .

# Architecture du projet

src/
│
├── components/
│   ├── Board.vue
│   ├── Column.vue
│   ├── Cards.vue
│   └── Form.vue
│
├── App.vue
└── main.js


### App.vue

Composant principal :

- stocke les données
- gère les méthodes
- gère localStorage
- centralise les événements

### Form.vue

Gestion du formulaire :

- ajout
- modification
- validation

### Board.vue

Affichage global du tableau.

### Column.vue

Affichage d'une colonne selon son statut.

### Cards.vue

Affichage d'une quête individuelle et de ses actions.

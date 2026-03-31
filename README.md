# Planificateur d'Itinéraire Urbain

[![Release](https://img.shields.io/badge/version-1.2.0-blue.svg)](https://moule.informatique.univ-paris-diderot.fr/delarmin/gla-groupe-3-lundi/-/releases)
[![Java](https://img.shields.io/badge/Java-17+-orange.svg)](https://www.oracle.com/java/)
[![Maven](https://img.shields.io/badge/Maven-3.6+-red.svg)](https://maven.apache.org/)

Un logiciel de planification d'itinéraire urbain qui calcule les trajets les plus optimisés en temps ou en distance sur le réseau de transport d'Île-de-France.

**[📺 Regardez la démonstration du produit](https://www.youtube.com/watch?v=-vzrLvmfEwU)**

## Caractéristiques principales

- ✅ **Calcul d'itinéraires optimisés** : En temps ou en distance
- 🗺️ **Intégration cartographique** : Affichage interactif sur une carte
- 🚌 **Support multi-transports** : Bus, métro, RER, tram, piéton
- ⏰ **Gestion des horaires** : Recherche en fonction des horaires réels
- 🚶 **Déplacements à pied** : Intégration des chemins piétons au début, pendant et à la fin du trajet
- 📍 **Recherche flexible** : Par adresse ou coordonnées GPS
- 🔄 **Réseau IDFM** : Données à jour du réseau de transport Île-de-France

## 📋 Table des matières

- [Installation](#installation)
- [Utilisation](#utilisation)
- [Architecture](#architecture)
- [Tests](#tests)
- [Structure du projet](#structure-du-projet)
- [Contribution](#contribution)
- [Historique des versions](#historique-des-versions)
- [Auteurs](#auteurs)



## Installation

### Prérequis

| Requirement | Version |
|-------------|---------|
| Java JDK | 17+ |
| Maven | 3.6+ |
| Connexion internet | Recommandée |

> **Note** : Une connexion internet est requise pour afficher la carte et faire les recherches par adresses. Sans connexion, vous devez fournir des coordonnées GPS valides en Île-de-France.

### Clonage du projet

Deux méthodes disponibles :

**Option 1 : Git (recommandé)**
```bash
git clone https://moule.informatique.univ-paris-diderot.fr/delarmin/gla-groupe-3-lundi.git
cd gla-groupe-3-lundi
```

**Option 2 : Téléchargement**
Téléchargez la dernière version depuis les [releases](https://moule.informatique.univ-paris-diderot.fr/delarmin/gla-groupe-3-lundi/-/releases)

### Compilation

Le projet utilise **Maven** pour la gestion de la construction.

```bash
# Compilation et tests
make all
```

Ou directement avec Maven :
```bash
mvn clean verify
```

Cela générera un JAR dans le dossier `target/`

## Utilisation

### Démarrage rapide

```bash
make run
```

Cette commande :
1. ✓ Crée les fichiers de configuration
2. ✓ Télécharge les données du réseau IDFM
3. ✓ Lance l'interface graphique

### Options de lancement avancé

Le JAR compilé accepte plusieurs options :

```bash
java -jar target/project-1.2.0.jar [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--gui` | Lance l'interface graphique (configuration automatique) |
| `--create-files` | Crée les fichiers CSV de données et le dossier d'horaires |
| `--parse` | Parse les fichiers et crée le modèle du programme (debug) |
| `--info` | Affiche les informations de l'application |
| `--help` | Affiche le manuel d'utilisation |

### Exemples d'utilisation

```bash
# Lancer avec interface graphique
java -jar target/project-1.2.0.jar --gui

# Créer uniquement les fichiers de données
java -jar target/project-1.2.0.jar --create-files

# Afficher les informations de l'application
java -jar target/project-1.2.0.jar --info
```

### Interface graphique

L'application offre une interface intuitive pour :
- Saisir votre point de départ et d'arrivée
- Choisir le mode d'optimisation (temps ou distance)
- Visualiser l'itinéraire sur la carte
- Consulter les horaires des transports
- Voir les détails du trajet (arrêts, correspondances, temps, etc.) 

### Tests

Deux suites de tests optionnelles pour la validation et l'optimisation :

**Test de déterminisme** - Validation de la génération de fichiers :
```bash
mvn test -D runDeterminismTest=true
```
> ⏱️ Peut être long à exécuter

**Test d'efficacité** - Analyse des performances de l'algorithme :
```bash
mvn test -D runEfficiencyTest=true
```
> Génère un log avec les résultats de recherche et leurs temps d'exécution

**Tous les tests** :
```bash
mvn test
```

## Architecture

### Vue d'ensemble

Le projet suit une architecture en couches :

```
┌─────────────────────────────────┐
│      Interface Graphique (GUI)  │
├─────────────────────────────────┤
│    Contrôleurs (Keyboard/Mouse) │
├─────────────────────────────────┤
│    Modèle (Graph, Itinerary)    │
├─────────────────────────────────┤
│  Algorithme A* + Cost Functions │
├─────────────────────────────────┤
│    Extraction IDFM (CSV)        │
└─────────────────────────────────┘
```

### Composants principaux

| Composant | Description |
|-----------|-------------|
| **AStar** | Implémentation de l'algorithme A* pour la recherche d'itinéraires |
| **Graph** | Structure de graphe représentant le réseau de transport |
| **GUI** | Interface graphique interactive avec cartographie |
| **Controllers** | Gestion des entrées utilisateur (clavier, souris) |
| **IDFM** | Extraction et parsing des données du réseau |
| **Utils** | Fonctions utilitaires (GPS, CSV, etc.) |

## Structure du projet

```
Map_itinerary/
├── src/
│   ├── main/java/fr/u_paris/gla/project/
│   │   ├── astar/           # Algorithme de recherche d'itinéraire
│   │   ├── controllers/     # Gestion des entrées utilisateur
│   │   ├── graph/           # Modèle du réseau de transport
│   │   ├── idfm/            # Extraction des données IDFM
│   │   ├── io/              # Format et sérialisation
│   │   ├── utils/           # Utilités (GPS, CSV, etc.)
│   │   └── views/           # Interface graphique
│   ├── test/java/           # Tests unitaires
│   └── resources/           # Ressources
├── target/                  # Fichiers compilés
├── UML/                     # Diagrammes UML
├── pom.xml                  # Configuration Maven
├── Makefile                 # Commandes de construction
└── README.md               # Ce fichier
```

## 📚 Documentation et aide

Pour des explications plus détaillées concernant l'utilisation et la structure, consultez le [wiki du projet](https://moule.informatique.univ-paris-diderot.fr/delarmin/gla-groupe-3-lundi/-/wikis/home).

## 🤝 Contribution

Les contributions sont bienvenues ! Voici comment contribuer :

1. Créez une branche pour votre feature : `git checkout -b feature/AmazingFeature`
2. Commandez vos changements : `git commit -m 'Add AmazingFeature'`
3. Pushez vers la branche : `git push origin feature/AmazingFeature`
4. Ouvrez une Pull Request

Veuillez vous assurer que :
- ✓ Le code compile sans erreurs
- ✓ Les tests passent : `mvn test`
- ✓ Le code suit les conventions du projet
- ✓ Les messages de commit sont clairs et explicites

## 📝 Historique des versions

### 1.2.0 - Version finale

**Nouvelles fonctionnalités :**
- ✨ Optimalité des trajets en temps
- ⏰ Affichage des horaires pour chaque station
- 🚶 Déplacements à pied (début, pendant, fin du trajet)

**Améliorations :**
- 🎨 Amélioration de l'UI/UX
- ⚡ Optimisation de l'algorithme
- 🐛 Corrections de bugs
- 🔧 Refactorisation du code

### 1.1.0

- Ajout de la gestion des horaires
- Optimisation des résultats
- Amélioration de l'interface utilisateur

### 1.0.0

- Prototype initial

## 👥 Auteurs

Pour plus d'informations sur l'équipe de développement, consultez [contacts.md](contacts.md)

---

## 📄 Licence

Projet réalisé dans le cadre du cours de Génie Logiciel Avancé - Université Paris Cité

**Dernière mise à jour :** Janvier 2025


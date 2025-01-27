# jenkins_pipeline_test

Ce projet contient un exemple simple de pipeline Jenkins utilisant Maven pour la construction, les tests et le déploiement d'un projet Java.

## Prérequis

Avant d'exécuter ce projet, assurez-vous d'avoir les éléments suivants installés :

- [Java JDK 17+](https://openjdk.java.net/)
- [Maven 3.x](https://maven.apache.org/)
- [Jenkins](https://www.jenkins.io/) configuré avec le plugin Maven

## Cloner le dépôt

Clonez ce projet dans votre répertoire local en utilisant Git :

```bash
git clone https://github.com/Nouhaila1937/jenkins_pipeline_test.git
cd jenkins_pipeline_test
```
## Description du pipeline Jenkins
Ce projet utilise un pipeline Jenkins pour automatiser les étapes suivantes :

-  Installation de Maven : Le pipeline vérifie que Maven est installé et disponible dans le chemin d'exécution.
-   Echo de la version de Maven : Affiche la version de Maven utilisée dans le pipeline.
-   Build : Compile le projet en utilisant Maven avec la commande mvn clean package -DskipTests=true.
-  Tests unitaires : Exécute les tests unitaires avec mvn test.

## Comment utiliser
-   Configurer Jenkins :

Créez un nouveau job Jenkins en sélectionnant "Pipeline" comme type de projet.
Dans la configuration du job, assurez-vous d'utiliser un agent qui a Maven et Java installés.
-   Configurer le dépôt Git dans Jenkins :

Ajoutez l'URL du dépôt Git dans la configuration du job.
Exemple d'URL : https://github.com/Nouhaila1937/jenkins_pipeline_test.git
-  Configurer le pipeline :

Dans le champ "Pipeline Script", sélectionnez "Pipeline script " et spécifiez le dépôt Git 
```bash
pipeline {
    agent any

    tools {
        maven "M399"
    }

    stages {
        stage('Echo Version') {
            steps {
                sh "echo 'Printing Maven Version'"
                sh "mvn -version"
            }
        }

        stage('Build') {
    steps {
        // Cloner le dépôt
        git branch: 'main', url: 'https://github.com/Nouhaila1937/jenkins_pipeline_test'

        // Se déplacer dans le sous-répertoire contenant le pom.xml
        dir('jenkins-pipeline-demo') {
            // Afficher les fichiers du répertoire pour vérifier la présence du pom.xml
            sh "ls -l"

            // Exécuter Maven dans le répertoire où se trouve le pom.xml
            sh "mvn clean package -DskipTests=true"
        }
    }
}
        stage('Unit Test') {
            steps {
               // Se déplacer dans le répertoire contenant le pom.xml pour exécuter les tests
                dir('jenkins-pipeline-demo') {
                    // Exécuter les tests unitaires avec Maven
                    sh "mvn test"
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline terminé.'
        }

        success {
            echo 'Le build et les tests ont réussi.'
        }

        failure {
            echo 'Le build ou les tests ont échoué.'
        }
    }
}
```
-  Lancer le job Jenkins :

Cliquez sur "Build Now" pour exécuter le pipeline et voir les résultats.
Exemple de commande Maven
Voici quelques commandes Maven que tu peux utiliser dans ton projet :

## Construire le projet :
```bash
mvn clean package -DskipTests=true
```
## Exécuter les tests unitaires :
```bash
mvn test
```
## Compiler le projet :
```bash
mvn compile
```

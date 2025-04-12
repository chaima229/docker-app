node{

    stage("SCM Checkout"){
        git credentialsId: 'git-credentials', branch: 'main', url: 'https://github.com/chaima229/docker-app.git'
    }
    
    stage("MVN package"){
        def mvnHome = tool name: 'maven-tool', type: 'maven'
        def mvnCMD = "${mvnHome}/bin/mvn"
        sh "${mvnCMD} clean package"
    }

    stage("Build Docker Image"){
        sh "build -t chaima229/docker-app:1.0.0 ."
    }

    stage("Push Docker Image"){
        withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerHubPwd')]) {
            sh "docker login -u mellouk -p ${dockerHubPwd}"
        }
        sh "docker push chaima229/docker-app:1.0.0"
    }
    
    stage("Run Container on Dev Server"){
        sh "docker run -d -p 8081:8080 --name my-app-v2 Jenkinsfile"
    }




// pipeline {
//     agent any

//     stages {
//         // Étape 1 : Checkout du code source depuis Git
//         stage('Checkout') {
//             steps {
//                 git credentialsId: 'git-credentials', branch: 'main', url: 'https://github.com/chaima229/docker-app.git'
//             }
//         }

//         // Étape 2 : Construction du projet avec Maven
//         stage('Build with Maven') {
//             steps {
//                 script {
//                     def mvnHome = tool name: 'maven-tool', type: 'maven'
//                     def mvnCMD = "${mvnHome}/bin/mvn"
//                     sh "${mvnCMD} clean package"
//                 }
//             }
//         }

//         // Étape 3 : Vérification de la version Docker
//         stage('Check Docker Version') {
//             steps {
//                 sh 'docker --version'
//             }
//         }

//         // Étape 4 : Vérification des permissions du socket Docker
//         stage('Check Docker Socket Permissions') {
//             steps {
//                 sh 'ls -l /var/run/docker.sock'
//             }
//         }

//         // Étape 5 : Construction de l'image Docker
//         stage('Build Docker Image') {
//             steps {
//                 sh 'docker build -t chaima229/docker-app:1.0.0 .'
//             }
//         }

//         // Étape 6 : Pousser l'image Docker vers Docker Hub
//         stage('Push Docker Image') {
//             steps {
//                 withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerHubPwd')]) {
//                     sh 'echo $dockerHubPwd | docker login -u chaimaamellouk --password-stdin'
//                 }
//                 sh 'docker push chaima229/docker-app:1.0.0'
//             }
//         }

//         // Étape 7 : Lancer le conteneur Docker (optionnel)
//         stage('Run Docker Container') {
//             steps {
//                 sh 'docker run -d -p 8080:8080 --name myapp-container chaima229/docker-app:1.0.0'
//             }
//         }
//     }

//     // Gestion des erreurs et succès
//     post {
//         failure {
//             echo 'Pipeline failed!'
//         }
//         success {
//             echo 'Pipeline succeeded!'
//         }
//     }
// }

    
// }



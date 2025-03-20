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
    
}



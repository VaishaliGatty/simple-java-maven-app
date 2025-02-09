pipeline {
    agent any

    tools {
        maven 'local_maven'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving artifacts'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

       stage('Deploy to Tomcat') {
    steps {
        script {
            withCredentials([usernamePassword(credentialsId: 'Tomcat-cred', 
                                             usernameVariable: 'TOMCAT_USER', 
                                             passwordVariable: 'TOMCAT_PASS')]) {
                echo 'Deploying WAR to Tomcat...'
                deploy adapters: [tomcat9(
                    credentialsId: 'Tomcat-cred', 
                    url: 'http://localhost:8080/manager/text', // Correct URL
                    path: '/',
                    war: '**/target/*.war'
                )]
            }
        }
    }
}

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}

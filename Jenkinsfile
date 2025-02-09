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
                    // Using Jenkins credentials securely
                //    withCredentials([usernamePassword(credentialsId: 'Tomcat-cred', 
                //         usernameVariable: 'TOMCAT_USER', 
                //         passwordVariable: 'TOMCAT_PASS')]) {
                //         echo 'Deploying WAR to Tomcat...'
                //         deploy adapters: [tomcat9(
                //             credentialsId: 'Tomcat-cred', 
                //             url: 'http://localhost:8080/manager', 
                //             username: TOMCAT_USER, 
                //             password: TOMCAT_PASS,
                //             path: ''
                //         )], war: '**/*.war', contextPath: '/'
                //     }
                deploy contextPath: 'simple-java-maven-app', war: 'target/*.war'
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

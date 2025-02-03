pipeline{
    agent any
     tools {
        maven 'local_maven'
    }
    stages{
    stage('Build')
    {
        steps{
            echo 'Building the project...'
            bat 'mvn clean package'
        }
        post{
            success{
                echo 'archieve artifacts'
               archiveArtifacts artifacts: '**/*.war'
            }
        }
    }
    stage('Deploy to Tomcat'){
      steps{
        deploy adapters: [tomcat9(credentialsId:'Tomcat-cred',path: '', url: 'http://localhost:8080/',username: TOMCAT_USER,
                            password: TOMCAT_PASS)], contextPath: null, war: '**/*.war'
      }
    }
}
}

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
        deploy adapters: [tomcat9(path: '', url: 'http://localhost:8080/', username: 'Vaish',
                            password: '1234')], contextPath: null, war: '**/*.war'
      }
    }
}
}

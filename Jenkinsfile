pipeline {
    agent any

    stages {
        stage('pull scm git ') {
            steps {
                git branch: 'main', url: 'https://github.com/GitUzair/Amazon-Jenkins.git'
            }
        }
        stage('compile ') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('build') {
            steps {
                 sh 'mvn clean install'
            }
        }

        
    }

  post{

  success{
     echo 'Build is success'
  }
    
  failure{
       echo 'Failure in the build'
   }

  }

}

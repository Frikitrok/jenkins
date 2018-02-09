pipeline {
    agent {
        node {
          label 'master'
        }
    }
    stages {
        stage('Clone git repo') {
            steps {
                sh 'rm -rf ./maven'
                //sh 'git clone https://github.com/Frikitrok/maven-hometask ./maven'
            }
        }
        stage('Make build') {
            agent {
                docker { 
                    image 'maven:alpine' 
                    //args  '-v /var/lib/jenkins/workspace/maven-proj/maven/:/maven'
                    customWorkspace './maven'
                }
            }
            steps {
                sh 'ls -la'
                sh 'mvn install'
            }
        }
    }
}

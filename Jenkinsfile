pipeline {
    agent {
        node {
          label 'master'
        }
    }
    stages {
        stage('Clone git repo') {
            steps {
                sh 'rm -rf /tmp/maven'
                sh 'git clone https://github.com/Frikitrok/maven-hometask /tmp/maven'
            }
        }
        stage('Make build') {
            agent {
                docker { 
                    image 'maven:alpine' 
                    args  '-v /tmp/maven:/maven'
                }
            }
            steps {
                sh 'cd /maven'
                sh 'mvn install'
            }
        }
    }
}

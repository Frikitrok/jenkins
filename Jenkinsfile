peline {
    agent {
        node {
          label 'master'
        }
    }
    stages {
        stage('Clone git repo') {
            steps {
                sh 'rm -rf ./gradle'
                //sh 'git clone https://github.com/Frikitrok/gradle-hometask ./gradle'
            }
        }
        stage('Make build') {
            agent {
                docker { 
                    image 'gradle:alpine' 
                    customWorkspace './gradle'
                }
            }
            steps {
                sh 'ls -la'
                sh 'gradle clean build'
            }
        }
    }
}


pipeline {
    agent {
        node {
          label 'master'
        }
    }
    stages {
        stage('Get and Make build') {
            agent {
                docker { 
                    image 'gradle:alpine' 
                    customWorkspace './gradle'
                }
            }
            steps {
                sh 'ls -la'
                sh 'gradle clean build'
                sh 'ls -la'
            }
        }
        stage('Push to Artifactory'){
            agent  {
                label {
                    label 'master'
                    customWorkspace './gradle'
                }
            }
            steps{
                sh 'cd ../..'
                sh 'ls -la'
                script {
                     def server = Artifactory.server('artifactory-main')
                     def buildInfo = Artifactory.newBuildInfo()
                   //  def rtGradle = Artifactory.newGradleBuild()
                     server.publishBuildInfo(buildInfo)
                     
                     def uploadSpec = """{
                      "files": [
                        {
                          "pattern": "./build/libs/*.jar",
                          "target": "generic-local"
                        }
                     ]
                    }"""
                    server.upload(uploadSpec)
                }
            }
        }
        stage('Clear old builds') {
            agent  {
                label {
                    label 'master'
                    customWorkspace './gradle'
                }
            }
            steps {
                sh 'rm -rf *'
            }
        }
    }
}



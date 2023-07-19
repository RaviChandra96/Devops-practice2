pipeline {
    agent {
        node {
            label 'java11'
        }
    
    }

    options {
                timestamps()
                buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '2'))
                timeout(time: 240, unit: 'MINUTES')
               // disableConcurrentBuilds()
                }

        stages {
            stage ('AppCodeCheckout') {
                steps {

                    git 'https://github.com/RaviChandra96/Devops-practice2.git'

                }
            }
            stage ('CI Build') {

                steps {

                    sh 'mvn clean package'
                   
                     }
    
            }

            stage ('Docker Build && Push && DEPLOY ') {
               

                steps {
                    withCredentials([string(credentialsId: 'ravianil203', variable: 'dckr_pat_qXAqmTec58r2zGHOIMksgma0fm0')]) {


                    sh 'docker build . -t ravianil203/app30:test'
                    sh 'docker login -u ravianil203 -p ${dckr_pat_qXAqmTec58r2zGHOIMksgma0fm0}'
                    sh 'docker push ravianil203/app30:test'
                   // sh 'docker run -p 8111:8080 -d ravianil203/app30:test'
                }

                }
            
        }

            stage('Archive and clean workspace') {
                steps {
                    
                    archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
                    cleanWs()
                }

            }
        }  
}

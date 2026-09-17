pipeline
{
    agent any

    stages{
    stage('git checkout'){

            steps{

                git branch: 'mastercheff', url:'https://github.com/venugopal-cloud/onlinebookstore.git'
            }
        }

    stage('clean and install'){
   
            steps{

                sh  'mvn clean install'
            }
        }

        stage('package'){

            steps{

                sh  'mvn package'
            }
        }

        stage('Archive the Artifact'){

            steps{

                sh  'mvn clean install'
            }
            post{
                success {

                    archiveArtifacts artifact: 'target/*.war'
                }
            }
        }

        stage('Test Cases'){

            steps{

                sh  'mvn test'
            }
        }

        stage('Test Results Reports'){

            steps{

                sh  'target/surface-reports/*xml'
            }
        }

        stage('Deploy to tomcat server'){

            steps{

                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'ba2c85cb-2c4c-4b2d-8392-3fff9ac06adb', path: '', url: 'http://localhost:8080/')], contextPath: 'Venu Services', war: '**/*.war'
            }
        }
    }

}
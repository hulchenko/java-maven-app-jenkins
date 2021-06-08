pipeline {
    agent any
    tools {
        maven 'maven-3.8'
    }
    stages {
        stage('build jar'){
            steps {
                script {
                    echo "building the application.."
                    sh "mvn package"
                }
            }
        }
                stage('build image'){
            steps {
                script {
                    echo "building docker image.."
                    withCredentials([usernamePassword(credentialsId: 'github-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]){
                        sh 'docker build -t hulchenko/demo-app:jma-2.0 .'
                        sh "echo $PASSWORD | docker login -u $USER --password-stdin"
                        sh 'docker push hulchenko/demo-app:jma-2.0'
                    }
                }
            }
        } 
        stage("deploy"){
            steps {
                script {
                    echo "deploying the application.."
                }
            }
        }
    }
}
#!/usr/bin/env groovy
def gv

pipeline {
    agent any
    parameters {
        choice(name:'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }
    stages {
        stage('init') {
    steps {
        script {
            gv = load "script.groovy"
        }
    }
}
        stage('build') {
            steps {
                script {
                    script {
                        gv.buildApp()
                    }
                }
            }
        }
        stage('test') {
            when {
                expression {
                    params.executeTests
                }
            }
            steps {
                script {
                    gv.testApp()
                }
            }
        }
        stage('deploy') {
            input {
                message "Select the deployment environment"
                ok "Done!"
                parameters {
                    choice(name:'ENV-ONE', choices: ['dev', 'staging', 'prod'], description: 'environment choices')
                    choice(name:'ENV-TWO', choices: ['dev', 'staging', 'prod'], description: 'environment choices')
                }
            }
            steps {
                script {
                    gv.deployApp()
                    echo "Deploying to ${ENV-ONE}"
                    echo "Deploying to ${ENV-TWO}"
                }
            }
        }
    }
}

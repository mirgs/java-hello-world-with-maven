#!/usr/bin/env groovy
pipeline {
    agent any
    stages {
        stage('Setup') {
            steps {
                git url:'https://github.com/mirgs/java-hello-world-with-maven.git', branch: 'master'
            }
        } 

        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv(credentialsId: 'aee1ab08-f0d6-4abe-9861-89e3c97916ce', installationName: 'local') {
                    sh 'mvn install'
                    sh 'sonar:sonar'
                }
            }
        }       
    }
}
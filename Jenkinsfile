#!/usr/bin/env groovy
pipeline {
    agent any
    stages {
        stage('Setup') {
            steps {
                git url:'https://github.com/mirgs/java-hello-world-with-maven.git', branch: 'master'
            }
        } 
		
		stage('Build') {
            steps {
				withMaven (maven: 'maven-3.6.3') {
					sh 'mvn clean install'
				}
            }
        } 

        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv(credentialsId: 'aee1ab08-f0d6-4abe-9861-89e3c97916ce', installationName: 'local') {
					withMaven (maven: 'maven-3.6.3') {
						sh 'mvn sonar:sonar \
						-Dsonar.sourceEncoding=UTF-8 \
						-Dsonar.login=admin \
						-Dsonar.password=sinensia1'
					}
                }
            }
        }       
    }
}
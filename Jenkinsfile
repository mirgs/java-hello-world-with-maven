#!/usr/bin/env groovy
pipeline {
    agent any
	/*tools {
        jdk 'OpenJDK-8.0'
    }*/
    stages {
        stage('Setup') {
            steps {
                git url:'https://github.com/mirgs/java-hello-world-with-maven.git', branch: 'master'
            }
        } 
		
		stage('Build') {
            steps {
                sh "mvn clean install -f pom.xml"
            }
        } 

        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv(credentialsId: 'aee1ab08-f0d6-4abe-9861-89e3c97916ce', installationName: 'local') {
                    sh "mvn sonar:sonar -f pom.xml \
		    		-Dsonar.sourceEncoding=UTF-8"
                }
            }
        }       
    }
}
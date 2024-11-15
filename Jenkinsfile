pipeline {
    
	agent any
    tools {
	    maven "maven3"
	    jdk "java17"
	}
	
    stages{
        
        stage ('fetch code') {
            steps {
                git branch: 'main', url: 'https://github.com/hkhcoder/vprofile-project.git'
            }
        }
        stage('build-app'){
            steps {
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('code analysis with sonarqube') {
          
		  environment {
             scannerHome = tool 'sonar-scanner-6'
          }
          steps {
            withSonarQubeEnv('sonar-server') {
               sh '''${scannerHome}/bin/sonar-scanner \
                   -Dsonar.projectKey=java-app \
                   -Dsonar.projectName=javaapp-repo \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.organization=myreg-app'''
            }
          }
        }
    }
}

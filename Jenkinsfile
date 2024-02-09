pipeline {
    agent { label 'jenkins_Agent' }
    tools {
        jdk 'java17'
        maven 'Maven3'
    }
    stages {
        stage('Clean Up WorkSpace') {
            steps {
                cleanWs()
            }
        }

        stage('Clone the GitHub') {
            steps {
                git branch: 'main', credentialsId: 'Github_ID', url: 'https://github.com/sivaPrasad96/sample_devops_project.git'
            }
        }

        stage('Build the App') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test the App') {
            steps {
                sh 'mvn test'
            }
        }

        stage('SonarQube Analysis chk') {
            steps {
                withSonarQubeEnv(credentialsId: 'jenkins_sonar_token') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }
}

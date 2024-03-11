pipeline {
    agent any

    triggers {
        cron('H/10 * * * 1')
    }

    tools {
        maven 'maven'
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Test with JaCoCo') {
            steps {
                bat 'mvn test jacoco:report'
            }

            post {
                always {
                    jacoco(execPattern: 'target/jacoco.exec')
                }
            }
        }
    }

    post {
        success {
            echo 'Build was successful!'
        }

        failure {
            echo 'Build failed.'
        }
    }
}
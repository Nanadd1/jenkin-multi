pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    extensions: [
                        [$class: 'LocalBranch', localBranch: 'main']
                    ],
                    userRemoteConfigs: [[url: 'https://github.com/Nanadd1/jenkin-multi.git']]
                ])
                
                // Debugging: Show what was checked out
                sh 'git branch -a'
                sh 'ls -la src/main/java/com/example/'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
    }
}
            

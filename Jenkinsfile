 pipeline {
    agent any
    
    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()  // Clean workspace before checkout
            }
        }
        
        stage('Force Checkout main') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: 'refs/heads/main']],  // Absolute reference
                    extensions: [
                        [$class: 'LocalBranch', localBranch: 'main'],
                        [$class: 'CleanBeforeCheckout']
                    ],
                    userRemoteConfigs: [[
                        url: 'https://github.com/Nanadd1/jenkin-multi.git',
                        refspec: '+refs/heads/main:refs/remotes/origin/main'  // Force main
                    ]]
                ])
                
                // Debugging - show what was checked out
                sh 'git branch -a'
                sh 'git log -1'
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

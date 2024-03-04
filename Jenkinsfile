pipeline {
    agent any
    
    stages {
        stage('Install Apache2') {
            steps {
                script {
                    // Install Apache2
                    sh 'echo 8 | sudo -S apt-get update
                    sh 'sudo apt-get install apache2 -y'
                }
            }
        }
        
        stage('Read Apache log file') {
            steps {
                script {
                    // Read Apache log file
                    sh 'tail -f /var/log/apache2/access.log > apache_log.txt &'
                }
            }
        }
        
        stage('Search for errors') {
            steps {
                script {
                    // Search for 4xx and 5xx errors in log file
                    sh 'grep -E " 4[0-9][0-9]| 5[0-9][0-9]" apache_log.txt > errors.txt'
                }
            }
        }
        
        stage('Display results') {
            steps {
                script {
                    // Display results in Jenkins console
                    sh 'cat errors.txt'
                }
            }
        }
    }
    
    post {
        always {
            // Clean up files
            deleteDir()
        }
    }
}

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Application build stage...'
            }
        }
        stage('Test') {
            steps {
                // Print the current working directory
                sh 'pwd'
                
                // List the contents of the Jenkins workspace
                sh 'ls -la ${WORKSPACE}'

                // Remove existing files on the remote server first
                sh '''
                    gcloud compute ssh root@saba-apache --zone=us-west4-a -- "rm -rf /var/www/html/*"
                '''

                // Then copy new files from Jenkins workspace to the remote server
                sh '''
                    gcloud compute scp --recurse ${WORKSPACE}/* root@saba-apache:/var/www/html --zone=us-central1-a
                '''
            }
        }
        stage('Run') {
            steps {
                echo 'Application run stage'
            }
        }
    }
}

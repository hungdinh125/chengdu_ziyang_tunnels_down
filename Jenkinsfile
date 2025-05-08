pipeline {
    agent any
    stages {
        stage('Enable virtual environment pyats') {
            steps {
                echo 'Setup PYATS environment'
                sh 'python3 -m venv pyats'
                sh 'source pyats/bin/activate'
            }
        }
        stage('List files cloned from Git') {
            steps {
                echo 'Confirm required files are cloned'
                sh 'ls -la'                
            }
        }
        stage('Run the Python script for Chengdu and Ziyang') {
            steps {
                echo 'Activate Python script to check tunnels down'
                sh 'python3 chengdu_ziyang_tunnels.py'                
            }
        }
    }
    post {
        always {
            cleanWs(cleanWhenNotBuilt: true,
                    deleteDirs: true,
                    disableDeferredWipeout: true,
                    notFailBuild: true)
        }
    }
}
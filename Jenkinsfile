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
        stage('Copy baseline file into workspace') {
            steps {
                sh 'cp /var/lib/jenkins/baseline_tunnels.txt ./baseline_tunnels.txt'
            }
        }
        stage('Run the Python script for Chengdu and Ziyang') {
            steps {
                echo 'Activate Python script to check tunnels down'
                sh 'python3 chengdu_ziyang_tunnels.py'                
            }
        }
        stage('Copy updated baseline back to home') {
            steps {
                sh 'cp baseline_tunnels.txt /var/lib/jenkins/baseline_tunnels.txt'
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

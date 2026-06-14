pipeline {
    agent any

    stages {

        stage('Setup') {
            steps {
                sh '''
                venv/bin/python --version
                venv/bin/pip list
                '''
            }
        }

        stage('Flake8') {
            steps {
                sh 'venv/bin/flake8 tests/'
            }
        }

        stage('Pytest') {
            steps {
                sh 'venv/bin/pytest tests/'
            }
        }

        stage('Package App') {
            steps {
                sh '''
                rm -f my_splunk_app-1.0.0.tar.gz
                venv/bin/slim package my_splunk_app/
                '''
            }
        }

        stage('AppInspect') {
            steps {
                sh 'venv/bin/splunk-appinspect inspect my_splunk_app-1.0.0.tar.gz'
            }
        }

    }
}

pipeline {
    agent any

    stages {
        stage('Dependencies'){
            steps {
                sh 'pip install pylint'
            }
        }
        stage('Lint') {
            steps {
                sh 'pylint --disable=R,C simple-django-app/cool_counters/*.py'
            }
        }
        stage('Deploy') {
            steps {
                sh 'python manage.py migrate'
                sh 'python manage.py runserver 0.0.0.0:8000'
            }
        }
    }
}


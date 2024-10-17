pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                sh '''
                    if [ -d "simple-django-app" ]; then
                        rm -rf simple-django-app
                    fi
                    git clone https://github.com/DiegoPardoMontero/simple-django-app.git
                '''
            }
        }

        stage('Setup Python Environment') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install pylint django
                '''
            }
        }

        stage('Lint') {
            steps {
                sh '''
                    . venv/bin/activate
                    pylint simple-django-app/cool_counters/*.py
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    . venv/bin/activate
                    cd simple-django-app/cool_counters
                    python manage.py migrate
                    python manage.py runserver 0.0.0.0:8000
                '''
            }
        }
    }
}

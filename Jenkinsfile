pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                // Clonar el repositorio de GitHub
                sh 'git clone https://github.com/DiegoPardoMontero/simple-django-app.git'
            }
        }

        stage('Setup Python Environment') {
            steps {
                // Crear el entorno virtual en una carpeta específica
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
                // Ejecutar Pylint dentro del entorno virtual
                sh '''
                    . venv/bin/activate
                    pylint simple-django-app
                '''
            }
        }

        stage('Test') {
            steps {
                // Ejecutar las pruebas de Django dentro del entorno virtual
                sh '''
                    . venv/bin/activate
                    cd simple-django-app/cool_counters
                    python manage.py test
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

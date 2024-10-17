pipeline {
    agent any

    stages {
        stage('Setup Python Environment') {
            steps {
                // Crear el entorno virtual en una carpeta específica
                sh '''
                    python3 -m venv venv
                    source venv/bin/activate
                    pip install --upgrade pip
                    pip install pylint django
                '''
            }
        }

        stage('Lint') {
            steps {
                // Activar el entorno virtual y ejecutar Pylint
                sh '''
                    source venv/bin/activate
                    pylint --disable=R,C simple-django-app/cool_counters/*.py
                '''
            }
        }

        stage('Deploy') {
            steps {
                // Activar el entorno virtual, aplicar migraciones y correr el servidor Django
                sh '''
                    source venv/bin/activate
                    python manage.py migrate
                    python manage.py runserver 0.0.0.0:8000
                '''
            }
        }
    }
}

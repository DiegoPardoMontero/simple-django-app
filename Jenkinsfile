pipeline {
    agent any

    stages {
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
                    pylint simple_django_app
                '''
            }
        }

        stage('Deploy') {
            steps {
                // Aplicar migraciones y levantar el servidor dentro del entorno virtual
                sh '''
                    . venv/bin/activate
                    python manage.py migrate
                    python manage.py runserver 0.0.0.0:8000
                '''
            }
        }
    }
}

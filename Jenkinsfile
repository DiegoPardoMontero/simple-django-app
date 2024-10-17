pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                // Borrar el directorio del repositorio si ya existe y luego clonar
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
                // Ejecutar Pylint dentro del entorno virtual y no fallar ante advertencias
                sh '''
                    . venv/bin/activate
                    pylint --exit-zero simple-django-app/cool_counters/manage.py
                '''
            }
        }        

        stage('Deploy') {
            steps {
                // Aplicar migraciones y levantar el servidor dentro del entorno virtual
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

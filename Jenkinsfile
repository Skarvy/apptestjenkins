pipeline {
    agent any

    stages {
        stage('Clonar Código') {
            steps {
                git branch: 'main', url: 'https://github.com/Skarvy/apptestjenkins.git'
            }
        }

        stage('Instalar Dependencias') {
            steps {
                sh 'npm install'
            }
        }

        stage('Ejecutar Pruebas') {
            steps {
                sh 'npm test'
            }
        }

        stage('Construir Imagen Docker') {
            steps {
                sh '''
                docker build -t basic-app:latest .
                '''
            }
        }

        stage('Desplegar') {
            steps {
                sh '''
                docker run -d -p 3000:3000 --name basic-app basic-app:latest
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline completada'
        }
        failure {
            echo 'La pipeline falló'
        }
    }
}

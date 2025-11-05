pipeline {
    agent any

    stages {
        stage('Clonar código desde GitHub') {
            steps {
                git branch: 'main', url: 'https://github.com/Ftorres91/hola_mundo.git'
            }
        }

        stage('Construir imagen Docker') {
            steps {
                script {
                    dockerImage = docker.build('miapp-php:latest')
                }
            }
        }

        stage('Ejecutar contenedor') {
            steps {
                script {
                    // Detener contenedor previo si existe
                    sh 'docker stop miapp-php || true'
                    sh 'docker rm miapp-php || true'
                    
                    // Iniciar contenedor nuevo
                    sh 'docker run -d -p 8081:80 --name miapp-php miapp-php:latest'
                }
            }
        }
    }

    post {
        success {
            echo '✅ Aplicación PHP desplegada correctamente.'
            echo '🌐 Accede en: http://localhost:8081'
        }
        failure {
            echo '❌ Error en la ejecución del pipeline.'
        }
    }
}

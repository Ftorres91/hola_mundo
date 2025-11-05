pipeline {
    agent any

    stages {
        stage('Clonar código desde GitHub') {
            steps {
                git 'https://github.com/Ftorres91/hola_mundo.git'
            }
        }

        stage('Construir imagen Docker') {
            steps {
                script {
                    dockerImage = docker.build("hola-mundo-php")
                }
            }
        }

        stage('Reiniciar contenedor') {
            steps {
                script {
                    // Detener contenedor previo (si existe)
                    sh 'docker rm -f hola_mundo || true'
                    // Ejecutar nuevo contenedor
                    dockerImage.run("-d -p 8081:80 --name hola_mundo")
                }
            }
        }
    }

    post {
        success {
            echo "✅ Desplegado correctamente en http://localhost:8081"
        }
        failure {
            echo "❌ Error en la ejecución del pipeline."
        }
    }
}


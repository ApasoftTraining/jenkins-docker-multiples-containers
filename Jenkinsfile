pipeline {
    agent none

    stages {
            

        stage('Build') {
            agent {
                docker {
                    image 'maven:3.8.6-openjdk-17'  // Usamos una imagen Maven con JDK 17
                    args '-v /root/.m2:/root/.m2'  // Compartir el repositorio local de Maven
                }
            }
            steps {
               
                        // Compilar el proyecto Maven
                        sh 'mvn clean compile'
                   
            }            
        }

        stage('Test') {
            agent {
                docker {
                    image 'maven:3.8.6-openjdk-17'  // Usamos la misma imagen Maven para las pruebas
                    
                    args '-v /root/.m2:/root/.m2'  // Compartir el repositorio local de Maven
                }
            }
            steps {
                
                        // Ejecutar pruebas unitarias
                        sh 'mvn test'
                    }
            
        }

        stage('Package') {
            agent {
                docker {
                    image 'maven:3.8.6-openjdk-17'  // Usamos la misma imagen Maven para empaquetar
                    args '-v /root/.m2:/root/.m2'  // Compartir el repositorio local de Maven
                }
            }
            steps {
                  
                        sh 'mvn package'
                    }
            
            
        }

        stage('Deploy') {
            agent {
                docker {
                    image 'maven:3.8.6-openjdk-17'  // Usamos la misma imagen Maven para desplegar
                    args '-v /root/.m2:/root/.m2'  // Compartir el repositorio local de Maven
                }
            }
            steps {
                
                        // Desplegar el JAR (opcional, dependiendo del entorno de despliegue)
                        // Puedes cambiar esta línea para desplegar a un servidor, Nexus, etc.
                        sh 'mvn deploy'
                    }
                
            
        }
    }

    post {
        always {
            echo 'Pipeline completado.'
        }
        success {
            echo 'Pipeline ejecutado con éxito.'
        }
        failure {
            echo 'Pipeline falló.'
        }
    }
}

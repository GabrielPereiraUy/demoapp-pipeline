pipeline {
  agent any
  stages {
    stage('Construir') {
      steps {
        echo 'Construyendo Pipe'
        sh 'sh run_build.script.sh'
      }
    }

    stage('Prueba en Linux') {
      parallel {
        stage('Prueba en Linux') {
          steps {
            echo 'Ejecutando la Prueba en Linux'
            sh 'sh run_linux_test.sh'
          }
        }

        stage('Prueba en Windows') {
          steps {
            echo 'Ejecutando Prueba en Windows'
          }
        }

      }
    }

    stage('Etapa de Despliegue') {
      steps {
        echo 'Ingreso de Mensaje Manual'
        input 'Tenemos tu Ok para el despiegue?'
        timestamps()
      }
    }

    stage('Despliegue en Producción') {
      steps {
        echo 'Se despliega en Producción'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'gabriel.pereira@utec.edu.uy', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}
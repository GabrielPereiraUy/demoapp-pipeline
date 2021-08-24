pipeline {
  agent any
  stages {
    stage('Construyento la App') {
      steps {
        echo 'Paso 1 construyendo la App'
        sh 'sh run_build_script.sh'
      }
    }

    stage('Prueba de Linux') {
      steps {
        echo 'Realizando la Prueba en Linux'
        sh 'sh run_linux_tests.sh'
      }
    }

    stage('Confirmacion Manual') {
      steps {
        echo 'Esperando por la confirmacion manual'
        input 'Esta todo Ok para desplegar?'
        timestamps() {
          echo 'Momento de confirmacion del ok Manual'
        }

      }
    }

    stage('Desplegando en Produccion') {
      steps {
        echo 'Desplegando en Produccion'
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
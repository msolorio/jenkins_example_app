pipeline {
    agent { docker { image 'node:16.13.1-alpine' } }

    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                  echo "Multiline shell steps work too"
                  ls -lah
                '''
                sh 'node --version'
            }
        }

        stage('Test') {
          steps {
            echo 'Testing'
          }
        }

        stage('Deploy - Staging') {
          steps {
            echo 'Deploying staging'
          }
        }

        stage('Sanity check') {
          steps {
            input "Does the staging environment look ok?"
          }
        }

        stage('Deploy - Production') {
          steps {
            echo 'Deploying prod'
          }
        }

        post {
            always {
              echo 'This will always run'
              deleteDir()
            }
            success {
              echo 'Pipeline was successful'
              mail to: 'msolorio1@gmail.com',
                subject: 'Successful Pipeline',
                body: 'hello from Jenkins'
            }
            failure {
              echo 'Pipeline failed'
              mail to: 'msolorio1@gmail.com',
                subject: "Failed Pipeline",
                body: "hello from Jenkins"
            }
            unstabled {
              echo 'run was marked as unstable'
            }
            changed {
              echo 'State of the pipeline has changed'
            }
        }
    }
}

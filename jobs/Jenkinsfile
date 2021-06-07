pipeline {
    agent {
        label 'master' 
    }
    environment {
        appName = "variable" 
    }
    stages {
        stage ('install') {
            steps {
                sh "npm install"
            }
        }

        stage ('run') {
            steps {
                sh "node index.js"
            }
        }

        stage ('test') {
            steps {
                sh "npm test"
            }
        }      
    }
    //El apartado post se ejecuta siempre al terminar los stages
    post {
        //Always se ejecuta siempre que terminan los stages, sin importar el estado 
        always {          
            deleteDir()
            sh "echo 'fase always'"
        }
        //Sucess se ejecuta si se ejecuto todo con exito
        success {
            sh "echo 'fase success'"
        }
        //Failure se ejecuta si hubo alguna falla
        failure {
            sh "echo 'fase failure'"
        }   
    }
}  
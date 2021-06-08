import groovy.json.JsonSlurperClassic

def jsonParse(def json) {
    new groovy.json.JsonSlurperClassic().parseText(json)
}

pipeline {
    agent {
        label 'master' 
    }
    environment {
        appName = "variable" 
    }
    stages {
        stage ('Instalacion de dependencias') {
            steps {
                sh "npm install"
            }
        }

        stage ('Run') {
            steps {
                sh "node index.js"
            }
        }

        stage ('Realizacion de Test') {
            steps {
                sh "npm test"
            }
        }      
    }
    //El apartado post se ejecuta siempre al terminar los stages
    post {
        //Always se ejecuta siempre que terminan los stages, sin importar el estado 
        always {          
            sh "echo 'fase always'"
        }
        //Sucess se ejecuta si se ejecuto todo con exito
        success {
            sh "cp index.html /var/www/html"
            sh "cp index.css /var/www/html"
            sh "cp index.js /var/www/html"
            sh "echo 'Despliegue correcto' "
        }
        //Failure se ejecuta si hubo alguna falla
        failure {
            sh "echo 'Despliegue detenido, se sigue en la version anterior'"
        }   
    }
}  

pipeline {
    agent any
    parameters {
        choice(name: 'ENVIRONMENT', choices: ['INT', 'QA', 'PROD', ], description: 'Run test on (INT or QA or PROD)')
    }
    stages {
        stage('Ejecutar Tareas de Respaldo') {
            steps {
                echo "Voy a respaldar un directorio"
                // Falta agregar la fecha actual al respaldo ${BUILD_TIMESTAMP}
                fileOperations([fileZipOperation(folderPath: 'C:\\test1', outputFolderPath: 'C:\\respaldo')])
                echo "Respaldado el directorio"
            }
        }
        stage('Descargar repositorio de GitHub') {
            steps {
                echo "Voy a descargar el repositorio desde GitHub"
                checkout([$class: 'GitSCM',
                        branches: [[name: 'main']],
                        userRemoteConfigs: [[url: 'https://github.com/roselynpinango/JenkinsProject.git']]])
                echo "Descargado el repositorio desde GitHub"
            }
        }
        stage('Copiar archivos de un lugar a otro') { // for display purposes
            steps {
                echo "Voy a copiar los archivos de un directorio a otro"
                fileOperations([folderCopyOperation(destinationFolderPath: 'C:\\test2', sourceFolderPath: 'C:\\test1')])
                echo "Copiados los archivos de un directorio a otro"
            }
        }
        stage('Ejecucion de script SQL') {
            steps {
                echo "Voy a ejecutar un script SQL"
                bat "'C:\\Program Files\\MySQL\\MySQL Server 8.0\\bin\\mysql.exe' -h localhost -P 3306 -u root -prose -D inventariodb < C:\\test2\\01_inventariodb_countproducts.sql"
                echo "Ejecutado el script SQL"
            }
        }
        stage('Envio de Notificacion por correo') {
            steps {
                echo "Todo salio genial!"
                echo "Comenzando a enviar el correo"
                //mail bcc: '', body: '$DEFAULT_CONTENT', cc: '', from: 'roselyn.pinango@gmail.com', replyTo: 'roselyn.pinango@gmail.com', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'roselyn.pinango@gmail.com'
                //emailext body: '$DEFAULT_CONTENT', recipientProviders: [requestor()], subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'roselyn.pinango@gmail.com'
                echo "Luego de enviar el correo"  
            }
        }
    }
}

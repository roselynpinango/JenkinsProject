pipeline {
    agent any
    parameters {
        choice(name: 'ENVIRONMENT', choices: ['INT', 'QA', 'PROD', ], description: 'Run test on (int or qa or prod)')
    }
    stages {
        stage('Respaldar directorio') {
            steps {
                echo "Voy a respaldar un directorio"
                fileOperations([fileZipOperation(folderPath: 'C:\\test1', outputFolderPath: 'C:\\respaldo')])
                echo "Respaldado el directorio"
            }
        }
        stage('Copiar archivos de un lugar a otro') { // for display purposes
            steps {
                echo "Voy a copiar los archivos de un directorio a otro"
                fileOperations([folderCopyOperation(destinationFolderPath: 'C:\\test2', sourceFolderPath: 'C:\\test1')])
               
                echo "Copié los archivos de un directorio a otro"
            }
        }
        stage('Ejecución de script SQL') {
            steps {
                echo "Voy a ejecutar un script SQL"
                // Pendiente 
                echo "Ejecutado el script SQL"
            }
        }
        stage('Resultado') {
            steps {
                echo "Todo salió genial!"
                echo "Comenzando a enviar el correo"
                mail bcc: '', body: '$DEFAULT_CONTENT', cc: '', from: 'roselyn.pinango@gmail.com', replyTo: 'roselyn.pinango@gmail.com', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'roselyn.pinango@gmail.com'
                //emailext body: '$DEFAULT_CONTENT', recipientProviders: [requestor()], subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'roselyn.pinango@gmail.com'
                echo "Luego de enviar el correo"  
            }
        }
    }
}

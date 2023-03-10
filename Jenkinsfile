pipeline  {
    agent any

    environment {
        TARGETHOST = '172.16.49.225'
        APP_USER = 'wwwroot'
        APP_DEPLOY_DIR = '/app/pay/ver/front-msa/'
        // TARGETHOST = '172.16.49.106'
        // APP_USER = 'wwwroot'
        // APP_DEPLOY_DIR = '/app/pay/ver/front-msa/'
    }

    stages {
        stage('Install') {
            steps {
                nodejs(nodeJSInstallationName: 'NodeJS 14.16.1') {
                    sh '''node -v
                    npm -v
                    npm i'''
                }
            }
        }
    }
}
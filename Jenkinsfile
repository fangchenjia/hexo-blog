pipeline  {
    agent any
    stages {
        stage('Pull') {
            steps {
                git credentialsId: 'gitee-183', url: 'https://gitee.com/fangchenjia/hexo-blog.git'
                sh '''
                rm themes/anzhiyu -rf
                git clone -b main https://gitee.com/fangchenjia/hexo-theme-anzhiyu-mine.git themes/anzhiyu
                '''
            }
        }
        stage('Install') {
            steps {
                nodejs(nodeJSInstallationName: 'v14.13.0') {

                    sh '''node -v
                    npm -v
                    npm i'''
                }
            }
        }
        stage('Bulid') {
            steps {
                nodejs(nodeJSInstallationName: 'v14.13.0') {
                    sh '''npm run clean
                    npm run build
                    tar -zcvf public.tar.gz public'''
                }
            }
        }
        stage('Deploy') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'myServer', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /opt/MyDocker/dockerData/nginx/html/
                rm -rf hexo
                mkdir hexo
                tar -zxvf public.tar.gz -C hexo/
                rm -rf public.tar.gz''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: 'opt/MyDocker/dockerData/nginx/html/', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'public.tar.gz')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}
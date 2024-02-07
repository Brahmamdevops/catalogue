pipeline{
     agent {
        node {
            label 'AGENT-1'
            
        }
    }
    
     environment { 
        packageVersion = ""
        nexusUrl ="172.31.5.38:8081"
    }

    options {
        ansiColor('xterm')
        // timeout(time: 1, unit: 'HOURS')
        // disableConcurrentBuilds()
    }
    
    stages {
        stage('get the version') {
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                        packageVersion  = packageJson.version
                        echo " apllication $packageVersion " 
                }
        
            }
        }

        stage('Install Dependencies') {
            steps {
                sh """
                    npm install 
                """
            }
        }
        stage('build') {
            steps {
                sh """  
                ls -la
                zip -q -r catalogue.zip ./* -x ".git" -x "*.zip"
                ls -ltr 
                """
            }
        }

        stage('uplaoding artifact') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: "${nexusUrl}",
                    groupId: 'com.roboshop',
                    version: "${packageVersion}",
                    repository: 'catalogue',
                    credentialsId: 'nexus-auth',
                        artifacts: [
                            [artifactId: 'catalogue',
                            classifier: '',
                            file: 'catalogue.zip',
                            type: 'zip']
                ]
     )
            }
        }
        
    }

     // post build
    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
        failure { 
            echo 'this runs when pipeline is failed, used generally to send some alerts'
        }
        success{
            echo 'I will say Hello when pipeline is success'
        }
    }
}
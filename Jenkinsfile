pipeline{
     agent {
        node {
            label 'AGENT-1'
            
        }
    }
    
     environment { 
        packageVersion = ""
    }

    options {
        ansiColor('xterm')
        // timeout(time: 1, unit: 'HOURS')
        // disableConcurrentBuilds()
    }
    
    stages{
        stage('Init') {
            steps {
                script{
                    def packageJson = readJSON file: 'package.json'
                        packageJson.version = packageVersion  
                    echo " apllication $packageVersion " 
                }
            }
        }
    }
}
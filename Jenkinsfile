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
    }
}
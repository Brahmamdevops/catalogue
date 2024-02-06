pipeline{
     agent {
        node {
            label 'AGENT-1'
            
        }
    }
    
     environment { 
        packageVersion=""
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
                    def v=package.json
                    v.version = packageVersion   
                }
            }
        }
    }
}
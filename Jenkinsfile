pipeline {
    agent {
        docker {
            image 'openjdk'
        }
    }
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            steps {
                sh 'javac Hello.java && java Hello'
                
            }
        }
        stage('Results') {
            steps {
                
                def logz = currentBuild.rawBuild.getLog(10000);
                
                def result = logz.find { it.contains('Ola Words') }
                
                if (result) {
                        error ('Falha resultado diferente do esperado ( Ola Mundo ) ' + result)
                            
                }
            
            }
        }
       
    }
}

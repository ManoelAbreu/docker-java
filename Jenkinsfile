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
                javac Hello.java
            }
        }
       
    }
}

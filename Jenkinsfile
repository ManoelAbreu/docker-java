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
                script {

                    def logz = currentBuild.rawBuild.getLog(10000);

                    def result = logz.find { it.contains('mundasdsado') };

                    if (!result) {
                            error ('Falha resultado diferente do esperado ( Ola Mundo ) ' + result);

                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Jenkins - Email enviado apos o build'

            emailext body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
                subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"

        }
    }
}

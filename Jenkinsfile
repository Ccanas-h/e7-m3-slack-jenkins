pipeline {
    agent any
        stages {
            stage('Initialize') {
                steps {
                    script {
                        echo 'Inicializando pipeline'
                        slackSend(message: "Inicializando pipeline ${env.JOB_NAME} ", color: 'good')
                    }
                }
            }
            stage('Build') {
                steps {
                    script {
                        sh 'mvn -B package'
                        if (currentBuild.result == 'FAILURE') {
                        slackSend(message: "Error en la compilacion  ${env.JOB_NAME} ", color: '#CD5C5C')
                        }else {
                        slackSend(message: "Compilado exitoso ${env.JOB_NAME} ", color: '#3633FF')
                        }
                    }
                }
            }

            stage('Test') {
                steps {
                    script {
                        sh 'mvn clean verify'
                        if (currentBuild.result == 'FAILURE') {
                        slackSend(message: "Tests fallidos ${env.JOB_NAME} ", color: '#CD5C5C')
                        }else {
                        slackSend(message: "Test hecho correctamente ${env.JOB_NAME} ", color: '#3633FF')
                        }
                    }
                }
            }
        }

    post {
        always {
            script {
                echo 'Prueba'

                if (currentBuild.result == 'SUCCESS') {
                    slackSend(channel: '@U05690FEL7P', message: "SUCCES Post - Proyecto Creado  *${currentBuild.currentResult}:* build ${env.BUILD_NUMBER}, ${env.JOB_NAME}", color: '#00FF04')
                }else if (currentBuild.result == 'FAILURE') {
                    slackSend(channel: '@U05690FEL7P', message: "FAILURE Post - Proyecto fallido *${currentBuild.currentResult}:* build ${env.BUILD_NUMBER}, ${env.JOB_NAME}", color: '#FF0000')
                }
            }
        }
    }
}

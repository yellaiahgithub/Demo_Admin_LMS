pipeline {
    agent any

    stages {
        stage('cloning the code') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/dev']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/yellaiahgithub/Demo_Admin_LMS.git']]])
            }
        }
        stage('slack notification') {
            steps {
                slackSend channel: 'yellaiah', message: 'slackSend "started ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"', teamDomain: 'myprojectspace', tokenCredentialId: 'lll'
            }
        }
        stage('Approval From Project Manager') {
            steps {
                script {
                    timeout(10) {
                        mail bcc: '', body: "Please click on the below link to review and approve deployment http://http://13.233.99.60:8080/job/kona_lms_frontend/configure/${env.BUILD_NUMBER}/console ", cc: '', from: '', replyTo: '', subject: 'Need approval to deploy', to: 'mubeen507@gmail.com'
                        input id: 'Deploygate', message: "Deploy ${env.JOB_NAME}?", ok: 'deploy'
                        }
                }
            }
        }
        stage('docker build') {
            steps {
                sh 'docker build -t lll .'
            }
        }
    }
}

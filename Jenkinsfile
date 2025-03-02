// pipeline {
//     agent {
//         docker {
//             image 'node:16-buster-slim'
//             args '-p 3000:3000'
//         }
//     }
//     stages {
//         stage('Build') {
//             steps {
//                 sh 'npm install'
//             }
//         }
//         stage('Test') {
//             steps {
//                 sh './jenkins/scripts/test.sh'
//             }
//         }
//         stage('Manual Approval') {
//             steps {
//                 script {
//                     input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
//                 }
//             }
//         }
//         stage('Deploy') { 
//             steps {
//                 sh './jenkins/scripts/deliver.sh'
//                 sh 'sleep 60'
//                 echo 'Pipeline has finished successfully.'
//                 sh './jenkins/scripts/kill.sh'
//             }
//         }
    
//     }
// }

node {
    def dockerImage = 'node:16-buster-slim'
    def dockerArgs = '-p 3000:3000 -u root'

    docker.image(dockerImage).inside(dockerArgs) {
        stage('Build') {
            sh 'npm install'
        }

        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }

        stage('Manual Approval') {
            script {
                input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
            }
        }

        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
                // sh '''
                // apt update && apt install -y openssh-client
                // ssh -V  # Verifikasi instalasi SSH client
                // '''
                sh 'pwd && ls -la'
                    withCredentials([sshUserPrivateKey(credentialsId: 'ssh-key-ec2', keyFileVariable: 'SSH_KEY')]) {
                        sh '''
                        scp -r -o StrictHostKeyChecking=no -i ${SSH_KEY} /build ubuntu@13.229.209.37:/home/ubuntu
                        '''
                        }
            // sh 'sleep 60'
            echo 'Pipeline has finished successfully.'
            sh './jenkins/scripts/kill.sh'
        }
    }
}
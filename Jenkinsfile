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
    def dockerArgs = '-p 3000:3000'
    
    stage('Build') {
        docker.image(dockerImage).inside(dockerArgs) {
            sh 'npm install'
        }
    }
    
    stage('Test') {
        docker.image(dockerImage).inside(dockerArgs) {
            sh './jenkins/scripts/test.sh'
        }
    }
    
    stage('Manual Approval') {
        script {
            input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
        }
    }    
    stage('Deploy') {
        sh './jenkins/scripts/deliver.sh'
        sh 'sleep 10'
        sh './jenkins/scripts/kill.sh'
        echo 'Pipeline has finished successfully.'
    }
}

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
    stage('Build') {
        steps {
            sh 'npm install'
        }
    }
    stage('Test') {
        steps {
            sh './jenkins/scripts/test.sh'
        }
    }
    stage('Manual Approval') {
        steps {
            script {
                input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
            }
        }
    }
    stage('Deploy') { 
        steps {
            sh './jenkins/scripts/deliver.sh'
            sh 'sleep 60'
            echo 'Pipeline has finished successfully.'
            sh './jenkins/scripts/kill.sh'
        }
    }
}

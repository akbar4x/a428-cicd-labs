pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
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
        stage('Deploy') { 
            // steps {
            //     sh './jenkins/scripts/deliver.sh' 
            //     input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)' 
            //     sh './jenkins/scripts/kill.sh' 
            // }
            steps {
                sh './jenkins/scripts/deliver.sh'
                echo 'Menunggu selama 1 menit agar aplikasi dapat diuji...'
                sh 'sleep 60'  // Jeda selama 1 menit sebelum aplikasi dihentikan
                sh './jenkins/scripts/kill.sh'  // Mengakhiri aplikasi setelah 1 menit
            }
        }
    }
}
// node {
//     def dockerImage = 'node:16-buster-slim'
//     def dockerArgs = '-p 3000:3000'
//     docker.image(dockerImage).inside(dockerArgs) {
//         stage('Build') {
//             sh 'npm install'
//         }
//         stage('Test') {
//             sh './jenkins/scripts/test.sh'
//         }
//     }
// }
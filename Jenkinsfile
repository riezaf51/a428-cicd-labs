node {
    stage('Build') {
        def nodeContainer = docker.image('node:16-buster-slim')
        nodeContainer.inside('-p 3000:3000 --user root') {
            sh 'npm install'
        }
    }

    stage('Test') {
        def nodeContainer = docker.image('node:16-buster-slim')
        nodeContainer.inside('-p 3000:3000 --user root') {
            sh './jenkins/scripts/test.sh'
        }
    }

    stage('Deploy') {
        def nodeContainer = docker.image('node:16-buster-slim')
        nodeContainer.inside('-p 3000:3000 --user root') {
            sh './jenkins/scripts/deliver.sh'
            input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
            sh './jenkins/scripts/kill.sh'
        }
    }
}

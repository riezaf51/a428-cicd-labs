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

    stage('Manual Approval') {
        input message: 'Lanjutkan ke tahap Deploy?'
    }

    stage('Deploy') {
        def nodeContainer = docker.image('node:16-buster-slim')
        nodeContainer.inside('-p 3000:3000 --user root') {
            sh './jenkins/scripts/deliver.sh'
            
            // Pause for a minute
            sleep 60
            
            sh './jenkins/scripts/kill.sh'
        }
    }
}

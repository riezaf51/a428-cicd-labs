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
}

node ('master') {
    def app
    stage('cloning git') {
        checkout scm
    }
    stage('Build-and-Tag') {
        sh 'echo build and tag'
        app = docker.build("venmaum/expblock")
    }
    stage('Post-to-dockerhub') {
        docker.withRegistry('https://registry.hub.docker.com','Docker_credentials'){
            app.push("latest")
        }
    }
   environment {
        PATH = "$PATH:/usr/bin"
    }
    stage('Pull-image-server') {
        sh "docker-compose down"
        sh "docker-compose up -d"
    }
}

node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }
    stage('Initialize'){

        def dockerHome = tool 'myDocker'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
    }
    stage('Build image') {
  
       app = docker.build("riddhigala18/python-app")
    }

    stage('Test image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', '1801') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}

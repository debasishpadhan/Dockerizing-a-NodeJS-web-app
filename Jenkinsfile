node {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("dpadhan/nodejsapp")
	
    }

    stage('Test image') {
        
        app.inside {
            echo "Tests passed"
        }
    }

    stage('Push image') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
            app.push("version${env.BUILD_NUMBER}")
            app.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
	stage('Email Notification') {
		mail bcc: '', body: 'test mail setup', cc: 'dpadhan10@gmail.com', from: '', replyTo: '', subject: 'Jenkins mail setup', to: 'papunaws@gmail.com'
	}
	stage('Skype Notification') {
		notifyEvents message: 'Hello <b>world</b>', token: '9kwgMyapizr8whRRqJPYS87AOZ7U5EUk'
	}
}

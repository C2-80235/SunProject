pipeline {
    agent any
    stages {
	stage ('SCM') {
	    steps {
		git branch: 'main', url: 'https://github.com/C2-80235/SunProject'
	    }
	}
	stage ('docker login') {
            steps {
                sh 'echo dckr_pat_OoxH6jNe33liBx8TknXWkNh5DaU | /usr/bin/docker login -u shnk --password-stdin'
            }
        }
        stage ('build docker image') {
            steps {
                sh '/usr/bin/docker image build -t shnk/sunproject .'
            }
        }
        
        stage ('push docker image') {
            steps {
                sh '/usr/bin/docker image push shnk/sunproject'
            }
        }
		stage ('create docker service') {
			steps {
				sh '/usr/bin/docker container run -d --name suncon -p 8080:80 shnk/sunproject'
			}
		}
        

    }
}

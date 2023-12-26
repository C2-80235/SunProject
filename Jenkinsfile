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
#		stage ('remove docker service') {
#			steps {
#				sh '/usr/bin/docker service rm myservice'
#			}
#		}
		stage ('create docker service') {
			steps {
				sh '/usr/bin/docker service create --replicas 5 --name myservice -p 8080:80 shnk/sunproject'
			}
		}
        stage ('reload docker service') {
            steps {
                sh '/usr/bin/docker service update --image shnk/sunproject --force myservice'
            }
        }

    }
}

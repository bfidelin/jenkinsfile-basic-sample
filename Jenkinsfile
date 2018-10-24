node {
 	// Clean workspace before doing anything
    deleteDir()

    try {
        stage ('Clone') {
        	checkout scm
        }
        stage ('Build') {
        	sh "echo 'shell scripts to build project...'"
        }
        stage ('Tests') {
	        parallel 'static': {
	            sh "echo 'shell scripts to run static tests...'"
	        },
	        'unit': {
	            sh "echo 'shell scripts to run unit tests...'"
	        },
	        'integration': {
	            sh "echo 'shell scripts to run integration tests...'"
	        }
        }
      	stage ('Deploy') {
            sh """echo 'shell scripts to deploy to server...'
	          export RD_URL=http://rundeck:4440
		  export RD_USER=admin                                    
		  export RD_PASSWORD=admin
		  export RD_COLOR=0
		  rd run  -j playbook_nginx.yml  -p CICD 
               """

      	}
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}





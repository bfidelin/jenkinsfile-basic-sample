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
            sh "echo 'shell scripts to deploy to server...'"
		 steps {
  script {
    step([$class: "RundeckNotifier",
          includeRundeckLogs: true,
          jobId: "a62ec870-8094-4baa-8dd8-cb6a824e4415"
          nodeFilters: "",
          options: """
                   PARAM_1=value1
                   PARAM_2=value2
                   PARAM_3=
                   """,
          rundeckInstance: "Default",
          shouldFailTheBuild: true,
          shouldWaitForRundeckJob: true,
          tags: "",
          tailLog: true])
  }
}

      	}
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}





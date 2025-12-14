pipeline{
	agent {label 'demo'}
        
	environment {
		REGISTRY = "http://sw.docker.org"
		IMAGE_NAME = "web-fe"
		IMAGE_TAG = "${BUILD_ID}"
		STACK_NAME = "test"
	}

	stages{

		stage ("Checkout"){
				steps {	
					checkout scm
				}
			}


		stage ("Build"){
			steps{
			   script{
				docker.build($IMAGE_NAME)
				}
			}
		}


		stage ("Push"){
			steps {
				script {
				    docker.withRegistry(env.REGISTRY) {
                        	    docker.image(env.IMAGE_NAME).push(env.BUILD_ID)
                		    }
				}

			}
		}
	}

}









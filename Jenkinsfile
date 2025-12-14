pipeline{
	agent {label 'demo'}
        
	environment {
		REGISTRY = "http://sw.docker.org"
		IMAGE_NAME = "web-fe"
		IMAGE_TAG = "${BUILD_ID}"
		STACK_NAME = "test_jenkins"
		IMAGE_FULL_NAME = "${REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG}"
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
				docker.build(env.IMAGE_NAME)
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



		stage ("Deploy"){
			agent {label "swarm-manager"}

			steps{
				sh """
					IMAGE=${IMAGE_FULL_NAME} docker stack deploy -c stack.yml ${STACK_NAME}
				"""
			}
		}
	}

}









def imageName = "web-fe"
def registry = 'http://sw.docker.org'
node('demo'){
	
	stage ('Checkout'){
		checkout scm
	}

	stage ('Build'){
		docker.build(imageName)
	}

	stage ('Push'){
		docker.withRegistry(registry, 'registry') {
			docker.image(imageName).push(env.BUILD_ID)
		}
	}


}

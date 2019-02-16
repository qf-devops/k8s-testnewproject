node('kube-label') {
    docker.withRegistry('https://hub.docker.com/') {
    	def mvnHome

    	stage('checkout'){

        mvnHome = tool 'M3'
        git url: 'https://github.com/quickfixtech/k8s-testnewproject.git'

        sh "git rev-parse HEAD > .git/commit-id"
        def commit_id = readFile('.git/commit-id').trim()
        println commit_id
        }

   
        stage('build'){
	        sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean install"
    	}

    	 

    	

    	stage('create deployment'){
    	    //sh 'kubectl delete deployments testnewprojectapi || true'
	    sh 'kubectl create -f deployment.yaml --validate=false'
    	}

    	stage('create service'){
	  //  sh 'kubectl delete services testnewprojectapiservice || true'
	    sh 'kubectl create -f services.yaml --validate=false'
    	}
   
    }
}

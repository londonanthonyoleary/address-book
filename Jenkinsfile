pipeline {

   agent {
      label "default"
   }

    environment {
        PROJECT_ID = 's-epo-itcoopk8spoc-prj'
        CLUSTER_NAME = 'epo-dev'
        LOCATION = 'europe-west3'
        CREDENTIALS_ID = 'epo-dev-terraform-anthonyoleary'
    }


	
	stage("Deploy to staging") {
        
	    steps{
//		 helm upgrade DEMO-address-book-develop-preemptible helm/address-book --install --wait --namespace=default --set instance=develop --set k8s.clusterName=epo-dev --set lifecycle=preemptible --set featureBranch=default --set jenkinsBranch=develop --timeout 10m

git url: 'https://github.com/londonanthonyoleary/address-book'
                step([$class: 'KubernetesEngineBuilder', 
                        projectId: "s-epo-itcoopk8spoc-prj",
                        clusterName: "epo-dev",
                        zone: "europe-west3",
                        manifestPattern: 'hem/address-book/',
                        credentialsId: "epo-dev-terraform-anthonyoleary",
                        verifyDeployments: true])

            }
	}
        
}

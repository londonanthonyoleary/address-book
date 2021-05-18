pipeline {

 agent any

    environment {
        PROJECT_ID = 's-epo-itcoopk8spoc-prj'
        CLUSTER_NAME = 'epo-dev'
        LOCATION = 'europe-west3'
        CREDENTIALS_ID = 'epo-dev-terraform-anthonyoleary'
    }


	stages {
	stage("Deploy to staging") {
        
	    steps{
               git url: 'https://github.com/londonanthonyoleary/address-book'
                step([$class: 'KubernetesEngineBuilder', 
                        projectId: "s-epo-itcoopk8spoc-prj",
                        clusterName: "epo-dev",
                        zone: "europe-west3-a",
                        manifestPattern: 'hem/address-book/',
                        credentialsId: "s-epo-itcoopk8spoc-prj",
                        verifyDeployments: true])

            }
	}
    }
        
}

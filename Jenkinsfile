/*
    Helm install
 */
def helmInstall (namespace, release) {
    echo "Installing ${release} in ${namespace}"

    script {
        /*
        release = "${release}-${namespace}"
        sh "helm repo add helm ${HELM_REPO}; helm repo update"
        sh """
            helm upgrade --install --namespace ${namespace} ${release} \
                --set imagePullSecrets=${IMG_PULL_SECRET} \
                --set image.repository=${DOCKER_REG}/${IMAGE_NAME},image.tag=${DOCKER_TAG} helm/acme
        """
        */
        sh "helm upgrade address-book-develop-preemptible-JENKINS helm/address-book --install --wait --namespace=default --set instance=develop --set k8s.clusterName=epo-dev --set lifecycle=preemptible --set featureBranch=default --set jenkinsBranch=develop --timeout 10m"

        sh "sleep 5"
    }
}


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
steps {
       // namespace = 'default'
       // echo "Deploying"
        helmInstall('default', "123")
        /*
	    steps{
               git url: 'https://github.com/londonanthonyoleary/address-book'
                step([$class: 'KubernetesEngineBuilder', 
                        projectId: "s-epo-itcoopk8spoc-prj",
                        clusterName: "epo-dev",
                        zone: "europe-west3",
                        manifestPattern: 'helm/address-book/',
                        credentialsId: "s-epo-itcoopk8spoc-prj",
                        verifyDeployments: true])

            }
            */
	}
      }
    }
        
}

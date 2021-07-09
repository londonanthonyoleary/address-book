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
        //sh "helm upgrade address-book-develop-preemptible-JENKINS helm/address-book --install --wait --namespace=default --set instance=develop --set k8s.clusterName=epo-dev --set lifecycle=preemptible --set featureBranch=default --set jenkinsBranch=develop --timeout 10m"
        sh "helm upgrade address-book-develop-preemptible-JENKINS helm/address-book --install --wait --namespace=default --set instance=develop --set k8s.clusterName=epo-jenkins-cluster --set lifecycle=preemptible --set featureBranch=default --set jenkinsBranch=develop --timeout 10m"

        sh "sleep 5"
    }
}


pipeline {

 //agent any
/*
agent {
        docker { image 'bitnami/kubectl' }
    }
*/

 agent {
    kubernetes {
      label 'sample-app'
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
metadata:
labels:
  component: ci
spec:
  # Use service account that can deploy to all namespaces
  # serviceAccountName: epo-jenkins-anthony@s-epo-itcoopk8spoc-prj.iam.gserviceaccount.com
  # serviceAccountName: epo-jenkins-anthony
  # serviceAccountName: s-epo-itcoopk8spoc-prj
  # serviceAccountName: epo-dev-terraform-anthonyoleary
  # serviceAccountName: jenkinswithagent
  # serviceAccountName: jenkins
  serviceAccountName: epo-jenkins-service-account@s-epo-itcoopk8spoc-prj.iam.gserviceaccount.com
  containers:
  - name: gcloud
    image: gcr.io/cloud-builders/gcloud
    command:
    - cat
    tty: true
  - name: kubectl
    image: gcr.io/cloud-builders/kubectl
    command:
    - cat
    tty: true
  - name: helm
    image: gcr.io/s-epo-itcoopk8spoc-prj/helm
    command:
    - cat
    tty: true
"""
}
  }


    environment {
        PROJECT_ID = 's-epo-itcoopk8spoc-prj'
        //CLUSTER_NAME = 'epo-dev'
	CLUSTER_NAME = 'epo-jenkins-cluster'    
        LOCATION = 'europe-west3'  
      //  CREDENTIALS_ID = 'epo-dev-terraform-anthonyoleary'
                CREDENTIALS_ID = 's-epo-itcoopk8spoc-prj'


// for helm
CLOUDSDK_COMPUTE_REGION='europe-west3'
//CLOUDSDK_CONTAINER_CLUSTER='epo-dev'
CLOUDSDK_CONTAINER_CLUSTER='epo-jenkins-cluster'	    
//GCLOUD_PROJECT='s-epo-itcoopk8spoc-prj'
//SERVICE_ACCOUNT="epo-jenkins-anthony@s-epo-itcoopk8spoc-prj.iam.gserviceaccount.com"
SERVICE_ACCOUNT="epo-jenkins-service-account@s-epo-itcoopk8spoc-prj.iam.gserviceaccount.com"
    }


	stages {
/*
  stage('Run Helm') {
      steps {
      script {      
      container('helm') {
        sh "helm ls"
       }
      } 
      }
  }
  */

/*
  stage('Run Helm') {
      steps {
          withCredentials([file(credentialsId: 's-epo-itcoopk8spoc-prj', variable: 'KUBECONFIG')]) {
      //     CredentialsUtil.getGoogleCredential(credentialsId: 's-epo-itcoopk8spoc-prj') {
      // withCredentials(credentialsId: 's-epo-itcoopk8spoc-prj') {

      script {      
      container('helm') {
        sh "helm ls"
       }
      } 
      }
      }
  }
  */
      stage('Deploy Production') {
      // Production branch
    
      steps{
        container('kubectl') {
        // Change deployed image in canary to the one we just built
        //  step([$class: 'KubernetesEngineBuilder', namespace:'default', projectId: 's-epo-itcoopk8spoc-prj', clusterName: "epo-dev", zone: "europe-west3-a", manifestPattern: 'simple-deploy.yaml', credentialsId: "s-epo-itcoopk8spoc-prj", verifyDeployments: false])
          //step([$class: 'KubernetesEngineBuilder', namespace:'default', projectId: 's-epo-itcoopk8spoc-prj', clusterName: "epo-dev", zone: "europe-west3", manifestPattern: 'simple-deploy.yaml', credentialsId: "s-epo-itcoopk8spoc-prj", verifyDeployments: false])
           step([$class: 'KubernetesEngineBuilder', namespace:'default', projectId: 's-epo-itcoopk8spoc-prj', clusterName: "epo-jenkins-cluster", zone: "europe-west3", manifestPattern: 'simple-deploy.yaml', credentialsId: "s-epo-itcoopk8spoc-prj", verifyDeployments: false])

         // sh("echo http://`kubectl --namespace=production get service/${FE_SVC_NAME} -o jsonpath='{.status.loadBalancer.ingress[0].ip}'` > ${FE_SVC_NAME}")
         sh("echo gggg1")
       //  sh("gcloud container clusters get-credentials --zone europe-west3 epo-jenkins-anthony ")
       //  sh("echo gggg2")
        }

       container('helm') {
         // kubectl create clusterrolebinding permissive-binding --clusterrole=cluster-admin --user=admin --user=kubelet --group=system:serviceaccounts
         // https://github.com/helm/charts/issues/1092
         sh("echo before helm")
         sh("helm version")
        // sh("kubectl config get-contexts --cluster epo-dev")

         sh("kubectl config get-contexts")
         sh("kubectl config get-clusters")
         //sh("kubectl config set-context gke_s-epo-itcoopk8spoc-prj_europe-west3_epo-dev --cluster=epo-dev --namespace=default")
        // sh("gcloud container clusters get-credentials epo-dev --region europe-west3 --project s-epo-itcoopk8spoc-prj")
//authentication issue:	 sh("gcloud container clusters get-credentials epo-jenkins-cluster --region europe-west3 --project s-epo-itcoopk8spoc-prj")      
         sh("echo after get-contect")
          
        // sh("kubectl config use-context gke_s-epo-itcoopk8spoc-prj_europe-west3_epo-dev")
        // sh("helm upgrade address-book-develop-preemptible helm/address-book --install --wait --namespace=default --set instance=develop --set k8s.clusterName=epo-dev --set lifecycle=preemptible --set featureBranch=default --set jenkinsBranch=develop --timeout 2m")
         sh("helm upgrade address-book-develop-preemptible helm/address-book --install --wait --namespace=default --set instance=develop --set k8s.clusterName=epo-jenkins-cluster --set lifecycle=preemptible --set featureBranch=default --set jenkinsBranch=develop --timeout 2m")
 
       }
      
    }

/*
	  stage("Deploy to staging") {
steps {
       // namespace = 'default'
        echo "Deploying"
       // helmInstall('default', "123")
        
	    
               git url: 'https://github.com/londonanthonyoleary/address-book'
                step([$class: 'KubernetesEngineBuilder', 
                        projectId: "s-epo-itcoopk8spoc-prj",
                        clusterName: "epo-dev",
                        zone: "europe-west3",
                        manifestPattern: 'simple-deploy.yaml',
                        credentialsId: "s-epo-itcoopk8spoc-prj",
                        verifyDeployments: true])
	}
      }
      */


    }
        
}

}

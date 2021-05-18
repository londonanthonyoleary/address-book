

>
docker pull containerhub.internal.epo.org:7777/address-book:0.0.1-g48d5c7e05

docker tag containerhub.internal.epo.org:7777/address-book:0.0.1-g48d5c7e05 eu.gcr.io/s-epo-itcoopk8spoc-prj/address-book:latest
gcloud auth login
docker push eu.gcr.io/s-epo-itcoopk8spoc-prj/address-book:latest 

> branch anthonygcp

  context-path: /sp-ui-npefiling/addressbook-api


>
helm upgrade address-book-develop-preemptible helm/address-book --install --wait --namespace=default --set instance=develop --set k8s.clusterName=epo-dev --set lifecycle=preemptible --set featureBranch=default --set jenkinsBranch=develop --timeout 10m


>
git remote add google ssh://aoleary.external@epo.org@source.developers.google.com:2022/p/s-epo-itcoopk8spoc-prj/r/address-book

 gcloud auth login
 git push --all google
# k8s-mediawiki


Create the Docker file using steps in below link 

https://www.mediawiki.org/wiki/Manual:Running_MediaWiki_on_Red_Hat_Linux
use image - centos7 
Install the httpd and php packages and uncompress the mediawiki tar file
provide the entrypoint and cmd in dockerfile 

Path of dockerfile- mediawiki-dockeri/Dockerfile 

Build the Image and push the same In Docker Hub using below steps.

docker build -t vishal26778/mediawiki:latest 
Retaging the existing Image 
docker tag hi vishal26778/mediawiki:latest
docker push vishal26778/mediawiki:latest


Setup  helm3 on local machine 

curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
$ chmod 700 get_helm.sh
$ ./get_helm.sh

Install kubectl Binaries  

curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.17.0/bin/linux/amd64/kubectl
chmod +x kubectl 

mv kubectl  /usr/local/bin/

kubectl version --short


Setup Ingress controller for K8s Cluster using Helm3

helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm install my-release ingress-nginx/ingress-nginx

Create the Helm charts for mysql and mediawiki 
Path of helm charts - helm/mysql/
                      helm/mediawiki 

For mysql used a stable helm charts available , Created a new db, user and password for mediawiki setup 

helm install -f helm/mysql/values.yaml  mysql  helm/mysql 
For Mediawiki created own chart using 

helm create mediawiki 
added the desired value in  mediawiki/values.yaml 

Install the chart which will create k8s objects deployment,repicasets,service,pod,hpa,ingress 
helm install -f helm/mediawiki/values.yaml  mediawiki  helm/mediawiki

Used ROlling deployment Strategy which create new pod and check the readiness and then terminate the old pod. For scaling used HPA for horizontal scalling when there is Increased in cpu. 

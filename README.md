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

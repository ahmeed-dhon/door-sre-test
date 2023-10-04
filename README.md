## Disclaimer

- I don't have any prior experience to code using either Golang or Nodejs
- The backend code was made by using online example from internet
- The tools used for this test answer are Jenkins for CI/CD, and Helm to deploy to K8s

### golang-service
- Code source: https://gobyexample.com/http-server
- The binary that will be running inside the Docker container is made by using multi-stage build.
- First, the binary is build by using Golang docker image as a builder
- Then, the binary is copied to the Alpine Docker image that will run the binary
- This is done to optimize the Docker image size, and to prevent any code (sensitive or not) to be included inside the Docker image.
- This golang service will run on port 8090

### nodejs-service
- Code source: ttps://www.tutorialsteacher.com/nodejs/create-nodejs-web-server
- This one is quite straightforward, just copy the server.js file to the nodejs Docker image then run the nodejs server as is

### Jenkinsfile
- The CI/CD process is assumed to use Jenkins
- The docker image repository will be using AWS ECR (the account number is just for example)
- Stages explanation
	- `stage ('Checkout')` Jenkins will checkout the code repository and set the directory name as `dist`
	- `stage ('Docker Linter for golang') ` and `stage ('Docker Linter for nodejs")` this stage will do basic docker linter to check any error inside the dockerfile
	- `stage("Build image golang")` and `stage("Build image nodejs")` this stage will build the docker image by using Jenkins'Docker pipeline plugin
	- `stage("Push image golang")` and `stage("Push image nodejs")` this stage will push the docker image to the ECR by using the provided credential
	- `stage("Remove local image")` this stage will remove local docker image that already been pushed to the ECR. This is done to make sure that Jenkins local storage is not full and always available for future deployment.
	- `stage ('Deploy')` this stage will deploy the backend service to k8s cluster by using Helm
		- `helm upgrade --atomic --install` this command will run the installation for the manifest. 
			- `--atomic` is set to roll back the install/upgrade process in case of failed installation
			- `--install` is set to install the manifest for the first time if no release is installed in the cluster.
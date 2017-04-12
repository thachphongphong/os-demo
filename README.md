#DEMO STEP

### Login into OPENSHIFT

oc login -u https://api.preview.openshift.com --token=steves-special-token

### Create new project

oc new-project demo

### Create new build

oc new-build --name=os-springboot-demo codecentric/springboot-maven3-centos~https://github.com/thachphongphong/os-springboot-demo.git

### Create new app

oc new-app --name=os-springboot-demo -i os-springboot-demo

### Create new routes
oc create route edge --hostname os-springboot-demo.preview.openshiftapps.com --service os-springboot-demo
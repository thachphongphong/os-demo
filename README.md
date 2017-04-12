#DEMO STEP

## Login into OPENSHIFT

```oc login -u https://api.preview.openshift.com --token=steves-special-token```

## Create new project

```oc new-project demo```

## CREATE A SERVICE USE S2I (source to image)

### Create new build

```oc new-build --name=spring-boot-demo codecentric/springboot-maven3-centos~https://github.com/thachphongphong/spring-boot-sample-simple.git```

### Create new app

```oc new-app --name=spring-boot-demo -i spring-boot-demo```

### Create new routes

```oc create route edge --hostname spring-boot-demo.preview.openshiftapps.com --service spring-boot-demo```
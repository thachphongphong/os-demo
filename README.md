#DEMO STEP

## Login into OPENSHIFT

```oc login -u https://api.preview.openshift.com --token=steves-special-token```

## Create new project

```oc new-project demo```

## CREATE A APP USE S2I (source to image)

### Create new build

```oc new-build --name=spring-boot-demo codecentric/springboot-maven3-centos~https://github.com/thachphongphong/osspringbootdemo.git```

### Create new app

```oc new-app --name=spring-boot-demo -i spring-boot-demo```

### Create new routes

```oc create route edge --hostname spring-boot-demo.44fs.preview.openshiftapps.com --service spring-boot-demo```

## CREATE A APP WITH WAR FILE (wildfly:latest or tomcat-s2i)

```oc new-app wildfly:latest~. --name mysample```

```oc start-build mysample --from-file=sample.war```

```oc expose svc mysample```

[Docker image nginx-s2i](https://hub.docker.com/r/lunik/s2i-nginx/) 

## CREATE A APP FROM DOCKER IMAGE

docker pull openshift/hello-openshift

###Registry: registry.preview.openshift.com

1.https://api.preview.openshift.com/oauth/token/request
> oc login --token=MFDrUPYX11u8vIFxppvUb5PUkimZ5eGcAn5qk3T0ycA --server=https://api.preview.openshift.com

2. login to registry
docker login -u `oc whoami` -p `oc whoami -t` registry.preview.openshift.com


3.
docker tag NAME registry.preview.openshift.com/<project name>/<image name>
> docker tag openshift/hello-openshift registry.preview.openshift.com/ldt/hello-openshift

4.
docker push registry.preview.openshift.com/<project name>/<image name>
> docker push registry.preview.openshift.com/ldt/hello-openshift

5.
oc get is

5.
oc new-app hello-openshift --name=hello-openshift

6.create route
> oc create route edge --hostname hello-openshift.44fs.preview.openshiftapps.com --service hello-openshift

7.delete
oc delete is NAME

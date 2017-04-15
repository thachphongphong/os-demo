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

```oc create route edge --hostname spring-boot-demo-ldt.44fs.preview.openshiftapps.com --insecure-policy=Redirect --service spring-boot-demo```

## CREATE A APP WITH WAR FILE (wildfly:latest or tomcat-s2i)
1. create new app

```oc new-app wildfly:latest~. --name mysample```

2. create a build

```oc start-build mysample --from-file=sample.war```

3. create serive and route
```oc expose svc mysample```

[Docker image nginx-s2i](https://hub.docker.com/r/lunik/s2i-nginx/) 

## CREATE A APP FROM DOCKER IMAGE

docker pull openshift/hello-openshift

###Registry: registry.preview.openshift.com

1. Get token and login
> https://api.preview.openshift.com/oauth/token/request
> oc login --token=MFDrUPYX11u8vIFxppvUb5PUkimZ5eGcAn5qk3T0ycA --server=https://api.preview.openshift.com

2. login to registry
> docker login -u `oc whoami` -p `oc whoami -t` registry.preview.openshift.com


3. tag image
docker tag NAME registry.preview.openshift.com/<project name>/<image name>
> docker tag openshift/hello-openshift registry.preview.openshift.com/ldt/hello-openshift

4. push image
 docker push registry.preview.openshift.com/<project name>/<image name>
> docker push registry.preview.openshift.com/ldt/hello-openshift

5. check image is exist
oc get is

6. create new app with image
oc new-app hello-openshift --name=hello-openshift

7. create route
> oc create route edge --hostname hello-openshift-ldt.44fs.preview.openshiftapps.com  --service hello-openshift

9.delete
oc delete is NAME


## DELETE PROJECT

oc delete project <project_name>

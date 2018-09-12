# Debugging Microservices

  * [Jaeger](https://github.com/dwojciec/debugging-microservices#jaeger)
  * [Squash](https://github.com/dwojciec/debugging-microservices#squash)
  * [Gloo](https://github.com/dwojciec/debugging-microservices#gloo)
 
    
# Jaeger 

## Demo deployment
The application demo used is the famous "Hot R.O.D - Rides on Demand". We are deploying Jaeger and the application on top of Openshift.

```
oc new-project jaeger-test
oc process -f https://raw.githubusercontent.com/jaegertracing/jaeger-openshift/master/all-in-one/jaeger-all-in-one-template.yml | oc create -f -
oc process -f https://raw.githubusercontent.com/dwojciec/debugging-microservices/master/jaeger/hotrod-app.yml | oc create -f -

```

## Demo scenario


## More informations
  
  * [`Jaeger OpenShift Templates`](https://github.com/jaegertracing/jaeger-openshift/blob/master/README.md)
  
  * [`Hot R.O.D - Rides on demand`](https://github.com/jaegertracing/jaeger/tree/master/examples/hotrod)

  * Developing a Go program using OpenTracing -  Tutorial [`here`](https://github.com/yurishkuro/opentracing-tutorial/tree/master/go)


# Squash 
**Prerequisites** : using a Openshift version 3.9. For higher version of 3.9 you have to change the version of the squash image (from v0.2.1 to v0.3.1) to use but not tested yet on 3.10. 

squash-server and squash-client images are available [`server`](https://hub.docker.com/r/soloio/squash-server/tags/) and [`client`](https://hub.docker.com/r/soloio/squash-client/tags/)

## Demo deployment

```
oc new-project squash
oc process -f https://raw.githubusercontent.com/dwojciec/debugging-microservices/master/squash/squash-template.yaml -l name=squash | oc create -f -
oc adm policy add-scc-to-user privileged -z squash-client
oc get route
export SQUASH_SERVER_URL=

```

###install squash CLI locally on Linux or Mac OSX
see : [`here`](https://github.com/solo-io/squash/tree/master/docs/install#command-line-interface-cli)

```
squash list a
squash list r 
```

### install squash IDE plugin (Visual Studio Code and IntelliJ)
see: [`here`](https://github.com/solo-io/squash/blob/master/docs/IDEs.md#ides)
 
###locally clone Application example  

```
$ oc new-project demo-squash
$ oc process -f https://raw.githubusercontent.com/dwojciec/debugging-microservices/master/squash/demo-squash.yaml | oc create -f - 

```

## Demo scenario


# Gloo
 **Prerequisites** : installation of glooctl command line interface tool  from [`here`](https://github.com/solo-io/glooctl/releases/latest/)
 
 ```
 exemple on MAC OSX:
 
 wget https://github.com/solo-io/glooctl/releases/download/v0.3.0/glooctl-darwin-amd64
 ```
 
## Demo deployment

We are installing gloo inside a project called *gloo-system* using **glooctl** CLI installed above. 
We are deploying a simple petclinic java springboot apps attached to a mysql app, and an application service written in GO which adds "location" colums to the list of veterinarians Menu.
 
 ```
 $ oc login 
 $ glooctl install openshift 
 $ oc project gloo-system
 
 Petclinic Monolithic app 
 $ oc project default
 $ oc create -f https://raw.githubusercontent.com/solo-io/gloo/master/example/demo/yamls/pet-clinic.yaml
 
 Veterinarian app service written in GO
 $ oc create https://raw.githubusercontent.com/solo-io/gloo/master/example/demo/yamls/vets.yaml
 ```
 
 Note - source code for this demo is here: [https://github.com/solo-io/spring-petclinic](https://github.com/solo-io/spring-petclinic), [https://github.com/solo-io/petclinic-vet](https://github.com/solo-io/petclinic-vet). 
 

 Creation of a **AWS Lambda function**
 
 Let's expand the app functionality by displaying a contact form and saving the contact response to an AWS S3 bucket.
 To do it you can follow the procedure [`here`](https://github.com/solo-io/gloo/tree/master/example/demo#add-some-cloud)
 
 ## Demo scenario
 
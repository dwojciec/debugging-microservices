# Debugging Microservices

  * Jaeger
  * Squash
 
    
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
see: ['here'](https://github.com/solo-io/squash/blob/master/docs/IDEs.md#ides)
 
###locally clone Application example  

```
$ oc new-project demo-squash
$ oc process -f https://raw.githubusercontent.com/dwojciec/debugging-microservices/master/squash/demo-squash.yaml | oc create -f - 

```

## Demo scenario



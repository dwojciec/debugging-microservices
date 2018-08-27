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
## Demo deployment

## Demo scenario



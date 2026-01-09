```shell
kubectl run curl --image=curlimages/curl --rm=true --restart=Never -ti -- -X POST -v \
   -H "content-type: application/json"  \
   -d '{"customerId":"123"}' \
   http://webhook-eventsource-svc.argo-events.svc.cluster.local/example
```
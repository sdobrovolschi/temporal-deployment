### Produce an event to RabbitMQ
```shell
kubectl run curl --image=docker.io/curlimages/curl -i --rm --restart=Never -- sh -c '
  UUID=$(cat /proc/sys/kernel/random/uuid)

  curl -X POST \
    -u default_user_MI2WjwyxlKx-XlTFhnb:kb-zdYP4cggl4GiSGjzLMud8hwg11lRB \
    -H "content-type: application/json" \
    -d "{
        \"routing_key\": \"\",
        \"properties\": {
          \"content_type\": \"application/json\"
        },
        \"payload\": \"{\\\"messageId\\\":\\\"$UUID\\\",\\\"userId\\\":\\\"4ff2cd72-77b1-4c4e-98e5-26c0f0aafc10\\\",\\\"event\\\":\\\"travelPurchaseMade\\\",\\\"properties\\\":{\\\"amount\\\":{\\\"value\\\":75.25,\\\"currency\\\":\\\"EUR\\\"}}}\",
        \"payload_encoding\": \"string\"
      }" \
    http://rabbitmq-cluster.rabbitmq-system.svc.cluster.local:15672/api/exchanges/%2F/exchange-event/publish
'
```

### Produce a blast of events to RabbitMQ
```shell
kubectl run curl --image=docker.io/curlimages/curl -i --rm --restart=Never -- sh -c '
for i in $(seq 1 10000); do
  UUID=$(cat /proc/sys/kernel/random/uuid)

  curl -X POST \
    -u default_user_MI2WjwyxlKx-XlTFhnb:kb-zdYP4cggl4GiSGjzLMud8hwg11lRB \
    -H "content-type: application/json" \
    -d "{\"routing_key\":\"\",\"properties\":{\"content_type\":\"application/json\"},\"payload\":\"{\\\"messageId\\\":\\\"$UUID\\\",\\\"userId\\\":\\\"4ff2cd72-77b1-4c4e-98e5-26c0f0aafc10\\\",\\\"event\\\":\\\"travelPurchaseMade\\\",\\\"properties\\\":{\\\"amount\\\":{\\\"value\\\":75.25,\\\"currency\\\":\\\"EUR\\\"}}}\",\"payload_encoding\":\"string\"}" \
    http://rabbitmq-cluster.rabbitmq-system.svc.cluster.local:15672/api/exchanges/%2F/exchange-event/publish
done
'
```

# Cloudify manager AIO helm chart

## Description

It's a helm chart for cloudify manager which is:

* Not highly available, has one replica only.
* Has no persistent volume to survive restarts/failures.
* Has all components on board (as part of docker container): Message Broker and DB part of it.

**This is the best and most simple way to make yourself familiar with cloudify, running a Cloudify manager AIO is a matter of minutes**


## Installation

helm repo add cloudify-helm https://cloudify-cosmo.github.io/cloudify-helm

helm install cloudify-manager-aio cloudify-helm/cloudify-manager-aio


## Configuration options for values.yaml:

### Image:

```
image:
  repository: "cloudifyplatform/community-cloudify-manager-aio"
  tag: "latest"
  pullPolicy: IfNotPresent
```

### Service:

```
service:
  type: LoadBalancer
  name: cloudify-manager-aio
  rabbitmq:
    port: 5671
  http:
    port: 80
  https:
    port: 443
  internalRest:
    port: 53333
```

### node selector - select on which nodes cloudify manager AIO may run:

```
nodeSelector: {}
# nodeSelector:
#   nodeType: onDemand 
```


### resources requests and limits:
```
resources:
  requests:
    memory: 0.5Gi
    cpu: 0.5
```

### readiness probe may be enabled/disabled
```
readinessProbe:
  enabled: true
  port: 80
  path: /console
  initialDelaySeconds: 10
```


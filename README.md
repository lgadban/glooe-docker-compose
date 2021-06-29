## Install Gloo in mTLS mode

Need to set value:
```
global:
  glooMtls:
    enabled: true
```

## Expose xDS services via Passthrough Routes
```
oc apply -f xds-routes.yaml
```

## Retrieve cert data for mTLS
```
mkdir gloo-mtls-certs

oc get secret -n gloo-system gloo-mtls-certs -o jsonpath='{.data.tls\.key}' | base64 -d > gloo-mtls-certs/tls.key
oc get secret -n gloo-system gloo-mtls-certs -o jsonpath='{.data.tls\.crt}' | base64 -d > gloo-mtls-certs/tls.crt
oc get secret -n gloo-system gloo-mtls-certs -o jsonpath='{.data.ca\.crt}' | base64 -d > gloo-mtls-certs/ca.crt
```

## Run data-plane via Docker
```
docker-compose up -d
```

## Setup `Gateway` and configure petstore sample app
```
oc apply -f gloo-configs/vm-gateway.yaml
oc apply -f gloo-configs/vm-petstore.yaml
```
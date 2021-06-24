Need to set value:
```
global:
  glooMtls:
    enabled: true
```

```
mkdir gloo-mtls-certs

oc get secret -n gloo-system gloo-mtls-certs -o jsonpath='{.data.tls\.key}' | base64 -d > gloo-mtls-certs/tls.key

oc get secret -n gloo-system gloo-mtls-certs -o jsonpath='{.data.tls\.crt}' | base64 -d > gloo-mtls-certs/tls.crt

oc get secret -n gloo-system gloo-mtls-certs -o jsonpath='{.data.ca\.crt}' | base64 -d > gloo-mtls-certs/ca.crt
```

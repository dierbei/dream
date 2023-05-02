## GatewayClass

#### 参考文档
```text
# GatewayClass
https://gateway-api.sigs.k8s.io/api-types/gatewayclass/
```

#### Istio Ingress
```yaml
apiVersion: networking.istio.io/v1alpha3
kind: GatewayClass
metadata:
  name: my-gateway-class
spec:
  controllerName: istio.io/gateway-controller
```
# nginx-ingress

## Nodeport-ingress
Note: Refer to https://kubernetes.github.io/ingress-nginx/deploy/ for more information

1) The following Mandatory Command is required for all deployment
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/mandatory.yaml
```
2) Since we are using bare-metal servers, we install ingress as a NodePort service.. 
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/provider/baremetal/service-nodeport.yaml
```
i) if want a fixed nodeport port number Run
```
kubectl apply -f ./ingress/service-nodeport_withfixednodeport.yaml
```
3) Verify the installation
```
kubectl get pods --all-namespaces -l app.kubernetes.io/name=ingress-nginx
```
4) Apply deployment to test ingress
```
kubectl apply -f ./ingress/papaya.yaml
kubectl apply -f ./ingress/durian.yaml
kubectl apply -f ./ingress/fruits-ingress.yaml
```
5) Access the services
```
curl localhost:30080/durian
curl localhost:30080/papaya
```
## With Metallb
Note: Refer to https://metallb.universe.tf/installation/ for more information

1) To install MetalLB, apply the manifest:
```
kubectl apply -f https://raw.githubusercontent.com/google/metallb/v0.8.3/manifests/metallb.yaml
```
2) Layer 2 configuration config.yaml
```
apiVersion: v1
kind: ConfigMap
metadata:
  namespace: metallb-system
  name: config
data:
  config: |
    address-pools:
    - name: default
      protocol: layer2
      addresses:
      - 203.0.113.10-203.0.113.15

```
```
kubectl apply -f ./ingress/metallbconfig.yaml
```

# nginx-ingress

## Quickstart
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

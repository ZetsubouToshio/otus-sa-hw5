# Добавить репозиторий
```
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
```
# Установка 
```
helm install nginx ingress-nginx/ingress-nginx -f values.yaml --atomic
```

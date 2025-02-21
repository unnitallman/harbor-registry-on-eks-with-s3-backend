kubectl create secret generic aws-s3-secret -n harbor \
  --from-literal=AWS_ACCESS_KEY_ID=<AWS_ACCESS_KEY_ID> \
  --from-literal=AWS_SECRET_ACCESS_KEY=<AWS_SECRET_ACCESS_KEY> \
  --dry-run=client -o yaml | kubectl apply -f -

kubectl get secret aws-s3-secret -n harbor -o jsonpath='{.data}' | jq

helm repo add harbor https://helm.goharbor.io && helm repo update
helm install harbor harbor/harbor -n harbor -f values.yaml
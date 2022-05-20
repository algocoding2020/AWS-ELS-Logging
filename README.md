# AWS-ELS-Logging

containers redirect logs to /var/log/containers/.*.log files

EFK stack for logging

Elastic search, FlunetD/FluentBit, Kibana

Fluentd demo:

kubectl apply -f  fluentd.yml

kubectl get pods -w --namespace-kube-system

kubectl apply -f loadbalancer-service.yaml

kubectl apply-f  hello-k8s-forlog.yml

now create ES using aws cli

aws es create-elasticsearch-domain \

  --domain-name eks-logs \

  --elasticsearch-version 7.4 \

  --elasticsearch-cluster-config \

  InstanceType=t2.small.elasticsearch,InstanceCount=1 \

  --ebs-options EBSEnabled=true,VolumeType=standard,VolumeSize=10 \

  --access-policies '{"Version":"2012-10-17","Statement":[{"Effect":"Allow","Principal":{"AWS":["*"]},"Action":["es:*"],"Resource":"*"}]}'

EKS uses lambda to push the logs from cloudwatch

you are no need to create lambda ,AWS will dothat . You just need IAM role towith ES fullaccess .

in cloudwatch use subscription filter and configure ES  by selecting ES and lambda role

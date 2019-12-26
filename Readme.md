# sysdig-testing




## Prerequisite
NOTE: This tutorial will create a cluster in us-west-1 using the 10.0.0.0/16 subnet

- terraform – https://www.terraform.io
- kubectl
- aws-iam-authenticator --> https://github.com/awsdocs/amazon-eks-user-guide/blob/master/doc_source/install-aws-iam-authenticator.md
- awscli


## EKS Installation with terraform
```
- git clone https://github.com/Eslamanwar/sysdig-testing.git
- export AWS_ACCESS_KEY_ID={YOUR-AWS-ACCESS-KEY-ID}
- export AWS_SECRET_ACCESS_KEY={YOUR-AWS-SECRET-ACCESS-KEY}
- cd eks/
- terraform init 
- terraform plan
- terraform apply
```

### Setting Up kubectl to connect to cluster
```
mkdir ~/.kube/
terraform output kubeconfig>~/.kube/config
terraform output config_map_aws_auth > configmap.yml
kubectl apply -f configmap.yml
```

### Check and verify eks installation
```
kubectl version
kubectl get nodes -o wide
```



## Deploy Sysdig
- Modify the ./sysdig/Secret.yaml file and insert your Sysdig cloud Access key encoded 64 format

```
- kubectl create -f ./sysdig/
```

## Deploy sample java application to collect promethus metrics
```
- kubectl create -f sample-app/sample-app.yaml
```



## Results
- with sysdig you can monitor the Network traffic between pods
![alt text](https://github.com/Eslamanwar/sysdig-testing/blob/master/images/network-traffic.png?raw=true)



- It can be intergrated to collect promethues metrics for the sample application we just created
![alt text](https://github.com/Eslamanwar/sysdig-testing/blob/master/images/Promethus-metrics.png?raw=true)







## Deploy promethus server with node exporter

```
kubectl create -f prometheus/
```


![alt text](https://github.com/Eslamanwar/sysdig-testing/blob/master/images/promethus.png?raw=true)







































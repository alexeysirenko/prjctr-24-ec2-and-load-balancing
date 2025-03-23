# prjctr-24-ec2-and-load-balancing

Replace with your AWS ECR registry URL and run:

```
docker build -t test-dev:latest .
docker tag test-dev:latest 523717802721.dkr.ecr.eu-central-1.amazonaws.com/test-dev:latest
aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 523717802721.dkr.ecr.eu-central-1.amazonaws.com/test-dev
docker push 523717802721.dkr.ecr.eu-central-1.amazonaws.com/test-dev:latest
cd .terraform
terraform init
terraform apply -var-file="terraform.tfvars"
```

You should receive in the output DNS name of the load balancer (for example):

```
alb_dns_name = "test-dev-alb-443113966.eu-central-1.elb.amazonaws.com"
```

Open it in your browser or with the `curl` (example):

````
You can test your ALB quickly using `curl`. Run this command (example):

```shell
curl -s http://test-dev-alb-443113966.eu-central-1.elb.amazonaws.
com:80
````

```
Hello from ip-10-0-4-139.eu-central-1.compute.internal
```

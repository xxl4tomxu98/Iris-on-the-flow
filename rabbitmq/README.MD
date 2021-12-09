# Katana ML Skipper RabbitMQ Service

[RabbitMQ](https://www.rabbitmq.com/) is open source message broker service, it enables services communication and workflow operations. Katana ML Skipper communication service runs on top of RabbitMQ.

## Author

[Katana ML](https://katanaml.io), [Andrej Baranovskij](https://github.com/abaranovskis-redsamurai)

## Instructions

To run all services, check instructions in main [README](https://github.com/katanaml/katana-skipper/blob/master/README.md)

### Running RabbitMQ service locally

1. Run Docker Compose script

``` shell
docker-compose up --build -d
```

2 RabbitMQ dashboard

``` url
http://localhost:15672 (skipper/welcome1)
```

#### Build and run Kubernetes Pod

Instructions are based on content explained by [That DevOps Guy](https://www.youtube.com/c/MarcelDempers)

1. Create namespace

``` shell
kubectl create ns rabbits
```

2 Check storage class

``` shell
kubectl get storageclass
```

3 Define RabbitMQ role mappings

``` shell
kubectl apply -n rabbits -f rabbit-rbac.yaml
```

4 Define RabbitMQ secret

``` shell
kubectl apply -n rabbits -f rabbit-secret.yaml
```

5 Define RabbitMQ configs

``` shell
kubectl apply -n rabbits -f rabbit-configmap.yaml
```

6 Create RabbitMQ cluster and pods

``` shell
kubectl apply -n rabbits -f rabbit-statefulset.yaml
```

7 Verify pods

``` shell
kubectl -n rabbits get pods
```

8 Verify assigned persistence volumes

``` shell
kubectl -n rabbits get pvc
```

9 Open external access, to access RabbitMQ UI

``` shell
kubectl -n rabbits port-forward rabbitmq-0 15672:15672
```

10 RabbitMQ UI URL

``` url
http://localhost:15672/ (skipper/welcome1)
```

11 Scale RabbitMQ cluster

``` shell
kubectl scale -n rabbits statefulsets rabbitmq --replicas=2
```

12 Delete all resources

``` shell
kubectl delete all --all -n rabbits
```

## Structure

``` shell
.
├── Dockerfile
├── init.sh
├── rabbit-configmap.yaml
├── rabbit-rbac.yaml
├── rabbit-secret.yaml
├── rabbit-statefulset.yaml
└── README.MD
```

## License

Licensed under the Apache License, Version 2.0. Copyright 2020-2021 Katana ML, Andrej Baranovskij. [Copy of the license](https://github.com/katanaml/katana-skipper/blob/master/LICENSE).

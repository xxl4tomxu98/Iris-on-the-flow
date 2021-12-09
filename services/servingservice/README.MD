# Katana ML Skipper Serving Service

## Author

[Katana ML](https://katanaml.io), [Andrej Baranovskij](https://github.com/abaranovskis-redsamurai)

## Instructions

To run all services, check instructions in main [README](https://github.com/katanaml/katana-skipper/blob/master/README.md)

### Run the service without Docker

1. Install libraries

``` shell
pip install -r requirements.txt
```

2 Start service

``` shell
python main.py
```

3 Start storage service

``` shell
python storage_controller.py
```

#### Build and run individual container

1. Build container

``` shell
docker build --tag katanaml/serving-service .
```

2 Run container

``` shell
docker run -it -d --name serving-service katanaml/serving-service:latest
```

#### Build and run Kubernetes Pod

1. Create namespace

``` shell
kubectl create ns katana-skipper
```

2 Check available storage class

``` shell
kubectl get storageclass
```

3 Create volume

``` shell
kubectl apply -f servingservice-pv.yaml
```

4 Create volume claim

``` shell
kubectl apply -n katana-skipper -f servingservice-pvc.yaml
```

5 Create Pod

``` shell
kubectl apply -n katana-skipper -f servingservice-pod.yaml
```

6 Check Pod status

``` shell
kubectl get -n katana-skipper pods
```

7 Open Pod logs, use storage-service for sidecar container logs

``` shell
kubectl logs -n katana-skipper -f -l app=serving-service -c serving-main-service
```

or

``` shell
kubectl logs -n katana-skipper -f <POD_NAME> -c serving-main-service
```

8 Check volume

``` shell
kubectl get pv
```

9 Check volume claim

``` shell
kubectl get -n katana-skipper pvc
```

10 Execute commands inside container

``` shell
kubectl exec -it -n katana-skipper <POD_NAME> -c serving-main-service -- bash
```

11 Scale Pod

``` shell
kubectl scale -n katana-skipper deployment serving-service --replicas=3
```

12 Delete Deployment and Volumes

``` shell
kubectl delete -n katana-skipper -f servingservice-pod.yaml
```

``` shell
kubectl delete -n katana-skipper -f servingservice-pvc.yaml
```

``` shell
kubectl delete -f servingservice-pv.yaml
```

13 Delete all resources

``` shell
kubectl delete all --all -n katana-skipper
```

## Structure

``` stru
.
├── app
│   └── serving_service.py
├── main.py
├── Dockerfile
├── README.md
├── servingservice-pv.yaml
├── servingservice-pvc.yaml
├── servingservice-pod.yaml
├── storage
├────  app
│       └── storage_service.py
│      ├── Dockerfile
│      ├── requirements.txt
│      └── storage_controller.py
└── requirements.txt
```

## License

Licensed under the Apache License, Version 2.0. Copyright 2020-2021 Katana ML, Andrej Baranovskij. [Copy of the license](https://github.com/katanaml/katana-skipper/blob/master/LICENSE).

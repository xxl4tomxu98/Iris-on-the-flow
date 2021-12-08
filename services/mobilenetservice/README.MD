# Katana ML Skipper Mobilenet Service

## Author

[Katana ML](https://katanaml.io), [Andrej Baranovskij](https://github.com/abaranovskis-redsamurai)

## Instructions

This is a sample service implementation with JavaScript and Node.js

To run all services, check instructions in main [README](https://github.com/katanaml/katana-skipper/blob/master/README.md)

### Run the service without Docker

1. Install dependencies:

``` shell
npm install
```

2 Start service

``` shell
node src/main.js
```

or with live reload

``` shell
nodemon src/main.js
```

### Build and run individual container

1. Build container

``` shell
docker build --tag katanaml/mobilenet-service .
```

2 Run container

``` shell
docker run -it -d --name mobilenet-service katanaml/mobilenet-service:latest
```

3 Monitor logs

``` shell
docker logs --follow mobilenet-service
```

### Build and run Kubernetes Pod

1. Create namespace

``` shell
kubectl create ns katana-skipper
```

2 Create Pod

``` shell
kubectl apply -n katana-skipper -f mobilenetservice-pod.yaml
```

3 Check Pod status

``` shell
kubectl get -n katana-skipper pods
```

4 Open Pod logs

``` shell
kubectl logs -n katana-skipper -f -l app=mobilenet-service
```

5 Execute commands inside container

``` shell
kubectl exec -it -n katana-skipper <POD_NAME> -c mobilenet-service -- bash
```

6 Scale Pod

``` shell
kubectl scale -n katana-skipper deployment mobilenet-service --replicas=2
```

7 Delete Deployment and Volumes

``` shell
kubectl delete -n katana-skipper -f mobilenetservice-pod.yaml
```

8 Delete all resources

``` shell
kubectl delete all --all -n katana-skipper
```

## Structure

``` shell
.
├── src
│   └── app
│       ├── orange.jpeg
│       └── mobilenet_service.js
├──── main.js
├── Dockerfile
├── mobilenetservice-pod.yaml
├── README.md
├── package-lock.json
└── package.json
```

## License

Licensed under the Apache License, Version 2.0. Copyright 2020-2021 Katana ML, Andrej Baranovskij. [Copy of the license](https://github.com/katanaml/katana-skipper/blob/master/LICENSE).

# Katana ML Skipper Logger

Logger service, logging runs in the background, without blocking API endpoint.

## Author

[Katana ML](https://katanaml.io), [Andrej Baranovskij](https://github.com/abaranovskis-redsamurai)

## Instructions

To run all services, check instructions in main [README](https://github.com/katanaml/katana-skipper/blob/master/README.md)

### Run the service without Docker

1. Install libraries

``` shell
pip install -r requirements.txt
```

2 Start FastAPI

``` shell
uvicorn endpoint:app --port=5001 --reload
```

3 Logger FastAPI endpoints

``` url
http://127.0.0.1:5001/docs
```

4 Monitor logs

``` shell
docker logs --follow skipper-logger
```

### Build and run individual container

1. Build container

``` shell
docker build --tag katanaml/skipper-logger .
```

2 Run container

``` shell
docker run -it -d --name skipper-logger -p 5001:5001  katanaml/skipper-logger:latest
```

3 Logger FastAPI endpoints

``` url
http://127.0.0.1:5001/docs
```

4 Monitor logs

``` shell
docker logs --follow skipper-logger
```

### Build and run Kubernetes Pod

1. Create namespace

``` shell
kubectl create ns katana-skipper
```

2 Create Pod

``` shell
kubectl apply -n katana-skipper -f logger-pod.yaml
```

3 Check Pod status

``` shell
kubectl get -n katana-skipper pods
```

4 Describe Pod

``` shell
kubectl describe -n katana-skipper pods skipper-logger
```

5 Open Pod port for testing purposes

``` shell
kubectl port-forward -n katana-skipper deploy/skipper-logger 5001:5001
```

6 Open Pod logs

``` shell
kubectl logs -n katana-skipper -f -l app=skipper-logger
```

7 Test URL

``` shell
http://127.0.0.1:5001/docs
```

8 Check Pod service

``` shell
kubectl get -n katana-skipper svc skipper-logger
```

9 Delete Deployment

``` shell
kubectl delete -n katana-skipper -f logger-pod.yaml
```

10 Delete all resources

``` shell
kubectl delete all --all -n katana-skipper
```

## Structure

``` shell
.
├── api 
│   ├── logger.py
│   ├── models.py
│   └── router.py
├── endpoint.py
├── Dockerfile
├── README.md
├── logger-pod.yaml
└── requirements.txt
```

## License

Licensed under the Apache License, Version 2.0. Copyright 2020-2021 Katana ML, Andrej Baranovskij. [Copy of the license](https://github.com/katanaml/katana-skipper/blob/master/LICENSE).

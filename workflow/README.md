# Katana ML Skipper Workflow

Returns queue name, based on task ID. This allows to route event to the correct queue, without hardcoding logic in the Web API.

## Author

[Katana ML](https://katanaml.io), [Andrej Baranovskij](https://github.com/abaranovskis-redsamurai)

## Instructions

To run all services, check instructions in main [README](https://github.com/katanaml/katana-skipper/blob/master/README.md)

### Run the service without Docker

1 Install libraries

``` shell
pip install -r requirements.txt
```

2 Start FastAPI

``` shell
uvicorn endpoint:app --port=5000 --reload
```

3 Workflow FastAPI endpoints

``` url
http://127.0.0.1:5000/docs
```

### Build and run individual container

1 Build container

``` shell
docker build --tag katanaml/skipper-workflow .
```

2 Run container

``` shell
docker run -it -d --name skipper-workflow -p 5000:5000  katanaml/skipper-workflow:latest
```

3 Workflow FastAPI endpoints

``` url
http://127.0.0.1:5000/docs
```

#### Build and run Kubernetes Pod

1 Create namespace

``` shell
kubectl create ns katana-skipper
```

2 Create Pod

``` shell
kubectl apply -n katana-skipper -f workflow-pod.yaml
```

3 Check Pod status

``` shell
kubectl get -n katana-skipper pods
```

4 Describe Pod

``` shell
kubectl describe -n katana-skipper pods skipper-workflow
```

5 Open Pod port for testing purposes

``` shell
kubectl port-forward -n katana-skipper deploy/skipper-workflow 5000:5000
```

6 Open Pod logs

``` shell
kubectl logs -n katana-skipper -f -l app=skipper-workflow
```

7 Test URL

``` url
http://127.0.0.1:5000/docs
```

8 Check Pod service

``` shell
kubectl get -n katana-skipper svc skipper-workflow
```

9 Delete Deployment

``` shell
kubectl delete -n katana-skipper -f workflow-pod.yaml
```

10 Delete all resources

``` shell
kubectl delete all --all -n katana-skipper
```

## Structure

``` shell
.
├── api 
│   ├── models.py
│   ├── router.py
│   ├── workflow.json
│   └── workflow.py
├── endpoint.py
├── Dockerfile
├── README.md
├── workflow-pod.yaml
└── requirements.txt
```

## License

Licensed under the Apache License, Version 2.0. Copyright 2020-2021 Katana ML, Andrej Baranovskij. [Copy of the license](https://github.com/katanaml/katana-skipper/blob/master/LICENSE).

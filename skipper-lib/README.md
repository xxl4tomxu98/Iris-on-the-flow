# Katana ML Skipper

## Overview

This is a helper library for Katana ML Skipper workflow product. The idea of this library is to wrap all reusable code to simplify and improve workflow implementation.

Supported functionality:

- API to communicate with RabbitMQ for event receiver/producer
- Workflow call helper
- Logger call helper

## Author

[Katana ML](https://katanaml.io), [Andrej Baranovskij](https://github.com/abaranovskis-redsamurai)

## Instructions

Version number should be updated in __init__.py and pyproject.toml

1 Install Poetry

``` shell
pip install poetry
```

2 Add pika and requests libraries

``` shell
poetry add pika
poetry add requests
```

3 Build

``` shell
poetry build
```

4 Publish to TestPyPI

``` shell
poetry publish -r testpypi
```

5 Install from TestPyPI

``` shell
pip install -i https://test.pypi.org/simple/ --extra-index-url https://pypi.org/simple  skipper-lib
```

6 Publish to PyPI

``` shell
poetry publish
```

7 Install from PyPI

``` shell
pip install skipper-lib
```

8 Test imported library from CMD

``` shell
python -m skipper_lib
```

9 Import EventReceiver

``` shell
from skipper_lib.events.event_receiver import EventReceiver
```

10 Import EventProducer

``` shell
from skipper_lib.events.event_producer import EventProducer
```

## Structure

``` shell
.
├── LICENSE
├── poetry.lock
├── pyproject.toml
├── skipper_lib
│   ├── __init__.py
│   ├── __main__.py
│   ├── events
│       ├── __init__.py
│       ├── exchange_producer.py
│       ├── exchange_receiver.py
│       ├── event_producer.py
│       └── event_receiver.py
│   ├── logger
│       ├── __init__.py
│       └── logger_helper.py
│   ├── workflow
│       ├── __init__.py
│       └── workflow_helper.py
└── README.md
```

## License

Licensed under the Apache License, Version 2.0. Copyright 2020-2021 Katana ML, Andrej Baranovskij. [Copy of the license](https://github.com/katanaml/katana-skipper/blob/master/LICENSE).

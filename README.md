# lacp-service

lacp-service is an example python application using [Frinx uniconfig framework](https://frinx.io/blog/uniconfig-framework)
to provision simple [LACP service](https://en.wikipedia.org/wiki/Link_aggregation). Purpose of the application is to
show potentional users of uniconfig how to use it in an efficient and simple manner.

## Prerequisites

To be able to run and play wit the application, you need to have [Frinx ODL distribution](https://frinxio.github.io/Frinx-docs/FRINX_ODL_Distribution/carbon.html) 
up and running. Devices you want to configure have to be accesible by uniconfig.            

`lacp_service.py` requires python 3.6 and flask installed in your environment. You need to also install swagger_uniconfig package. You can do it with following command:

```
pip install frinx_uniconfig-3.1.7.rc16_frinx_SNAPSHOT-py3-none-any.whl
```

## Provisioning the service

Now you should be able to provision the LACP service. You can start the application

```
export FLASK_APP=lacp_service.py
flask run
```

lacp_service.py exposes really simple and straightforward REST API. To provision new LACP service, issue simple POST request

```
curl --request POST \
  --url http://127.0.0.1:5000/service/new-service \
  --header 'Content-Type: application/json' \
  --data '{\n    "node1": {\n        "name": "xr5",\n        "bundle": "122",\n        "ports": [\n            "GigabitEthernet0/0/0/1",\n            "GigabitEthernet0/0/0/3"\n        ]\n    },\n    "node2": {\n        "name": "xr6",\n        "bundle": "187",\n        "ports": [\n            "GigabitEthernet0/0/0/2"\n        ]\n    }\n}'
```

lacp_service.py basically translates this POSt request into openconfig uniconfig based configuration and provision the service.



# Aggregate multiple connections with LACP service

In this lab, you will learn about LACP service. It is an example Python application that is using Frinx uniconfig framework to provision simple LACP service. Purpose of the application is to show potentional users of uniconfig how to use it in an efficient and simple manner.

## Objective

* Understand how LACP service can be used to agregate multiple network connections
* Learn how to use LACP service to agregate several parallel connections into 1 logical connection

### Completion Time: XZY minutes

## Prerequisites

* Install and run the FRINX ODL distribution
* Install Python 3.6 or higher
* Install FLASK
* Install and run Postman
* Mount 2 routers via Postman environment

For further guidance click on Installation and configuration guide located on top of the page.

## Step 1: Provision the LACP service

After meeting up with all required prerequisites, you should be able to provision the LACP service.  
You can open the Terminal and start the application with following commands:

```
export FLASK_APP=lacp_service.py
flask run
```
Application lacp_service.py exposes really simple and straightforward REST API.  
To provision new LACP service, issue simple POST request:

```
curl --request POST \
  --url http://127.0.0.1:5000/service/new-service \
  --header 'Content-Type: application/json' \
  --data '{\n    "node1": {\n        "name": "xr5",\n        "bundle": "122",\n        "ports": [\n            "GigabitEthernet0/0/0/1",\n            "GigabitEthernet0/0/0/3"\n        ]\n    },\n    "node2": {\n        "name": "xr6",\n        "bundle": "187",\n        "ports": [\n            "GigabitEthernet0/0/0/2"\n        ]\n    }\n}'
```

We can see that lacp_service.py basically translates this POST request into openconfig uniconfig based configuration and provision the service.



# CFK Playground
Playground repo to test different things in Confluent for Kubernetes. As of today, we test:

| **Scenario**                       | **Notes**                                           |
|------------------------------------|-----------------------------------------------------|
| [Connect](./Connect)               | We deploy Connect with additional Connector plugins |
| [SchemaRegistry](./SchemaRegistry) | We want to deploy a schema CR with Data Contracts   |

## Setup
* [Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster using Azure portal](https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-portal?tabs=azure-cli)
* [Confluent for Kubernetes Quick Start](https://docs.confluent.io/operator/current/co-quickstart.html)
* Deploy cluster via `kubectl apply -f ./cluster.yaml -n confluent`

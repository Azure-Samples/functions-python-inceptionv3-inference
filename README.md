---
topic: sample
languages:
    - python
products:
    - azure-functions
author: priyaananthasankar
---

# Image Classification using Tensorflow

This sample uses functions to classify an image from a pretrained Inception V3 model using tensorflow API's

# Getting Started

## Deploy to Azure

### Prerequisites

- Install Python 3.6+
- Install [Functions Core Tools](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local#v2)
- Install Docker
- Note: If run on Windows, use Ubuntu WSL to run deploy script

### Steps

- Click Deploy to Azure Button to deploy resources

[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/)

or

- Deploy through Azure CLI
    - Open AZ CLI and run ```az group create -l [region] -n [resourceGroupName]``` to create a resource group in your Azure subscription (i.e. [region] could be westus2, eastus, etc.)
    - Run ```az group deployment create --name [deploymentName] --resource-group [resourceGroupName] --template-file azuredeploy.json```

- Download pretrained inception V3 model
  - Clone [this](https://github.com/taey16/tf.git) repository and copy classify_image_graph_def.pb from [here](https://github.com/taey16/tf/tree/master/imagenet) to the InceptionV3Classifier folder

- Deploy Function App
  - [Create/Activate virtual environment](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-python#create-and-activate-a-virtual-environment)
  - Run `func azure functionapp publish [functionAppName] --build-native-deps` 

## Test

- Send the following body in a HTTP POST request as a query param
```
http://[functionappname]/api/InceptionV3Classifier?img=[url of image]

```

## Local Testing

For any local testing, use the sample local.settings.json and host.json, create [virtual environment](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-python#create-and-activate-a-virtual-environment) and run `func host start`

## Example

```
http post http://localhost:7071/api/InceptionV3Classifier\?img\="https://www.balisafarimarinepark.com/wp-content/uploads/2017/11/19437535_10154869044788931_4755399083724169206_n-671.jpg"

[
    "tiger, Panthera tigris (score = 0.86580)"
]
```

# References

- [Create your first Python Function](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-python)
- [Tensorflow Tutorials](https://www.tensorflow.org/tutorials/)


---
page_type: sample
languages:
- python
products:
- azure
- azure-functions
description: "This sample uses functions to classify an image from a pretrained Inception V3 model using tensorflow APIs."
azureDeploy: "https://github.com/Azure-Samples/functions-python-inceptionv3-inference/blob/master/azuredeploy.json"
---

# Image Classification using Tensorflow

This sample uses functions to classify an image from a pretrained Inception V3 model using tensorflow API's

## Getting Started

### Deploy to Azure

#### Prerequisites

- Install Python 3.6+
- Install [Functions Core Tools](https://docs.microsoft.com/azure/azure-functions/functions-run-local#v2)
- Install Docker
- Note: If run on Windows, use Ubuntu WSL to run deploy script

#### Steps

- Click Deploy to Azure Button to deploy resources

[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/)

or

- Deploy through Azure CLI
    - Open AZ CLI and run ```az group create -l [region] -n [resourceGroupName]``` to create a resource group in your Azure subscription (i.e. [region] could be westus2, eastus, etc.)
    - Run ```az group deployment create --name [deploymentName] --resource-group [resourceGroupName] --template-file azuredeploy.json```

- Download pretrained inception V3 model
  - Clone [this](https://github.com/taey16/tf.git) repository and copy classify_image_graph_def.pb from [here](https://github.com/taey16/tf/tree/master/imagenet) to the InceptionV3Classifier folder

- Deploy Function App to Azure
  - Run `func azure functionapp publish [functionAppName] --build-native-deps` 

- Local Development
  - Refer links below to create/activate virtual environment for local development

### Test

- Send the following body in a HTTP POST request as a query param

```http
http://[functionappname]/api/InceptionV3Classifier?img=[url of image]
```

### Local Testing

For any local testing, use the sample local.settings.json and host.json, create [virtual environment](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-python#create-and-activate-a-virtual-environment) and run `func host start`

### Example

```http
http post https://[functionappname].azurewebsites.net/api/inceptionv3classifier\?img\=https://www.balisafarimarinepark.com/wp-content/uploads/2017/11/19437535_10154869044788931_4755399083724169206_n-671.jpg

[
    "tiger, Panthera tigris (score = 0.86580)"
]
```

Note: If using Postman, remove the escape characters from the query param of the URL.

## References

- [Create your first Python Function](https://docs.microsoft.com/azure/azure-functions/functions-create-first-function-python)
- [Create/Activate virtual environment](https://docs.microsoft.com/azure/azure-functions/functions-create-first-function-python#create-and-activate-a-virtual-environment)
- [Tensorflow Tutorials](https://www.tensorflow.org/tutorials/)


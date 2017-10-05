---
title: Istanze di contenitore di Azure - Gruppo multicontenitore | Azure Docs
description: Istanze di contenitore di Azure - Gruppo multicontenitore
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 140f58582645ea32f77e901eb13364ed145bbecf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-container-group"></a><span data-ttu-id="0b146-103">Distribuire un gruppo di contenitori</span><span class="sxs-lookup"><span data-stu-id="0b146-103">Deploy a container group</span></span>

<span data-ttu-id="0b146-104">Istanze di contenitore di Azure supporta la distribuzione di più contenitori in un singolo host usando un *gruppo di contenitori*.</span><span class="sxs-lookup"><span data-stu-id="0b146-104">Azure Container Instances support the deployment of multiple containers onto a single host using a *container group*.</span></span> <span data-ttu-id="0b146-105">Ciò è utile quando si compila un contenitore collaterale dell'applicazione per la registrazione, il monitoraggio o qualsiasi altra configurazione in cui un servizio necessita di un secondo processo associato.</span><span class="sxs-lookup"><span data-stu-id="0b146-105">This is useful when building an application sidecar for logging, monitoring, or any other configuration where a service needs a second attached process.</span></span> 

<span data-ttu-id="0b146-106">Questo documento descrive come eseguire una configurazione multicontenitore con contenitore collaterale tramite un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0b146-106">This document walks through running a simple multi-container sidecar configuration using an Azure Resource Manager template.</span></span>

## <a name="configure-the-template"></a><span data-ttu-id="0b146-107">Configurare il modello</span><span class="sxs-lookup"><span data-stu-id="0b146-107">Configure the template</span></span>

<span data-ttu-id="0b146-108">Creare un file denominato `azuredeploy.json` e copiare il codice JSON seguente al suo interno.</span><span class="sxs-lookup"><span data-stu-id="0b146-108">Create a file named `azuredeploy.json` and copy the following json into it.</span></span> 

<span data-ttu-id="0b146-109">In questo esempio viene definito un gruppo di contenitori con due contenitori e un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="0b146-109">In this sample, a container group with two containers and a public IP address is defined.</span></span> <span data-ttu-id="0b146-110">Il primo contenitore del gruppo esegue un'applicazione con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="0b146-110">The first container of the group runs an internet facing application.</span></span> <span data-ttu-id="0b146-111">Il secondo contenitore, ovvero il contenitore collaterale, invia una richiesta HTTP all'applicazione Web principale tramite la rete locale del gruppo.</span><span class="sxs-lookup"><span data-stu-id="0b146-111">The second container, the sidecar, makes an HTTP request to the main web application via the group's local network.</span></span> 

<span data-ttu-id="0b146-112">Questo esempio di contenitore collaterale può essere esteso per attivare un avviso se si riceve un codice di risposta HTTP diverso da 200 OK.</span><span class="sxs-lookup"><span data-stu-id="0b146-112">This sidecar example could be expanded to trigger an alert if it received an HTTP response code other than 200 OK.</span></span> 

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
  },
  "variables": {
    "container1name": "aci-tutorial-app",
    "container1image": "microsoft/aci-helloworld:latest",
    "container2name": "aci-tutorial-sidecar",    
    "container2image": "microsoft/aci-tutorial-sidecar"
  },
    "resources": [
      {
        "name": "myContainerGroup",
        "type": "Microsoft.ContainerInstance/containerGroups",
        "apiVersion": "2017-08-01-preview",
        "location": "[resourceGroup().location]",
        "properties": {
          "containers": [
            {
              "name": "[variables('container1name')]",
              "properties": {
                "image": "[variables('container1image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                },
                "ports": [
                  {
                    "port": 80
                  }
                ]
              }
            },
            {
              "name": "[variables('container2name')]",
              "properties": {
                "image": "[variables('container2image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                }
              }
            }
          ],
          "osType": "Linux",
          "ipAddress": {
            "type": "Public",
            "ports": [
              {
                "protocol": "tcp",
                "port": "80"
              }
            ]
          }
        }
      }
    ],
    "outputs": {
      "containerIPv4Address": {
        "type": "string",
        "value": "[reference(resourceId('Microsoft.ContainerInstance/containerGroups/', 'myContainerGroup')).ipAddress.ip]"
      }
    }
  }
```

<span data-ttu-id="0b146-113">Per usare un registro di immagini del contenitore privato, aggiungere un oggetto al documento JSON con il formato seguente.</span><span class="sxs-lookup"><span data-stu-id="0b146-113">To use a private container image registry, add an object to the json document with the following format.</span></span>

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-the-template"></a><span data-ttu-id="0b146-114">Distribuire il modello</span><span class="sxs-lookup"><span data-stu-id="0b146-114">Deploy the template</span></span>

<span data-ttu-id="0b146-115">Creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0b146-115">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="0b146-116">Distribuire il modello con il comando [az group deployment create](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="0b146-116">Deploy the template with the [az group deployment create](/cli/azure/group/deployment#create) command.</span></span>

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

<span data-ttu-id="0b146-117">Entro pochi secondi si riceverà una risposta iniziale da Azure.</span><span class="sxs-lookup"><span data-stu-id="0b146-117">Within a few seconds, you will receive an initial response from Azure.</span></span> 

## <a name="view-deployment-state"></a><span data-ttu-id="0b146-118">Visualizzare lo stato della distribuzione</span><span class="sxs-lookup"><span data-stu-id="0b146-118">View deployment state</span></span>

<span data-ttu-id="0b146-119">Per visualizzare lo stato della distribuzione, usare il comando `az container show`.</span><span class="sxs-lookup"><span data-stu-id="0b146-119">To view the state of the deployment, use the `az container show` command.</span></span> <span data-ttu-id="0b146-120">Il comando restituisce l'indirizzo IP pubblico con provisioning eseguito su cui è possibile accedere all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0b146-120">This returns the provisioned public IP address over which the application can be accessed.</span></span>

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

<span data-ttu-id="0b146-121">Output:</span><span class="sxs-lookup"><span data-stu-id="0b146-121">Output:</span></span>

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a><span data-ttu-id="0b146-122">Visualizzare i log</span><span class="sxs-lookup"><span data-stu-id="0b146-122">View logs</span></span>   

<span data-ttu-id="0b146-123">Visualizzare l'output del log di un contenitore con il comando `az container logs`.</span><span class="sxs-lookup"><span data-stu-id="0b146-123">View the log output of a container using the `az container logs` command.</span></span> <span data-ttu-id="0b146-124">L'argomento `--container-name` specifica il contenitore da cui effettuare il pull dei log.</span><span class="sxs-lookup"><span data-stu-id="0b146-124">The `--container-name` argument specifies the container from which to pull logs.</span></span> <span data-ttu-id="0b146-125">In questo esempio viene specificato il primo contenitore.</span><span class="sxs-lookup"><span data-stu-id="0b146-125">In this example, the first container is specified.</span></span> 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

<span data-ttu-id="0b146-126">Output:</span><span class="sxs-lookup"><span data-stu-id="0b146-126">Output:</span></span>

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

<span data-ttu-id="0b146-127">Per visualizzare i log per il contenitore collaterale, eseguire lo stesso comando specificando il nome del secondo contenitore.</span><span class="sxs-lookup"><span data-stu-id="0b146-127">To see the logs for the side-car container, run the same command specifying the second container name.</span></span>

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

<span data-ttu-id="0b146-128">Output:</span><span class="sxs-lookup"><span data-stu-id="0b146-128">Output:</span></span>

```bash
Every 3.0s: curl -I http://localhost                                                                                                                       Mon Jul 17 11:27:36 2017

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0  0  1663    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
HTTP/1.1 200 OK
Accept-Ranges: bytes
Content-Length: 1663
Content-Type: text/html; charset=utf-8
Last-Modified: Sun, 16 Jul 2017 02:08:22 GMT
Date: Mon, 17 Jul 2017 18:27:36 GMT
```

<span data-ttu-id="0b146-129">Come si può notare, il contenitore collaterale invia periodicamente una richiesta HTTP all'applicazione Web principale tramite la rete locale del gruppo per verificare che l'applicazione sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0b146-129">As you can see, the sidecar is periodically making an HTTP request to the main web application via the group's local network to ensure that it is running.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b146-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0b146-130">Next steps</span></span>

<span data-ttu-id="0b146-131">In questo documento sono stati illustrati i passaggi necessari per la distribuzione di un'istanza multicontenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b146-131">This document covered the steps needed for deploying a multi-container Azure container instance.</span></span> <span data-ttu-id="0b146-132">Per un'esperienza end-to-end di Istanze di contenitore di Azure, vedere l'apposita esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0b146-132">For an end to end Azure Container Instances experience, see the Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="0b146-133">[Esercitazione su Istanze di contenitore di Azure]: ./container-instances-tutorial-prepare-app.md</span><span class="sxs-lookup"><span data-stu-id="0b146-133">[Azure Container Instances tutorial]: ./container-instances-tutorial-prepare-app.md</span></span>

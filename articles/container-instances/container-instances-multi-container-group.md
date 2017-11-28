---
title: Istanze di contenitori - gruppo multi-contenitore aaaAzure | Documenti di Azure
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
ms.openlocfilehash: 976f578cd2a9bf7f05ab97f24662139bb72062ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-group"></a><span data-ttu-id="28666-103">Distribuire un gruppo di contenitori</span><span class="sxs-lookup"><span data-stu-id="28666-103">Deploy a container group</span></span>

<span data-ttu-id="28666-104">Istanze di contenitore di Azure supporta la distribuzione di hello di più contenitori in un singolo host usando un *gruppo contenitore*.</span><span class="sxs-lookup"><span data-stu-id="28666-104">Azure Container Instances support hello deployment of multiple containers onto a single host using a *container group*.</span></span> <span data-ttu-id="28666-105">Ciò è utile quando si compila un contenitore collaterale dell'applicazione per la registrazione, il monitoraggio o qualsiasi altra configurazione in cui un servizio necessita di un secondo processo associato.</span><span class="sxs-lookup"><span data-stu-id="28666-105">This is useful when building an application sidecar for logging, monitoring, or any other configuration where a service needs a second attached process.</span></span> 

<span data-ttu-id="28666-106">Questo documento descrive come eseguire una configurazione multicontenitore con contenitore collaterale tramite un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="28666-106">This document walks through running a simple multi-container sidecar configuration using an Azure Resource Manager template.</span></span>

## <a name="configure-hello-template"></a><span data-ttu-id="28666-107">Configurare il modello di hello</span><span class="sxs-lookup"><span data-stu-id="28666-107">Configure hello template</span></span>

<span data-ttu-id="28666-108">Creare un file denominato `azuredeploy.json` e hello copia seguendo json al suo interno.</span><span class="sxs-lookup"><span data-stu-id="28666-108">Create a file named `azuredeploy.json` and copy hello following json into it.</span></span> 

<span data-ttu-id="28666-109">In questo esempio viene definito un gruppo di contenitori con due contenitori e un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="28666-109">In this sample, a container group with two containers and a public IP address is defined.</span></span> <span data-ttu-id="28666-110">primo contenitore di Hello del gruppo di hello esegue un'applicazione con connessione internet.</span><span class="sxs-lookup"><span data-stu-id="28666-110">hello first container of hello group runs an internet facing application.</span></span> <span data-ttu-id="28666-111">secondo contenitore Hello, Car hello, rende un'applicazione web principale di HTTP richiesta toohello tramite rete locale del gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="28666-111">hello second container, hello sidecar, makes an HTTP request toohello main web application via hello group's local network.</span></span> 

<span data-ttu-id="28666-112">In questo esempio Car potrebbe essere tootrigger espanso un avviso se ricevuto un codice di risposta HTTP diversi da 200 OK.</span><span class="sxs-lookup"><span data-stu-id="28666-112">This sidecar example could be expanded tootrigger an alert if it received an HTTP response code other than 200 OK.</span></span> 

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

<span data-ttu-id="28666-113">toouse un contenitore privato immagine del Registro di sistema, aggiungere un documento json di oggetti toohello con hello seguente formato.</span><span class="sxs-lookup"><span data-stu-id="28666-113">toouse a private container image registry, add an object toohello json document with hello following format.</span></span>

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a><span data-ttu-id="28666-114">Distribuire il modello di hello</span><span class="sxs-lookup"><span data-stu-id="28666-114">Deploy hello template</span></span>

<span data-ttu-id="28666-115">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="28666-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="28666-116">Distribuire il modello di hello con hello [distribuzione gruppo az creare](/cli/azure/group/deployment#create) comando.</span><span class="sxs-lookup"><span data-stu-id="28666-116">Deploy hello template with hello [az group deployment create](/cli/azure/group/deployment#create) command.</span></span>

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

<span data-ttu-id="28666-117">Entro pochi secondi si riceverà una risposta iniziale da Azure.</span><span class="sxs-lookup"><span data-stu-id="28666-117">Within a few seconds, you will receive an initial response from Azure.</span></span> 

## <a name="view-deployment-state"></a><span data-ttu-id="28666-118">Visualizzare lo stato della distribuzione</span><span class="sxs-lookup"><span data-stu-id="28666-118">View deployment state</span></span>

<span data-ttu-id="28666-119">stato hello tooview hello della distribuzione di, utilizzare hello `az container show` comando.</span><span class="sxs-lookup"><span data-stu-id="28666-119">tooview hello state of hello deployment, use hello `az container show` command.</span></span> <span data-ttu-id="28666-120">Restituisce l'indirizzo IP pubblico hello provisioning su quale hello è possibile accedere all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="28666-120">This returns hello provisioned public IP address over which hello application can be accessed.</span></span>

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

<span data-ttu-id="28666-121">Output:</span><span class="sxs-lookup"><span data-stu-id="28666-121">Output:</span></span>

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a><span data-ttu-id="28666-122">Visualizzare i log</span><span class="sxs-lookup"><span data-stu-id="28666-122">View logs</span></span>   

<span data-ttu-id="28666-123">Visualizzare l'output del log di un contenitore utilizzando hello hello `az container logs` comando.</span><span class="sxs-lookup"><span data-stu-id="28666-123">View hello log output of a container using hello `az container logs` command.</span></span> <span data-ttu-id="28666-124">Hello `--container-name` argomento specifica contenitore hello dai quali registri toopull.</span><span class="sxs-lookup"><span data-stu-id="28666-124">hello `--container-name` argument specifies hello container from which toopull logs.</span></span> <span data-ttu-id="28666-125">In questo esempio viene specificato il primo contenitore di hello.</span><span class="sxs-lookup"><span data-stu-id="28666-125">In this example, hello first container is specified.</span></span> 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

<span data-ttu-id="28666-126">Output:</span><span class="sxs-lookup"><span data-stu-id="28666-126">Output:</span></span>

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

<span data-ttu-id="28666-127">hello toosee registri per il contenitore di lato car hello, eseguire hello specificando hello secondo nome del contenitore stesso comando.</span><span class="sxs-lookup"><span data-stu-id="28666-127">toosee hello logs for hello side-car container, run hello same command specifying hello second container name.</span></span>

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

<span data-ttu-id="28666-128">Output:</span><span class="sxs-lookup"><span data-stu-id="28666-128">Output:</span></span>

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

<span data-ttu-id="28666-129">Come si può notare, Car hello periodicamente esegue un'applicazione web principale di HTTP richiesta toohello tramite tooensure di rete locale del gruppo di hello in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="28666-129">As you can see, hello sidecar is periodically making an HTTP request toohello main web application via hello group's local network tooensure that it is running.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28666-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="28666-130">Next steps</span></span>

<span data-ttu-id="28666-131">Questo documento coperto passaggi hello necessari per la distribuzione di un multi-contenitore di istanza del contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="28666-131">This document covered hello steps needed for deploying a multi-container Azure container instance.</span></span> <span data-ttu-id="28666-132">Per un fine tooend che esperienza di istanze di contenitori di Azure, vedere l'esercitazione di istanze di contenitori di Azure di hello.</span><span class="sxs-lookup"><span data-stu-id="28666-132">For an end tooend Azure Container Instances experience, see hello Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="28666-133">[Esercitazione su Istanze di contenitore di Azure]: ./container-instances-tutorial-prepare-app.md</span><span class="sxs-lookup"><span data-stu-id="28666-133">[Azure Container Instances tutorial]: ./container-instances-tutorial-prepare-app.md</span></span>

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
# <a name="deploy-a-container-group"></a>Distribuire un gruppo di contenitori

Istanze di contenitore di Azure supporta la distribuzione di hello di più contenitori in un singolo host usando un *gruppo contenitore*. Ciò è utile quando si compila un contenitore collaterale dell'applicazione per la registrazione, il monitoraggio o qualsiasi altra configurazione in cui un servizio necessita di un secondo processo associato. 

Questo documento descrive come eseguire una configurazione multicontenitore con contenitore collaterale tramite un modello di Azure Resource Manager.

## <a name="configure-hello-template"></a>Configurare il modello di hello

Creare un file denominato `azuredeploy.json` e hello copia seguendo json al suo interno. 

In questo esempio viene definito un gruppo di contenitori con due contenitori e un indirizzo IP pubblico. primo contenitore di Hello del gruppo di hello esegue un'applicazione con connessione internet. secondo contenitore Hello, Car hello, rende un'applicazione web principale di HTTP richiesta toohello tramite rete locale del gruppo di hello. 

In questo esempio Car potrebbe essere tootrigger espanso un avviso se ricevuto un codice di risposta HTTP diversi da 200 OK. 

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

toouse un contenitore privato immagine del Registro di sistema, aggiungere un documento json di oggetti toohello con hello seguente formato.

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a>Distribuire il modello di hello

Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

Distribuire il modello di hello con hello [distribuzione gruppo az creare](/cli/azure/group/deployment#create) comando.

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

Entro pochi secondi si riceverà una risposta iniziale da Azure. 

## <a name="view-deployment-state"></a>Visualizzare lo stato della distribuzione

stato hello tooview hello della distribuzione di, utilizzare hello `az container show` comando. Restituisce l'indirizzo IP pubblico hello provisioning su quale hello è possibile accedere all'applicazione.

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

Output:

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a>Visualizzare i log   

Visualizzare l'output del log di un contenitore utilizzando hello hello `az container logs` comando. Hello `--container-name` argomento specifica contenitore hello dai quali registri toopull. In questo esempio viene specificato il primo contenitore di hello. 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

Output:

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

hello toosee registri per il contenitore di lato car hello, eseguire hello specificando hello secondo nome del contenitore stesso comando.

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

Output:

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

Come si può notare, Car hello periodicamente esegue un'applicazione web principale di HTTP richiesta toohello tramite tooensure di rete locale del gruppo di hello in fase di esecuzione.

## <a name="next-steps"></a>Passaggi successivi

Questo documento coperto passaggi hello necessari per la distribuzione di un multi-contenitore di istanza del contenitore di Azure. Per un fine tooend che esperienza di istanze di contenitori di Azure, vedere l'esercitazione di istanze di contenitori di Azure di hello.

> [!div class="nextstepaction"]
> [Esercitazione su Istanze di contenitore di Azure]: ./container-instances-tutorial-prepare-app.md

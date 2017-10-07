---
title: esercitazione per istanze di contenitori aaaAzure - distribuire app | Documenti Microsoft
description: Esercitazione di Istanze di contenitore di Azure - Distribuire un'app
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a>Distribuire un tooAzure contenitore istanze di contenitori

Si tratta di hello ultimo di un'esercitazione in tre parti. Nelle sezioni precedenti, [è stata creata un'immagine contenitore](container-instances-tutorial-prepare-app.md) e [inserito tooan del Registro di sistema di Azure contenitore](container-instances-tutorial-prepare-acr.md). In questa sezione viene completata l'esercitazione hello distribuendo hello contenitore tooAzure istanze di contenitori. I passaggi completati comprendono:

> [!div class="checklist"]
> * Definizione di un gruppo di contenitori usando un modello di Azure Resource Manager
> * Distribuzione di gruppo contenitore hello utilizzando hello CLI di Azure
> * Visualizzare i log dei contenitori

## <a name="deploy-hello-container-using-hello-azure-cli"></a>Distribuire il contenitore di hello utilizzando hello CLI di Azure

Hello CLI di Azure consente la distribuzione di un contenitore tooAzure istanze di contenitori, in un unico comando. Poiché l'immagine contenitore hello è ospitato in hello privato del Registro di sistema contenitore di Azure, è necessario includere tooaccess necessarie le credenziali di hello è. Se necessario, è possibile trovarle con una query come illustrato di seguito.

Server di accesso del registro contenitori (sostituire con il nome del registro):

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

Password del registro contenitori:

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

toodeploy immagine contenitore dal Registro di sistema di hello contenitore con una risorsa richiesta di 1 core CPU e 1GB di memoria, eseguire hello comando seguente:

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

Entro pochi secondi si riceverà una risposta iniziale da Azure Resource Manager. stato di hello tooview hello della distribuzione di, utilizzare:

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

È possibile continuare a eseguire questo comando fino a quando non hello stato cambia da *in sospeso* troppo*esecuzione*. Sarà quindi possibile procedere.

## <a name="view-hello-application-and-container-logs"></a>Visualizzare i log dell'applicazione e il contenitore di hello

Al termine della distribuzione di hello, aprire l'indirizzo IP di toohello browser illustrato nell'output di hello di hello comando seguente:

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Hello world app nel browser hello][aci-app-browser]

È inoltre possibile visualizzare l'output del log del contenitore hello hello:

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

Output:

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, il processo di hello distribuire le istanze di contenitori di tooAzure contenitori è completato. sono stata completata Hello alla procedura seguente:

> [!div class="checklist"]
> * Distribuzione di contenitore hello dall'utilizzo del Registro di sistema di Azure contenitore hello hello CLI di Azure
> * Visualizzazione di un'applicazione hello in browser hello
> * Visualizzazione dei log di contenitore hello

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png

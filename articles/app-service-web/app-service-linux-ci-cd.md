---
title: Distribuzione con App Web di Azure in Linux aaaContinuous | Documenti Microsoft
description: Come la distribuzione continua toosetup nell'App Web di Azure in Linux.
keywords: servizio app di azure, linux, oss, acr
services: app-service
documentationcenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: f94d837e27605da58428f507ab2b0eb3af3297e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a>Distribuzione continua con App Web di Azure in Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

In questa esercitazione si configura la distribuzione continua per un'immagine personalizzata del contenitore da repository del [Registro contenitori di Azure](https://azure.microsoft.com/en-us/services/container-registry/) o dall'[hub Docker](https://hub.docker.com).

## <a name="step-1---sign-in-tooazure"></a>Passaggio 1 - Sign in tooAzure

Accedi toohello portale di Azure all'indirizzo http://portal.azure.com

## <a name="step-2---enable-container-continuous-deployment-feature"></a>Passaggio 2: Abilitare la funzionalità di distribuzione continua del contenitore

È possibile abilitare funzionalità di distribuzione continua hello mediante [CLI di Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) e l'esecuzione di hello comando seguente

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

In hello  **[portale di Azure](https://portal.azure.com/)**, fare clic su hello **servizio App** opzione a sinistra di hello della pagina hello.

Fare clic sul nome hello dell'app che si desidera tooconfigure Hub Docker la distribuzione continua per.

In hello **impostazioni App**, aggiungere un'app denominata `DOCKER_ENABLE_CI` con valore hello `true`.

![inserire l'immagine dell'impostazione dell'app](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a>Passaggio 3 - Preparare l'URL webhook

È possibile ottenere utilizzando URL del Webhook hello [CLI di Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) e l'esecuzione di hello comando seguente

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

Per l'URL del Webhook hello, è necessario hello toohave seguenti endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.

È possibile ottenere il `publishingusername` e `publishingpwd` scaricando hello web app pubblicare profilo utilizzando hello portale di Azure.

![inserire l'immagine dell'aggiunta del webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a>Passaggio 4 - Aggiungere un webhook

### <a name="azure-container-registry"></a>Registro di sistema del contenitore di Azure

Nel pannello del portale del registro fare clic su **Webhook** e creare un nuovo webhook facendo clic su **Aggiungi**. In hello **creare webhook** pannello, denominare il webhook. Per hello Webhook URI, è necessario tooprovide hello URL ottenuto dal **passaggio 3**

Assicurarsi che ambito hello è definito come hello repository che contiene l'immagine del contenitore.

![inserimento dell'immagine del webhhok](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

Quando viene aggiornata l'immagine di hello, hello web app aggiornata automaticamente con una nuova immagine hello.

### <a name="docker-hub"></a>Hub Docker

Nella pagina Hub Docker, fare clic su **Webhook**, quindi **CREATE A WEBHOOK** (CREA UN WEBHOOK).

![inserire l'immagine dell'aggiunta del webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

Per l'URL del Webhook hello, è necessario tooprovide hello URL ottenuto dal **passaggio 3**

![inserire l'immagine dell'aggiunta del webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

Quando viene aggiornata l'immagine di hello, hello web app aggiornata automaticamente con una nuova immagine hello.

## <a name="next-steps"></a>Passaggi successivi
* [Definizione di App Web di Azure in Linux](./app-service-linux-intro.md)
* [Registro contenitori di Azure](https://azure.microsoft.com/en-us/services/container-registry/)
* [Uso della configurazione PM2 per Node.js in App Web su Linux](app-service-linux-using-nodejs-pm2.md)
* [Uso di .NET Core in App Web di Azure in Linux](app-service-linux-using-dotnetcore.md)
* [Uso di Ruby in App Web di Azure in Linux](app-service-linux-ruby-get-started.md)
* [Come immagine di toouse una Docker personalizzata per l'App Web di Azure in Linux](./app-service-linux-using-custom-docker-image.md)
* [Domande frequenti su App Web del Servizio app di Azure su Linux](./app-service-linux-faq.md) 
* [Gestire App Web in Linux tramite interfaccia della riga di comando di Azure 2.0](./app-service-linux-cli.md)




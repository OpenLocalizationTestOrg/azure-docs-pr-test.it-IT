---
title: App Web in Linux con Azure CLI 2.0 aaaManage | Documenti Microsoft
description: Gestire App Web in Linux tramite interfaccia della riga di comando di Azure.
keywords: servizio app di Azure, app Web, interfaccia della riga di comando, domande frequenti, linux, oss
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 5e8e0da8a362450c56d2e87e087f77598ec874ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a>Gestire App Web in Linux tramite interfaccia della riga di comando di Azure

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

Utilizzando i comandi di hello in questo articolo sono in grado di toocreate e gestire un'App Web in Linux con CLI di Azure 2.0.
È possibile iniziare a utilizzare hello nuova versione di hello CLI in due modi:

* [Installare l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) sul computer.
* Utilizzare [Azure Cloud Shell (anteprima)](../cloud-shell/overview.md)


## <a name="create-a-linux-app-service-plan"></a>Creare un nuovo piano di servizio app

toocreate un piano di servizio a Linux App, è possibile utilizzare hello comando seguente:

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a>Creare un contenitore Docker personalizzato App Web

toocreate un'app web e configurarlo toorun contenitore Docker personalizzato, è possibile utilizzare hello comando seguente:

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a>Attivare la registrazione di contenitore Docker hello

tooactivate hello registrazione contenitore Docker, è possibile usare hello comando seguente:

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a>Modifica contenitore Docker personalizzata hello per un'App Web esistente in App di Linux

toochange un'app creata in precedenza, da hello corrente Docker immagine tooa nuova immagine, è possibile utilizzare hello comando seguente:

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a>Utilizzo di immagini Docker da un registro privato

È possibile configurare delle immagini dell'app toouse un registro di sistema privato. È necessario tooprovide hello url per il Registro di sistema, un nome utente e password. Questa operazione può essere eseguita mediante hello comando seguente:

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a>Abilitare la distribuzione continua per le immagini Docker personalizzate

Con hello comando seguente è possibile abilitare la funzionalità CD hello e ottenere l'url del webhook hello. Questo url può essere utilizzato tooconfigure si repository DockerHub o del Registro di sistema contenitore di Azure.

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a>Creare un'App Web in App di Linux usando uno dei nostri Framework di runtime integrati

toocreate un'App Web di PHP 5.6 sull'App di Linux, è possibile utilizzare hello comando seguente.

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a>Modificare la versione del framework per un'App Web esistente in App di Linux

toochange un'app creata in precedenza, da hello corrente framework versione tooNode.js 6.11, è possibile utilizzare hello comando seguente:

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a>Configurare le distribuzioni Git per l'App Web

tooset le distribuzioni Git per l'app, è possibile utilizzare hello comando seguente:

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a>Passaggi successivi
* [Definizione di App Web di Azure in Linux](app-service-linux-intro.md)
* [Installare l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [Azure Cloud Shell (anteprima)](../cloud-shell/overview.md)
* [Configurare gli ambienti di gestione temporanea nel Servizio app di Azure](./web-sites-staged-publishing.md)
* [Distribuzione continua con App Web di Azure in Linux](./app-service-linux-ci-cd.md)

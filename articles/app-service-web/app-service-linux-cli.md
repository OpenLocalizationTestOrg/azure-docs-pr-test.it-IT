---
title: Gestire App Web in Linux tramite interfaccia della riga di comando di Azure 2.0| Microsoft Docs
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
ms.openlocfilehash: 04aceecf0cb4cad5c838b7254bf7079a36bbd0d8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a>Gestire App Web in Linux tramite interfaccia della riga di comando di Azure

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

Utilizzando i comandi in questo articolo si è in grado di creare e gestire un'App Web in Linux con interfaccia della riga di comando di Azure 2.0.
È possibile iniziare a usare la nuova versione dell'interfaccia della riga di comando in due modi:

* [Installare l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) sul computer.
* Utilizzare [Azure Cloud Shell (anteprima)](../cloud-shell/overview.md)


## <a name="create-a-linux-app-service-plan"></a>Creare un nuovo piano di servizio app

Per creare un piano di servizio app Linux, è possibile utilizzare il comando seguente:

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a>Creare un contenitore Docker personalizzato App Web

Per creare un'app Web e configurarla per l'esecuzione di un contenitore Docker personalizzato, è possibile utilizzare il comando seguente:

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-the-docker-container-logging"></a>Attivare la registrazione del contenitore Docker

Per attivare la registrazione del contenitore Docker è possibile usare il comando seguente:

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-the-custom-docker-container-for-an-existing-web-app-on-linux-app"></a>Modificare il contenitore Docker personalizzato per un'App Web esistente in App di Linux

Per modificare un'app creata in precedenza, dall'immagine del Docker attuale a una nuova immagine, è possibile utilizzare il comando seguente:

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a>Utilizzo di immagini Docker da un registro privato

È possibile configurare l'app per utilizzare le immagini da un registro di sistema privato. È necessario specificare l'url per il Registro di sistema, nome utente e password. È possibile fare ciò utilizzando il comando seguente:

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a>Abilitare la distribuzione continua per le immagini Docker personalizzate

Con il comando seguente è possibile abilitare la funzionalità CD e ottenere l'url del webhook. Questo url consente di configurare il repository DockerHub o del Registro contenitori di Azure.

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a>Creare un'App Web in App di Linux usando uno dei nostri Framework di runtime integrati

Per creare un'App Web di PHP 5.6 sull'App di Linux, è possibile utilizzare il comando seguente.

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a>Modificare la versione del framework per un'App Web esistente in App di Linux

Per modificare un'applicazione creata in precedenza, dalla versione del framework corrente a Node.js 6.11, è possibile utilizzare il comando seguente:

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a>Configurare le distribuzioni Git per l'App Web

Per configurare le distribuzioni Git per l'app, è possibile utilizzare il comando seguente:

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a>Passaggi successivi
* [Definizione di App Web di Azure in Linux](app-service-linux-intro.md)
* [Installare l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [Azure Cloud Shell (anteprima)](../cloud-shell/overview.md)
* [Configurare gli ambienti di gestione temporanea nel Servizio app di Azure](./web-sites-staged-publishing.md)
* [Distribuzione continua con App Web di Azure in Linux](./app-service-linux-ci-cd.md)

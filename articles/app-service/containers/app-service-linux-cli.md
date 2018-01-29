---
title: Gestire l'app Web per i contenitori tramite l'interfaccia della riga di comando di Azure 2.0 | Microsoft Docs
description: Gestire l'app Web per i contenitori tramite l'interfaccia della riga di comando di Azure.
keywords: servizio app di Azure, app Web, interfaccia della riga di comando, domande frequenti, linux, oss
services: app-service
documentationCenter: 
author: ahmedelnably
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 54c979313a6ffa43008aa9870332b92d2b2f182a
ms.sourcegitcommit: bc8d39fa83b3c4a66457fba007d215bccd8be985
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/10/2017
---
# <a name="manage-web-app-for-containers-using-azure-cli"></a>Gestire l'app Web per i contenitori tramite l'interfaccia della riga di comando di Azure

Usando i comandi in questo articolo si è in grado di creare e gestire un'app Web per i contenitori con l'interfaccia della riga di comando di Azure 2.0.
È possibile iniziare a usare la nuova versione dell'interfaccia della riga di comando in due modi:

* [Installare l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) sul computer.
* Utilizzare [Azure Cloud Shell (anteprima)](../../cloud-shell/overview.md)

## <a name="create-a-linux-app-service-plan"></a>Creare un nuovo piano di servizio app

Per creare un piano di servizio app Linux, è possibile utilizzare il comando seguente:

```azurecli-interactive
az appservice plan create -n appname -g rgname --is-linux -l "South Central US" --sku S1 --number-of-workers 1
```

## <a name="create-a-custom-docker-container-web-app"></a>Creare un'app Web per contenitore Docker personalizzato

Per creare un'app Web e configurarla per l'esecuzione di un contenitore Docker personalizzato, è possibile utilizzare il comando seguente:

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```

## <a name="activate-the-docker-container-logging"></a>Attivare la registrazione del contenitore Docker

Per attivare la registrazione del contenitore Docker è possibile usare il comando seguente:

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```

## <a name="change-the-custom-docker-container-for-an-existing-web-app-for-containers-app"></a>Cambiare il contenitore Docker personalizzato per un'app Web per i contenitori esistente

Per modificare un'app creata in precedenza, dall'immagine del Docker attuale a una nuova immagine, è possibile utilizzare il comando seguente:

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
```

## <a name="using-docker-images-from-a-private-registry"></a>Utilizzo di immagini Docker da un registro privato

È possibile configurare l'app per utilizzare le immagini da un registro di sistema privato. È necessario specificare l'URL per il Registro di sistema, nome utente e password. È possibile fare ciò utilizzando il comando seguente:

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
```

## <a name="enable-continuous-deployments-for-custom-docker-images"></a>Abilitare la distribuzione continua per le immagini Docker personalizzate

Con il comando seguente è possibile abilitare la funzionalità CD e ottenere l'url del webhook. Questo URL consente di configurare i repository DockerHub o registro contenitori di Azure.

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
```

## <a name="create-a-web-app-for-containers-app-using-one-of-our-built-in-runtime-frameworks"></a>Creare un'app Web per i contenitori usando uno dei nostri Framework di runtime integrati

Per creare un'app Web per i contenitori PHP 5.6, è possibile usare il comando seguente.

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
```

## <a name="change-framework-version-for-an-existing-web-app-for-containers-app"></a>Modificare la versione del framework per un'App Web esistente in app per i contenitori

Per modificare un'applicazione creata in precedenza, dalla versione del framework corrente a Node.js 6.11, è possibile utilizzare il comando seguente:

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
```

## <a name="set-up-git-deployments-for-your-web-app"></a>Configurare le distribuzioni Git per l'app Web

Per configurare le distribuzioni Git per l'app, è possibile utilizzare il comando seguente:

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
```

## <a name="next-steps"></a>Passaggi successivi

* [Che cos'è il Servizio app di Azure in Linux?](app-service-linux-intro.md)
* [Installare l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)
* [Azure Cloud Shell (anteprima)](../../cloud-shell/overview.md)
* [Configurare gli ambienti di gestione temporanea nel Servizio app di Azure](../../app-service/web-sites-staged-publishing.md?toc=%2fazure%2fapp-service%2fcontainers%2ftoc.json)
* [Distribuzione continua con l'app Web per contenitori](app-service-linux-ci-cd.md)

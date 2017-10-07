---
title: esercitazione per il servizio contenitore aaaAzure - preparare App | Documenti Microsoft
description: Esercitazione sul servizio contenitore di Azure - App di preparazione
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenitori, Micro-Service, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b537ecc9ff50358fb65b128bfe6eb894dd088cc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-images-toobe-used-with-azure-container-service"></a>Crea contenitore immagini toobe utilizzato con il servizio contenitore di Azure

In questa esercitazione, parte uno di sette, si prepara un'applicazione multi-contenitore per l'uso in Kubernetes. I passaggi completati comprendono:  

> [!div class="checklist"]
> * Clonazione dell'origine applicazione da GitHub  
> * Creazione di un'immagine contenitore dall'origine di applicazione hello
> * Test di un'applicazione hello in un ambiente locale in Docker

Una volta completato, dopo l'applicazione hello è accessibile in ambiente di sviluppo locale.

![Immagine del cluster Kubernetes in Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

Nelle esercitazioni successive, immagine contenitore hello è caricato tooan del Registro di sistema di Azure contenitore e quindi eseguiti in un Azure ospitati Kubernetes cluster.

## <a name="before-you-begin"></a>Prima di iniziare

Questa esercitazione presuppone una conoscenza di base dei concetti principali di Docker, come contenitori, immagini dei contenitore e comandi essenziali. Se necessario, vedere [Introduzione a Docker]( https://docs.docker.com/get-started/) per una panoramica sui concetti fondamentali relativi al contenitore. 

toocomplete questa esercitazione, è necessario un ambiente di sviluppo di Docker. Docker offre pacchetti che consentono di configurare facilmente Docker in qualsiasi sistema [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) o [Linux](https://docs.docker.com/engine/installation/#supported-platforms).

## <a name="get-application-code"></a>Ottenere il codice dell'applicazione

applicazione di esempio Hello utilizzata in questa esercitazione è un'app di voto base. un'applicazione Hello è costituito da un componente front-end web e un'istanza di Redis back-end. il componente web Hello viene compresso in un'immagine contenitore personalizzato. istanza di Redis Hello utilizza un'immagine dall'Hub Docker non modificata.  

Usare git toodownload una copia dell'ambiente di sviluppo tooyour applicazione hello.

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Un creato in precedenza Docker compose di file e un file manifesto Kubernetes interno hello clonato directory è codice sorgente dell'applicazione hello. Questi file sono utilizzati toocreate asset nel set di esercitazione hello. 

## <a name="create-container-images"></a>Creare immagini del contenitore

[Docker Compose](https://docs.docker.com/compose/) può essere utilizzato tooautomate hello compilazione fuori immagini contenitore e la distribuzione di hello di applicazioni multi-contenitore.

Eseguire l'immagine di docker compose.yml file toocreate hello contenitore hello, hello download Redis immagine e avviare un'applicazione hello.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

Al termine, utilizzare hello [immagini docker](https://docs.docker.com/engine/reference/commandline/images/) comando immagini hello creato toosee.

```bash
docker images
```

Si noti che sono state scaricate o create tre immagini. Hello *azure voto-anteriore* immagine contiene un'applicazione hello. È stata derivata da hello *nginx pallone* immagine. immagine di Redis Hello è stato scaricato dall'Hub Docker.

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

Eseguire hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) comando toosee hello contenitori in esecuzione.

```bash
docker ps
```

Output:

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a>Testare l'applicazione in locale

Sfoglia toohttp://localhost:8080 toosee hello in esecuzione dell'applicazione.

![Immagine del cluster Kubernetes in Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a>Pulire le risorse

Ora che la funzionalità dell'applicazione è stata convalidata, hello contenitori in esecuzione può essere arrestato e rimosso. Non eliminare le immagini contenitore hello. Hello *azure voto-anteriore* immagine è l'istanza del Registro di sistema di Azure contenitore tooan caricato nella prossima esercitazione hello.

Eseguire hello seguente hello toostop contenitori in esecuzione.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

Eliminare i contenitori di hello arrestato con hello comando seguente.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

Al termine, si dispone di un'immagine contenitore che contiene un'applicazione hello Azure voto.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, un'applicazione è stata testata e le immagini contenitore creato per un'applicazione hello. sono stata completata Hello alla procedura seguente:

> [!div class="checklist"]
> * La clonazione di origine dell'applicazione hello da GitHub  
> * Creazione di un'immagine del contenitore dall'origine applicazione
> * Applicazione hello testata in un ambiente locale in Docker

Spostare toohello Avanti toolearn esercitazione sull'archiviazione di immagini contenitore in un registro di sistema di contenitore di Azure.

> [!div class="nextstepaction"]
> [Push tooAzure immagini contenitore del Registro di sistema](./container-service-tutorial-kubernetes-prepare-acr.md)

---
title: Azure Swarm aaaManage cluster con l'API di Docker | Documenti Microsoft
description: Distribuire cluster contenitori Docker Swarm tooa contenitore nel servizio di Azure
services: container-service
documentationcenter: 
author: rgardler
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: Docker, Contenitori, Micro-servizi, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: bb9b07c82a7b48caeb2e351455797cbf2a6e7480
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="container-management-with-docker-swarm"></a>Gestione dei contenitori con Docker Swarm
Docker Swarm offre un ambiente per la distribuzione di carichi di lavoro in contenitori in un set di host Docker in pool. Docker sciame utilizza API di Docker native hello. flusso di lavoro di Hello per la gestione dei contenitori in un Docker Swarm è quasi identica toowhat che sarebbe in un singolo host contenitore. Questo documento fornisce semplici esempi di distribuzione di carichi di lavoro in contenitori, in un'istanza del servizio contenitore di Azure di Docker Swarm. Per una documentazione più dettagliata su Docker Swarm, vedere [Docker Swarm in Docker.com](https://docs.docker.com/swarm/).

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

Prerequisiti toohello gli esercizi di questo documento:

[Creare un cluster Swarm nel servizio contenitore di Azure](container-service-deployment.md)

[Connettersi con cluster sciame hello contenitore nel servizio di Azure](../container-service-connect.md)

## <a name="deploy-a-new-container"></a>Distribuire un nuovo contenitore
un nuovo contenitore di hello Docker Swarm, toocreate utilizzare hello `docker run` comando (assicurandosi che è stato aperto un master di toohello tunnel SSH in base ai prerequisiti hello sopra). In questo esempio crea un contenitore da hello `yeasy/simple-web` immagine:

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

Dopo aver creato il contenitore di hello, utilizzare `docker ps` tooreturn informazioni contenitore hello. Notare che l'agente sciame hello host contenitore hello è elencato:

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

È ora possibile accedere a un'applicazione hello che è in esecuzione in questo contenitore tramite nome DNS pubblico hello di bilanciamento del carico di hello sciame agente. È possibile trovare queste informazioni nel portale di Azure hello:  

![Risultati della visita reali](./media/container-service-docker-swarm/real-visit.jpg)  

Per impostazione predefinita hello bilanciamento del carico con porte 80, aperta 8080 e 443. Se si desidera tooconnect su un'altra porta occorre tooopen tale porta in hello bilanciamento del carico di Azure per hello Pool di agenti.

## <a name="deploy-multiple-containers"></a>Distribuire più contenitori
Più contenitori vengono avviati, tramite l'esecuzione di 'docker run' più volte, è possibile utilizzare hello `docker ps` toosee comando che ospita i contenitori di hello eseguono. Nell'esempio hello seguente, tre contenitori vengono distribuiti uniformemente tra tre agenti di sciame hello:  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a>Distribuire contenitori con Docker Compose
È possibile utilizzare Docker Compose tooautomate hello distribuzione e configurazione di più contenitori. toodo in tal caso, verificare che è stato creato un tunnel SSH (Secure Shell) e che è stata impostata la variabile DOCKER_HOST hello (vedere hello i prerequisiti sopra).

Creare un file docker-compose.yml nel sistema locale. toodo, utilizzare questo [esempio](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).

```bash
web:
  image: adtd/web:0.1
  ports:
    - "80:80"
  links:
    - rest:rest-demo-azure.marathon.mesos
rest:
  image: adtd/rest:0.1
  ports:
    - "8080:8080"

```

Eseguire `docker-compose up -d` toostart le distribuzioni di contenitori hello:

```bash
user@ubuntu:~/compose$ docker-compose up -d
Pulling rest (adtd/rest:0.1)...
swarm-agent-3B7093B8-0: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-3: Pulling adtd/rest:0.1... : downloaded
Creating compose_rest_1
Pulling web (adtd/web:0.1)...
swarm-agent-3B7093B8-3: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-0: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/web:0.1... : downloaded
Creating compose_web_1
```

Infine, verrà restituito hello elenco di contenitori in esecuzione. Questo elenco contiene contenitori hello che sono stati distribuiti tramite Docker Compose:

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

Naturalmente, è possibile utilizzare `docker-compose ps` tooexamine hello solo contenitori definiti nel `compose.yml` file.

## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni su Docker Swarm](https://docs.docker.com/swarm/)


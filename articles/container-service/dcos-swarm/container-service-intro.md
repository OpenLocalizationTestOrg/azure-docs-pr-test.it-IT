---
title: aaaDocker contenitore hosting nel cloud di Azure | Documenti Microsoft
description: Il servizio contenitore di Azure fornisce un modo toosimplify hello creazione, configurazione e gestione di un cluster di macchine virtuali che sono preconfigurati toorun contenitore applicazioni.
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Contenitori, Micro-servizi, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 46a0071a7497a3ff44d75413b49f1d06f844c446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodocker-container-hosting-solutions-with-azure-container-service"></a>Introduzione tooDocker contenitore soluzioni con il servizio contenitore di Azure 
Il servizio contenitore di Azure, è più semplice per l'utente toocreate, configurare e gestire un cluster di macchine virtuali che sono preconfigurati toorun contenitore applicazioni. Usa una configurazione ottimizzata di strumenti di pianificazione e orchestrazione open source comuni. Questo consente di toouse le competenze esistenti, o disegnare su un corpo di grandi dimensioni e in continua crescito di esperienza della community, toodeploy e gestire le applicazioni basate sul contenitore in Microsoft Azure.

![Il servizio contenitore di Azure fornisce un mezzo toomanage contenitore applicazioni su più host in Azure.](./media/acs-intro/acs-cluster-new.png)

Il servizio contenitore Azure sfrutta tooensure formato contenitore Docker di hello che i contenitori di applicazioni siano completamente portabili. Supporta inoltre la scelta di maratona e controller di dominio o del sistema operativo, Docker Swarm o Kubernetes in modo da poter ridimensionare toothousands queste applicazioni di contenitori o persino decine di migliaia.

Tramite il servizio contenitore di Azure, è possibile sfruttare le funzionalità di livello aziendale di Azure, mantenendo al tempo stesso la portabilità dell'applicazione, tra cui portabilità in livelli di orchestrazione hello.

## <a name="using-azure-container-service"></a>Utilizzo del servizio contenitore di Azure
L'obiettivo di Microsoft con il servizio contenitore di Azure è tooprovide un ambiente host del contenitore tramite strumenti open source e tecnologie che sono comuni tra i clienti oggi. toothis fine, è necessario esporre gli endpoint dell'API standard hello per le scelte orchestrator (controller di dominio o del sistema operativo, Docker Swarm o Kubernetes). Tramite questi endpoint, è possibile utilizzare qualsiasi software che è in grado di comunicare con gli endpoint toothose. Ad esempio, nel caso di hello di endpoint di Docker Swarm hello, è possibile scegliere l'interfaccia della riga di comando toouse hello Docker (CLI). Per i controller di dominio o del sistema operativo, è possibile scegliere hello DCOS CLI. Per Kubernetes, è possibile scegliere `kubectl`.

## <a name="creating-a-docker-cluster-by-using-azure-container-service"></a>Creazione di un cluster Docker con il servizio contenitore di Azure
toobegin mediante il servizio contenitore di Azure, si distribuisce un cluster il servizio contenitore di Azure tramite il portale di hello (hello ricerca Marketplace per **servizio contenitore di Azure**), utilizzando un modello di gestione risorse di Azure ([Docker Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm), [DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), o [Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)), o con hello [CLI di Azure 2.0](container-service-create-acs-cluster-cli.md). modelli di avvio rapido possono essere modificato tooinclude aggiuntive o avanzate configurazione di Azure Hello. Per altre informazioni, vedere [Distribuire un cluster del servizio contenitore di Azure](container-service-deployment.md).

## <a name="deploying-an-application"></a>Distribuzione di un'applicazione
Il servizio contenitore di Azure consente di scegliere tra Docker Swarm, DC/OS o Kubernetes per l'orchestrazione. La modalità di distribuzione dell'applicazione dipende dall'agente di orchestrazione scelto.

### <a name="using-dcos"></a>Uso di DC/OS
Controller di dominio o sistema operativo è un sistema operativo distribuito basato sul kernel di sistemi distribuiti Apache Mesos hello. Apache Mesos si trova in hello Apache Software Foundation e vengono elencate alcune delle hello [protagonisti in IT](http://mesos.apache.org/documentation/latest/powered-by-mesos/) come utenti e collaboratori.

![Servizio contenitore di Azure configurato per DC/OS che mostra agenti e schemi.](media/acs-intro/dcos.png)

DC/OS e Apache Mesos offrono un set di funzionalità molto ampio:

* Scalabilità collaudata
* Schemi replicati a tolleranza di errore e slave con Apache ZooKeeper
* Supporto per i contenitori formattati Docker
* Isolamento nativo tra le attività con i contenitori Linux
* Pianificazione di più risorse (memoria, CPU, disco e porte)
* Java, Python e API C++ per lo sviluppo di nuove applicazioni parallele
* Interfaccia utente Web per la visualizzazione dello stato del cluster

Per impostazione predefinita, controller di dominio o sistema operativo in esecuzione nel servizio contenitore di Azure include una piattaforma di orchestrazione hello maratona per la pianificazione di carichi di lavoro. Tuttavia, in hello DC/distribuzione del sistema operativo del servizio ACS è incluso hello Mesosphere universo di servizi che possono essere aggiunti tooyour servizio. Servizi in hello universo includono Spark, Hadoop, Cassandra e molto altro ancora.

![Universe DC/OS nel servizio contenitore di Azure](media/dcos/universe.png)

#### <a name="using-marathon"></a>Uso di Marathon
Maratona è un init cluster a livello di sistema e controllo per i servizi in cgroups - o, in caso di hello contenitore del servizio di Azure, i contenitori di Docker in formato. Marathon offre un'interfaccia utente Web da cui è possibile distribuire le applicazioni. L'accesso avviene tramite un URL simile a `http://DNS_PREFIX.REGION.cloudapp.azure.com`, dove DNS\_PREFIX e REGION vengono definiti in fase di distribuzione. Naturalmente, è anche possibile fornire il proprio nome DNS. Per ulteriori informazioni sull'esecuzione di un contenitore utilizzando l'interfaccia utente web maratona di hello, vedere [gestione dei contenitori di controller di dominio o del sistema operativo tramite l'interfaccia utente web di maratona hello](container-service-mesos-marathon-ui.md).

![Elenco di applicazioni Marathon](media/dcos/marathon-applications-list.png)

Inoltre, è possibile utilizzare hello API REST per la comunicazione con maratona. Esistono una serie di librerie client disponibili per ogni strumento. Coprono un'ampia gamma di linguaggi, e, naturalmente, è possibile utilizzare il protocollo HTTP hello in qualsiasi linguaggio. Inoltre, molti strumenti comuni di DevOps forniscono il supporto per Marathon. Ciò fornisce flessibilità massima per il team operativo quando si lavora con un cluster del servizio contenitore di Azure. Per ulteriori informazioni sull'esecuzione di un contenitore utilizzando l'API REST maratona hello, vedere [gestione dei contenitori di controller di dominio o del sistema operativo tramite l'API REST maratona hello](container-service-mesos-marathon-rest.md).

### <a name="using-docker-swarm"></a>Utilizzo di Docker Swarm
Docker Swarm fornisce clustering nativo per Docker. Poiché Docker Swarm serve hello standard API di Docker, qualsiasi strumento che già comunica con un daemon di Docker è possibile usare gli host di toomultiple sciame tootransparently scala sul servizio contenitore di Azure.

![Il servizio contenitore di Azure configurato toouse sciame.](media/acs-intro/acs-swarm2.png)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

Strumenti supportati per la gestione dei contenitori in un cluster sciame includono, ma non sono limitati a, seguente hello:

* Dokku
* Docker CLI e Docker Compose
* Krane
* Jenkins

### <a name="using-kubernetes"></a>Uso di Kubernetes
Kubernetes è un diffuso strumento open source di livello di produzione per l'orchestrazione di contenitori. Kubernetes automatizza la distribuzione, il ridimensionamento e la gestione delle applicazioni nei contenitori. Poiché è una soluzione open source e dipende dalla community open source hello, in base a cui viene eseguito senza problemi nel servizio contenitore di Azure e può essere utilizzato toodeploy contenitori su larga scala nel servizio contenitore di Azure.

![Il servizio contenitore di Azure configurato toouse Kubernetes.](media/acs-intro/kubernetes.png)

Dispone di un set completo di funzionalità tra cui:
* Scalabilità orizzontale
* Bilanciamento del carico e rilevamento del servizio
* Gestione della configurazione e segreti
* Implementazioni e ripristini automatizzati basati sull'API
* Riparazione automatica

## <a name="videos"></a>Video
Introduzione al servizio contenitore di Azure (101):  

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Container-Service-101/player]
>
>

Hello applicazioni utilizzando creazione servizio contenitore di Azure (compilazione 2016)

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/B822/player]
>
>

## <a name="next-steps"></a>Passaggi successivi

Distribuire un cluster di servizio di contenitore mediante hello [portale](container-service-deployment.md) o [CLI di Azure 2.0](container-service-create-acs-cluster-cli.md).

---
title: cluster di controller di dominio o sistema operativo Azure aaaMonitor - Datadog | Documenti Microsoft
description: Monitorare un cluster del servizio contenitore di Azure con Datadog. Utilizzare hello controller di dominio o del sistema operativo dell'interfaccia utente toodeploy hello Datadog agenti tooyour cluster web.
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenitori, controller di dominio/sistema operativo, Docker Swarm, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a>Monitorare un cluster DC/OS del servizio contenitore di Azure con Datadog
In questo articolo si distribuirà Datadog agenti tooall hello agente i nodi del cluster del servizio di contenitore di Azure. Per questa configurazione, sarà necessario un account con Datadog. 

## <a name="prerequisites"></a>Prerequisiti
[Distribuire](container-service-deployment.md) e [connettere](../container-service-connect.md) un cluster configurato dal servizio contenitore di Azure. Esplorare hello [dell'interfaccia utente maratona](container-service-mesos-marathon-ui.md). Andare troppo[http://datadoghq.com](http://datadoghq.com) tooset Datadog conto. 

## <a name="datadog"></a>Datadog
Datadog è un servizio che raccoglie dati di monitoraggio dai contenitori all'interno del cluster del servizio contenitore di Azure. Datadog è dotato di un dashboard di integrazione Docker in cui è possibile visualizzare metriche specifiche all'interno dei propri contenitori. Le metriche raccolte dai contenitori sono organizzate per CPU, memoria, rete e I/O. Datadog suddivide le metriche in contenitori e immagini. Un esempio di quali hello dell'interfaccia utente sembra che per la CPU è di sotto l'utilizzo.

![Interfaccia utente Datadog](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a>Configurare una distribuzione Datadog con Marathon
Questa procedura viene illustrato come tooconfigure e la distribuzione Datadog applicazioni tooyour cluster con maratona. 

Accedere all'interfaccia utente del controller di dominio/sistema operativo da [http://localhost:80/](http://localhost:80/). Una volta nell'interfaccia utente di controller di dominio/OS passare hello toohello "Universo" che si trova in hello in basso a sinistra e quindi cercare "Datadog" e fare clic su "Installa".

![Pacchetto Datadog all'interno di hello l'universo dei controller di dominio o del sistema operativo](./media/container-service-monitoring/datadog1.png)

Ora toocomplete hello configurazione sarà necessario un account Datadog o un account di prova. Dopo aver eseguito il nel sito Web Datadog toohello cercare toohello sinistra e passare tooIntegrations -> quindi [API](https://app.datadoghq.com/account/settings#api). 

![Chiave API di Datadog](./media/container-service-monitoring/datadog2.png)

Quindi immettere la chiave API in configurazione Datadog hello all'interno di hello l'universo dei controller di dominio o del sistema operativo. 

![Configurazione Datadog in hello l'universo dei controller di dominio o del sistema operativo](./media/container-service-monitoring/datadog3.png) 

In hello sopra configurazione istanze sono impostate too10000000 pertanto ogni volta che viene aggiunto un nuovo nodo cluster toohello Datadog distribuirà automaticamente un nodo toothat agente. Si tratta di una soluzione temporanea. Dopo aver installato il pacchetto di hello si deve passare sito Web Datadog toohello indietro e si trova "[dashboard](https://app.datadoghq.com/dash/list)." Da qui si vedrà Custom and Integration Dashboards. Hello [dashboard Docker](https://app.datadoghq.com/screen/integration/docker) disporrà di tutte le metriche di contenitore hello è necessario per il monitoraggio del cluster. 


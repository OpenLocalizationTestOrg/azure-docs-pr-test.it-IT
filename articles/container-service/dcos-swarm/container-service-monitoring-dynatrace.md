---
title: cluster di controller di dominio o sistema operativo Azure aaaMonitor - Dynatrace | Documenti Microsoft
description: Monitorare un cluster DC/OS del servizio contenitore di Azure con Dynatrace. Distribuire hello Dynatrace OneAgent tramite il dashboard di controller di dominio/OS hello.
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: Contenitori, controller di dominio/sistema operativo, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 9e2e2d1c8b454422d1db30dac7c385d31d336853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a>Monitorare un cluster DC/OS del servizio contenitore di Azure con Dynatrace SaaS/Managed
In questo articolo verrà illustrato come hello toodeploy [Dynatrace](https://www.dynatrace.com/) toomonitor OneAgent tutti hello nodi agente nel cluster il servizio contenitore di Azure. Per questa configurazione, è necessario un account con Dynatrace SaaS/Managed. 

## <a name="dynatrace-saasmanaged"></a>Dynatrace SaaS/Managed
Dynatrace è una soluzione di monitoraggio nativa del cloud per gli ambienti cluster e dei contenitori altamente dinamici. Consente di ottimizzare la toobetter contenitore distribuzioni e le allocazioni di memoria utilizzando i dati di utilizzo in tempo reale. È in grado di individuare automaticamente problemi a livello di applicazioni e infrastruttura fornendo una baseline automatizzata, oltre alla correlazione dei problemi e al rilevamento delle cause principali.

Figura Hello seguente è illustrato hello UI Dynatrace:

![Interfaccia utente di Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a>Prerequisiti 
[Distribuire](container-service-deployment.md) e [connettersi](./../container-service-connect.md) tooa cluster configurato dal servizio di contenitore di Azure. Esplorare hello [dell'interfaccia utente maratona](container-service-mesos-marathon-ui.md). Andare troppo[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset conto Dynatrace SaaS.  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a>Configurare una distribuzione Dynatrace con Marathon
La procedura mostra come tooconfigure e la distribuzione Dynatrace applicazioni tooyour cluster con maratona.

1. Accedere all'interfaccia utente del controller di dominio/sistema operativo da [http://localhost:80/](http://localhost:80/). Una volta nell'interfaccia utente di controller di dominio/OS hello, passare toohello **universo** scheda e quindi cercare **Dynatrace**.

    ![Dynatrace in Universe (Universo) di DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. configurazione di hello toocomplete, è necessario un account Dynatrace SaaS o un account di prova. Una volta accedere al dashboard Dynatrace hello, selezionare **distribuire Dynatrace**.

    ![Dynatrace - Set up PaaS integration (Configura integrazione Paas)](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. Nella pagina hello selezionare **configurare l'integrazione di PaaS**. 

    ![Token API di Dynatrace](./media/container-service-monitoring-dynatrace/api-token.png) 

4. Immettere il token dell'API in hello Dynatrace OneAgent configurazione all'interno di hello l'universo dei controller di dominio o del sistema operativo. 

    ![Configurazione Dynatrace OneAgent in hello l'universo dei controller di dominio o del sistema operativo](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. Impostare le istanze di hello toohello numero dei nodi si intende toorun. L'impostazione di un numero più alto inoltre funziona, ma i controller di dominio o del sistema operativo continuerà a tentare toofind nuove istanze fino a raggiungere quel numero effettivamente. Se si preferisce, è anche possibile impostare questo valore tooa come 1000000. In questo caso, ogni volta che un nuovo nodo viene aggiunto il cluster toohello, Dynatrace distribuisce automaticamente un agente toothat nuovo nodo, il prezzo di hello del controller di dominio o sistema operativo costantemente tentativo toodeploy altre istanze.

    ![Configurazione Dynatrace nel controller di dominio o del sistema operativo universo-le istanze di hello](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a>Passaggi successivi

Dopo aver installato il pacchetto di hello, spostarsi indietro toohello Dynatrace dashboard. È possibile esplorare le metriche di utilizzo diversi hello per contenitori hello all'interno del cluster. 

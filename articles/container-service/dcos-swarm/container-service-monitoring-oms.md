---
title: cluster di controller di dominio o sistema operativo Azure aaaMonitor - Operations Manager | Documenti Microsoft
description: Monitorare un cluster DC/OS del servizio contenitore di Azure con Microsoft Operations Management Suite.
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a>Monitorare un cluster DC/OS del servizio contenitore di Azure con Operations Management Suite

Microsoft Operations Management Suite (OMS) è la soluzione Microsoft per la gestione IT basata sul cloud che consente di gestire e proteggere l'infrastruttura locale e cloud. Soluzione di contenitore è una soluzione Analitica di Log di OMS, che consente di visualizzare l'inventario contenitore hello, prestazioni e i log in un'unica posizione. È possibile audit, risoluzione dei contenitori di visualizzazione dei log di hello in posizione centralizzata e trovare rumore utilizzo in eccesso contenitore in un host.

![](media/container-service-monitoring-oms/image1.png)

Per ulteriori informazioni sulla soluzione di contenitore, vedere toothe [contenitore soluzione Log Analitica](../../log-analytics/log-analytics-containers.md).

## <a name="setting-up-oms-from-hello-dcos-universe"></a>Configurazione di OMS da universo di controller di dominio/OS hello


In questo articolo presuppone che sia stato configurato un controller di dominio o sistema operativo e aver distribuito le applicazioni web semplice contenitore nel cluster hello.

### <a name="pre-requisite"></a>Prerequisito.
- [Sottoscrizione di Microsoft Azure](https://azure.microsoft.com/free/): è gratuita.  
- Configurazione dell'area di lavoro di Microsoft OMS (vedere il "Passaggio 3" sotto)
- [Interfaccia della riga di comando di DC/OS](https://dcos.io/docs/1.8/usage/cli/install/) installata.

1. Nel dashboard di controller di dominio/OS hello, fare clic su universo e cercare "OMS', come illustrato di seguito.

![](media/container-service-monitoring-oms/image2.png)

2. Fare clic su **Installa**. Verrà visualizzato un pop backup con informazioni sulla versione di hello OMS e un **Installa pacchetto** o **installazione avanzata** pulsante. Quando fa clic su **installazione avanzata**, determinando toohello **proprietà di configurazione specifiche OMS** pagina.

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. In questo caso, verrà chiesto hello tooenter `wsid` (hello ID area di lavoro OMS) e `wskey` (hello OMS chiave primaria per l'id dell'area di lavoro hello). entrambi tooget `wsid` e `wskey` toocreate è necessario un account OMS alla <https://mms.microsoft.com>. Seguire hello passaggi toocreate un account. Dopo aver terminato la creazione di account di hello, è necessario tooobtain il `wsid` e `wskey` facendo **impostazioni**, quindi **Connected Sources**e quindi **server Linux** , come illustrato di seguito.

 ![](media/container-service-monitoring-oms/image5.png)

4. Selezionare hello numero è OMS istanze desiderate e fare clic sul pulsante di hello 'Verifica e installa'. In genere, si desidererà toohave hello numero OMS istanze toohello uguale della macchina virtuale è presente nel cluster di agente. Agente OMS per Linux viene installato come singoli contenitori in ogni macchina virtuale che desideri toocollect informazioni per il monitoraggio e registrazione.

## <a name="setting-up-a-simple-oms-dashboard"></a>Configurazione di un dashboard OMS semplice

Dopo aver installato hello agente OMS per Linux in macchine virtuali di hello, il passaggio successivo è tooset i dashboard OMS hello. Esistono due modi toodo questo: portale OMS o il portale di Azure.

### <a name="oms-portal"></a>Portale di OMS 

Accedi al portale di OMS toohello (<https://mms.microsoft.com>) e passare toohello **raccolta soluzioni**.

![](media/container-service-monitoring-oms/image6.png)

Una volta nel hello **raccolta soluzioni**selezionare **contenitori**.

![](media/container-service-monitoring-oms/image7.png)

Dopo aver selezionato hello contenitore soluzione, si noterà hello riquadro nella pagina Dashboard panoramica di OMS hello. Una volta hello caricamento dati del contenitore sono indicizzati, si noterà riquadro hello popolato con informazioni sui riquadri di visualizzazione delle soluzioni.

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a>Portale di Azure 

Portale di account di accesso tooAzure all'indirizzo <https://portal.microsoft.com/>. Passare a **Marketplace**, selezionare **Monitoraggio + gestione** e fare clic su **Visualizza tutto**. Dopodiché, digitare `containers` nella ricerca Verrà visualizzato "contenitori" nei risultati della ricerca hello. Selezionare **Contenitori** e fare clic su **Crea**.

![](media/container-service-monitoring-oms/image9.png)

Dopo avere fatto clic su **Crea**, verrà chiesto di indicare l'area di lavoro. Selezionarne una esistente, oppure creare una nuova area di lavoro.

![](media/container-service-monitoring-oms/image10.PNG)

Dopo averla selezionata, fare clic su **Crea**.

![](media/container-service-monitoring-oms/image11.png)

Per ulteriori informazioni sulla soluzione contenitore OMS hello, consultare toothe [contenitore soluzione Log Analitica](../../log-analytics/log-analytics-containers.md).

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a>Come tooscale agente OMS con ACS controller di dominio o del sistema operativo 

Nel caso in cui è necessario toohave installato l'agente OMS insufficiente conteggio effettivo nodo hello o scalabilità VMSS aggiungendo altre VM, è possibile farlo scalando hello `msoms` servizio.

È possibile andare tooMarathon o hello scheda DC/servizi del sistema operativo dell'interfaccia utente e la scalabilità verticale il numero di nodi.

![](media/container-service-monitoring-oms/image12.PNG)

Nodi tooother che non hanno ancora installato l'agente OMS hello verrà distribuito.

## <a name="uninstall-ms-oms"></a>Disinstallare OMS di Microsoft

toouninstall MS OMS immettere hello comando seguente:

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a>Facci sapere
Cosa funziona? Cosa manca? Altre è necessario per questa toobe utili per l'utente? Scrivere a <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.

## <a name="next-steps"></a>Passaggi successivi

 Ora che è stato impostato toomonitor OMS ai contenitori,[visualizzare il dashboard di contenitore](../../log-analytics/log-analytics-containers.md).

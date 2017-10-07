---
title: aaaAzure il monitoraggio dei contenitori dell'infrastruttura di servizi e diagnostica | Documenti Microsoft
description: Informazioni su come toomonitor e diagnosticare contenitori orchestrati in Microsoft Azure Service Fabric con soluzioni di contenitori di OMS.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/10/2017
ms.author: dekapur
ms.openlocfilehash: cd79111cf78b9d76a60d489bb9953587aa06186d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-windows-server-containers-with-oms"></a>Monitoraggio dei contenitori Windows Server con OMS

## <a name="oms-containers-solution"></a>Soluzione Contenitori di OMS

il team di Operations Management Suite (OMS) Hello ha pubblicato una soluzione di contenitori per la diagnostica e monitoraggio per i contenitori. Con la propria soluzione di infrastruttura del servizio, questa soluzione è le distribuzioni di contenitori un ottimo strumento toomonitor orchestrati nell'infrastruttura del servizio. Ecco un esempio semplice di quale dashboard hello nella soluzione hello il seguente aspetto:

![Dashboard OMS di base](./media/service-fabric-diagnostics-containers-windowsserver/oms-containers-dashboard.png)

Raccoglie inoltre diversi tipi di registri che è possibile eseguire query nello strumento di OMS Log Analitica hello, e può essere utilizzato toovisualize qualsiasi metriche o gli eventi generati. tipi di log Hello raccolti sono:

1. ContainerInventory: informazioni su posizione, nome e immagini dei contenitori
2. ContainerImageInventory: informazioni sulle immagini distribuite, inclusi ID o dimensioni
3. ContainerLog: log degli errori specifici, log Docker (stdout e così via) e altre voci
4. ContainerServiceLog: comandi del daemon Docker che sono stati eseguiti
5. Delle prestazioni: contatori incluso contenitore della cpu, memoria, il traffico di rete, i/o del disco e metriche personalizzate da hello ospitano macchine

Questo articolo descrive tooset necessari passaggi di hello formare il contenitore di monitoraggio per il cluster. ulteriori informazioni sulla soluzione di contenitori di OMS, toolearn estrarre loro [documentazione](../log-analytics/log-analytics-containers.md).

## <a name="1-set-up-a-service-fabric-cluster"></a>1. Configurare un cluster di Service Fabric

Creare un cluster utilizzando il modello di gestione risorse di Azure hello trovato [qui](https://github.com/dkkapur/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Sample). Verificare che tooadd un nome di area di lavoro OMS univoco. Questo modello viene anche impostato toodeploying compilazione di un cluster in anteprima hello di Service Fabric (v255.255), il che significa che non può essere utilizzato nell'ambiente di produzione e non può essere aggiornato tooa diversa versione di Service Fabric. Se si decide di questo modello per toouse a lungo termine o di produzione usare, modificare una versione di hello tooa numero di versione stabile.

Una volta configurato il cluster hello, confermare che si installa certificato appropriato hello e assicurarsi che sia in grado di tooconnect toohello cluster.

Verificare che il gruppo di risorse sia configurato correttamente dall'intestazione toohello [portale di Azure](https://portal.azure.com/) e individuazione di distribuzione hello. gruppo di risorse Hello dovrebbe contenere tutte le risorse di Service Fabric hello e hanno anche una soluzione Analitica di Log, nonché una soluzione di Service Fabric.

Per la modifica di un cluster di Service Fabric esistente:
* Verificare che sia abilitata la diagnostica (in caso contrario, abilitarla tramite [l'aggiornamento di set di scalabilità della macchina virtuale hello](/rest/api/virtualmachinescalesets/create-or-update-a-set))
* Aggiungere un'area di lavoro OMS tramite la creazione di una soluzione di "Servizio Fabric Analitica" tramite hello Azure Marketplace
* Modifica di origini dati hello di hello Service Fabric soluzione toopick dei dati dalle tabelle di archiviazione di Azure appropriate hello (impostate da WAD) in hello gruppo di risorse che hello cluster si trova in
* Aggiungi agente hello come un [set di scalabilità della macchina virtuale toohello estensione](/powershell/module/azurerm.compute/add-azurermvmssextension) tramite PowerShell o l'aggiornamento di set di scalabilità della macchina virtuale hello (stesso collegamento sopra, modello di gestione risorse di hello toomodify)

## <a name="2-deploy-a-container"></a>2. Distribuire un contenitore

Una volta cluster hello è pronto e aver verificato che sia possibile accedervi, è possibile distribuire tooit un contenitore. Se si sceglie di versione di anteprima hello toouse come set dal modello hello, è possibile esplorare anche docker di nuovo di Service Fabric compongono la funzionalità. Tenere presente che hello prima volta che un'immagine contenitore è distribuito tooa cluster, vengono visualizzate più immagini di hello toodownload minuti a seconda delle dimensioni.

## <a name="3-add-hello-containers-solution"></a>3. Aggiungere hello contenitori soluzione

In hello portale di Azure, creare una risorsa contenitori (in hello monitoraggio + gestione categoria) tramite Azure Marketplace. 

![Aggiunta della soluzione Contenitori](./media/service-fabric-diagnostics-containers-windowsserver/containers-solution.png)

Nel passaggio della creazione di hello, richiede un'area di lavoro OMS. Selezionare hello ne è stata creata con la distribuzione di hello precedente. Questo passaggio viene aggiunta una soluzione di contenitori all'interno dell'area di lavoro OMS e viene rilevato automaticamente dall'agente OMS hello distribuite dal modello hello. agente di Hello inizierà a raccogliere dati sui processi di contenitori hello cluster hello e circa 10-15 minuti, si dovrebbe essere chiaro backup con i dati come immagine di hello del dashboard hello sopra soluzione di hello.

## <a name="4-next-steps"></a>4. Passaggi successivi

OMS offre vari strumenti in hello dell'area di lavoro toomake se più utili per l'utente. Esplorare hello opzioni toocustomize hello soluzione tooyour esigenze seguenti:
- Ottenere conoscenza con hello [ricerca e l'esecuzione di query log](../log-analytics/log-analytics-log-searches.md) funzionalità fornite come parte del Log Analitica
- Configurare hello OMS agent toopick backup specifici contatori delle prestazioni (passare toohello area Home > Impostazioni > dati > i contatori delle prestazioni di Windows)
- Configurare OMS tooset [automatizzata avvisi](../log-analytics/log-analytics-alerts.md) tooaid regole di rilevamento e di diagnostica

---
title: Analisi degli eventi dell'infrastruttura di servizio con OMS aaaAzure | Documenti Microsoft
description: Informazioni sulla visualizzazione e l'analisi di eventi con OMS per il monitoraggio e la diagnostica dei cluster di Azure Service Fabric.
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
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 526519293e70982c95e31241465b87f190096f74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-oms"></a>Analisi e visualizzazione degli eventi con OMS

Operations Management Suite (OMS) è una raccolta di servizi di gestione che ti consentono di monitoraggio e diagnostica per le applicazioni e i servizi ospitati nel cloud hello. leggere una panoramica più dettagliata di OMS e offre, tooget [novità OMS?](../operations-management-suite/operations-management-suite-overview.md)

## <a name="log-analytics-and-hello-oms-workspace"></a>Analitica e hello area di lavoro OMS log

Log Analytics raccoglie i dati dalle risorse gestite, tra cui una tabella di archiviazione o un agente di Azure, e li gestisce in un repository centrale. dati Hello possono essere quindi utilizzato per la visualizzazione, avvisi e analisi, o ulteriormente l'esportazione. Log Analytics supporta i dati sulle prestazioni, sugli eventi o altri dati personalizzati.

Quando è configurato OMS, si avrà accesso tooa specifiche *area di lavoro OMS*, da dove dati possono essere eseguita una query o visualizzati nei dashboard.

Una volta ricevuti i dati dal Log Analitica, OMS dispone di numerosi *soluzioni di gestione* che sono soluzioni predefinite toomonitor dati in ingresso, scenari tooseveral personalizzato. Questi includono un *servizio Fabric Analitica* soluzione e un *contenitori* soluzione, che sono quelli più importanti due hello toodiagnostics e il monitoraggio se si utilizzano i cluster di Service Fabric. Esistono numerosi altri anche che vale la pena di esplorazione e OMS consente inoltre la creazione di hello delle soluzioni personalizzate, che consente di leggere informazioni sui [qui](../operations-management-suite/operations-management-suite-solutions.md). Ogni soluzione scelto toouse per un cluster sarà configurato in hello stessa area di lavoro OMS, insieme ai Log Analitica. Aree di lavoro consentono di dashboard personalizzati e visualizzazione dei dati e i dati di toohello modifiche che si desidera toocollect, elaborare e analizzare.

## <a name="setting-up-an-oms-workspace-with-hello-service-fabric-solution"></a>Configurazione di un'area di lavoro OMS con soluzioni di infrastruttura servizio hello

È consigliabile che si aggiungono hello soluzione di infrastruttura del servizio nell'area di lavoro OMS, in quanto fornisce un dashboard utile che mostra hello vari canali di log in ingresso dal livello di piattaforma e l'applicazione hello e hello in grado di tooquery Service Fabric specifico log. Di seguito è una soluzione di infrastruttura servizio relativamente semplice l'aspetto seguente, con una singola applicazione distribuita in cluster hello:

![Soluzione OMS SF](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-solution.png)

Esistono due modi tooprovision e configurare un'area di lavoro OMS, tramite un modello di gestione risorse o direttamente da Azure Marketplace. Utilizzare prima di hello quando si distribuisce un cluster e hello quest'ultimo se si dispone già di un cluster distribuito con la diagnostica è abilitata.

### <a name="deploying-oms-using-a-resource-management-template"></a>Distribuzione di OMS con il modello di gestione risorse

Ciò si verifica in fase di creazione di cluster hello - quando si distribuisce un cluster utilizzando un modello di gestione risorse, un modello di hello è inoltre possibile creare una nuova area di lavoro OMS, aggiungere tooit soluzione di infrastruttura servizio hello e configurarlo tooread dati dall'archiviazione appropriato hello tabelle.

>[!NOTE]
>Per questo toowork, diagnostica ha attivato affinché tooexist tabelle di archiviazione di Azure hello per OMS toobe / Log Analitica tooread informazioni da.

[Qui](https://azure.microsoft.com/resources/templates/service-fabric-oms/) viene illustrato un modello di esempio che è possibile usare e modificare in base alle necessità e che esegue le azioni descritte sopra. In caso di hello che si desidera più Facoltatività, esistono alcuni altri modelli che consentono di creare diverse opzioni a seconda di dove nel processo di hello potrebbe essere di configurazione di un'area di lavoro OMS, è reperibile in [Service Fabric e OMS modelli](https://azure.microsoft.com/resources/templates/?term=service+fabric+OMS).

### <a name="deploying-oms-using-through-azure-marketplace"></a>Distribuzione di OMS tramite Azure Marketplace

Se si preferisce un'area di lavoro OMS tooadd dopo aver distribuito un cluster, visitare tooAzure Marketplace e cercare *"Servizio Fabric Analitica"*. Deve essere presente solo una risorsa che viene visualizzato, nella categoria "Monitoraggio gestione +" hello, illustrato di seguito:

![Analisi SF OMS in Marketplace](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-analytics.png)

Se si fa clic su **Crea** viene richiesta un'area di lavoro OMS. Fare clic su **Selezionare un'area di lavoro** e quindi **Crea una nuova area di lavoro**. Compilare le voci necessarie hello - hello qui è che la sottoscrizione hello per hello Service Fabric deve essere l'area di lavoro OMS cluster e hello hello stesso. Dopo aver convalidato le voci, l'area di lavoro OMS verrà distribuita in pochi minuti. Mentre viene completata la distribuzione, la creazione di hello del Pannello di soluzioni di Service Fabric hello ancora rimarrà aperta. Assicurarsi che hello stessa area di lavoro viene visualizzato in *area di lavoro OMS* e fare clic su **crea** nella parte inferiore di hello, tooadd hello dell'area di lavoro di Service Fabric soluzione toohello.

## <a name="using-hello-oms-agent"></a>Tramite l'agente OMS hello

È consigliabile toouse EventFlow WAD come soluzioni di aggregazione, in quanto consentono per un toodiagnostics approccio più modulare e monitoraggio. Ad esempio, se si desidera toochange l'output da EventFlow, non richiede alcuna strumentazione effettivo tooyour cambia, solo un file di configurazione tooyour semplice modifica. Se, tuttavia, tooinvest con OMS si è disposti toocontinue utilizzarlo per analisi eventi (non dispone di hello toobe solo piattaforma utilizzare, ma piuttosto che sarà almeno una delle piattaforme hello), è consigliabile acquisire familiarità con impostazione hello [</C0>agenteOMS<spanclass="notranslate">](../log-analytics/log-analytics-windows-agents.md).</span> È inoltre necessario utilizzare agente OMS hello durante la distribuzione di cluster tooyour contenitori, come descritto di seguito.

il processo di Hello per eseguire questa operazione è relativamente semplice, poiché è sufficiente agente hello tooadd come set di scalabilità della macchina virtuale un modello di gestione risorse di estensione tooyour, assicurando che si ottiene installato in tutti i nodi. È possibile trovare un modello di gestione risorse di esempio che distribuisce l'area di lavoro OMS hello con hello soluzione Service Fabric (come sopra) e aggiunge i nodi di hello agente tooyour per i cluster che eseguono [Windows](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Windows) o [Linux](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Linux).

vantaggi di Hello di questo sono i seguenti hello:

* Dati più dettagliati sul lato di contatori e le metriche delle prestazioni hello
* Facile tooconfigure dati raccolti da hello e apportare le modifiche tooit senza ridistribuire le applicazioni del cluster o cluster hello, poiché le modifiche toohello impostazioni dell'agente di hello possono essere eseguite dall'area di lavoro OMS hello e verranno reimpostata agente hello in modo automatico. tooconfigure hello OMS agent toopick backup specifici contatori delle prestazioni, dell'area di lavoro di passare toohello **Home > Impostazioni > dati > i contatori delle prestazioni di Windows** e selezionare hello i dati raccolti toosee
* Visualizzare i dati più velocemente rispetto al fatto che presenti toobe archiviata prima di essere prelevate da OMS / Log Analitica
* Il monitoraggio dei contenitori è molto più semplice, poiché può prelevare log, ovvero stdout, stderror, e registri di docker, ovvero metriche di prestazioni sui livelli di contenitori e nodi

considerazione principale di Hello qui è che poiché si tratta di un agente, in cui verrà distribuito il cluster, insieme a tutte le applicazioni, pertanto si verificheranno alcune un impatto minimo toohello delle prestazioni delle applicazioni in cluster hello.

## <a name="monitoring-containers"></a>Monitoraggio di contenitori

Durante la distribuzione di cluster di Service Fabric tooa contenitori, è consigliabile che hello cluster è stato configurato con l'agente OMS hello e tale soluzione contenitori hello è stato aggiunto tooyour OMS workspace tooenable monitoraggio e diagnostica. Ecco i contenitori di hello soluzione simile in un'area di lavoro:

![Dashboard OMS di base](./media/service-fabric-diagnostics-event-analysis-oms/oms-containers-dashboard.png)

agente Hello abilita la raccolta di hello dei log specifici per i contenitori che è possibile eseguire query in OMS o utilizzato toovisualized indicatori di prestazioni. tipi di log Hello raccolti sono:

* ContainerInventory: informazioni su posizione, nome e immagini dei contenitori
* ContainerImageInventory: informazioni sulle immagini distribuite, inclusi ID o dimensioni
* ContainerLog: log degli errori specifici, log Docker (stdout e così via) e altre voci
* ContainerServiceLog: comandi del daemon Docker che sono stati eseguiti
* Delle prestazioni: contatori incluso contenitore della cpu, memoria, il traffico di rete, i/o del disco e metriche personalizzate da hello ospitano macchine

Questo articolo descrive tooset necessari passaggi di hello formare il contenitore di monitoraggio per il cluster. ulteriori informazioni sulla soluzione di contenitori di OMS, toolearn estrarre loro [documentazione](../log-analytics/log-analytics-containers.md).

tooset backup hello soluzione contenitore nell'area di lavoro, assicurarsi di disporre l'agente OMS hello distribuite nei nodi del cluster seguendo i passaggi di hello indicati sopra. Una volta cluster hello è pronto, è possibile distribuire tooit un contenitore. Tenere presente che hello prima volta che un'immagine contenitore è distribuito tooa cluster, vengono visualizzate più immagini di hello toodownload minuti a seconda delle dimensioni.

In Azure Marketplace, cercare *contenitori* e creare una risorsa contenitori (in hello monitoraggio + gestione categoria).

![Aggiunta della soluzione Contenitori](./media/service-fabric-diagnostics-event-analysis-oms/containers-solution.png)

Nel passaggio della creazione di hello, richiede un'area di lavoro OMS. Selezionare hello ne è stata creata con la distribuzione di hello precedente. Questo passaggio viene aggiunta una soluzione di contenitori all'interno dell'area di lavoro OMS e viene rilevato automaticamente dall'agente OMS hello distribuite dal modello hello. agente di Hello inizierà a raccogliere dati sui processi di contenitori hello in cluster hello e meno di 15 minuti o in tal caso, si dovrebbe essere chiaro backup con i dati, come immagine di hello del dashboard hello sopra soluzione di hello.


## <a name="next-steps"></a>Passaggi successivi

Esplorare hello seguente OMS strumenti e opzioni toocustomize che tooyour un'area di lavoro deve:

* Per i cluster locale, OMS offre un Gateway (in avanti il Proxy HTTP) che può essere utilizzati toosend tooOMS di dati. Per ulteriori informazioni in [senza tooOMS accesso a Internet usando hello OMS Gateway di connessione dei computer](../log-analytics/log-analytics-oms-gateway.md)
* Configurare OMS tooset [automatizzata avvisi](../log-analytics/log-analytics-alerts.md) tooaid nel rilevando e diagnostica
* Ottenere conoscenza con hello [ricerca e l'esecuzione di query log](../log-analytics/log-analytics-log-searches.md) funzionalità fornite come parte del Log Analitica

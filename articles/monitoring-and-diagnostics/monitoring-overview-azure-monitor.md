---
title: Cenni preliminari su Monitor aaaAzure | Documenti Microsoft
description: "Monitoraggio di Azure raccoglie dati statistici da usare in avvisi, webhook, scalabilità automatica e automazione. L'articolo elenca anche altre opzioni di monitoraggio di Microsoft."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: ffa304e7b158f0fceb7f60ab88fab291976aa0e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-monitor"></a>Panoramica di Monitoraggio di Azure
In questo articolo viene fornita una panoramica di hello servizio monitoraggio di Azure in Microsoft Azure. Viene descritto cosa Monitor di Azure e fornisce i puntatori tooadditional informazioni su come toouse Monitor di Azure.  Se si preferisce un video di introduzione, vedere i collegamenti di passaggi avanti nella parte inferiore di hello di questo articolo. 

## <a name="why-monitor-your-application-or-system"></a>Perché monitorare l'applicazione o il sistema
Le applicazioni cloud sono complesse e hanno molte parti mobili. Il monitoraggio fornisce tooensure dati che l'applicazione resta alto e in esecuzione in uno stato integro. Consente inoltre toostave è impostata su off problemi potenziali o risolvere i problemi oltre quelle. Inoltre, è possibile utilizzare Monitoraggio dati toogain approfondite sull'applicazione. Tali informazioni possono consentono di prestazioni dell'applicazione tooimprove o manutenibilità o automatizzare le operazioni che altrimenti richiederebbero un intervento manuale.


## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a>Monitoraggio di Azure e altri prodotti per il monitoraggio di Microsoft
Attualmente Monitoraggio di Azure offre metriche e log dell'infrastruttura di livello base per la maggior parte dei servizi in Microsoft Azure, Servizi di Azure che non ancora inseriti i dati di monitoraggio di Azure verranno inseriti in tale posizione in hello future.

Microsoft offre altri prodotti e servizi con funzionalità di monitoraggio aggiuntive per sviluppatori, DevOps o ITOps, che hanno anche installazioni locali. Per una panoramica e per informazioni sull'integrazione di questi diversi prodotti e servizi, vedere [Monitoraggio in Microsoft Azure](monitoring-overview.md).

## <a name="monitoring-sources---compute"></a>Monitoraggio delle origini: calcolo

![Modello di monitoraggio e diagnostica per risorse non di calcolo](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)

i servizi di calcolo Hello includono 
- Servizi cloud 
- Macchine virtuali 
- Set di scalabilità di macchine virtuali 
- Service Fabric

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a>Applicazione: log di diagnostica, log applicazioni e metriche
Applicazioni possono essere eseguite su hello del sistema operativo Guest nel modello di calcolo hello. Le applicazioni creano il proprio set di log e metriche. Monitoraggio di Azure si basa su hello diagnostica Windows Azure estensione (Windows o Linux) toocollect la maggior parte dei registri e le metriche a livello di applicazione. i tipi di Hello includono

* Contatori delle prestazioni
* Log applicazioni
* Registri eventi di Windows
* Origine dell'evento .NET
* Log di IIS
* ETW basato su manifesto
* Dump di arresto anomalo del sistema
* Log degli errori dei clienti

Senza l'estensione diagnostica hello, sono disponibili solo pochi metriche come l'utilizzo della CPU. 

### <a name="host-and-guest-vm-metrics"></a>Metriche delle VM host e guest
Hello risorse di calcolo elencate in precedenza dispongono di un host dedicato macchina virtuale e sistema operativo che interagiscono con guest. macchina virtuale host Hello e sistema operativo guest sono l'equivalente hello della macchina virtuale radice e macchina virtuale guest nel modello di hypervisor Hyper-V hello. È possibile raccogliere le metriche in entrambi. È anche possibile raccogliere i log di diagnostica nel sistema operativo guest hello.   

### <a name="activity-log"></a>Log attività
È possibile cercare hello Log attività (precedentemente denominato Operational o i log di controllo) per informazioni sulla risorsa stessa forma visualizzata hello dell'infrastruttura di Azure. log Hello contiene informazioni quali volte quando le risorse vengano create o eliminate.  Per altre informazioni, vedere [Panoramica del log attività di Azure](monitoring-overview-activity-logs.md). 

## <a name="monitoring-sources---everything-else"></a>Monitoraggio delle origini: altro

![Modello di monitoraggio e diagnostica per risorse di calcolo](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a>Risorsa: log di diagnostica e metriche
Da raccogliere i log di diagnostica e le metriche variano in base al tipo di risorsa hello. Ad esempio, le app Web sono incluse statistiche relative hello IO del disco e percentuale di CPU. Tali metriche non esistono invece per una coda del bus di servizio, che invece fornisce metriche come le dimensioni della coda e la velocità effettiva dei messaggi. In [Metriche supportate](monitoring-supported-metrics.md) è disponibile un elenco delle metriche che è possibile raccogliere per ogni risorsa. 

### <a name="host-and-guest-vm-metrics"></a>Metriche delle VM host e guest
Non esiste necessariamente una corrispondenza 1:1 tra la risorsa e una determinata VM host o guest e di conseguenza le metriche della VM non sono disponibili.

### <a name="activity-log"></a>Log attività
log attività Hello è hello come per le risorse di calcolo.  

## <a name="uses-for-monitoring-data"></a>Uso dei dati di monitoraggio
Dopo aver raccolto i dati, è possibile effettuare hello seguenti in Monitoraggio di Azure

### <a name="route"></a>Route
È possibile trasmettere i percorsi di tooother dati monitoraggio in tempo reale.

Tra gli esempi sono inclusi:

- È possibile utilizzare i relativi strumenti di visualizzazione e analisi più complete di trasmissione tooApplication Insights.
- È possibile distribuire strumenti di terze parti toothird inviare tooEvent hub. 

### <a name="store-and-archive"></a>Archiviare
Alcuni dati di monitoraggio sono già archiviati e disponibili in Monitoraggio di Azure per un periodo di tempo specificato. 
- Le metriche vengono archiviate per 30 giorni. 
- Le voci di log attività vengono archiviate per 90 giorni. 
- I log di diagnostica non vengono archiviati. 

Se si desiderano toostore dati più lungo di hello periodi di tempo elencate in precedenza, è possibile utilizzare una risorsa di archiviazione Azure. I dati di monitoraggio vengono mantenuti nell'account di archiviazione in base ai criteri di conservazione impostati. È toopay per hello spazio hello richiede dati nell'archiviazione di Azure. 

Alcuni modi toouse dati:

- Fare in modo che i dati scritti vengano letti ed elaborati da altri strumenti all'interno o all'esterno di Azure.
- Per scaricare i dati di hello in locale per un archivio locale o modificare i criteri di conservazione dei dati di hello cloud tookeep per lunghi periodi di tempo.  
- Mantenere i dati hello in archiviazione di Azure per un periodo illimitato per scopi di archiviazione. 

### <a name="query"></a>Query
È possibile usare hello Azure monitoraggio l'API REST di comandi dell'interfaccia della riga di comando (CLI) su più piattaforme, i cmdlet di PowerShell o hello .NET SDK tooaccess hello dati nel sistema di hello o archiviazione di Azure

Tra gli esempi sono inclusi:

* Recuperare i dati per un'applicazione di monitoraggio personalizzata che si è scritta.
* Creare query personalizzate e inviare tale applicazione di terze parti tooa di dati.

### <a name="visualize"></a>Visualizzazione
La visualizzazione di dati di monitoraggio in grafici e grafici consente di individuare le tendenze più veloce rispetto alla ricerca tramite dati hello stessi.  

Ecco alcuni metodi di visualizzazione:

* Utilizzare hello portale di Azure
* Dati di route tooAzure Application Insights
* Dati di route tooMicrosoft Power BI
* Route hello dati tooa visualizzazione di terze parti strumento usando di streaming live o con lo strumento di hello leggere da un archivio in archiviazione di Azure


### <a name="automate"></a>Automazione
È possibile utilizzare gli avvisi di monitoraggio dati tootrigger o addirittura interi processi. Tra gli esempi sono inclusi:

* Usare le istanze di calcolo di dati tooautoscale verso l'alto o verso il basso in base al carico dell'applicazione.
* Inviare messaggi di posta elettronica quando una metrica supera una soglia predeterminata.
* Chiama un tooexecute (webhook) URL web di un'azione in un sistema all'esterno di Azure
* Avvia un runbook in automazione di Azure tooperform una varietà di attività

## <a name="methods-of-accessing-azure-monitor"></a>Metodi di accesso a Monitoraggio di Azure
In generale, è possibile modificare il rilevamento di dati, routing e il recupero utilizzando uno dei seguenti metodi hello. Non tutti i metodi sono disponibili per tutte le azioni o tutti i tipi di dati.

* [Portale di Azure](https://portal.azure.com)
* [PowerShell](insights-powershell-samples.md)  
* [Interfaccia della riga di comando multipiattaforma](insights-cli-samples.md)
* [API REST](https://docs.microsoft.com/rest/api/monitor/)
* [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su:
- Una procedura dettagliata video solo di Monitoraggio di Azure è disponibile alla pagina  
[Introduzione a Monitoraggio di Azure](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor). Un altro video che illustra uno scenario in cui è possibile usare Monitoraggio di Azure è disponibile alle pagine [Explore Microsoft Azure monitoring and diagnostics](https://channel9.msdn.com/events/Ignite/2016/BRK2234) (Esplorare le funzionalità Diagnostica e Monitoraggio di Microsoft Azure) e [Azure Monitor in a video from Ignite 2016](https://myignite.microsoft.com/videos/4977) (Monitoraggio di Azure in un video di Ignite 2016)
- Eseguire tramite l'interfaccia Monitor Azure hello [Introduzione al monitoraggio di Azure](monitoring-get-started.md)
- Impostare hello [estensioni di diagnostica Azure](../azure-diagnostics.md) se si siano tentando toodiagnose problemi nel servizio Cloud, la macchina virtuale, applicare la scalabilità macchina virtuale set o applicazione di Service Fabric.
- [Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) se si siano tentando toodiagnostic problemi nell'applicazione servizio Web app.
- [Risoluzione dei problemi di Archiviazione di Azure](../storage/common/storage-e2e-troubleshooting.md) , utile per l'uso di BLOB, tabelle o code di archiviazione.
- [Log Analitica](https://azure.microsoft.com/documentation/services/log-analytics/) e hello [Operations Management Suite](https://www.microsoft.com/oms/)

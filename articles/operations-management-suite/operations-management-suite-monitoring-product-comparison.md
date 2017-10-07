---
title: confronto tra prodotti monitoraggio aaaMicrosoft | Documenti Microsoft
description: "Microsoft Operations Management Suite (OMS) è la soluzione Microsoft per la gestione IT basata sul cloud che consente di gestire e proteggere l'infrastruttura locale e cloud.  In questo articolo identifica diversi servizi hello inclusi in OMS e vengono forniti i collegamenti tootheir dettagliate contenuto."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: a63ca0ad-61f8-425d-a48c-d87ba518c104
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/27/2016
ms.author: bwren
ms.openlocfilehash: 61144a298fe73c35181070d552c41b96fc445097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-monitoring-product-comparison"></a>Confronto tra i prodotti per il monitoraggio Microsoft
Questo articolo fornisce un confronto tra System Center Operations Manager (SCOM) e di Log Analitica Operations Management Suite (OMS) in termini di loro architettura, la logica di come si esegue il monitoraggio risorse e come funzionano analisi dei dati hello hello sono raccogliere.  Si tratta di toogive comprendere i concetti fondamentali della loro differenze e i punti di forza di.  

## <a name="basic-architecture"></a>Architettura di base
### <a name="system-center-operations-manager"></a>System Center Operations Manager
Tutti i componenti SCOM vengono installati nel data center.  [Gli agenti vengono installati](http://technet.microsoft.com/library/hh551142.aspx) in computer Windows e Linux gestiti da SCOM.  Gli agenti si connettono troppo[server di gestione](https://technet.microsoft.com/library/hh301922.aspx) che comunicano con hello SCOM database e del data warehouse.  Gli agenti si basano su server toomanagement tooconnect l'autenticazione di dominio.  Quelli all'esterno di un dominio trusted può eseguire l'autenticazione del certificato o connettersi tooa [Server Gateway](https://technet.microsoft.com/library/hh212823.aspx).

SCOM richiede due database SQL, uno per i dati operativi e un altro warehouse toosupport reporting e i dati analisi dei dati.  Oggetto [Reporting Server](https://technet.microsoft.com/library/hh298611.aspx) esegue tooreport SQL Reporting Services su dati dal data warehouse di hello. 

SCOM può monitorare le risorse cloud usando i Management Pack per prodotti come [Azure](https://www.microsoft.com/download/details.aspx?id=38414), [Office 365](https://www.microsoft.com/download/details.aspx?id=43708) e [AWS](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/AWSManagementPack.html).  Questi management pack utilizzare uno o più agenti locali come proxy per l'individuazione del cloud di risorse e l'esecuzione di flussi di lavoro toomeasure delle prestazioni e disponibilità.  Gli agenti proxy vengono inoltre utilizzati troppo[monitorare dispositivi di rete](https://technet.microsoft.com/library/hh212935.aspx) e altre risorse esterne.

Hello Console operatore è un'applicazione Windows che si connette tooone hello dei server di gestione e consente tooview amministratore hello e analizza i dati raccolti e configura l'ambiente SCOM hello.  Una console basata sul Web può essere ospitata da un server IIS e offre l'analisi dei dati tramite un browser.

![Architettura SCOM](media/operations-management-suite-monitoring-product-comparison/scom-architecture.png)

### <a name="log-analytics"></a>Log Analytics
La maggior parte dei componenti di OMS sono nel cloud di Azure hello è possibile distribuire e gestire con un costo minimo e di lavoro di amministrazione.  Tutti i dati raccolti da Log Analitica vengono archiviati nel repository OMS hello.

Log Analytics può raccogliere dati da una delle tre origini seguenti:

* Macchine fisiche e virtuali che eseguono Windows e hello [Microsoft Monitoring Agent (MMA)](https://technet.microsoft.com/library/mt484108.aspx) o Linux e hello [agente Operations Management Suite per Linux](https://technet.microsoft.com/library/mt622052.aspx).  Questi computer possono essere locali oppure macchine virtuali in Azure o in un altro cloud.
* Un account di archiviazione di Azure con dati di [Diagnostica di Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) raccolti dalla macchina virtuale, dal ruolo Web o dal ruolo di lavoro di Azure.
* [Gruppo di gestione SCOM tooa connessione](https://technet.microsoft.com/library/mt484104.aspx).  In questa configurazione, gli agenti di hello comunicano con i server di gestione di SCOM che offrono un database SCOM toohello dati hello in cui viene quindi recapitato toohello archivio dati OMS.
  Gli amministratori di analizzare i dati raccolti e configurare Log Analitica con il portale OMS hello cui è ospitato in Azure ed è possibile accedervi da qualsiasi browser.  App per dispositivi mobili tooaccess questi dati sono disponibili per le piattaforme standard hello.

![Architettura di Log Analytics](media/operations-management-suite-monitoring-product-comparison/log-analytics-architecture.png)

### <a name="integrating-scom-and-log-analytics"></a>Integrazione di SCOM e Log Analytics
Quando SCOM viene utilizzato come origine dati per i Log Analitica è possibile sfruttare le funzionalità di hello di entrambi i prodotti in un ambiente ibrido ambiente di monitoraggio.  È possibile configurare gli agenti SCOM esistenti tramite toobe Operations Console hello gestiti da OMS, inoltre toocontinuing toorun management pack da SCOM.  
I dati da un gruppo di gestione SCOM connesso vengono recapitati tooLog Analitica utilizzando uno dei quattro metodi:

* Gli eventi e i dati sulle prestazioni vengono raccolti dall'agente hello e recapitati tooSCOM.  Server di gestione SCOM offrono quindi hello dati tooLog Analitica.
* Alcuni eventi, ad esempio i log di IIS e gli eventi di sicurezza continuano toobe consegnati direttamente tooLog Analitica dall'agente hello.
* Alcune soluzioni verranno recapitare agente toohello software aggiuntivo o richiedere che i software sia installato toocollect ulteriori dati.  Questi dati verranno in genere essere inviati direttamente tooLog Analitica.
* Alcune soluzioni verranno raccolti dati direttamente dal server di gestione di SCOM che non provengono da agente hello.  Ad esempio, hello [soluzione Alert Management](https://technet.microsoft.com/library/mt484092.aspx) raccoglie gli avvisi da SCOM dopo che sono state create.

## <a name="monitoring-logic"></a>Logica di monitoraggio
SCOM e Analitica Log funzionano con dati simili raccolti dagli agenti, ma presentano differenze fondamentali come definire e implementare la logica per la raccolta dati e la modalità che analizzano i dati di hello raccolti.

### <a name="operations-manager"></a>Operations Manager
Logica di monitoraggio per SCOM è implementato in [management pack](https://technet.microsoft.com/library/hh457558.aspx) che contiene la logica per l'individuazione dei componenti toomonitor, misurare l'integrità di hello sui componenti e per la raccolta dei dati tooanalyze.  Il monitoraggio dei dati può essere semplice quanto la raccolta di un contatore delle prestazioni o degli eventi oppure può usare una logica complessa implementata in uno script.  Sono disponibili per un'ampia gamma di Management Pack che includono il monitoraggio completo [applicazioni Microsoft e di terze parti](http://go.microsoft.com/fwlink/?LinkId=82105) nei dispositivi di rete e toohardware aggiunta.  È possibile [creare i propri Management Pack](http://aka.ms/mpauthor) per applicazioni personalizzate.

Management Pack contengono più flussi di lavoro che eseguono ciascuna una funzione di monitoraggio distinct, ad esempio un contatore delle prestazioni, la verifica dello stato di hello di un servizio oppure eseguire uno script.  Ogni flusso di lavoro viene eseguito in modo indipendente e definisce i propri risultati, ad esempio il database a cui verrà scritta tooand se verrà generato un avviso. 

È possibile ignorare i dettagli del flusso di lavoro, ad esempio frequenza hello che vengono eseguiti, soglia hello in cui è considerato un errore e hello alla gravità dell'avviso hello che generano.  È anche possibile fornire altre funzionalità aggiungendo i propri flussi di lavoro.

![Override](media/operations-management-suite-monitoring-product-comparison/scom-overrides.png)

Management Pack vengono installati nel database di Operations Manager hello e distribuito automaticamente tooagents dai server di gestione.  Ogni agente verrà automaticamente di scaricare i management pack e caricare i flussi di lavoro toohello pertinenti applicazioni installati.  Dati raccolti dall'agente hello viene recapitati toohello indietro i server di gestione per l'inserimento in hello SCOM database e del data warehouse.  Hello Console operatore consente tooview e analizzare i dati tramite i report inclusi nel management pack di hello, dashboard e visualizzazioni personalizzate.

come illustrata nel seguente diagramma hello distribuzione Hello dei management pack.

![Flusso di Management Pack](media/operations-management-suite-monitoring-product-comparison/scom-mpflow.png)

### <a name="log-analytics"></a>Log Analytics
#### <a name="event-and-performance-collection"></a>Raccolta di eventi e prestazioni
Log Analytics raccoglie gli eventi e i contatori delle prestazioni dai sistemi degli agenti, usando origini come il registro eventi di Windows, i log di IIS e Syslog.  È possibile definire i criteri per il quale i dati vengono raccolti tramite il portale di Log Analitica hello e quindi creare le query Log tooanalyze hello raccolti dati.  Un set di criteri standard viene definito quando si crea l'area di lavoro di OMS ed è possibile definire dati aggiuntivi per applicazioni specifiche. 

![Definizione di registri eventi in Log Analytics](media/operations-management-suite-monitoring-product-comparison/log-analytics-definedata.png)

Sebbene SCOM dispone di numerosi flussi di lavoro dettagliati che in genere definiscono i criteri specifici per i dati e azione hello che deve essere eseguita in risposta, Log Analitica con criteri più generale per la raccolta dati.  Query log e le soluzioni offrono più criteri di destinazione per l'analisi e dati specifici nel cloud hello che vengono raccolte.

#### <a name="solutions"></a>Soluzioni
Le soluzioni forniscono la logica aggiuntiva per la raccolta e l'analisi dei dati.  È possibile selezionare le soluzioni tooadd tooyour OMS sottoscrizione dalla raccolta di soluzioni hello.

![Raccolta soluzioni](media/operations-management-suite-monitoring-product-comparison/log-analytics-solutiongallery.png)

Le soluzioni vengono eseguite principalmente nel cloud hello fornendo un'analisi degli eventi e contatori delle prestazioni raccolti nel repository OMS hello.  Possono anche definire toobe dati aggiuntivi che può essere analizzati con query Log o tramite l'interfaccia utente aggiuntive fornite dalla soluzione hello nel dashboard OMS hello raccolti. 

Ad esempio, hello [soluzione Change Tracking](https://technet.microsoft.com/library/mt484099.aspx) rileva modifiche nei sistemi degli agenti e scrive gli eventi toohello OMS repository che possono essere analizzati con più visualizzazioni grafiche che riepilogano ha rilevato modifiche di configurazione.  Possibile drill-down dalla vista hello riepilogato query log hello tale visualizzazione in dettaglio i dati raccolti dalla soluzione hello.

Mentre è possibile selezionare quali soluzioni si aggiunge la sottoscrizione tooyour, non è attualmente necessario hello possibilità toocreate soluzioni personalizzate.  È possibile selezionare gli eventi di hello e toocollect i contatori delle prestazioni e creare visualizzazioni personalizzate in base alle proprie query log.

logica di monitoraggio per Log Analitica Hello viene riepilogata in hello seguente diagramma.

![Flusso di soluzioni di Log Analytics](media/operations-management-suite-monitoring-product-comparison/log-analytics-solution-flow.png)

## <a name="health-monitoring"></a>Monitoraggio dell'integrità
### <a name="operations-manager"></a>Operations Manager
SCOM può modellare hello componenti diversi dell'applicazione e forniscono un sistema in tempo reale per ogni.  In questo modo si toonot solo Vista ha rilevato errori e le prestazioni nel tempo, ma anche toovalidate hello integrità effettivo di un'applicazione o di sistema e ciascuno dei relativi componenti in un determinato momento.  Poiché hello riconosce i periodi di tempo che un'applicazione è disponibile, il motore di integrità hello in SCOM supporta anche accordi di livello di servizio (SLA) quale analizzare e generare rapporti sulla disponibilità hello di un'applicazione nel tempo.

Ad esempio, visualizzazione hello seguente mostra integrità in tempo reale di hello motori di database SQL monitorati da SCOM.  integrità Hello di ogni database hello per uno dei motori di database hello viene visualizzato nella parte inferiore di hello metà della vista hello.

![Vista di stato](media/operations-management-suite-monitoring-product-comparison/scom-state-view.png)

Esplora stati per uno dei motori di database hello Hello è illustrato di seguito con monitoraggio hello che viene utilizzati toodetermine l'integrità complessiva.  Questi monitoraggi sono definiti nel management pack di SQL hello ed eseguire tutti i motori di database SQL individuati da SCOM.

![Esplora stati](media/operations-management-suite-monitoring-product-comparison/scom-health-explorer.png)

I componenti su più sistemi possono essere combinati toomeasure hello integrità di un'applicazione distribuita.  Questo può essere particolarmente utile per le applicazioni line-of-business che includono più componenti distribuiti.  È possibile creare un modello di integrità hello di ogni componente di rollup in disponibilità per un'applicazione hello.

Active Directory è un esempio di un management pack che fornisce un modello tooanalyze relativi componenti distribuiti.  diagramma di esempio Hello riportato di seguito mostra hello integrità hello ambiente generale e relazione hello tra foreste, domini e controller di dominio.  Ognuno di questi componenti sono inclusi i componenti secondari e simili toohello SQL esempio monitor multipli.

![Vista diagramma SCOM](media/operations-management-suite-monitoring-product-comparison/scom-diagram-view.png)

### <a name="log-analytics"></a>Log Analytics
OMS non includono un applicazioni toomodel motore comuni o misurare lo stato di integrità in tempo reale.  Le singole soluzioni possono valutare hello integrità complessiva di determinati servizi in base ai dati raccolti e sull'analisi in tempo reale di hello agente tooperform può installare logica personalizzata.  Poiché le soluzioni vengono eseguiti nel cloud hello con repository OMS toohello di accesso, forniscono spesso un'analisi più approfondita rispetto a è in genere eseguite dai management pack. 

Ad esempio, hello [soluzioni AD Assessment e SQL Assessment](https://technet.microsoft.com/library/mt484102.aspx) analizzare i dati raccolti e fornire una valutazione per diversi aspetti dell'ambiente di hello.  Sono incluse indicazioni per i miglioramenti che possono essere effettuati tooimprove hello disponibilità e prestazioni dell'ambiente hello.

![Soluzioni di valutazione di AD](media/operations-management-suite-monitoring-product-comparison/log-analytics-ad-assessment.png)

## <a name="data-analysis"></a>Analisi dei dati
SCOM e Analitica di Log forniscono diverse funzionalità tooanalyze raccolti dati.  SCOM con viste e dashboard in hello Operations Console per l'analisi dei dati più recenti in un'ampia gamma di formati e i report per presentare i dati di data warehouse di hello in formato tabulare.  Log Analitica fornisce un'interfaccia e il linguaggio di query log completo per l'analisi dei dati nel repository OMS hello.  Quando SCOM viene utilizzato come origine dati per i Log Analitica, repository hello include i dati raccolti da SCOM pertanto strumenti Log Analitica hello possono essere dati tooanalyze utilizzati da entrambi i sistemi.

### <a name="operations-manager"></a>Operations Manager
#### <a name="views"></a>Visualizzazioni
Le viste in Operations Console hello consentono tooview diversi tipi di dati raccolti da SCOM in formati diversi, in genere in formato tabulare per grafici a linee per i dati sulle prestazioni e dati dello stato, avvisi ed eventi.  Visualizzazioni eseguono analisi minimo o il consolidamento dei dati hello ma consentono di toofilter in base a criteri tooparticular. 

![Visualizzazioni](media/operations-management-suite-monitoring-product-comparison/scom-views.png)

Management Pack in genere forniscono supporto applicazione hello o sistema che esegue il monitoraggio di più visualizzazioni.  Questo può includere visualizzazioni stato per oggetti diversi hello individuati dal management pack di hello, viste avvisi per problemi rilevati e le viste per i contatori delle prestazioni.

Le visualizzazioni sono particolarmente adatti per l'analisi di stato corrente di hello dell'ambiente hello inclusi gli avvisi aperti e lo stato di integrità hello degli oggetti e sistemi monitorati.  È possibile drill-down dei dati di evento o alle prestazioni toodetailed supporto di un avviso particolare in ordine toodiagnose alla causa radice. Analogamente, è possibile visualizzare hello prestazioni e l'integrità dei diversi componenti di un'applicazione di tooassess il relativo stato di integrità corrente.

#### <a name="dashboards"></a>Dashboard
Dashboard nella Console operatore di lavoro principalmente con hello hello stessi dati, viste, ma sono più personalizzabili e possono includere visualizzazioni più dettagliate.  È disponibile un set di dashboard standard che è possibile personalizzare facilmente per le proprie esigenze.  È anche possibile usare un widget di PowerShell che può visualizzare i dati restituiti da una query di PowerShell.

![Dashboard](media/operations-management-suite-monitoring-product-comparison/scom-dashboard.png)

Gli sviluppatori devono toodashboards di hello possibilità tooadd componenti personalizzati che includono i management pack.  Queste possono essere estremamente specializzata tooa particolare applicazione, ad esempio dashboard hello in hello management pack di SQL illustrato di seguito.  Questo dashboard può anche essere usato come modello per le versioni personalizzate.

![Dashboard di SQL](media/operations-management-suite-monitoring-product-comparison/scom-sql-dashboard.png)

#### <a name="reports"></a>Report
I report in SCOM analizzare i dati dal data warehouse di hello in formato tabulare.  È possibile stamparli e pianificarne il recapito automatizzato in formati di file diversi, inclusi PDF, CSV e Word.  I report funzionano con i dati dal data warehouse di hello in modo che siano particolarmente adatti per l'analisi delle tendenze a lungo termine.

I Management Pack forniscono in genere report personalizzati per una determinata applicazione.  È anche possibile selezionare un report da una raccolta report di generici che è possibile personalizzare per le proprie applicazioni o per l'esecuzione di un'analisi ad hoc.

Di seguito è un report di prestazioni di esempio che mostra i dati raccolti da hello Management Pack di Active Directory.

![Report](media/operations-management-suite-monitoring-product-comparison/scom-report.png)

### <a name="log-analytics"></a>Log Analytics
Log Analitica ha un [il linguaggio di query](https://technet.microsoft.com/library/mt484120.aspx) che è possibile utilizzare analysis tooperform tra dati provenienti da più applicazioni senza hello necessità toocreate una visualizzazione personalizzata o un report.  Poiché OMS viene implementato nel cloud hello, le prestazioni delle query e analisi dei dati non sono limitazioni hardware tooany di soggetto e possono analizzare rapidamente le query incluse milioni di record. 

Le query in Log Analitica sono anche altre funzionalità di base per hello.  Si può salvare una query, esportare tooExcel relativi risultati o automaticamente di eseguire a intervalli regolari e generare un avviso se i risultati corrispondono a determinati criteri.  

![Flusso di query di log](media/operations-management-suite-monitoring-product-comparison/log-analytics-query-flow.png)

Di seguito è riportato un esempio di una query di Log Analytics.  In questo esempio tutti gli eventi con "avviato" nel nome hello vengono restituiti e raggruppati per l'evento ID.  utente Hello fornisce semplicemente query hello e Analitica Log generati in modo dinamico l'analisi di hello tooperform dell'interfaccia utente hello.  Gli elementi selezionati nell'elenco di hello restituirà hello in dettaglio i dati di evento.

![Query di log](media/operations-management-suite-monitoring-product-comparison/log-analytics-query.png)

Inoltre tooproviding analisi ad hoc, le query in Analitica Log possono essere salvate per utilizzi futuri e anche aggiunto tooyour [dashboard OMS](http://technet.microsoft.com/library/mt484090.aspx) come illustrato nell'esempio seguente hello.

![dashboard OMS](media/operations-management-suite-monitoring-product-comparison/log-analytics-dashboard.png)

## <a name="next-steps"></a>Passaggi successivi
* Distribuire [System Center Operations Manager (SCOM)](https://technet.microsoft.com/library/hh205987.aspx).
* Iscriviti a [Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics).  


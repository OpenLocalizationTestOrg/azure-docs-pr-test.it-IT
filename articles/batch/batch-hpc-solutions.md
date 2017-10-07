---
title: aaaBatch e soluzioni HPC nel cloud hello - Azure | Documenti Microsoft
description: Informazioni sugli scenari Batch e High Performance Computing (HPC e Big Compute) e sulle opzioni per le soluzioni in Azure
services: batch, virtual-machines, cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: aab5401d-2baf-4cf2-bf20-ad224de33888
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c5a3c8859d1f95040bcdad15942a815d71eb4486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="batch-and-hpc-solutions-for-large-scale-computing-workloads"></a>Batch e soluzioni HPC per carichi di lavoro di elaborazione su larga scala

Azure offre soluzioni cloud scalabili ed efficienti per batch computing e high performance computing (HPC), dette anche *Big Compute*. Vedere di seguito i carichi di lavoro Big Compute e toosupport di servizi di Azure li oppure passare direttamente troppo[scenari della soluzione](#scenarios) più avanti in questo articolo. In questo articolo è principalmente per fornitori di software indipendenti, ai responsabili IT e responsabili delle decisioni tecniche, ma altri professionisti IT e sviluppatori possono utilizzare toofamiliarize it autonomamente con queste soluzioni.

Le organizzazioni hanno problemi di elaborazione su larga scala: progettazione tecnica e analisi, rendering delle immagini, modellazione complessa, simulazioni Monte Carlo, calcoli di valutazione dei rischi finanziari e altri ancora. Azure consente alle organizzazioni di risolvere questi problemi con risorse hello, scala e alla pianificazione di che cui necessitano. Con Azure, le organizzazioni possono:

* Creare soluzioni ibride, estensione di un cloud di toohello di on-premise HPC cluster toooffload punta carichi di lavoro
* Eseguire carichi di lavoro e strumenti di cluster HPC interamente in Azure
* Utilizzare i servizi di Azure gestiti e scalabili, ad esempio [Batch](https://azure.microsoft.com/documentation/services/batch/) toorun i carichi di lavoro con utilizzo intensivo di calcolo senza toodeploy e gestire l'infrastruttura di calcolo

Sebbene esula hello in questo articolo, Azure fornisce inoltre agli sviluppatori e i partner un set completo di funzionalità, opzioni di architettura e sviluppo strumenti toobuild su larga scala, personalizzato Big Compute flussi di lavoro. È un ecosistema di partner crescente toohelp pronto rendere i carichi di lavoro Big Compute produttivo hello cloud di Azure.

## <a name="batch-and-hpc-applications"></a>Applicazioni Batch e HPC
A differenza delle applicazioni Web e molte applicazioni line-of-business, le applicazioni Batch e HPC presentano un inizio e una fine definiti e possono essere eseguite in base a una pianificazione o su richiesta, talvolta per ore o anche di più. La maggior parte rientrano in due categorie principali: *intrinsecamente parallele* (detta anche "imbarazzantemente parallela", perché vengono risolti i problemi di hello prestano toorunning in parallelo in più computer o processori) e *accoppiamento*. Vedere hello nella tabella seguente per ulteriori informazioni su questi tipi di applicazioni. Alcune soluzioni Azure si avvicina a lavoro migliore per un tipo o altri hello.

> [!NOTE]
> Nelle soluzioni Batch e HPC, un'istanza in esecuzione di un'applicazione viene in genere denominata *processo* e ogni processo può essere suddiviso in *attività*. E hello risorse di cluster di calcolo per un'applicazione hello vengono spesso denominate *nodi di calcolo*.
> 
> 

| Tipo | Caratteristiche | esempi |
| --- | --- | --- |
| **Intrinsecamente parallela**<br/><br/>![Intrinsecamente parallela][parallel] |• Singoli computer seguono la logica dell'applicazione in modo indipendente<br/><br/> • Aggiunta computer consente hello applicazione tooscale e diminuire il tempo di calcolo<br/><br/>• L'applicazione è costituita da file eseguibili separati oppure è suddivisa in un gruppo di servizi richiamati da un client (un'architettura orientata al servizio o applicazione SOA) |• Modellazione del rischio finanziario<br/><br/>• Rendering ed elaborazione di immagini<br/><br/>• Codifica e transcodifica multimediale<br/><br/>• Simulazioni Monte Carlo<br/><br/>• Test del Software |
| **Tightly coupled**<br/><br/>![Tightly coupled][coupled] |• Applicazione richiede calcolo nodi toointeract o exchange i risultati intermedi<br/><br/>• Calcolo nodi possono avvenire tramite hello interfaccia MPI (Message Passing), un protocollo di comunicazione comune per il calcolo parallelo<br/><br/>• un'applicazione hello è la larghezza di banda e latenza toonetwork sensibili<br/><br/>• Le prestazioni dell'applicazione possono essere migliorate con tecnologie di rete ad alta velocità, come InfiniBand e l'accesso diretto a memoria remota (RDMA) |• Modellazione di serbatoi per petrolio e gas di <br/><br/>• Progettazione tecnica e analisi, ad esempio fluidodinamica computazionale<br/><br/>• Simulazioni fisiche, ad esempio incidenti stradali e reazioni nucleari<br/><br/>• Previsioni meteorologiche |

### <a name="considerations-for-running-batch-and-hpc-applications-in-hello-cloud"></a>Considerazioni per l'esecuzione batch e le applicazioni HPC nel cloud hello
È possibile eseguire facilmente la migrazione di molte applicazioni che vengono progettati toorun tooAzure di cluster HPC locale o ambiente ibrido (cross-premise) tooa. Tuttavia, vi possono essere alcune limitazioni o considerazioni, tra cui:

* **Disponibilità di risorse cloud** -in base al tipo hello di utilizzare le risorse di calcolo cloud, potrebbe non essere in grado di toorely sulla disponibilità continua del computer durante l'esecuzione di un processo. Stato di avanzamento e la gestione dello stato verificare che punta è comuni tecniche toohandle possibili errori temporanei e più necessarie quando si usano risorse cloud.
* **Accesso ai dati** -tecniche di accesso ai dati comunemente disponibili in cluster aziendali, ad esempio NFS, potrebbero richiedere una configurazione speciale nel cloud hello. In alternativa, potrebbe essere necessario per il cloud hello procedure di accesso tooadopt dati diversi e modelli.
* **Lo spostamento dei dati** : per le applicazioni che processo grandi quantità di dati, strategie siano necessari toomove hello dati in risorse di archiviazione e toocompute cloud. Potrebbe essere necessaria una rete cross-premise ad alta velocità, come [Azure ExpressRoute](https://azure.microsoft.com/services/expressroute/). Prendere inoltre in considerazione le limitazioni legali, normative o le limitazioni di criteri per l'archiviazione o l'accesso a tali dati.
* **Gestione delle licenze** : rivolgersi al fornitore dell'hello di qualsiasi applicazione commerciale per le licenze o altre restrizioni per l'esecuzione in hello cloud. Non tutti i fornitori offrono licenze con pagamento in base al consumo. È possibile per la soluzione necessaria tooplan per un server di gestione licenze nel cloud hello o connettersi a server licenze di tooan locale.

### <a name="big-compute-or-big-data"></a>Big Compute o Big Data?
non è sempre crittografato Hello linea tra le applicazioni Big Compute e Big Data di separazione e alcune applicazioni possono presentare caratteristiche di entrambi. Entrambe prevedono l'esecuzione di calcoli su larga scala, in genere in cluster di computer. Ma hello soluzione approcci e gli strumenti di supporto possono essere diversi.

• **Big Compute** tende tooinvolve applicazioni che si basano sulla potenza della CPU e memoria, ad esempio simulazioni tecniche, modellazione, valutazione dei rischi finanziari e rendering digitale. infrastruttura di Hello per una soluzione Big Compute potrebbe includere i computer con processori multicore specializzati calcolo non elaborato di tooperform e specializzato, ad alta velocità rete hardware tooconnect hello.

• **Big Data**: risolve i problemi di analisi dei dati che prevedono grandi quantità di dati che non possono essere gestite da un singolo computer o un sistema di gestione database, ad esempio volumi elevati di log Web o altri dati di business intelligence. Big Data tende toorely più sulla capacità del disco e sulle prestazioni dei / o sulla potenza della CPU. Sono inoltre strumenti di Big Data specifici come Apache Hadoop toomanage hello cluster e per partizionare dati hello. Per informazioni su Azure HDInsight e altre soluzioni di Azure Hadoop, vedere [Hadoop](https://azure.microsoft.com/solutions/hadoop/).

## <a name="compute-management-and-job-scheduling"></a>Gestione del calcolo e pianificazione dei processi
L'esecuzione di Batch e HPC applicazioni spesso include un *Gestione cluster di* e *pianificatore di processi* toohelp gestire le risorse di calcolo in cluster e allocarli toohello applicazioni che eseguono processi hello. Queste funzioni possono essere eseguite da strumenti separati o da uno strumento o un servizio integrato.

* **Gestione cluster** : effettua il provisioning, rilascia e gestisce le risorse di calcolo (o nodi di calcolo). Gestione cluster di è possibile automatizzare l'installazione di immagini del sistema operativo e le applicazioni nei nodi di calcolo, scalare le risorse di calcolo in base toodemands e monitorare le prestazioni di hello dei nodi di hello.
* **Utilità di pianificazione di processo** -specifica hello risorse, quali processori o memoria, un'applicazione esigenze e hello condizioni quando è in esecuzione. Un'utilità di pianificazione di processo gestisce una coda dei processi e alloca le risorse toothem in base alle priorità assegnata o ad altre caratteristiche.

Clustering e strumenti per i cluster di Windows e Linux di pianificazione dei processi possono eseguire la migrazione ben tooAzure. Ad esempio, [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029), la soluzione cluster di elaborazione gratuita di Microsoft per carichi di lavoro HPC Windows e Linux, offre diverse opzioni per l'esecuzione in Azure. È anche possibile creare cluster Linux strumenti open source di toorun come coppia e SLURM. È anche possibile visualizzare tooAzure soluzioni griglia commerciale, ad esempio [TIBCO DataSynapse GridServer](https://azure.microsoft.com/blog/tibco-datasynapse-comes-to-the-azure-marketplace/), [sala spettro IBM e n LSF](https://azure.microsoft.com/blog/ibm-and-microsoft-azure-support-spectrum-symphony-and-spectrum-lsf/), e [Univa griglia motore](http://www.univa.com/products/grid-engine).

Come illustrato nelle sezioni che seguono hello, è anche possibile sfruttare i vantaggi di servizi di Azure toomanage risorse di calcolo e pianificare gli strumenti di gestione di cluster tradizionali processi senza (o in aggiunta a).

## <a name="scenarios"></a>Scenari
Ecco tre scenari comuni toorun carichi di lavoro di Big Compute in Azure con soluzioni di cluster HPC esistenti, servizi di Azure o una combinazione di due hello. Sono elencate le considerazioni fondamentali per la scelta di ogni scenario, che però non sono esaustive. Più su hello disponibili servizi di Azure che è possibile utilizzare nella soluzione sono successivo nell'articolo hello.

| Scenario | Perché sceglierlo |
| --- | --- | --- |
| **Potenziamento un tooAzure cluster HPC**<br/><br/>[![Cluster burst][burst_cluster]](./media/batch-hpc-solutions/burst_cluster.png) <br/><br/> Altre informazioni:<br/>• [Potenziamento tooAzure istanze di lavoro con HPC Pack](https://technet.microsoft.com/library/gg481749.aspx)<br/><br/>• [Configurare un cluster di elaborazione ibrido con HPC Pack](../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)<br/><br/>• [Potenziamento tooAzure Batch con HPC Pack](https://technet.microsoft.com/library/mt612877.aspx)<br/><br/> |• Combinare [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) o un altro cluster locale con altre risorse di Azure in una soluzione ibrida.<br/><br/>• Estendere il toorun di carichi di lavoro Big Compute su piattaforma come istanze di macchine virtuali (attualmente solo Windows Server) un servizio (PaaS).<br/><br/>• Accedere a un archivio dati o un server licenze locale tramite una rete virtuale di Azure facoltativa |
| **Creare un cluster HPC interamente in Azure**<br/><br/>[![Cluster in IaaS][iaas_cluster]](./media/batch-hpc-solutions/iaas_cluster.png)<br/><br/>Altre informazioni:<br/>• [Soluzioni cluster HPC in Azure](big-compute-resources.md)<br/><br/> |• Distribuire rapidamente e in modo coerente applicazioni e strumenti cluster in macchine virtuali di infrastruttura distribuita come servizio (IaaS) Windows o Linux standard o personalizzate.<br/><br/>• Eseguire diversi carichi di lavoro Big Compute tramite la soluzione scelta di pianificazione dei processi hello.<br/><br/>• Utilizzare servizi di Azure aggiuntivi inclusi rete e archiviazione toocreate basato su cloud soluzioni complete. |
| **Scalabilità orizzontale tooAzure un'applicazione parallela**<br/><br/>[![Azure Batch][batch_proc]](./media/batch-hpc-solutions/batch_proc.png)<br/><br/>Altre informazioni:<br/>• [Nozioni di base su Azure Batch](batch-technical-overview.md)<br/><br/>• [Introduzione alla libreria di Azure Batch hello per .NET](batch-dotnet-get-started.md) |• Sviluppare con [Azure Batch](https://azure.microsoft.com/documentation/services/batch/) tooscale out vari toorun di carichi di lavoro di Big Compute nel pool di macchine virtuali di Windows o Linux.<br/><br/>• Usare un toomanage la distribuzione del servizio di piattaforma Azure e il ridimensionamento automatico delle macchine virtuali, una pianificazione di processi, il ripristino di emergenza, lo spostamento dei dati, la gestione delle dipendenze e distribuzione dell'applicazione. |

## <a name="azure-services-for-big-compute"></a>Servizi di Azure per Big Compute
Ecco informazioni sul calcolo hello, dati, rete e servizi correlati che è possibile combinare per soluzioni Big Compute e flussi di lavoro. Per informazioni dettagliate sui servizi di Azure, vedere hello servizi Azure [documentazione](https://azure.microsoft.com/documentation/). Hello [scenari](#scenarios) più indietro in questo articolo mostra solo alcuni modi per usare questi servizi.

> [!NOTE]
> Azure introduce regolarmente nuovi servizi che possono risultare utili per il proprio scenario. In caso di domande, contattare un [partner Azure](https://pinpoint.microsoft.com/en-US/search?keyword=azure) o inviare un messaggio di posta elettronica all'indirizzo *bigcompute@microsoft.com*.
> 
> 

### <a name="compute-services"></a>Servizi di calcolo
Servizi di calcolo di Azure sono core hello di una soluzione Big Compute e hello calcolo diversi servizi offerta vantaggi per i diversi scenari. A livello di base, questi servizi offrono modalità diverse per applicazioni toorun nelle istanze di calcolo basate sulla macchina virtuale forniti da Azure tramite la tecnologia Hyper-V di Windows Server. Queste istanze possono eseguire strumenti e sistemi operativi Linux e Windows standard e personalizzati. Azure offre un'ampia gamma di [dimensioni delle istanze](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) con diverse configurazioni di core CPU, memoria, capacità del disco e altre caratteristiche. A seconda delle esigenze, è possibile ridimensionare hello istanze toothousands di core e quindi ridimensionare verso il basso quando è necessario un numero inferiore di risorse.

> [!NOTE]
> Sfruttare i vantaggi di hello Azure [le istanze con utilizzo intensivo di calcolo, ad esempio hello H serie](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooimprove hello prestazioni e scalabilità dei carichi di lavoro HPC. Queste istanze supportano anche applicazioni MPI parallele che richiedono una rete di applicazione a bassa latenza e a velocità elevata. Inoltre sono disponibile [N serie](../virtual-machines/windows/sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) le macchine virtuali con intervallo di hello GPU NVIDIA tooexpand degli scenari di elaborazione e la visualizzazione in Azure.  
> 
> 

| Service | Descrizione |
| --- | --- |
| **[Macchine virtuali](https://azure.microsoft.com/documentation/services/virtual-machines/)**<br/><br/> |• Forniscono un'infrastruttura distribuita come servizio (IaaS) di calcolo con tecnologia Microsoft Hyper-V<br/><br/>• Consentono di eseguire il provisioning tooflexibly e gestire i computer cloud permanenti da immagini di Windows Server o Linux standard da hello [Azure Marketplace](https://azure.microsoft.com/marketplace/), immagini e i dischi dati è fornire o<br/><br/>• Possono essere distribuite e gestite come [set di scalabilità di macchine Virtuali](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/) toobuild su larga scala servizi dalle macchine virtuali identiche, con capacità di tooincrease o diminuire la scalabilità automatica automaticamente<br/><br/>• Eseguire in locale applicazioni interamente nel cloud hello e strumenti di cluster di calcolo<br/><br/> |
| **[Servizi cloud](https://azure.microsoft.com/documentation/services/cloud-services/)**<br/><br/> |• Possono eseguire applicazioni Big Compute in istanze di ruolo di lavoro, ovvero macchine virtuali su cui è in esecuzione una versione di Windows Server e gestite completamente da Azure<br/><br/>• Consentono applicazioni scalabili e affidabili con costi generali amministrativi ridotti, eseguite secondo il modello PaaS (piattaforma distribuita come servizio)<br/><br/>• Potrebbero richiedere strumenti aggiuntivi o sviluppo toointegrate con soluzioni di cluster HPC locale |
| **[Batch](https://azure.microsoft.com/documentation/services/batch/)**<br/><br/> |• Esegue carichi di lavoro su larga scala in parallelo e in batch in un servizio completamente gestito<br/><br/>• Garantisce la pianificazione dei processi e il ridimensionamento automatico di un pool gestito di macchine virtuali<br/><br/>• Consente agli sviluppatori toobuild ed eseguire applicazioni come un servizio o abilitare per il cloud le applicazioni esistenti<br/> |

### <a name="storage-services"></a>Servizi di archiviazione
In genere una soluzione Big Compute opera su un set di dati di input e genera dati per i relativi risultati. Alcuni dei servizi di archiviazione di Azure hello utilizzati in soluzioni Big Compute:

* [BLOB, tabelle e archiviazione delle code](https://azure.microsoft.com/documentation/services/storage/) : gestione di grandi quantità di dati non strutturati, dati NoSQL e messaggi per flusso di lavoro e comunicazione, rispettivamente. Ad esempio, è possibile utilizzare l'archiviazione blob per grandi set di dati tecnici o per le immagini di input hello o i processi dell'applicazione di file multimediali. È possibile utilizzare le code per la comunicazione asincrona in una soluzione. Vedere [tooMicrosoft introduzione di archiviazione di Azure](../storage/common/storage-introduction.md).
* [Archiviazione di Azure File](https://azure.microsoft.com/services/storage/files/) -file comuni di condivisioni e i dati in Azure tramite hello protocollo SMB standard, è necessaria per alcune soluzioni di cluster HPC.
* [Archivio Data Lake](https://azure.microsoft.com/services/data-lake-store/) -fornisce un iperscalabile Apache Hadoop Distributed File System per cloud hello, utile per i batch, in tempo reale e analitica interattivo.

### <a name="data-and-analysis-services"></a>Servizi dati e analisi
Alcuni scenari di Big Compute implicano i flussi di dati su larga scala o generano i dati che necessitano di ulteriore elaborazione o analisi. Azure offre diversi servizi dati e analisi, tra cui:

* [Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) : consente la creazione di flussi di lavoro basati sui dati (pipeline) che uniscono, aggregano e trasformano dati di archivi dati locali, basati sul cloud e Internet.
* [Database SQL](https://azure.microsoft.com/documentation/services/sql-database/) -fornisce le funzionalità principali di hello di un sistema di gestione di database relazionali Microsoft SQL Server in un servizio gestito.
* [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/) : consente di distribuire ed esegue il provisioning di cluster Windows Server o Linux basato su Apache Hadoop in hello cloud toomanage, analizzare e report sui big data.
* [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) : consente di creare, testare, usare e gestire soluzioni di analisi predittiva in un servizio completamente gestito.

### <a name="additional-services"></a>Servizi aggiuntivi
La soluzione Big Compute potrebbe essere necessario altri servizi di Azure tooconnect tooresources locale o in altri ambienti. Tra gli esempi sono inclusi:

* [Rete virtuale](https://azure.microsoft.com/documentation/services/virtual-network/) -crea una sezione logicamente isolata in Azure tooconnect risorse di Azure tooeach altri o tooyour locale data center. Con una rete virtuale cross-premise, le applicazioni Big Compute possono accedere ai dati locali, ai servizi Active Directory e ai server licenze.
* [ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) : crea una connessione privata tra i data center Microsoft e l'infrastruttura disponibile localmente o in un ambiente con percorso condiviso. ExpressRoute offre una maggiore sicurezza, più affidabilità, velocità più elevate e minori latenze rispetto alle connessioni rispetto hello Internet.
* [Bus di servizio](https://azure.microsoft.com/documentation/services/service-bus/) -offre diversi meccanismi per applicazioni toocommunicate o lo scambio di dati, se si trovano in Azure, in un'altra piattaforma cloud o in un data center.

## <a name="next-steps"></a>Passaggi successivi
* Vedere [risorse tecniche per Batch e HPC](big-compute-resources.md) toofind informazioni tecniche sulla toobuild la soluzione.
* Esaminare le opzioni di Azure con partner, inclusi Cycle Computing e UberCloud.
* Ottenere informazioni sulle soluzioni Big Compute di Azure offerte da [Towers Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222), [Altair](https://azure.microsoft.com/blog/availability-of-altair-radioss-rdma-on-microsoft-azure/), [ANSYS](https://azure.microsoft.com/blog/ansys-cfd-and-microsoft-azure-perform-the-best-hpc-scalability-in-the-cloud/) e [d3VIEW](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088).
* Per gli annunci più recenti di hello, vedere hello [blog del team di Microsoft HPC e Batch](http://blogs.technet.com/b/windowshpc/) hello e [blog di Azure](https://azure.microsoft.com/blog/tag/hpc/).

<!--Image references-->
[parallel]: ./media/batch-hpc-solutions/parallel.png
[coupled]: ./media/batch-hpc-solutions/coupled.png
[iaas_cluster]: ./media/batch-hpc-solutions/iaas_cluster.png
[burst_cluster]: ./media/batch-hpc-solutions/burst_cluster.png
[batch_proc]: ./media/batch-hpc-solutions/batch_proc.png

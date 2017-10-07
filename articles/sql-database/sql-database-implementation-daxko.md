---
title: aaaAzure SQL Database Azure Case Study - Daxko/CSI | Documenti Microsoft
description: Informazioni sul Daxko/CSI utilizzo tooaccelerate Database SQL relativo ciclo di sviluppo e tooenhance il servizio clienti e delle prestazioni
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 00c8a713-f20c-4d6b-b8b7-0c1b9ba5f05b
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 3e3d58a1d9c3c919fc0e4cdb2765f680719c19d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="daxkocsi-used-azure-tooaccelerate-its-development-cycle-and-tooenhance-its-customer-services-and-performance"></a>Daxko/CSI utilizzato Azure tooaccelerate relativo ciclo di sviluppo e tooenhance il servizio clienti e delle prestazioni
![Logo Daxko/CSI](./media/sql-database-implementation-daxko/csidaxkologo25.png)

Software Daxko/CSI affrontare un problema: la base per i clienti dei centri di idoneità e ricreazione stato grazie toohello successo della soluzione completa di software aziendale rapidamente, in crescita, ma mantenersi hello infrastruttura IT ha bisogno per tale crescita. clientela è il test della società hello personale IT. società Hello è sempre più vincolata dall'overhead di operazioni con aumento, in particolare per la gestione dei relativi database crescente. L'overhead di operazioni è stato ancora peggio, Taglia in risorse di sviluppo di nuove iniziative, ad esempio nuove funzionalità di mobilità per hello software aziendale.

In base tooDavid Molina, direttore di sviluppo del prodotto in Daxko/CSI Azure Software CSI fornito con modello (PaaS) platform-as-a-service di hello necessarie toosimplify gestione di database, aumentare la scalabilità e liberare risorse toofocus in software anziché ops. "Il database SQL di Azure ha rappresentato un'ottima opzione per la nostra azienda. Senza tooworry sulla gestione di SQL Server, un cluster di failover e hello tutte le altre esigenze di infrastruttura è ideale per noi."

Poiché la migrazione tooAzure, CSI Software richiede un personale addetto alle operazioni di toomanage solo due su 600 database del cliente. la società Hello utilizza pool elastici di Database SQL di Azure in base alle dimensioni di database del cliente toomove e necessitano.

Molina continua, "clienti ritenevano hello modificare immediatamente. Prima di adoperare i pool elastici, i clienti registravano occasionalmente timeout e altri problemi durante i picchi di attività. Con Azure pool elastico, essi possono potenziamento in base alle esigenze e utilizzare software hello senza problemi."

Inoltre tooimproving delle prestazioni per i clienti, Azure pool elastici liberate risorse Software CSI toofocus sullo sviluppo di nuovi servizi e funzionalità, anziché gestire operazioni e gestione. Tali risorse IT ha contribuito CSI Software migliorare il software dell'organizzazione, garantendo, SpectrumNG, toohelp coinvolgere membri palestra, migliorare l'efficienza di personale e concedere accesso mobile di personale e i membri per le attività interattive e notifiche in tempo reale.

Azure ha anche contribuito CSI Software accelerare e migliorare lo sviluppo di hello e ciclo di qualità (QA) tramite le opzioni di automazione. Con l'implementazione di Azure della società hello, gestori di compilazione possono creare un pacchetto dei componenti con un semplice clic hello. Come descritto Molina, "come parte del ciclo di rilascio hello, QA è ora in grado di toodeploy tooa di ambiente di test in Azure, che riproduce strettamente stack la produzione. È possibile distribuire le compilazioni immediatamente toovet ambiente di sviluppo tooour cambia. Questo fattore rappresenta per noi una vera conquista, poiché in precedenza non disponevamo di un sistema di parità per i test".

## <a name="offloading-toohello-cloud"></a>Offload toohello cloud
Prima di spostare toohello cloud, CSI Software ha compilato correttamente backup in un data center locale Houston la propria infrastruttura multi-tenant. In formato espanso società hello, riscontrate difficoltà crescenti crescente di acquisto, provisioning e gestione di tutti i componenti hardware hello e software necessari toosupport dai propri clienti. Operazioni toohandle del personale IT è diventato un altro collo di bottiglia che ha portato rallentamento tooa il provisioning di nuove risorse e implementazione di nuovi servizi toocustomers.

Software CSI ha analizzato le opzioni cloud per eliminare le spese generali e concentrarsi sul codice e non più sulle operazioni. società Hello scoperto che molti dei provider di cloud superiore hello solo offrono soluzioni di infrastruttura come servizio (IaaS) che richiedono un elevato IT personale toomanage hello IaaS stack. Fine hello, Software CSI determinato che soluzioni PaaS per Azure hello sono migliore di hello adatta alle proprie esigenze. Viene spiegato Molina "Azure Ottiene software hello di hardware e del sistema insufficiente modo hello, in modo che è possibile concentrarsi sulle offerte del software, riducendo al contempo il sovraccarico del reparto IT."

## <a name="making-hello-transition-tooazure"></a>Rendendo hello transizione tooAzure
Dopo aver selezionato Azure per la soluzione PaaS, CSI Software è stata avviata la migrazione il cloud toohello back-end dell'infrastruttura e i database. TooAzure precedente, i clienti SpectrumNG necessitassero tooinstall un'applicazione client che comunica con un servizio Windows Communication Foundation (WCF) sul back-end hello. In base tooMolina, "anche se alcuni clienti ospitato tutti gli elementi nei propri Data Center, è realizzata multitenant toobe di hello del prodotto. È ospitato tutti gli elementi in un Data Center Houston utilizzando SQL Server come archivio dati hello.

"Offerta prodotto incluso anche un membro orientati portale web (scritto in ASP.net), che era presenza del cliente di toobe progettata con l'etichetta vuoti toomatch hello web e pagine online un API SOAP toosupport hello e qualsiasi integrazione di terze parti."

cloud di Hello migrazione toohello non accettava lungo per l'architettura di hello. In base tooMolina, "maggioranza hello sforzo hello gestiti con la modifica di modalità di hello è leggere informazioni sui file di configurazione, una modifica della stringa di connessione centralizzata, e l'automazione hello packaging, caricamento e la distribuzione ai rilasci."

hello toodevelop compilare automazione, CSI ingegneri usato Azure PowerShell e API REST toocreate i pacchetti e caricarli tooa ambiente di gestione temporanea per il rilascio ogni notte.
Hello complessivo transizione tooan distribuzione basato su cloud di Azure è avvenuta rapidamente e senza problemi per il team IT Software CSI hello. Viene spiegato Molina "In tutti, abbiamo un ambiente beta nel cloud hello entro tre settimane toofour l'aggiunta di progetto hello. Un successo sorprendente la nostra azienda", spiega Molina.

Dopo la configurazione e test hello ambiente, CSI Software ha iniziato la migrazione di clienti. Per i clienti che già utilizzano Software CSI hosting, transizione hello è stato quasi trasparente. Per i clienti di eseguire la migrazione da una distribuzione locale, cloud toohello di migrazione hello ha richiesto tempo aggiuntivo, ma è stata ancora principalmente senza problemi per clienti e CSI Software.

Per i del nuovi clienti, Software CSI personale IT utilizzare hello seguenti tooon-scheda processo li tooAzure:

1. Script di PowerShell Azure vengono utilizzati toospin un nuovo database per il cliente hello. tutti i clienti inizia in una tooensure di livello premium la velocità effettiva sufficiente iniziale per la transizione hello.
2. Se possibile, CSI Software utilizza hello migrazione guidata SQL Azure toomove dati esistenti tooan Database SQL di Azure istanza.
3. Infine, Microsoft SQL Server Integration Services (SSIS) sono utilizzati tooreconcile eventuali discrepanze nei dati di hello o tooperform le operazioni di pulitura di dati come richiesto.

Oggi, circa il 99% dei clienti di CSI Software è ospitato in Azure, in quattro datacenter regionali (centro-settentrionale, centro-meridionale, est e ovest). Con i Data Center nell'area geografica di ogni cliente, la latenza viene mantenuta tooa minimo.

## <a name="azure-elastic-pools-free-up-it-resources"></a>I pool elastici di Aure liberano risorse IT
Diverse funzionalità di Azure ha contribuito a Software CSI MAIUSC dall'infrastruttura e le operazioni funzionalità toobeing con stato attivo e lo sviluppo con stato attivo. Vantaggi principali di hello forse sono stato dal pool elastico.

Al momento, CSI Software fornisce ai clienti circa 550 database. Prima di pool elastico, era difficile toomanage che molti database all'interno di una struttura di livello. Gestori di OPS era tooassign livelli di prestazioni in base alle esigenze di potenziamento hello di clienti, che ha richiesto IT-risorse elevato overhead. Grazie ai pool elastici, i responsabili possono assegnare ai tenant pool Premium o Standard, a seconda delle esigenze, e quindi spostare i clienti in base alle dimensioni e alle esigenze. I clienti ritenevano effetti hello del pool elastico hello quasi immediatamente. prima di pool elastico, clienti hanno riscontrato timeout e altri problemi durante i periodi di utilizzo di burst, ma con il pool elastico, i clienti possono ora picchi di attività in base alle esigenze e potranno continuare a toouse SpectrumNG senza problemi.

## <a name="azure-active-geo-replication-accelerates-reporting"></a>La replica geografica attiva di Azure accelera la creazione di rapporti
Numerosi clienti CSI Software stanno traendo vantaggio dalla replica geografica attiva di Azure. Con la replica geografica attiva, backup toofour database secondari leggibili possono essere configurati in hello aree dei Data Center uguale o diverso. Software CSI si avvalgono di replica geografica attiva in due modi: in primo luogo, i database secondari hello sono disponibili nel caso di hello di un Data Center hello o un'interruzione dell'impossibilità tooconnect toohello database primario; e, in secondo luogo, i database secondari hello siano leggibili e possono essere utilizzato toooffload carichi di lavoro di sola lettura come processi di reporting. Alcuni clienti Software CSI utilizzare tooaccelerate questo vantaggio reporting flussi di lavoro.

## <a name="csi-software-application-logic-and-architecture"></a>Architettura e logica dell'applicazione CSI Software
SpectrumNG usa i ruoli Web. Poiché l'applicazione hello è multi-tenant, un servizio WCF è richiesta di connessione iniziale hello toohandle utilizzati dai clienti. Come stati Molina, "richiesta hello identifica ogni cliente, che quindi consente a compilare una stringa di connessione out tootheir database toodo qualsiasi dobbiamo toodo."

Per il livello di hello web del servizio, CSI Software consente di sfruttare la scalabilità automatica Azure, in base a giorno e l'ora. Le risorse disponibili sono tooaccommodate automaticamente un aumento di utilizzo più elevato durante l'orario di ufficio, in base toohello fuso orario di ogni Data Center regionale. Le risorse vengono inoltre impostati tooscale verso il basso nei fine settimana, quando le esigenze dei clienti sono inferiori.

![Architettura di Daxko/CSI](./media/sql-database-implementation-daxko/figure1.png)

Figura 1. Un ruolo di lavoro dei servizi cloud consente di disegnare dati strutturati dal database SQL di Azure e dati semistrutturati dall'archiviazione di tabelle. Gli utenti SpectrumNG interagiscono con i dati tramite un ruolo Web dei servizi cloud.

## <a name="using-web-apps-and-a-web-plan-tier-for-mobile-apps"></a>Uso di app Web e di un livello di piano Web per le app per dispositivi mobili
Utilizzando il Database SQL di Azure liberare le risorse per il Software CSI tooenable nuove iniziative, tra cui una piattaforma per dispositivi mobili completa basata su un'API personalizzata ospitata nell'App web di Azure. piattaforma Hello consente ai membri palestra e toouse i dispositivi mobili toocheck personale, classi di una cartella di lavoro e ricevere messaggi.

piattaforma Hello Usa tootake architettura orientata ai servizi (SOA) un singolo componente, ad esempio un sistema POS (Point of sale) o un sistema di vendite, spostarlo nel piano di web tooanother entrata hello e girare toosupport un servizio tale componente, lasciando tutti gli altri elementi piano di web Hello originale. Questa funzione offre a CSI Software massima flessibilità e consente di mantenere bassi i costi.

## <a name="azure-lets-csi-software-developers-focus-on-apps-and-services"></a>Azure consente agli sviluppatori Software CSI di concentrarsi su applicazioni e servizi
Database SQL di Azure non è semplicemente un tooSpectrumNG boon clienti, usufruire del servizio di hello veloce e affidabile, è anche un vincente per del CSI Software personale IT e sviluppatori. Grazie all'offload tooAzure ops nel cloud hello, Software CSI ridotto il sovraccarico per le risorse e l'infrastruttura, notevolmente accelerated relativi cicli di sviluppo e non occorre più fornire prestazioni di toooptimize toomicromanage database per il tenant.

## <a name="more-information"></a>Altre informazioni
* toolearn ulteriori informazioni sui pool elastici Azure, vedere [pool elastici](sql-database-elastic-pool.md).
* toolearn informazioni sugli strumenti di database e una scalabilità elastica, vedere [strumenti di database elastico e una scalabilità elastica](sql-database-elastic-scale-get-started.md).
* vedere toolearn più sulla migrazione di un database di SQL Server, vedere [eseguire la migrazione di un tooAzure di database di SQL Server](sql-database-cloud-migrate.md).
* toolearn più sulla replica geografica attiva, vedere [replica geografica attiva](sql-database-geo-replication-overview.md).
* toolearn ulteriori informazioni sui ruoli Web e ruoli di lavoro, vedere [i ruoli di lavoro](../fundamentals-introduction-to-azure.md#compute).    
* toolearn ulteriori informazioni su Azure Service Bus, vedere [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).
* toolearn ulteriori informazioni su scalabilità automatica, vedere [il ridimensionamento di servizi cloud](../cloud-services/cloud-services-how-to-scale.md).


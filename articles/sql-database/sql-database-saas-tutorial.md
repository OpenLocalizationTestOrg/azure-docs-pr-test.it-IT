---
title: aaaDeploy ed esplorare l'applicazione di SaaS Wingtip hello multi-tenant che utilizza Database SQL di Azure | Documenti Microsoft
description: Distribuire ed esplorare hello Wingtip SaaS multi-tenant dell'applicazione, che illustra i modelli di SaaS utilizzando il Database SQL di Azure.
keywords: esercitazione database SQL
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: sstein
ms.openlocfilehash: 7c528ee19472d3b8c7a285b2f86013945e8f4bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-explore-a-multi-tenant-application-that-uses-azure-sql-database---wingtip-saas"></a>Distribuire ed esplorare un'applicazione multi-tenant che utilizza il database SQL di Azure - SaaS Wingtip

In questa esercitazione, si distribuisce ed Esplora l'applicazione SaaS Wingtip hello. un'applicazione Hello utilizza un database-per tenant, modello di applicazione SaaS tooservice più tenant. un'applicazione Hello è tooshowcase progettato le funzionalità di Database SQL di Azure che semplificano l'abilitazione di scenari di SaaS.

Cinque minuti dopo aver fatto clic hello *distribuire tooAzure* pulsante riportato di seguito, dispone di un'applicazione SaaS multi-tenant, utilizzando il Database di SQL, massimo e in esecuzione nel cloud hello. un'applicazione Hello viene distribuita con tre tenant di esempio, ciascuno con il proprio database, tutti distribuiti in un pool elastico SQL. app Hello è distribuito tooyour sottoscrizione di Azure, offrendo tooexplore accesso completo e lavoro con hello singoli componenti dell'applicazione. sono disponibili nel repository WingtipSaaS GitHub hello Hello applicazione origine gestione e codice di script.


In questa esercitazione si apprenderà:

> [!div class="checklist"]

> * Come toodeploy hello applicazione SaaS Wingtip
> * Dove tooget hello codice sorgente dell'applicazione e script di gestione
> * Sui server hello e pool di database che costituiscono l'applicazione hello
> * Come tenant mappati dati tootheir con hello *catalogo*
> * Come tooprovision un nuovo tenant
> * Come toomonitor tenant attività nell'applicazione hello

tooexplore vari SaaS gestione e Progettazione modelli, un [serie di esercitazioni correlate](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials) disponibile che si basano su questa distribuzione iniziale. Durante passando esercitazioni hello, approfondire script hello fornito ed esaminare l'implementazione dei diversi modelli di SaaS hello. Eseguire gli script hello in ogni esercitazione toogain una comprensione più approfondita come tooimplement hello Database SQL di molte funzionalità che semplificano lo sviluppo di applicazioni SaaS.

## <a name="prerequisites"></a>Prerequisiti

toocomplete completamento di questa esercitazione, assicurarsi che i hello seguenti prerequisiti:

* Azure PowerShell è installato. Per informazioni dettagliate, vedere [Introduzione ad Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="deploy-hello-wingtip-saas-application"></a>Distribuire un'applicazione SaaS Wingtip hello

Distribuire app SaaS Wingtip hello:

1. Facendo clic su hello **distribuire tooAzure** apre modello di distribuzione SaaS Wingtip hello toohello portale Azure. modello di Hello richiede due valori di parametro. un nome per un nuovo gruppo di risorse e un nome utente che distingue questa distribuzione da altre distribuzioni di app SaaS Wingtip hello. passaggio successivo Hello fornisce dettagli per l'impostazione di questi valori.

   Verificare che toonote hello valori esatti che si utilizzano, poiché sarà necessario tooenter in una configurazione del file in un secondo momento.

   <a href="http://aka.ms/deploywtpapp" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

1. Immettere i valori dei parametri necessari per la distribuzione di hello:

    > [!IMPORTANT]
    > Alcune impostazioni di autenticazione e per i firewall server sono intenzionalmente non protette a scopo dimostrativo. **Creare un nuovo gruppo di risorse** e non utilizzare gruppi di risorse, server o pool esistenti. Non utilizzare l'applicazione o le risorse che crea per la produzione. Elimina la risorsa gruppo quando si è concluso toostop applicazione hello correlato di fatturazione.

    * **Gruppo di risorse** : selezionare questa opzione **Crea nuovo** e fornire un **nome** per il gruppo di risorse hello. Selezionare un **percorso** dall'elenco a discesa hello.
    * **Utente**: alcune risorse richiedono nomi univoci a livello globale. l'univocità tooensure, ogni volta che si distribuisce un'applicazione hello fornire un valore toodifferentiate risorse create, dalle risorse create da qualsiasi altra distribuzione di applicazioni Wingtip hello. Si consiglia di toouse short **utente** nome, ad esempio le iniziali dell'utente e a un numero (ad esempio, *bg1*) e quindi usare tale nel nome del gruppo di risorse hello (ad esempio, *wingtip-bg1*). Il parametro **Utente** può contenere solo lettere, numeri e trattini (senza spazi). primo e l'ultimo carattere Hello deve essere una lettera o un numero (sono consigliato tutte lettere minuscole).


1. **Distribuire un'applicazione hello**.

    * Fare clic su tooagree toohello termini e condizioni.
    * Fare clic su **Acquista**.

1. Monitorare lo stato di distribuzione, fare clic su **notifiche** (icona del controllo del segnale acustico hello a destra della casella di ricerca hello). Distribuzione hello Wingtip SaaS app richiede circa cinque minuti.

   ![distribuzione completata](media/sql-database-saas-tutorial/succeeded.png)

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a>Scaricare e sbloccare script Wingtip SaaS hello

Durante la distribuzione di un'applicazione hello, scaricare gli script di gestione e codice sorgente hello.

> [!IMPORTANT]
> I contenuti eseguibili (script, DLL) possono essere bloccati da Windows quando si scaricano e si estraggono i file ZIP da un'origine esterna. Durante l'estrazione di script hello da un file zip, è possibile eseguire operazioni di hello seguenti file con estensione zip hello toounblock prima dell'estrazione. In questo modo, gli script hello consentiti toorun.

1. Sfoglia troppo[repository di github Wingtip SaaS hello](https://github.com/Microsoft/WingtipSaaS).
1. Fare clic su **Clona o scarica**.
1. Fare clic su **ZIP di Download** e salvare il file hello.
1. Pulsante destro del mouse hello **WingtipSaaS master.zip** file e selezionare **proprietà**.
1. In hello **generale** , selezionare **Unblock**, fare clic su **applica**.
1. Fare clic su **OK**.
1. Estrarre il file hello.

Gli script si trovano in hello *... \\WingtipSaaS master\\moduli Learning* cartella.

## <a name="update-hello-configuration-file-for-this-deployment"></a>Aggiornare il file di configurazione hello per questa distribuzione

Prima di eseguire qualsiasi script, impostare hello *gruppo di risorse* e *utente* valori **UserConfig.psm1**. Impostare queste variabili toohello valori impostati durante la distribuzione.

1. Apri... \\Moduli learning\\*UserConfig.psm1* in hello *PowerShell ISE*
1. Aggiornamento *ResourceGroupName* e *nome* con valori specifici di hello per la distribuzione (su righe 10 e 11 solo).
1. Salvare le modifiche di hello!

L'impostazione qui semplicemente modo si possono evitare tooupdate questi valori specifici della distribuzione in ogni script.

## <a name="run-hello-application"></a>Eseguire un'applicazione hello

app Hello illustra eventi, ad esempio sale insieme, le associazioni jazz, sportive, che ospitano gli eventi. Eventi registrati come clienti (o tenant) della piattaforma Wingtip hello, per gli eventi toolist un modo semplice e vendono il ticket. Per ogni sessione Ottiene un toomanage app web personalizzati sono elencati i relativi eventi e vendere il ticket, isolato dagli altri tenant e indipendenti. In realtà hello, ogni tenant Ottiene un database SQL distribuito in un pool elastico SQL.

Un centro **Hub eventi** fornisce un elenco di tenant URL tooyour specifica distribuzione.

1. Aprire hello _Hub eventi_ nel web browser: http://events.wtp.&lt; UTENTE&gt;. trafficmanager.net (sostituire con il nome utente della distribuzione):

    ![Hub eventi](media/sql-database-saas-tutorial/events-hub.png)

1. Fare clic su **Fabrikam Jazz Club** in *Events Hub* (Hub eventi).

   ![Events](./media/sql-database-saas-tutorial/fabrikam.png)


distribuzione di hello toocontrol delle richieste in ingresso, hello app utilizza [ *Azure Traffic Manager*](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview). le pagine di eventi Hello, che sono specifici del tenant, richiedono che i nomi di tenant vengono inclusi negli URL hello. Tutti hello tenant URL includono specifici *utente* valore e seguire questo formato: http://events.wtp.&lt; UTENTE&gt;.trafficmanager.net/*fabrikamjazzclub*. app eventi Hello analizza nome tenant hello dall'URL hello e utilizza una chiave tooaccess un catalogo tramite toocreate [ *gestione mappa partizioni*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-scale-shard-map-management). mappe di catalogo Hello hello percorso database toohello chiave del tenant. Hello **Hub eventi** utilizza metadati estesi nel nome del tenant di hello catalogo tooretrieve hello associato a ogni elenco di hello tooprovide database degli URL.

In un ambiente di produzione, si creerà in genere un record DNS CNAME [ *puntare un dominio internet della società* ](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-point-internet-domain) al profilo di gestione traffico hello.

## <a name="start-generating-load-on-hello-tenant-databases"></a>Avviare la generazione di carico sui database tenant hello

Ora che hello app viene distribuita, si inserisce toowork! Hello *Demo LoadGenerator* script di PowerShell avvia un carico di lavoro in esecuzione su tutti i database tenant. carico di lavoro reale Hello in molte applicazioni SaaS è in genere sporadici e imprevedibili. toosimulate questo tipo di carico, il generatore di hello produce un carico distribuito tra tutti i tenant, con picchi casuale per ogni tenant che si verificano a intervalli casuale. Per questo motivo che sono necessari diversi minuti per tooemerge modello di carico hello, è migliore toolet hello generatore per almeno tre o quattro minuti prima di monitoraggio hello caricare.

1. In hello *PowerShell ISE*aprire hello... \\Moduli learning\\utilità\\*Demo LoadGenerator.ps1* script.
1. Premere **F5** per eseguire script hello e avviare il generatore di carico hello (lasciare hello valori predefiniti per ora).

> [!IMPORTANT]
> toorun altri script, aprire una nuova finestra di PowerShell ISE. Generatore di carico Hello è in esecuzione come una serie di processi nella sessione di PowerShell locale. Hello *Demo LoadGenerator.ps1* script avvia hello carico effettivo generatore script viene eseguito come un'attività di primo piano più di una serie di processi in background di generazione del carico. Un processo del generatore di carico viene richiamato per ogni database registrato nel catalogo di hello. i processi di Hello sono in esecuzione nella sessione di PowerShell locale, quindi chiudere la sessione di PowerShell hello Arresta tutti i processi. Se si sospende il computer, la generazione del carico viene messa in pausa e riprende quando si riattiva il computer.

Una volta il generatore di carico hello richiama i processi di generazione del carico per ogni tenant, l'attività di primo piano hello rimane in uno stato di richiamo di processo, in cui viene avviato processi in background aggiuntive per i nuovi tenant che verrà eseguito il provisioning. È possibile utilizzare *Ctrl-C* o premere hello *arrestare* pulsante toostop hello in primo piano attività, ma esistente in background i processi continueranno la generazione di carico in ogni database. Se è necessario toomonitor, controllare i processi in background hello *Get-Job*, *Receive-Job* e *Stop-Job*. Durante l'esecuzione di attività in primo piano hello è possibile utilizzare hello stesso tooexecute di sessione di PowerShell altri script. toorun altri script, aprire una nuova finestra di PowerShell ISE.

Se si desidera toorestart hello carico generatore sessione, ad esempio con parametri diversi, è possibile interrompere attività in primo piano hello e quindi eseguire di nuovo hello *Demo LoadGenerator.ps1* script. Eseguire di nuovo *Demo LoadGenerator.ps1* innanzitutto interrompe le attualmente in esecuzione processi e quindi generatore hello riavvii che avvia un nuovo set di processi utilizzando i parametri correnti di hello.

Per il momento, lasciare il generatore di carico hello in esecuzione in stato di hello chiamata processo.


## <a name="provision-a-new-tenant"></a>Effettuare il provisioning di un nuovo tenant

la distribuzione iniziale di Hello crea tre tenant di esempio, ma è possibile crearne un altro tenant toosee questo impatto di un'applicazione hello distribuito. flusso di lavoro Hello provisioning tenant Wingtip SaaS dettagliato in hello [esercitazione il provisioning e catalogo](sql-database-saas-tutorial-provision-and-catalog.md). Questo passaggio descrive come creare rapidamente un nuovo tenant.

1. Apri... \\Modules\Provision di apprendimento e catalogo\\*Demo ProvisionAndCatalog.ps1* in hello *PowerShell ISE*.
1. Premere **F5** per eseguire script hello (lasciare hello i valori predefiniti per ora).

   > [!NOTE]
   > Utilizzare molti script Wingtip SaaS *$PSScriptRoot* tooallow esplorazione funzioni toocall cartelle in altri script. Questa variabile viene valutata solo quando l'esecuzione dello script hello premendo **F5**.  L'evidenziazione e l'esecuzione di una selezione (**F8**) può causare errori, quindi premere **F5** per l'esecuzione di script.

nuovo database di tenant Hello viene creato in un pool elastico SQL, inizializzato e registrato nel catalogo di hello. Dopo il provisioning ha esito positivo, il nuovo tenant di hello del ticket di vendita *eventi* sito verrà visualizzato nel browser:

![Nuovo tenant](./media/sql-database-saas-tutorial/red-maple-racing.png)

Aggiornare hello *Hub eventi* e nuovo tenant hello viene ora visualizzato nell'elenco di hello.


## <a name="explore-hello-servers-pools-and-tenant-databases"></a>Esplorare server hello, pool e il database del tenant

Ora che si è iniziato a eseguire un caricamento raccolta hello di tenant, ecco alcune risorse che sono stati distribuiti hello:

1. Nel [portale di Azure](http://portal.azure.com), esplorare tooyour elenco di istanze di SQL Server e aprire il **catalogo -&lt;utente&gt;**  server. server di catalogo Hello contiene due database. Hello **tenantcatalog**, hello e **basetenantdb** (vuota *finale* o database modello che viene copiato toocreate nuovi tenant).

   ![database](./media/sql-database-saas-tutorial/databases.png)

1. Tornare indietro tooyour elenco di istanze di SQL Server e aprire hello **tenants1 -&lt;utente&gt;**  server che ospita i database tenant hello. Ogni database tenant è un database _standard elastico_ in un pool standard da 50 eDTU. Si noti inoltre è presente un _acero rosso NASCAR_ database, database tenant hello è effettuato il provisioning in precedenza.

   ![server](./media/sql-database-saas-tutorial/server.png)

## <a name="monitor-hello-pool"></a>Monitoraggio hello pool

Se il generatore di carico hello è stata eseguita per diversi minuti, sufficiente dati dovrebbero essere toostart disponibili una panoramica delle funzionalità incorporate in pool e i database di monitoraggio hello.

1. Esplora server toohello **tenants1 -&lt;utente&gt;**, fare clic su **Pool1** per visualizzare l'utilizzo delle risorse per il pool di hello (Generatore di carico hello è stato eseguito per un'ora in hello seguenti grafici) :

   ![monitorare il pool](./media/sql-database-saas-tutorial/monitor-pool.png)

Quello che dimostrano chiaramente questi due grafici è quanto i pool elastici e database SQL siano adatti ai carichi di lavoro di applicazioni SaaS. Quattro database che ognuno sono bursting tooas quanto 40 Edtu facilmente supportati in un pool di 50 eDTU. Se è stato eseguito il provisioning come database autonomo, si verifica ogni toobe necessario un S2 (DTU 50) toosupport hello picchi. costo di Hello di 4 autonomo S2 database sarebbe prezzo di quasi 3 volte hello del pool di hello e pool hello dispone ancora di una notevole quantità di capacità aggiuntiva per molti altri database. In situazioni reali, ai clienti del Database SQL sono attualmente in esecuzione backup di database too500 200 eDTU pool. Per ulteriori informazioni, vedere hello [esercitazione il monitoraggio delle prestazioni](sql-database-saas-tutorial-performance-monitoring.md).


## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso:

> [!div class="checklist"]

> * Come toodeploy hello applicazione SaaS Wingtip
> * Sui server hello e pool di database che costituiscono l'applicazione hello
> * I tenant sono mappate tootheir dati con hello *catalogo*
> * Come tooprovision nuovi tenant
> * Come tooview pool utilizzo toomonitor tenant attività
> * Correlazione di fatturazione toodelete esempio risorse toostop

Ora provare hello [esercitazione il provisioning e del catalogo](sql-database-saas-tutorial-provision-and-catalog.md)



## <a name="additional-resources"></a>Risorse aggiuntive

* Ulteriori [esercitazioni basate su hello applicazione SaaS Wingtip](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* toolearn sui pool elastico, vedere [ *che cos'è un pool elastico SQL di Azure*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool)
* toolearn sui processi elastici, vedere [ *i database di gestione dei cloud di scalabilità orizzontale*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)
* toolearn sulle applicazioni SaaS multi-tenant, vedere [ *Progettazione modelli per applicazioni SaaS multi-tenant*](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)

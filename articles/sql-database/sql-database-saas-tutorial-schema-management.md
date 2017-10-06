---
title: schema di Database SQL di Azure aaaManage in un'applicazione multi-tenant | Documenti Microsoft
description: "Gestire lo schema per più tenant in un'applicazione multi-tenant che usa il database SQL di Azure"
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
ms.date: 07/28/2017
ms.author: billgib; sstein
ms.openlocfilehash: ea946e556808dabd60dd39cb8173d0512d4bddec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-schema-for-multiple-tenants-in-hello-wingtip-saas-application"></a>Gestione dello schema per più tenant nell'applicazione SaaS Wingtip hello

Hello [prima esercitazione Wingtip SaaS](sql-database-saas-tutorial.md) viene illustrato come applicazione hello può eseguire il provisioning di un database tenant e registrarlo nel catalogo di hello. Come qualsiasi altra applicazione, hello app SaaS Wingtip evolveranno nel tempo e in alcuni casi sarà necessario database toohello le modifiche. Le modifiche possono includere schema nuovo o modificato, i dati di riferimento nuove o modificate e prestazioni dell'applicazione ottimali tooensure attività manutenzione routine del database. Con un'applicazione SaaS, queste modifiche devono toobe distribuiti in modo coordinato tra un fleet potenzialmente grande di database tenant. Per questi toobe modifiche in futuro tenant database, è necessario toobe incorporate nel processo di provisioning hello.

In questa esercitazione vengono illustrati due scenari - distribuzione degli aggiornamenti di dati di riferimento per tutti i tenant, e un indice su hello regolarli tabella contenente i dati di riferimento di hello. Hello [processi elastici](sql-database-elastic-jobs-overview.md) funzionalità viene utilizzato tooexecute queste operazioni in tutti i tenant e hello *finale* database tenant che viene utilizzato come modello per i nuovi database.

In questa esercitazione si apprenderà come:

> [!div class="checklist"]

> * Creare un account di processo
> * Eseguire query in più tenant
> * Aggiornare i dati in tutti i database tenant
> * Creare un indice su una tabella in tutti i database tenant


toocomplete questa esercitazione, assicurarsi che i hello seguenti prerequisiti siano soddisfatti:

* app SaaS Wingtip Hello viene distribuita. toodeploy in meno di cinque minuti, vedere [Distribuisci ed esplorare l'applicazione SaaS Wingtip hello](sql-database-saas-tutorial.md)
* Azure PowerShell è installato. Per informazioni dettagliate, vedere [Introduzione ad Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)
* è installata la versione più recente Hello di SQL Server Management Studio (SSMS). [Scaricare e installare SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

*Questa esercitazione Usa le funzionalità di hello servizio Database SQL in un'anteprima limitata (processi di Database elastico). Se si desidera toodo questa esercitazione, specificare l'id sottoscrizione tooSaaSFeedback@microsoft.com con soggetto = elastico anteprima dei processi. Dopo aver ricevuto una conferma che la sottoscrizione è stata abilitata, [scaricare e installare i cmdlet di processi di pre-release più recenti hello](https://github.com/jaredmoo/azure-powershell/releases). Questa versione di anteprima è limitata. Per eventuali domande o richieste di supporto, contattare SaaSFeedback@microsoft.com.*


## <a name="introduction-toosaas-schema-management-patterns"></a>Introduzione tooSaaS modelli di gestione dello Schema

Hello single-tenant per ogni database SaaS serie vantaggi in diversi modi isolamento dei dati hello risultante, ma in hello contemporaneamente introduce complessità hello di gestione e la gestione di molti database. [I processi elastici](sql-database-elastic-jobs-overview.md) facilita l'amministrazione e gestione del livello dati SQL di hello. I processi consentono di toosecurely ed eseguire in modo affidabile, attività (script T-SQL) indipendentemente dall'interazione dell'utente o input, rispetto a un gruppo di database. Questo metodo può essere utilizzato toodeploy schema e le modifiche ai dati di riferimento comuni tra tutti i tenant in un'applicazione. Processi elastici possono anche essere utilizzati toomaintain un *finale* utilizzata la copia del database hello toocreate nuovi tenant, assicurando che ha sempre hello più recenti dello schema e dati di riferimento.

![schermata](media/sql-database-saas-tutorial-schema-management/schema-management.png)


## <a name="elastic-jobs-limited-preview"></a>Anteprima limitata del servizio Processi elastici

È disponibile una nuova versione del servizio Processi elastici che è ora una funzionalità integrata di database SQL di Azure, che non richiede servizi o componenti aggiuntivi. Questa nuova versione del servizio Processi elastici è attualmente in anteprima limitata. Questa versione di anteprima limitato attualmente supporta gli account di processo di PowerShell toocreate e toocreate T-SQL e gestire i processi.

> [!NOTE]
> *Questa esercitazione Usa le funzionalità di hello servizio Database SQL in un'anteprima limitata (processi di Database elastico). Se si desidera toodo questa esercitazione, specificare l'id sottoscrizione tooSaaSFeedback@microsoft.com con soggetto = elastico anteprima dei processi. Dopo aver ricevuto una conferma che la sottoscrizione è stata abilitata, [scaricare e installare i cmdlet di processi di pre-release più recenti hello](https://github.com/jaredmoo/azure-powershell/releases). Questa versione di anteprima è limitata. Per eventuali domande o richieste di supporto, contattare SaaSFeedback@microsoft.com.*

## <a name="get-hello-wingtip-application-scripts"></a>Ottenere script per l'applicazione hello Wingtip

Hello Wingtip SaaS script e codice sorgente dell'applicazione sono disponibili in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repository github. [I passaggi di script di SaaS Wingtip hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="create-a-job-account-database-and-new-job-account"></a>Creare un database di account per processi e un nuovo account per processi

In questa esercitazione è necessario che utilizzare PowerShell toocreate hello processo account account di database e processo. Come MSDB e SQL Agent, Usa i processi elastico SQL Azure database definizioni processi toostore, lo stato del processo e la cronologia. Una volta creato l'account di processo hello, è possibile creare e monitorare i processi immediatamente.

1. Apri... \\Moduli learning\\la gestione dello Schema\\*Demo SchemaManagement.ps1* in hello **PowerShell ISE**.
1. Premere **F5** script hello toorun.

Hello *Demo SchemaManagement.ps1* script chiamate hello *Distribuisci SchemaManagement.ps1* script toocreate un *S2* database denominato **jobaccount** sul server di catalogo hello. Crea quindi un account di processo hello, passando database jobaccount hello come una chiamata di creazione account di parametro toohello del processo.

## <a name="create-a-job-toodeploy-new-reference-data-tooall-tenants"></a>Creare un processo toodeploy nuovi riferimenti dati tooall tenant

Ogni database tenant include un set di tipi di evento che definiscono il tipo di hello di eventi vengono ospitati in un luogo. In questo esercizio, si distribuisce un tipi di eventi aggiuntivi di aggiornamento tooall hello tenant database tooadd due: *moto NASCAR* e *dei Club*. Questi tipi di eventi corrispondono toohello immagine di sfondo che viene visualizzato nell'app di eventi di hello tenant.

Fare clic su hello luogo tipo menu a discesa e convalidare che sono disponibili le opzioni di tipo solo 10 luogo e in particolare che 'Moto NASCAR' e 'Dei Club' non sono inclusi nell'elenco di hello.

Ora è possibile crearne un hello tooupdate processo *VenueTypes* tabella in tutti i database tenant hello e aggiungere nuovi tipi di evento hello.

toocreate un nuovo processo, viene usato un set di processi di stored procedure create nel database di jobaccount hello quando è stato creato l'account di processo hello di sistema.

1. Aprire SQL Server Management Studio e connettersi a server di catalogo toohello: catalogo -\<utente\>. database.windows.net server
1. Anche la connessione server tenant toohello: tenants1 -\<utente\>. database.windows.net
1. Sfoglia toohello *contosoconcerthall* database hello *tenants1* hello server e query *VenueTypes* tabella tooconfirm che *NASCAR moto*  e *dei Club* **non** nell'elenco risultati hello.
1. File aperti hello... \\Moduli di formazione\\la gestione dello Schema\\DeployReferenceData.sql
1. Modifica istruzione hello: impostare @wtpUser = &lt;utente&gt; e sostituire il valore di utente hello utilizzato quando si distribuiscono app Wingtip hello
1. Verificare di essere connessi toohello jobaccount database e premere **F5** per eseguire script hello

* **SP\_aggiungere\_destinazione\_gruppo** crea nome gruppo di destinazione hello DemoServerGroup, ora è necessario tooadd membri di destinazione.
* **SP\_aggiungere\_destinazione\_gruppo\_membro** aggiunge un *server* tipo di membro, che considera tutti i database in tale server (nota hello tenants1-didestinazione&lt; Utente&gt; server che contiene i database tenant hello) fase del processo di esecuzione deve essere inclusi nel processo di hello, hello secondo consiste nell'aggiunta di un *database* il tipo di membro di destinazione, in particolare hello (il database 'finale' basetenantdb) che si trova nel catalogo -&lt;utente&gt; server e infine un'altra *database* gruppo membro tipo tooinclude hello adhocanalytics database di destinazione che viene utilizzato in un'esercitazione successiva.
* **sp\_add\_job** crea un processo denominato "Reference Data Deployment" (Distribuzione dati di riferimento)
* **SP\_aggiungere\_jobstep** crea il passaggio di processo hello contenente T-SQL comando testo tooupdate hello tabella di riferimento, VenueTypes
* Hello rimanenti nello script hello visualizzazioni esistenza hello di oggetti hello e l'esecuzione del processo di monitoraggio. Utilizzare queste valore di stato query tooreview hello in hello **ciclo di vita** toodetermine colonna quando il processo di hello è stata completata in tutti i database tenant e altri database hello due contenente la tabella di riferimento hello.

1. In SQL Server Management Studio, passare toohello *contosoconcerthall* database hello *tenants1* hello server e query *VenueTypes* tabella tooconfirm che *moto NASCAR* e *dei Club* **sono** ora nell'elenco dei risultati di hello.


## <a name="create-a-job-toomanage-hello-reference-table-index"></a>Creare un indice nella tabella di riferimento di processo toomanage hello

Esercizio precedente simile toohello questo esercizio crea un indice di hello toorebuild processo sulla chiave primaria nella tabella di riferimento hello, potrebbe eseguire un'operazione di gestione di database tipico un amministratore dopo un carico di dati di grandi dimensioni in una tabella.

Crea un processo utilizzando hello stesso processi 'per il sistema' stored procedure.

1. Aprire SQL Server Management Studio e connettersi toohello catalogo -&lt;utente&gt;. database.windows.net server
1. File aperti hello... \\Moduli di formazione\\la gestione dello Schema\\OnlineReindex.sql
1. Fare clic destro, selezionare una connessione e connettersi toohello catalogo -&lt;utente&gt;. database.windows.net server, se non è già connesso.
1. Verificare che si sono connessi toohello jobaccount database e si preme script hello toorun di F5

* sp\_add\_job crea un nuovo processo denominato "Online Reindex PK\_\_VenueTyp\_\_265E44FD7FD4C885"
* SP\_aggiungere\_jobstep crea il passaggio di processo hello contenente l'indice di hello tooupdate testo comando T-SQL




## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:

> [!div class="checklist"]

> * Creare un tooquery di account di processo in più tenant
> * Aggiornare i dati in tutti i database tenant
> * Creare un indice su una tabella in tutti i database tenant

[Esercitazione sull'analisi ad hoc](sql-database-saas-tutorial-adhoc-analytics.md)


## <a name="additional-resources"></a>Risorse aggiuntive

* [Altre esercitazioni che si basano su una distribuzione di applicazioni SaaS Wingtip hello](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Gestione dei database cloud con scalabilità orizzontale](sql-database-elastic-jobs-overview.md)
* [Creare e gestire database SQL di Azure con scalabilità orizzontale](sql-database-elastic-jobs-create-and-manage.md)

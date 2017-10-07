---
title: "query di analitica aaaRun su più database SQL di Azure | Documenti Microsoft"
description: Estrarre i dati dai database tenant in un database di analisi per l'analisi offline
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
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a>Estrarre i dati dai database tenant in un database di analisi per l'analisi offline

In questa esercitazione è utilizzare una query di toorun processo elastico in tutti i database tenant. il processo di Hello estrae i dati di vendita di ticket e li carica in un database analitica (o del data warehouse) per l'analisi. Hello database analitica viene quindi eseguita una query tooextract informazioni approfondite sui dati operativi quotidiane di tutti i tenant.


In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare database analitica di hello tenant
> * Creare un processo pianificato tooretrieve dati e popolare il database di analitica hello

toocomplete questa esercitazione, assicurarsi che i hello seguenti prerequisiti siano soddisfatti:

* app SaaS Wingtip Hello viene distribuita. toodeploy in meno di cinque minuti, vedere [Distribuisci ed esplorare l'applicazione SaaS Wingtip hello](sql-database-saas-tutorial.md)
* Azure PowerShell è installato. Per informazioni dettagliate, vedere [Introduzione ad Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)
* è installata la versione più recente Hello di SQL Server Management Studio (SSMS). [Scaricare e installare SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a>Modello di analisi operativa del tenant

Uno dei hello delle opportunità con applicazioni SaaS è toouse hello tenant avanzato i dati archiviati nel cloud hello. Utilizzare questo dati toogain approfondite operazione hello e l'utilizzo dell'applicazione e i tenant. Questi dati possono assistere lo sviluppo di funzionalità e miglioramenti altri investimenti in app hello e piattaforma. L'accesso a questi dati è semplice quando sono raccolti in un singolo database multi-tenant, ma non è altrettanto semplice in una distribuzione su larga scala potenzialmente in migliaia di database. Un approccio tooaccessing questi dati sono processi toouse elastico, abilitare i risultati della query che restituiscono risultati dal processo esecuzione toobe acquisiti in un database di output e una tabella.

## <a name="get-hello-wingtip-application-scripts"></a>Ottenere script per l'applicazione hello Wingtip

Hello Wingtip SaaS script e codice sorgente dell'applicazione sono disponibili in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repository github. [I passaggi di script di SaaS Wingtip hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="deploy-a-database-for-tenant-analytics-results"></a>Distribuire un database per i risultati di analisi dei tenant

In questa esercitazione è necessario toohave che Hello di toocapture distribuito un database risultante dall'esecuzione del processo di script, che contengono query che restituiscono risultati. Per iniziare verrà creato un database denominato tenantanalytics a questo scopo.

1. Apri... \\Moduli learning\\Analitica Operational\\Tenant Analitica\\*Demo TenantAnalyticsDB.ps1* in hello *PowerShell ISE* e impostare Hello il valore seguente:
   * **$DemoScenario** = **2***Distribuire il database di analisi operativo*
1. Premere **F5** script dimostrativo di hello toorun (hello che chiama *Distribuisci TenantAnalyticsDB.ps1* script) che consente di creare database analitica di hello tenant.

## <a name="create-some-data-for-hello-demo"></a>Creare alcuni dati per la demo hello

1. Apri... \\Moduli learning\\Analitica Operational\\Tenant Analitica\\*Demo TenantAnalyticsDB.ps1* in hello *PowerShell ISE* e impostare Hello il valore seguente:
   * **$DemoScenario** = **1***Acquistare biglietti per gli eventi in tutte le sedi*
1. Premere **F5** toorun hello script e creare ticket di cronologia di acquisto.


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a>Creare un analitica di tenant ScheduledJob tooretrieve sugli acquisti di ticket

Questo script crea informazioni di acquisto un processo tooretrieve ticket da tutti i tenant. Una volta aggregato in una singola tabella, è possibile ottenere metriche dettagliate sull'acquisto di modelli tra tenant hello ticket.

1. Aprire SQL Server Management Studio e connettersi toohello catalogo -&lt;utente&gt;. database.windows.net server
1. Aprire ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*
1. Modificare &lt;utente&gt;, utilizza hello utente il nome utilizzato per la distribuzione di app SaaS Wingtip hello nella parte superiore di hello dello script hello **sp\_aggiungere\_destinazione\_gruppo\_membro** e **sp\_aggiungere\_jobstep**
1. Fare clic destro, selezionare **connessione**e collegare il catalogo toohello -&lt;utente&gt;. database.windows.net server, se non è già connesso.
1. Verificare di essere connesso toohello **jobaccount** database e premere **F5** per eseguire script hello

* **SP\_aggiungere\_destinazione\_gruppo** crea nome gruppo di destinazione hello *TenantGroup*, ora è necessario tooadd membri di destinazione.
* **SP\_aggiungere\_destinazione\_gruppo\_membro** aggiunge un *server* che considera tutti i database in tale server (nota hello customer1 - tipo di membro di destinazione &lt;Utente&gt; server che contiene i database tenant hello) fase del processo di esecuzione deve essere inclusi nel processo di hello.
* **sp\_add\_job** crea un nuovo processo pianificato settimanale denominato "Ticket Purchases from all Tenants" (Acquisti di biglietti da tutti i tenant)
* **SP\_aggiungere\_jobstep** crea il passaggio di processo hello tooretrieve testo di comando T-SQL contenente tutte le informazioni di acquisto di hello ticket da tutti i tenant e hello copia la restituzione di set di risultati in una tabella denominata  *AllTicketsPurchasesfromAllTenants*
* Hello rimanenti nello script hello visualizzazioni esistenza hello di oggetti hello e l'esecuzione del processo di monitoraggio. Esaminare il valore di stato hello da hello **ciclo di vita** stato hello toomonitor della colonna. Una volta, ha avuto esito positivo, il processo di hello è stata completata in tutti i database tenant e hello due altri database contenenti hello fare riferimento a tabella.

In esecuzione script hello dovrebbe restituire risultati simili:

![results](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a>Creare un processo tooretrieve un numero di ticket di riepilogo acquista da tutti i tenant

Questo script crea una somma tooretrieve processo di tutti gli acquisti di ticket da tutti i tenant.

1. Aprire SQL Server Management Studio e connettersi toohello *catalogo -&lt;utente&gt;. database.windows.net* server
1. File aperti hello... \\Moduli di formazione\\il provisioning e catalogo\\Analitica Operational\\Tenant Analitica\\*risultati TicketPurchasesfromAllTenants.sql*
1. Modificare &lt;utente&gt;, utilizza hello utente il nome utilizzato per la distribuzione di app SaaS Wingtip hello nello script hello, hello **sp\_aggiungere\_jobstep** stored procedure
1. Fare clic destro, selezionare **connessione**e collegare il catalogo toohello -&lt;utente&gt;. database.windows.net server, se non è già connesso.
1. Verificare di essere connesso toohello **tenantanalytics** database e premere **F5** per eseguire script hello

In esecuzione script hello dovrebbe restituire risultati simili:

![results](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* **sp\_add\_job** crea un nuovo processo pianificato settimanale denominato "ResultsTicketsOrders"

* **SP\_aggiungere\_jobstep** crea il passaggio di processo hello tooretrieve testo di comando T-SQL contenente tutte le informazioni di acquisto di hello ticket da tutti i tenant e la restituzione di set di risultati in una tabella denominata CountofTicketOrders hello di copia

* Hello rimanenti nello script hello visualizzazioni esistenza hello di oggetti hello e l'esecuzione del processo di monitoraggio. Esaminare il valore di stato hello da hello **ciclo di vita** stato hello toomonitor della colonna. Una volta, ha avuto esito positivo, il processo di hello è stata completata in tutti i database tenant e hello due altri database contenenti hello fare riferimento a tabella.


## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:

> [!div class="checklist"]
> * Distribuire un database di analisi dei tenant
> * Creare un processo pianificato tooretrieve analitiche di dati tra i tenant

Congratulazioni.

## <a name="additional-resources"></a>Risorse aggiuntive

* Ulteriori [esercitazioni in cui si basano su hello applicazione SaaS Wingtip](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Processi elastici](sql-database-elastic-jobs-overview.md)

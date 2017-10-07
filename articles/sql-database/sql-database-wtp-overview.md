---
title: aaaIntro Wingtip SaaS - app multi-tenant di Database SQL di Azure | Documenti Microsoft
description: Ottenere informazioni tramite un'applicazione multi-tenant di esempio che utilizza Database SQL di Azure, app SaaS Wingtip hello
keywords: esercitazione database SQL
services: sql-database
author: stevestein
manager: jhubbard
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: sstein
ms.openlocfilehash: daeed293116fca22718831b780533be6ef2ad178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-wingtip-saas-application"></a>Introduzione toohello applicazione SaaS Wingtip

Hello *Wingtip SaaS* applicazione è un'app multi-tenant di esempio, che illustra i vantaggi specifici di hello del Database SQL. app Hello utilizza un database-per tenant, modello di applicazione SaaS tooservice più tenant. app Hello è una funzionalità di tooshowcase progettato del Database SQL di Azure che consentono scenari SaaS, inclusi diversi modelli di progettazione e gestione SaaS. tooquickly la configurazione e in esecuzione, app SaaS Wingtip hello distribuisce in meno di cinque minuti.

Applicazione di origine codice e la gestione di script è disponibile nel hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repository github. script di hello toorun, [hello Learning moduli cartella download](#download-and-unblock-the-wingtip-saas-scripts) tooyour computer locale.

## <a name="sql-database-wingtip-saas-tutorials"></a>Esercitazioni su SaaS con l'applicazione Wingtip e database SQL

Dopo aver distribuito l'applicazione hello, esplorare hello seguenti esercitazioni in cui si basano su una distribuzione iniziale di hello. Queste esercitazioni illustrano i comuni modelli SaaS che sfruttano le funzionalità predefinite del database SQL, di SQL Data Warehouse e di altri servizi di Azure. Esercitazioni includono gli script di PowerShell, con spiegazioni dettagliate che semplificano notevolmente la comprensione, e implementazione di hello stessi modelli di gestione SaaS nelle applicazioni.


| Esercitazione | Descrizione |
|:--|:--|
|[Distribuire ed esplorare l'applicazione SaaS Wingtip hello](sql-database-saas-tutorial.md)| **INIZIARE DA QUI.** Distribuire ed esplorare hello Wingtip SaaS applicazione tooyour sottoscrizione di Azure. |
|[Effettuare il provisioning di tenant e registrarli nel catalogo](sql-database-saas-tutorial-provision-and-catalog.md)| Informazioni sulle modalità di applicazione hello connessione tootenants utilizzando un database di catalogo e come catalogo hello esegue il mapping ai tenant tootheir dati. |
|[Monitorare e gestire le prestazioni](sql-database-saas-tutorial-performance-monitoring.md)| Informazioni su come toouse monitoraggio funzionalità di Database SQL e come tooset avvisi quando vengono superate le soglie delle prestazioni. |
|[Eseguire il monitoraggio con Log Analytics (OMS)](sql-database-saas-tutorial-log-analytics.md) | Informazioni sull'utilizzo di [Log Analitica](../log-analytics/log-analytics-overview.md) toomonitor grandi quantità di risorse, tra più pool. |
|[Ripristinare un tenant singolo](sql-database-saas-tutorial-restore-single-tenant.md)| Informazioni su come toorestore un tooa database tenant precedente punto nel tempo. Sono inclusi anche i passaggi toorestore tooa parallelo di database, lasciando hello tenant database esistente, è online. |
|[Gestire uno schema di tenant](sql-database-saas-tutorial-schema-management.md)| Informazioni su come schema tooupdate e aggiornare i dati di riferimento tra tutti i tenant Wingtip SaaS. |
|[Eseguire analisi ad hoc](sql-database-saas-tutorial-adhoc-analytics.md) | Creare un database di analisi ad-hoc ed eseguire query distribuite in tempo reale su tutti i tenant.  |
|[Eseguire l'analisi di tenant](sql-database-saas-tutorial-tenant-analytics.md) | Estrarre i dati del tenant in un database di analisi o in un data warehouse per l'esecuzione offline di query di analisi. |



## <a name="application-architecture"></a>Architettura dell'applicazione

app SaaS Wingtip Hello utilizza il modello di database per tenant hello e l'efficienza di toomaximize pool elastico SQL. Per il provisioning e il mapping dei dati tootheir tenant, viene utilizzato un database di catalogo. un'applicazione SaaS Wingtip core Hello, utilizza un pool con tre tenant di esempio, più hello database del catalogo. Molte delle esercitazioni di SaaS Wingtip causare distribuzione iniziale di componenti aggiuntivi toohello hello completato, introducendo i database analitici, tra database la gestione dello schema e così via.


![Architettura SaaS Wingtip](media/sql-database-wtp-overview/app-architecture.png)


Anche se passando esercitazioni hello e l'utilizzo con app hello, è importante toofocus sui modelli di hello SaaS in relazione a livello di dati toohello. In altre parole, lo stato attivo su un livello di dati hello e non oltre analizzano hello app stessa. Comprendere l'implementazione di hello di questi modelli di SaaS è tooimplementing chiave questi modelli nelle applicazioni, prendendo in considerazione tutte le modifiche necessarie per i requisiti aziendali specifici.

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a>Scaricare e sbloccare script Wingtip SaaS hello

I contenuti eseguibili (script, DLL) possono essere bloccati da Windows quando si scaricano e si estraggono i file ZIP da un'origine esterna. Durante l'estrazione di script hello da un file zip, ***procedura hello di sotto di file con estensione zip hello toounblock prima dell'estrazione***. In questo modo, gli script hello consentiti toorun.

1. Sfoglia troppo[repository di github Wingtip SaaS hello](https://github.com/Microsoft/WingtipSaaS).
1. Fare clic su **Clona o scarica**.
1. Fare clic su **ZIP di Download** e salvare il file hello.
1. Pulsante destro del mouse hello **WingtipSaaS master.zip** file e selezionare **proprietà**.
1. In hello **generale** , selezionare **Unblock**.
1. Fare clic su **OK**.
1. Estrarre il file hello.

Gli script si trovano in hello *... \\WingtipSaaS master\\moduli Learning* cartella.


## <a name="working-with-hello-wingtip-saas-powershell-scripts"></a>Utilizzo di script di PowerShell SaaS Wingtip hello

hello tooget più fuori: esempio hello è necessario toodive negli script hello fornito. Utilizzare i punti di interruzione ed eseguire un'istruzione tramite gli script hello, esaminando hello dettagli di implementazione dei diversi modelli di SaaS hello. passaggio tooeasily tramite hello fornito script e moduli per comprendere meglio, è consigliabile utilizzare hello hello [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).

### <a name="update-hello-configuration-file-for-your-deployment"></a>Aggiornare il file di configurazione hello per la distribuzione

Modifica hello **UserConfig.psm1** file con hello risorsa utente e gruppo valore impostato durante la distribuzione:

1. Aprire hello *PowerShell ISE* e caricare... \\Moduli di formazione\\*UserConfig.psm1* 
1. Aggiornamento *ResourceGroupName* e *nome* con valori specifici di hello per la distribuzione (su righe 10 e 11 solo).
1. Salvare le modifiche di hello!

Impostare questi valori qui semplicemente modo si possono evitare tooupdate questi valori specifici della distribuzione in ogni script.

### <a name="execute-scripts-by-pressing-f5"></a>Eseguire gli script premendo F5

Utilizzare numerosi script *$PSScriptRoot* toonavigate cartelle, e *$PSScriptRoot* viene valutata solo quando gli script vengono eseguiti premendo **F5**.  L'evidenziazione e l'esecuzione di una selezione (**F8**) può causare errori, quindi premere **F5** per l'esecuzione di script.

### <a name="step-through-hello-scripts-tooexamine-hello-implementation"></a>Passaggio tramite l'implementazione di hello tooexamine script hello

script di Hello migliore modo toounderstand hello è avanzando li toosee quali azioni eseguono. Estrarre hello incluso **Demo -** script che presentano un flusso di lavoro generale toofollow semplice. Hello **Demo -** script Mostra hello passaggi necessari tooaccomplish ogni attività, quindi impostare i punti di interruzione e analisi più approfondita in singoli hello prevede i dettagli di implementazione toosee hello diversi modelli di SaaS.

Suggerimenti per esplorare e scorrere gli script PowerShell:

* Aprire **Demo -** degli script in PowerShell ISE hello.
* Eseguire o continuare con **F5**. Non è consigliabile usare **F8** perché la variabile *$PSScriptRoot* non viene valutata durante l'esecuzione di selezioni di uno script.
* Aggiungere punti di interruzione facendo clic o selezionando una riga e premendo **F9**.
* Eseguire una funzione o una chiamata dello script in blocco con **F10** (comando Esegui istruzione/routine).
* Eseguire una funzione o una chiamata dello script un'istruzione alla volta con **F11**.
* Uscire da funzione corrente hello o script chiamata utilizzando **MAIUSC + F11**.


## <a name="explore-database-schema-and-execute-sql-queries-using-ssms"></a>Esplorare lo schema del database ed eseguire query SQL tramite SSMS

Utilizzare [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) tooconnect ed esplorazione hello server applicazioni e database.

distribuzione di Hello dispone inizialmente di due Database di SQL Server tooconnect troppo-hello *tenants1 -&lt;utente&gt;*  server e hello *catalogo -&lt;utente&gt;* server. una connessione riuscita demo tooensure, entrambi i server hanno un [regola del firewall](sql-database-firewall-configure.md) consentendo a tutti gli indirizzi IP tramite.


1. Aprire *SSMS* e connettersi toohello *tenants1 -&lt;utente&gt;. database.windows.net* server.
1. Fare clic su **Connetti** > **Motore di database...**:

   ![server di catalogo](media/sql-database-wtp-overview/connect.png)

1. Le credenziali per la demo sono: Account di accesso = *developer*, Password = *P@ssword1*

   ![connessione](media\sql-database-wtp-overview\tenants1-connect.png)

1. Ripetere i passaggi 2-3 e connettersi toohello *catalogo -&lt;utente&gt;. database.windows.net* server.

Dopo avere stabilito la connessione, entrambi i server dovrebbero essere visibili. L'elenco dei database potrebbe essere diverso a seconda di tenant hello che è stato effettuato il provisioning:

![esplora oggetti](media/sql-database-wtp-overview/object-explorer.png)



## <a name="next-steps"></a>Passaggi successivi

[Distribuire un'applicazione SaaS Wingtip hello](sql-database-saas-tutorial.md)

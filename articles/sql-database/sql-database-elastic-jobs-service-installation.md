---
title: i processi di database elastico aaaInstalling | Documenti Microsoft
description: "Eseguire l'installazione della funzionalità processi elastico hello."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a>Installazione dei processi di database elastici (panoramica)
[**I processi di Database elastici** ](sql-database-elastic-jobs-overview.md) può essere installato tramite PowerShell o tramite hello Portal.You classico di Azure potrà accedere a toocreate e gestire processi mediante l'API di PowerShell hello solo se si installa il pacchetto di PowerShell hello. Inoltre, hello APIs di PowerShell fornisce molte più funzionalità rispetto a portale hello in questo momento.

Se è già stato installato **i processi di Database elastico** tramite hello portale da un oggetto esistente **pool elastico**, anteprima più recente di Powershell hello include script tooupgrade l'installazione esistente. È altamente consigliabile tooupgrade toohello l'installazione più recente **i processi di Database elastico** componenti vantaggio tootake ordine delle nuove funzionalità vengono esposte tramite hello APIs di PowerShell.

## <a name="prerequisites"></a>Prerequisiti
* Una sottoscrizione di Azure. Per una versione di valutazione gratuita, vedere [Versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Azure PowerShell. Installare hello utilizzando la versione più recente hello [installazione guidata piattaforma Web](http://go.microsoft.com/fwlink/p/?linkid=320376). Per informazioni dettagliate, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).
* [Utilità della riga di comando di NuGet](https://nuget.org/nuget.exe) è usato tooinstall hello Database elastico processi pacchetto. Per altre informazioni, vedere http://docs.nuget.org/docs/start-here/installing-nuget.

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a>Scaricare e importare hello Database elastico processi PowerShell pacchetto
1. Avviare la finestra di comando di Microsoft Azure PowerShell e passare toohello directory in cui è stato scaricato NuGet utilità della riga di comando (nuget.exe).
2. Scaricare e importare **i processi di Database elastico** pacchetto nella directory corrente di hello con hello comando seguente:
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    Hello **i processi di Database elastico** i file si trovano nella directory locale di hello in una cartella denominata **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** in *x.x.xxxx.x* riflette il numero di versione di hello. cmdlet di PowerShell Hello (inclusi DLL client richieste) si trovano in hello **tools\ElasticDatabaseJobs** sottodirectory hello tooinstall gli script di PowerShell, aggiornare e disinstallare anche si trovano in hello  **strumenti** sottodirectory.
3. Passare sottodirectory strumenti toohello nella cartella Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x hello digitando cd strumenti, ad esempio:
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. Eseguire ElasticDatabaseJobs directory di hello.\InstallElasticDatabaseJobsCmdlets.ps1 script toocopy hello in $home\Documents\WindowsPowerShell\Modules. Verranno inoltre automaticamente importate modulo hello da utilizzare, ad esempio:
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a>Installare i componenti di processi di Database elastico hello utilizzando PowerShell
1. Avviare una finestra di comando di Microsoft Azure PowerShell e passare sottodirectory \tools toohello nella cartella Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x hello: digitare cd \tools
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. Eseguire lo script di PowerShell.\InstallElasticDatabaseJobs.ps1 hello e fornire valori per le variabili di richieste. Questo script crea componenti hello descritti in [componenti e sui prezzi dei processi di Database elastico](sql-database-elastic-jobs-overview.md#components-and-pricing) configurazione servizio Cloud di Azure hello tooappropriately fanno uso dei componenti dipendenti hello.

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

Quando si esegue questo comando, viene visualizzata una finestra in cui vengono richiesti **Nome utente** e **Password**. Non si tratta le credenziali di Azure, immettere nome utente hello e una password che saranno le credenziali di amministratore hello da toocreate per nuovo server hello.

parametri di Hello forniti nella chiamata di questo esempio possono essere modificati per le impostazioni desiderate. esempio Hello vengono fornite ulteriori informazioni sul comportamento di hello di ogni parametro:

<table style="width:100%">
  <tr>
    <th>.</th>
    <th>Description</th>
  </tr>

<tr>
    <td>ResourceGroupName</td>
    <td>Fornisce nome gruppo di risorse di Azure hello creato hello toocontain nuovo componenti di Azure. Per impostazione predefinita questo parametro troppo "__ElasticDatabaseJob". Non è consigliabile toochange questo valore.</td>
    </tr>

</tr>

    <tr>
    <td>ResourceGroupLocation</td>
    <td>Fornisce hello Azure percorso toobe utilizzato per hello nuovo componenti di Azure. Questo parametro toohello posizione centrale USA per impostazione predefinita.</td>
</tr>

<tr>
    <td>ServiceWorkerCount</td>
    <td>Fornisce il numero di hello del servizio worker tooinstall. Questo parametro per impostazione predefinita too1. Un numero elevato di thread di lavoro può essere utilizzato tooscale out hello servizio e tooprovide la disponibilità elevata. È consigliabile toouse "2" per le distribuzioni che richiedono la disponibilità elevata del servizio hello.</td>
    </tr>

</tr>
    <tr>
    <td>ServiceVmSize</td>
    <td>Fornisce dimensioni delle macchine Virtuali hello per l'utilizzo della hello servizio Cloud. Questo parametro per impostazione predefinita tooA0. Vengono accettati i valori di parametri di A3/A0/A1/A2, causando il lavoro hello ruolo toouse una dimensione molto piccola/piccole, medie e grandi, rispettivamente. Per altre informazioni sulle dimensioni dei ruoli di lavoro, vedere [Componenti e prezzi dei processi di database elastici](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</tr>
    <tr>
    <td>SqlServerDatabaseSlo</td>
    <td>Fornisce l'obiettivo del livello di servizio hello per un'edizione Standard. Questo parametro per impostazione predefinita tooS0. Vengono accettati i valori dei parametri di S0/S1, S2 o S3 determinando hello Database SQL di Azure toouse hello rispettivo SLO. Per ulteriori informazioni sugli SLO del database SQL, vedere [Componenti e prezzi dei processi di database elastici](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorUserName</td>
    <td>Fornisce il nome utente amministratore di hello per hello appena creati server di Database SQL di Azure. Quando non viene specificato, è possibile che il tooprompt credenziali hello verrà aperta una finestra di PowerShell le credenziali.</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorPassword</td>
    <td>Fornisce la password di amministratore di hello per hello appena creati server di Database SQL di Azure. Quando non viene specificato, è possibile che il tooprompt credenziali hello verrà aperta una finestra di PowerShell le credenziali.</td>
</tr>
</table>

Per i sistemi che con un numero elevato di processi in esecuzione in parallelo rispetto a un numero elevato di database di destinazione, è consigliabile, ad esempio parametri toospecify: ServiceWorkerCount - 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a>Aggiornare un'installazione dei componenti dei processi di database elastici esistente tramite PowerShell
**Processi di database elastici** possono essere aggiornati all'interno di un'installazione esistente per la scalabilità e la disponibilità elevata. Questo processo consente gli aggiornamenti futuri del codice di servizio senza dovere toodrop e ricreare il database di controllo hello. Questo processo può inoltre essere utilizzato all'interno di hello stesso conteggio della versione toomodify hello servizio VM dimensioni o hello server worker.

tooupdate hello dimensione della macchina virtuale un'installazione, hello eseguire lo script con parametri seguente toohello valori aggiornati delle prescelto.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th>.</th>
  <th>Description</th>
</tr>

  <tr>
    <td>ResourceGroupName</td>
    <td>Identifica nome gruppo di risorse di Azure hello utilizzato quando i componenti dei processi di Database elastico hello sono stati inizialmente installati. Per impostazione predefinita questo parametro troppo "__ElasticDatabaseJob". Perché non è consigliabile toochange questo valore, non dovrebbe essere toospecify questo parametro.</td>
    </tr>
</tr>

</tr>

  <tr>
    <td>ServiceWorkerCount</td>
    <td>Fornisce il numero di hello del servizio worker tooinstall.  Questo parametro per impostazione predefinita too1.  Un numero elevato di thread di lavoro può essere utilizzato tooscale out hello servizio e tooprovide la disponibilità elevata.  È consigliabile toouse "2" per le distribuzioni che richiedono la disponibilità elevata del servizio hello.</td>
</tr>

</tr>

    <tr>
    <td>ServiceVmSize</td>
    <td>Fornisce dimensioni delle macchine Virtuali hello per l'utilizzo della hello servizio Cloud. Questo parametro per impostazione predefinita tooA0. Vengono accettati i valori di parametri di A3/A0/A1/A2, causando il lavoro hello ruolo toouse una dimensione molto piccola/piccole, medie e grandi, rispettivamente. Per altre informazioni sulle dimensioni dei ruoli di lavoro, vedere [Componenti e prezzi dei processi di database elastici](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a>Installare i componenti di processi di Database elastico hello utilizzando hello portale
Dopo aver [creato un pool elastico](sql-database-elastic-pool-manage-portal.md), è possibile installare **i processi di Database elastico** esecuzione tooenable componenti delle attività amministrative in tutti i database nel pool elastico hello. A differenza di quando utilizzare hello **i processi di Database elastico** APIs di PowerShell, interfaccia portale hello è attualmente soggetta a restrizioni tooonly per eseguire un pool esistente.

**Toocomplete tempo stimato:** 10 minuti.

1. Dalla visualizzazione dashboard hello del pool elastico di hello tramite hello [portale Azure](https://portal.azure.com/#) , fare clic su **processo di creazione**.
2. Se si sta creando un processo per hello prima volta, è necessario installare **i processi di Database elastico** facendo **condizioni per l'anteprima**.
3. Accettare le condizioni di hello facendo hello casella di controllo.
4. Nella visualizzazione hello "Installazione servizi", fare clic su **processo CREDENZIALI**.
   
    ![Installazione di servizi di hello][1]
5. Digitare un nome utente e una password per un amministratore del database. Come parte dell'installazione di hello, viene creato un nuovo server di Database SQL di Azure. All'interno di questo nuovo server, un nuovo database, noto come database del controllo hello, viene creato e utilizzato i metadati di hello toocontain per i processi di Database elastico. nome utente Hello e la password creati in questo caso vengono utilizzati a scopo di hello di registrazione nel database del controllo toohello. Una credenziale separata viene usata per l'esecuzione di script sul database hello pool hello.
   
    ![Creare nome utente e password][2]
6. Fare clic su pulsante OK hello. i componenti di Hello vengono creati automaticamente in pochi minuti in un nuovo [gruppo di risorse](../azure-resource-manager/resource-group-overview.md). è stato aggiunto il nuovo gruppo di risorse Hello toohello avviare discussioni, come illustrato di seguito. Tutti i processi di database elastico, una volta create (servizio Cloud, Database SQL, Bus di servizio e archiviazione) vengono creati nel gruppo di hello.
   
    ![gruppo di risorse nella schermata iniziale][3]
7. Se si tenta di toocreate o gestire un processo durante l'installazione, i processi di database elastico quando si specifica **credenziali** hello seguente messaggio verrà visualizzato.
   
    ![Distribuzione ancora in corso][4]

Se la disinstallazione è necessario, eliminare il gruppo di risorse di hello. Vedere [come toouninstall hello Database elastico processo componenti](sql-database-elastic-jobs-uninstall.md).

## <a name="next-steps"></a>Passaggi successivi
Verificare che una credenziale con diritti di hello appropriati per l'esecuzione dello script viene creato in ogni database nel gruppo di hello, per ulteriori informazioni, vedere [la protezione del Database SQL](sql-database-manage-logins.md).
Vedere [creazione e gestione dei processi di un Database elastico](sql-database-elastic-jobs-create-and-manage.md) tooget avviato.

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png

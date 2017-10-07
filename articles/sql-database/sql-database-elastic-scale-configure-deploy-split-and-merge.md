---
title: un servizio di suddivisione unione aaaDeploy | Documenti Microsoft
description: Suddivisione e unione con gli strumenti di database elastico
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a>Distribuire un servizio di divisione e unione
strumento di unione di menu combinato Hello consente di spostare i dati tra database partizionati. Vedere [Spostamento di dati tra database cloud con numero maggiore di istanze](sql-database-elastic-scale-overview-split-and-merge.md)

## <a name="download-hello-split-merge-packages"></a>Scaricare i pacchetti hello unione di menu combinato
1. Scaricare hello NuGet più recente da [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).
2. Aprire un prompt dei comandi e passare toohello directory in cui è stato scaricato nuget.exe. download di Hello include commmands di PowerShell.
3. Scaricare il pacchetto suddivisione unione più recente di hello nella directory corrente di hello con hello comando seguente:
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

file Hello vengono inseriti in una directory denominata **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** in *x.x.xxx.x* riflette il numero di versione di hello. Trovare i file del servizio di suddivisione unione hello in hello **content\splitmerge\service** sottodirectory e hello gli script di PowerShell di unione di menu combinato (e client necessari file con estensione dll) in hello **content\splitmerge\powershell** sottodirectory.

## <a name="prerequisites"></a>Prerequisiti
1. Creare un database di database SQL di Azure che verrà utilizzato come database di stato di unione di menu combinato hello. Passare toohello [portale di Azure](https://portal.azure.com). Creazione personalizzata di un nuovo **database SQL**. Assegnare un nome di database hello e creare un nuovo amministratore e una password. Impossibile verificare toorecord hello nome e la password per un uso successivo.
2. Verificare che il server di database SQL di Azure consente tooit tooconnect servizi di Azure. Nel portale hello hello **le impostazioni del Firewall**, verificare che hello **Consenti l'accesso ai servizi tooAzure** impostazione troppo**su**. Fare clic su hello "icona Salva".
   
   ![Servizi consentiti][1]
3. Creare un account di archiviazione di Azure che verrà usato per l'output di diagnostica. Passare toohello portale di Azure. Nella barra sinistra hello, fare clic su **New**, fare clic su **dati e archiviazione**, quindi **archiviazione**.
4. Creare un servizio cloud di Azure che conterrà il servizio di divisione e unione.  Passare toohello portale di Azure. Nella barra sinistra hello, fare clic su **New**, quindi **calcolo**, **servizio Cloud**, e **crea**. 

## <a name="configure-your-split-merge-service"></a>Configurare il servizio di divisione e unione
### <a name="split-merge-service-configuration"></a>Configurazione del servizio di divisione e unione
1. Nella cartella hello in cui è stato scaricato assembly hello suddivisione unione, creare una copia di hello **ServiceConfiguration.Template.cscfg** file fornita insieme **SplitMergeService.cspkg** e rinominarlo **ServiceConfiguration. cscfg**.
2. Aprire **ServiceConfiguration. cscfg** in un editor di testo, ad esempio Visual Studio che convalida l'input, ad esempio formato hello di identificazioni personali del certificato.
3. Creare un nuovo database o scegliere un tooserve database esistente come database di stato hello per le operazioni di unione di menu combinato e recuperare la stringa di connessione hello di tale database. 
   
   > [!IMPORTANT]
   > In questo momento, database di stato hello deve utilizzare regole di confronto latino hello (SQL\_Latin1\_generale\_CP1\_CI\_AS). Per ulteriori informazioni, vedere [Nome regole di confronto Windows (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).
   >

   Con il database SQL di Azure, la stringa di connessione hello è in genere formato hello:
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. Immettere la stringa di connessione nel file cscfg hello in entrambi hello **SplitMergeWeb** e **SplitMergeWorker** sezioni ruolo nell'impostazione ElasticScaleMetadata hello.
5. Per hello **SplitMergeWorker** ruolo, immettere un'archiviazione tooAzure stringa di connessione valida per hello **WorkerRoleSynchronizationStorageAccountConnectionString** impostazione.

### <a name="configure-security"></a>Configurare la sicurezza
Per istruzioni dettagliate tooconfigure hello sicurezza hello servizio, vedere toohello [configurazione della sicurezza suddivisione unione](sql-database-elastic-scale-split-merge-security-configuration.md).

Ai fini di hello di una distribuzione di test semplice per questa esercitazione, un set minimo di passaggi di configurazione eseguita il servizio hello tooget attivo e in esecuzione. Questi passaggi abilitano solo hello una macchina/account eseguirle toocommunicate con servizio hello.

### <a name="create-a-self-signed-certificate"></a>Creare un certificato autofirmato
Creare una nuova directory e da questo hello execute directory seguente comando utilizzando un [prompt dei comandi per sviluppatori per Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) finestra:

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

Richiesto per una chiave privata di tooprotect hello password. Immettere una password complessa e confermarla. Verrà chiesto di hello password toobe utilizzato più volte dopo che. Fare clic su **Sì** in tooimport fine hello è archivio radice attendibile autorità di certificazione toohello.

### <a name="create-a-pfx-file"></a>Creare un file PFX
Eseguire hello comando seguente da hello stessa finestra in cui è stato eseguito makecert; Utilizzare hello stessa password che è usato toocreate hello certificato:

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a>Importare il certificato di client hello nell'archivio personale hello
1. In Esplora risorse fare doppio clic su **MyCert.pfx**.
2. In hello **importazione guidata certificati** selezionare **utente corrente** e fare clic su **Avanti**.
3. Verificare il percorso di file hello e fare clic su **Avanti**.
4. Digitare la password hello, lasciare **includono tutte le proprietà estese** selezionata e fare clic su **Avanti**.
5. Lasciare **archivio certificati selezionare automaticamente hello […]**  selezionata e fare clic su **Avanti**.
6. Fare clic su **Fine**, quindi su **OK**.

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a>Caricare il servizio cloud toohello di hello PFX file
1. Passare toohello [portale Azure](https://portal.azure.com).
2. Selezionare **Servizi cloud**.
3. Selezionare servizio cloud hello creato in precedenza per il servizio di suddivisione/unione hello.
4. Fare clic su **certificati** nel menu superiore hello.
5. Fare clic su **caricare** barra inferiore hello.
6. Selezionare i file PFX hello e immettere hello uguale alla password precedente.
7. Al termine, copiare l'identificazione personale del certificato hello da hello nuova voce di elenco hello.

### <a name="update-hello-service-configuration-file"></a>File di configurazione del servizio di aggiornamento hello
Incollare l'identificazione personale del certificato hello copiato in precedenza nell'attributo/valore di identificazione personale hello di queste impostazioni.
Per il ruolo di lavoro hello:
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

Per il ruolo web hello:

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

Tenere presente che per le distribuzioni di produzione certificati separati devono essere utilizzati per hello autorità di certificazione, per la crittografia, hello certificato del Server e i certificati client. Per istruzioni dettagliate, vedere l'articolo relativo alla [configurazione della sicurezza](sql-database-elastic-scale-split-merge-security-configuration.md).

## <a name="deploy-your-service"></a>Distribuire il servizio
1. Passare toohello [portale di Azure](https://manage.windowsazure.com).
2. Fare clic su hello **servizi Cloud** scheda hello sinistra e selezionare il servizio cloud hello creato in precedenza.
3. Fare clic su **Dashboard**.
4. Scegliere l'ambiente di gestione temporanea hello, quindi fare clic su **carica una nuova distribuzione di gestione temporanea**.
   
   ![Staging][3]
5. Nella finestra di dialogo hello immettere un'etichetta di distribuzione. Per 'Package' e 'Configuration', fare clic su 'Da Local' e scegliere hello **SplitMergeService.cspkg** file e il file con estensione cscfg configurata in precedenza.
6. Verificare che tale casella hello **Distribuisci anche se uno o più ruoli contengono una singola istanza** è selezionata.
7. Raggiunto il pulsante di segni di graduazione hello nella distribuzione di hello nella parte inferiore destra toobegin hello. Previsto tootake toocomplete di pochi minuti.

   ![Carica][4]

## <a name="troubleshoot-hello-deployment"></a>Risoluzione dei problemi di distribuzione hello
Se il ruolo web toocome online, è probabile che un problema di configurazione di sicurezza hello. Verificare che hello che SSL è configurato come descritto in precedenza.

Se il ruolo di lavoro ha esito negativo toocome online, ma il ruolo web ha esito positivo, è probabilmente un problema di connessione database stato toohello creato in precedenza.

* Assicurarsi che la stringa di connessione hello nel file con estensione cscfg è accurata.
* Verificare che siano presenti database e server hello e che la password e l'id utente hello siano corretti.
* Per il database di SQL Azure, la stringa di connessione hello deve essere formato hello:

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* Verificare che non inizia con il nome del server hello **https://**.
* Verificare che il server di database SQL di Azure consente tooit tooconnect servizi di Azure. toodo, aprire https://manage.windowsazure.com, scegliere "Database di SQL" hello a sinistra, fare clic su "Server" nella parte superiore di hello e selezionare il server. Fare clic su **configura** in hello in alto e verificare che hello **servizi Azure** impostazione troppo "Yes". (Vedere la sezione Prerequisiti hello sezione nella parte superiore di hello di questo articolo).

## <a name="test-hello-service-deployment"></a>Testare la distribuzione del servizio hello
### <a name="connect-with-a-web-browser"></a>Connettersi con un Web browser
Determinare l'endpoint web hello del servizio di suddivisione-unione. È possibile trovare questo in hello portale classico di Azure da passare toohello **Dashboard** del servizio cloud e cercando nella **URL del sito** sul lato destro hello. Sostituire **http://** con **https://** poiché le impostazioni di sicurezza predefinite hello disabilitano endpoint hello HTTP. Caricare la pagina hello per questo URL nel browser.

### <a name="test-with-powershell-scripts"></a>Eseguire i test con gli script di PowerShell
distribuzione di Hello e l'ambiente può essere testati eseguendo gli script di PowerShell di esempio hello incluso.

file di script Hello forniti sono:

1. **SetupSampleSplitMergeEnvironment.ps1** : consente di impostare un livello di dati di test per divisione e unione (per una descrizione dettagliata, vedere la tabella sottostante).
2. **ExecuteSampleSplitMerge.ps1** -esegue le operazioni di test nel test hello livello dati (vedere la tabella seguente per una descrizione dettagliata)
3. **GetMappings.ps1** - principale script che visualizza lo stato corrente di hello di mapping delle partizioni hello di esempio.
4. **ShardManagement.psm1** -script helper che esegue il wrapping hello ShardManagement API
5. **SqlDatabaseHelpers.psm1**: script helper per creare e gestire database SQL
   
   <table style="width:100%">
     <tr>
       <th>File PowerShell</th>
       <th>Passi</th>
     </tr>
     <tr>
       <th rowspan="5">SetupSampleSplitMergeEnvironment.ps1</th>
       <td>1.    Crea un database di gestione delle mappe partizioni.</td>
     </tr>
     <tr>
       <td>2.    Crea 2 database partizioni.
     </tr>
     <tr>
       <td>3.    Crea una mappa partizioni per tali database (elimina eventuali mappe partizioni esistenti per i database). </td>
     </tr>
     <tr>
       <td>4.    Crea una tabella di esempio di piccole dimensioni in entrambe le partizioni hello e popola la tabella hello in una delle partizioni hello.</td>
     </tr>
     <tr>
       <td>5.    Dichiara hello SchemaInfo per la tabella partizionata hello.</td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th>File PowerShell</th>
       <th>Passi</th>
     </tr>
   <tr>
       <th rowspan="4">ExecuteSampleSplitMerge.ps1 </th>
       <td>1.    Invia un divisione richiesta toohello suddivisione unione servizio front-end web, che divide i dati hello metà dalla partizione secondo di hello prima partizione toohello.</td>
     </tr>
     <tr>
       <td>2.    Esegue il polling hello front-end web per suddividere lo stato di richiesta e attende fino al completamento di richiesta di hello hello.</td>
     </tr>
     <tr>
       <td>3.    Invia un merge richiesta toohello suddivisione unione servizio front-end web, che sposta i dati di hello dalla partizione prima di hello seconda partizione toohello indietro.</td>
     </tr>
     <tr>
       <td>4.    Esegue il polling hello front-end web per lo stato richiesta di unione di hello e attende il completamento della richiesta di hello.</td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a>Utilizzare PowerShell tooverify la distribuzione
1. Aprire una nuova finestra di PowerShell passare toohello directory in cui è stato scaricato il pacchetto di suddivisione unione hello e quindi passare alla directory "powershell" hello.
2. Creare un server di database SQL di Azure (o scegliere un server esistente) in cui verranno create gestore mappe partizioni di hello e partizioni.
   
   > [!NOTE]
   > Hello SetupSampleSplitMergeEnvironment.ps1 script crea tutti questi database in hello stesso server da script hello tookeep predefinito semplice. Non è una restrizione di hello suddivisione unione servizio stesso.
   >
   
   Un accesso con autenticazione SQL con toohello di accesso in lettura/scrittura che database saranno necessaria per dati di unione di menu combinato servizio toomove hello e aggiornare la mappa partizioni hello. Poiché hello servizio di suddivisione unione viene eseguito nel cloud hello, non supporta attualmente l'autenticazione integrata.
   
   Verificare che sia configurato il server di SQL Azure hello tooallow accesso dall'indirizzo IP hello della macchina hello eseguire tali script. È possibile trovare questa impostazione nel server SQL Azure hello / configurazione / indirizzi IP consentiti.
3. Eseguire l'ambiente di esempio hello toocreate script SetupSampleSplitMergeEnvironment.ps1 hello.
   
   L'esecuzione dello script verrà cancellano i dati di gestione di mappa partizioni esistenti strutture di database di gestione della mappa partizioni hello e partizioni hello. Potrebbe essere script hello toorerun utile se si desidera mappa partizioni di hello toore inizializzare o partizioni.
   
   Riga di comando di esempio:

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. Eseguire hello Getmappings.ps1 script tooview hello mapping attualmente presenti nell'ambiente di esempio hello.
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. Eseguire hello ExecuteSampleSplitMerge.ps1 script tooexecute un'operazione di divisione (spostamento dei dati di hello metà nella partizione secondo di hello prima partizione toohello) e quindi un'operazione di unione (spostamento dati hello nella partizione prima di hello). Se è stato configurato SSL e l'endpoint http hello sinistro disabilitata, verificare di utilizzare endpoint https:// hello.
   
   Riga di comando di esempio:

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   Se si riceve hello di sotto di errore, è probabilmente un problema con il certificato dell'endpoint di Web. Ritentare la connessione degli endpoint Web toohello con un browser qualsiasi e controllare se è presente un errore di certificato.
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   Se ha avuto esito positivo, output di hello dovrebbe essere simile hello riportato di seguito:
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. Ora è possibile sperimentare il processo con altri tipi di dati. Tutti questi script accettano un parametro di ShardKeyType - facoltativo che consente di tipo di chiave toospecify hello. valore predefinito di Hello è Int32, ma è anche possibile specificare Int64, Guid o Binary.

## <a name="create-requests"></a>Creare richieste
servizio Hello può essere utilizzato tramite l'interfaccia utente web hello o mediante l'importazione e uso di modulo di PowerShell SplitMerge.psm1 hello che verrà inviate le richieste tramite ruolo web hello.

servizio Hello può spostare i dati in tabelle partizionate sia tabelle di riferimento. Una tabella partizionata ha una colonna chiave di partizionamento e ospita dati di riga diversi per ogni partizione. Una tabella di riferimento non è partizionata in modo che contenga hello stessa riga di dati in ogni partizione. Tabelle di riferimento sono utili per i dati non vengono modificati spesso e viene utilizzato tooJOIN con le tabelle partizionate nelle query.

In ordine tooperform un'operazione di unione di menu combinato, è necessario dichiarare tabelle partizionate hello e tabelle di riferimento che si desidera toohave spostato. Questa operazione viene eseguita con hello **SchemaInfo** API. Questa API è hello **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** dello spazio dei nomi.

1. Per ogni tabella partizionata, creare un **ShardedTableInfo** oggetto che descrive nome di schema della tabella hello padre (facoltativo, valore predefinito è troppo "dbo"), hello nome della tabella e il nome di colonna della tabella che contiene la chiave di partizionamento orizzontale hello hello.
2. Per ogni tabella di riferimento, creare un **ReferenceTableInfo** oggetto che descrive nome di schema della tabella hello padre (facoltativo, valore predefinito è troppo "dbo") e il nome di tabella hello.
3. Aggiungere hello sopra TableInfo oggetti tooa nuova **SchemaInfo** oggetto.
4. Ottenere un riferimento tooa **ShardMapManager** oggetto e chiamare **GetSchemaInfoCollection**.
5. Aggiungere hello **SchemaInfo** toohello **SchemaInfoCollection**, fornendo il nome della mappa partizioni hello.

Un esempio di questo può essere visualizzato in hello SetupSampleSplitMergeEnvironment.ps1 script.

Hello servizio di suddivisione unione non crea il database di destinazione hello (o dello schema per tutte le tabelle nel database di hello) per l'utente. Devono essere creati in precedenza prima di inviare un servizio toohello richiesta.

## <a name="troubleshooting"></a>Risoluzione dei problemi
Si può vedere hello messaggio seguente durante l'esecuzione di script di powershell di esempio hello:

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

Questo errore indica che il certificato SSL non è configurato correttamente. Seguire le istruzioni di hello nella sezione 'Connessione con un web browser'.

Se non è possibile inviare richieste, potrebbe essere visualizzato il seguente messaggio:

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

In questo caso, controllare il file di configurazione, in base alle impostazioni hello particolare per **WorkerRoleSynchronizationStorageAccountConnectionString**. Questo errore indica in genere che il ruolo di lavoro hello Impossibile inizializzare correttamente il database dei metadati hello al primo utilizzo. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png


---
title: "aaaMoving dati tra database cloud di scalabilità orizzontale | Documenti Microsoft"
description: "Illustra la modalità di partizioni toomanipulate e spostare i dati tramite un servizio indipendente elastica utilizzando le API di database."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 204fd902-0397-4185-985a-dea3ed7c7d9f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 629dee06e22609e9b61edf93ba5c38d997132d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-between-scaled-out-cloud-databases"></a>Spostamento di dati tra database cloud con scalabilità orizzontale
Se si è un Software come un sviluppatore del servizio e improvvisamente app sottoposto a grande richiesta, è necessario crescita hello tooaccommodate. A tale scopo aggiungerà altri database (partizioni). Come si ridistribuire hello dati toohello i nuovi database senza compromettere l'integrità dei dati di hello? Hello utilizzare **strumento di merge di divisione** dati toomove vincolata database toohello nuovi database.  

strumento di unione di menu combinato Hello viene eseguito come servizio web di Azure. Un amministratore o lo sviluppatore utilizza hello strumento toomove shardlet (dati da una partizione) tra i diversi database (partizioni). strumento Hello utilizza partizioni mappa toomaintain hello metadati database del servizio Gestione e verificare i mapping coerenti.

![Panoramica][1]

## <a name="download"></a>Download
[Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/)

## <a name="documentation"></a>Documentazione
1. [Esercitazione relativa allo strumento divisione-unione del database elastico](sql-database-elastic-scale-configure-deploy-split-and-merge.md)
2. [Configurazione della sicurezza dei servizi di "split and merge"](sql-database-elastic-scale-split-merge-security-configuration.md)
3. [Considerazioni sulla sicurezza dello strumento di suddivisione-unione](sql-database-elastic-scale-split-merge-security-configuration.md)
4. [Gestione mappe partizioni](sql-database-elastic-scale-shard-map-management.md)
5. [Eseguire la migrazione di database esistente tooscale-out](sql-database-elastic-convert-to-use-elastic-tools.md)
6. [Strumenti di database elastici](sql-database-elastic-scale-introduction.md)
7. [Glossario sugli strumenti di database elastici](sql-database-elastic-scale-glossary.md)

## <a name="why-use-hello-split-merge-tool"></a>Perché utilizzare lo strumento di unione di menu combinato hello?
**Flessibilità**

Le applicazioni devono toostretch in modo flessibile oltre i limiti di hello di un singolo database di database SQL di Azure. Utilizzare i dati di toomove strumento hello come i database necessari toonew mantenendo l'integrità.

**Split toogrow** 

È necessario tooincrease complessivo rapida crescita delle toohandle capacità. toodo, creare capacità aggiuntiva dai dati di partizionamento orizzontale hello e distribuendolo tra i database in modo incrementale più fino a quando non sono soddisfatte esigenze di capacità. Questo è un esempio di funzione 'split' hello. 

**Merge tooshrink**

Capacità è necessario compattare scadenza toohello carattere stagionale di un'azienda. unità di scala Hello strumento consente che ridurre toofewer quando business rallenta. funzionalità 'merge' Hello hello scalabilità elastica suddivisione unione servizio descrive questo requisito. 

**Gestire gli hotspot mediante lo spostamento di shardlet**

Con più tenant per ogni database, allocazione hello di shardlet tooshards può causare colli di bottiglia toocapacity su alcune partizioni. È necessario allocare nuovamente gli shardlet o lo spostamento toonew shardlet occupato o meno utilizzate partizioni. 

## <a name="concepts--key-features"></a>Concetti e funzionalità principali
**Servizi ospitati dal cliente**

suddivisione di Hello-unione viene recapitato come un servizio ospitato sul cliente. È necessario distribuire e ospitare il servizio di hello nella sottoscrizione di Microsoft Azure. pacchetto di Hello scaricati da NuGet contiene un toocomplete del modello di configurazione con le informazioni di hello per una distribuzione specifica. Vedere hello [esercitazione suddivisione unione](sql-database-elastic-scale-configure-deploy-split-and-merge.md) per informazioni dettagliate. Poiché il servizio di hello viene eseguito nella sottoscrizione di Azure, è possibile controllare e configurare la maggior parte degli aspetti di sicurezza del servizio di hello. modello predefinito Hello include hello opzioni tooconfigure SSL, l'autenticazione client basata su certificato, la crittografia per le credenziali archiviate, protegge DoS e le restrizioni IP. Sono disponibili ulteriori informazioni su hello gli aspetti di sicurezza seguente documento hello [configurazione della protezione di suddivisione unione](sql-database-elastic-scale-split-merge-security-configuration.md).

predefinito Hello distribuito viene eseguito il servizio con un unico ruolo web e di un lavoro. Ogni utilizza dimensioni della macchina virtuale A1 hello in servizi Cloud di Azure. Mentre è possibile modificare queste impostazioni quando si distribuisce il pacchetto di hello, è possibile modificare dopo una corretta distribuzione di hello in esecuzione il servizio cloud, (tramite hello portale di Azure). Si noti che il ruolo di lavoro hello non deve essere configurato per più di una singola istanza per motivi tecnici. 

**Integrazione della mappa partizioni**

il servizio di suddivisione unione Hello interagisce con mappa partizioni hello di un'applicazione hello. Quando si utilizza toosplit servizio di suddivisione unione hello o intervalli di unione o toomove shardlet tra le partizioni, il servizio hello mantiene automaticamente mappa partizioni hello backup toodate. toodo in tal caso, il servizio hello si connette toohello database manager mappa di partizione dell'applicazione hello e gestisce gli intervalli e i mapping come stato di avanzamento delle richieste di suddivisione/unione/spostamento. In questo modo la mappa partizioni hello sempre presenta una visualizzazione aggiornata quando le operazioni di unione di menu combinato sono in corso. Suddiviso, operazioni di spostamento di shardlet e di tipo merge vengono implementate tramite lo spostamento di un batch di shardlet dalla partizione di destinazione di hello origine partizione toohello. Durante la hello shardlet spostamento operazione hello shardlet soggetto toohello batch corrente sono contrassegnati come offline nella mappa partizioni hello e non sono disponibili per le connessioni di routine dipendente dai dati utilizzando hello **OpenConnectionForKey** API. 

**Connessioni a shardlet coerenti**

Quando lo spostamento dei dati viene avviata per un nuovo batch di shardlet, qualsiasi partizione-mappa fornita dipendente dai dati routing connessioni toohello partizioni archiviazione hello shardlet sono terminate e le successive connessioni da mappa partizioni hello toohello API queste shardlet sono bloccati mentre lo spostamento dei dati di Hello è in corso incoerenze tooavoid ordine. Gli shardlet tooother le connessioni sul hello stesso partizione verrà inoltre ottenere terminato, ma avrà esito positivo nuovamente immediatamente nel tentativo successivo. Dopo aver spostato batch hello, hello shardlet sono contrassegnati come online nuovamente per la partizione di destinazione hello e dati di origine hello viene rimosso dalla partizione di origine hello. servizio Hello passa questi passaggi per ogni batch fino a quando non sono stati spostati tutti gli shardlet. Questo comporta le operazioni di kill connessione tooseveral corso hello di completare l'operazione split/merge/spostamento hello.  

**Gestione della disponibilità di shardlet**

Limitazione della connessione hello la terminazione del batch corrente di toohello di shardlet, come illustrato in precedenza limita l'ambito hello del batch tooone indisponibilità di shardlet alla volta. Questo è preferibile un approccio in partizioni completa hello resta offline per tutti i relativi shardlet hello durante un'operazione di divisione o di unione. dimensioni Hello di un batch, definita come numero di hello di shardlet distinct toomove contemporaneamente, sono un parametro di configurazione. Può essere definito per ogni operazione di divisione e unione a seconda delle esigenze di disponibilità e prestazioni dell'applicazione hello. Si noti che l'intervallo di hello da bloccare nella mappa partizioni hello può essere più grande delle dimensioni di batch hello specificata. Questo avviene perché il servizio di hello rileva dimensioni dell'intervallo hello in modo che il numero effettivo di hello di valori di chiave di partizionamento orizzontale nei dati hello corrisponda circa dimensioni batch hello. Questo aspetto è importante tooremember soprattutto per le chiavi di partizionamento orizzontale scarsamente popolato. 

**Archiviazione dei metadati**

il servizio di suddivisione unione Hello utilizza un database toomaintain stato e tookeep registra durante l'elaborazione della richiesta. utente Hello crea il database nella propria sottoscrizione e prevede la stringa di connessione hello nel file di configurazione hello per la distribuzione del servizio hello. Gli amministratori dell'organizzazione dell'utente hello possono inoltre connettersi toothis lo stato di richiesta di database tooreview e tooinvestigate informazioni dettagliate in potenziali problemi.

**Rilevamento del partizionamento orizzontale**

il servizio di suddivisione unione Hello riconosce la differenza tra tabelle partizionate di (1), tabelle di riferimento (2) e (3) normali tabelle. la semantica di Hello di un'operazione di suddivisione/unione/spostamento dipende dal tipo di hello della tabella hello utilizzata e è definita come segue: 

* **Tabelle partizionate**: Split, merge e le operazioni di spostamento spostano gli shardlet dalla partizione di origine tootarget. Dopo il completamento di hello complessiva richiesta, tali shardlet non sono più presenti nell'origine hello. Si noti che le tabelle di destinazione di hello necessario tooexist nella partizione di destinazione hello e non devono contenere dati hello tooprocessing precedente intervallo destinazione dell'operazione di hello. 
* **Fare riferimento a tabelle**: per le tabelle di riferimento, hello split, merge e spostare le operazioni di copiare i dati di hello dalla partizione di destinazione toohello origine hello. Si noti, tuttavia, che non si verificano modifiche al partizione di destinazione hello per una determinata tabella se qualsiasi riga è già presente in questa tabella nella destinazione hello. tabella Hello è toobe vuota per qualsiasi tooget di operazione copia tabella di riferimento elaborati.
* **Altre tabelle**: altre tabelle possono essere presenti in hello origine o destinazione hello di un'operazione di divisione e unione. il servizio di suddivisione unione Hello Ignora queste tabelle per le operazioni di copia o lo spostamento dei dati. Si noti, tuttavia, che in caso di vincoli queste tabelle possono interferire con le operazioni.

Hello informazioni sul riferimento e tabelle partizionate vengono fornite da hello **SchemaInfo** API nella mappa partizioni hello. Hello seguente esempio di seguito viene illustrato l'utilizzo di hello di queste API in un oggetto smm di partizioni specificato mappa manager: 

    // Create hello schema annotations 
    SchemaInfo schemaInfo = new SchemaInfo(); 

    // Reference tables 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "region")); 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "nation")); 

    // Sharded tables 
    schemaInfo.Add(new ShardedTableInfo("dbo", "customer", "C_CUSTKEY")); 
    schemaInfo.Add(new ShardedTableInfo("dbo", "orders", "O_CUSTKEY")); 

    // Publish 
    smm.GetSchemaInfoCollection().Add(Configuration.ShardMapName, schemaInfo); 

Hello tabelle 'region' e 'nazione' sono definite come tabelle di riferimento verrà copiato con operazioni di suddivisione/unione/spostamento. "cliente" e "ordini" a loro volta sono definite come tabelle partizionate. C_CUSTKEY e O_CUSTKEY fungere da chiave di partizionamento orizzontale hello. 

**Integrità referenziale**

il servizio di suddivisione unione Hello analizza le dipendenze tra le tabelle e utilizza le operazioni di hello toostage relazioni di chiave primaria-chiave esterna per lo spostamento delle tabelle di riferimento e gli shardlet. Le tabelle di riferimento vengono in genere copiate per prime in ordine di dipendenza, quindi vengono copiati gli shardlet, in base al rispettivo ordine di dipendenza in ogni batch. Ciò è necessario in modo che vengono rispettati i vincoli di chiave esterna-chiave primaria nella partizione di destinazione hello in arrivo di nuovi dati hello. 

**Coerenza della mappa partizioni e completamento finale**

In presenza di hello di errori, il servizio di suddivisione unione hello riprende le operazioni dopo qualsiasi interruzione e ha lo scopo toocomplete qualsiasi nelle richieste di stato di avanzamento. Tuttavia, potrebbero esserci irreversibile situazioni, ad esempio, quando la partizione di destinazione hello viene perduto o danneggiato ripristinato. In tali circostanze, alcuni shardlet che doveva toobe spostato può continuare tooreside nella partizione di origine hello. servizio Hello assicura che i mapping di shardlet vengono aggiornati solo dopo i dati necessari hello destinazione toohello copiati correttamente. Gli Shardlet vengono eliminati solo nell'origine hello dopo che tutti i relativi dati sono stati copiati toohello destinazione e sono stati aggiornati i mapping corrispondente hello. l'operazione di eliminazione Hello avviene in background hello durante l'intervallo di hello è già online nella partizione di destinazione hello. servizio di suddivisione unione Hello garantisce sempre la correttezza dei mapping hello archiviato nella mappa partizioni hello.

## <a name="hello-split-merge-user-interface"></a>interfaccia utente di suddivisione unione Hello
pacchetto del servizio di suddivisione unione Hello include un ruolo di lavoro e un ruolo web. ruolo web Hello è le richieste di unione di menu combinato toosubmit utilizzato in modo interattivo. come indicato di seguito sono riportati i componenti principali di Hello dell'interfaccia utente di hello:

* Tipo di operazione: tipo di operazione hello è un pulsante di opzione che controlla il tipo di hello di operazione eseguita dal servizio hello per questa richiesta. È possibile scegliere tra hello split, merge e scenari di spostamento. È anche possibile annullare un'operazione inviata in precedenza. È possibile usare richieste di suddivisione, unione e spostamento per le mappe partizioni di tipo intervallo. Le mappe partizioni di tipo elenco supportano solo operazioni di spostamento.
* Mappa partizioni: sezione successiva hello di richiesta parametri copertura informazioni mappa partizioni hello e la mappa partizioni di hosting del database hello. In particolare, è necessario tooprovide hello nome del server di Database SQL di Azure hello e shardmap hello di hosting del database, partizioni di credenziali tooconnect toohello eseguire il mapping del database e infine hello Nome mappa partizioni hello. Attualmente, operazione hello accetta solo un singolo set di credenziali. Queste credenziali necessitano disporre delle autorizzazioni sufficienti di toohave tooperform modifica mappa partizioni toohello, nonché i dati utente toohello su partizioni hello.
* Intervallo di origine (suddivisione e unione): un'operazione di suddivisione e unione elabora un intervallo usando le relative chiavi superiore e inferiore. toospecify un'operazione con un unbounded valore di chiave superiore, controllo casella di controllo "chiave superiore è max" hello e lasciare vuota campo chiave elevata hello. Hello intervallo valori di chiave specificato non è necessario tooprecisely corrispondono ai limiti della mappa di partizione e un mapping. Se non si specifica i limiti di intervallo in qualsiasi servizio hello dedurrà intervallo più vicino hello è automaticamente. È possibile utilizzare hello PowerShell GetMappings.ps1 tooretrieve hello corrente i mapping degli script in una mappa partizioni specificato.
* Il comportamento di origine Split (divisione): per le operazioni di divisione, definire l'intervallo di origine di hello toosplit punto hello. Questo scopo è fornire una chiave di partizionamento orizzontale hello in cui si desidera hello divisa toooccur. Pulsante di opzione Usa hello specificare se si desidera parte inferiore di hello di hello toomove di intervallo (hello suddividere la chiave escluse) o se si desidera toomove parte superiore di hello (incluse chiave split hello).
* Origine Shardlet (spostare): spostare le operazioni sono diverse dalla divisione o operazioni di unione, in quanto non richiedono un'origine di hello toodescribe intervallo. Un'origine per lo spostamento è semplicemente identificata dal valore di chiave di partizionamento orizzontale hello pianificare toomove.
* Partizioni (divisione) di destinazione: dopo avere fornito hello informazioni sull'origine hello dell'operazione di divisione, è necessario toodefine in cui si desidera hello dati toobe copiati server di database SQL di Azure tooby fornendo hello e nome del database di destinazione hello.
* Intervallo di destinazione (unione): le operazioni di unione spostare gli shardlet tooan esistente partizioni. Per identificare partizioni esistenti hello, fornendo i limiti di intervallo esistente hello che si desidera toomerge con intervallo di hello.
* Dimensione batch: controlli di dimensioni di batch hello hello numero di shardlet che andrà offline contemporaneamente durante lo spostamento dei dati di hello. Si tratta di un valore intero in cui è possibile utilizzare i valori inferiori e si toolong sensibili i tempi di inattività per gli shardlet. Valori più grandi aumenta il tempo necessario hello che un determinato shardlet è offline ma può migliorare le prestazioni.
* Id operazione (Annulla): Se si dispone di un'operazione in corso che non è più necessario, è possibile annullare operazione hello fornendo l'ID operazione in questo campo. È possibile recuperare l'ID operazione hello dalla tabella di stato richiesta hello (vedere la sezione 8.1) oppure dall'output di hello nel browser web hello in cui è stato inviato richiesta hello.

## <a name="requirements-and-limitations"></a>Requisiti e limitazioni
Hello l'implementazione corrente del servizio di suddivisione unione hello è soggetto toohello seguenti requisiti e limitazioni: 

* partizioni Hello necessario tooexist ed essere registrate nella mappa partizioni hello prima di poter eseguire un'operazione di unione di menu combinato su tali partizioni. 
* servizio Hello non crea le tabelle o altri oggetti di database automaticamente come parte delle operazioni. Ciò significa che hello dello schema per tabelle partizionate tutti e fanno riferimento a tabelle necessario tooexist sull'operazione di suddivisione/unione/spostamento di hello destinazione partizioni tooany precedente. Tabelle partizionate, in particolare, sono necessari toobe vuota nell'intervallo di hello in nuovi shardlet sono toobe aggiunte da un'operazione di suddivisione/unione/spostamento. In caso contrario, hello operazione non riuscirà hello iniziale verifica di coerenza nella partizione di destinazione hello. Si noti che i dati di riferimento viene copiati solo se la tabella di riferimento hello è vuota e che non esistono alcun coerenza garantisce anche con le operazioni di scrittura simultanee tooother considerare nelle tabelle di riferimento hello. È consigliabile questo: durante l'esecuzione di operazioni di suddivisione/unione, senza altre operazioni di scrittura di apportare modifiche toohello tabelle di riferimento.
* servizio Hello si basa su identità di riga definita da un indice univoco o chiave che include prestazioni tooimprove chiave di partizionamento orizzontale hello e affidabilità per gli shardlet di grandi dimensioni. In questo modo sarà possibile dati toomove del servizio hello un'anche maggiore granularità rispetto appena hello partizionamento orizzontale valore della chiave. In questo modo quantità massima di hello tooreduce di spazio del log e i blocchi che sono necessari durante l'operazione di hello. È consigliabile creare un indice univoco o chiave primaria tra la chiave di partizionamento orizzontale hello in una tabella specificata, se si desidera toouse tale tabella con le richieste di suddivisione/unione/spostamento. Per motivi di prestazioni chiave di partizionamento orizzontale hello deve essere hello iniziali colonne chiave hello hello indici o.
* Corso hello di elaborazione delle richieste, alcuni dati shardlet possono essere presenti sia in origine hello e partizioni di destinazione hello. Si tratta tooprotect necessarie in caso di errori durante lo spostamento di shardlet hello. Hello integrazione di suddivisione-unione con mappa partizioni hello assicura che le connessioni tramite hello dati dipendenti routing API hello **OpenConnectionForKey** metodo nella mappa partizioni hello non vengono visualizzati tutti gli stati intermedi non coerenti. Tuttavia, se connessione origine toohello o hello destinazione partizioni senza utilizzare hello **OpenConnectionForKey** (metodo), gli stati intermedi non coerenti potrebbero essere visibili quando sono richieste di suddivisione/unione/spostamento in corso.. Queste connessioni possono visualizzare i risultati parziali o duplicati in base a temporizzazione hello o connessione hello sottostante di hello partizioni. Questa limitazione attualmente include le connessioni hello dalla scalabilità elastica Multi-Shard-query.
* database dei metadati Hello per il servizio di suddivisione unione hello non deve essere condivise tra diversi ruoli. Ad esempio, un ruolo del servizio di suddivisione unione hello in esecuzione in gestione temporanea deve toopoint tooa metadati diversi database di ruolo di produzione hello.

## <a name="billing"></a>Fatturazione
il servizio di suddivisione unione Hello viene eseguito come servizio cloud nella sottoscrizione di Microsoft Azure. Pertanto di tooyour istanza del servizio hello vengano addebitati costi per i servizi cloud. Se non si eseguono spesso operazioni di suddivisione/unione/spostamento, è consigliabile eliminare il servizio cloud di suddivisione-unione, in modo da ridurre i costi per le istanze dei servizi cloud in esecuzione o distribuite. È possibile distribuire di nuovo e iniziare la configurazione eseguibile immediatamente ogni volta che è necessario tooperform dividere o unire le operazioni. 

## <a name="monitoring"></a>Monitoraggio
### <a name="status-tables"></a>Tabelle di stato
Servizio di suddivisione unione Hello fornisce hello **RequestStatus** tabella nel database dell'archivio di metadati hello per il monitoraggio delle richieste in corso e completate. Hello tabella una riga per ogni richiesta di unione di menu combinato che è stato inviato toothis istanza del servizio di suddivisione unione hello. Fornisce le seguenti informazioni per ogni richiesta hello:

* **Timestamp**: hello ora e data di inizio richiesta hello.
* **ID operazione**: un GUID che identifica in modo univoco la richiesta hello. Questa richiesta può essere anche usato toocancel hello operazione mentre è ancora in corso.
* **Stato**: hello stato corrente della richiesta di hello. Per le richieste in corso, vengono anche elencate hello fase corrente in cui hello è richiesta.
* **CancelRequest**: un flag che indica se la richiesta hello è stata annullata.
* **Lo stato di avanzamento**: una stima della percentuale di completamento per l'operazione di hello. Un valore pari a 50 indica che l'operazione di hello è circa il 50% completato.
* **Details**: valore XML che fornisce un report di stato più dettagliato. report stato di avanzamento Hello viene aggiornato periodicamente come set di righe vengono copiate dal tootarget di origine. In caso di errori o eccezioni, questa colonna include inoltre informazioni più dettagliate sull'errore hello.

### <a name="azure-diagnostics"></a>Diagnostica Azure
il servizio di suddivisione unione Hello Usa diagnostica Azure basato su Azure SDK 2.5 per il monitoraggio e diagnostica. Controllare la configurazione di diagnostica hello come illustrato qui: [abilitazione di diagnostica in servizi Cloud di Azure e macchine virtuali](../cloud-services/cloud-services-dotnet-diagnostics.md). pacchetto di download Hello include due configurazioni di diagnostica - uno per ruolo web hello e uno per il ruolo di lavoro hello. Queste configurazioni di diagnostica per il servizio hello attenersi alle linee guida hello [nozioni di base del servizio Cloud in Microsoft Azure](https://code.msdn.microsoft.com/windowsazure/Cloud-Service-Fundamentals-4ca72649). Include hello definizioni toolog i contatori delle prestazioni, log IIS, registri eventi di Windows e registri eventi applicazioni di unione di menu combinato. 

## <a name="deploy-diagnostics"></a>Distribuire la diagnostica
tooenable il monitoraggio e diagnostica usando la configurazione di diagnostica hello per i ruoli di lavoro e web hello forniti dal pacchetto NuGet hello, eseguire hello comandi usando Azure PowerShell seguente: 

    $storage_name = "<YourAzureStorageAccount>" 

    $key = "<YourAzureStorageAccountKey" 

    $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key  


    $config_path = "<YourFilePath>\SplitMergeWebContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWeb" 


    $config_path = "<YourFilePath>\SplitMergeWorkerContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWorker" 

È possibile trovare ulteriori informazioni su come tooconfigure e distribuire le impostazioni di diagnostica: [abilitazione di diagnostica in servizi Cloud di Azure e macchine virtuali](../cloud-services/cloud-services-dotnet-diagnostics.md). 

## <a name="retrieve-diagnostics"></a>Recuperare la diagnostica
È possibile accedere facilmente i dati di diagnostica da hello Esplora Server Visual Studio in Azure parte della struttura ad albero di Esplora Server hello hello. Aprire un'istanza di Visual Studio e sulla barra dei menu hello fare clic su Visualizza e a Esplora Server. Fare clic su hello icona Azure tooconnect tooyour sottoscrizione di Azure. Passare quindi tooAzure -> archiviazione -> <your storage account> -> tabelle -> WADLogsTable. Per altre informazioni, vedere [Esplorazione delle risorse di archiviazione con Esplora server](http://msdn.microsoft.com/library/azure/ff683677.aspx). 

![WADLogsTable][2]

Hello WADLogsTable evidenziati nella figura hello precedente contiene hello eventi dal registro applicazioni del servizio di suddivisione unione hello dettagliati. Si noti che la configurazione predefinita hello di hello scaricato pacchetto si concentri su una distribuzione di produzione. Pertanto intervallo hello vengono estratti i registri e i contatori da istanze del servizio hello è di grandi dimensioni (5 minuti). Per sviluppo e test, è necessario inferiore intervallo hello modificando le impostazioni di diagnostica hello di web hello o tooyour ruolo di lavoro hello. Fare clic sul ruolo hello in hello Esplora Server di Visual Studio (vedere sopra), quindi modificare hello periodo di trasferimento nella finestra di dialogo di hello per le impostazioni di configurazione di diagnostica hello: 

![Configurazione][3]

## <a name="performance"></a>Prestazioni
In generale, prestazioni migliori sono toobe previsto dal hello superiore, più i livelli di servizio ad alte prestazioni nel Database SQL di Azure. Superiore delle allocazioni dei / o, memoria e CPU per i livelli di servizio superiore hello vantaggio hello la copia bulk e le operazioni che Usa servizio di suddivisione unione hello di eliminazione. Per questo motivo, aumentare il livello di servizio hello solo per i database per un periodo di tempo definito limitato.

servizio Hello esegue inoltre query convalida come parte delle normale operazioni. Queste query convalida controllare imprevisto presenza di dati nell'intervallo di destinazione hello e assicurarsi che qualsiasi operazione di suddivisione/unione/spostamento inizia da uno stato coerente. Queste query tutti funzionano su intervalli di chiavi di partizionamento orizzontale definiti dall'ambito di hello dell'operazione di hello e dimensioni di batch hello fornite come parte della definizione di richiesta di hello. Queste query prestazioni ottimali quando un indice è presente con la chiave di partizionamento orizzontale hello hello colonna iniziale. 

Inoltre, una proprietà di univocità con la chiave di partizionamento orizzontale hello come colonna iniziale hello consentirà hello servizio toouse un approccio ottimizzato che limita il consumo di risorse in termini di memoria e spazio del log. Questa proprietà di unicità è necessario toomove le dimensioni di dati di grandi dimensioni (in genere superiore a 1GB). 

## <a name="how-tooupgrade"></a>Come tooupgrade
1. Seguire i passaggi di hello in [distribuire un servizio di suddivisione unione](sql-database-elastic-scale-configure-deploy-split-and-merge.md).
2. Modificare il file di configurazione del servizio cloud per il distribuzione di suddivisione unione tooreflect hello nuovi parametri di configurazione. Un nuovo parametro richiesto è informazioni hello sul certificato di hello utilizzato per la crittografia. Un modo semplice di toodo toocompare hello nuova configurazione file di modello dal download hello contro la configurazione esistente. Assicurarsi di aggiungere le impostazioni di hello per "DataEncryptionPrimaryCertificateThumbprint" e "DataEncryptionPrimary" per il ruolo di lavoro hello e web hello.
3. Prima di distribuire hello tooAzure di aggiornamento, assicurarsi che vengono completate tutte le operazioni split-merge attualmente in esecuzione. È possibile farlo facilmente eseguendo query sulle tabelle di RequestStatus e PendingWorkflows hello nel database dei metadati di merge di divisione hello per le richieste in corso.
4. Aggiornare la distribuzione del servizio cloud esistente per l'unione di menu combinato nella sottoscrizione di Azure con il nuovo pacchetto di hello e il file di configurazione di servizio aggiornato.

Non è necessario tooprovision un nuovo database di metadati per l'unione di menu combinato tooupgrade. nuova versione di Hello comporta l'aggiornamento automatico dei metadati del database toohello nuova versione esistente. 

## <a name="best-practices--troubleshooting"></a>Procedure consigliate e risoluzione dei problemi
* Definire un tenant di prova e sperimentare le principali operazioni di suddivisione/unione/spostamento con tenant di prova hello tra partizioni diverse. Verificare che tutti i metadati sia definito correttamente nella mappa partizioni e che le operazioni di hello non violino i vincoli o le chiavi esterne.
* Dimensioni dei dati tenant test hello Keep sopra hello dimensione massima di dati più grande tenant tooensure non si è verificato la dimensione dei dati correlati. Ciò consente di valutare hello tempo toomove un singolo tenant intorno a un limite superiore. 
* Assicurarsi che lo schema consenta le eliminazioni. il servizio di suddivisione unione Hello richiede dei dati dalla partizione di origine hello tooremove possibilità hello dopo aver copiato toohello destinazione dati hello. Ad esempio, **trigger delete** può impedire l'eliminazione di dati hello origine hello servizio hello e potrebbe essere toofail operazioni.
* chiave di partizionamento orizzontale Hello deve essere la colonna iniziale di hello la chiave primaria o una definizione di indice univoco. Questo garantisce prestazioni ottimali hello hello query convalida divisione o di unione e per hello operazioni lo spostamento e l'eliminazione di dati effettivi che funzionano sempre in intervalli di chiavi di partizionamento orizzontale.
* Colloca il servizio di suddivisione unione nel centro dati e area in cui si trovano i database, hello. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-overview-split-and-merge/split-merge-overview.png
[2]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics.png
[3]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics-config.png


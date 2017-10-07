---
title: emulatore di archiviazione di Azure hello aaaUse per lo sviluppo e test | Documenti Microsoft
description: "emulatore di archiviazione di Azure Hello offre un ambiente di sviluppo locale disponibile per lo sviluppo e il testing delle applicazioni di servizio di archiviazione Azure. Informazioni su come le richieste vengono autenticate, come emulatore toohello tooconnect dall'applicazione, nonché come toouse hello strumento da riga di comando."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: f480b059-df8a-4a63-b05a-7f2f5d1f5c2a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: marsma
ms.openlocfilehash: 7cbe6ef5f172bb526c9d8a329b2fe9e6c0ec59d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-storage-emulator-for-development-and-testing"></a>Utilizzare l'emulatore di archiviazione Azure hello per lo sviluppo e test

emulatore di archiviazione di Microsoft Azure Hello fornisce un ambiente locale in grado di emulare servizi hello di tabella, di accodamento e Blob di Azure per scopi di sviluppo. Usa emulatore di archiviazione hello, è possibile testare l'applicazione nei servizi di archiviazione hello localmente, senza creare una sottoscrizione di Azure o eventuali costi. Quando si è soddisfatti delle modalità di funzionamento dell'applicazione nell'emulatore hello, è possibile passare un account di archiviazione di Azure nel cloud hello toousing.

## <a name="get-hello-storage-emulator"></a>Ottenere l'emulatore di archiviazione hello
Hello emulatore di archiviazione è disponibile come parte di hello [Microsoft Azure SDK](https://azure.microsoft.com/downloads/). È inoltre possibile installare l'emulatore di archiviazione hello utilizzando hello [programma di installazione autonomo](https://go.microsoft.com/fwlink/?linkid=717179&clcid=0x409) (download diretto). emulatore di archiviazione hello tooinstall, è necessario disporre dei privilegi di amministratore nel computer in uso.

emulatore di archiviazione Hello attualmente viene eseguita solo su Windows. Per coloro che considerano un emulatore di archiviazione per Linux, un'opzione è community hello mantenuta, l'emulatore di archiviazione di origine aprire [Azurite](https://github.com/arafato/azurite).

> [!NOTE]
> Dati creati in una versione dell'emulatore di archiviazione hello non sono garantiti toobe accessibili quando si utilizza una versione diversa. Se è necessario toopersist i dati a lungo termine hello, è consigliabile archiviare i dati in un account di archiviazione di Azure anziché nell'emulatore di archiviazione hello.
> <p/>
> emulatore di archiviazione Hello dipende dalle specifiche versioni di librerie OData hello. Sostituzione di DLL di OData hello usato dall'emulatore di archiviazione hello con altre versioni non è supportata e può causare comportamenti imprevisti. Tuttavia, qualsiasi versione di OData supportata dal servizio di archiviazione hello può essere utilizzato toosend richieste toohello emulatore.
>

## <a name="how-hello-storage-emulator-works"></a>Funzionamento dell'emulatore di archiviazione hello
emulatore di archiviazione Hello utilizza un'istanza locale di Microsoft SQL Server e servizi di archiviazione Azure tooemulate sistema hello file locale. Per impostazione predefinita, l'emulatore di archiviazione hello utilizza un database in Microsoft SQL Server 2012 Express LocalDB. È possibile scegliere tooconfigure hello archiviazione emulatore tooaccess un'istanza locale di SQL Server anziché l'istanza di LocalDB hello. Per ulteriori informazioni, vedere hello [inizio e inizializzazione dell'emulatore di archiviazione di hello](#start-and-initialize-the-storage-emulator) sezione più avanti in questo articolo.

emulatore di archiviazione Hello connette tooSQL Server o a LocalDB mediante l'autenticazione di Windows.

Esistono alcune differenze nelle funzionalità tra l'emulatore di archiviazione hello e servizi di archiviazione Azure. Per ulteriori informazioni su queste differenze, vedere hello [differenze tra l'emulatore di archiviazione hello e archiviazione di Azure](#differences-between-the-storage-emulator-and-azure-storage) sezione più avanti in questo articolo.

## <a name="start-and-initialize-hello-storage-emulator"></a>Avviare e inizializzare l'emulatore di archiviazione hello
toostart hello emulatore di archiviazione Azure:
1. Seleziona hello **avviare** hello o preme **Windows** chiave.
1. Iniziare a digitare `Azure Storage Emulator`.
1. Selezionare emulatore hello hello elenco di applicazioni visualizzate.

Quando viene avviato l'emulatore di archiviazione hello, verrà visualizzata una finestra del prompt dei comandi. È possibile utilizzare questa console finestra toostart e arrestare hello emulatore di archiviazione, cancellare i dati, ottenere lo stato e inizializzare emulatore hello. Per ulteriori informazioni, vedere hello [riferimento dello strumento da riga di comando emulatore di archiviazione](#storage-emulator-command-line-tool-reference) sezione più avanti in questo articolo.

Quando l'emulatore di hello è in esecuzione, si noterà un'icona nell'area di notifica della barra delle applicazioni di Windows hello.

Quando si chiude una finestra prompt dei comandi dell'emulatore di archiviazione hello, l'emulatore di archiviazione hello continuerà toorun. toobring la finestra di console hello emulatore di archiviazione di nuovo, seguire passaggi precedenti, come se avviare l'emulatore di archiviazione hello hello.

Hello prima esecuzione dell'emulatore di archiviazione hello, ambiente di archiviazione locale hello viene inizializzato automaticamente. il processo di inizializzazione Hello crea un database in LocalDB e riserva le porte HTTP per ogni servizio di archiviazione locale.

emulatore di archiviazione Hello è installato per impostazione predefinita troppo`C:\Program Files (x86)\Microsoft SDKs\Azure\Storage Emulator`.

> [!TIP]
> È possibile utilizzare hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) toowork con risorse dell'emulatore di archiviazione locale. Cercare "(sviluppo)" in "Account di archiviazione" nella struttura ad albero di hello archiviazione Esplora risorse dopo aver installato e avviato l'emulatore di archiviazione hello.
>

### <a name="initialize-hello-storage-emulator-toouse-a-different-sql-database"></a>Inizializzare toouse emulatore di archiviazione hello un altro database SQL
È possibile utilizzare hello archiviazione emulatore strumento da riga di comando tooinitialize hello archiviazione emulatore toopoint tooa SQL database istanza diversa istanza di LocalDB predefinita hello:

1. Finestra della console dell'emulatore di archiviazione hello aperta come descritto in hello [inizio e inizializzazione dell'emulatore di archiviazione di hello](#start-and-initialize-the-storage-emulator) sezione.
1. Nella finestra della console hello, digitare hello seguente comando, in cui `<SQLServerInstance>` hello nome dell'istanza di SQL Server hello. toouse LocalDB, specificare `(localdb)\MSSQLLocalDb` come istanza di SQL Server hello.

  `AzureStorageEmulator.exe init /server <SQLServerInstance>`

  È inoltre possibile utilizzare hello comando, che indirizza hello emulatore toouse hello istanza predefinita di SQL Server seguente:

  `AzureStorageEmulator.exe init /server .\\`

  In alternativa, è possibile utilizzare hello comando, che reinizializza l'istanza di LocalDB hello database toohello predefinita seguente:

  `AzureStorageEmulator.exe init /forceCreate`

Per altre informazioni su questi comandi, vedere [Informazioni di riferimento sullo strumento da riga di comando dell'emulatore di archiviazione](#storage-emulator-command-line-tool-reference).

> [!TIP]
> È possibile utilizzare hello [Microsoft SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms) toomanage (SSMS) istanze di SQL Server, inclusi installazione LocalDB hello. In hello SMSS **connettersi tooServer** finestra di dialogo, specificare `(localdb)\MSSQLLocalDb` in hello **nome Server:** istanza LocalDB toohello tooconnect di campo.

## <a name="authenticating-requests-against-hello-storage-emulator"></a>Autenticazione delle richieste nell'emulatore di archiviazione hello
Dopo aver installato e avviato l'emulatore di archiviazione hello, è possibile testare il codice su di essa. Come con l'archiviazione di Azure nel cloud hello, ogni richiesta effettuata nell'emulatore di archiviazione hello deve essere autenticata, a meno che non è una richiesta anonima. È possibile autenticare le richieste nell'emulatore di archiviazione hello utilizzando l'autenticazione chiave condivisa o con una firma di accesso condiviso (SAS).

### <a name="authenticate-with-shared-key-credentials"></a>Autenticazione con credenziali con chiave condivisa
[!INCLUDE [storage-emulator-connection-string-include](../../../includes/storage-emulator-connection-string-include.md)]

Per altre informazioni sulle stringhe di connessione, vedere [Configurare le stringhe di connessione di Archiviazione di Azure](../storage-configure-connection-string.md).

### <a name="authenticate-with-a-shared-access-signature"></a>Eseguire l'autenticazione con una firma di accesso condiviso
Alcune librerie client di archiviazione di Azure, ad esempio libreria Xamarin hello, supportano solo l'autenticazione con un token di firma di accesso condiviso. È possibile creare token SAS hello usando uno strumento come hello [Esplora archivi](http://storageexplorer.com/) o un'altra applicazione che supporta l'autenticazione chiave condivisa.

È anche possibile generare un token di firma di accesso condiviso usando Azure PowerShell. Hello esempio seguente genera un token di firma di accesso condiviso con il contenitore di blob tooa le autorizzazioni complete:

1. Se hai già fatto, installare Azure PowerShell (uso hello la versione più recente dei cmdlet di Azure PowerShell hello è consigliato). Per le istruzioni di installazione, vedere [Installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps).
2. Aprire Azure PowerShell ed eseguire i comandi seguenti, la sostituzione di hello `ACCOUNT_NAME` e `ACCOUNT_KEY==` con le proprie credenziali, e `CONTAINER_NAME` con un nome di propria scelta:

```powershell
$context = New-AzureStorageContext -StorageAccountName "ACCOUNT_NAME" -StorageAccountKey "ACCOUNT_KEY=="

New-AzureStorageContainer CONTAINER_NAME -Permission Off -Context $context

$now = Get-Date

New-AzureStorageContainerSASToken -Name CONTAINER_NAME -Permission rwdl -ExpiryTime $now.AddDays(1.0) -Context $context -FullUri
```

Hello risultante firma di accesso condiviso URI per il nuovo contenitore di hello dovrebbe essere simile a:

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2015-07-08T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3Dsss
```

firma di accesso condiviso Hello creato con questo esempio è valido per un giorno. firma Hello concede l'accesso completo (lettura, scrittura, eliminazione, elenco) tooblobs all'interno del contenitore di hello.

Per altre informazioni sulle firme di accesso condiviso, vedere [Uso delle firme di accesso condiviso in Archiviazione di Azure](../storage-dotnet-shared-access-signature-part-1.md).

## <a name="addressing-resources-in-hello-storage-emulator"></a>Indirizzamento delle risorse nell'emulatore di archiviazione hello
endpoint del servizio per l'emulatore di archiviazione hello Hello sono diversi da quelli di un account di archiviazione di Azure. differenza Hello infatti il computer locale hello non esegue la risoluzione dei nomi di dominio, che richiedono gli indirizzi locali di hello archiviazione emulatore endpoint toobe.

Quando si indirizza una risorsa in un account di archiviazione di Azure, utilizzare hello segue lo schema. nome dell'account Hello è parte del nome host dell'URI hello e risorsa hello indirizzata fa parte del percorso dell'URI hello:

`<http|https>://<account-name>.<service-name>.core.windows.net/<resource-path>`

Ad esempio, hello seguente URI è un indirizzo valido per un blob in un account di archiviazione di Azure:

`https://myaccount.blob.core.windows.net/mycontainer/myblob.txt`

Tuttavia, hello emulatore di archiviazione, perché il computer locale hello non eseguire la risoluzione dei nomi di dominio, nome dell'account hello è parte del percorso dell'URI hello anziché il nome host hello. Utilizzare hello seguendo il formato dell'URI per una risorsa nell'emulatore di archiviazione hello:

`http://<local-machine-address>:<port>/<account-name>/<resource-path>`

Ad esempio, hello indirizzo seguente può essere usato per accedere a un blob nell'emulatore di archiviazione hello:

`http://127.0.0.1:10000/myaccount/mycontainer/myblob.txt`

endpoint del servizio per l'emulatore di archiviazione hello Hello sono:

* Servizio BLOB: `http://127.0.0.1:10000/<account-name>/<resource-path>`
* Servizio di accodamento: `http://127.0.0.1:10001/<account-name>/<resource-path>`
* Servizio tabelle: `http://127.0.0.1:10002/<account-name>/<resource-path>`

### <a name="addressing-hello-account-secondary-with-ra-grs"></a>Indirizzamento account hello secondario con RA-GRS
A partire dalla versione 3.1, l'emulatore di archiviazione hello supporta la replica con ridondanza geografica e accesso in lettura (RA-GRS). Per le risorse di archiviazione nel cloud hello e nell'emulatore locale hello, è possibile accedere a posizione secondaria hello aggiungendo - nome dell'account toohello secondario. Ad esempio, hello seguente indirizzo può essere usato per l'accesso a un blob mediante la replica secondaria di sola lettura hello nell'emulatore di archiviazione hello:

`http://127.0.0.1:10000/myaccount-secondary/mycontainer/myblob.txt`

> [!NOTE]
> Per l'accesso programmatico toohello secondario con l'emulatore di archiviazione hello, usare hello libreria Client di archiviazione per .NET versione 3.2 o successive. Vedere hello [Microsoft Azure Storage Client Library per .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx) per informazioni dettagliate.
>
>

## <a name="storage-emulator-command-line-tool-reference"></a>Riferimenti allo strumento da riga di comando emulatore di archiviazione
A partire dalla versione 3.0, una finestra della console viene visualizzata quando si avvia emulatore di archiviazione hello. Utilizzare la riga di comando hello hello console finestra toostart e arrestare hello emulatore, nonché query per lo stato ed eseguire altre operazioni.

> [!NOTE]
> Se si dispone di hello installato emulatore di calcolo di Microsoft Azure, viene visualizzata un'icona nella barra delle applicazioni quando si avvia emulatore di archiviazione hello. Fare clic su hello icona tooreveal un menu che consente un toostart modo visivo e arrestare hello emulatore di archiviazione.
>
>

### <a name="command-line-syntax"></a>Sintassi della riga di comando
`AzureStorageEmulator.exe [start] [stop] [status] [clear] [init] [help]`

### <a name="options"></a>Opzioni
elenco di hello tooview di opzioni, digitare `/help` al prompt dei comandi di hello.

| Opzione | Descrizione | Comando | Argomenti |
| --- | --- | --- | --- |
| **Inizia** |Avvio dell'emulatore di archiviazione hello. |`AzureStorageEmulator.exe start [-inprocess]` |*-in-Process*: avviare l'emulatore hello nel processo corrente di hello anziché creare un nuovo processo. |
| **Stop** |Emulatore di archiviazione hello viene arrestata. |`AzureStorageEmulator.exe stop` | |
| **Status** |Stampa hello lo stato dell'emulatore di archiviazione hello. |`AzureStorageEmulator.exe status` | |
| **Cancella** |Cancella dati hello in tutti i servizi specificati nella riga di comando hello. |`AzureStorageEmulator.exe clear [blob] [table] [queue] [all]                                                    ` |*blob*: cancella i dati BLOB. <br/>*queue*: cancella i dati della coda. <br/>*table*: cancella i dati delle tabelle. <br/>*all*: cancella tutti i dati in tutti i servizi. |
| **Init** |Esegue un'inizializzazione una tantum tooset emulatore hello. |<code>AzureStorageEmulator.exe init [-server serverName] [-sqlinstance instanceName] [-forcecreate&#124;-skipcreate] [-reserveports&#124;-unreserveports] [-inprocess]</code> |*-server nomeserver\nomeistanza*: Specifica il server di hello ospita l'istanza SQL hello. <br/>*instanceName - sqlinstance*: Specifica il nome di hello di hello toobe di istanza SQL utilizzato nell'istanza del server predefinita hello. <br/>*-forcecreate*: forza la creazione di database SQL di hello, anche se esiste già. <br/>*-skipcreate*: ignora la creazione del database SQL di hello. Questa opzione ha la precedenza sull'opzione -forcecreate.<br/>*-reserveports*: tenta porte hello HTTP tooreserve associate ai servizi hello.<br/>*-unreserveports*: tenta prenotazioni tooremove per le porte HTTP hello associate ai servizi hello. Questa opzione ha la precedenza sull'opzione -reserveports.<br/>*-in-Process*: esegue l'inizializzazione nel processo corrente di hello anziché generare un nuovo processo. processo corrente Hello deve essere avviato con autorizzazioni elevate se si modificano le prenotazioni di porte. |

## <a name="differences-between-hello-storage-emulator-and-azure-storage"></a>Differenze tra l'emulatore di archiviazione hello e archiviazione di Azure
Poiché l'emulatore di archiviazione hello è un ambiente di emulato in esecuzione in un'istanza locale di SQL, esistono differenze nelle funzionalità tra l'emulatore hello e un account di archiviazione di Azure nel cloud hello:

* emulatore di archiviazione Hello supporta solo un singolo account fisso e una chiave di autenticazione noto.
* emulatore di archiviazione Hello non è un servizio di archiviazione scalabile e non supporta un numero elevato di client simultanei.
* Come descritto in [indirizzamento delle risorse nell'emulatore di archiviazione hello](#addressing-resources-in-the-storage-emulator), le risorse vengono indirizzate in modo diverso nell'emulatore di archiviazione hello rispetto a un account di archiviazione di Azure. Questa differenza è perché la risoluzione dei nomi di dominio è disponibile nel cloud hello ma non nei computer locali di hello.
* A partire dalla versione 3.1, l'account dell'emulatore di archiviazione hello supporta la replica con ridondanza geografica e accesso in lettura (RA-GRS). Nell'emulatore hello, dispongano di tutti gli account RA-GRS è abilitata e non sono mai intervalli tra repliche primarie e secondarie hello. le operazioni Get Blob Service Stats e Get Queue Service Stats Get Table Service Stats Hello sono supportate negli account hello secondario e restituiscono sempre il valore di hello di hello `LastSyncTime` elemento risposta come hello corrente tempo secondo toohello sottostante Database SQL.
* servizio File Hello e gli endpoint del servizio protocollo SMB non sono attualmente supportati nell'emulatore di archiviazione hello.
* Se si utilizza una versione di servizi di archiviazione hello che non è ancora supportata dall'emulatore hello, l'emulatore di archiviazione hello restituisce un errore di VersionNotSupportedByEmulator (codice di stato HTTP 400 - richiesta non valida).

### <a name="differences-for-blob-storage"></a>Differenze per l'archiviazione BLOB
Hello le differenze seguenti si applica tooBlob archiviazione nell'emulatore hello:

* emulatore di archiviazione Hello supporta solo dimensioni di blob too2 GB.
* Copia incrementale consente di snapshot da sovrascrivere i BLOB toobe copiato, che restituisce un errore nel servizio hello.
* Get Page Ranges Diff non funziona con gli snapshot copiati usando il BLOB di copia incrementale.
* Un'operazione Put Blob può essere completata su un blob che esiste nell'emulatore di archiviazione hello con un lease attivo, anche se non è stato specificato alcun ID lease hello nella richiesta di hello.
* Aggiungere le operazioni non sono supportate dall'emulatore hello Blob. Se si tenta un'operazione su un blob di Accodamento restituisce un errore FeatureNotSupportedByEmulator (codice di stato HTTP 400 - richiesta non valida).

### <a name="differences-for-table-storage"></a>Differenze per l'archiviazione tabelle
Hello le differenze seguenti si applica tooTable archiviazione nell'emulatore hello:

* Le proprietà di data nel servizio tabelle nell'emulatore di archiviazione hello hello supportano solo i intervallo hello è supportato da SQL Server 2005 (sono necessari toobe entro il 1 gennaio 1753). Tutte le date precedenti al 1 ° gennaio 1753 vengono modificate toothis valore. la precisione delle date Hello è limitato toohello precisione di SQL Server 2005, vale a dire che le date sono precise too1/300 di secondo.
* emulatore di archiviazione Hello supporta valori di proprietà chiave di riga e di chiave di partizione meno di 512 byte ogni. Inoltre, dimensione totale di hello del nome dell'account hello, nome della tabella e i nomi delle proprietà chiave insieme non può superare i 900 byte.
* dimensione totale di Hello di una riga in una tabella nell'emulatore di archiviazione hello è tooless limitata a 1 MB.
* Nell'emulatore di archiviazione hello, proprietà dei dati tipo `Edm.Guid` o `Edm.Binary` supporto hello solo `Equal (eq)` e `NotEqual (ne)` nella query, gli operatori di confronto di stringhe di filtro.

### <a name="differences-for-queue-storage"></a>Differenze per l'archiviazione di accodamento
Non esistono archiviazione tooQueue specifiche differenze nell'emulatore hello.

## <a name="storage-emulator-release-notes"></a>Note sulla versione dell'emulatore di archiviazione
### <a name="version-52"></a>Versione 5.2
* emulatore di archiviazione Hello supporta ora la versione 2017-04-17 dei servizi di archiviazione hello sugli endpoint di servizio Blob, coda e tabella.
* È stato risolto un bug per cui i valori delle proprietà di tabella non venivano codificati correttamente.

### <a name="version-51"></a>Versione 5.1
* Correzione di un bug in cui è stato restituzione di emulatore di archiviazione hello hello `DataServiceVersion` intestazione in alcune risposte in cui non è servizio hello.

### <a name="version-50"></a>Versione 5.0
* installazione dell'emulatore di archiviazione Hello non verifica non è più MSSQL esistente e installa .NET Framework.
* installazione dell'emulatore di archiviazione Hello non crea più database hello come parte dell'installazione. Se necessario, il database verrà comunque creato come parte del processo di avvio.
* Per la creazione del database non è più necessaria l'elevazione dei privilegi.
* Per l'avvio non sono più necessarie prenotazioni di porte.
* Aggiunge le opzioni seguenti troppo hello`init`: `-reserveports` (richiede l'elevazione dei privilegi), `-unreserveports` (richiede l'elevazione dei privilegi), `-skipcreate`.
* opzione dell'interfaccia utente emulatore di archiviazione sull'icona dell'area di notifica sistema hello ora Hello avvia hello interfaccia della riga di comando. GUI di Hello precedente non è più disponibile.
* Alcune DLL sono state rimosse o rinominate.

### <a name="version-46"></a>Versione 4.6
* emulatore di archiviazione Hello supporta ora la versione 2016-05-31 dei servizi di archiviazione hello sugli endpoint di servizio Blob, coda e tabella.

### <a name="version-45"></a>Versione 4.5
* Correzione di un bug che ha causato l'inizializzazione e l'installazione di toofail emulatore di archiviazione hello hello il backup di database è stato rinominato.

### <a name="version-44"></a>Versione 4.4
* emulatore di archiviazione Hello supporta ora la versione 2015-12-11 dei servizi di archiviazione hello sugli endpoint di servizio Blob, coda e tabella.
* Hello garbage collection dell'emulatore di archiviazione dei dati blob è ora più efficiente quando si lavora con un numero elevato di BLOB.
* Correzione di un bug che ha causato toobe ACL XML convalidato in modo leggermente diverso dal servizio di archiviazione hello qual è il contenitore.
* Correzione di un bug che causa talvolta max e min DateTime valori toobe riportato nel fuso orario non corretto di hello.

### <a name="version-43"></a>Versione 4.3
* emulatore di archiviazione Hello supporta ora la versione 2015-07-08 dei servizi di archiviazione hello sugli endpoint di servizio Blob, coda e tabella.

### <a name="version-42"></a>Versione 4.2
* emulatore di archiviazione Hello supporta ora la versione 2015-04-05 di servizi di archiviazione hello sugli endpoint di servizio Blob, coda e tabella.

### <a name="version-41"></a>Versione 4.1
* emulatore di archiviazione Hello supporta ora la versione 2015-02-21 dei servizi di archiviazione hello sugli endpoint di servizio Blob, coda e tabella, ad eccezione delle nuove funzionalità di Accodamento Blob hello.
* Se si utilizza una versione di servizi di archiviazione hello che non è ancora supportata dall'emulatore hello, emulatore hello restituisce un messaggio di errore significativo. È consigliabile utilizzare una versione più recente di hello dell'emulatore hello. Se si verifica un errore di VersionNotSupportedByEmulator (codice di stato HTTP 400 - richiesta non valida), scaricare l'ultima versione di hello dell'emulatore di archiviazione hello.
* Correzione di un bug in cui una race condition ha causato tabella entità dati toobe non corretto durante le operazioni di merge simultanei.

### <a name="version-40"></a>Versione 4.0
* emulatore di archiviazione Hello eseguibile è stato rinominato troppo*AzureStorageEmulator.exe*.

### <a name="version-32"></a>Versione 3.2
* emulatore di archiviazione Hello supporta ora versione 2014-02-14 dei servizi di archiviazione hello sugli endpoint di servizio Blob, coda e tabella. Endpoint del servizio file non sono attualmente supportati nell'emulatore di archiviazione hello. Vedere [controllo delle versioni per i servizi di archiviazione Azure hello](/rest/api/storageservices/Versioning-for-the-Azure-Storage-Services) per informazioni dettagliate sulla versione 2014-02-14.

### <a name="version-31"></a>Versione 3.1
* Archiviazione con ridondanza geografica e accesso in lettura (RA-GRS) è ora supportato nell'emulatore di archiviazione hello. Get Blob Service Stats Hello, Get Queue Service Stats e ottenere le API di statistiche di tabella del servizio sono supportate per l'account di hello secondario e restituiscono sempre il valore di hello dell'elemento di risposta di hello LastSyncTime come hello toohello secondo corrente ora sottostante SQL database. Per l'accesso programmatico toohello secondario con l'emulatore di archiviazione hello, usare hello libreria Client di archiviazione per .NET versione 3.2 o successive. Per informazioni, vedere hello Microsoft Azure Storage Client Library per il riferimento di .NET.

### <a name="version-30"></a>Versione 3.0
* non è più disponibile in hello stesso pacchetto come emulatore di calcolo hello Hello emulatore di archiviazione Azure.
* interfaccia utente grafica dell'emulatore di archiviazione Hello è deprecata a favore di un'interfaccia della riga di comando gestibile tramite script. Per informazioni dettagliate sull'interfaccia della riga di comando hello, vedere riferimento allo strumento da riga di comando emulatore di archiviazione. interfaccia grafica Hello continuerà toobe presente nella versione 3.0, ma essere accessibile solo quando viene installato hello emulatore di calcolo facendo clic sull'icona dell'area di notifica sistema hello e selezionando Mostra interfaccia utente emulatore di archiviazione.
* La versione 2013-08-15 dei servizi di archiviazione Azure hello è ora completamente supportata. (In precedenza questa versione era supportata solo dalla versione 2.2.1 dell'emulatore di archiviazione di anteprima.)

## <a name="next-steps"></a>Passaggi successivi

* Valutare l'emulatore di archiviazione multipiattaforma mantenuto community open source hello [Azurite](https://github.com/arafato/azurite). 
* [Esempi di archiviazione di Azure usando .NET](../storage-samples-dotnet.md) contiene esempi di codice tooseveral collegamenti è possibile utilizzare quando si sviluppa l'applicazione.
* È possibile utilizzare hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) toowork con risorse in cloud di account di archiviazione e nell'emulatore di archiviazione hello.

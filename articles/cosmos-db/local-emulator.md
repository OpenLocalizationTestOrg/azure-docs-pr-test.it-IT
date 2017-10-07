---
title: aaaDevelop localmente con hello Azure Cosmos DB emulatore | Documenti Microsoft
description: "Utilizza hello Azure Cosmos DB emulatore, è possibile sviluppare e testare l'applicazione in locale per gratuito, senza creare una sottoscrizione di Azure."
services: cosmos-db
documentationcenter: 
keywords: Emulatore di Azure Cosmos DB
author: arramac
manager: jhubbard
editor: 
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: arramac
ms.openlocfilehash: fb5449489e5f71664e72d8e11e583315be371bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a>Utilizzare hello Azure Cosmos DB emulatore per sviluppo locale e il test

<table>
<tr>
  <td><strong>File binari</strong></td>
  <td>[Scarica MSI](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><strong>Docker</strong></td>
  <td>[Hub docker](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><strong>Origine docker</strong></td>
  <td>[Github](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
Hello Azure Cosmos DB emulatore offre un ambiente locale che emula hello Azure Cosmos DB servizio a scopo di sviluppo. Utilizza hello Azure Cosmos DB emulatore, è possibile sviluppare e testare l'applicazione localmente, senza creare una sottoscrizione di Azure o eventuali costi. Quando si è soddisfatti delle modalità di funzionamento dell'applicazione nell'emulatore di Azure Cosmos DB hello, è possibile passare un account Azure Cosmos DB nel cloud hello toousing.

Questo articolo descrive hello seguenti attività: 

> [!div class="checklist"]
> * L'installazione dell'emulatore hello
> * Esecuzione hello emulatore in Docker per Windows
> * Autenticazione delle richieste
> * Utilizzando Esplora dati Ciao hello emulatore
> * Esportazione di certificati SSL
> * La chiamata di hello emulatore dalla riga di comando hello
> * Raccolta dei file di traccia

Si consiglia di iniziare, è possibile guardare hello seguente video, in cui Kirill Gavrylyuk viene illustrata la modalità di avvio tooget con hello Azure Cosmos DB emulatore. Si noti che video hello fa riferimento toohello emulatore come hello DocumentDB emulatore, ma è stato rinominato hello dello strumento hello Azure Cosmos DB emulatore dal toccare video hello. Tutte le informazioni hello video siano ancora corrette per hello Azure Cosmos DB emulatore. 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a>Funzionamento di hello emulatore
Hello Azure Cosmos DB emulatore fornisce un'emulazione ad alta fedeltà del servizio Azure Cosmos DB hello. Supporta le stesse funzionalità di Azure Cosmos DB, incluso il supporto per la creazione e l'esecuzione di query su documenti JSON, il provisioning e la scalabilità delle raccolte e l'esecuzione di stored procedure e trigger. È possibile sviluppare e testare applicazioni utilizzando l'emulatore di Azure Cosmos DB hello e distribuirli tooAzure su scala globale apportando solo una singola configurazione modificare toohello endpoint della connessione per il database di Azure Cosmos.

Quando abbiamo creato un'emulazione locale ad alta fedeltà del servizio Azure Cosmos DB effettivo hello, l'implementazione di hello di hello Azure Cosmos DB emulatore è diverso da quello del servizio hello. Ad esempio, hello Azure Cosmos DB emulatore utilizza i componenti del sistema operativo standard, ad esempio hello file system locale per la persistenza e stack del protocollo HTTPS per la connettività. Ciò significa che alcune funzionalità che si basa sull'infrastruttura di Azure come globale, la latenza di millisecondo cifra di letture/scritture, i livelli di coerenza e non sono disponibili tramite hello Azure Cosmos DB emulatore.

> [!NOTE]
> In questo Ciao ora Esplora dati hello emulatore supporta solo la creazione di hello di API DocumentDB raccolte e raccolte di MongoDB. Hello Esplora dati nell'emulatore hello non supporta attualmente la creazione di hello di tabelle e grafici. 

## <a name="system-requirements"></a>Requisiti di sistema
Hello Azure Cosmos DB emulatore ha hello requisiti hardware e software seguenti:

* Requisiti software
  * Windows Server 2012 R2, Windows Server 2016 o Windows Server 10
*   Requisiti hardware minimi
  * 2 GB di RAM
  * 10 GB di spazio su disco disponibile

## <a name="installation"></a>Installazione
È possibile scaricare e installare l'emulatore di Azure Cosmos DB hello da hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator). 

> [!NOTE]
> tooinstall, configurare ed eseguire hello Azure Cosmos DB emulatore, è necessario disporre dei privilegi amministrativi nel computer di hello.

## <a name="running-on-docker-for-windows"></a>Esecuzione in Docker per Windows

Hello Azure Cosmos DB emulatore può essere eseguito in Docker per Windows. Hello emulatore non funzionano in Docker per Oracle Linux.

Dopo aver [Docker per Windows](https://www.docker.com/docker-windows) installato, è possibile effettuare il pull immagine dell'emulatore hello dall'Hub Docker eseguendo hello comando seguente dalla shell preferite (cmd.exe, PowerShell, ecc.).

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
immagine di hello toostart, eseguire hello i comandi seguenti.

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

risposta Hello è simile toohello seguenti:

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import hello SSL certificate from an administrator command prompt on hello host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

Chiudere la shell interattiva hello quando hello è stato avviato l'emulatore verrà contenitore dell'emulatore di arresto hello.

Utilizzare endpoint hello e la chiave master dalla risposta hello nel client e importare il certificato SSL hello nell'host. hello hello tooimport certificato SSL, seguito da un prompt dei comandi di amministratore:

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a>Avviare l'emulatore hello

toostart hello Azure Cosmos DB emulatore, selezionare il pulsante di avvio di hello o premere tasto Windows hello. Iniziare a digitare **Azure Cosmos DB emulatore**e l'emulatore hello selezionare dall'elenco di hello delle applicazioni. 

![Selezionare hello o preme hello Windows chiave di avvio, iniziare a digitare * * Azure Cosmos DB emulatore * * ed emulatore hello selezionare dall'elenco di hello delle applicazioni](./media/local-emulator/database-local-emulator-start.png)

Quando l'emulatore di hello è in esecuzione, si noterà un'icona nell'area di notifica della barra delle applicazioni di Windows hello. ![Notifica della barra delle applicazioni dell'emulatore locale di Azure Cosmos DB](./media/local-emulator/database-local-emulator-taskbar.png)

Hello Azure Cosmos DB emulatore per impostazione predefinita viene eseguito nel computer locale a hello ("localhost") in ascolto sulla porta 8081.

Hello Cosmos DB emulatore Azure è installato per impostazione predefinita toohello `C:\Program Files\Azure Cosmos DB Emulator` directory. È possibile anche avviare e arrestare l'emulatore hello dalla riga di comando hello. Per altre informazioni, vedere le [informazioni di riferimento sullo strumento da riga di comando](#command-line).

## <a name="start-data-explorer"></a>Avviare Esplora dati

Avvio dell'emulatore di Azure Cosmos DB hello hello Azure Cosmos DB Data Explorer verrà automaticamente aperta nel browser. indirizzo Hello verrà visualizzato come [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html). Se si chiudere hello explorer e si desidera toore aperta è in un secondo momento, è possibile aprire hello URL nel browser o avviarlo da hello Azure Cosmos DB emulatore nell'icona di Windows hello, come illustrato di seguito.

![Utilità di avvio di Esplora dati dell'emulatore locale di Azure Cosmos DB](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a>Preparazione per gli aggiornamenti
Esplora dati indica se è disponibile un nuovo aggiornamento per il download. 

> [!NOTE]
> Dati creati in una versione di hello Azure Cosmos DB emulatore non sono garantiti toobe accessibili quando si utilizza una versione diversa. Se è necessario toopersist i dati a lungo termine hello, è consigliabile archiviare i dati in un account Azure Cosmos DB anziché nell'emulatore di Azure Cosmos DB hello. 

## <a name="authenticating-requests"></a>Autenticazione delle richieste
Proprio come con DB Cosmos Azure nel cloud hello, tutte le richieste effettuate su hello Azure Cosmos DB emulatore devono essere autenticata. Hello Azure Cosmos DB emulatore supporta un singolo account fisso e una chiave di autenticazione noto per l'autenticazione chiave master. Questo account e questa chiave sono hello uniche credenziali consentite per l'utilizzo con hello Azure Cosmos DB emulatore. Sono:

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> chiave master di Hello supportati da hello Azure Cosmos DB emulatore deve essere utilizzato solo con l'emulatore hello. È possibile utilizzare l'account di Azure Cosmos DB produzione e la chiave con hello Azure Cosmos DB emulatore. 

> [!NOTE] 
> Se è stato avviato l'emulatore hello con opzione /Key hello, quindi utilizzare il tasto di hello generato invece di "C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw = ="

Inoltre, esattamente come hello Azure Cosmos DB servizio hello Azure Cosmos DB emulatore supporta solo le comunicazioni protette tramite SSL.

## <a name="running-hello-emulator-on-a-local-network"></a>Emulatore hello in esecuzione in una rete locale

È possibile eseguire l'emulatore hello in una rete locale. tooenable l'accesso alla rete, specificare l'opzione /AllowNetworkAccess hello hello [riga di comando](#command-line-syntax), che richiede di specificare /Key = key_string o /KeyFile = nome_file. È possibile utilizzare /GenKeyFile = nome_file toogenerate un file con una chiave casuale sin dall'inizio.  Non è possibile passare tale troppo/KeyFile = nome_file o /Key = contents_of_file.

accesso alla rete tooenable per hello hello utente devono arresta emulatore hello ed Elimina directory dei dati dell'emulatore hello (C:\Users\user_name\AppData\Local\CosmosDBEmulator).

## <a name="developing-with-hello-emulator"></a>Lo sviluppo con hello emulatore
Una volta che si sono hello Azure Cosmos DB dell'emulatore in esecuzione sul desktop, è possibile utilizzare qualsiasi tipo supportato [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) o hello [API REST di Azure Cosmos DB](/rest/api/documentdb/) toointeract con hello emulatore. Hello Azure Cosmos DB emulatore include anche una finestra di esplorazione dati incorporato che consente di creare raccolte per DocumentDB hello e MongoDB APIs e visualizzare e modificare i documenti senza scrivere alcun codice.   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

Se si utilizza [Azure Cosmos DB supporto del protocollo per MongoDB](mongodb-introduction.md), utilizzare hello seguente stringa di connessione:

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

È possibile utilizzare strumenti esistenti come [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB emulatore. È inoltre possibile migrare i dati tra hello Azure Cosmos DB emulatore e il servizio di Azure Cosmos DB hello utilizzando hello [utilità di migrazione di dati di Azure Cosmos DB](https://github.com/azure/azure-documentdb-datamigrationtool).

> [!NOTE] 
> Se è stato avviato l'emulatore hello con opzione /Key hello, quindi utilizzare il tasto di hello generato invece di "C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw = ="

Utilizzando l'emulatore di Azure Cosmos DB hello, per impostazione predefinita, è possibile creare raccolte con partizione singola too25 o raccolta partizionata 1. Per ulteriori informazioni sulla modifica di questo valore, vedere [impostazione hello PartitionCount valore](#set-partitioncount).

## <a name="export-hello-ssl-certificate"></a>Esportare il certificato SSL di hello

Linguaggi .NET e runtime utilizzare hello archivio certificati Windows toosecurely connettersi toohello emulatore locale di Azure Cosmos DB. Gli altri linguaggi hanno il proprio metodo di gestione e uso dei certificati. Java usa il proprio [archivio certificati](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html), mentre Python usa i [wrapper per i socket](https://docs.python.org/2/library/ssl.html).

In ordine tooobtain toouse un certificato con linguaggi e Runtime che non si integrano con l'archivio certificati Windows hello è necessario tooexport utilizzando Gestione certificati di Windows hello. È possibile avviarlo eseguendo certlm.msc o seguire le istruzioni dettagliate hello in [esportare i certificati dell'emulatore di hello Azure Cosmos DB](./local-emulator-export-ssl-certificates.md). Quando il gestore di certificati hello è in esecuzione, aprire hello dei certificati personali come illustrato di seguito e l'esportazione hello certificato con il nome descrittivo di hello "DocumentDBEmulatorCertificate" come file x. 509 (. cer) con codifica BASE 64.

![Certificato SSL dell'emulatore locale di Azure Cosmos DB](./media/local-emulator/database-local-emulator-ssl_certificate.png)

certificato x. 509 Hello può essere importato nell'archivio di certificati di Java hello seguendo le istruzioni hello [aggiunta di un certificato toohello archivio certificati Autorità di certificazione Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store). Una volta hello certificato viene importato nell'archivio certificati hello, le applicazioni Java e MongoDB saranno in grado di tooconnect toohello Azure Cosmos DB emulatore.

Durante la connessione dell'emulatore toohello da Python e Node.js SDK, verifica SSL è disabilitata.

## <a id="command-line"></a>Riferimenti allo strumento da riga di comando
Dal percorso di installazione di hello, si può utilizzare toostart della riga di comando hello e arresta emulatore hello, configurare le opzioni ed eseguire altre operazioni.

### <a name="command-line-syntax"></a>Sintassi della riga di comando

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

elenco di hello tooview di opzioni, digitare `CosmosDB.Emulator.exe /?` al prompt dei comandi di hello.

<table>
<tr>
  <td><strong>Opzione</strong></td>
  <td><strong>Descrizione</strong></td>
  <td><strong>Comando</strong></td>
  <td><strong>Argomenti</strong></td>
</tr>
<tr>
  <td>[Nessun argomento]</td>
  <td>Avvio hello Azure Cosmos DB emulatore con le impostazioni predefinite.</td>
  <td>CosmosDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>[Help]</td>
  <td>Visualizza l'elenco di hello supportati gli argomenti della riga di comando.</td>
  <td>CosmosDB.Emulator.exe /?</td>
  <td></td>
</tr>
<tr>
  <td>Shutdown</td>
  <td>Arresta l'emulatore di Azure Cosmos DB hello.</td>
  <td>CosmosDB.Emulator.exe /Shutdown</td>
  <td></td>
</tr>
<tr>
  <td>DataPath</td>
  <td>Specifica il percorso di hello nei file di dati quali toostore. Il valore predefinito è %LocalAppdata%\CosmosDBEmulator.</td>
  <td>CosmosDB.Emulator.exe /DataPath=&lt;percorsodati&gt;</td>
  <td>&lt;percorsodati&gt;: percorso accessibile</td>
</tr>
<tr>
  <td>Porta</td>
  <td>Specifica toouse numero di porta hello per emulatore hello.  Il valore predefinito è 8081.</td>
  <td>CosmosDB.Emulator.exe /Port=&lt;porta&gt;</td>
  <td>&lt;porta&gt;: numero di porta singolo</td>
</tr>
<tr>
  <td>MongoPort</td>
  <td>Specifica hello toouse numero di porta per la compatibilità di MongoDB API. Il valore predefinito è 10255.</td>
  <td>CosmosDB.Emulator.exe /MongoPort=&lt;portaMongo&gt;</td>
  <td>&lt;portaMongo&gt;: numero di porta singolo</td>
</tr>
<tr>
  <td>DirectPorts</td>
  <td>Specifica hello toouse di porte per la connessione diretta. I valori predefiniti sono 10251, 10252, 10253 e 10254.</td>
  <td>CosmosDB.Emulator.exe /DirectPorts:&lt;portedirette&gt;</td>
  <td>&lt;portedirette&gt;: elenco delimitato da virgole di 4 porte.</td>
</tr>
<tr>
  <td>Chiave</td>
  <td>Chiave di autorizzazione per l'emulatore hello. La chiave deve essere hello codifica base 64 di un vettore di 64 byte.</td>
  <td>CosmosDB.Emulator.exe /Key:&lt;chiave&gt;</td>
  <td>&lt;chiave&gt;: chiave deve essere hello codifica base 64 di un vettore di 64 byte</td>
</tr>
<tr>
  <td>EnableRateLimiting</td>
  <td>Specifica che il comportamento di limitazione della frequenza è abilitato.</td>
  <td>CosmosDB.Emulator.exe /EnableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>DisableRateLimiting</td>
  <td>Specifica che il comportamento di limitazione della frequenza è disabilitato.</td>
  <td>CosmosDB.Emulator.exe /DisableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>NoUI</td>
  <td>Non visualizzare emulatore hello interfaccia utente.</td>
  <td>CosmosDB.Emulator.exe /NoUI</td>
  <td></td>
</tr>
<tr>
  <td>NoExplorer</td>
  <td>Non mostra Esplora documenti all'avvio.</td>
  <td>CosmosDB.Emulator.exe /NoExplorer</td>
  <td></td>
</tr>
<tr>
  <td>PartitionCount</td>
  <td>Specifica hello il numero massimo di raccolte partizionate. Vedere [modificare hello numero di raccolte](#set-partitioncount) per ulteriori informazioni.</td>
  <td>CosmosDB.Emulator.exe /PartitionCount=&lt;conteggiopartizioni&gt;</td>
  <td>&lt;partitioncount&gt;: numero massimo di raccolte con partizione singola consentite. Il valore predefinito è 25. Il valore massimo consentito è 250.</td>
</tr>
<tr>
  <td>DefaultPartitionCount</td>
  <td>Specifica il numero predefinito di hello di partizioni per una raccolta partizionata.</td>
  <td>CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;numeropredefinitopartizioni&gt;</td>
  <td>&lt;numeropredefinitopartizioni&gt; Il valore predefinito è 25.</td>
</tr>
<tr>
  <td>AllowNetworkAccess</td>
  <td>Abilita accesso emulatore toohello in rete. È necessario passare anche /Key =&lt;key_string&gt; /KeyFile o =&lt;file_name&gt; tooenable accesso alla rete.</td>
  <td>CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;stringa_chiave&gt;<br><br>oppure<br><br>CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;nome_file&gt;</td>
  <td></td>
</tr>
<tr>
  <td>NoFirewall</td>
  <td>Non modificare le regole del firewall quando si usa /AllowNetworkAccess.</td>
  <td>CosmosDB.Emulator.exe /NoFirewall</td>
  <td></td>
</tr>
<tr>
  <td>GenKeyFile</td>
  <td>Generare una nuova chiave di autorizzazione e salvare toohello file specificato. chiave Hello generato può essere utilizzato con hello /Key o /KeyFile opzioni.</td>
  <td>CosmosDB.Emulator.exe /GenKeyFile =&lt;tookey percorso file&gt;</td>
  <td></td>
</tr>
<tr>
  <td>Coerenza</td>
  <td>Impostare livello di coerenza hello predefinito per l'account di hello.</td>
  <td>CosmosDB.Emulator.exe /Consistency=&lt;coerenza&gt;</td>
  <td>&lt;coerenza&gt;: valore deve essere uno dei seguenti hello [livelli di coerenza](consistency-levels.md): BoundedStaleness, sicuro, eventuale o sessione.  valore predefinito di Hello è sessione.</td>
</tr>
<tr>
  <td>?</td>
  <td>Mostra messaggio hello.</td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a>Differenze tra hello Azure Cosmos DB emulatore e Azure Cosmos DB 
Poiché hello Azure Cosmos DB emulatore fornisce un ambiente di emulato in esecuzione in una workstation di sviluppo locale, esistono alcune differenze nelle funzionalità tra emulatore hello e un account Azure Cosmos DB nel cloud hello:

* Hello Azure Cosmos DB emulatore supporta solo un singolo account fisso e una chiave master del nota.  Rigenerazione della chiave non è possibile in hello Azure Cosmos DB emulatore.
* Hello Azure Cosmos DB emulatore non è un servizio scalabile e non supporta un numero elevato di raccolte.
* Hello Azure Cosmos DB emulatore non simula diverse [livelli di coerenza Azure Cosmos DB](consistency-levels.md).
* Hello Azure Cosmos DB emulatore non viene simulata [multiarea replica](distribute-data-globally.md).
* Hello Azure Cosmos DB emulatore non supporta l'override di quota hello servizio che sono disponibili nel servizio di Azure Cosmos DB hello (ad esempio i limiti di dimensioni di documento, archiviazione della raccolta partizionata maggiore).
* Come la copia di hello Azure Cosmos DB emulatore potrebbe non essere backup toodate con le modifiche più recenti di hello con il servizio di Azure Cosmos DB hello, eseguire [pianificazione della capacità di Azure Cosmos DB](https://www.documentdb.com/capacityplanner) velocità effettiva di produzione stima di tooaccurately (RUs) requisiti dell'applicazione.

## <a id="set-partitioncount"></a>Modificare il numero di hello di raccolte

Per impostazione predefinita, è possibile creare raccolte con partizione singola too25 o 1 raccolta partizionata utilizzando hello Azure Cosmos DB emulatore. Modificando hello **PartitionCount** valore, è possibile creare raccolte con partizione singola too250 o le raccolte partizionate 10 o qualsiasi combinazione di due che non superano 250 singolo hello partizioni (in cui 1 partizionata raccolta = raccolta singola partizione 25).

Se si tenta di toocreate una raccolta dopo che è stato superato il numero di partizione corrente hello, emulatore hello genera un'eccezione ServiceUnavailable, con successivo messaggio hello.

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

numero di hello toochange di raccolte disponibili toohello Azure Cosmos DB emulatore, hello seguenti:

1. Eliminare tutti i dati di Azure Cosmos DB emulatore locali facendo clic su hello **emulatore di Azure Cosmos DB** icona sulla barra delle applicazioni hello, quindi fare clic su **Reimposta dati...** .
2. Eliminare tutti i dati dell'emulatore dalla cartella C:\Users\user_name\AppData\Local\CosmosDBEmulator.
3. Chiudere tutte le istanze aperte facendo clic su hello **emulatore di Azure Cosmos DB** icona sulla barra delle applicazioni hello, quindi fare clic su **uscita**. Potrebbe richiedere un minuto per tutte le istanze tooexit.
4. Installare una versione più recente di hello di hello [emulatore di Azure Cosmos DB](https://aka.ms/cosmosdb-emulator).
5. Avvia emulatore di hello con flag PartitionCount hello impostando un valore < = 250. Ad esempio: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.

## <a name="troubleshooting"></a>Risoluzione dei problemi

Utilizzare hello toohelp di risolvere i problemi riscontrati con l'emulatore di Azure Cosmos DB hello suggerimenti seguenti:

- Se è installata una nuova versione di hello emulatore e segnalano errori, assicurarsi che ripristinare i dati. È possibile ripristinare i dati facendo clic sull'icona di Azure Cosmos DB emulatore hello sulla barra delle applicazioni hello, e quindi fare clic su Reimposta dati... Se non viene risolto errori hello, è possibile disinstallare e reinstallare l'applicazione hello. Vedere [disinstallare emulatore locale hello](#uninstall) per le istruzioni.

- Se si blocca l'emulatore di Azure Cosmos DB hello, raccogliere i file di dump dalla cartella c:\Users\user_name\AppData\Local\CrashDumps comprimerli e collegarli tramite posta elettronica tooan troppo[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

- Se si verificano arresti anomali del sistema in CosmosDB.StartupEntryPoint.exe, eseguire hello comando seguente da un prompt dei comandi di amministratore:`lodctr /R` 

- Se si verifica un problema di connettività, [raccogliere i file di traccia](#trace-files)comprimerli e collegarli tramite posta elettronica tooan troppo[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

- Se si riceve un **servizio non disponibile** dei messaggi, hello emulatore potrebbe essersi verificato un errore dello stack di rete hello tooinitialize. Toosee di controllo se si dispone di hello Pulse secure Juniper reti client o installati, come i driver di filtro rete potrebbero causare il problema di hello. La disinstallazione di driver di filtro di rete di terze parti in genere consente di correggere il problema di hello.

### <a id="trace-files"></a>Raccogliere i file di traccia

toocollect debug tracce, eseguire hello dopo i comandi da un prompt dei comandi amministrativo:

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. `CosmosDB.Emulator.exe /shutdown`. Espressioni di controllo hello sistema toomake che hello programma è arrestato, potrebbe richiedere un minuto. È anche possibile fare clic **uscita** nell'interfaccia utente dell'emulatore di Azure Cosmos DB hello.
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. Riprodurre il problema di hello. Se Esplora dati non funziona, è necessario solo toowait per hello browser tooopen per pochi secondi toocatch hello correggere l'errore.
5. `CosmosDB.Emulator.exe /stoptraces`
6. Passare troppo`%ProgramFiles%\Azure Cosmos DB Emulator` e trovare il file docdbemulator_000001.etl hello.
7. Inviare file con estensione etl hello insieme ai passaggi ripetizione bug troppo[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) per il debug.

### <a id="uninstall"></a>Disinstallare hello emulatore locale

1. Chiudere tutte le istanze aperte di hello emulatore locale facendo clic sull'icona di Azure Cosmos DB emulatore hello sulla barra delle applicazioni hello, e quindi fare clic su Esci. Potrebbe richiedere un minuto per tutte le istanze tooexit.
2. Nella casella di ricerca di Windows hello, digitare **App e funzionalità** e fare clic su hello **App e funzionalità (impostazioni di sistema)** risultato.
3. Nell'elenco di App hello scorrere troppo**emulatore di Azure Cosmos DB**, selezionarla, fare clic su **Disinstalla**, confermare, quindi fare clic su **Disinstalla** nuovamente.
4. Quando viene disinstallata l'applicazione hello, passare tooC:\Users\<utente > cartella hello \AppData\Local\CosmosDBEmulator e delete. 

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, effettuata seguente hello:

> [!div class="checklist"]
> * Installato hello emulatore locale
> * Rand hello emulatore in Docker per Windows
> * Autenticazione delle richieste
> * Ciao Esplora dati hello emulatore utilizzato
> * Esportazione dei certificati SSL
> * Chiamata hello emulatore dalla riga di comando hello
> * Raccolta dei file di traccia

In questa esercitazione, si è appreso come toouse hello emulatore locale di sviluppo locale disponibile. È possibile continuare l'esercitazione successiva toohello e informazioni su come i certificati SSL emulatore tooexport. 

> [!div class="nextstepaction"]
> [Esportare i certificati di Azure Cosmos DB emulatore hello](local-emulator-export-ssl-certificates.md)

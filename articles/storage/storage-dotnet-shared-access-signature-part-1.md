---
title: aaaUsing condiviso (SAS) firme di accesso in archiviazione di Azure | Documenti Microsoft
description: Informazioni condivise toouse accesso firme (SAS) toodelegate accesso tooAzure risorse di archiviazione, inclusi BLOB, code, tabelle e file.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 46fd99d7-36b3-4283-81e3-f214b29f1152
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/18/2017
ms.author: marsma
ms.openlocfilehash: 53e06c78fbfdaa5fd209add719995ef2a6bc8f61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-shared-access-signatures-sas"></a>Uso delle firme di accesso condiviso

Una firma di accesso condiviso (SAS) fornisce un tooobjects di accesso limitato toogrant modo nell'account di archiviazione tooother client, senza esporre la chiave dell'account. In questo articolo è fornire una panoramica del modello di firma di accesso condiviso hello, le procedure consigliate di firma di accesso condiviso ed esaminare alcuni esempi.

Per ulteriori esempi di codice l'utilizzo di SAS rispetto a quelle fornite in questa sezione, vedere [Introduzione all'archiviazione Blob di Azure in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) e altri esempi disponibili in hello [esempi di codice di Azure](https://azure.microsoft.com/documentation/samples/?service=storage) libreria. È possibile scaricare le applicazioni di esempio hello ed eseguirli o esaminare il codice hello su GitHub.

## <a name="what-is-a-shared-access-signature"></a>Informazioni sulle firme di accesso condiviso
Firma di accesso condiviso fornisce l'accesso delegato tooresources nell'account di archiviazione. Una firma di accesso condiviso, è possibile concedere ai client accedono tooresources nell'account di archiviazione, senza condividere le chiavi dell'account. Si tratta di hello punto chiave di utilizzo di firme di accesso condiviso nelle applicazioni, una firma di accesso condiviso è un tooshare in modo sicuro le risorse di archiviazione senza compromettere le chiavi dell'account.

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

Una firma di accesso condiviso consente un controllo granulare tipo hello di accesso che è concedere tooclients che dispongono di hello SAS, tra cui:

* intervallo di Hello in cui hello è valido, inclusi l'ora di inizio hello e l'ora di scadenza hello SAS.
* autorizzazioni Hello concesse da hello SAS. Ad esempio, una firma di accesso condiviso per un blob potrebbe concedono autorizzazioni di lettura e blob toothat le autorizzazioni di scrittura, ma non eliminare le autorizzazioni.
* Un indirizzo IP facoltativo o intervallo di indirizzi IP dai quali archiviazione di Azure accetta hello SAS. Ad esempio, specificare un intervallo di indirizzi IP appartenenti tooyour organizzazione.
* protocollo Hello su cui l'archiviazione di Azure accetterà hello SAS. È possibile utilizzare questo tooclients accesso toorestrict di parametro facoltativo tramite HTTPS.

## <a name="when-should-you-use-a-shared-access-signature"></a>Perché usare una firma di accesso condiviso
Quando si desidera tooprovide accesso tooresources nel client di tooany account di archiviazione che non presenta le chiavi di accesso dell'account di archiviazione, è possibile utilizzare una firma di accesso condiviso. L'account di archiviazione include sia una chiave di accesso primaria e secondaria, di concedere l'account di accesso amministrativo tooyour e tutte le risorse in esso contenuti. Esposizione di uno di questi tasti apre il possibilità toohello account d'uso dannoso o non appropriata. Le firme di accesso condiviso forniscono un metodo alternativo che consente ai client tooread, scrittura ed eliminare i dati nell'account di archiviazione in base toohello autorizzazioni che sono state concesse in modo esplicito e senza necessità di una chiave dell'account.

Uno scenario comune è utile in una firma di accesso condiviso è un servizio in cui gli utenti di leggere e scrivere il proprio account di archiviazione di dati tooyour. Uno scenario in cui i dati utente vengono archiviati nell'account di archiviazione è caratterizzato da due modelli di progettazione standard:

1. I client caricano e scaricano dati tramite un servizio proxy front-end che esegue l'autenticazione. Il servizio proxy front-end offre il vantaggio di hello di convalida delle regole di business, ma per grandi quantità di dati o transazioni con volumi elevati, creazione di un servizio che possono essere ridimensionati toomatch richiesta può essere costoso o difficile.

  ![Diagramma dello scenario: il servizio proxy front-end][sas-storage-fe-proxy-service]

1. Un semplice servizio autentica il client di hello in base alle esigenze e quindi genera una firma di accesso condiviso. Una volta client hello riceve hello SAS, risorse dell'account di archiviazione possono accedere direttamente con le autorizzazioni di hello definite dalle hello SAS e per l'intervallo di hello consentito da hello SAS. Hello SAS riduce hello necessario per il routing di tutti i dati tramite il servizio front-end proxy hello.

  ![Diagramma dello scenario: servizio provider di firma di accesso condiviso][sas-storage-provider-service]

Molti servizi reali possono usare una combinazione di questi due approcci. Ad esempio, potrebbe essere elaborati alcuni dati e convalidati tramite proxy front-end hello, mentre altri dati vengano salvati e/o leggere direttamente tramite firma di accesso condiviso.

Inoltre, sarà necessario toouse un oggetto di origine SAS tooauthenticate hello in un'operazione di copia in determinati scenari:

* Quando si copia un blob tooanother blob che risiede in un altro account di archiviazione, è necessario utilizzare un blob di origine hello tooauthenticate SAS. Facoltativamente, è possibile utilizzare un firma di accesso condiviso tooauthenticate hello blob di destinazione nonché.
* Quando si copia un file tooanother file che si trova in un altro account di archiviazione, è necessario utilizzare un file di origine hello tooauthenticate SAS. Facoltativamente, è possibile utilizzare un firma di accesso condiviso tooauthenticate hello destinazione file.
* Quando si copia un file di blob tooa o un blob tooa file, è necessario utilizzare un oggetto origine hello tooauthenticate SAS, anche se gli oggetti di origine e destinazione hello risiedono hello stesso account di archiviazione.

## <a name="types-of-shared-access-signatures"></a>Tipi di firme di accesso condiviso
È possibile creare due tipi di firme di accesso condiviso:

* **Firma di accesso condiviso del servizio.** accedono a delegati SAS del servizio Hello risorsa tooa solo uno dei servizi di archiviazione hello: hello servizio Blob, coda, tabella o File. Vedere [la costruzione di una firma di accesso condiviso servizio](https://msdn.microsoft.com/library/dn140255.aspx) e [servizio SAS esempi](https://msdn.microsoft.com/library/dn140256.aspx) per informazioni dettagliate sulla creazione di token di firma di accesso condiviso servizio hello.
* **Firma di accesso condiviso dell'account.** delegati di firma di accesso condiviso di Hello account di accesso tooresources in uno o più dei servizi di archiviazione hello. Operazioni di hello disponibili mediante il servizio di firma di accesso condiviso sono anche disponibili tramite un account di firma di accesso condiviso. Inoltre, con account hello firma di accesso condiviso, è possibile delegare toooperations di accesso che si applicano tooa determinato servizio, ad esempio **Get/Set proprietà del servizio** e **ottenere statistiche del servizio**. È inoltre possibile delegare accesso tooread, scrittura e le operazioni di eliminazione in contenitori blob, tabelle, code e le condivisioni di file che non sono consentite con un firma di accesso condiviso del servizio. Vedere [la costruzione di una firma di accesso condiviso](https://msdn.microsoft.com/library/mt584140.aspx) per informazioni dettagliate sulla creazione di token di firma di accesso condiviso di hello account.

## <a name="how-a-shared-access-signature-works"></a>Funzionamento della firma di accesso condiviso
Firma di accesso condiviso è un URI con segno che punta tooone o altre risorse di archiviazione e include un token che contiene un set di parametri di query speciale. token Hello indica come risorse hello accessibili da client hello. Uno dei parametri di query hello, hello firma, viene costruito dai parametri SAS hello e firmato con una chiave dell'account hello. Questa firma viene utilizzata da hello tooauthenticate di archiviazione di Azure SAS.

Di seguito è riportato un esempio di un URI SAS, l'URI di risorsa con hello e token SAS hello:

![Componenti di un URI di firma di accesso condiviso][sas-storage-uri]

token SAS Hello è una stringa di generazione in hello *client* lato (vedere hello [esempi SAS](#sas-examples) sezione per esempi di codice). Un token di firma di accesso condiviso che è generare alla libreria client di archiviazione hello, ad esempio, non viene rilevato da archiviazione di Azure in alcun modo. È possibile creare un numero illimitato di token di firma di accesso condiviso sul lato client hello.

Quando un client fornisce un tooAzure URI SAS archiviazione come parte di una richiesta, il servizio hello controlla i parametri SAS hello e tooverify firma è valida per l'autenticazione richiesta hello. Se il servizio di hello verifica che la firma di hello è valida, quindi hello richiesta viene autenticata. In caso contrario, richiesta di hello viene rifiutata con codice di errore 403 (accesso negato).

## <a name="shared-access-signature-parameters"></a>Parametri della firma di accesso condiviso
account Hello SAS token SAS del servizio di includere alcuni parametri comuni e prendere alcuni parametri che sono diversi.

### <a name="parameters-common-tooaccount-sas-and-service-sas-tokens"></a>Parametri comuni tooaccount SAS e i token SAS del servizio
* **Versione dell'API** un parametro facoltativo che specifica hello archiviazione servizio versione toouse tooexecute hello richiesta.
* **Versione del servizio** un parametro obbligatorio che specifica hello archiviazione servizio versione toouse tooauthenticate hello richiesta.
* **Ora di inizio.** Si tratta hello tempo in cui hello firma di accesso condiviso diventa valida. ora di inizio Hello per una firma di accesso condiviso è facoltativo. Se viene omessa un'ora di inizio, hello SAS ha validità immediata. Hello ora di inizio deve essere espressa in formato UTC (Coordinated Universal Time), con un identificatore di formato UTC speciale ("Z"), ad esempio `1994-11-05T13:15:30Z`.
* **Scadenza.** Si tratta hello tempo dopo il quale hello firma di accesso condiviso non è più valido. Secondo le procedure consigliate è preferibile specificare una data di scadenza per una firma di accesso condiviso oppure associarla a criteri di accesso archiviati. Hello ora di scadenza deve essere espressi in formato UTC (Coordinated Universal Time), con un identificatore di formato UTC speciale ("Z"), ad esempio `1994-11-05T13:15:30Z` (vedere più sotto).
* **Autorizzazione.** autorizzazioni di Hello specificate nella firma di accesso condiviso hello indicano le operazioni client hello può eseguire su una risorsa di archiviazione hello utilizzando hello SAS. Le autorizzazioni disponibili per la firma di accesso condiviso dell'account e del servizio sono diverse.
* **IP.** Parametro facoltativo che specifica un indirizzo IP o un intervallo di indirizzi IP all'esterno di Azure (vedere la sezione hello [lo stato di configurazione della sessione di Routing](../expressroute/expressroute-workflows.md#routing-session-configuration-state) per Express Route) da cui richieste tooaccept.
* **Protocol.** Parametro facoltativo che specifica il protocollo di hello consentito per una richiesta. I valori possibili sono HTTP e HTTPS (`https,http`), che è solo il valore di predefinito hello o HTTPS (`https`). Si noti che HTTP only non è un valore consentito.
* **Signature.** firma Hello viene costruita da hello altri parametri specificati come token parte e quindi crittografate. È utilizzato hello tooauthenticate SAS.

### <a name="parameters-for-a-service-sas-token"></a>Parametri per il token della firma di accesso condiviso del servizio
* **Risorsa di archiviazione.** Le risorse di archiviazione per cui è possibile delegare l'accesso con una firma di accesso condiviso del servizio sono:
  * Contenitori e BLOB
  * Condivisioni di file e file
  * Queues
  * Le tabelle e gli intervalli di entità della tabella.

### <a name="parameters-for-an-account-sas-token"></a>Parametri per il token della firma di accesso condiviso dell'account
* **Servizio o servizi.** Un account sa possibile delegare l'accesso tooone o più dei servizi di archiviazione hello. Ad esempio, è possibile creare un account di delegati diritti di accesso del servizio Blob e File toohello SAS. Oppure è possibile creare una firma di accesso condiviso che i delegati accedere tooall quattro servizi (Blob, coda, tabella e File).
* **Tipi di risorse di archiviazione.** Un account sa applica tooone o altre classi di risorse di archiviazione, piuttosto che una risorsa specifica. È possibile creare un account SAS toodelegate accesso:
  * API a livello di servizio, che vengono chiamate su risorsa di account di archiviazione hello. Ad esempio: **Get/Set Service Properties**, **Get Service Stats** e **List Containers/Queues/Tables/Shares**.
  * Le API a livello di contenitore, che vengono chiamate con gli oggetti contenitore hello per ogni servizio: blob contenitori, le code, tabelle e le condivisioni file. Ad esempio: **Create/Delete Container**, **Create/Delete Queue**, **Create/Delete Table**, **Create/Delete Share** e **List Blobs/Files and Directories**.
  * API a livello di oggetto, che vengono chiamate su BLOB, messaggi di coda, entità tabelle e file. Ad esempio: **Put Blob**, **Query Entity**, **Get Messages** e **Create File**.

## <a name="examples-of-sas-uris"></a>Esempi di URI di firma di accesso condiviso

### <a name="service-sas-uri-example"></a>Esempio di URI di firma di accesso condiviso del servizio

Di seguito è riportato un esempio di un servizio URI SAS che fornisce leggere e scrivere i blob tooa autorizzazioni. tabella Hello viene suddivisa in ogni parte di hello URI toounderstand il contributo di toohello SAS:

```
https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2015-04-05&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D
```

| Nome | Parte firma di accesso condiviso | Descrizione |
| --- | --- | --- |
| URI del BLOB |`https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt` |indirizzo Hello del blob hello. Si noti che è vivamente consigliato l'uso di HTTPS. |
| Versione dei servizi di archiviazione |`sv=2015-04-05` |Per i servizi di archiviazione versione 2012-02-12 e versioni successive, questo parametro indica toouse versione hello. |
| Ora di inizio |`st=2015-04-29T22%3A18%3A26Z` |Specificata nell'ora UTC. Se si desidera hello SAS toobe valido immediatamente, omettere l'ora di inizio hello. |
| Scadenza |`se=2015-04-30T02%3A23%3A26Z` |Specificata nell'ora UTC. |
| Risorsa |`sr=b` |risorsa Hello è un blob. |
| Autorizzazioni |`sp=rw` |autorizzazioni Hello concesse da hello SAS includono Read (r) e scrittura (w). |
| Intervallo IP |`sip=168.1.5.60-168.1.5.70` |Hello intervallo di indirizzi IP da cui verrà accettata una richiesta. |
| Protocol |`spr=https` |Sono consentite solo richieste tramite HTTPS. |
| Firma |`sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D` |Utilizzare blob toohello di tooauthenticate accesso. firma di Hello è un HMAC calcolato su una stringa da firmare e una chiave utilizzando l'algoritmo SHA256 hello e quindi codificato con codifica Base64. |

### <a name="account-sas-uri-example"></a>Esempio di URI di firma di accesso condiviso dell'account

Di seguito è riportato un esempio di un account di firma di accesso condiviso che utilizza hello stessi parametri comuni sul token hello. Poiché questi parametri sono già stati illustrati in precedenza, non sono descritti qui. Solo i parametri di hello che sono specifici tooaccount che SAS sono descritti nella tabella hello riportato di seguito.

```
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&srt=s&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B
```

| Nome | Parte firma di accesso condiviso | Descrizione |
| --- | --- | --- |
| URI della risorsa |`https://myaccount.blob.core.windows.net/?restype=service&comp=properties` |Hello endpoint del servizio Blob, con i parametri per ottenere le proprietà del servizio (quando viene chiamato con GET) o impostare le proprietà del servizio (quando viene chiamato con SET). |
| Services |`ss=bf` |si applica Hello SAS toohello Blob e servizi File |
| Tipi di risorse |`srt=s` |Hello SAS si applica a livello di tooservice operazioni. |
| Autorizzazioni |`sp=rw` |le autorizzazioni di Hello concedono accesso tooread e le operazioni di scrittura. |

Dato che le autorizzazioni sono limitate toohello livello di servizio, operazioni accessibili con questa firma di accesso condiviso sono **Get Blob Service Properties** (lettura) e **Set Blob Service Properties** (scrittura). Tuttavia, con un URI di risorsa diverso, hello stesso token di firma di accesso condiviso potrebbe anche essere utilizzato toodelegate accesso troppo**Get Blob Service Stats** (lettura).

## <a name="controlling-a-sas-with-a-stored-access-policy"></a>Controllo di una firma di accesso condiviso con criteri di accesso archiviati
Una firma di accesso condiviso può assumere una delle due forme seguenti:

* **Firma di accesso condiviso ad hoc:** quando si crea una firma di accesso condiviso ad hoc, l'ora di inizio hello, ora di scadenza e le autorizzazioni per hello SAS vengono specificate URI SAS hello (o implicite, in caso di hello in cui ora di inizio è omesso). È possibile creare questa firma di accesso condiviso come firma di accesso condiviso dell'account o del servizio.
* **Firma di accesso condiviso con criteri di accesso archiviati:** criteri di accesso archiviati è definito in un contenitore di risorse, un contenitore blob, tabella, coda o - condivisione file e può essere utilizzato toomanage vincoli per uno o più firme di accesso condiviso. Quando si associa una firma di accesso condiviso con criteri di accesso archiviati, hello SAS eredita i vincoli di hello - ora di inizio hello, ora di scadenza e le autorizzazioni, definite per i criteri di accesso archiviato hello.

> [!NOTE]
> Al momento, una firma di accesso condiviso dell'account deve essere una firma di accesso condiviso ad-hoc. I criteri di accesso archiviati non sono ancora supportati per la firma di accesso condiviso dell'account.

Hello differenza tra hello due forme è importante per uno scenario di chiave: revoche di certificati. Poiché un URI SAS è un URL, qualsiasi utente che consente di ottenere hello firma di accesso condiviso può essere utilizzato, indipendentemente dal fatto che ha originariamente creato. Se una firma di accesso condiviso viene pubblicato, può essere utilizzato da chiunque in HelloWorld. Tooanyone una firma di accesso condiviso concede l'accesso tooresources numericamente, fino a quando non si verifica una delle quattro operazioni:

1. ora di scadenza Hello specificato su hello che SAS viene raggiunto.
2. ora di scadenza Hello specificato nel criterio di accesso archiviato hello hello che viene raggiunto SAS (se viene fatto riferimento a un criterio di accesso archiviato e se si specifica un'ora di scadenza) a cui fa riferimento. Ciò può verificarsi perché l'intervallo di hello o perché è stato modificato i criteri di accesso di hello archiviata con un'ora di scadenza in hello precedente, che sono un modo toorevoke hello SAS.
3. Hello archiviati i criteri di accesso a cui fa riferimento hello che SAS viene eliminato, ovvero hello toorevoke di un altro modo SAS. Si noti che se si ricrea il criterio di accesso archiviato hello con esattamente hello stesso nome, SAS esistente tutti i token vengono nuovamente essere valido in base toohello autorizzazioni associate che Criteri di accesso archiviati (presupponendo che tale ora di scadenza hello nella firma di accesso condiviso non è stato passato hello). Se si sta prendendo in considerazione hello toorevoke SAS, essere toouse che un altro nome se si ricrea il criterio di accesso hello con un'ora di scadenza in hello future.
4. chiave dell'account che è stato utilizzato toocreate hello SAS Hello viene rigenerato. La rigenerazione di una chiave dell'account causerà tutti i componenti dell'applicazione utilizzando tale tooauthenticate toofail chiave fino a quando non verranno aggiornati toouse hello sia altri chiave dell'account appena rigenerata hello o la chiave di account valido.

> [!IMPORTANT]
> Un URI di firma di accesso condiviso è associato con firma di hello toocreate utilizzati chiave account hello e hello associati criteri di accesso archiviati (se presente). Se si specifica alcun criterio di accesso archiviati, hello solo modo toorevoke una firma di accesso condiviso è toochange hello account chiave.

## <a name="authenticating-from-a-client-application-with-a-sas"></a>Autenticazione da un'applicazione client con una firma di accesso condiviso
Un client che è in possesso di una firma di accesso condiviso può utilizzare hello SAS tooauthenticate una richiesta per un account di archiviazione per il quale non dispongono di chiavi dell'account di hello. Una firma di accesso condiviso può essere incluso in una stringa di connessione o utilizzato direttamente dal costruttore appropriato hello o un metodo.

### <a name="using-a-sas-in-a-connection-string"></a>Uso di una firma di accesso condiviso in una stringa di connessione
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

### <a name="using-a-sas-in-a-constructor-or-method"></a>Uso di una firma di accesso condiviso in un costruttore o in un metodo
Molti costruttori libreria client di archiviazione di Azure e overload offrono un parametro di firma di accesso condiviso, in modo che è possibile autenticare un servizio di toohello richiesta con una firma di accesso condiviso.

Ad esempio, un URI SAS Ecco toocreate usato un blob in blocchi tooa riferimento. Hello SAS fornisce hello solo le credenziali necessarie per la richiesta di hello. riferimento di blob Hello blocco viene quindi usato per un'operazione di scrittura:

```csharp
string sasUri = "https://storagesample.blob.core.windows.net/sample-container/" +
    "sampleBlob.txt?sv=2015-07-08&sr=b&sig=39Up9JzHkxhUIhFEjEH9594DJxe7w6cIRCg0V6lCGSo%3D" +
    "&se=2016-10-18T21%3A51%3A37Z&sp=rcw";

CloudBlockBlob blob = new CloudBlockBlob(new Uri(sasUri));

// Create operation: Upload a blob with hello specified name toohello container.
// If hello blob does not exist, it will be created. If it does exist, it will be overwritten.
try
{
    MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    msWrite.Position = 0;
    using (msWrite)
    {
        await blob.UploadFromStreamAsync(msWrite);
    }

    Console.WriteLine("Create operation succeeded for SAS {0}", sasUri);
    Console.WriteLine();
}
catch (StorageException e)
{
    if (e.RequestInformation.HttpStatusCode == 403)
    {
        Console.WriteLine("Create operation failed for SAS {0}", sasUri);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    else
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}

```

## <a name="best-practices-when-using-sas"></a>Procedure consigliate per l'uso di SAS
Quando si usano firme di accesso condiviso nelle applicazioni, è necessario toobe considerare due potenziali rischi:

* In caso di diffusione di una firma di accesso condiviso, chiunque la ottiene può usarla e questo potrebbe compromettere l'account di archiviazione.
* Se una firma di accesso condiviso fornito tooa client applicazione scade e l'applicazione hello è Impossibile tooretrieve una nuova firma di accesso condiviso dal servizio, la funzionalità dell'applicazione hello può essere ostacolata.

salve le indicazioni seguenti per l'utilizzo di firme di accesso condiviso consente di ridurre tali rischi:

1. **Utilizzare sempre HTTPS** toocreate o la distribuzione di una firma di accesso condiviso. Se una firma di accesso condiviso viene passato tramite HTTP e intercettato, un attacco di un attacco man-in-the-middle è in grado di tooread hello SAS e utilizzarlo come hello destinato potrebbe essere utente, potrebbe compromettere i dati sensibili o alla possibilità di danneggiamento dei dati da hello utente malintenzionato.
2. **Laddove possibile fare riferimento a criteri di accesso archiviati.** Archiviate consentono di criteri di accesso hello autorizzazioni toorevoke opzione senza chiavi dell'account di archiviazione tooregenerate hello. Scadenza set di hello su questi notevolmente in hello (o futuri infinito) e assicurarsi che ha aggiornato regolarmente toomove più lontano in hello future.
3. **Usare scadenze a breve termine per una firma di accesso condiviso ad hoc.** In questo modo, anche se una firma di accesso condiviso viene compromessa, è valida solo per un breve periodo di tempo. Questo consiglio è particolarmente importante se non è possibile fare riferimento a criteri di accesso archiviati Date di scadenza breve termine anche limitare hello di dati che possono essere scritti i blob tooa limitando hello ora disponibili tooupload tooit.
4. **Dispone di client rinnova automaticamente hello SAS, se necessario.** I client devono rinnovare hello SAS anche prima della scadenza di hello, nel tempo tooallow ordine per i tentativi se il servizio di hello fornendo hello SAS è disponibile. Se condiviso deve toobe utilizzato per un numero ridotto di controllo immediato, le operazioni di breve durate che previsto toobe completata entro il periodo di scadenza hello e questo potrebbe essere necessario come hello che firma di accesso condiviso non è previsto toobe rinnovato. Tuttavia, se si dispone di client che effettua regolarmente le richieste tramite firma di accesso condiviso, quindi il possibilità hello di scadenza entra in gioco. Hello è importante considerare il toobalance hello necessità per hello SAS toobe breve durata (indicato in precedenza) con tooensure necessità hello che hello client richiede il rinnovo anticipata sufficiente (tooavoid interruzione a causa di rinnovo in scadenza precedente toosuccessful di toohello SAS).
5. **Prestare attenzione all'ora di inizio della firma di accesso condiviso.** Se si imposta ora di inizio hello per una firma di accesso condiviso troppo**ora**, quindi a causa di inclinazione tooclock (le differenze nell'ora corrente di macchine toodifferent), gli errori possono essere osservati saltuariamente per hello alcuni minuti prima. In generale, impostare toobe ora di inizio hello almeno 15 minuti in hello precedente. Oppure evitare di impostarla, in modo che la firma diventi immediatamente valida in tutti i casi. Hello vale in genere anche - tempo tooexpiry tenere presente che è possibile osservare i minuti too15 del clock di inclinazione in entrambe le direzioni in qualsiasi richiesta. Per i client che usano un resto versione preliminare too2012-02-12, hello la durata massima per una firma di accesso condiviso che non fa riferimento a un criterio di accesso archiviati è di 1 ora e tutti i criteri che specifica a lungo termine rispetto che avrà esito negativo.
6. **Essere specifico con toobe risorse hello accessibili.** Una procedura consigliata è un utente con privilegi minimi necessari di hello tooprovide. Se un utente deve solo accesso in lettura tooa singola entità, quindi concedere loro l'accesso in lettura toothat singola entità ed entità tooall accesso non in lettura/scrittura/eliminazione. Ciò consente di ridurre i danni hello se una firma di accesso condiviso è compromesso perché hello SAS energetico nella mani hello di un utente malintenzionato.
7. **Comprendere che all'account verrà fatturato qualsiasi tipo di utilizzo, incluso quello effettuato con la firma di accesso condiviso.** Se si fornisce l'accesso in scrittura tooa blob, un utente può scegliere tooupload un blob di 200GB. Se è stato loro concesso anche l'accesso in lettura, si può scegliere toodownload sarà 10 volte, assunzione di 2 TB in uscita il costo per l'utente. Nuovamente, fornire autorizzazioni limitate toohelp ridurre possibili azioni di hello di utenti malintenzionati. Utilizzare questa minaccia di breve durata tooreduce SAS, ma tenere conto del clock sfasamento dell'ora di fine hello.
8. **Convalidare i dati scritti tramite la firma di accesso condiviso.** Quando un'applicazione client scrive un account di archiviazione di dati tooyour, tenere presente che si possono verificare problemi con i dati. Se l'applicazione richiede che i dati essere convalidati o autorizzati prima che venga toouse pronto, è consigliabile eseguire la convalida dopo la scrittura di dati hello e prima che venga utilizzato dall'applicazione. Questa procedura consente di proteggere anche rispetto a dati danneggiati o dannoso scritti tooyour account, un utente che ha acquisito correttamente hello SAS, o da un utente di sfruttare una firma di accesso condiviso persa.
9. **Non usare sempre SAS.** Talvolta i rischi di hello associati a una specifica operazione su account di archiviazione hello superare vantaggi in termini di firma di accesso condiviso. Per tali operazioni, creare un servizio di livello intermedio che scrive l'account di archiviazione tooyour dopo l'esecuzione di business di regola di convalida, l'autenticazione e controllo. Inoltre, a volte risulta più semplice accesso toomanage in altri modi. Ad esempio, se si desidera toomake tutti i BLOB in un contenitore sia leggibile pubblicamente, è possibile apportare hello contenitore pubblico, anziché fornire un client tooevery di firma di accesso condiviso per l'accesso.
10. **Usare archiviazione Analitica toomonitor l'applicazione.** È possibile utilizzare per la registrazione e metrica tooobserve eventuali picchi errori di autenticazione a causa di un'interruzione di tooan la firma di accesso condiviso provider servizio o toohello accidentale rimozione dei criteri di accesso archiviati. Vedere hello [Blog del Team di archiviazione Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) per ulteriori informazioni.

## <a name="sas-examples"></a>Esempi di firma di accesso condiviso
Di seguito sono riportati alcuni esempi di entrambi i tipi di firma di accesso condiviso, dell'account e del servizio.

toorun questi esempi in c#, è necessario hello tooreference seguenti pacchetti NuGet nel progetto:

* [Libreria Client di archiviazione Azure per .NET](http://www.nuget.org/packages/WindowsAzure.Storage), versione 6. x o versioni successive (toouse account SA).
* [Gestione configurazione di Azure](http://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)

Per ulteriori esempi che illustrano come toocreate e verificare una firma di accesso condiviso, vedere [Azure esempi di codice per l'archiviazione](https://azure.microsoft.com/documentation/samples/?service=storage).

### <a name="example-create-and-use-an-account-sas"></a>Esempio: Creare e usare una firma di accesso condiviso dell'account
esempio di codice seguente Hello crea un account di firma di accesso condiviso valido per servizi File e hello Blob e fornisce hello autorizzazioni client lettura, scrittura ed elencare le autorizzazioni tooaccess a livello di servizio API. account Hello SAS limita tooHTTPS protocollo hello, in modo hello richiesta deve essere effettuata con HTTPS.

```csharp
static string GetAccountSASToken()
{
    // toocreate hello account SAS, you need toouse your shared key credentials. Modify for your account.
    const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

    // Create a new access policy for hello account.
    SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()
        {
            Permissions = SharedAccessAccountPermissions.Read | SharedAccessAccountPermissions.Write | SharedAccessAccountPermissions.List,
            Services = SharedAccessAccountServices.Blob | SharedAccessAccountServices.File,
            ResourceTypes = SharedAccessAccountResourceTypes.Service,
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Protocols = SharedAccessProtocol.HttpsOnly
        };

    // Return hello SAS token.
    return storageAccount.GetSharedAccessSignature(policy);
}
```

toouse hello account SAS tooaccess a livello di servizio API per il servizio Blob hello, costruire un oggetto client Blob utilizzando hello SAS e hello endpoint di archiviazione Blob dell'account di archiviazione.

```csharp
static void UseAccountSAS(string sasToken)
{
    // Create new storage credentials using hello SAS token.
    StorageCredentials accountSAS = new StorageCredentials(sasToken);
    // Use these credentials and hello account name toocreate a Blob service client.
    CloudStorageAccount accountWithSAS = new CloudStorageAccount(accountSAS, "account-name", endpointSuffix: null, useHttps: true);
    CloudBlobClient blobClientWithSAS = accountWithSAS.CreateCloudBlobClient();

    // Now set hello service properties for hello Blob client created with hello SAS.
    blobClientWithSAS.SetServiceProperties(new ServiceProperties()
    {
        HourMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        MinuteMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        Logging = new LoggingProperties()
        {
            LoggingOperations = LoggingOperations.All,
            RetentionDays = 14,
            Version = "1.0"
        }
    });

    // hello permissions granted by hello account SAS also permit you tooretrieve service properties.
    ServiceProperties serviceProperties = blobClientWithSAS.GetServiceProperties();
    Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
    Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
    Console.WriteLine(serviceProperties.HourMetrics.Version);
}
```

### <a name="example-create-a-stored-access-policy"></a>Esempio: Creare criteri di accesso archiviati
Hello codice seguente crea un criterio di accesso archiviati in un contenitore. È possibile utilizzare i vincoli toospecify hello accesso dei criteri per un servizio di firma di accesso condiviso nel contenitore hello o nei relativi BLOB.

```csharp
private static async Task CreateSharedAccessPolicyAsync(CloudBlobContainer container, string policyName)
{
    // Create a new shared access policy and define its constraints.
    // hello access policy provides create, write, read, list, and delete permissions.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
        // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
        SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.List |
            SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create | SharedAccessBlobPermissions.Delete
    };

    // Get hello container's existing permissions.
    BlobContainerPermissions permissions = await container.GetPermissionsAsync();

    // Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    await container.SetPermissionsAsync(permissions);
}
```

### <a name="example-create-a-service-sas-on-a-container"></a>Esempio: Creare una firma di accesso condiviso del servizio su un contenitore
Hello di codice seguente crea una firma di accesso condiviso in un contenitore. Se viene specificato il nome di hello di un criterio di accesso archiviato esistente, tale criterio è associato a hello SAS. Se non viene fornito alcun criterio di accesso archiviati, codice hello crea una firma di accesso condiviso ad hoc nel contenitore hello.

```csharp
private static string GetContainerSasUri(CloudBlobContainer container, string storedPolicyName = null)
{
    string sasContainerToken;

    // If no stored policy is specified, create a new access policy and define its constraints.
    if (storedPolicyName == null)
    {
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocPolicy = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List
        };

        // Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
        sasContainerToken = container.GetSharedAccessSignature(adHocPolicy, null);

        Console.WriteLine("SAS for blob container (ad hoc): {0}", sasContainerToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello container. In this case, all of hello constraints for the
        // shared access signature are specified on hello stored access policy, which is provided by name.
        // It is also possible toospecify some constraints on an ad-hoc SAS and others on hello stored access policy.
        sasContainerToken = container.GetSharedAccessSignature(null, storedPolicyName);

        Console.WriteLine("SAS for blob container (stored access policy): {0}", sasContainerToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

### <a name="example-create-a-service-sas-on-a-blob"></a>Esempio: Creare una firma di accesso condiviso del servizio su un BLOB
Hello di codice seguente crea una firma di accesso condiviso in un blob. Se viene specificato il nome di hello di un criterio di accesso archiviato esistente, tale criterio è associato a hello SAS. Se non viene fornito alcun criterio di accesso archiviati, codice hello crea una firma di accesso condiviso ad hoc su blob hello.

```csharp
private static string GetBlobSasUri(CloudBlobContainer container, string blobName, string policyName = null)
{
    string sasBlobToken;

    // Get a reference tooa blob within hello container.
    // Note that hello blob may not exist yet, but a SAS can still be created for it.
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    if (policyName == null)
    {
        // Create a new access policy and define its constraints.
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocSAS = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create
        };

        // Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
        sasBlobToken = blob.GetSharedAccessSignature(adHocSAS);

        Console.WriteLine("SAS for blob (ad hoc): {0}", sasBlobToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello blob. In this case, all of hello constraints for the
        // shared access signature are specified on hello container's stored access policy.
        sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

        Console.WriteLine("SAS for blob (stored access policy): {0}", sasBlobToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

## <a name="conclusion"></a>Conclusioni
Firme di accesso condiviso sono utili per fornire autorizzazioni limitate tooclients di account di archiviazione tooyour che non dovrebbero essere chiave dell'account hello. Di conseguenza, sono una parte essenziale del modello di sicurezza hello per le applicazioni che utilizzano l'archiviazione di Azure. Se si seguono consigliate hello elencate di seguito, è possibile utilizzare una maggiore flessibilità tooprovide SAS di accesso tooresources nell'account di archiviazione, senza compromettere la sicurezza dell'applicazione hello.

## <a name="next-steps"></a>Passaggi successivi
* [Gestire BLOB e accesso in lettura anonimo toocontainers](storage-manage-access-to-resources.md)
* [Delega dell'accesso con una firma di accesso condiviso](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [Introduzione alla firma di accesso condiviso per tabelle e code](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)

[sas-storage-fe-proxy-service]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-fe-proxy-service.png
[sas-storage-provider-service]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-provider-service.png
[sas-storage-uri]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-uri.png

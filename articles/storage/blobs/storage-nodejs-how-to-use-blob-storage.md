---
title: aaaHow toouse archiviazione Blob da Node.js | Documenti Microsoft
description: Archiviare dati non strutturati nel cloud hello con archiviazione Blob di Azure (archiviazione di oggetti).
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 572e7fc9f7b19ff01720a7cadd495c809ed49fb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a>Come toouse archiviazione Blob da Node.js
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>Panoramica
In questo articolo illustra come tooperform scenari comuni di utilizzo dell'archiviazione Blob. esempi di Hello vengono scritti tramite hello API Node.js. scenari di Hello trattati includono come tooupload, elenco, scaricare ed eliminare i BLOB.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Creare un'applicazione Node.js
Per istruzioni su come toocreate un'applicazione Node.js, vedere [creare un'app web Node.js in Azure App Service], [compilare e distribuire un tooan di applicazione del servizio Cloud di Azure Node.js](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) : utilizzo di Windows PowerShell, o [compilare e distribuire un tooAzure di app web Node. js utilizzando WebMatrix](https://www.microsoft.com/web/webmatrix/).

## <a name="configure-your-application-tooaccess-storage"></a>Configurare l'archiviazione tooaccess applicazione
toouse archiviazione di Azure, è necessario hello Azure Storage SDK per Node.js, che include un set di librerie di praticità che comunicano con servizi REST di archiviazione hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Utilizzare un pacchetto di hello tooobtain nodo Package Manager (NPM)
1. Utilizzare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Unix), toonavigate toohello cartella in cui è stato creato l'esempio applicazione.
2. Tipo **npm installare archiviazione di azure** nella finestra di comando hello. Output del comando hello è simile toohello esempio di codice seguente.

        azure-storage@0.5.0 node_modules\azure-storage
        +-- extend@1.2.1
        +-- xmlbuilder@0.4.3
        +-- mime@1.2.11
        +-- node-uuid@1.4.3
        +-- validator@3.22.2
        +-- underscore@1.4.4
        +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
        +-- xml2js@0.2.7 (sax@0.5.2)
        +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. È possibile eseguire manualmente hello **ls** comando tooverify che un **nodo\_moduli** cartella è stata creata. All'interno di tale cartella, trovare hello **archiviazione di azure** pacchetto che contiene le librerie di hello che è necessario un archivio tooaccess.

### <a name="import-hello-package"></a>Importa pacchetto di hello
Utilizzando blocco note o un altro editor di testo, aggiungere hello seguente toohello cima hello **server.js** file dell'applicazione hello in cui si intende toouse archiviazione:

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Configurare una connessione di archiviazione di Azure
Hello modulo Azure verrà lette le variabili di ambiente hello `AZURE_STORAGE_ACCOUNT` e `AZURE_STORAGE_ACCESS_KEY`, o `AZURE_STORAGE_CONNECTION_STRING`, per le informazioni necessarie tooconnect tooyour account di archiviazione Azure. Se non vengono impostate queste variabili di ambiente, è necessario specificare le informazioni sull'account hello quando si chiama **createBlobService**.

Per un esempio di impostazione delle variabili di ambiente hello in hello [portale di Azure](https://portal.azure.com) per un'app web di Azure, vedere [app web Node. js utilizzando hello del servizio tabelle di Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).

## <a name="create-a-container"></a>Creare un contenitore
Hello **BlobService** oggetto consente di collaborare con i contenitori e BLOB. Hello codice seguente viene creata una **BlobService** oggetto. Aggiungere il seguente hello parte superiore di hello di **server.js**:

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> È possibile accedere in modo anonimo un blob utilizzando **createBlobServiceAnonymous** e fornendo l'indirizzo host hello. Ad esempio, usare `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Utilizzare un nuovo contenitore, toocreate **createContainerIfNotExists**. Hello esempio di codice seguente crea un nuovo contenitore denominato 'mycontainer':

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

Se il contenitore di hello appena creato, `result.created` è true. Se il contenitore di hello esiste già, `result.created` è false. `response`contiene informazioni sull'operazione di hello, incluse le informazioni di hello ETag per il contenitore di hello.

### <a name="container-security"></a>Sicurezza del contenitore
Per impostazione predefinita, i nuovi contenitori sono privati e non è possibile accedervi in modo anonimo. contenitore di hello toomake pubblico in modo che sia possibile accedervi in modo anonimo, è possibile impostare il livello di accesso del contenitore hello troppo**blob** o **contenitore**.

* **BLOB** -consente l'accesso in lettura anonimo tooblob contenuto e i metadati all'interno del contenitore, ma non toocontainer metadati, ad esempio l'elenco di tutti i BLOB in un contenitore
* **contenitore** -consente l'accesso in lettura anonimo tooblob contenuto e i metadati, nonché i metadati del contenitore

Hello esempio di codice riportato di seguito viene illustrato il livello di accesso hello impostazione troppo**blob**:

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

In alternativa, è possibile modificare il livello di accesso hello di un contenitore utilizzando **setContainerAcl** toospecify il livello di accesso hello. esempio modifiche hello accesso livello toocontainer di codice seguente di Hello:

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

risultato Hello contiene informazioni sull'operazione di hello, tra cui hello corrente **ETag** per contenitore hello.

### <a name="filters"></a>Filtri
È possibile applicare facoltativo il filtraggio operazioni toooperations eseguita mediante **BlobService**. Le operazioni di filtro possono includere la registrazione, la ripetizione automatica dei tentativi e così via. I filtri sono oggetti che implementano un metodo con firma hello:

```nodejs
function handle (requestOptions, next)
```

Dopo aver eseguito il pre-elaborazione sulle opzioni di richiesta di hello, metodo hello deve toocall "Avanti", il passaggio di un callback con hello seguente firma:

```nodejs
function (returnObject, finalCallback, next)
```

In questo callback e dopo l'elaborazione di hello returnObject (risposta hello dal server di hello richiesta toohello), il callback di hello richiede tooeither richiamare successivamente se esiste l'elaborazione di altri filtri toocontinue o semplicemente richiamare servizio hello di finalCallback tooend chiamata.

Due filtri, che implementano la logica di ripetizione sono inclusi in Azure SDK per Node.js, hello **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**. Hello seguito creato un **BlobService** oggetto che utilizza hello **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a>Caricare un BLOB in un contenitore
Esistono tre tipi di BLOB: BLOB in blocchi, BLOB di pagine e BLOB di accodamento. I BLOB in blocchi è toomore in modo efficiente caricare i dati di grandi dimensioni. I BLOB di accodamento sono ottimizzati per le operazioni di accodamento. I BLOB di pagine sono ottimizzati per le operazioni di lettura/scrittura. Per altre informazioni, vedere [Informazioni sui BLOB in blocchi, sui BLOB di aggiunta e sui BLOB di pagine](http://msdn.microsoft.com/library/azure/ee691964.aspx).

### <a name="block-blobs"></a>BLOB in blocchi
blob in blocchi tooa dati tooupload, utilizzare hello seguenti:

* **createBlockBlobFromLocalFile** : crea un nuovo blob in blocchi e carica il contenuto di hello di un file
* **createBlockBlobFromStream** : crea un nuovo blob in blocchi e carica il contenuto di hello di un flusso
* **createBlockBlobFromText** : crea un nuovo blob in blocchi e carica il contenuto di hello di una stringa
* **createWriteStreamToBlockBlob** -fornisce un blob in blocchi tooa flusso scrittura

esempio di codice seguente Hello carica il contenuto di hello di hello **test.txt** file **myblob**.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

Hello `result` restituito da questi metodi contiene informazioni sull'operazione di hello, ad esempio hello **ETag** del blob hello.

### <a name="append-blobs"></a>BLOB di accodamento
tooupload dati tooa nuovo blob di accodamento, utilizzare hello seguente:

* **createAppendBlobFromLocalFile** : crea un nuovo blob di aggiunta e carica il contenuto di hello di un file
* **createAppendBlobFromStream** : crea un nuovo blob di aggiunta e carica il contenuto di hello di un flusso
* **createAppendBlobFromText** : crea un nuovo blob di aggiunta e carica il contenuto di hello di una stringa
* **createWriteStreamToNewAppendBlob** : crea un nuovo blob di aggiunta e quindi fornisce un tooit toowrite flusso

esempio di codice seguente Hello carica il contenuto di hello di hello **test.txt** file **myappendblob**.

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

tooappend un tooan blocco esistente aggiungere blob, utilizzare hello seguenti:

* **appendFromLocalFile** -accodare hello contenuto di un file tooan esistente aggiungere blob
* **appendFromStream** -accodare hello contenuto di un flusso tooan esistente aggiungere blob
* **appendFromText** -aggiungere contenuto hello di tooan una stringa esistente aggiungere blob
* **appendBlockFromStream** -accodare hello contenuto di un flusso tooan esistente aggiungere blob
* **appendBlockFromText** -aggiungere contenuto hello di tooan una stringa esistente aggiungere blob

> [!NOTE]
> appendFromXXX API eseguirà alcune chiamate non necessari server di convalida lato client toofail tooavoid veloce. contrariamente alle API appendBlockFromXXX.
>
>

esempio di codice seguente Hello carica il contenuto di hello di hello **test.txt** file **myappendblob**.

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a>BLOB di pagine
blob di pagine tooa dati tooupload, utilizzare hello seguenti:

* **createPageBlob** : crea un nuovo BLOB di pagine con una lunghezza specifica
* **createPageBlobFromLocalFile** : crea un nuovo blob di pagine e carica il contenuto di hello di un file
* **createPageBlobFromStream** : crea un nuovo blob di pagine e carica il contenuto di hello di un flusso
* **createWriteStreamToExistingPageBlob** -fornisce un blob di pagine esistente scrittura flusso tooan
* **createWriteStreamToNewPageBlob** : crea un nuovo blob di pagine e quindi fornisce un tooit toowrite flusso

esempio di codice seguente Hello carica il contenuto di hello di hello **test.txt** file **mypageblob**.

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> I BLOB di pagine sono costituiti da "pagine" da 512 byte. Quando si caricano dati con una dimensione che non corrisponde a un multiplo di 512, viene visualizzato un errore.
>
>

## <a name="list-hello-blobs-in-a-container"></a>Elenco di BLOB hello in un contenitore
BLOB di hello toolist in un contenitore, usare hello **listBlobsSegmented** metodo. Se si desidera tooreturn BLOB con un prefisso specifico, utilizzare **listBlobsSegmentedWithPrefix**.

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

Hello `result` contiene un `entries` raccolta, ovvero una matrice di oggetti che descrivono ogni blob. Se non è possibile restituire tutti i BLOB, hello `result` fornisce inoltre un `continuationToken`, che è possibile utilizzare come hello secondo parametro tooretrieve ulteriori voci.

## <a name="download-blobs"></a>Scaricare BLOB
dati toodownload da un blob, utilizzare l'esempio hello:

* **getBlobToLocalFile** -scrive hello blob contenuto toofile
* **getBlobToStream** -scrive hello blob contenuto tooa flusso
* **getBlobToText** -scrive il contenuto di blob hello tooa stringa
* **createReadStream** -fornisce un tooread flusso dal blob hello

Hello esempio di codice seguente viene illustrato come utilizzare **getBlobToStream** contenuto hello toodownload di hello **myblob** blob e di archiviarlo toohello **txt** file utilizzando un flusso:

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

Hello `result` contiene informazioni sui blob di hello, tra cui **ETag** informazioni.

## <a name="delete-a-blob"></a>Eliminare un BLOB
Chiamare infine toodelete un blob, **deleteBlob**. Hello eliminazioni hello blob denominato di esempio di codice seguente **myblob**.

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a>Accesso simultaneo
blob di tooa toosupport accesso simultaneo da più client o più istanze di processo, è possibile utilizzare **eTag** o **lease**.

* **ETag** -fornisce un modo toodetect che hello blob o contenitore è stato modificato da un altro processo
* **Lease** : fornisce una scrittura esclusivo, rinnovabile, tooobtain modo o eliminare il blob tooa di accesso per un periodo di tempo

### <a name="etag"></a>ETag
Se è necessario tooallow più client o istanze toowrite toohello Blob di pagine o blocchi del Blob contemporaneamente, utilizzare ETag. Hello ETag consente toodetermine se hello contenitore o blob è stato modificato dopo la lettura di inizialmente o creato, che consente di sovrascrivere le modifiche a commit da un altro client o processo tooavoid.

È possibile impostare le condizioni di ETag utilizzando hello facoltativo `options.accessConditions` parametro. Hello esempio di codice seguente solo carica hello **test.txt** contenuti file se il blob hello esiste già e contiene il valore di ETag hello `etagToMatch`.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

Quando si utilizzano valori eTag, modello generale di hello è:

1. Ottenere hello ETag come risultato di hello di creazione un elenco operazione get.
2. Eseguire un'azione, il controllo che non è stato modificato il valore ETag hello.

Se è stato modificato il valore di hello, ciò indica che un altro client o un'istanza modificato hello blob o contenitore perché è stato ottenuto il valore di ETag hello.

### <a name="lease"></a>Lease
È possibile acquisire un nuovo lease utilizzando hello **acquireLease** metodo, specificando hello blob o il contenitore che si desidera tooobtain un lease in. Ad esempio, hello seguente codice acquisisce un lease su **myblob**.

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

Operazioni successive su **myblob** deve fornire hello `options.leaseId` parametro. come viene restituito l'ID lease di Hello `result.id` da **acquireLease**.

> [!NOTE]
> Per impostazione predefinita, la durata del lease hello è infinita. È possibile specificare una durata non infinito (compreso tra 15 e 60 secondi), fornendo hello `options.leaseDuration` parametro.
>
>

Utilizzare tooremove un lease, **releaseLease**. toobreak un lease, ma impedire ad altri utenti di ottenere un nuovo lease finché la durata originale hello è scaduto, utilizzare **breakLease**.

## <a name="work-with-shared-access-signatures"></a>Usare le firme di accesso condiviso di Azure
Firme di accesso condiviso (SAS) sono un tooblobs di accesso granulare tooprovide in modo sicuro e contenitori senza fornire il nome account di archiviazione o chiavi. Firme di accesso condiviso sono spesso i dati tooyour di accesso utilizzato tooprovide limitate, ad esempio per consentire a un'app mobile tooaccess BLOB.

> [!NOTE]
> Mentre è inoltre possibile consentire l'accesso anonimo tooblobs, firme di accesso condiviso consentono di tooprovide più controllato l'accesso, come è necessario generare hello SAS.
>
>

Un'applicazione attendibile, ad esempio un servizio basato su cloud genera firme di accesso condiviso utilizzando hello **generateSharedAccessSignature** di hello **BlobService**e fornisce tooan non attendibili o applicazione con attendibilità parziale, ad esempio un'app per dispositivi mobili. Le firme generate utilizzando un criterio, che descrive l'avvio di hello di accesso condiviso e la data di fine durante cui hello firme di accesso condiviso sono valide, nonché hello accedere titolare livello di firme di accesso condiviso toohello concesso.

esempio di codice seguente Hello genera un nuovo criterio di accesso condiviso che consente di hello condiviso accesso firme titolare tooperform operazioni di lettura nel hello **myblob** blob e scade 100 minuti dopo il tempo di hello viene creato.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

Si noti che le informazioni sull'host hello deve essere fornito, come richiesto quando titolare firme di accesso condiviso hello tenta anche contenitore hello tooaccess.

quindi l'applicazione client Hello utilizza le firme di accesso condiviso con **BlobServiceWithSAS** tooperform operazioni blob hello. Hello seguente ottiene informazioni sul **myblob**.

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

Poiché le firme di accesso condiviso hello generate con accesso in sola lettura, se viene effettuato un tentativo di blob hello toomodify, verrà restituito un errore.

### <a name="access-control-lists"></a>Elenchi di controllo di accesso
È anche possibile utilizzare criteri di accesso di accesso controllo elenco (ACL) tooset hello di SAS. Ciò è utile se si desidera tooallow più client tooaccess un contenitore ma forniscono criteri di accesso diversi per ogni client.

Un elenco di controllo di accesso viene implementato usando una matrice di criteri di accesso, con un ID associato a ogni criterio. Hello esempio di codice seguente definisce due criteri, uno per "user1" e uno per 'Utente2':

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Hello seguente ottiene di esempio di codice hello gli ACL per **mycontainer**e quindi aggiunge nuovi criteri hello utilizzando **setBlobAcl**. Risultato:

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Una volta hello che ACL viene impostato, è possibile quindi creare le firme di accesso condiviso in base all'ID di hello per un criterio. esempio di codice seguente Hello crea nuove firme di accesso condiviso per 'Utente2':

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello seguenti risorse.

* [Riferimento per le API di Azure Storage SDK per Node][Riferimento per le API di Azure Storage SDK per Node]
* [Blog del team di Archiviazione di Azure][Blog del team di Archiviazione di Azure]
* Repository di [Azure Storage SDK per Node][Azure Storage SDK for Node] su GitHub
* [Centro per sviluppatori di Node. js](https://azure.microsoft.com/develop/nodejs/)
* [Trasferimento dati con hello utilità della riga di comando AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

[App web Node. js utilizzando hello del servizio tabelle di Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)    
[Compilare e distribuire un tooAzure di app web Node. js utilizzando WebMatrix]: https://www.microsoft.com/web/webmatrix/  
[Utilizzando hello REST API]: [portale] http://msdn.microsoft.com/library/azure/hh264518.aspx: https://portal.azure.com [compilare e distribuire un tooan di applicazione del servizio Cloud di Azure Node.js](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Blog del Team di archiviazione di Azure]: http:// [Azure Storage SDK per nodo di riferimento all'API] blogs.msdn.com/b/windowsazurestorage/: http://dl.windowsazure.com/nodestoragedocs/index.html

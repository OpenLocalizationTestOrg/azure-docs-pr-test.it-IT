---
title: Come usare l'archiviazione BLOB di Azure da iOS | Microsoft Docs
description: Archiviare i dati non strutturati nel cloud con l'archivio BLOB (archivio di oggetti) di Azure.
services: storage
documentationcenter: ios
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: df188021-86fc-4d31-a810-1b0e7bcd814b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: objective-c
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: f238804e6031fcf3f194695a06bf5b88733a27b9
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-use-blob-storage-from-ios"></a>Come usare l'archivio BLOB da iOS
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Panoramica
Questa guida illustra i diversi scenari comuni di uso del servizio di archiviazione BLOB di Microsoft Azure. Gli esempi sono scritti in Objective-C e usano la [libreria del client di archiviazione di Azure per iOS](https://github.com/Azure/azure-storage-ios). Gli scenari illustrati includono **caricamento**, **visualizzazione in elenchi**, **download** e **eliminazione** di BLOB. Per ulteriori informazioni sui BLOB, vedere la sezione [Passaggi successivi](#next-steps) . È possibile scaricare l' [app di esempio](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) per visualizzare rapidamente l'uso di Archiviazione di Azure in un'applicazione iOS.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="import-the-azure-storage-ios-library-into-your-application"></a>Importare la libreria iOS di Archiviazione di Azure nell'applicazione
È possibile importare la libreria iOS di archiviazione di Azure nell'applicazione tramite l'uso del [CocoaPod di Archiviazione di Azure](https://cocoapods.org/pods/AZSClient) o importando il file **Framework** . CocoaPod è lo strumento consigliato, in quanto semplifica l'integrazione della libreria. Tuttavia, l'importazione dal file del framework è meno impegnativa per il progetto esistente.

Per usare questa libreria, sono necessari i componenti seguenti:
- iOS 8+
- Xcode 7+

## <a name="cocoapod"></a>CocoaPod
1. Se non ancora installato, [installare CocoaPod](https://guides.cocoapods.org/using/getting-started.html#toc_3) nel computer aprendo una finestra del terminale ed eseguendo il comando seguente
    
    ```shell   
    sudo gem install cocoapods
    ```

2. Successivamente, nella directory del progetto (la directory contenente il file con estensione xcodeproj), creare un nuovo file denominato _Podfile_ (senza estensione). Aggiungere il codice seguente a _Podfile_ e salvare.

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. Nella finestra del terminale passare alla directory del progetto ed eseguire il comando seguente

    ```shell    
    pod install
    ```

4. Se il file con estensione xcodeproj è aperto in Xcode, chiuderlo. Nella directory del progetto aprire il file di progetto appena creato che avrà l'estensione xcworkspace. Si tratta del file che verrà usato d'ora in poi.

## <a name="framework"></a>Framework
L'altro modo per usare la libreria consiste nel creare il framework manualmente:

1. Per prima cosa, scaricare o clonare il [repository azure-storage-ios](https://github.com/azure/azure-storage-ios).
2. Andare ad *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library* e aprire `AZSClient.xcodeproj` in Xcode.
3. In alto a sinistra in Xcode cambiare lo schema attivo da "Azure Storage Client Library" a "Framework".
4. Compilare il progetto (⌘+B). Verrà creato un file `AZSClient.framework` sulla scrivania.

È quindi possibile importare il file framework nell'applicazione eseguendo le seguenti operazioni:

1. Creare un nuovo progetto o aprire il progetto esistente in Xcode.
2. Trascinare `AZSClient.framework` nella struttura del progetto Xcode.
3. Selezionare *Copy items if needed* (Copia elementi se necessario) e fare clic su *Add* (Aggiungi).
4. Fare clic sul progetto nel riquadro di spostamento a sinistra e fare clic sulla scheda *General* nella parte superiore dell'editor del progetto.
5. Nella sezione *Linked Frameworks and Libraries* fare clic sul pulsante Add (+).
6. Nell'elenco di librerie già fornito cercare `libxml2.2.tbd` e aggiungerla al progetto.

## <a name="import-the-library"></a>Importare la libreria 
```objc
// Include the following import statement to use blob APIs.
#import <AZSClient/AZSClient.h>
```

Se si usa Swift, è necessario creare un'intestazione provvisoria e importare <AZSClient/AZSClient.h> qui:

1. Creare un file di intestazione `Bridging-Header.h` e aggiungere l'istruzione di importazione precedente.
2. Passare alla scheda *Build Settings* (Impostazioni compilazione) e cercare *Objective-C Bridging Header* (Intestazione provvisoria Objective-C).
3. Fare doppio clic nel campo di *Objective-C Bridging Header* (Intestazione provvisoria Objective-C) e aggiungere il percorso al file di intestazione: `ProjectName/Bridging-Header.h`
4. Creare il progetto (⌘+B) per verificare che l'intestazione provvisoria sia stata prelevata da Xcode.
5. È possibile iniziare a usare la libreria direttamente in qualsiasi file Swift, in quanto non è necessario importare istruzioni.

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a>Operazioni asincrone
> [!NOTE]
> Tutti i metodi che eseguono una richiesta al servizio sono operazioni asincrone. Negli esempi di codice si noterà che questi metodi hanno un gestore completamento. Il codice nel gestore completamento verrà eseguito **dopo** il completamento della richiesta. Il codice dopo il gestore completamento verrà eseguito **mentre** la richiesta è in corso.
> 
> 

## <a name="create-a-container"></a>Creare un contenitore
Ogni BLOB nell'archivio di Azure deve risiedere in un contenitore. L'esempio seguente mostra come creare un contenitore, denominato *newcontainer*, nell'account di archiviazione se non esiste già. Quando si sceglie un nome per il contenitore, tenere presenti le regole indicate in precedenza.

```objc
-(void)createContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"newcontainer"];

    // Create container in your Storage account if the container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

È possibile verificarne il funzionamento controllando [Esplora archivi di Microsoft Azure](http://storageexplorer.com) e accertandosi che *newcontainer* sia nell'elenco di contenitori dell'account di archiviazione.

## <a name="set-container-permissions"></a>Impostare le autorizzazioni del contenitore
Per impostazione predefinita, le autorizzazioni di un contenitore vengono configurate per l'accesso **Privato** . I contenitori, tuttavia, offrono alcune opzioni diverse per l'accesso al contenitore:

* **Privato**: dati BLOB e contenitore possono essere letti solo dal proprietario dell'account.
* **BLOB**: i dati BLOB all'interno di questo contenitore possono essere letti tramite richiesta anonima, ma i dati del contenitore non sono disponibili. I client non possono enumerare i BLOB all'interno del contenitore tramite richiesta anonima.
* **Contenitore**: dati BLOB e contenitore possono essere letti tramite richiesta anonima. I client possono enumerare i BLOB all'interno del contenitore tramite richiesta anonima, ma non sono in grado di enumerare i contenitori all'interno dell'account di archiviazione.

L'esempio seguente mostra come creare un contenitore con autorizzazioni di accesso **Contenitore**, che consentono l'accesso pubblico in sola lettura a tutti gli utenti in Internet:

```objc
-(void)createContainerWithPublicAccess{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create container in your Storage account if the container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a>Caricare un BLOB in un contenitore
Come accennato nella sezione [Concetti del servizio BLOB](#blob-service-concepts) , l'archiviazione BLOB offre tre diversi tipi di BLOB: BLOB in blocchi, BLOB di accodamento e BLOB di pagine. La libreria iOS di Archiviazione di Azure supporta tutti e tre i tipi di BLOB. Nella maggior parte dei casi è consigliabile usare il tipo di BLOB in blocchi.

L'esempio seguente mostra come caricare un BLOB in blocchi da NSString. Se in questo contenitore esiste già un BLOB con lo stesso nome, i contenuti del BLOB verranno sovrascritti.

```objc
-(void)uploadBlobToContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists)
        {
            if (error){
                NSLog(@"Error in creating container.");
            }
            else{
                // Create a local blob object
                AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

                // Upload blob to Storage
                [blockBlob uploadFromText:@"This text will be uploaded to Blob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

È possibile verificarne il funzionamento controllando [Esplora archivi di Microsoft Azure](http://storageexplorer.com) e accertandosi che il contenitore *containerpublic* contenga il BLOB *sampleblob*. Poiché in questo esempio è stato usato un contenitore pubblico, per verificarne il funzionamento è anche possibile passare all'URI dei BLOB:

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

Oltre che per caricare un BLOB in blocchi da NSString, esistono metodi simili per NSData, NSInputStream o un file locale.

## <a name="list-the-blobs-in-a-container"></a>Elencare i BLOB in un contenitore
L'esempio seguente mostra come elencare tutti i BLOB in un contenitore. Quando si esegue questa operazione, tenere presenti i parametri seguenti:     

* **continuationToken** : il token di continuazione indica dove deve iniziare l'operazione di elenco. Se non viene specificato alcun token, i BLOB verranno elencati dall'inizio. È possibile elencare qualsiasi numero di BLOB, da zero a un massimo impostato. Anche se questo metodo restituisce zero risultati, se `results.continuationToken` non è nil, il servizio potrebbe includere altri BLOB che non sono stati elencati.
* **prefix** : è possibile specificare il prefisso da usare per l'elenco di BLOB. Verranno elencati solo i BLOB che iniziano con questo prefisso.
* **useFlatBlobListing** : come accennato nella sezione [Assegnazione di nome e riferimento a contenitori e BLOB](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) , anche se il servizio BLOB è uno schema di Archiviazione semplice, è possibile creare una gerarchia virtuale assegnando ai BLOB un nome con le informazioni sul percorso. Gli elenchi non semplici, tuttavia, non sono attualmente supportati. Questa funzionalità sarà disponibile a breve. Per ora, questo valore dovrebbe essere **YES** (Sì).
* **blobListingDetails** : è possibile specificare quali elementi includere quando si elencano i BLOB
  * _AZSBlobListingDetailsNone_: elenca solo i BLOB di cui è stato eseguito il commit e non restituisce i metadati dei BLOB.
  * _AZSBlobListingDetailsSnapshots_: elenca i BLOB di cui è stato eseguito il commit e gli snapshot dei BLOB.
  * _AZSBlobListingDetailsMetadata_: recupera i metadati per ogni BLOB restituito nell'elenco.
  * _AZSBlobListingDetailsUncommittedBlobs_: elenca ii BLOB di cui è stato eseguito il commit e quelli per cui non è stato eseguito.
  * _AZSBlobListingDetailsCopy_: include le proprietà di copia nell'elenco.
  * _AZSBlobListingDetailsAll_: elenca tutti i BLOB di cui è stato eseguito il commit, quelli per cui non è stato eseguito e gli snapshot disponibili, nonché restituisce tutti i metadati e lo stato di copia per questi BLOB.
* **maxResults** : numero massimo di risultati da restituire per questa operazione. Per non impostare un limite, usare -1.
* **completionHandler** : blocco di codice da eseguire con i risultati dell'operazione di elenco.

In questo esempio viene usato un metodo helper per chiamare in modo ricorsivo il metodo list blobs ogni volta che viene restituito un token di continuazione.

```objc
-(void)listBlobsInContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    //List all blobs in container
    [self listBlobsInContainerHelper:blobContainer continuationToken:nil prefix:nil blobListingDetails:AZSBlobListingDetailsAll maxResults:-1 completionHandler:^(NSError *error) {
        if (error != nil){
            NSLog(@"Error in creating container.");
        }
    }];
}

//List blobs helper method
-(void)listBlobsInContainerHelper:(AZSCloudBlobContainer *)container continuationToken:(AZSContinuationToken *)continuationToken prefix:(NSString *)prefix blobListingDetails:(AZSBlobListingDetails)blobListingDetails maxResults:(NSUInteger)maxResults completionHandler:(void (^)(NSError *))completionHandler
{
    [container listBlobsSegmentedWithContinuationToken:continuationToken prefix:prefix useFlatBlobListing:YES blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:^(NSError *error, AZSBlobResultSegment *results) {
        if (error)
        {
            completionHandler(error);
        }
        else
        {
            for (int i = 0; i < results.blobs.count; i++) {
                NSLog(@"%@",[(AZSCloudBlockBlob *)results.blobs[i] blobName]);
            }
            if (results.continuationToken)
            {
                [self listBlobsInContainerHelper:container continuationToken:results.continuationToken prefix:prefix blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:completionHandler];
            }
            else
            {
                completionHandler(nil);
            }
        }
    }];
}
```

## <a name="download-a-blob"></a>Scaricare un BLOB
L'esempio seguente mostra come scaricare un BLOB in un oggetto NSString.

```objc
-(void)downloadBlobToString{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

    // Download blob
    [blockBlob downloadToTextWithCompletionHandler:^(NSError *error, NSString *text) {
        if (error) {
            NSLog(@"Error in downloading blob");
        }
        else{
            NSLog(@"%@",text);
        }
    }];
}
```

## <a name="delete-a-blob"></a>Eliminare un BLOB
L'esempio seguente mostra come eliminare un BLOB.

```objc
-(void)deleteBlob{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob1"];

    // Delete blob
    [blockBlob deleteWithCompletionHandler:^(NSError *error) {
        if (error) {
            NSLog(@"Error in deleting blob.");
        }
    }];
}
```

## <a name="delete-a-blob-container"></a>Eliminare un contenitore BLOB
L'esempio seguente mostra come eliminare un contenitore.

```objc
-(void)deleteContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Delete container
    [blobContainer deleteContainerIfExistsWithCompletionHandler:^(NSError *error, BOOL success) {
        if(error){
            NSLog(@"Error in deleting container");
        }
    }];
}
```

## <a name="next-steps"></a>Passaggi successivi
A questo punto, dopo avere appreso a usare l'archiviazione BLOB da iOS, seguire questi collegamenti per acquisire maggiori informazioni sulla libreria iOS e il servizio di archiviazione.

* [Libreria client di archiviazione di Azure per iOS](https://github.com/azure/azure-storage-ios)
* [Documentazione di riferimento iOS di Archiviazione di Azure](http://azure.github.io/azure-storage-ios/)
* [API REST dei servizi di archiviazione di Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog del team di Archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage)

In caso di domande sulla libreria, è possibile pubblicare un post nel [forum di Azure su MSDN](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) o in [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).
Per inviare suggerimenti per Archiviazione di Azure, pubblicare un post nella pagina dei [commenti e suggerimenti per Archiviazione di Azure](https://feedback.azure.com/forums/217298-storage/).


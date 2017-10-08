---
title: aaaHow toouse archiviazione Blob di Azure da iOS | Documenti Microsoft
description: Archiviare dati non strutturati nel cloud hello con archiviazione Blob di Azure (archiviazione di oggetti).
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
ms.openlocfilehash: cc08b76b682537a9a51e970c76bd76c7c06a4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ios"></a>Come toouse archiviazione Blob da iOS
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Panoramica
In questo articolo viene illustrato come tooperform scenari comuni di utilizzo dell'archiviazione Blob di Microsoft Azure. esempi di Hello scritte in Objective-C e utilizzare hello [libreria Client di archiviazione di Azure per iOS](https://github.com/Azure/azure-storage-ios). Hello scenari trattati includono **caricamento**, **elenco**, **download**, e **eliminazione** BLOB. Per ulteriori informazioni sui blob, vedere hello [passaggi successivi](#next-steps) sezione. È inoltre possibile scaricare hello [app di esempio](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly vedere hello utilizzo dell'archiviazione di Azure in un'applicazione iOS.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a>Hello Azure Storage iOS libreria di importazione in un'applicazione
È possibile importare libreria iOS di archiviazione di Azure hello in un'applicazione tramite l'utilizzo di hello [CocoaPod di archiviazione di Azure](https://cocoapods.org/pods/AZSClient) o importando hello **Framework** file. CocoaPod è hello consigliata modo come semplifica l'integrazione libreria hello, tuttavia, l'importazione dal file framework hello è meno intrusiva per il progetto esistente.

toouse questa libreria, è necessario hello seguenti:
- iOS 8+
- Xcode 7+

## <a name="cocoapod"></a>CocoaPod
1. Se non è già fatto, [CocoaPods installare](https://guides.cocoapods.org/using/getting-started.html#toc_3) nel computer in uso aprendo una finestra terminale e in esecuzione hello comando seguente
    
    ```shell   
    sudo gem install cocoapods
    ```

2. Successivamente, nella directory di progetto hello (directory hello che contiene il file con estensione xcodeproj), creare un nuovo file denominato _Podfile_(senza estensione di file). Aggiungere i seguenti too_Podfile_ hello e salvare.

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. Nella finestra terminal hello passare toohello directory del progetto e hello esecuzione comando seguente

    ```shell    
    pod install
    ```

4. Se il file con estensione xcodeproj è aperto in Xcode, chiuderlo. Nel file di progetto progetto directory aprire hello appena creato che avrà estensione .xcworkspace hello. Questo è il file hello in che verranno utilizzate da per ora.

## <a name="framework"></a>Framework
Hello altro modo libreria hello toouse è framework hello toobuild manualmente:

1. First, download o hello clone [repository di archiviazione-azure-ios](https://github.com/azure/azure-storage-ios).
2. Andare ad *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library* e aprire `AZSClient.xcodeproj` in Xcode.
3. In hello superiore sinistro di Xcode, hello modifica attiva di schema da "Azure Storage Client Library" troppo "Framework".
4. Compilazione progetto hello (⌘ + B). Verrà creato un file `AZSClient.framework` sulla scrivania.

È quindi possibile importare file di framework hello nell'applicazione eseguendo hello seguenti:

1. Creare un nuovo progetto o aprire il progetto esistente in Xcode.
2. Trascinamento della selezione hello `AZSClient.framework` in Xcode project navigator.
3. Selezionare *Copy items if needed* (Copia elementi se necessario) e fare clic su *Add* (Aggiungi).
4. Fare clic sul progetto nel riquadro di navigazione a sinistra hello e fare clic su hello *generale* scheda nella parte superiore di hello dell'editor di progetto hello.
5. In hello *Linked Frameworks and Libraries* fare clic sul pulsante Aggiungi hello (+).
6. Nell'elenco delle librerie già fornito hello cercare `libxml2.2.tbd` e aggiungerlo tooyour progetto.

## <a name="import-hello-library"></a>Importare hello libreria 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

Se si utilizza codice Swift, sarà anche necessario toocreate un'intestazione provvisorio e importare < AZSClient/AZSClient.h > non esiste:

1. Creare un file di intestazione `Bridging-Header.h`e aggiungere hello prima istruzione di importazione.
2. Passare toohello *Build Settings* scheda e cercare *intestazione Bridging Objective-C*.
3. Fare doppio clic sul campo hello di *intestazione Bridging Objective-C* e aggiungere i file di intestazione tooyour hello percorso:`ProjectName/Bridging-Header.h`
4. Compilazione hello progetto (⌘ + B) tooverify che hello bridging intestazione è stato prelevato da Xcode.
5. Iniziare a usare la libreria hello direttamente in qualsiasi file Swift, non è necessario per le istruzioni di importazione.

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a>Operazioni asincrone
> [!NOTE]
> Tutti i metodi che eseguono una richiesta nel servizio hello sono operazioni asincrone. Negli esempi di codice hello, sono disponibili che questi metodi hanno un gestore di completamento. Verrà eseguito il codice all'interno del gestore di completamento hello **dopo** hello richiesta è stata completata. Codice dopo che verrà eseguito il gestore di completamento hello **mentre** hello richiesta.
> 
> 

## <a name="create-a-container"></a>Creare un contenitore
Ogni BLOB nell'archivio di Azure deve risiedere in un contenitore. Hello esempio seguente viene illustrato come toocreate un contenitore, chiamare *newcontainer*, nell'account di archiviazione, se non esiste già. Quando si sceglie un nome per il contenitore, tenere in considerazione hello indicate in precedenza regole di denominazione.

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

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

È possibile verificare il funzionamento esaminando hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) e verificare che *newcontainer* è presente nell'elenco di hello di contenitori per l'account di archiviazione.

## <a name="set-container-permissions"></a>Impostare le autorizzazioni del contenitore
Per impostazione predefinita, le autorizzazioni di un contenitore vengono configurate per l'accesso **Privato** . I contenitori, tuttavia, offrono alcune opzioni diverse per l'accesso al contenitore:

* **Privato**: i dati blob e contenitore possono essere letti hello account solo dal proprietario.
* **BLOB**: i dati BLOB all'interno di questo contenitore possono essere letti tramite richiesta anonima, ma i dati del contenitore non sono disponibili. I client non è possibile enumerare i BLOB all'interno del contenitore di hello tramite una richiesta anonima.
* **Contenitore**: dati BLOB e contenitore possono essere letti tramite richiesta anonima. I client possono enumerare i BLOB all'interno del contenitore di hello tramite una richiesta anonima, ma non è possibile enumerare i contenitori nell'account di archiviazione hello.

Hello seguente esempio illustra come toocreate un contenitore con **contenitore** le autorizzazioni, che consentono l'accesso pubblico, di sola lettura per tutti gli utenti hello Internet di accesso:

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

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a>Caricare un BLOB in un contenitore
Come accennato in hello [concetti relativi al servizio Blob](#blob-service-concepts) sezione nell'archiviazione Blob offre tre diversi tipi di BLOB: BLOB in blocchi, BLOB di aggiunta e BLOB di pagine. libreria di iOS Hello archiviazione di Azure supporta tutti e tre i tipi di BLOB. Nella maggior parte dei casi, blob in blocchi è consigliata toouse tipo hello.

Hello di esempio seguente viene illustrato come un blocco tooupload blob da un NSString. Se un blob con stesso nome esiste già in questo contenitore hello, hello contenuto di questo blob verrà sovrascritto.

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

                // Upload blob tooStorage
                [blockBlob uploadFromText:@"This text will be uploaded tooBlob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

È possibile verificare il funzionamento esaminando hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) e verifica di tale contenitore, hello *containerpublic*, contiene il blob di hello, *sampleblob*. In questo esempio, è stato usato un contenitore pubblico per poter verificare anche che l'applicazione ha lavorato passare toohello BLOB URI:

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

Inoltre un blob in blocchi da un NSString toouploading, sono disponibili metodi simili per NSData, NSInputStream o un file locale.

## <a name="list-hello-blobs-in-a-container"></a>Elenco di BLOB hello in un contenitore
Hello esempio seguente viene illustrato come toolist tutti i BLOB in un contenitore. Quando si esegue questa operazione, tenere in considerazione hello seguenti parametri:     

* **continuationToken** -hello rappresenta token di continuazione in cui deve iniziare hello operazione di elenco. Se viene specificato alcun token, verranno visualizzate BLOB dall'inizio hello. Qualsiasi numero di BLOB può essere elencato, da zero backup tooa imposta un valore massimo. Anche se questo metodo restituisce zero risultati, se `results.continuationToken` non è null, potrebbero essere presenti altri BLOB nel servizio hello che non sono stati elencati.
* **prefisso** -è possibile specificare hello toouse di prefisso per l'elenco di blob. Verranno elencati solo i BLOB che iniziano con questo prefisso.
* **useFlatBlobListing** - come indicato in hello [denominazione e riferimento a contenitori e blob](#naming-and-referencing-containers-and-blobs) sezione, sebbene hello servizio Blob è uno schema di archiviazione lineare, è possibile creare una gerarchia virtuale assegnando un BLOB con percorso informazioni. Gli elenchi non semplici, tuttavia, non sono attualmente supportati. Questa funzionalità sarà disponibile a breve. Per ora, questo valore dovrebbe essere **YES** (Sì).
* **blobListingDetails** -è possibile specificare quali tooinclude elementi quando si elencano i BLOB
  * _AZSBlobListingDetailsNone_: elenca solo i BLOB di cui è stato eseguito il commit e non restituisce i metadati dei BLOB.
  * _AZSBlobListingDetailsSnapshots_: elenca i BLOB di cui è stato eseguito il commit e gli snapshot dei BLOB.
  * _AZSBlobListingDetailsMetadata_: recupera i metadati per ogni blob restituito nell'elenco di hello.
  * _AZSBlobListingDetailsUncommittedBlobs_: elenca ii BLOB di cui è stato eseguito il commit e quelli per cui non è stato eseguito.
  * _AZSBlobListingDetailsCopy_: includere copia le proprietà nell'elenco di hello.
  * _AZSBlobListingDetailsAll_: elenca tutti i BLOB di cui è stato eseguito il commit, quelli per cui non è stato eseguito e gli snapshot disponibili, nonché restituisce tutti i metadati e lo stato di copia per questi BLOB.
* **maxResults** -hello numero massimo di risultati tooreturn per questa operazione. Utilizzare -1 toonot impostare un limite.
* **completionHandler** -blocco hello di codice tooexecute con risultati hello di hello operazione di elenco.

In questo esempio, un metodo helper viene utilizzato toorecursively chiamata hello elenco BLOB ogni volta che viene restituito un token di continuazione.

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
Hello seguente esempio viene illustrato come un oggetto di blob tooa NSString toodownload.

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
Hello seguente esempio viene illustrato come toodelete un blob.

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
Hello seguente esempio viene illustrato come toodelete un contenitore.

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
Ora che si è appreso come toouse nell'archiviazione Blob da iOS, seguire questi toolearn collegamenti ulteriori informazioni sulla raccolta iOS hello e hello servizio di archiviazione.

* [Libreria client di archiviazione di Azure per iOS](https://github.com/azure/azure-storage-ios)
* [Documentazione di riferimento iOS di Archiviazione di Azure](http://azure.github.io/azure-storage-ios/)
* [API REST dei servizi di archiviazione di Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog del team di Archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage)

In caso di domande relative a questa libreria, è disponibile toopost tooour [forum MSDN di Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) o [Overflow dello Stack](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).
Se si dispone di suggerimenti sulle funzionalità di archiviazione di Azure, è possibile inviare troppo[commenti e suggerimenti di archiviazione Azure](https://feedback.azure.com/forums/217298-storage/).


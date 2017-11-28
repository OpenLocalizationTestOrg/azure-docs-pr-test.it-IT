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
# <a name="how-toouse-blob-storage-from-ios"></a><span data-ttu-id="4cfa6-103">Come toouse archiviazione Blob da iOS</span><span class="sxs-lookup"><span data-stu-id="4cfa6-103">How toouse Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="4cfa6-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="4cfa6-104">Overview</span></span>
<span data-ttu-id="4cfa6-105">In questo articolo viene illustrato come tooperform scenari comuni di utilizzo dell'archiviazione Blob di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-105">This article will show you how tooperform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="4cfa6-106">esempi di Hello scritte in Objective-C e utilizzare hello [libreria Client di archiviazione di Azure per iOS](https://github.com/Azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="4cfa6-106">hello samples are written in Objective-C and use hello [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="4cfa6-107">Hello scenari trattati includono **caricamento**, **elenco**, **download**, e **eliminazione** BLOB.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-107">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="4cfa6-108">Per ulteriori informazioni sui blob, vedere hello [passaggi successivi](#next-steps) sezione.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-108">For more information on blobs, see hello [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="4cfa6-109">È inoltre possibile scaricare hello [app di esempio](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly vedere hello utilizzo dell'archiviazione di Azure in un'applicazione iOS.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-109">You can also download hello [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly see hello use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="4cfa6-110">Hello Azure Storage iOS libreria di importazione in un'applicazione</span><span class="sxs-lookup"><span data-stu-id="4cfa6-110">Import hello Azure Storage iOS library into your application</span></span>
<span data-ttu-id="4cfa6-111">È possibile importare libreria iOS di archiviazione di Azure hello in un'applicazione tramite l'utilizzo di hello [CocoaPod di archiviazione di Azure](https://cocoapods.org/pods/AZSClient) o importando hello **Framework** file.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-111">You can import hello Azure Storage iOS library into your application either by using hello [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing hello **Framework** file.</span></span> <span data-ttu-id="4cfa6-112">CocoaPod è hello consigliata modo come semplifica l'integrazione libreria hello, tuttavia, l'importazione dal file framework hello è meno intrusiva per il progetto esistente.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-112">CocoaPod is hello recommended way as it makes integrating hello library easier, however importing from hello framework file is less intrusive for your existing project.</span></span>

<span data-ttu-id="4cfa6-113">toouse questa libreria, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="4cfa6-113">toouse this library, you need hello following:</span></span>
- <span data-ttu-id="4cfa6-114">iOS 8+</span><span class="sxs-lookup"><span data-stu-id="4cfa6-114">iOS 8+</span></span>
- <span data-ttu-id="4cfa6-115">Xcode 7+</span><span class="sxs-lookup"><span data-stu-id="4cfa6-115">Xcode 7+</span></span>

## <a name="cocoapod"></a><span data-ttu-id="4cfa6-116">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="4cfa6-116">CocoaPod</span></span>
1. <span data-ttu-id="4cfa6-117">Se non è già fatto, [CocoaPods installare](https://guides.cocoapods.org/using/getting-started.html#toc_3) nel computer in uso aprendo una finestra terminale e in esecuzione hello comando seguente</span><span class="sxs-lookup"><span data-stu-id="4cfa6-117">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running hello following command</span></span>
    
    ```shell   
    sudo gem install cocoapods
    ```

2. <span data-ttu-id="4cfa6-118">Successivamente, nella directory di progetto hello (directory hello che contiene il file con estensione xcodeproj), creare un nuovo file denominato _Podfile_(senza estensione di file).</span><span class="sxs-lookup"><span data-stu-id="4cfa6-118">Next, in hello project directory (hello directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="4cfa6-119">Aggiungere i seguenti too_Podfile_ hello e salvare.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-119">Add hello following too_Podfile_ and save.</span></span>

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. <span data-ttu-id="4cfa6-120">Nella finestra terminal hello passare toohello directory del progetto e hello esecuzione comando seguente</span><span class="sxs-lookup"><span data-stu-id="4cfa6-120">In hello terminal window, navigate toohello project directory and run hello following command</span></span>

    ```shell    
    pod install
    ```

4. <span data-ttu-id="4cfa6-121">Se il file con estensione xcodeproj è aperto in Xcode, chiuderlo.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-121">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="4cfa6-122">Nel file di progetto progetto directory aprire hello appena creato che avrà estensione .xcworkspace hello.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-122">In your project directory open hello newly created project file which will have hello .xcworkspace extension.</span></span> <span data-ttu-id="4cfa6-123">Questo è il file hello in che verranno utilizzate da per ora.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-123">This is hello file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="4cfa6-124">Framework</span><span class="sxs-lookup"><span data-stu-id="4cfa6-124">Framework</span></span>
<span data-ttu-id="4cfa6-125">Hello altro modo libreria hello toouse è framework hello toobuild manualmente:</span><span class="sxs-lookup"><span data-stu-id="4cfa6-125">hello other way toouse hello library is toobuild hello framework manually:</span></span>

1. <span data-ttu-id="4cfa6-126">First, download o hello clone [repository di archiviazione-azure-ios](https://github.com/azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="4cfa6-126">First, download or clone hello [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="4cfa6-127">Andare ad *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library* e aprire `AZSClient.xcodeproj` in Xcode.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-127">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open `AZSClient.xcodeproj` in Xcode.</span></span>
3. <span data-ttu-id="4cfa6-128">In hello superiore sinistro di Xcode, hello modifica attiva di schema da "Azure Storage Client Library" troppo "Framework".</span><span class="sxs-lookup"><span data-stu-id="4cfa6-128">At hello top-left of Xcode, change hello active scheme from "Azure Storage Client Library" too"Framework".</span></span>
4. <span data-ttu-id="4cfa6-129">Compilazione progetto hello (⌘ + B).</span><span class="sxs-lookup"><span data-stu-id="4cfa6-129">Build hello project (⌘+B).</span></span> <span data-ttu-id="4cfa6-130">Verrà creato un file `AZSClient.framework` sulla scrivania.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-130">This will create an `AZSClient.framework` file on your Desktop.</span></span>

<span data-ttu-id="4cfa6-131">È quindi possibile importare file di framework hello nell'applicazione eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="4cfa6-131">You can then import hello framework file into your application by doing hello following:</span></span>

1. <span data-ttu-id="4cfa6-132">Creare un nuovo progetto o aprire il progetto esistente in Xcode.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-132">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="4cfa6-133">Trascinamento della selezione hello `AZSClient.framework` in Xcode project navigator.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-133">Drag and drop hello `AZSClient.framework` into your Xcode project navigator.</span></span>
3. <span data-ttu-id="4cfa6-134">Selezionare *Copy items if needed* (Copia elementi se necessario) e fare clic su *Add* (Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="4cfa6-134">Select *Copy items if needed*, and click on *Finish*.</span></span>
4. <span data-ttu-id="4cfa6-135">Fare clic sul progetto nel riquadro di navigazione a sinistra hello e fare clic su hello *generale* scheda nella parte superiore di hello dell'editor di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-135">Click on your project in hello left-hand navigation and click hello *General* tab at hello top of hello project editor.</span></span>
5. <span data-ttu-id="4cfa6-136">In hello *Linked Frameworks and Libraries* fare clic sul pulsante Aggiungi hello (+).</span><span class="sxs-lookup"><span data-stu-id="4cfa6-136">Under hello *Linked Frameworks and Libraries* section, click hello Add button (+).</span></span>
6. <span data-ttu-id="4cfa6-137">Nell'elenco delle librerie già fornito hello cercare `libxml2.2.tbd` e aggiungerlo tooyour progetto.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-137">In hello list of libraries already provided, search for `libxml2.2.tbd` and add it tooyour project.</span></span>

## <a name="import-hello-library"></a><span data-ttu-id="4cfa6-138">Importare hello libreria</span><span class="sxs-lookup"><span data-stu-id="4cfa6-138">Import hello Library</span></span> 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

<span data-ttu-id="4cfa6-139">Se si utilizza codice Swift, sarà anche necessario toocreate un'intestazione provvisorio e importare < AZSClient/AZSClient.h > non esiste:</span><span class="sxs-lookup"><span data-stu-id="4cfa6-139">If you are using Swift, you will need toocreate a bridging header and import <AZSClient/AZSClient.h> there:</span></span>

1. <span data-ttu-id="4cfa6-140">Creare un file di intestazione `Bridging-Header.h`e aggiungere hello prima istruzione di importazione.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-140">Create a header file `Bridging-Header.h`, and add hello above import statement.</span></span>
2. <span data-ttu-id="4cfa6-141">Passare toohello *Build Settings* scheda e cercare *intestazione Bridging Objective-C*.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-141">Go toohello *Build Settings* tab, and search for *Objective-C Bridging Header*.</span></span>
3. <span data-ttu-id="4cfa6-142">Fare doppio clic sul campo hello di *intestazione Bridging Objective-C* e aggiungere i file di intestazione tooyour hello percorso:`ProjectName/Bridging-Header.h`</span><span class="sxs-lookup"><span data-stu-id="4cfa6-142">Double-click on hello field of *Objective-C Bridging Header* and add hello path tooyour header file: `ProjectName/Bridging-Header.h`</span></span>
4. <span data-ttu-id="4cfa6-143">Compilazione hello progetto (⌘ + B) tooverify che hello bridging intestazione è stato prelevato da Xcode.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-143">Build hello project (⌘+B) tooverify that hello bridging header was picked up by Xcode.</span></span>
5. <span data-ttu-id="4cfa6-144">Iniziare a usare la libreria hello direttamente in qualsiasi file Swift, non è necessario per le istruzioni di importazione.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-144">Start using hello library directly in any Swift file, there is no need for import statements.</span></span>

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="4cfa6-145">Operazioni asincrone</span><span class="sxs-lookup"><span data-stu-id="4cfa6-145">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="4cfa6-146">Tutti i metodi che eseguono una richiesta nel servizio hello sono operazioni asincrone.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-146">All methods that perform a request against hello service are asynchronous operations.</span></span> <span data-ttu-id="4cfa6-147">Negli esempi di codice hello, sono disponibili che questi metodi hanno un gestore di completamento.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-147">In hello code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="4cfa6-148">Verrà eseguito il codice all'interno del gestore di completamento hello **dopo** hello richiesta è stata completata.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-148">Code inside hello completion handler will run **after** hello request is completed.</span></span> <span data-ttu-id="4cfa6-149">Codice dopo che verrà eseguito il gestore di completamento hello **mentre** hello richiesta.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-149">Code after hello completion handler will run **while** hello request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="4cfa6-150">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="4cfa6-150">Create a container</span></span>
<span data-ttu-id="4cfa6-151">Ogni BLOB nell'archivio di Azure deve risiedere in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-151">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="4cfa6-152">Hello esempio seguente viene illustrato come toocreate un contenitore, chiamare *newcontainer*, nell'account di archiviazione, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-152">hello following example shows how toocreate a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="4cfa6-153">Quando si sceglie un nome per il contenitore, tenere in considerazione hello indicate in precedenza regole di denominazione.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-153">When choosing a name for your container, be mindful of hello naming rules mentioned above.</span></span>

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

<span data-ttu-id="4cfa6-154">È possibile verificare il funzionamento esaminando hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) e verificare che *newcontainer* è presente nell'elenco di hello di contenitori per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-154">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in hello list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="4cfa6-155">Impostare le autorizzazioni del contenitore</span><span class="sxs-lookup"><span data-stu-id="4cfa6-155">Set Container Permissions</span></span>
<span data-ttu-id="4cfa6-156">Per impostazione predefinita, le autorizzazioni di un contenitore vengono configurate per l'accesso **Privato** .</span><span class="sxs-lookup"><span data-stu-id="4cfa6-156">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="4cfa6-157">I contenitori, tuttavia, offrono alcune opzioni diverse per l'accesso al contenitore:</span><span class="sxs-lookup"><span data-stu-id="4cfa6-157">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="4cfa6-158">**Privato**: i dati blob e contenitore possono essere letti hello account solo dal proprietario.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-158">**Private**: Container and blob data can be read by hello account owner only.</span></span>
* <span data-ttu-id="4cfa6-159">**BLOB**: i dati BLOB all'interno di questo contenitore possono essere letti tramite richiesta anonima, ma i dati del contenitore non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-159">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="4cfa6-160">I client non è possibile enumerare i BLOB all'interno del contenitore di hello tramite una richiesta anonima.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-160">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="4cfa6-161">**Contenitore**: dati BLOB e contenitore possono essere letti tramite richiesta anonima.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-161">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="4cfa6-162">I client possono enumerare i BLOB all'interno del contenitore di hello tramite una richiesta anonima, ma non è possibile enumerare i contenitori nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-162">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="4cfa6-163">Hello seguente esempio illustra come toocreate un contenitore con **contenitore** le autorizzazioni, che consentono l'accesso pubblico, di sola lettura per tutti gli utenti hello Internet di accesso:</span><span class="sxs-lookup"><span data-stu-id="4cfa6-163">hello following example shows you how toocreate a container with **Container** access permissions, which will allow public, read-only access for all users on hello Internet:</span></span>

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

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="4cfa6-164">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="4cfa6-164">Upload a blob into a container</span></span>
<span data-ttu-id="4cfa6-165">Come accennato in hello [concetti relativi al servizio Blob](#blob-service-concepts) sezione nell'archiviazione Blob offre tre diversi tipi di BLOB: BLOB in blocchi, BLOB di aggiunta e BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-165">As mentioned in hello [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="4cfa6-166">libreria di iOS Hello archiviazione di Azure supporta tutti e tre i tipi di BLOB.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-166">hello Azure Storage iOS library supports all three types of blobs.</span></span> <span data-ttu-id="4cfa6-167">Nella maggior parte dei casi, blob in blocchi è consigliata toouse tipo hello.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-167">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="4cfa6-168">Hello di esempio seguente viene illustrato come un blocco tooupload blob da un NSString.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-168">hello following example shows how tooupload a block blob from an NSString.</span></span> <span data-ttu-id="4cfa6-169">Se un blob con stesso nome esiste già in questo contenitore hello, hello contenuto di questo blob verrà sovrascritto.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-169">If a blob with hello same name already exists in this container, hello contents of this blob will be overwritten.</span></span>

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

<span data-ttu-id="4cfa6-170">È possibile verificare il funzionamento esaminando hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) e verifica di tale contenitore, hello *containerpublic*, contiene il blob di hello, *sampleblob*.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-170">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that hello container, *containerpublic*, contains hello blob, *sampleblob*.</span></span> <span data-ttu-id="4cfa6-171">In questo esempio, è stato usato un contenitore pubblico per poter verificare anche che l'applicazione ha lavorato passare toohello BLOB URI:</span><span class="sxs-lookup"><span data-stu-id="4cfa6-171">In this sample, we used a public container so you can also verify that this application worked by going toohello blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="4cfa6-172">Inoltre un blob in blocchi da un NSString toouploading, sono disponibili metodi simili per NSData, NSInputStream o un file locale.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-172">In addition toouploading a block blob from an NSString, similar methods exist for NSData, NSInputStream, or a local file.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="4cfa6-173">Elenco di BLOB hello in un contenitore</span><span class="sxs-lookup"><span data-stu-id="4cfa6-173">List hello blobs in a container</span></span>
<span data-ttu-id="4cfa6-174">Hello esempio seguente viene illustrato come toolist tutti i BLOB in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-174">hello following example shows how toolist all blobs in a container.</span></span> <span data-ttu-id="4cfa6-175">Quando si esegue questa operazione, tenere in considerazione hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="4cfa6-175">When performing this operation, be mindful of hello following parameters:</span></span>     

* <span data-ttu-id="4cfa6-176">**continuationToken** -hello rappresenta token di continuazione in cui deve iniziare hello operazione di elenco.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-176">**continuationToken** - hello continuation token represents where hello listing operation should start.</span></span> <span data-ttu-id="4cfa6-177">Se viene specificato alcun token, verranno visualizzate BLOB dall'inizio hello.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-177">If no token is provided, it will list blobs from hello beginning.</span></span> <span data-ttu-id="4cfa6-178">Qualsiasi numero di BLOB può essere elencato, da zero backup tooa imposta un valore massimo.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-178">Any number of blobs can be listed, from zero up tooa set maximum.</span></span> <span data-ttu-id="4cfa6-179">Anche se questo metodo restituisce zero risultati, se `results.continuationToken` non è null, potrebbero essere presenti altri BLOB nel servizio hello che non sono stati elencati.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-179">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on hello service that have not been listed.</span></span>
* <span data-ttu-id="4cfa6-180">**prefisso** -è possibile specificare hello toouse di prefisso per l'elenco di blob.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-180">**prefix** - You can specify hello prefix toouse for blob listing.</span></span> <span data-ttu-id="4cfa6-181">Verranno elencati solo i BLOB che iniziano con questo prefisso.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-181">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="4cfa6-182">**useFlatBlobListing** - come indicato in hello [denominazione e riferimento a contenitori e blob](#naming-and-referencing-containers-and-blobs) sezione, sebbene hello servizio Blob è uno schema di archiviazione lineare, è possibile creare una gerarchia virtuale assegnando un BLOB con percorso informazioni.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-182">**useFlatBlobListing** - As mentioned in hello [Naming and referencing containers and blobs](#naming-and-referencing-containers-and-blobs) section, although hello Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="4cfa6-183">Gli elenchi non semplici, tuttavia, non sono attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-183">However, non-flat listing is currently not supported.</span></span> <span data-ttu-id="4cfa6-184">Questa funzionalità sarà disponibile a breve.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-184">This feature is coming soon.</span></span> <span data-ttu-id="4cfa6-185">Per ora, questo valore dovrebbe essere **YES** (Sì).</span><span class="sxs-lookup"><span data-stu-id="4cfa6-185">For now, this value should be **YES**.</span></span>
* <span data-ttu-id="4cfa6-186">**blobListingDetails** -è possibile specificare quali tooinclude elementi quando si elencano i BLOB</span><span class="sxs-lookup"><span data-stu-id="4cfa6-186">**blobListingDetails** - You can specify which items tooinclude when listing blobs</span></span>
  * <span data-ttu-id="4cfa6-187">_AZSBlobListingDetailsNone_: elenca solo i BLOB di cui è stato eseguito il commit e non restituisce i metadati dei BLOB.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-187">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="4cfa6-188">_AZSBlobListingDetailsSnapshots_: elenca i BLOB di cui è stato eseguito il commit e gli snapshot dei BLOB.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-188">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="4cfa6-189">_AZSBlobListingDetailsMetadata_: recupera i metadati per ogni blob restituito nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-189">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in hello listing.</span></span>
  * <span data-ttu-id="4cfa6-190">_AZSBlobListingDetailsUncommittedBlobs_: elenca ii BLOB di cui è stato eseguito il commit e quelli per cui non è stato eseguito.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-190">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="4cfa6-191">_AZSBlobListingDetailsCopy_: includere copia le proprietà nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-191">_AZSBlobListingDetailsCopy_: Include copy properties in hello listing.</span></span>
  * <span data-ttu-id="4cfa6-192">_AZSBlobListingDetailsAll_: elenca tutti i BLOB di cui è stato eseguito il commit, quelli per cui non è stato eseguito e gli snapshot disponibili, nonché restituisce tutti i metadati e lo stato di copia per questi BLOB.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-192">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="4cfa6-193">**maxResults** -hello numero massimo di risultati tooreturn per questa operazione.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-193">**maxResults** - hello maximum number of results tooreturn for this operation.</span></span> <span data-ttu-id="4cfa6-194">Utilizzare -1 toonot impostare un limite.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-194">Use -1 toonot set a limit.</span></span>
* <span data-ttu-id="4cfa6-195">**completionHandler** -blocco hello di codice tooexecute con risultati hello di hello operazione di elenco.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-195">**completionHandler** - hello block of code tooexecute with hello results of hello listing operation.</span></span>

<span data-ttu-id="4cfa6-196">In questo esempio, un metodo helper viene utilizzato toorecursively chiamata hello elenco BLOB ogni volta che viene restituito un token di continuazione.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-196">In this example, a helper method is used toorecursively call hello list blobs method every time a continuation token is returned.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="4cfa6-197">Scaricare un BLOB</span><span class="sxs-lookup"><span data-stu-id="4cfa6-197">Download a blob</span></span>
<span data-ttu-id="4cfa6-198">Hello seguente esempio viene illustrato come un oggetto di blob tooa NSString toodownload.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-198">hello following example shows how toodownload a blob tooa NSString object.</span></span>

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

## <a name="delete-a-blob"></a><span data-ttu-id="4cfa6-199">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="4cfa6-199">Delete a blob</span></span>
<span data-ttu-id="4cfa6-200">Hello seguente esempio viene illustrato come toodelete un blob.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-200">hello following example shows how toodelete a blob.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="4cfa6-201">Eliminare un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="4cfa6-201">Delete a blob container</span></span>
<span data-ttu-id="4cfa6-202">Hello seguente esempio viene illustrato come toodelete un contenitore.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-202">hello following example shows how toodelete a container.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4cfa6-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4cfa6-203">Next steps</span></span>
<span data-ttu-id="4cfa6-204">Ora che si è appreso come toouse nell'archiviazione Blob da iOS, seguire questi toolearn collegamenti ulteriori informazioni sulla raccolta iOS hello e hello servizio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4cfa6-204">Now that you've learned how toouse Blob Storage from iOS, follow these links toolearn more about hello iOS library and hello Storage service.</span></span>

* [<span data-ttu-id="4cfa6-205">Libreria client di archiviazione di Azure per iOS</span><span class="sxs-lookup"><span data-stu-id="4cfa6-205">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="4cfa6-206">Documentazione di riferimento iOS di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4cfa6-206">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="4cfa6-207">API REST dei servizi di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4cfa6-207">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="4cfa6-208">Blog del team di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4cfa6-208">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="4cfa6-209">In caso di domande relative a questa libreria, è disponibile toopost tooour [forum MSDN di Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) o [Overflow dello Stack](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span><span class="sxs-lookup"><span data-stu-id="4cfa6-209">If you have questions regarding this library, feel free toopost tooour [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="4cfa6-210">Se si dispone di suggerimenti sulle funzionalità di archiviazione di Azure, è possibile inviare troppo[commenti e suggerimenti di archiviazione Azure](https://feedback.azure.com/forums/217298-storage/).</span><span class="sxs-lookup"><span data-stu-id="4cfa6-210">If you have feature suggestions for Azure Storage, please post too[Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>


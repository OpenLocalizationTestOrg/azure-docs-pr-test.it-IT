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
ms.openlocfilehash: b5f43156d46b1ab9dd10ff5a93427270c1b839ca
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-ios"></a><span data-ttu-id="6299c-103">Come usare l'archivio BLOB da iOS</span><span class="sxs-lookup"><span data-stu-id="6299c-103">How to use Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="6299c-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6299c-104">Overview</span></span>
<span data-ttu-id="6299c-105">Questa guida illustra i diversi scenari comuni di uso del servizio di archiviazione BLOB di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6299c-105">This article will show you how to perform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="6299c-106">Gli esempi sono scritti in Objective-C e usano la [libreria del client di archiviazione di Azure per iOS](https://github.com/Azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="6299c-106">The samples are written in Objective-C and use the [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="6299c-107">Gli scenari illustrati includono **caricamento**, **visualizzazione in elenchi**, **download** e **eliminazione** di BLOB.</span><span class="sxs-lookup"><span data-stu-id="6299c-107">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="6299c-108">Per ulteriori informazioni sui BLOB, vedere la sezione [Passaggi successivi](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="6299c-108">For more information on blobs, see the [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="6299c-109">È possibile scaricare l' [app di esempio](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) per visualizzare rapidamente l'uso di Archiviazione di Azure in un'applicazione iOS.</span><span class="sxs-lookup"><span data-stu-id="6299c-109">You can also download the [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) to quickly see the use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="import-the-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="6299c-110">Importare la libreria iOS di Archiviazione di Azure nell'applicazione</span><span class="sxs-lookup"><span data-stu-id="6299c-110">Import the Azure Storage iOS library into your application</span></span>
<span data-ttu-id="6299c-111">È possibile importare la libreria iOS di archiviazione di Azure nell'applicazione tramite l'uso del [CocoaPod di Archiviazione di Azure](https://cocoapods.org/pods/AZSClient) o importando il file **Framework** .</span><span class="sxs-lookup"><span data-stu-id="6299c-111">You can import the Azure Storage iOS library into your application either by using the [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing the **Framework** file.</span></span> <span data-ttu-id="6299c-112">CocoaPod è lo strumento consigliato, in quanto semplifica l'integrazione della libreria. Tuttavia, l'importazione dal file del framework è meno impegnativa per il progetto esistente.</span><span class="sxs-lookup"><span data-stu-id="6299c-112">CocoaPod is the recommended way as it makes integrating the library easier, however importing from the framework file is less intrusive for your existing project.</span></span>

<span data-ttu-id="6299c-113">Per usare questa libreria, sono necessari i componenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="6299c-113">To use this library, you need the following:</span></span>
- <span data-ttu-id="6299c-114">iOS 8+</span><span class="sxs-lookup"><span data-stu-id="6299c-114">iOS 8+</span></span>
- <span data-ttu-id="6299c-115">Xcode 7+</span><span class="sxs-lookup"><span data-stu-id="6299c-115">Xcode 7+</span></span>

## <a name="cocoapod"></a><span data-ttu-id="6299c-116">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="6299c-116">CocoaPod</span></span>
1. <span data-ttu-id="6299c-117">Se non ancora installato, [installare CocoaPod](https://guides.cocoapods.org/using/getting-started.html#toc_3) nel computer aprendo una finestra del terminale ed eseguendo il comando seguente</span><span class="sxs-lookup"><span data-stu-id="6299c-117">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running the following command</span></span>
    
    ```shell   
    sudo gem install cocoapods
    ```

2. <span data-ttu-id="6299c-118">Successivamente, nella directory del progetto (la directory contenente il file con estensione xcodeproj), creare un nuovo file denominato _Podfile_ (senza estensione).</span><span class="sxs-lookup"><span data-stu-id="6299c-118">Next, in the project directory (the directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="6299c-119">Aggiungere il codice seguente a _Podfile_ e salvare.</span><span class="sxs-lookup"><span data-stu-id="6299c-119">Add the following to _Podfile_ and save.</span></span>

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. <span data-ttu-id="6299c-120">Nella finestra del terminale passare alla directory del progetto ed eseguire il comando seguente</span><span class="sxs-lookup"><span data-stu-id="6299c-120">In the terminal window, navigate to the project directory and run the following command</span></span>

    ```shell    
    pod install
    ```

4. <span data-ttu-id="6299c-121">Se il file con estensione xcodeproj è aperto in Xcode, chiuderlo.</span><span class="sxs-lookup"><span data-stu-id="6299c-121">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="6299c-122">Nella directory del progetto aprire il file di progetto appena creato che avrà l'estensione xcworkspace.</span><span class="sxs-lookup"><span data-stu-id="6299c-122">In your project directory open the newly created project file which will have the .xcworkspace extension.</span></span> <span data-ttu-id="6299c-123">Si tratta del file che verrà usato d'ora in poi.</span><span class="sxs-lookup"><span data-stu-id="6299c-123">This is the file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="6299c-124">Framework</span><span class="sxs-lookup"><span data-stu-id="6299c-124">Framework</span></span>
<span data-ttu-id="6299c-125">L'altro modo per usare la libreria consiste nel creare il framework manualmente:</span><span class="sxs-lookup"><span data-stu-id="6299c-125">The other way to use the library is to build the framework manually:</span></span>

1. <span data-ttu-id="6299c-126">Per prima cosa, scaricare o clonare il [repository azure-storage-ios](https://github.com/azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="6299c-126">First, download or clone the [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="6299c-127">Andare ad *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library* e aprire `AZSClient.xcodeproj` in Xcode.</span><span class="sxs-lookup"><span data-stu-id="6299c-127">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open `AZSClient.xcodeproj` in Xcode.</span></span>
3. <span data-ttu-id="6299c-128">In alto a sinistra in Xcode cambiare lo schema attivo da "Azure Storage Client Library" a "Framework".</span><span class="sxs-lookup"><span data-stu-id="6299c-128">At the top-left of Xcode, change the active scheme from "Azure Storage Client Library" to "Framework".</span></span>
4. <span data-ttu-id="6299c-129">Compilare il progetto (⌘+B).</span><span class="sxs-lookup"><span data-stu-id="6299c-129">Build the project (⌘+B).</span></span> <span data-ttu-id="6299c-130">Verrà creato un file `AZSClient.framework` sulla scrivania.</span><span class="sxs-lookup"><span data-stu-id="6299c-130">This will create an `AZSClient.framework` file on your Desktop.</span></span>

<span data-ttu-id="6299c-131">È quindi possibile importare il file framework nell'applicazione eseguendo le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="6299c-131">You can then import the framework file into your application by doing the following:</span></span>

1. <span data-ttu-id="6299c-132">Creare un nuovo progetto o aprire il progetto esistente in Xcode.</span><span class="sxs-lookup"><span data-stu-id="6299c-132">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="6299c-133">Trascinare `AZSClient.framework` nella struttura del progetto Xcode.</span><span class="sxs-lookup"><span data-stu-id="6299c-133">Drag and drop the `AZSClient.framework` into your Xcode project navigator.</span></span>
3. <span data-ttu-id="6299c-134">Selezionare *Copy items if needed* (Copia elementi se necessario) e fare clic su *Add* (Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="6299c-134">Select *Copy items if needed*, and click on *Finish*.</span></span>
4. <span data-ttu-id="6299c-135">Fare clic sul progetto nel riquadro di spostamento a sinistra e fare clic sulla scheda *General* nella parte superiore dell'editor del progetto.</span><span class="sxs-lookup"><span data-stu-id="6299c-135">Click on your project in the left-hand navigation and click the *General* tab at the top of the project editor.</span></span>
5. <span data-ttu-id="6299c-136">Nella sezione *Linked Frameworks and Libraries* fare clic sul pulsante Add (+).</span><span class="sxs-lookup"><span data-stu-id="6299c-136">Under the *Linked Frameworks and Libraries* section, click the Add button (+).</span></span>
6. <span data-ttu-id="6299c-137">Nell'elenco di librerie già fornito cercare `libxml2.2.tbd` e aggiungerla al progetto.</span><span class="sxs-lookup"><span data-stu-id="6299c-137">In the list of libraries already provided, search for `libxml2.2.tbd` and add it to your project.</span></span>

## <a name="import-the-library"></a><span data-ttu-id="6299c-138">Importare la libreria</span><span class="sxs-lookup"><span data-stu-id="6299c-138">Import the Library</span></span> 
```objc
// Include the following import statement to use blob APIs.
#import <AZSClient/AZSClient.h>
```

<span data-ttu-id="6299c-139">Se si usa Swift, è necessario creare un'intestazione provvisoria e importare <AZSClient/AZSClient.h> qui:</span><span class="sxs-lookup"><span data-stu-id="6299c-139">If you are using Swift, you will need to create a bridging header and import <AZSClient/AZSClient.h> there:</span></span>

1. <span data-ttu-id="6299c-140">Creare un file di intestazione `Bridging-Header.h` e aggiungere l'istruzione di importazione precedente.</span><span class="sxs-lookup"><span data-stu-id="6299c-140">Create a header file `Bridging-Header.h`, and add the above import statement.</span></span>
2. <span data-ttu-id="6299c-141">Passare alla scheda *Build Settings* (Impostazioni compilazione) e cercare *Objective-C Bridging Header* (Intestazione provvisoria Objective-C).</span><span class="sxs-lookup"><span data-stu-id="6299c-141">Go to the *Build Settings* tab, and search for *Objective-C Bridging Header*.</span></span>
3. <span data-ttu-id="6299c-142">Fare doppio clic nel campo di *Objective-C Bridging Header* (Intestazione provvisoria Objective-C) e aggiungere il percorso al file di intestazione: `ProjectName/Bridging-Header.h`</span><span class="sxs-lookup"><span data-stu-id="6299c-142">Double-click on the field of *Objective-C Bridging Header* and add the path to your header file: `ProjectName/Bridging-Header.h`</span></span>
4. <span data-ttu-id="6299c-143">Creare il progetto (⌘+B) per verificare che l'intestazione provvisoria sia stata prelevata da Xcode.</span><span class="sxs-lookup"><span data-stu-id="6299c-143">Build the project (⌘+B) to verify that the bridging header was picked up by Xcode.</span></span>
5. <span data-ttu-id="6299c-144">È possibile iniziare a usare la libreria direttamente in qualsiasi file Swift, in quanto non è necessario importare istruzioni.</span><span class="sxs-lookup"><span data-stu-id="6299c-144">Start using the library directly in any Swift file, there is no need for import statements.</span></span>

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="6299c-145">Operazioni asincrone</span><span class="sxs-lookup"><span data-stu-id="6299c-145">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="6299c-146">Tutti i metodi che eseguono una richiesta al servizio sono operazioni asincrone.</span><span class="sxs-lookup"><span data-stu-id="6299c-146">All methods that perform a request against the service are asynchronous operations.</span></span> <span data-ttu-id="6299c-147">Negli esempi di codice si noterà che questi metodi hanno un gestore completamento.</span><span class="sxs-lookup"><span data-stu-id="6299c-147">In the code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="6299c-148">Il codice nel gestore completamento verrà eseguito **dopo** il completamento della richiesta.</span><span class="sxs-lookup"><span data-stu-id="6299c-148">Code inside the completion handler will run **after** the request is completed.</span></span> <span data-ttu-id="6299c-149">Il codice dopo il gestore completamento verrà eseguito **mentre** la richiesta è in corso.</span><span class="sxs-lookup"><span data-stu-id="6299c-149">Code after the completion handler will run **while** the request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="6299c-150">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="6299c-150">Create a container</span></span>
<span data-ttu-id="6299c-151">Ogni BLOB nell'archivio di Azure deve risiedere in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="6299c-151">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="6299c-152">L'esempio seguente mostra come creare un contenitore, denominato *newcontainer*, nell'account di archiviazione se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="6299c-152">The following example shows how to create a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="6299c-153">Quando si sceglie un nome per il contenitore, tenere presenti le regole indicate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6299c-153">When choosing a name for your container, be mindful of the naming rules mentioned above.</span></span>

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

<span data-ttu-id="6299c-154">È possibile verificarne il funzionamento controllando [Esplora archivi di Microsoft Azure](http://storageexplorer.com) e accertandosi che *newcontainer* sia nell'elenco di contenitori dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6299c-154">You can confirm that this works by looking at the [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in the list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="6299c-155">Impostare le autorizzazioni del contenitore</span><span class="sxs-lookup"><span data-stu-id="6299c-155">Set Container Permissions</span></span>
<span data-ttu-id="6299c-156">Per impostazione predefinita, le autorizzazioni di un contenitore vengono configurate per l'accesso **Privato** .</span><span class="sxs-lookup"><span data-stu-id="6299c-156">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="6299c-157">I contenitori, tuttavia, offrono alcune opzioni diverse per l'accesso al contenitore:</span><span class="sxs-lookup"><span data-stu-id="6299c-157">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="6299c-158">**Privato**: dati BLOB e contenitore possono essere letti solo dal proprietario dell'account.</span><span class="sxs-lookup"><span data-stu-id="6299c-158">**Private**: Container and blob data can be read by the account owner only.</span></span>
* <span data-ttu-id="6299c-159">**BLOB**: i dati BLOB all'interno di questo contenitore possono essere letti tramite richiesta anonima, ma i dati del contenitore non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="6299c-159">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="6299c-160">I client non possono enumerare i BLOB all'interno del contenitore tramite richiesta anonima.</span><span class="sxs-lookup"><span data-stu-id="6299c-160">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="6299c-161">**Contenitore**: dati BLOB e contenitore possono essere letti tramite richiesta anonima.</span><span class="sxs-lookup"><span data-stu-id="6299c-161">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="6299c-162">I client possono enumerare i BLOB all'interno del contenitore tramite richiesta anonima, ma non sono in grado di enumerare i contenitori all'interno dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6299c-162">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="6299c-163">L'esempio seguente mostra come creare un contenitore con autorizzazioni di accesso **Contenitore**, che consentono l'accesso pubblico in sola lettura a tutti gli utenti in Internet:</span><span class="sxs-lookup"><span data-stu-id="6299c-163">The following example shows you how to create a container with **Container** access permissions, which will allow public, read-only access for all users on the Internet:</span></span>

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

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="6299c-164">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="6299c-164">Upload a blob into a container</span></span>
<span data-ttu-id="6299c-165">Come accennato nella sezione [Concetti del servizio BLOB](#blob-service-concepts) , l'archiviazione BLOB offre tre diversi tipi di BLOB: BLOB in blocchi, BLOB di accodamento e BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="6299c-165">As mentioned in the [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="6299c-166">La libreria iOS di Archiviazione di Azure supporta tutti e tre i tipi di BLOB.</span><span class="sxs-lookup"><span data-stu-id="6299c-166">The Azure Storage iOS library supports all three types of blobs.</span></span> <span data-ttu-id="6299c-167">Nella maggior parte dei casi è consigliabile usare il tipo di BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="6299c-167">In most cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="6299c-168">L'esempio seguente mostra come caricare un BLOB in blocchi da NSString.</span><span class="sxs-lookup"><span data-stu-id="6299c-168">The following example shows how to upload a block blob from an NSString.</span></span> <span data-ttu-id="6299c-169">Se in questo contenitore esiste già un BLOB con lo stesso nome, i contenuti del BLOB verranno sovrascritti.</span><span class="sxs-lookup"><span data-stu-id="6299c-169">If a blob with the same name already exists in this container, the contents of this blob will be overwritten.</span></span>

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

<span data-ttu-id="6299c-170">È possibile verificarne il funzionamento controllando [Esplora archivi di Microsoft Azure](http://storageexplorer.com) e accertandosi che il contenitore *containerpublic* contenga il BLOB *sampleblob*.</span><span class="sxs-lookup"><span data-stu-id="6299c-170">You can confirm that this works by looking at the [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that the container, *containerpublic*, contains the blob, *sampleblob*.</span></span> <span data-ttu-id="6299c-171">Poiché in questo esempio è stato usato un contenitore pubblico, per verificarne il funzionamento è anche possibile passare all'URI dei BLOB:</span><span class="sxs-lookup"><span data-stu-id="6299c-171">In this sample, we used a public container so you can also verify that this application worked by going to the blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="6299c-172">Oltre che per caricare un BLOB in blocchi da NSString, esistono metodi simili per NSData, NSInputStream o un file locale.</span><span class="sxs-lookup"><span data-stu-id="6299c-172">In addition to uploading a block blob from an NSString, similar methods exist for NSData, NSInputStream, or a local file.</span></span>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="6299c-173">Elencare i BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="6299c-173">List the blobs in a container</span></span>
<span data-ttu-id="6299c-174">L'esempio seguente mostra come elencare tutti i BLOB in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="6299c-174">The following example shows how to list all blobs in a container.</span></span> <span data-ttu-id="6299c-175">Quando si esegue questa operazione, tenere presenti i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="6299c-175">When performing this operation, be mindful of the following parameters:</span></span>     

* <span data-ttu-id="6299c-176">**continuationToken** : il token di continuazione indica dove deve iniziare l'operazione di elenco.</span><span class="sxs-lookup"><span data-stu-id="6299c-176">**continuationToken** - The continuation token represents where the listing operation should start.</span></span> <span data-ttu-id="6299c-177">Se non viene specificato alcun token, i BLOB verranno elencati dall'inizio.</span><span class="sxs-lookup"><span data-stu-id="6299c-177">If no token is provided, it will list blobs from the beginning.</span></span> <span data-ttu-id="6299c-178">È possibile elencare qualsiasi numero di BLOB, da zero a un massimo impostato.</span><span class="sxs-lookup"><span data-stu-id="6299c-178">Any number of blobs can be listed, from zero up to a set maximum.</span></span> <span data-ttu-id="6299c-179">Anche se questo metodo restituisce zero risultati, se `results.continuationToken` non è nil, il servizio potrebbe includere altri BLOB che non sono stati elencati.</span><span class="sxs-lookup"><span data-stu-id="6299c-179">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on the service that have not been listed.</span></span>
* <span data-ttu-id="6299c-180">**prefix** : è possibile specificare il prefisso da usare per l'elenco di BLOB.</span><span class="sxs-lookup"><span data-stu-id="6299c-180">**prefix** - You can specify the prefix to use for blob listing.</span></span> <span data-ttu-id="6299c-181">Verranno elencati solo i BLOB che iniziano con questo prefisso.</span><span class="sxs-lookup"><span data-stu-id="6299c-181">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="6299c-182">**useFlatBlobListing** : come accennato nella sezione [Assegnazione di nome e riferimento a contenitori e BLOB](#naming-and-referencing-containers-and-blobs) , anche se il servizio BLOB è uno schema di Archiviazione semplice, è possibile creare una gerarchia virtuale assegnando ai BLOB un nome con le informazioni sul percorso.</span><span class="sxs-lookup"><span data-stu-id="6299c-182">**useFlatBlobListing** - As mentioned in the [Naming and referencing containers and blobs](#naming-and-referencing-containers-and-blobs) section, although the Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="6299c-183">Gli elenchi non semplici, tuttavia, non sono attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="6299c-183">However, non-flat listing is currently not supported.</span></span> <span data-ttu-id="6299c-184">Questa funzionalità sarà disponibile a breve.</span><span class="sxs-lookup"><span data-stu-id="6299c-184">This feature is coming soon.</span></span> <span data-ttu-id="6299c-185">Per ora, questo valore dovrebbe essere **YES** (Sì).</span><span class="sxs-lookup"><span data-stu-id="6299c-185">For now, this value should be **YES**.</span></span>
* <span data-ttu-id="6299c-186">**blobListingDetails** : è possibile specificare quali elementi includere quando si elencano i BLOB</span><span class="sxs-lookup"><span data-stu-id="6299c-186">**blobListingDetails** - You can specify which items to include when listing blobs</span></span>
  * <span data-ttu-id="6299c-187">_AZSBlobListingDetailsNone_: elenca solo i BLOB di cui è stato eseguito il commit e non restituisce i metadati dei BLOB.</span><span class="sxs-lookup"><span data-stu-id="6299c-187">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="6299c-188">_AZSBlobListingDetailsSnapshots_: elenca i BLOB di cui è stato eseguito il commit e gli snapshot dei BLOB.</span><span class="sxs-lookup"><span data-stu-id="6299c-188">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="6299c-189">_AZSBlobListingDetailsMetadata_: recupera i metadati per ogni BLOB restituito nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="6299c-189">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in the listing.</span></span>
  * <span data-ttu-id="6299c-190">_AZSBlobListingDetailsUncommittedBlobs_: elenca ii BLOB di cui è stato eseguito il commit e quelli per cui non è stato eseguito.</span><span class="sxs-lookup"><span data-stu-id="6299c-190">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="6299c-191">_AZSBlobListingDetailsCopy_: include le proprietà di copia nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="6299c-191">_AZSBlobListingDetailsCopy_: Include copy properties in the listing.</span></span>
  * <span data-ttu-id="6299c-192">_AZSBlobListingDetailsAll_: elenca tutti i BLOB di cui è stato eseguito il commit, quelli per cui non è stato eseguito e gli snapshot disponibili, nonché restituisce tutti i metadati e lo stato di copia per questi BLOB.</span><span class="sxs-lookup"><span data-stu-id="6299c-192">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="6299c-193">**maxResults** : numero massimo di risultati da restituire per questa operazione.</span><span class="sxs-lookup"><span data-stu-id="6299c-193">**maxResults** - The maximum number of results to return for this operation.</span></span> <span data-ttu-id="6299c-194">Per non impostare un limite, usare -1.</span><span class="sxs-lookup"><span data-stu-id="6299c-194">Use -1 to not set a limit.</span></span>
* <span data-ttu-id="6299c-195">**completionHandler** : blocco di codice da eseguire con i risultati dell'operazione di elenco.</span><span class="sxs-lookup"><span data-stu-id="6299c-195">**completionHandler** - The block of code to execute with the results of the listing operation.</span></span>

<span data-ttu-id="6299c-196">In questo esempio viene usato un metodo helper per chiamare in modo ricorsivo il metodo list blobs ogni volta che viene restituito un token di continuazione.</span><span class="sxs-lookup"><span data-stu-id="6299c-196">In this example, a helper method is used to recursively call the list blobs method every time a continuation token is returned.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="6299c-197">Scaricare un BLOB</span><span class="sxs-lookup"><span data-stu-id="6299c-197">Download a blob</span></span>
<span data-ttu-id="6299c-198">L'esempio seguente mostra come scaricare un BLOB in un oggetto NSString.</span><span class="sxs-lookup"><span data-stu-id="6299c-198">The following example shows how to download a blob to a NSString object.</span></span>

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

## <a name="delete-a-blob"></a><span data-ttu-id="6299c-199">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="6299c-199">Delete a blob</span></span>
<span data-ttu-id="6299c-200">L'esempio seguente mostra come eliminare un BLOB.</span><span class="sxs-lookup"><span data-stu-id="6299c-200">The following example shows how to delete a blob.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="6299c-201">Eliminare un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="6299c-201">Delete a blob container</span></span>
<span data-ttu-id="6299c-202">L'esempio seguente mostra come eliminare un contenitore.</span><span class="sxs-lookup"><span data-stu-id="6299c-202">The following example shows how to delete a container.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6299c-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6299c-203">Next steps</span></span>
<span data-ttu-id="6299c-204">A questo punto, dopo avere appreso a usare l'archiviazione BLOB da iOS, seguire questi collegamenti per acquisire maggiori informazioni sulla libreria iOS e il servizio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6299c-204">Now that you've learned how to use Blob Storage from iOS, follow these links to learn more about the iOS library and the Storage service.</span></span>

* [<span data-ttu-id="6299c-205">Libreria client di archiviazione di Azure per iOS</span><span class="sxs-lookup"><span data-stu-id="6299c-205">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="6299c-206">Documentazione di riferimento iOS di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="6299c-206">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="6299c-207">API REST dei servizi di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="6299c-207">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="6299c-208">Blog del team di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="6299c-208">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="6299c-209">In caso di domande sulla libreria, è possibile pubblicare un post nel [forum di Azure su MSDN](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) o in [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span><span class="sxs-lookup"><span data-stu-id="6299c-209">If you have questions regarding this library, feel free to post to our [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="6299c-210">Per inviare suggerimenti per Archiviazione di Azure, pubblicare un post nella pagina dei [commenti e suggerimenti per Archiviazione di Azure](https://feedback.azure.com/forums/217298-storage/).</span><span class="sxs-lookup"><span data-stu-id="6299c-210">If you have feature suggestions for Azure Storage, please post to [Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>


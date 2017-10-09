---
title: archiviazione di Azure in applicazioni Windows Store aaaUse | Documenti Microsoft
description: Informazioni su come toocreate un di Windows Store app che utilizza l'archiviazione Blob di Azure, coda, tabella o File.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 63c4b29d-b2f2-4d7c-b164-a0d38f4d14f6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: ac21b0695c0d77c1d81c1b921718fb929945d45e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a><span data-ttu-id="0c161-103">Come toouse di archiviazione di Azure in applicazioni Windows Store</span><span class="sxs-lookup"><span data-stu-id="0c161-103">How toouse Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="0c161-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0c161-104">Overview</span></span>
<span data-ttu-id="0c161-105">Questa guida viene illustrata la modalità di avvio tooget con lo sviluppo di un'applicazione Windows Store che utilizza spazio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c161-105">This guide shows how tooget started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="0c161-106">Download degli strumenti richiesti</span><span class="sxs-lookup"><span data-stu-id="0c161-106">Download required tools</span></span>
* <span data-ttu-id="0c161-107">[Visual Studio](https://www.visualstudio.com/downloads/) rende facile toobuild, eseguire il debug, localizzare, creare un pacchetto e distribuire applicazioni Windows Store.</span><span class="sxs-lookup"><span data-stu-id="0c161-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy toobuild, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="0c161-108">È richiesto Visual Studio 2012 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="0c161-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="0c161-109">Hello [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) fornisce una libreria di classi Windows Runtime per l'utilizzo di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c161-109">hello [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="0c161-110">[WCF Data Services strumenti per App di Windows Store](http://www.microsoft.com/download/details.aspx?id=30714) estende l'esperienza di Aggiungi riferimento al servizio hello con supporto per OData sul lato client per applicazioni Windows Store in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0c161-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends hello Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="0c161-111">Sviluppo di applicazioni</span><span class="sxs-lookup"><span data-stu-id="0c161-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="0c161-112">Preparazione</span><span class="sxs-lookup"><span data-stu-id="0c161-112">Getting ready</span></span>
<span data-ttu-id="0c161-113">Creare un nuovo progetto di app di Windows Store in Visual Studio 2012 o versione successiva:</span><span class="sxs-lookup"><span data-stu-id="0c161-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![store-apps-storage-vs-project][store-apps-storage-vs-project]

<span data-ttu-id="0c161-115">Successivamente, aggiungere un toohello riferimento Azure Storage Client Library facendo **riferimenti**, facendo clic su **Aggiungi riferimento**e quindi esplorare toohello Storage Client Library per Windows Runtime che si download:</span><span class="sxs-lookup"><span data-stu-id="0c161-115">Next, add a reference toohello Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing toohello Storage Client Library for Windows Runtime that you downloaded:</span></span>

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a><span data-ttu-id="0c161-117">Tramite i servizi di coda e di libreria hello con hello Blob</span><span class="sxs-lookup"><span data-stu-id="0c161-117">Using hello library with hello Blob and Queue services</span></span>
<span data-ttu-id="0c161-118">A questo punto, l'app è servizi di accodamento e Blob di Azure di hello toocall pronto.</span><span class="sxs-lookup"><span data-stu-id="0c161-118">At this point, your app is ready toocall hello Azure Blob and Queue services.</span></span> <span data-ttu-id="0c161-119">Aggiungere il seguente hello **utilizzando** istruzioni in modo da fare riferimento direttamente a tipi di archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="0c161-119">Add hello following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="0c161-120">Successivamente, aggiungere una pagina di tooyour pulsante.</span><span class="sxs-lookup"><span data-stu-id="0c161-120">Next, add a button tooyour page.</span></span> <span data-ttu-id="0c161-121">Aggiungere hello seguente codice tooits **fare clic su** eventi e modificare il metodo del gestore eventi tramite hello [parola chiave async](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span><span class="sxs-lookup"><span data-stu-id="0c161-121">Add hello following code tooits **Click** event and modify your event handler method by using hello [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="0c161-122">Questo codice presuppone che si abbiano due variabili di stringa, *accountName* e *accountKey*.</span><span class="sxs-lookup"><span data-stu-id="0c161-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="0c161-123">Rappresentano nome hello dell'account e hello chiave account di archiviazione associato a tale account.</span><span class="sxs-lookup"><span data-stu-id="0c161-123">They represent hello name of your storage account and hello account key that is associated with that account.</span></span>

<span data-ttu-id="0c161-124">Compilare ed eseguire un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="0c161-124">Build and run hello application.</span></span> <span data-ttu-id="0c161-125">Facendo clic su pulsante hello controllerà se un contenitore denominato *container1* esista nell'account e quindi crearlo se non.</span><span class="sxs-lookup"><span data-stu-id="0c161-125">Clicking hello button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-hello-library-with-hello-table-service"></a><span data-ttu-id="0c161-126">Utilizzo della libreria hello con hello del servizio tabelle</span><span class="sxs-lookup"><span data-stu-id="0c161-126">Using hello library with hello Table service</span></span>
<span data-ttu-id="0c161-127">Tipi che sono utilizzati toocommunicate con il servizio tabelle di Azure hello dipendono da WCF Data Services per la libreria di app Windows Store hello.</span><span class="sxs-lookup"><span data-stu-id="0c161-127">Types that are used toocommunicate with hello Azure Table service depend on WCF Data Services for hello Windows Store app library.</span></span> <span data-ttu-id="0c161-128">Successivamente, aggiungere che un riferimento toohello necessarie librerie WCF utilizzando hello Console di gestione pacchetti:</span><span class="sxs-lookup"><span data-stu-id="0c161-128">Next, add a reference toohello required WCF libraries by using hello Package Manager Console:</span></span>

![store-apps-storage-package-manager][store-apps-storage-package-manager]

<span data-ttu-id="0c161-130">Comando che segue di hello utilizzare toopoint percorso toohello Package Manager nel computer:</span><span class="sxs-lookup"><span data-stu-id="0c161-130">Use hello following command toopoint Package Manager toohello location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="0c161-131">Questo comando aggiungerà automaticamente tutti i riferimenti richiesti tooyour progetto.</span><span class="sxs-lookup"><span data-stu-id="0c161-131">This command will automatically add all required references tooyour project.</span></span> <span data-ttu-id="0c161-132">Se non si desidera toouse hello Console di gestione pacchetti, è possibile aggiungere la cartella di hello NuGet WCF Data Services nell'elenco delle origini pacchetto toohello computer locale e quindi aggiungere il riferimento di hello tramite hello dell'interfaccia utente, come descritto in [gestione utilizzando pacchetti NuGet finestra di dialogo Hello](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span><span class="sxs-lookup"><span data-stu-id="0c161-132">If you do not want toouse hello Package Manager Console, you can add hello WCF Data Services NuGet folder on your local machine toohello list of package sources and then add hello reference through hello UI, as described in [Managing NuGet Packages Using hello Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="0c161-133">Quando si è fatto riferimento pacchetto NuGet WCF Data Services hello, modificare codice hello del pulsante **fare clic su** evento:</span><span class="sxs-lookup"><span data-stu-id="0c161-133">When you have referenced hello WCF Data Services NuGet package, change hello code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="0c161-134">Questo codice verifica se esiste una tabella denominata *table1* nell'account, creandone una se non esiste.</span><span class="sxs-lookup"><span data-stu-id="0c161-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="0c161-135">È inoltre possibile aggiungere un tooMicrosoft.WindowsAzure.Storage.Table.dll di riferimento, che è disponibile in hello stesso pacchetto scaricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0c161-135">You can also add a reference tooMicrosoft.WindowsAzure.Storage.Table.dll, which is available in hello same package that you downloaded.</span></span> <span data-ttu-id="0c161-136">Questa libreria contiene funzionalità aggiuntive, come la serializzazione basata su reflection e le query generiche.</span><span class="sxs-lookup"><span data-stu-id="0c161-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="0c161-137">Si noti che questa libreria non supporta JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0c161-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png

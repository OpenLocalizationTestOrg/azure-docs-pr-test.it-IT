---
title: Usare Archiviazione di Azure nelle app di Windows Store | Microsoft Docs
description: Scoprire come creare un'applicazione di Windows Store che usa l'archiviazione BLOB, code, tabelle o file di Azure.
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
ms.openlocfilehash: 43d38584270fbbbe6fa4e4ff8cef72ca44e14acc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-storage-in-windows-store-apps"></a><span data-ttu-id="7ecb2-103">Come usare l'archiviazione di Azure nelle app di Windows Store</span><span class="sxs-lookup"><span data-stu-id="7ecb2-103">How to use Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="7ecb2-104">Overview</span><span class="sxs-lookup"><span data-stu-id="7ecb2-104">Overview</span></span>
<span data-ttu-id="7ecb2-105">In questa guida viene illustrato come iniziare a sviluppare un'applicazione Windows Store che utilizzi l'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7ecb2-105">This guide shows how to get started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="7ecb2-106">Download degli strumenti richiesti</span><span class="sxs-lookup"><span data-stu-id="7ecb2-106">Download required tools</span></span>
* <span data-ttu-id="7ecb2-107">[Visual Studio](https://www.visualstudio.com/downloads/) semplifica le operazioni di compilazione, debug, localizzazione, creazione di pacchetti e distribuzione delle app di Windows Store.</span><span class="sxs-lookup"><span data-stu-id="7ecb2-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy to build, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="7ecb2-108">È richiesto Visual Studio 2012 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="7ecb2-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="7ecb2-109">La [libreria client di archiviazione di Azure](https://www.nuget.org/packages/WindowsAzure.Storage) fornisce una libreria di classi per Windows Runtime per l'uso di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7ecb2-109">The [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="7ecb2-110">[strumenti di WCF Data Services per app di Windows Store](http://www.microsoft.com/download/details.aspx?id=30714) ampliano l'esperienza della finestra di dialogo Aggiungi riferimento al servizio con il supporto OData lato client per le app di Windows Store in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ecb2-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends the Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="7ecb2-111">Sviluppo di applicazioni</span><span class="sxs-lookup"><span data-stu-id="7ecb2-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="7ecb2-112">Preparazione</span><span class="sxs-lookup"><span data-stu-id="7ecb2-112">Getting ready</span></span>
<span data-ttu-id="7ecb2-113">Creare un nuovo progetto di app di Windows Store in Visual Studio 2012 o versione successiva:</span><span class="sxs-lookup"><span data-stu-id="7ecb2-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![store-apps-storage-vs-project][store-apps-storage-vs-project]

<span data-ttu-id="7ecb2-115">Quindi aggiungere un riferimento alla libreria client di archiviazione di Azure facendo clic con il pulsante destro del mouse su **Riferimenti**, quindi scegliendo **Aggiungi riferimento** e passando alla libreria client di archiviazione per Windows Runtime scaricata:</span><span class="sxs-lookup"><span data-stu-id="7ecb2-115">Next, add a reference to the Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing to the Storage Client Library for Windows Runtime that you downloaded:</span></span>

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-the-library-with-the-blob-and-queue-services"></a><span data-ttu-id="7ecb2-117">Usare la libreria con BLOB e i servizi di accodamento</span><span class="sxs-lookup"><span data-stu-id="7ecb2-117">Using the library with the Blob and Queue services</span></span>
<span data-ttu-id="7ecb2-118">A questo punto l'app è pronta per chiamare i servizi BLOB e di accodamento di Azure.</span><span class="sxs-lookup"><span data-stu-id="7ecb2-118">At this point, your app is ready to call the Azure Blob and Queue services.</span></span> <span data-ttu-id="7ecb2-119">Aggiungere le seguenti istruzioni **using** in modo che sia possibile fare direttamente riferimento ai tipi di archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="7ecb2-119">Add the following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="7ecb2-120">Quindi, aggiungere un pulsante alla propria pagina.</span><span class="sxs-lookup"><span data-stu-id="7ecb2-120">Next, add a button to your page.</span></span> <span data-ttu-id="7ecb2-121">Aggiungere il codice seguente al relativo evento **Click** e modificare il metodo di gestione degli eventi utilizzando la [parola chiave async](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span><span class="sxs-lookup"><span data-stu-id="7ecb2-121">Add the following code to its **Click** event and modify your event handler method by using the [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="7ecb2-122">Questo codice presuppone che si abbiano due variabili di stringa, *accountName* e *accountKey*.</span><span class="sxs-lookup"><span data-stu-id="7ecb2-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="7ecb2-123">Esse rappresentano il nome dell’account di archiviazione e la chiave dell'account associati a tale account.</span><span class="sxs-lookup"><span data-stu-id="7ecb2-123">They represent the name of your storage account and the account key that is associated with that account.</span></span>

<span data-ttu-id="7ecb2-124">Compilare ed eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7ecb2-124">Build and run the application.</span></span> <span data-ttu-id="7ecb2-125">Fare clic sul pulsante per controllare prima se esiste un contenitore denominato *container1* nel proprio account e crearlo se non esiste.</span><span class="sxs-lookup"><span data-stu-id="7ecb2-125">Clicking the button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-the-library-with-the-table-service"></a><span data-ttu-id="7ecb2-126">Utilizzare la libreria con il servizio tabelle</span><span class="sxs-lookup"><span data-stu-id="7ecb2-126">Using the library with the Table service</span></span>
<span data-ttu-id="7ecb2-127">I tipi utilizzati per comunicare con il servizio tabelle di Azure dipendono dalla libreria di Servizi dati WCF per le app di Windows Store.</span><span class="sxs-lookup"><span data-stu-id="7ecb2-127">Types that are used to communicate with the Azure Table service depend on WCF Data Services for the Windows Store app library.</span></span> <span data-ttu-id="7ecb2-128">Di seguito, aggiungere un riferimento alle librerie WCF richieste usando la Console di Gestione pacchetti:</span><span class="sxs-lookup"><span data-stu-id="7ecb2-128">Next, add a reference to the required WCF libraries by using the Package Manager Console:</span></span>

![store-apps-storage-package-manager][store-apps-storage-package-manager]

<span data-ttu-id="7ecb2-130">Utilizzare il comando seguente per indirizzare Gestione Pacchetti alla posizione sul proprio computer:</span><span class="sxs-lookup"><span data-stu-id="7ecb2-130">Use the following command to point Package Manager to the location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="7ecb2-131">Questo comando consente di aggiungere automaticamente tutti i riferimenti richiesto al proprio progetto.</span><span class="sxs-lookup"><span data-stu-id="7ecb2-131">This command will automatically add all required references to your project.</span></span> <span data-ttu-id="7ecb2-132">Qualora non si desideri usare la Console di Gestione pacchetti è inoltre possibile aggiungere la cartella NuGet dei Servizi dati WCF sul computer locale all'elenco di origini pacchetti, quindi aggiungere il riferimento attraverso l'interfaccia utente, come descritto nell’articolo sulla [Gestione dei pacchetti NuGet mediante la finestra di dialogo](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span><span class="sxs-lookup"><span data-stu-id="7ecb2-132">If you do not want to use the Package Manager Console, you can add the WCF Data Services NuGet folder on your local machine to the list of package sources and then add the reference through the UI, as described in [Managing NuGet Packages Using the Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="7ecb2-133">Dopo aver fatto riferimento al pacchetto NuGet dei Servizi dati WCF modificare il codice nell'evento **Click** del proprio pulsante:</span><span class="sxs-lookup"><span data-stu-id="7ecb2-133">When you have referenced the WCF Data Services NuGet package, change the code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="7ecb2-134">Questo codice verifica se esiste una tabella denominata *table1* nell'account, creandone una se non esiste.</span><span class="sxs-lookup"><span data-stu-id="7ecb2-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="7ecb2-135">È inoltre possibile aggiungere un riferimento a Microsoft.WindowsAzure.Storage.Table.dll, disponibile nello stesso pacchetto scaricato.</span><span class="sxs-lookup"><span data-stu-id="7ecb2-135">You can also add a reference to Microsoft.WindowsAzure.Storage.Table.dll, which is available in the same package that you downloaded.</span></span> <span data-ttu-id="7ecb2-136">Questa libreria contiene funzionalità aggiuntive, come la serializzazione basata su reflection e le query generiche.</span><span class="sxs-lookup"><span data-stu-id="7ecb2-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="7ecb2-137">Si noti che questa libreria non supporta JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7ecb2-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png

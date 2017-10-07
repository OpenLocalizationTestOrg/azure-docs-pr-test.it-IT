---
title: le funzioni di Azure tramite Visual Studio aaaDevelop | Documenti Microsoft
description: Informazioni su come toodevelop e testare le funzioni di Azure utilizzando gli strumenti di funzioni di Azure per Visual Studio 2017.
services: functions
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: glenga
ms.openlocfilehash: c9baf882bf58068cb9a8930bea337fe51b2a77ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a><span data-ttu-id="0f032-103">Azure Functions Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0f032-103">Azure Functions Tools for Visual Studio</span></span>  

<span data-ttu-id="0f032-104">Strumenti di funzioni di Azure per Visual Studio 2017 è un'estensione di Visual Studio che consente di sviluppare, testare e distribuire le funzioni tooAzure di c#.</span><span class="sxs-lookup"><span data-stu-id="0f032-104">Azure Functions Tools for Visual Studio 2017 is an extension for Visual Studio that lets you develop, test, and deploy C# functions tooAzure.</span></span> <span data-ttu-id="0f032-105">Se questa è la prima esperienza con le funzioni di Azure, è possibile acquisire informazioni, vedere [tooAzure un'introduzione funzioni](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f032-105">If this is your first experience with Azure Functions, you can learn more at [An introduction tooAzure Functions](functions-overview.md).</span></span>

<span data-ttu-id="0f032-106">Strumenti di Azure funzioni Hello fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="0f032-106">hello Azure Functions Tools provides hello following benefits:</span></span> 

* <span data-ttu-id="0f032-107">Modifica, compilazione ed esecuzione di funzioni nel computer di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="0f032-107">Edit, build, and run functions on your local development computer.</span></span> 
* <span data-ttu-id="0f032-108">Pubblicazione delle funzioni di Azure direttamente progetto tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0f032-108">Publish your Azure Functions project directly tooAzure.</span></span> 
* <span data-ttu-id="0f032-109">Utilizzare le associazioni di funzioni di processi Web attributi toodeclare direttamente nel hello codice c# anziché mantenendo un function.json separato per le definizioni di associazione.</span><span class="sxs-lookup"><span data-stu-id="0f032-109">Use WebJobs attributes toodeclare function bindings directly in hello C# code instead of maintaining a separate function.json for binding definitions.</span></span>
* <span data-ttu-id="0f032-110">Sviluppo e distribuzione di funzioni C# precompilate.</span><span class="sxs-lookup"><span data-stu-id="0f032-110">Develop and deploy pre-compiled C# functions.</span></span> <span data-ttu-id="0f032-111">Le funzioni precompilate offrono migliori prestazioni nell'avvio a freddo rispetto alle funzioni basate su script C#.</span><span class="sxs-lookup"><span data-stu-id="0f032-111">Pre-complied functions provide a better cold-start performance than C# script-based functions.</span></span> 
* <span data-ttu-id="0f032-112">Codice delle funzioni in c# con tutti i vantaggi di hello di sviluppo di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f032-112">Code your functions in C# while having all of hello benefits of Visual Studio development.</span></span> 

<span data-ttu-id="0f032-113">Questo argomento viene illustrato come toouse hello Azure funzioni Tools per Visual Studio 2017 toodevelop delle funzioni in c#.</span><span class="sxs-lookup"><span data-stu-id="0f032-113">This topic shows you how toouse hello Azure Functions Tools for Visual Studio 2017 toodevelop your functions in C#.</span></span> <span data-ttu-id="0f032-114">Verrà inoltre descritto come toopublish tooAzure il progetto come assembly .NET.</span><span class="sxs-lookup"><span data-stu-id="0f032-114">You also learn how toopublish your project tooAzure as a .NET assembly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f032-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0f032-115">Prerequisites</span></span>

<span data-ttu-id="0f032-116">Gli strumenti di funzioni di Azure è incluso nel carico di lavoro di hello lo sviluppo di Azure di [Visual Studio 2017 versione 15.3](https://www.visualstudio.com/vs/), o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="0f032-116">Azure Functions Tools is included in hello Azure development workload of [Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/), or a later version.</span></span> <span data-ttu-id="0f032-117">Assicurarsi di includere hello **lo sviluppo di Azure** carico di lavoro nell'installazione di Visual Studio 2017 versione 15.3:</span><span class="sxs-lookup"><span data-stu-id="0f032-117">Make sure you include hello **Azure development** workload in your Visual Studio 2017 version 15.3 installation:</span></span>

![Installare Visual Studio 2017 con carico di lavoro di hello lo sviluppo di Azure](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

<span data-ttu-id="0f032-119">toocreate e distribuire funzioni, è inoltre necessario:</span><span class="sxs-lookup"><span data-stu-id="0f032-119">toocreate and deploy functions, you also need:</span></span>

* <span data-ttu-id="0f032-120">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="0f032-120">An active Azure subscription.</span></span> <span data-ttu-id="0f032-121">Se non si possiede una sottoscrizione di Azure, sono disponibili [account gratuiti](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="0f032-121">If you don't have an Azure subscription, [free accounts](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) are available.</span></span>

* <span data-ttu-id="0f032-122">Un account dell'Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f032-122">An Azure Storage account.</span></span> <span data-ttu-id="0f032-123">toocreate un account di archiviazione, vedere [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="0f032-123">toocreate a storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
## <a name="create-an-azure-functions-project"></a><span data-ttu-id="0f032-124">Creare un progetto di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="0f032-124">Create an Azure Functions project</span></span> 

[!INCLUDE [Create a project using hello Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-hello-project-for-local-development"></a><span data-ttu-id="0f032-125">Configurare il progetto hello per lo sviluppo locale</span><span class="sxs-lookup"><span data-stu-id="0f032-125">Configure hello project for local development</span></span>

<span data-ttu-id="0f032-126">Quando si crea un nuovo progetto utilizzando il modello di Azure funzioni hello, si ottiene un progetto c# vuoto che contiene i seguenti file hello:</span><span class="sxs-lookup"><span data-stu-id="0f032-126">When you create a new project using hello Azure Functions template, you get an empty C# project that contains hello following files:</span></span>

* <span data-ttu-id="0f032-127">**host.JSON**: consente di configurare hello host funzioni.</span><span class="sxs-lookup"><span data-stu-id="0f032-127">**host.json**: Lets you configure hello Functions host.</span></span> <span data-ttu-id="0f032-128">Queste impostazioni si applicano sia durante l'esecuzione in locale che nell'esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="0f032-128">These settings apply both when running locally and in Azure.</span></span> <span data-ttu-id="0f032-129">Per altre informazioni, vedere l'articolo di riferimento su [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="0f032-129">For more information, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) reference article.</span></span>
    
* <span data-ttu-id="0f032-130">**local.settings.json**: mantiene le impostazioni usate quando si esegue Funzioni localmente.</span><span class="sxs-lookup"><span data-stu-id="0f032-130">**local.settings.json**: Maintains settings used when running functions locally.</span></span> <span data-ttu-id="0f032-131">Queste impostazioni non vengono utilizzate da Azure, vengono usati da hello [strumenti di base di Azure funzioni](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="0f032-131">These settings are not used by Azure, they are used by hello [Azure Functions Core Tools](functions-run-local.md).</span></span> <span data-ttu-id="0f032-132">Usare le impostazioni toospecify questo file, ad esempio le stringhe di connessione tooother Azure servizi.</span><span class="sxs-lookup"><span data-stu-id="0f032-132">Use this file toospecify settings, such as connection strings tooother Azure services.</span></span> <span data-ttu-id="0f032-133">Aggiungere un nuovo toohello chiave **valori** matrice per ogni connessione richiesta dalle funzioni nel progetto.</span><span class="sxs-lookup"><span data-stu-id="0f032-133">Add a new key toohello **Values** array for each connection required by functions in your project.</span></span> <span data-ttu-id="0f032-134">Per ulteriori informazioni, vedere [file delle impostazioni locali](functions-run-local.md#local-settings-file) nell'argomento di strumenti di base di Azure funzioni hello.</span><span class="sxs-lookup"><span data-stu-id="0f032-134">For more information, see [Local settings file](functions-run-local.md#local-settings-file) in hello Azure Functions Core Tools topic.</span></span>

<span data-ttu-id="0f032-135">il runtime di funzioni Hello utilizza internamente un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f032-135">hello Functions runtime uses an Azure Storage account internally.</span></span> <span data-ttu-id="0f032-136">Per tutti i trigger, tipi diversi da HTTP e ai webhook, è necessario impostare hello **Values.AzureWebJobsStorage** tooa Azure Storage account stringa di connessione della chiave.</span><span class="sxs-lookup"><span data-stu-id="0f032-136">For all trigger types other than HTTP and webhooks, you must set hello **Values.AzureWebJobsStorage** key tooa valid Azure Storage account connection string.</span></span>

[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

 <span data-ttu-id="0f032-137">stringa di connessione account archiviazione hello tooset:</span><span class="sxs-lookup"><span data-stu-id="0f032-137">tooset hello storage account connection string:</span></span>

1. <span data-ttu-id="0f032-138">In Visual Studio, aprire **Cloud Explorer**, espandere **Account di archiviazione** > **Account di archiviazione**, quindi selezionare **proprietà**e hello copia **stringa di connessione primaria** valore.</span><span class="sxs-lookup"><span data-stu-id="0f032-138">In Visual Studio, open **Cloud Explorer**, expand **Storage Account** > **Your Storage Account**, then select **Properties** and copy hello **Primary Connection String** value.</span></span>   

2. <span data-ttu-id="0f032-139">Nel progetto, aprire il file di progetto local.settings.json hello e impostare il valore di hello di hello **AzureWebJobsStorage** chiave toohello stringa di connessione è stata copiata.</span><span class="sxs-lookup"><span data-stu-id="0f032-139">In your project, open hello local.settings.json project file and set hello value of hello **AzureWebJobsStorage** key toohello connection string you copied.</span></span>

3. <span data-ttu-id="0f032-140">Ripetere hello precedente passaggio tooadd chiavi univoche toohello **valori** matrice per le connessioni richiesto dalle funzioni.</span><span class="sxs-lookup"><span data-stu-id="0f032-140">Repeat hello previous step tooadd unique keys toohello **Values** array for any other connections required by your functions.</span></span>  

## <a name="create-a-function"></a><span data-ttu-id="0f032-141">Creare una funzione</span><span class="sxs-lookup"><span data-stu-id="0f032-141">Create a function</span></span>

<span data-ttu-id="0f032-142">Nelle funzioni di pre-compilate, le associazioni hello utilizzate dalla funzione hello sono definite applicando gli attributi nel codice hello.</span><span class="sxs-lookup"><span data-stu-id="0f032-142">In pre-compiled functions, hello bindings used by hello function are defined by applying attributes in hello code.</span></span> <span data-ttu-id="0f032-143">Quando si utilizzano toocreate strumenti di Azure funzioni hello delle funzioni dai modelli fornito hello, questi attributi vengono applicati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0f032-143">When you use hello Azure Functions Tools toocreate your functions from hello provided templates, these attributes are applied for you.</span></span> 

1. <span data-ttu-id="0f032-144">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo del progetto e scegliere **Aggiungi** > **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="0f032-144">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="0f032-145">Selezionare **funzione Azure**, digitare un **nome** classe hello e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0f032-145">Select **Azure Function**, type a **Name** for hello class, and click **Add**.</span></span>

2. <span data-ttu-id="0f032-146">Scegliere il trigger, impostare le proprietà di associazione di hello e fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="0f032-146">Choose your trigger, set hello binding properties, and click **Create**.</span></span> <span data-ttu-id="0f032-147">Hello riportato di seguito le impostazioni di hello all'attivazione della creazione di una coda di archiviazione (funzione).</span><span class="sxs-lookup"><span data-stu-id="0f032-147">hello following example shows hello settings when creating a Queue storage triggered function.</span></span> 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    <span data-ttu-id="0f032-148">Una chiave di stringa di connessione denominata **QueueStorage** viene fornito, che è definito nel file local.settings.json hello.</span><span class="sxs-lookup"><span data-stu-id="0f032-148">A connection string key named **QueueStorage** is supplied, which is defined in hello local.settings.json file.</span></span> 
 
3. <span data-ttu-id="0f032-149">Esaminare hello appena aggiunta classe.</span><span class="sxs-lookup"><span data-stu-id="0f032-149">Examine hello newly added class.</span></span> <span data-ttu-id="0f032-150">Viene visualizzato un valore statico **eseguire** (metodo), che è stato attribuito hello **FunctionName** attributo.</span><span class="sxs-lookup"><span data-stu-id="0f032-150">You see a static **Run** method, that is attributed with hello **FunctionName** attribute.</span></span> <span data-ttu-id="0f032-151">Questo attributo indica che il metodo hello è il punto di ingresso hello per la funzione hello.</span><span class="sxs-lookup"><span data-stu-id="0f032-151">This attribute indicates that hello method is hello entry point for hello function.</span></span> 

    <span data-ttu-id="0f032-152">Ad esempio, hello seguente classe c# rappresenta una funzione di archiviazione generato coda base:</span><span class="sxs-lookup"><span data-stu-id="0f032-152">For example, hello following C# class represents a basic Queue storage triggered function:</span></span>

    ````csharp
    using System;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Host;
    
    namespace FunctionApp1
    {
        public static class Function1
        {
            [FunctionName("QueueTriggerCSharp")]        
            public static void Run([QueueTrigger("myqueue-items", Connection = "QueueStorage")]string myQueueItem, TraceWriter log)
            {
                log.Info($"C# Queue trigger function processed: {myQueueItem}");
            }
        }
    } 
    ````
 
    <span data-ttu-id="0f032-153">Un attributo specifico di associazione è parametro specificato per l'associazione tooeach applicato toohello metodo punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="0f032-153">A binding-specific attribute is applied tooeach binding parameter supplied toohello entry point method.</span></span> <span data-ttu-id="0f032-154">l'attributo Hello accetta informazioni di associazione hello come parametri.</span><span class="sxs-lookup"><span data-stu-id="0f032-154">hello attribute takes hello binding information as parameters.</span></span> <span data-ttu-id="0f032-155">Nell'esempio precedente hello hello primo parametro è un **QueueTrigger** attributo applicato, che indica la funzione coda attivata.</span><span class="sxs-lookup"><span data-stu-id="0f032-155">In hello previous example, hello first parameter has a **QueueTrigger** attribute applied, indicating queue triggered function.</span></span> <span data-ttu-id="0f032-156">nome della coda Hello e nome di impostazione di stringa di connessione vengono passati come parametri.</span><span class="sxs-lookup"><span data-stu-id="0f032-156">hello queue name and connection string setting name are passed as parameters.</span></span>  

## <a name="testing-functions"></a><span data-ttu-id="0f032-157">Test delle funzioni</span><span class="sxs-lookup"><span data-stu-id="0f032-157">Testing functions</span></span>

<span data-ttu-id="0f032-158">Azure Functions Core Tools consente di eseguire il progetto Funzioni di Azure nel computer di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="0f032-158">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="0f032-159">Si è richiesta tooinstall questi strumenti hello primo avvio di una funzione da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f032-159">You are prompted tooinstall these tools hello first time you start a function from Visual Studio.</span></span>  

<span data-ttu-id="0f032-160">tootest della funzione, premere F5.</span><span class="sxs-lookup"><span data-stu-id="0f032-160">tootest your function, press F5.</span></span> <span data-ttu-id="0f032-161">Se richiesto, accettare la richiesta di hello da toodownload di Visual Studio e installare gli strumenti di Azure funzioni Core (CLI).</span><span class="sxs-lookup"><span data-stu-id="0f032-161">If prompted, accept hello request from Visual Studio toodownload and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="0f032-162">È necessario anche tooenable un'eccezione del firewall in modo che gli strumenti di hello possono gestire le richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="0f032-162">You may also need tooenable a firewall exception so that hello tools can handle HTTP requests.</span></span>

<span data-ttu-id="0f032-163">Con il progetto hello in esecuzione, è possibile testare il codice come si testa funzione distribuito.</span><span class="sxs-lookup"><span data-stu-id="0f032-163">With hello project running, you can test your code as you would test deployed function.</span></span> <span data-ttu-id="0f032-164">Per altre informazioni, vedere [Strategie per il test del codice in Funzioni di Azure](functions-test-a-function.md).</span><span class="sxs-lookup"><span data-stu-id="0f032-164">For more information, see [Strategies for testing your code in Azure Functions](functions-test-a-function.md).</span></span> <span data-ttu-id="0f032-165">Durante l'esecuzione in modalità di debug, i punti di interruzione vengono raggiunti in Visual Studio come previsto.</span><span class="sxs-lookup"><span data-stu-id="0f032-165">When running in debug mode, breakpoints are hit in Visual Studio as expected.</span></span> 

<span data-ttu-id="0f032-166">Per un esempio di come tootest una coda attivata (funzione), vedere hello [esercitazione di avvio rapido di coda attivata funzione](functions-create-storage-queue-triggered-function.md#test-the-function).</span><span class="sxs-lookup"><span data-stu-id="0f032-166">For an example of how tootest a queue triggered function, see hello [queue triggered function quickstart tutorial](functions-create-storage-queue-triggered-function.md#test-the-function).</span></span>  

<span data-ttu-id="0f032-167">toolearn ulteriori informazioni sull'utilizzo di strumenti di base di hello Azure funzioni, vedere [codice e il test funzioni di Azure localmente](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="0f032-167">toolearn more about using hello Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>

## <a name="publish-tooazure"></a><span data-ttu-id="0f032-168">Pubblicare tooAzure</span><span class="sxs-lookup"><span data-stu-id="0f032-168">Publish tooAzure</span></span>

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
><span data-ttu-id="0f032-169">Le impostazioni che è stato aggiunto in local.settings.json hello devono essere aggiunti anche toohello funzione app in Azure.</span><span class="sxs-lookup"><span data-stu-id="0f032-169">Any settings you added in hello local.settings.json must be also added toohello function app in Azure.</span></span> <span data-ttu-id="0f032-170">Queste impostazioni non vengono aggiunte automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0f032-170">These settings are not added automatically.</span></span> <span data-ttu-id="0f032-171">È possibile aggiungere le impostazioni necessarie tooyour funzione app in uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0f032-171">You can add required settings tooyour function app in one of these ways:</span></span>
>
>* <span data-ttu-id="0f032-172">[Tramite il portale di Azure di hello](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="0f032-172">[Using hello Azure portal](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>
>* <span data-ttu-id="0f032-173">[Utilizzo di hello `--publish-local-settings` opzione per la pubblicazione in strumenti di base di Azure funzioni hello](functions-run-local.md#publish).</span><span class="sxs-lookup"><span data-stu-id="0f032-173">[Using hello `--publish-local-settings` publish option in hello Azure Functions Core Tools](functions-run-local.md#publish).</span></span>
>* <span data-ttu-id="0f032-174">[Utilizzando hello Azure CLI](/cli/azure/functionapp/config/appsettings#set).</span><span class="sxs-lookup"><span data-stu-id="0f032-174">[Using hello Azure CLI](/cli/azure/functionapp/config/appsettings#set).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0f032-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0f032-175">Next steps</span></span>

<span data-ttu-id="0f032-176">Per ulteriori informazioni sugli strumenti di funzioni di Azure, vedere la sezione delle domande più comuni di hello di hello [strumenti di Visual Studio 2017 per le funzioni di Azure](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) post di blog.</span><span class="sxs-lookup"><span data-stu-id="0f032-176">For more information about Azure Functions Tools, see hello Common Questions section of hello [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blog post.</span></span>

<span data-ttu-id="0f032-177">toolearn informazioni su strumenti di base di hello Azure funzioni, vedere [codice e il test funzioni di Azure localmente](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="0f032-177">toolearn more about hello Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>  
<span data-ttu-id="0f032-178">toolearn più sullo sviluppo di funzioni come librerie di classi .NET, vedere [librerie di classi .NET utilizzando con le funzioni di Azure](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="0f032-178">toolearn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> <span data-ttu-id="0f032-179">Inoltre, in questo argomento fornisce esempi di come toouse attributi toodeclare hello vari tipi di associazioni supportate dalle funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f032-179">This topic also provides examples of how toouse attributes toodeclare hello various types of bindings supported by Azure Functions.</span></span>    

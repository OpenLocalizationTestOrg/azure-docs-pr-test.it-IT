---
title: Sviluppare Funzioni di Azure con Visual Studio | Microsoft Docs
description: Informazioni su come sviluppare e testare Funzioni di Azure usando Azure Functions Tools for Visual Studio 2017.
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
ms.openlocfilehash: 1e0568bc58e8879cabe409cf8e9b5866f922e7c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a><span data-ttu-id="db021-103">Azure Functions Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="db021-103">Azure Functions Tools for Visual Studio</span></span>  

<span data-ttu-id="db021-104">Azure Functions Tools for Visual Studio 2017 è un'estensione di Visual Studio che consente di sviluppare, testare e distribuire funzioni C# in Azure.</span><span class="sxs-lookup"><span data-stu-id="db021-104">Azure Functions Tools for Visual Studio 2017 is an extension for Visual Studio that lets you develop, test, and deploy C# functions to Azure.</span></span> <span data-ttu-id="db021-105">Se questa è la prima esperienza con Funzioni di Azure, è consigliabile leggere altre informazioni in [Introduzione a Funzioni di Azure](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="db021-105">If this is your first experience with Azure Functions, you can learn more at [An introduction to Azure Functions](functions-overview.md).</span></span>

<span data-ttu-id="db021-106">Azure Functions Tools offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="db021-106">The Azure Functions Tools provides the following benefits:</span></span> 

* <span data-ttu-id="db021-107">Modifica, compilazione ed esecuzione di funzioni nel computer di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="db021-107">Edit, build, and run functions on your local development computer.</span></span> 
* <span data-ttu-id="db021-108">Pubblicazione del proprio progetto di Funzioni di Azure direttamente in Azure.</span><span class="sxs-lookup"><span data-stu-id="db021-108">Publish your Azure Functions project directly to Azure.</span></span> 
* <span data-ttu-id="db021-109">Utilizzo di attributi di processi Web per dichiarare associazioni di funzione direttamente nel codice C# anziché mantenere un file function.json separato per le definizioni di associazione.</span><span class="sxs-lookup"><span data-stu-id="db021-109">Use WebJobs attributes to declare function bindings directly in the C# code instead of maintaining a separate function.json for binding definitions.</span></span>
* <span data-ttu-id="db021-110">Sviluppo e distribuzione di funzioni C# precompilate.</span><span class="sxs-lookup"><span data-stu-id="db021-110">Develop and deploy pre-compiled C# functions.</span></span> <span data-ttu-id="db021-111">Le funzioni precompilate offrono migliori prestazioni nell'avvio a freddo rispetto alle funzioni basate su script C#.</span><span class="sxs-lookup"><span data-stu-id="db021-111">Pre-complied functions provide a better cold-start performance than C# script-based functions.</span></span> 
* <span data-ttu-id="db021-112">Possibilità di scrivere il codice delle funzioni in C# sfruttando al contempo tutti i vantaggi dello sviluppo in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db021-112">Code your functions in C# while having all of the benefits of Visual Studio development.</span></span> 

<span data-ttu-id="db021-113">Questo argomento illustra come usare Azure Functions Tools for Visual Studio 2017 per sviluppare le funzioni in C#.</span><span class="sxs-lookup"><span data-stu-id="db021-113">This topic shows you how to use the Azure Functions Tools for Visual Studio 2017 to develop your functions in C#.</span></span> <span data-ttu-id="db021-114">Spiega anche come pubblicare il progetto in Azure come assembly .NET.</span><span class="sxs-lookup"><span data-stu-id="db021-114">You also learn how to publish your project to Azure as a .NET assembly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db021-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="db021-115">Prerequisites</span></span>

<span data-ttu-id="db021-116">Gli strumenti di Funzioni di Azure sono inclusi nel carico di lavoro di sviluppo di Azure in [Visual Studio 2017 15.3](https://www.visualstudio.com/vs/) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="db021-116">Azure Functions Tools is included in the Azure development workload of [Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/), or a later version.</span></span> <span data-ttu-id="db021-117">Assicurarsi di includere il carico di lavoro di **sviluppo di Azure** nell'installazione di Visual Studio 2017 versione 15.3:</span><span class="sxs-lookup"><span data-stu-id="db021-117">Make sure you include the **Azure development** workload in your Visual Studio 2017 version 15.3 installation:</span></span>

![Installare Visual Studio 2017 con il carico di lavoro Sviluppo di Azure](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

<span data-ttu-id="db021-119">Per creare e distribuire funzioni, è necessario disporre anche di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="db021-119">To create and deploy functions, you also need:</span></span>

* <span data-ttu-id="db021-120">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="db021-120">An active Azure subscription.</span></span> <span data-ttu-id="db021-121">Se non si possiede una sottoscrizione di Azure, sono disponibili [account gratuiti](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="db021-121">If you don't have an Azure subscription, [free accounts](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) are available.</span></span>

* <span data-ttu-id="db021-122">Un account dell'Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="db021-122">An Azure Storage account.</span></span> <span data-ttu-id="db021-123">Per creare un account di archiviazione, vedere [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="db021-123">To create a storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
## <a name="create-an-azure-functions-project"></a><span data-ttu-id="db021-124">Creare un progetto di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="db021-124">Create an Azure Functions project</span></span> 

[!INCLUDE [Create a project using the Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-the-project-for-local-development"></a><span data-ttu-id="db021-125">Configurare il progetto per lo sviluppo locale</span><span class="sxs-lookup"><span data-stu-id="db021-125">Configure the project for local development</span></span>

<span data-ttu-id="db021-126">Quando si crea un nuovo progetto usando il modello di Funzioni di Azure, si ottiene un progetto C# vuoto che contiene i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="db021-126">When you create a new project using the Azure Functions template, you get an empty C# project that contains the following files:</span></span>

* <span data-ttu-id="db021-127">**host.json**: consente di configurare l'host di Funzioni.</span><span class="sxs-lookup"><span data-stu-id="db021-127">**host.json**: Lets you configure the Functions host.</span></span> <span data-ttu-id="db021-128">Queste impostazioni si applicano sia durante l'esecuzione in locale che nell'esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="db021-128">These settings apply both when running locally and in Azure.</span></span> <span data-ttu-id="db021-129">Per altre informazioni, vedere l'articolo di riferimento su [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="db021-129">For more information, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) reference article.</span></span>
    
* <span data-ttu-id="db021-130">**local.settings.json**: mantiene le impostazioni usate quando si esegue Funzioni localmente.</span><span class="sxs-lookup"><span data-stu-id="db021-130">**local.settings.json**: Maintains settings used when running functions locally.</span></span> <span data-ttu-id="db021-131">Queste impostazioni non vengono usate da Azure, bensì dagli [strumenti di base di Funzioni di Azure](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="db021-131">These settings are not used by Azure, they are used by the [Azure Functions Core Tools](functions-run-local.md).</span></span> <span data-ttu-id="db021-132">Usare questo file per specificare le impostazioni, ad esempio le stringhe di connessione ad altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="db021-132">Use this file to specify settings, such as connection strings to other Azure services.</span></span> <span data-ttu-id="db021-133">Aggiungere una nuova chiave alla matrice di **Valori** per ogni connessione richiesta dalle funzioni nel progetto.</span><span class="sxs-lookup"><span data-stu-id="db021-133">Add a new key to the **Values** array for each connection required by functions in your project.</span></span> <span data-ttu-id="db021-134">Per altre informazioni, vedere [Local settings file](functions-run-local.md#local-settings-file) (File delle impostazioni locali) nell'argomento sugli strumenti di base di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="db021-134">For more information, see [Local settings file](functions-run-local.md#local-settings-file) in the Azure Functions Core Tools topic.</span></span>

<span data-ttu-id="db021-135">Il runtime di Funzioni usa un account di archiviazione di Azure internamente.</span><span class="sxs-lookup"><span data-stu-id="db021-135">The Functions runtime uses an Azure Storage account internally.</span></span> <span data-ttu-id="db021-136">Per tutti i tipi di trigger diversi da HTTP e dai webhook, è necessario impostare la chiave **Values.AzureWebJobsStorage** su una stringa di connessione di account di archiviazione di Azure valida.</span><span class="sxs-lookup"><span data-stu-id="db021-136">For all trigger types other than HTTP and webhooks, you must set the **Values.AzureWebJobsStorage** key to a valid Azure Storage account connection string.</span></span>

[!INCLUDE [Note to not use local storage](../../includes/functions-local-settings-note.md)]

 <span data-ttu-id="db021-137">Per impostare la stringa di connessione dell'account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="db021-137">To set the storage account connection string:</span></span>

1. <span data-ttu-id="db021-138">In Visual Studio aprire **Cloud Explorer**, espandere **Account di archiviazione** > **Your Storage Account** (Account di archiviazione personale), quindi selezionare **Proprietà** e copiare il valore **Stringa di connessione primaria**.</span><span class="sxs-lookup"><span data-stu-id="db021-138">In Visual Studio, open **Cloud Explorer**, expand **Storage Account** > **Your Storage Account**, then select **Properties** and copy the **Primary Connection String** value.</span></span>   

2. <span data-ttu-id="db021-139">Nel progetto aprire il file di progetto local.settings.json e impostare il valore della chiave **AzureWebJobsStorage** sulla stringa di connessione copiata.</span><span class="sxs-lookup"><span data-stu-id="db021-139">In your project, open the local.settings.json project file and set the value of the **AzureWebJobsStorage** key to the connection string you copied.</span></span>

3. <span data-ttu-id="db021-140">Ripetere il passaggio precedente per aggiungere chiavi univoche alla matrice di **Valori** per tutte le altre connessioni richieste dalle funzioni.</span><span class="sxs-lookup"><span data-stu-id="db021-140">Repeat the previous step to add unique keys to the **Values** array for any other connections required by your functions.</span></span>  

## <a name="create-a-function"></a><span data-ttu-id="db021-141">Creare una funzione</span><span class="sxs-lookup"><span data-stu-id="db021-141">Create a function</span></span>

<span data-ttu-id="db021-142">Nelle funzioni precompilate le associazioni usate dalla funzione sono definite tramite l'applicazione di attributi nel codice.</span><span class="sxs-lookup"><span data-stu-id="db021-142">In pre-compiled functions, the bindings used by the function are defined by applying attributes in the code.</span></span> <span data-ttu-id="db021-143">Quando si usa Azure Functions Tools per creare le funzioni dai modelli forniti, questi attributi vengono applicati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="db021-143">When you use the Azure Functions Tools to create your functions from the provided templates, these attributes are applied for you.</span></span> 

1. <span data-ttu-id="db021-144">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo del progetto e scegliere **Aggiungi** > **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="db021-144">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="db021-145">Selezionare **Funzione di Azure**, digitare un **Nome** per la classe e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="db021-145">Select **Azure Function**, type a **Name** for the class, and click **Add**.</span></span>

2. <span data-ttu-id="db021-146">Scegliere il trigger, impostare le proprietà di associazione e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="db021-146">Choose your trigger, set the binding properties, and click **Create**.</span></span> <span data-ttu-id="db021-147">L'esempio seguente mostra le impostazioni quando si crea una funzione attivata da un'archiviazione code.</span><span class="sxs-lookup"><span data-stu-id="db021-147">The following example shows the settings when creating a Queue storage triggered function.</span></span> 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    <span data-ttu-id="db021-148">Viene specificata una chiave di stringa di connessione denominata **QueueStorage**, che è definita nel file local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="db021-148">A connection string key named **QueueStorage** is supplied, which is defined in the local.settings.json file.</span></span> 
 
3. <span data-ttu-id="db021-149">Si esamini la classe appena aggiunta.</span><span class="sxs-lookup"><span data-stu-id="db021-149">Examine the newly added class.</span></span> <span data-ttu-id="db021-150">Si vede un metodo **Run** statico a cui è associato l'attributo **FunctionName**.</span><span class="sxs-lookup"><span data-stu-id="db021-150">You see a static **Run** method, that is attributed with the **FunctionName** attribute.</span></span> <span data-ttu-id="db021-151">Questo attributo indica che il metodo è il punto di ingresso per la funzione.</span><span class="sxs-lookup"><span data-stu-id="db021-151">This attribute indicates that the method is the entry point for the function.</span></span> 

    <span data-ttu-id="db021-152">La classe C# seguente rappresenta ad esempio una funzione di base attivata dall'archiviazione code:</span><span class="sxs-lookup"><span data-stu-id="db021-152">For example, the following C# class represents a basic Queue storage triggered function:</span></span>

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
 
    <span data-ttu-id="db021-153">Un attributo specifico dell'associazione viene applicato a ogni parametro di associazione fornito al metodo del punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="db021-153">A binding-specific attribute is applied to each binding parameter supplied to the entry point method.</span></span> <span data-ttu-id="db021-154">L'attributo accetta le informazioni di associazione come parametri.</span><span class="sxs-lookup"><span data-stu-id="db021-154">The attribute takes the binding information as parameters.</span></span> <span data-ttu-id="db021-155">Nell'esempio precedente il primo parametro dispone di un attributo **QueueTrigger**, che indica la funzione attivata dalla coda.</span><span class="sxs-lookup"><span data-stu-id="db021-155">In the previous example, The first parameter has a **QueueTrigger** attribute applied, indicating queue triggered function.</span></span> <span data-ttu-id="db021-156">Il nome della coda e il nome di impostazione della stringa di connessione vengono passati come parametri.</span><span class="sxs-lookup"><span data-stu-id="db021-156">The queue name and connection string setting name are passed as parameters.</span></span>  

## <a name="testing-functions"></a><span data-ttu-id="db021-157">Test delle funzioni</span><span class="sxs-lookup"><span data-stu-id="db021-157">Testing functions</span></span>

<span data-ttu-id="db021-158">Azure Functions Core Tools consente di eseguire il progetto Funzioni di Azure nel computer di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="db021-158">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="db021-159">Verrà richiesto di installare questi strumenti al primo avvio di una funzione da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db021-159">You are prompted to install these tools the first time you start a function from Visual Studio.</span></span>  

<span data-ttu-id="db021-160">Per testare la funzione premere F5.</span><span class="sxs-lookup"><span data-stu-id="db021-160">To test your function, press F5.</span></span> <span data-ttu-id="db021-161">Se viene visualizzata, accettare la richiesta di Visual Studio di scaricare e installare gli strumenti dell'interfaccia della riga di comando Azure Functions Core Tools.</span><span class="sxs-lookup"><span data-stu-id="db021-161">If prompted, accept the request from Visual Studio to download and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="db021-162">Potrebbe essere necessario anche abilitare un'eccezione del firewall per consentire agli strumenti di gestire le richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="db021-162">You may also need to enable a firewall exception so that the tools can handle HTTP requests.</span></span>

<span data-ttu-id="db021-163">Con il progetto in esecuzione, è possibile testare il codice come si fa con una funzione distribuita.</span><span class="sxs-lookup"><span data-stu-id="db021-163">With the project running, you can test your code as you would test deployed function.</span></span> <span data-ttu-id="db021-164">Per altre informazioni, vedere [Strategie per il test del codice in Funzioni di Azure](functions-test-a-function.md).</span><span class="sxs-lookup"><span data-stu-id="db021-164">For more information, see [Strategies for testing your code in Azure Functions](functions-test-a-function.md).</span></span> <span data-ttu-id="db021-165">Durante l'esecuzione in modalità di debug, i punti di interruzione vengono raggiunti in Visual Studio come previsto.</span><span class="sxs-lookup"><span data-stu-id="db021-165">When running in debug mode, breakpoints are hit in Visual Studio as expected.</span></span> 

<span data-ttu-id="db021-166">Per un esempio di come testare una funzione attivata da una coda, vedere l'[esercitazione di avvio rapido alle funzioni attivate da code](functions-create-storage-queue-triggered-function.md#test-the-function).</span><span class="sxs-lookup"><span data-stu-id="db021-166">For an example of how to test a queue triggered function, see the [queue triggered function quickstart tutorial](functions-create-storage-queue-triggered-function.md#test-the-function).</span></span>  

<span data-ttu-id="db021-167">Per altre informazioni sull'utilizzo degli strumenti di base di Funzioni di Azure, vedere [Come scrivere codice per le funzioni di Azure e testarle in locale](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="db021-167">To learn more about using the Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>

## <a name="publish-to-azure"></a><span data-ttu-id="db021-168">Pubblicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="db021-168">Publish to Azure</span></span>

[!INCLUDE [Publish the project to Azure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
><span data-ttu-id="db021-169">Le impostazioni aggiunte nel file local.settings.json devono essere aggiunte anche all'app per le funzioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="db021-169">Any settings you added in the local.settings.json must be also added to the function app in Azure.</span></span> <span data-ttu-id="db021-170">Queste impostazioni non vengono aggiunte automaticamente.</span><span class="sxs-lookup"><span data-stu-id="db021-170">These settings are not added automatically.</span></span> <span data-ttu-id="db021-171">È possibile aggiungere le impostazioni necessarie per l'app per le funzioni in uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="db021-171">You can add required settings to your function app in one of these ways:</span></span>
>
>* <span data-ttu-id="db021-172">[Uso del portale di Azure](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="db021-172">[Using the Azure portal](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>
>* <span data-ttu-id="db021-173">[Uso dell'opzione di pubblicazione `--publish-local-settings` negli strumenti principali di Funzioni di Azure](functions-run-local.md#publish).</span><span class="sxs-lookup"><span data-stu-id="db021-173">[Using the `--publish-local-settings` publish option in the Azure Functions Core Tools](functions-run-local.md#publish).</span></span>
>* <span data-ttu-id="db021-174">[Uso dell'interfaccia della riga di comando di Azure](/cli/azure/functionapp/config/appsettings#set).</span><span class="sxs-lookup"><span data-stu-id="db021-174">[Using the Azure CLI](/cli/azure/functionapp/config/appsettings#set).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="db021-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="db021-175">Next steps</span></span>

<span data-ttu-id="db021-176">Per altre informazioni su Azure Functions Tools, vedere la sezione Common Questions (Domande comuni) del post di blog [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="db021-176">For more information about Azure Functions Tools, see the Common Questions section of the [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blog post.</span></span>

<span data-ttu-id="db021-177">Per altre informazioni sull'utilizzo degli strumenti di base di Funzioni di Azure, vedere [Come scrivere codice per le funzioni di Azure e testarle in locale](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="db021-177">To learn more about the Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>  
<span data-ttu-id="db021-178">Per altre informazioni sullo sviluppo di funzioni quali le librerie della classe .NET, vedere [Uso di librerie di classi .NET con Funzioni di Azure](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="db021-178">To learn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> <span data-ttu-id="db021-179">Questo argomento fornisce anche esempi d'uso degli attributi per dichiarare i vari tipi di associazioni supportate da Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="db021-179">This topic also provides examples of how to use attributes to declare the various types of bindings supported by Azure Functions.</span></span>    

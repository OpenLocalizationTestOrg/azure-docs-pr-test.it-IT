---
title: Management .NET SDK per Analisi di flusso di Azure | Microsoft Docs
description: Introduzione a .NET SDK per la gestione di Analisi di flusso. Informazioni su come configurare ed eseguire i processi di analisi. Creare un progetto, input, output e trasformazioni.
keywords: .NET SDK, API di analisi
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5e93de87-0c6f-4f4b-be98-08d63f832897
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/06/2017
ms.author: jeffstok
ms.openlocfilehash: f9aa812e6e82cc0f72d0cd1fe63058e53f794775
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-the-azure-stream-analytics-api-for-net"></a><span data-ttu-id="8887e-106">Management .NET SDK: impostare ed eseguire processi di analisi tramite l'API di Analisi di flusso di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="8887e-106">Management .NET SDK: Set up and run analytics jobs using the Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="8887e-107">Informazioni su come impostare ed eseguire processi di analisi tramite l'API di Analisi di flusso per .NET usando Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="8887e-107">Learn how to set up and run analytics jobs using the Stream Analytics API for .NET using the Management .NET SDK.</span></span> <span data-ttu-id="8887e-108">Impostare un progetto, creare origini di input e output, trasformazioni e avviare e arrestare i processi.</span><span class="sxs-lookup"><span data-stu-id="8887e-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="8887e-109">Per i processi di analisi, è possibile trasmettere i dati di flusso dall'archiviazione BLOB o da un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="8887e-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="8887e-110">Vedere la [documentazione di riferimento sulla gestione per l'API di Analisi di flusso per .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="8887e-110">See the [management reference documentation for the Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="8887e-111">Analisi dei flussi di Azure è un servizio completamente gestito che consente l'elaborazione di eventi complessi con bassa latenza, elevata disponibilità e scalabilità per lo streaming di dati nel cloud.</span><span class="sxs-lookup"><span data-stu-id="8887e-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="8887e-112">Analisi di flusso consente ai clienti di configurare processi di flusso per analizzare i flussi di dati e di condurre operazioni di analisi pressoché in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="8887e-112">Stream Analytics enables customers to set up streaming jobs to analyze data streams, and allows them to drive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="8887e-113">Il codice di esempio in questo articolo è stato aggiornato con la versione v2.x .NET SDK per la gestione di Analisi di flusso di Azure.</span><span class="sxs-lookup"><span data-stu-id="8887e-113">We have updated the sample code in this article with Azure Stream Analytics Management .NET SDK v2.x version.</span></span> <span data-ttu-id="8887e-114">Per il codice di esempio che usa la versione legacy (1.x) SDK, vedere [Usare Management .NET SDK v1.x per Analisi di flusso](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span><span class="sxs-lookup"><span data-stu-id="8887e-114">For sample code using the uses lagecy (1.x) SDK version, please see [Use the Management .NET SDK v1.x for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8887e-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8887e-115">Prerequisites</span></span>
<span data-ttu-id="8887e-116">Per eseguire le procedure descritte nell'articolo è necessario:</span><span class="sxs-lookup"><span data-stu-id="8887e-116">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="8887e-117">Installare Visual Studio 2017 o 2015.</span><span class="sxs-lookup"><span data-stu-id="8887e-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="8887e-118">Scaricare e installare [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8887e-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="8887e-119">Creare un gruppo di risorse di Azure nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8887e-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="8887e-120">Di seguito è riportato un esempio di script di Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8887e-120">The following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="8887e-121">Per informazioni su Azure PowerShell , vedere [Installare e configurare Azure PowerShell](/powershell/azure/overview);</span><span class="sxs-lookup"><span data-stu-id="8887e-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in to your Azure account
        Add-AzureAccount

        # Select the Azure subscription you want to use to create the resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered to the subscription, remove the remark symbol (#) to run the Register-AzureRMProvider cmdlet to register the provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="8887e-122">Configurare un'origine di input e una destinazione di output da usare.</span><span class="sxs-lookup"><span data-stu-id="8887e-122">Set up an input source and output target to use.</span></span> <span data-ttu-id="8887e-123">Per altre istruzioni, vedere [Aggiungere input](stream-analytics-add-inputs.md) per impostare un esempio di input e [Aggiungere output](stream-analytics-add-outputs.md) per impostare un esempio di output.</span><span class="sxs-lookup"><span data-stu-id="8887e-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) to set up a sample input and [Add Outputs](stream-analytics-add-outputs.md) to set up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="8887e-124">Configurare un progetto</span><span class="sxs-lookup"><span data-stu-id="8887e-124">Set up a project</span></span>
<span data-ttu-id="8887e-125">Per creare un processo di analisi usando l'API di Analisi di flusso per .NET, configurare prima il progetto.</span><span class="sxs-lookup"><span data-stu-id="8887e-125">To create an analytics job use the Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="8887e-126">Creare un'applicazione console .NET di Visual Studio C#.</span><span class="sxs-lookup"><span data-stu-id="8887e-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="8887e-127">Nella Console di Gestione pacchetti, eseguire i comandi seguenti per installare i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="8887e-127">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="8887e-128">Il primo è l'SDK per .NET di Analisi di flusso di Azure.</span><span class="sxs-lookup"><span data-stu-id="8887e-128">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="8887e-129">Il secondo è per l'autenticazione del client di Azure.</span><span class="sxs-lookup"><span data-stu-id="8887e-129">The second one is for Azure client authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. <span data-ttu-id="8887e-130">Aggiungere la sezione **appSettings** seguente al file App.config:</span><span class="sxs-lookup"><span data-stu-id="8887e-130">Add the following **appSettings** section to the App.config file:</span></span>
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    <span data-ttu-id="8887e-131">Sostituire i valori per **SubscriptionId** e **ActiveDirectoryTenantId** con gli ID della sottoscrizione di Azure e del tenant.</span><span class="sxs-lookup"><span data-stu-id="8887e-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="8887e-132">È possibile ottenere questi valori eseguendo il cmdlet Azure PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="8887e-132">You can get these values by running the following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="8887e-133">Aggiungere il riferimento seguente nel file con estensione csproj:</span><span class="sxs-lookup"><span data-stu-id="8887e-133">Add the following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

5. <span data-ttu-id="8887e-134">Aggiungere le istruzioni **using** seguenti al file di origine (Program.cs) nel progetto.</span><span class="sxs-lookup"><span data-stu-id="8887e-134">Add the following **using** statements to the source file (Program.cs) in the project:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. <span data-ttu-id="8887e-135">Aggiungere un metodo helper di autenticazione:</span><span class="sxs-lookup"><span data-stu-id="8887e-135">Add an authentication helper method:</span></span>

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="8887e-136">Creare un client di gestione di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="8887e-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="8887e-137">Un oggetto **StreamAnalyticsManagementClient** consente di gestire il processo e i componenti di processo, ad esempio l'input, l'output e la trasformazione.</span><span class="sxs-lookup"><span data-stu-id="8887e-137">A **StreamAnalyticsManagementClient** object allows you to manage the job and the job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="8887e-138">Aggiungere il codice seguente all'inizio del metodo **Main** .</span><span class="sxs-lookup"><span data-stu-id="8887e-138">Add the following code to the beginning of the **Main** method:</span></span>

   ```
    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamingJobName = "<YOUR STREAMING JOB NAME>";
    string inputName = "<YOUR JOB INPUT NAME>";
    string transformationName = "<YOUR JOB TRANSFORMATION NAME>";
    string outputName = "<YOUR JOB OUTPUT NAME>";
    
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    
    // Get credentials
    ServiceClientCredentials credentials = GetCredentials().Result;
    
    // Create Stream Analytics management client
    StreamAnalyticsManagementClient streamAnalyticsManagementClient = new StreamAnalyticsManagementClient(credentials)
    {
        SubscriptionId = ConfigurationManager.AppSettings["SubscriptionId"]
    };
   ```

<span data-ttu-id="8887e-139">Il valore della variabile **resourceGroupName** deve essere lo stesso del nome del gruppo di risorse creato o selezionato nei passaggi preliminari.</span><span class="sxs-lookup"><span data-stu-id="8887e-139">The **resourceGroupName** variable's value should be the same as the name of the resource group you created or picked in the prerequisite steps.</span></span>

<span data-ttu-id="8887e-140">Per automatizzare l'aspetto di presentazione delle credenziali della creazione del processo, fare riferimento a [Autenticazione di un'entità servizio con Gestione risorse di Azure](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="8887e-140">To automate the credential presentation aspect of job creation, refer to [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="8887e-141">Nelle sezioni rimanenti di questo articolo si presuppone che il codice sia all'inizio del metodo **Main** .</span><span class="sxs-lookup"><span data-stu-id="8887e-141">The remaining sections of this article assume that this code is at the beginning of the **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="8887e-142">Creare un processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="8887e-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="8887e-143">Il codice seguente crea un processo di Analisi di flusso nel gruppo di risorse che è stato definito.</span><span class="sxs-lookup"><span data-stu-id="8887e-143">The following code creates a Stream Analytics job under the resource group that you have defined.</span></span> <span data-ttu-id="8887e-144">Verranno aggiunti un input, un output e la trasformazione al processo in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="8887e-144">You will add an input, output, and transformation to the job later.</span></span>

   ```
   // Create a streaming job
   StreamingJob streamingJob = new StreamingJob()
   {
       Tags = new Dictionary<string, string>()
       {
           { "Origin", ".NET SDK" },
           { "ReasonCreated", "Getting started tutorial" }
       },
       Location = "West US",
       EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Drop,
       EventsOutOfOrderMaxDelayInSeconds = 5,
       EventsLateArrivalMaxDelayInSeconds = 16,
       OutputErrorPolicy = OutputErrorPolicy.Drop,
       DataLocale = "en-US",
       CompatibilityLevel = CompatibilityLevel.OneFullStopZero,
       Sku = new Sku()
       {
           Name = SkuName.Standard
       }
   };
   StreamingJob createStreamingJobResult = streamAnalyticsManagementClient.StreamingJobs.CreateOrReplace(streamingJob, resourceGroupName, streamingJobName);
   ```

## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="8887e-145">Creare un'origine di input di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="8887e-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="8887e-146">Il codice seguente crea un'origine di input di Analisi di flusso con il tipo di origine di input BLOB e la serializzazione CSV.</span><span class="sxs-lookup"><span data-stu-id="8887e-146">The following code creates a Stream Analytics input source with the blob input source type and CSV serialization.</span></span> <span data-ttu-id="8887e-147">Per creare un'origine di input di hub eventi, usare **EventHubStreamInputDataSource** anziché **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="8887e-147">To create an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="8887e-148">Analogamente, è possibile personalizzare il tipo di serializzazione dell'origine di input.</span><span class="sxs-lookup"><span data-stu-id="8887e-148">Similarly, you can customize the serialization type of the input source.</span></span>

   ```
   // Create an input
   StorageAccount storageAccount = new StorageAccount()
   {
       AccountName = "<YOUR STORAGE ACCOUNT NAME>",
       AccountKey = "<YOUR STORAGE ACCOUNT KEY>"
   };
   Input input = new Input()
   {
       Properties = new StreamInputProperties()
       {
           Serialization = new CsvSerialization()
           {
               FieldDelimiter = ",",
               Encoding = Encoding.UTF8
           },
           Datasource = new BlobStreamInputDataSource()
           {
               StorageAccounts = new[] { storageAccount },
               Container = "<YOUR STORAGE BLOB CONTAINER>",
               PathPattern = "{date}/{time}",
               DateFormat = "yyyy/MM/dd",
               TimeFormat = "HH",
               SourcePartitionCount = 16
           }
       }
   };
   Input createInputResult = streamAnalyticsManagementClient.Inputs.CreateOrReplace(input, resourceGroupName, streamingJobName, inputName);
   ```

<span data-ttu-id="8887e-149">Le origini di input, dall'archiviazione BLOB o un hub eventi, sono legate a un processo specifico.</span><span class="sxs-lookup"><span data-stu-id="8887e-149">Input sources, whether from Blob storage or an event hub, are tied to a specific job.</span></span> <span data-ttu-id="8887e-150">Per usare la stessa origine di input per processi diversi, è necessario chiamare nuovamente il metodo e specificare un nome diverso.</span><span class="sxs-lookup"><span data-stu-id="8887e-150">To use the same input source for different jobs, you must call the method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="8887e-151">Testare un'origine di input di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="8887e-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="8887e-152">Il metodo **TestConnection** verifica se il processo di Analisi di flusso è in grado di connettersi all'origine di input, nonché altri aspetti specifici del tipo di origine di input.</span><span class="sxs-lookup"><span data-stu-id="8887e-152">The **TestConnection** method tests whether the Stream Analytics job is able to connect to the input source as well as other aspects specific to the input source type.</span></span> <span data-ttu-id="8887e-153">Ad esempio, nell'origine di input BLOB creata in precedenza, il metodo verifica che il nome dell'account di archiviazione e la coppia di chiavi possano essere usati per connettersi all'account di archiviazione, nonché verificare che il contenitore specificato esista.</span><span class="sxs-lookup"><span data-stu-id="8887e-153">For example, in the blob input source you created in an earlier step, the method will check that the Storage account name and key pair can be used to connect to the Storage account as well as check that the specified container exists.</span></span>

   ```
   // Test the connection to the input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="8887e-154">Creare una destinazione di output di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="8887e-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="8887e-155">La creazione di una destinazione di output è molto simile alla creazione di un'origine di input di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="8887e-155">Creating an output target is very similar to creating a Stream Analytics input source.</span></span> <span data-ttu-id="8887e-156">Analogamente alle origini di input, le destinazioni di output sono legate a un processo specifico.</span><span class="sxs-lookup"><span data-stu-id="8887e-156">Like input sources, output targets are tied to a specific job.</span></span> <span data-ttu-id="8887e-157">Per usare la stessa destinazione di output per processi diversi, è necessario chiamare nuovamente il metodo e specificare un nome diverso.</span><span class="sxs-lookup"><span data-stu-id="8887e-157">To use the same output target for different jobs, you must call the method again and specify a different job name.</span></span>

<span data-ttu-id="8887e-158">Il codice seguente crea una destinazione di output (database SQL di Azure).</span><span class="sxs-lookup"><span data-stu-id="8887e-158">The following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="8887e-159">È possibile personalizzare il tipo di dati della destinazione di output e/o il tipo di serializzazione.</span><span class="sxs-lookup"><span data-stu-id="8887e-159">You can customize the output target's data type and/or serialization type.</span></span>

   ```
   // Create an output
   Output output = new Output()
   {
       Datasource = new AzureSqlDatabaseOutputDataSource()
       {
           Server = "<YOUR DATABASE SERVER NAME>",
           Database = "<YOUR DATABASE NAME>",
           User = "<YOUR DATABASE LOGIN>",
           Password = "<YOUR DATABASE LOGIN PASSWORD>",
           Table = "<YOUR DATABASE TABLE NAME>"
       }
   };
   Output createOutputResult = streamAnalyticsManagementClient.Outputs.CreateOrReplace(output, resourceGroupName, streamingJobName, outputName);
   ```

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="8887e-160">Testare una destinazione di output di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="8887e-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="8887e-161">Una destinazione di output di Analisi di flusso dispone inoltre del metodo **TestConnection** per il test delle connessioni.</span><span class="sxs-lookup"><span data-stu-id="8887e-161">A Stream Analytics output target also has the **TestConnection** method for testing connections.</span></span>

   ```
   // Test the connection to the output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="8887e-162">Creare una trasformazione di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="8887e-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="8887e-163">Il codice seguente crea una trasformazione di Analisi di flusso con la query "select * from Input" e specifica l'assegnazione di un'unità di streaming per il processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="8887e-163">The following code creates a Stream Analytics transformation with the query "select * from Input" and specifies to allocate one streaming unit for the Stream Analytics job.</span></span> <span data-ttu-id="8887e-164">Per altre informazioni sulla regolazione di unità di streaming, vedere [Scalabilità dei processi di Analisi di flusso di Azure](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="8887e-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with the value you put for the 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

<span data-ttu-id="8887e-165">Analogamente all'input e all'output, una trasformazione è inoltre collegata a un processo di Analisi di flusso specifico in cui è stato creata.</span><span class="sxs-lookup"><span data-stu-id="8887e-165">Like input and output, a transformation is also tied to the specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="8887e-166">Avvio di un processo di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="8887e-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="8887e-167">Dopo aver creato un processo di Analisi di flusso nonché gli input, gli output e la trasformazione, è possibile avviare il processo chiamando il metodo **Start** .</span><span class="sxs-lookup"><span data-stu-id="8887e-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start the job by calling the **Start** method.</span></span>

<span data-ttu-id="8887e-168">Il codice di esempio seguente avvia un processo di Analisi di flusso con un'ora di inizio dell'output personalizzato impostata sulle 12:12:12 UTC del 12 dicembre 2012:</span><span class="sxs-lookup"><span data-stu-id="8887e-168">The following sample code starts a Stream Analytics job with a custom output start time set to December 12, 2012, 12:12:12 UTC:</span></span>

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="8887e-169">Arresto di un processo di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="8887e-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="8887e-170">È possibile arrestare un processo di Analisi di flusso in esecuzione chiamando il metodo **Stop** .</span><span class="sxs-lookup"><span data-stu-id="8887e-170">You can stop a running Stream Analytics job by calling the **Stop** method.</span></span>

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="8887e-171">Eliminazione di un processo di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="8887e-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="8887e-172">Il metodo **Delete** consente di eliminare il processo, nonché le risorse secondarie sottostanti, inclusi gli input, gli output e la trasformazione del processo.</span><span class="sxs-lookup"><span data-stu-id="8887e-172">The **Delete** method will delete the job as well as the underlying sub-resources, including input(s), output(s), and transformation of the job.</span></span>

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a><span data-ttu-id="8887e-173">Supporto</span><span class="sxs-lookup"><span data-stu-id="8887e-173">Get support</span></span>
<span data-ttu-id="8887e-174">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="8887e-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8887e-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8887e-175">Next steps</span></span>
<span data-ttu-id="8887e-176">Sono state fornite le nozioni di base dell'utilizzo di .NET SDK per creare ed eseguire i processi di analisi.</span><span class="sxs-lookup"><span data-stu-id="8887e-176">You've learned the basics of using a .NET SDK to create and run analytics jobs.</span></span> <span data-ttu-id="8887e-177">Per altre informazioni, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8887e-177">To learn more, see the following:</span></span>

* [<span data-ttu-id="8887e-178">Introduzione ad Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="8887e-178">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="8887e-179">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="8887e-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="8887e-180">Ridimensionare i processi di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="8887e-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="8887e-181">[.NET SDK per la gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="8887e-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="8887e-182">Informazioni di riferimento sul linguaggio di query di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="8887e-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="8887e-183">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="8887e-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->
[5]: ./media/markdown-template-for-new-articles/octocats.png
[6]: ./media/markdown-template-for-new-articles/pretty49.png
[7]: ./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[azure.blob.storage]: http://azure.microsoft.com/documentation/services/storage/
[azure.blob.storage.use]: http://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/

[azure.event.hubs]: http://azure.microsoft.com/services/event-hubs/
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.forum]: http://go.microsoft.com/fwlink/?LinkId=512151

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

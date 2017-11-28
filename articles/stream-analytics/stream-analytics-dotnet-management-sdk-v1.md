---
title: aaaManagement v1. x SDK .NET per Azure flusso Analitica | Documenti Microsoft
description: Introduzione a .NET SDK per la gestione di Analisi di flusso. Informazioni su come tooset backup ed eseguire i processi analitica. Creare un progetto, input, output e trasformazioni.
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
ms.openlocfilehash: d205c388880e3d9c2ca5df218f4b68abac8c9780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="management-net-sdk-v1x-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a><span data-ttu-id="0507f-106">Gestione .NET SDK v1. x: consente di impostare e i processi di esecuzione analitica mediante hello API Analitica flusso di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="0507f-106">Management .NET SDK v1.x: Set up and run analytics jobs using hello Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="0507f-107">Informazioni su come tooset backup e processi di esecuzione analitica tramite hello flusso Analitica API per l'utilizzo di .NET hello Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="0507f-107">Learn how tooset up and run analytics jobs using hello Stream Analytics API for .NET using hello Management .NET SDK.</span></span> <span data-ttu-id="0507f-108">Impostare un progetto, creare origini di input e output, trasformazioni e avviare e arrestare i processi.</span><span class="sxs-lookup"><span data-stu-id="0507f-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="0507f-109">Per i processi di analisi, è possibile trasmettere i dati di flusso dall'archiviazione BLOB o da un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="0507f-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="0507f-110">Vedere hello [documentazione di riferimento di gestione per hello flusso Analitica API per .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="0507f-110">See hello [management reference documentation for hello Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="0507f-111">Analitica di flusso di Azure è un servizio completamente gestito che fornisce l'elaborazione di eventi di bassa latenza, elevata disponibilità, scalabili e complesso nel flusso di dati nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="0507f-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="0507f-112">Flusso Analitica consente tooset clienti di flussi di dati tooanalyze i processi di flusso e consente loro toodrive quasi in tempo reale analitica.</span><span class="sxs-lookup"><span data-stu-id="0507f-112">Stream Analytics enables customers tooset up streaming jobs tooanalyze data streams, and allows them toodrive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="0507f-113">Il codice di esempio in questo articolo usa ancora la versione legacy (1. x) di .NET SDK per la gestione di Analisi di flusso di Azure.</span><span class="sxs-lookup"><span data-stu-id="0507f-113">Sample code in this article still uses legacy (1.x) version of Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="0507f-114">Per il codice di esempio con hello aggiornate SDK versione, vedere [hello utilizzare Gestione .NET SDK per Analitica flusso](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).</span><span class="sxs-lookup"><span data-stu-id="0507f-114">For sample code using hello up-to-date SDK version, please see [Use hello Management .NET SDK for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0507f-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0507f-115">Prerequisites</span></span>
<span data-ttu-id="0507f-116">Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="0507f-116">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="0507f-117">Installare Visual Studio 2017 o 2015.</span><span class="sxs-lookup"><span data-stu-id="0507f-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="0507f-118">Scaricare e installare [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0507f-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="0507f-119">Creare un gruppo di risorse di Azure nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0507f-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="0507f-120">Hello seguito è riportato un esempio di script di PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="0507f-120">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="0507f-121">Per informazioni su Azure PowerShell , vedere [Installare e configurare Azure PowerShell](/powershell/azure/overview);</span><span class="sxs-lookup"><span data-stu-id="0507f-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="0507f-122">Impostare un'origine di input e output toouse di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0507f-122">Set up an input source and output target toouse.</span></span> <span data-ttu-id="0507f-123">Per ulteriori istruzioni, vedere [aggiungere input](stream-analytics-add-inputs.md) tooset di un input di esempio e [Aggiungi output](stream-analytics-add-outputs.md) tooset di un esempio di output.</span><span class="sxs-lookup"><span data-stu-id="0507f-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) tooset up a sample input and [Add Outputs](stream-analytics-add-outputs.md) tooset up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="0507f-124">Configurare un progetto</span><span class="sxs-lookup"><span data-stu-id="0507f-124">Set up a project</span></span>
<span data-ttu-id="0507f-125">toocreate un processo analitica usare hello flusso Analitica API per .NET, impostare innanzitutto il progetto.</span><span class="sxs-lookup"><span data-stu-id="0507f-125">toocreate an analytics job use hello Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="0507f-126">Creare un'applicazione console .NET di Visual Studio C#.</span><span class="sxs-lookup"><span data-stu-id="0507f-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="0507f-127">Nella Console di gestione pacchetti hello, seguente hello esecuzione comandi tooinstall pacchetti di NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="0507f-127">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="0507f-128">Hello uno viene innanzitutto hello Azure flusso Analitica Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="0507f-128">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="0507f-129">Hello secondo è hello client di Azure Active Directory che verrà utilizzato per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="0507f-129">hello second one is hello Azure Active Directory client that will be used for authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 1.8.3
        Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.28.4
3. <span data-ttu-id="0507f-130">Aggiungere il seguente hello **appSettings** file app. config di toohello sezione:</span><span class="sxs-lookup"><span data-stu-id="0507f-130">Add hello following **appSettings** section toohello App.config file:</span></span>
   
        <appSettings>
          <!--CSM Prod related values-->
          <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
          <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
          <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
          <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION" />
          <add key="ActiveDirectoryTenantId" value="YOU TENANT ID" />
        </appSettings>

    <span data-ttu-id="0507f-131">Sostituire i valori per **SubscriptionId** e **ActiveDirectoryTenantId** con gli ID della sottoscrizione di Azure e del tenant.</span><span class="sxs-lookup"><span data-stu-id="0507f-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="0507f-132">È possibile ottenere questi valori eseguendo hello cmdlet di Azure PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="0507f-132">You can get these values by running hello following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="0507f-133">Aggiungere hello dopo un riferimento nel file con estensione csproj:</span><span class="sxs-lookup"><span data-stu-id="0507f-133">Add hello following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

1. <span data-ttu-id="0507f-134">Aggiungere il seguente hello **utilizzando** istruzioni toohello file di origine (Program.cs) nel progetto hello:</span><span class="sxs-lookup"><span data-stu-id="0507f-134">Add hello following **using** statements toohello source file (Program.cs) in hello project:</span></span>
   
        using System;
        using System.Configuration;
        using System.Threading.Tasks;
        
        using Microsoft.Azure;
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
2. <span data-ttu-id="0507f-135">Aggiungere un metodo helper di autenticazione:</span><span class="sxs-lookup"><span data-stu-id="0507f-135">Add an authentication helper method:</span></span>

   ```   
   private static async Task<string> GetAuthorizationHeader()
   {
       var context = new AuthenticationContext(
           ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
           ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);

        AuthenticationResult result = await context.AcquireTokenASync(
           resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
           clientId: ConfigurationManager.AppSettings["AsaClientId"],
           redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
           promptBehavior: PromptBehavior.Always);

        if (result != null)
            return result.AccessToken;

       throw new InvalidOperationException("Failed tooacquire token");
   }
   ```  

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="0507f-136">Creare un client di gestione di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="0507f-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="0507f-137">Oggetto **StreamAnalyticsManagementClient** oggetto consente di toomanage hello processo e hello processo componenti, ad esempio input, output e la trasformazione.</span><span class="sxs-lookup"><span data-stu-id="0507f-137">A **StreamAnalyticsManagementClient** object allows you toomanage hello job and hello job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="0507f-138">Aggiungere hello dopo l'inizio di toohello codice hello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="0507f-138">Add hello following code toohello beginning of hello **Main** method:</span></span>

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";
    string streamAnalyticsInputName = "<YOUR JOB INPUT NAME>";
    string streamAnalyticsOutputName = "<YOUR JOB OUTPUT NAME>";
    string streamAnalyticsTransformationName = "<YOUR JOB TRANSFORMATION NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
        ConfigurationManager.AppSettings["SubscriptionId"],
        GetAuthorizationHeader().Result);

    // Create Stream Analytics management client
    StreamAnalyticsManagementClient client = new StreamAnalyticsManagementClient(aadTokenCredentials);

<span data-ttu-id="0507f-139">Hello **resourceGroupName** il valore della variabile deve essere uguale al nome hello della risorsa hello gruppo creato o selezionati nei passaggi prerequisiti hello hello.</span><span class="sxs-lookup"><span data-stu-id="0507f-139">hello **resourceGroupName** variable's value should be hello same as hello name of hello resource group you created or picked in hello prerequisite steps.</span></span>

<span data-ttu-id="0507f-140">aspetto di presentazione tooautomate hello credenziale di creazione del processo, fare riferimento troppo[l'autenticazione di un'entità servizio con Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="0507f-140">tooautomate hello credential presentation aspect of job creation, refer too[Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="0507f-141">Hello nelle restanti sezioni di questo articolo si presuppongono che il codice sia all'inizio di hello di hello **Main** metodo.</span><span class="sxs-lookup"><span data-stu-id="0507f-141">hello remaining sections of this article assume that this code is at hello beginning of hello **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="0507f-142">Creare un processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="0507f-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="0507f-143">Hello codice seguente crea un processo di flusso Analitica nel gruppo di risorse hello che sono state definite.</span><span class="sxs-lookup"><span data-stu-id="0507f-143">hello following code creates a Stream Analytics job under hello resource group that you have defined.</span></span> <span data-ttu-id="0507f-144">Si aggiungerà un processo toohello input, output e la trasformazione in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="0507f-144">You will add an input, output, and transformation toohello job later.</span></span>

    // Create a Stream Analytics job
    JobCreateOrUpdateParameters jobCreateParameters = new JobCreateOrUpdateParameters()
    {
        Job = new Job()
        {
            Name = streamAnalyticsJobName,
            Location = "<LOCATION>",
            Properties = new JobProperties()
            {
                EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Adjust,
                Sku = new Sku()
                {
                    Name = "Standard"
                }
            }
        }
    };

    JobCreateOrUpdateResponse jobCreateResponse = client.StreamingJobs.CreateOrUpdate(resourceGroupName, jobCreateParameters);


## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="0507f-145">Creare un'origine di input di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="0507f-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="0507f-146">Hello codice seguente crea un'origine di input flusso Analitica con tipo di origine di input blob hello e serializzazione CSV.</span><span class="sxs-lookup"><span data-stu-id="0507f-146">hello following code creates a Stream Analytics input source with hello blob input source type and CSV serialization.</span></span> <span data-ttu-id="0507f-147">utilizzare un'origine di input hub eventi, toocreate **EventHubStreamInputDataSource** anziché **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="0507f-147">toocreate an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="0507f-148">Analogamente, è possibile personalizzare il tipo di serializzazione hello hello origine di input.</span><span class="sxs-lookup"><span data-stu-id="0507f-148">Similarly, you can customize hello serialization type of hello input source.</span></span>

    // Create a Stream Analytics input source
    InputCreateOrUpdateParameters jobInputCreateParameters = new InputCreateOrUpdateParameters()
    {
        Input = new Input()
        {
            Name = streamAnalyticsInputName,
            Properties = new StreamInputProperties()
            {
                Serialization = new CsvSerialization
                {
                    Properties = new CsvSerializationProperties
                    {
                        Encoding = "UTF8",
                        FieldDelimiter = ","
                    }
                },
                DataSource = new BlobStreamInputDataSource
                {
                    Properties = new BlobStreamInputDataSourceProperties
                    {
                        StorageAccounts = new StorageAccount[]
                        {
                            new StorageAccount()
                            {
                                AccountName = "<YOUR STORAGE ACCOUNT NAME>",
                                AccountKey = "<YOUR STORAGE ACCOUNT KEY>"
                            }
                        },
                        Container = "samples",
                        PathPattern = ""
                    }
                }
            }
        }
    };

    InputCreateOrUpdateResponse inputCreateResponse =
        client.Inputs.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, jobInputCreateParameters);

<span data-ttu-id="0507f-149">Origini di input, dall'archiviazione Blob o un hub di eventi sono collegati tooa specifico processo.</span><span class="sxs-lookup"><span data-stu-id="0507f-149">Input sources, whether from Blob storage or an event hub, are tied tooa specific job.</span></span> <span data-ttu-id="0507f-150">toouse hello stessa origine di input per diversi processi, è necessario chiamare nuovamente il metodo hello e specificare un nome di processo diverso.</span><span class="sxs-lookup"><span data-stu-id="0507f-150">toouse hello same input source for different jobs, you must call hello method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="0507f-151">Testare un'origine di input di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="0507f-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="0507f-152">Hello **TestConnection** metodo verifica se il processo di flusso Analitica hello è in grado di tooconnect toohello input origine, nonché altri toohello di aspetti specifici tipo di origine di input.</span><span class="sxs-lookup"><span data-stu-id="0507f-152">hello **TestConnection** method tests whether hello Stream Analytics job is able tooconnect toohello input source as well as other aspects specific toohello input source type.</span></span> <span data-ttu-id="0507f-153">Ad esempio, in hello origine di input blob creato in un passaggio precedente, il metodo hello verifica che nome account di archiviazione hello e coppia di chiavi possa essere utilizzati tooconnect toohello account di archiviazione, nonché verificare che il contenitore specificato hello esiste.</span><span class="sxs-lookup"><span data-stu-id="0507f-153">For example, in hello blob input source you created in an earlier step, hello method will check that hello Storage account name and key pair can be used tooconnect toohello Storage account as well as check that hello specified container exists.</span></span>

    // Test input source connection
    DataSourceTestConnectionResponse inputTestResponse =
        client.Inputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsInputName);

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="0507f-154">Creare una destinazione di output di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="0507f-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="0507f-155">Creazione di una destinazione di output è molto simile toocreating un'origine di input flusso Analitica.</span><span class="sxs-lookup"><span data-stu-id="0507f-155">Creating an output target is very similar toocreating a Stream Analytics input source.</span></span> <span data-ttu-id="0507f-156">Come origini di input, output destinazioni sono tooa legati specifico processo.</span><span class="sxs-lookup"><span data-stu-id="0507f-156">Like input sources, output targets are tied tooa specific job.</span></span> <span data-ttu-id="0507f-157">toouse hello stessa destinazione di output per i processi diversi, è necessario chiamare nuovamente il metodo hello e specificare un nome di processo diverso.</span><span class="sxs-lookup"><span data-stu-id="0507f-157">toouse hello same output target for different jobs, you must call hello method again and specify a different job name.</span></span>

<span data-ttu-id="0507f-158">Hello di codice seguente crea una destinazione di output (database SQL di Azure).</span><span class="sxs-lookup"><span data-stu-id="0507f-158">hello following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="0507f-159">È possibile personalizzare il tipo di dati della destinazione dell'output di hello e/o tipo di serializzazione.</span><span class="sxs-lookup"><span data-stu-id="0507f-159">You can customize hello output target's data type and/or serialization type.</span></span>

    // Create a Stream Analytics output target
    OutputCreateOrUpdateParameters jobOutputCreateParameters = new OutputCreateOrUpdateParameters()
    {
        Output = new Output()
        {
            Name = streamAnalyticsOutputName,
            Properties = new OutputProperties()
            {
                DataSource = new SqlAzureOutputDataSource()
                {
                    Properties = new SqlAzureOutputDataSourceProperties()
                    {
                        Server = "<YOUR DATABASE SERVER NAME>",
                        Database = "<YOUR DATABASE NAME>",
                        User = "<YOUR DATABASE LOGIN>",
                        Password = "<YOUR DATABASE LOGIN PASSWORD>",
                        Table = "<YOUR DATABASE TABLE NAME>"
                    }
                }
            }
        }
    };

    OutputCreateOrUpdateResponse outputCreateResponse =
        client.Outputs.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, jobOutputCreateParameters);

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="0507f-160">Testare una destinazione di output di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="0507f-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="0507f-161">Hello dispone di una destinazione di output flusso Analitica **TestConnection** metodo per testare le connessioni.</span><span class="sxs-lookup"><span data-stu-id="0507f-161">A Stream Analytics output target also has hello **TestConnection** method for testing connections.</span></span>

    // Test output target connection
    DataSourceTestConnectionResponse outputTestResponse =
        client.Outputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsOutputName);

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="0507f-162">Creare una trasformazione di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="0507f-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="0507f-163">Hello codice seguente crea una trasformazione flusso Analitica con query hello "Seleziona * da un Input" e specifica tooallocate un'unità di streaming per il processo di flusso Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="0507f-163">hello following code creates a Stream Analytics transformation with hello query "select * from Input" and specifies tooallocate one streaming unit for hello Stream Analytics job.</span></span> <span data-ttu-id="0507f-164">Per altre informazioni sulla regolazione di unità di streaming, vedere [Scalabilità dei processi di Analisi di flusso di Azure](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="0507f-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

    // Create a Stream Analytics transformation
    TransformationCreateOrUpdateParameters transformationCreateParameters = new TransformationCreateOrUpdateParameters()
    {
        Transformation = new Transformation()
        {
            Name = streamAnalyticsTransformationName,
            Properties = new TransformationProperties()
            {
                StreamingUnits = 1,
                Query = "select * from Input"
            }
        }
    };

    var transformationCreateResp =
        client.Transformations.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, transformationCreateParameters);

<span data-ttu-id="0507f-165">Come input e output, una trasformazione è anche toohello legati processo di flusso Analitica specifico che in cui è stato creato.</span><span class="sxs-lookup"><span data-stu-id="0507f-165">Like input and output, a transformation is also tied toohello specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="0507f-166">Avvio di un processo di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="0507f-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="0507f-167">Dopo aver creato un processo di flusso Analitica e la relativa uno o più input, output e trasformazione, è possibile avviare il processo di hello dal chiamante hello **avviare** metodo.</span><span class="sxs-lookup"><span data-stu-id="0507f-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start hello job by calling hello **Start** method.</span></span>

<span data-ttu-id="0507f-168">Hello codice di esempio seguente avvia un processo di flusso Analitica con un output personalizzato inizio ora set tooDecember 12, 2012, 12:12:12 UTC:</span><span class="sxs-lookup"><span data-stu-id="0507f-168">hello following sample code starts a Stream Analytics job with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC:</span></span>

    // Start a Stream Analytics job
    JobStartParameters jobStartParameters = new JobStartParameters
    {
        OutputStartMode = OutputStartMode.CustomTime,
        OutputStartTime = new DateTime(2012, 12, 12, 0, 0, 0, DateTimeKind.Utc)
    };

    LongRunningOperationResponse jobStartResponse = client.StreamingJobs.Start(resourceGroupName, streamAnalyticsJobName, jobStartParameters);

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="0507f-169">Arresto di un processo di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="0507f-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="0507f-170">È possibile arrestare un processo in esecuzione di flusso Analitica hello chiamante **arrestare** metodo.</span><span class="sxs-lookup"><span data-stu-id="0507f-170">You can stop a running Stream Analytics job by calling hello **Stop** method.</span></span>

    // Stop a Stream Analytics job
    LongRunningOperationResponse jobStopResponse = client.StreamingJobs.Stop(resourceGroupName, streamAnalyticsJobName);

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="0507f-171">Eliminazione di un processo di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="0507f-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="0507f-172">Hello **eliminare** metodo elimina il processo di hello nonché hello sottostante risorse secondario, inclusi uno o più input, output e la trasformazione del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="0507f-172">hello **Delete** method will delete hello job as well as hello underlying sub-resources, including input(s), output(s), and transformation of hello job.</span></span>

    // Delete a Stream Analytics job
    LongRunningOperationResponse jobDeleteResponse = client.StreamingJobs.Delete(resourceGroupName, streamAnalyticsJobName);

## <a name="get-support"></a><span data-ttu-id="0507f-173">Supporto</span><span class="sxs-lookup"><span data-stu-id="0507f-173">Get support</span></span>
<span data-ttu-id="0507f-174">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="0507f-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0507f-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0507f-175">Next steps</span></span>
<span data-ttu-id="0507f-176">Si è appreso hello nozioni di base dell'utilizzo di un toocreate .NET SDK ed eseguire i processi analitica.</span><span class="sxs-lookup"><span data-stu-id="0507f-176">You've learned hello basics of using a .NET SDK toocreate and run analytics jobs.</span></span> <span data-ttu-id="0507f-177">toolearn vedere, più hello informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0507f-177">toolearn more, see hello following:</span></span>

* [<span data-ttu-id="0507f-178">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="0507f-178">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="0507f-179">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="0507f-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="0507f-180">Ridimensionare i processi di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="0507f-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="0507f-181">[.NET SDK per la gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="0507f-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="0507f-182">Informazioni di riferimento sul linguaggio di query di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="0507f-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="0507f-183">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="0507f-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

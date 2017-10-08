---
title: i processi di monitoraggio aaaProgrammatically in flusso Analitica | Documenti Microsoft
description: Informazioni su come tooprogrammatically monitorare i processi di flusso Analitica creati tramite le API REST, Azure SDK o PowerShell.
keywords: monitoraggio .net, monitoraggio processi, monitoraggio app
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 2ec02cc9-4ca5-4a25-ae60-c44be9ad4835
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 44a9c29c2161ee81ea76ece4646a8691bf5d5b48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="e2600-104">Creare un monitoraggio dei processi di Analisi di flusso a livello di codice</span><span class="sxs-lookup"><span data-stu-id="e2600-104">Programmatically create a Stream Analytics job monitor</span></span>

<span data-ttu-id="e2600-105">In questo articolo viene illustrato come tooenable monitoraggio per un processo di flusso Analitica.</span><span class="sxs-lookup"><span data-stu-id="e2600-105">This article demonstrates how tooenable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="e2600-106">Per i processi di analisi di flusso creati tramite le API REST, Azure SDK o PowerShell, il monitoraggio non è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="e2600-106">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span></span> <span data-ttu-id="e2600-107">È possibile attivarlo manualmente nel portale di Azure hello visitando la pagina di monitoraggio del processo toohello e facendo clic su hello abilitare pulsante o è possibile automatizzare questo processo seguendo i passaggi di hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e2600-107">You can manually enable it in hello Azure portal by going toohello job’s Monitor page and clicking hello Enable button or you can automate this process by following hello steps in this article.</span></span> <span data-ttu-id="e2600-108">dati di monitoraggio Hello verrà visualizzata nell'area di metriche di hello del portale di Azure per il processo di flusso Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="e2600-108">hello monitoring data will show up in hello Metrics area of hello Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2600-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e2600-109">Prerequisites</span></span>

<span data-ttu-id="e2600-110">Prima di iniziare questo processo, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="e2600-110">Before you begin this process, you must have hello following:</span></span>

* <span data-ttu-id="e2600-111">Visual Studio 2017 o 2015</span><span class="sxs-lookup"><span data-stu-id="e2600-111">Visual Studio 2017 or 2015</span></span>
* <span data-ttu-id="e2600-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) scaricato e installato</span><span class="sxs-lookup"><span data-stu-id="e2600-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span></span>
* <span data-ttu-id="e2600-113">Un processo di flusso Analitica esistente che deve toohave monitoraggio abilitata</span><span class="sxs-lookup"><span data-stu-id="e2600-113">An existing Stream Analytics job that needs toohave monitoring enabled</span></span>

## <a name="create-a-project"></a><span data-ttu-id="e2600-114">Creare un progetto</span><span class="sxs-lookup"><span data-stu-id="e2600-114">Create a project</span></span>

1. <span data-ttu-id="e2600-115">Creare un'applicazione console .NET di Visual Studio C#.</span><span class="sxs-lookup"><span data-stu-id="e2600-115">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="e2600-116">Nella Console di gestione pacchetti hello, seguente hello esecuzione comandi tooinstall pacchetti di NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="e2600-116">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="e2600-117">Hello uno viene innanzitutto hello Azure flusso Analitica Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="e2600-117">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="e2600-118">Hello secondo è hello Azure SDK di monitoraggio che verrà utilizzato monitoraggio tooenable.</span><span class="sxs-lookup"><span data-stu-id="e2600-118">hello second one is hello Azure Monitor SDK that will be used tooenable monitoring.</span></span> <span data-ttu-id="e2600-119">Hello ultima uno è hello Azure Active Directory client che verrà utilizzato per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e2600-119">hello last one is hello Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="e2600-120">Aggiungere i seguenti file app. config toohello di sezione appSettings hello.</span><span class="sxs-lookup"><span data-stu-id="e2600-120">Add hello following appSettings section toohello App.config file.</span></span>
   
   ```
   <appSettings>
     <!--CSM Prod related values-->
     <add key="ResourceGroupName" value="RESOURCE GROUP NAME" />
     <add key="JobName" value="YOUR JOB NAME" />
     <add key="StorageAccountName" value="YOUR STORAGE ACCOUNT"/>
     <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
     <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
     <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
     <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
     <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
     <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION ID" />
     <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
   </appSettings>
   ```
   <span data-ttu-id="e2600-121">Sostituire i valori per *SubscriptionId* e *ActiveDirectoryTenantId* con gli ID della sottoscrizione di Azure e del tenant.</span><span class="sxs-lookup"><span data-stu-id="e2600-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="e2600-122">È possibile ottenere questi valori eseguendo hello cmdlet di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="e2600-122">You can get these values by running hello following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="e2600-123">Aggiungere il seguente hello utilizzando istruzioni toohello file di origine (Program.cs) nel progetto hello.</span><span class="sxs-lookup"><span data-stu-id="e2600-123">Add hello following using statements toohello source file (Program.cs) in hello project.</span></span>
   
   ```
     using System;
     using System.Configuration;
     using System.Threading;
     using Microsoft.Azure;
     using Microsoft.Azure.Management.Insights;
     using Microsoft.Azure.Management.Insights.Models;
     using Microsoft.Azure.Management.StreamAnalytics;
     using Microsoft.Azure.Management.StreamAnalytics.Models;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
   ```
5. <span data-ttu-id="e2600-124">Aggiungere un metodo helper di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e2600-124">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="e2600-125">public static string GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="e2600-125">public static string GetAuthorizationHeader()</span></span>
   
         {
             AuthenticationResult result = null;
             var thread = new Thread(() =>
             {
                 try
                 {
                     var context = new AuthenticationContext(
                         ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
                         ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
   
                     result = context.AcquireToken(
                         resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                         clientId: ConfigurationManager.AppSettings["AsaClientId"],
                         redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
                         promptBehavior: PromptBehavior.Always);
                 }
                 catch (Exception threadEx)
                 {
                     Console.WriteLine(threadEx.Message);
                 }
             });
   
             thread.SetApartmentState(ApartmentState.STA);
             thread.Name = "AcquireTokenThread";
             thread.Start();
             thread.Join();
   
             if (result != null)
             {
                 return result.AccessToken;
             }
   
             throw new InvalidOperationException("Failed tooacquire token");
     <span data-ttu-id="e2600-126">}</span><span class="sxs-lookup"><span data-stu-id="e2600-126">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="e2600-127">Creare i client di gestione</span><span class="sxs-lookup"><span data-stu-id="e2600-127">Create management clients</span></span>

<span data-ttu-id="e2600-128">Hello codice seguente imposterà le variabili necessarie hello e i client di gestione.</span><span class="sxs-lookup"><span data-stu-id="e2600-128">hello following code will set up hello necessary variables and management clients.</span></span>

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials =
        new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader());

    Uri resourceManagerUri = new
    Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    // Create Stream Analytics and Insights management client
    StreamAnalyticsManagementClient streamAnalyticsClient = new
    StreamAnalyticsManagementClient(aadTokenCredentials, resourceManagerUri);
    InsightsManagementClient insightsClient = new
    InsightsManagementClient(aadTokenCredentials, resourceManagerUri);

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="e2600-129">Abilitare il monitoraggio per un processo di analisi di flusso esistente</span><span class="sxs-lookup"><span data-stu-id="e2600-129">Enable monitoring for an existing Stream Analytics job</span></span>

<span data-ttu-id="e2600-130">esempio di codice seguente Hello consente il monitoraggio per un **esistente** processo flusso Analitica.</span><span class="sxs-lookup"><span data-stu-id="e2600-130">hello following code enables monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="e2600-131">prima parte di Hello del codice hello esegue una richiesta GET hello flusso Analitica servizio tooretrieve informazioni processo Analitica flusso specifico hello.</span><span class="sxs-lookup"><span data-stu-id="e2600-131">hello first part of hello code performs a GET request against hello Stream Analytics service tooretrieve information about hello particular Stream Analytics job.</span></span> <span data-ttu-id="e2600-132">Usa hello *Id* proprietà (recuperata da una richiesta GET hello) come parametro per il metodo Put in hello hello seconda metà del codice hello, che invia una richiesta PUT toohello Insights monitoraggio dei servizi tooenable per hello Analitica di flusso processo.</span><span class="sxs-lookup"><span data-stu-id="e2600-132">It uses hello *Id* property (retrieved from hello GET request) as a parameter for hello Put method in hello second half of hello code, which sends a PUT request toohello Insights service tooenable monitoring for hello Stream Analytics job.</span></span>

>[!WARNING]
><span data-ttu-id="e2600-133">Se è già stato attivato il monitoraggio per un diverso processo di flusso Analitica, tramite hello portale di Azure o a livello di codice con hello sotto il codice, **è consigliabile fornire hello stesso nome di account di archiviazione utilizzato quando si attivato il monitoraggio.**</span><span class="sxs-lookup"><span data-stu-id="e2600-133">If you have previously enabled monitoring for a different Stream Analytics job, either through hello Azure portal or programmatically via hello below code, **we recommend that you provide hello same storage account name that you used when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="e2600-134">account di archiviazione Hello è collegato toohello area creato il processo di flusso Analitica nel, in modo non specifico processo di toohello stesso.</span><span class="sxs-lookup"><span data-stu-id="e2600-134">hello storage account is linked toohello region that you created your Stream Analytics job in, not specifically toohello job itself.</span></span>
> 
> <span data-ttu-id="e2600-135">Analitica flusso tutti i processi (e tutte le altre risorse di Azure) nella stessa area condividono questa toostore di account di archiviazione dati di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="e2600-135">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account toostore monitoring data.</span></span> <span data-ttu-id="e2600-136">Se si specifica un account di archiviazione diverso, potrebbe verificarsi effetti collaterali imprevisti hello il monitoraggio di altri processi di flusso Analitica o altre risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2600-136">If you provide a different storage account, it might cause unintended side effects in hello monitoring of your other Stream Analytics jobs or other Azure resources.</span></span>
> 
> <span data-ttu-id="e2600-137">nome account di archiviazione Hello utilizzare tooreplace `<YOUR STORAGE ACCOUNT NAME>` nel seguente codice hello deve essere un account di archiviazione in hello processo flusso Analitica hello che si sta abilitando il monitoraggio per la stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="e2600-137">hello storage account name that you use tooreplace `<YOUR STORAGE ACCOUNT NAME>` in hello following code should be a storage account that is in hello same subscription as hello Stream Analytics job that you are enabling monitoring for.</span></span>
> 
> 

    // Get an existing Stream Analytics job
    JobGetParameters jobGetParameters = new JobGetParameters()
    {
        PropertiesToExpand = "inputs,transformation,outputs"
    };
    JobGetResponse jobGetResponse = streamAnalyticsClient.StreamingJobs.Get(resourceGroupName, streamAnalyticsJobName, jobGetParameters);

    // Enable monitoring
    ServiceDiagnosticSettingsPutParameters insightPutParameters = new ServiceDiagnosticSettingsPutParameters()
    {
            Properties = new ServiceDiagnosticSettings()
            {
                StorageAccountName = "<YOUR STORAGE ACCOUNT NAME>"
            }
    };
    insightsClient.ServiceDiagnosticSettingsOperations.Put(jobGetResponse.Job.Id, insightPutParameters);



## <a name="get-support"></a><span data-ttu-id="e2600-138">Supporto</span><span class="sxs-lookup"><span data-stu-id="e2600-138">Get support</span></span>

<span data-ttu-id="e2600-139">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="e2600-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2600-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e2600-140">Next steps</span></span>

* [<span data-ttu-id="e2600-141">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="e2600-141">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="e2600-142">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="e2600-142">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="e2600-143">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="e2600-143">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="e2600-144">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="e2600-144">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="e2600-145">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="e2600-145">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)


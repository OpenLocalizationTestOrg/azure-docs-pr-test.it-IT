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
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a>Creare un monitoraggio dei processi di Analisi di flusso a livello di codice

In questo articolo viene illustrato come tooenable monitoraggio per un processo di flusso Analitica. Per i processi di analisi di flusso creati tramite le API REST, Azure SDK o PowerShell, il monitoraggio non è abilitato per impostazione predefinita. È possibile attivarlo manualmente nel portale di Azure hello visitando la pagina di monitoraggio del processo toohello e facendo clic su hello abilitare pulsante o è possibile automatizzare questo processo seguendo i passaggi di hello in questo articolo. dati di monitoraggio Hello verrà visualizzata nell'area di metriche di hello del portale di Azure per il processo di flusso Analitica hello.

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare questo processo, è necessario disporre delle seguenti hello:

* Visual Studio 2017 o 2015
* [Azure .NET SDK](https://azure.microsoft.com/downloads/) scaricato e installato
* Un processo di flusso Analitica esistente che deve toohave monitoraggio abilitata

## <a name="create-a-project"></a>Creare un progetto

1. Creare un'applicazione console .NET di Visual Studio C#.
2. Nella Console di gestione pacchetti hello, seguente hello esecuzione comandi tooinstall pacchetti di NuGet hello. Hello uno viene innanzitutto hello Azure flusso Analitica Management .NET SDK. Hello secondo è hello Azure SDK di monitoraggio che verrà utilizzato monitoraggio tooenable. Hello ultima uno è hello Azure Active Directory client che verrà utilizzato per l'autenticazione.
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. Aggiungere i seguenti file app. config toohello di sezione appSettings hello.
   
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
   Sostituire i valori per *SubscriptionId* e *ActiveDirectoryTenantId* con gli ID della sottoscrizione di Azure e del tenant. È possibile ottenere questi valori eseguendo hello cmdlet di PowerShell seguente:
   
   ```
   Get-AzureAccount
   ```
4. Aggiungere il seguente hello utilizzando istruzioni toohello file di origine (Program.cs) nel progetto hello.
   
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
5. Aggiungere un metodo helper di autenticazione.
   
     public static string GetAuthorizationHeader()
   
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
     }

## <a name="create-management-clients"></a>Creare i client di gestione

Hello codice seguente imposterà le variabili necessarie hello e i client di gestione.

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

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a>Abilitare il monitoraggio per un processo di analisi di flusso esistente

esempio di codice seguente Hello consente il monitoraggio per un **esistente** processo flusso Analitica. prima parte di Hello del codice hello esegue una richiesta GET hello flusso Analitica servizio tooretrieve informazioni processo Analitica flusso specifico hello. Usa hello *Id* proprietà (recuperata da una richiesta GET hello) come parametro per il metodo Put in hello hello seconda metà del codice hello, che invia una richiesta PUT toohello Insights monitoraggio dei servizi tooenable per hello Analitica di flusso processo.

>[!WARNING]
>Se è già stato attivato il monitoraggio per un diverso processo di flusso Analitica, tramite hello portale di Azure o a livello di codice con hello sotto il codice, **è consigliabile fornire hello stesso nome di account di archiviazione utilizzato quando si attivato il monitoraggio.**
> 
> account di archiviazione Hello è collegato toohello area creato il processo di flusso Analitica nel, in modo non specifico processo di toohello stesso.
> 
> Analitica flusso tutti i processi (e tutte le altre risorse di Azure) nella stessa area condividono questa toostore di account di archiviazione dati di monitoraggio. Se si specifica un account di archiviazione diverso, potrebbe verificarsi effetti collaterali imprevisti hello il monitoraggio di altri processi di flusso Analitica o altre risorse di Azure.
> 
> nome account di archiviazione Hello utilizzare tooreplace `<YOUR STORAGE ACCOUNT NAME>` nel seguente codice hello deve essere un account di archiviazione in hello processo flusso Analitica hello che si sta abilitando il monitoraggio per la stessa sottoscrizione.
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



## <a name="get-support"></a>Supporto

Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passaggi successivi

* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)


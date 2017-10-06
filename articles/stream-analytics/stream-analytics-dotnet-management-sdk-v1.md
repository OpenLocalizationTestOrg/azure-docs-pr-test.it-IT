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
# <a name="management-net-sdk-v1x-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a>Gestione .NET SDK v1. x: consente di impostare e i processi di esecuzione analitica mediante hello API Analitica flusso di Azure per .NET
Informazioni su come tooset backup e processi di esecuzione analitica tramite hello flusso Analitica API per l'utilizzo di .NET hello Management .NET SDK. Impostare un progetto, creare origini di input e output, trasformazioni e avviare e arrestare i processi. Per i processi di analisi, è possibile trasmettere i dati di flusso dall'archiviazione BLOB o da un hub eventi.

Vedere hello [documentazione di riferimento di gestione per hello flusso Analitica API per .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).

Analitica di flusso di Azure è un servizio completamente gestito che fornisce l'elaborazione di eventi di bassa latenza, elevata disponibilità, scalabili e complesso nel flusso di dati nel cloud hello. Flusso Analitica consente tooset clienti di flussi di dati tooanalyze i processi di flusso e consente loro toodrive quasi in tempo reale analitica.  

> [!NOTE]
> Il codice di esempio in questo articolo usa ancora la versione legacy (1. x) di .NET SDK per la gestione di Analisi di flusso di Azure. Per il codice di esempio con hello aggiornate SDK versione, vedere [hello utilizzare Gestione .NET SDK per Analitica flusso](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:

* Installare Visual Studio 2017 o 2015.
* Scaricare e installare [Azure .NET SDK](https://azure.microsoft.com/downloads/).
* Creare un gruppo di risorse di Azure nella sottoscrizione. Hello seguito è riportato un esempio di script di PowerShell di Azure. Per informazioni su Azure PowerShell , vedere [Installare e configurare Azure PowerShell](/powershell/azure/overview);  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* Impostare un'origine di input e output toouse di destinazione. Per ulteriori istruzioni, vedere [aggiungere input](stream-analytics-add-inputs.md) tooset di un input di esempio e [Aggiungi output](stream-analytics-add-outputs.md) tooset di un esempio di output.

## <a name="set-up-a-project"></a>Configurare un progetto
toocreate un processo analitica usare hello flusso Analitica API per .NET, impostare innanzitutto il progetto.

1. Creare un'applicazione console .NET di Visual Studio C#.
2. Nella Console di gestione pacchetti hello, seguente hello esecuzione comandi tooinstall pacchetti di NuGet hello. Hello uno viene innanzitutto hello Azure flusso Analitica Management .NET SDK. Hello secondo è hello client di Azure Active Directory che verrà utilizzato per l'autenticazione.
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 1.8.3
        Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.28.4
3. Aggiungere il seguente hello **appSettings** file app. config di toohello sezione:
   
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

    Sostituire i valori per **SubscriptionId** e **ActiveDirectoryTenantId** con gli ID della sottoscrizione di Azure e del tenant. È possibile ottenere questi valori eseguendo hello cmdlet di Azure PowerShell seguente:

        Get-AzureAccount

4. Aggiungere hello dopo un riferimento nel file con estensione csproj:

        <Reference Include="System.Configuration" />

1. Aggiungere il seguente hello **utilizzando** istruzioni toohello file di origine (Program.cs) nel progetto hello:
   
        using System;
        using System.Configuration;
        using System.Threading.Tasks;
        
        using Microsoft.Azure;
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
2. Aggiungere un metodo helper di autenticazione:

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

## <a name="create-a-stream-analytics-management-client"></a>Creare un client di gestione di Analisi di flusso.
Oggetto **StreamAnalyticsManagementClient** oggetto consente di toomanage hello processo e hello processo componenti, ad esempio input, output e la trasformazione.

Aggiungere hello dopo l'inizio di toohello codice hello **Main** metodo:

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

Hello **resourceGroupName** il valore della variabile deve essere uguale al nome hello della risorsa hello gruppo creato o selezionati nei passaggi prerequisiti hello hello.

aspetto di presentazione tooautomate hello credenziale di creazione del processo, fare riferimento troppo[l'autenticazione di un'entità servizio con Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).

Hello nelle restanti sezioni di questo articolo si presuppongono che il codice sia all'inizio di hello di hello **Main** metodo.

## <a name="create-a-stream-analytics-job"></a>Creare un processo di Analisi di flusso.
Hello codice seguente crea un processo di flusso Analitica nel gruppo di risorse hello che sono state definite. Si aggiungerà un processo toohello input, output e la trasformazione in un secondo momento.

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


## <a name="create-a-stream-analytics-input-source"></a>Creare un'origine di input di Analisi di flusso.
Hello codice seguente crea un'origine di input flusso Analitica con tipo di origine di input blob hello e serializzazione CSV. utilizzare un'origine di input hub eventi, toocreate **EventHubStreamInputDataSource** anziché **BlobStreamInputDataSource**. Analogamente, è possibile personalizzare il tipo di serializzazione hello hello origine di input.

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

Origini di input, dall'archiviazione Blob o un hub di eventi sono collegati tooa specifico processo. toouse hello stessa origine di input per diversi processi, è necessario chiamare nuovamente il metodo hello e specificare un nome di processo diverso.

## <a name="test-a-stream-analytics-input-source"></a>Testare un'origine di input di Analisi di flusso
Hello **TestConnection** metodo verifica se il processo di flusso Analitica hello è in grado di tooconnect toohello input origine, nonché altri toohello di aspetti specifici tipo di origine di input. Ad esempio, in hello origine di input blob creato in un passaggio precedente, il metodo hello verifica che nome account di archiviazione hello e coppia di chiavi possa essere utilizzati tooconnect toohello account di archiviazione, nonché verificare che il contenitore specificato hello esiste.

    // Test input source connection
    DataSourceTestConnectionResponse inputTestResponse =
        client.Inputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsInputName);

## <a name="create-a-stream-analytics-output-target"></a>Creare una destinazione di output di Analisi di flusso
Creazione di una destinazione di output è molto simile toocreating un'origine di input flusso Analitica. Come origini di input, output destinazioni sono tooa legati specifico processo. toouse hello stessa destinazione di output per i processi diversi, è necessario chiamare nuovamente il metodo hello e specificare un nome di processo diverso.

Hello di codice seguente crea una destinazione di output (database SQL di Azure). È possibile personalizzare il tipo di dati della destinazione dell'output di hello e/o tipo di serializzazione.

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

## <a name="test-a-stream-analytics-output-target"></a>Testare una destinazione di output di Analisi di flusso
Hello dispone di una destinazione di output flusso Analitica **TestConnection** metodo per testare le connessioni.

    // Test output target connection
    DataSourceTestConnectionResponse outputTestResponse =
        client.Outputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsOutputName);

## <a name="create-a-stream-analytics-transformation"></a>Creare una trasformazione di Analisi di flusso
Hello codice seguente crea una trasformazione flusso Analitica con query hello "Seleziona * da un Input" e specifica tooallocate un'unità di streaming per il processo di flusso Analitica hello. Per altre informazioni sulla regolazione di unità di streaming, vedere [Scalabilità dei processi di Analisi di flusso di Azure](stream-analytics-scale-jobs.md).

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

Come input e output, una trasformazione è anche toohello legati processo di flusso Analitica specifico che in cui è stato creato.

## <a name="start-a-stream-analytics-job"></a>Avvio di un processo di Analisi di flusso
Dopo aver creato un processo di flusso Analitica e la relativa uno o più input, output e trasformazione, è possibile avviare il processo di hello dal chiamante hello **avviare** metodo.

Hello codice di esempio seguente avvia un processo di flusso Analitica con un output personalizzato inizio ora set tooDecember 12, 2012, 12:12:12 UTC:

    // Start a Stream Analytics job
    JobStartParameters jobStartParameters = new JobStartParameters
    {
        OutputStartMode = OutputStartMode.CustomTime,
        OutputStartTime = new DateTime(2012, 12, 12, 0, 0, 0, DateTimeKind.Utc)
    };

    LongRunningOperationResponse jobStartResponse = client.StreamingJobs.Start(resourceGroupName, streamAnalyticsJobName, jobStartParameters);

## <a name="stop-a-stream-analytics-job"></a>Arresto di un processo di Analisi di flusso
È possibile arrestare un processo in esecuzione di flusso Analitica hello chiamante **arrestare** metodo.

    // Stop a Stream Analytics job
    LongRunningOperationResponse jobStopResponse = client.StreamingJobs.Stop(resourceGroupName, streamAnalyticsJobName);

## <a name="delete-a-stream-analytics-job"></a>Eliminazione di un processo di Analisi di flusso
Hello **eliminare** metodo elimina il processo di hello nonché hello sottostante risorse secondario, inclusi uno o più input, output e la trasformazione del processo di hello.

    // Delete a Stream Analytics job
    LongRunningOperationResponse jobDeleteResponse = client.StreamingJobs.Delete(resourceGroupName, streamAnalyticsJobName);

## <a name="get-support"></a>Supporto
Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passaggi successivi
Si è appreso hello nozioni di base dell'utilizzo di un toocreate .NET SDK ed eseguire i processi analitica. toolearn vedere, più hello informazioni seguenti:

* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi di flusso di Azure](stream-analytics-scale-jobs.md)
* [.NET SDK per la gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn889315.aspx).
* [Informazioni di riferimento sul linguaggio di query di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

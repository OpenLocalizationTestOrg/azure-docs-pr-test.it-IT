---
title: pipeline di dati aaaCreate tramite Azure .NET SDK | Documenti Microsoft
description: Informazioni su come tooprogrammatically creare, monitorare e gestire data factory di Azure con Data Factory SDK.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a>Creazione, monitoraggio e gestione delle istanze di Azure Data Factory mediante Azure Data Factory .NET SDK
## <a name="overview"></a>Panoramica
È possibile creare, monitorare e gestire le istanze di Data factory di Azure a livello di codice mediante Data Factory .NET SDK. Questo articolo contiene una procedura dettagliata che è possibile seguire toocreate un'applicazione console .NET di esempio che crea e controlla una data factory. 

> [!NOTE]
> In questo articolo non copre tutti hello API .NET di Data Factory. Per la documentazione completa sull'API .NET per Data Factory, vedere [Informazioni di riferimento sull'API NET di Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1). 

## <a name="prerequisites"></a>Prerequisiti
* Visual Studio 2012 o 2013 o 2015
* Scaricare e installare [Azure .NET SDK](http://azure.microsoft.com/downloads/).
* Azure PowerShell. Seguire le istruzioni [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) articolo tooinstall Azure PowerShell nel computer in uso. Usare Azure PowerShell toocreate un'applicazione Azure Active Directory.

### <a name="create-an-application-in-azure-active-directory"></a>Creare un'applicazione in Azure Active Directory
Creare un'applicazione Azure Active Directory, creare un'entità servizio per un'applicazione hello e assegnarlo toohello **Data Factory collaboratore** ruolo.

1. Avviare **PowerShell**.
2. Eseguire hello comando seguente e immettere nome utente hello e la password usati toosign in toohello portale di Azure.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Eseguire hello successivo comando tooview tutte le sottoscrizioni di hello per questo account.

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. Sottoscrizione hello tooselect da toowork con il comando seguente hello esecuzione. Sostituire  **&lt;NameOfAzureSubscription** &gt; con nome hello della sottoscrizione Azure.

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > Prendere nota delle **SubscriptionId** e **TenantId** dall'output di hello del comando.

5. Creare un gruppo di risorse di Azure denominato **ADFTutorialResourceGroup** eseguendo hello comando in hello PowerShell seguente.

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    Se il gruppo di risorse hello esiste già, specificare se tooupdate è (Y) o mantenerlo come (N).

    Se si utilizza un gruppo di risorse diverso, è necessario il nome hello toouse del gruppo di risorse al posto di ADFTutorialResourceGroup in questa esercitazione.
6. Creare un'applicazione Azure Active Directory.

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    Se viene visualizzato il seguente errore hello, specificare un URL diverso ed eseguire nuovamente il comando di hello.
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. Creare hello dell'entità servizio Active Directory.

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. Aggiungere servizio principale toohello **Data Factory collaboratore** ruolo.

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. Ottieni ID applicazione hello

    ```PowerShell
    $azureAdApplication 
    ```
    Annotare l'ID dell'applicazione hello (applicationID) dall'output di hello.

Da questi passaggi si avranno i quattro valori seguenti:

* ID tenant
* ID sottoscrizione
* ID applicazione
* Password (specificata nel primo comando hello)

## <a name="walkthrough"></a>Procedura dettagliata
In questa procedura dettagliata hello, creare una data factory con una pipeline che contiene un'attività di copia. attività di copia Hello copia dati da una cartella nella cartella tooanother di archiviazione blob di Azure in hello stesso nell'archiviazione blob. 

Attività di copia Hello esegue lo spostamento dei dati di hello in Azure Data Factory. attività Hello è alimentato da un servizio disponibile a livello globale che è possibile copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile. Vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo per informazioni dettagliate sulle attività di copia hello.

1. Creare un'applicazione console .NET in C# con Visual Studio 2012, 2013 o 2015.
   1. Avviare **Visual Studio** 2012, 2013 o 2015.
   2. Fare clic su **File**, punto troppo**New**, fare clic su **progetto**.
   3. Espandere **Modelli** e quindi selezionare **Visual C#**. In questa procedura dettagliata viene usato C#, ma è possibile usare qualsiasi linguaggio .NET.
   4. Selezionare **applicazione Console** dall'elenco di hello dei tipi di progetto su hello destra.
   5. Immettere **DataFactoryAPITestApp** per hello Name.
   6. Selezionare **C:\ADFGetStarted** per hello percorso.
   7. Fare clic su **OK** progetto hello toocreate.
2. Fare clic su **strumenti**, punto troppo**Gestione pacchetti NuGet**, fare clic su **Package Manager Console**.
3. In hello **Package Manager Console**, hello i passaggi seguenti:
   1. Eseguire hello pacchetto Data Factory tooinstall di comando seguente:`Install-Package Microsoft.Azure.Management.DataFactories`
   2. Eseguire hello seguente pacchetto di Azure Active Directory tooinstall comando (utilizzare API di Active Directory nel codice hello):`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`
4. Sostituire il contenuto di hello di **app** file nel progetto hello con hello seguente contenuto: 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. Nel file app. config hello, aggiornare i valori per  **&lt;ID applicazione&gt;**,  **&lt;Password&gt;**,  **&lt; ID sottoscrizione&gt;**, e  **&lt;ID tenant&gt;**  con valori personalizzati.
6. Aggiungere il seguente hello **utilizzando** istruzioni toohello **Program.cs** file nel progetto hello.

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```
6. Aggiungere hello dopo il codice che crea un'istanza di **DataPipelineManagementClient** classe toohello **Main** metodo. Utilizzare questo toocreate oggetto una data factory, un servizio collegato, i set di dati di input e output e una pipeline. È inoltre possibile utilizzare le sezioni di toomonitor questo oggetto di un set di dati in fase di esecuzione.

    ```csharp
    // create data factory management client

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > Sostituire il valore di hello di **resourceGroupName** con il nome di hello del gruppo di risorse di Azure. È possibile creare un gruppo di risorse utilizzando hello [New AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.
   >
   > Aggiorna nome di hello toobe factory (dataFactoryName) di dati univoco. Nome della data factory di hello deve essere globalmente univoco. Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .
7. Aggiungere hello dopo il codice che crea un **data factory di** toohello **Main** metodo.

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```
8. Aggiungere hello dopo il codice che crea un **servizio collegato di archiviazione di Azure** toohello **Main** metodo.

   > [!IMPORTANT]
   > Sostituire **storageaccountname** e **accountkey** con il nome e la chiave dell'account di archiviazione di Azure.

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```
9. Aggiungere hello dopo il codice che crea **set di dati di input e output** toohello **Main** metodo.

    Hello **FolderPath** per blob di input hello è troppo**adftutorial /** in **adftutorial** hello nome del contenitore di hello nell'archiviazione blob. Se questo contenitore non esiste nell'archiviazione blob di Azure, creare un contenitore con lo stesso nome: **adftutorial** e caricare un contenitore di toohello file di testo.

    output di Hello FolderPath per hello blob è impostato su: **adftutorial/apifactoryoutput / {Slice}** in **sezione** è calcolato in modo dinamico hello in base a valore di **SliceStart**(avvio di data e ora di ogni sezione).

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
    
                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
                },
    
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
            }
        }
    });
    ```
10. Aggiunta di codice seguente hello che **viene creato e attivato una pipeline** toohello **Main** metodo. Questa pipeline contiene una proprietà **CopyActivity** che accetta **BlobSource** come origine e **BlobSink** come sink.

    Attività di copia Hello esegue lo spostamento dei dati di hello in Azure Data Factory. attività Hello è alimentato da un servizio disponibile a livello globale che è possibile copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile. Vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo per informazioni dettagliate sulle attività di copia hello.

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new PipelineCreateOrUpdateParameters()
    {
        Pipeline = new Pipeline()
        {
            Name = PipelineName,
            Properties = new PipelineProperties()
            {
                Description = "Demo Pipeline for data transfer between blobs",
    
                // Initial value for pipeline's active period. With this, you won't need tooset slice status
                Start = PipelineActivePeriodStartTime,
                End = PipelineActivePeriodEndTime,
    
                Activities = new List<Activity>()
                {
                    new Activity()
                    {
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
                                Name = Dataset_Source
                            }
                        },
                        Outputs = new List<ActivityOutput>()
                        {
                            new ActivityOutput()
                            {
                                Name = Dataset_Destination
                            }
                        },
                        TypeProperties = new CopyActivity()
                        {
                            Source = new BlobSource(),
                            Sink = new BlobSink()
                            {
                                WriteBatchSize = 10000,
                                WriteBatchTimeout = TimeSpan.FromMinutes(10)
                            }
                        }
                    }
    
                },
            }
        }
    });
    ```
12. Aggiungere i seguenti toohello codice hello **Main** metodo tooget hello stato una sezione di dati di hello set di dati di output. In questo esempio è prevista solo una sezione.

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");
        // wait before hello next status check
        Thread.Sleep(1000 * 12);
    
        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });
    
        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```
13. **(facoltativo)**  Tooget eseguire dettagli per un toohello porzioni di dati di codice seguente di hello di Aggiungi **Main** metodo.

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();
    
    var datasliceRunListResponse = client.DataSliceRuns.List(
        resourceGroupName,
        dataFactoryName,
        Dataset_Destination,
        new DataSliceRunListParameters()
        {
            DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
        });
    
    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }
    
    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```
14. Aggiungere hello seguente metodo helper utilizzato dal hello **Main** metodo toohello **programma** classe. Questo metodo viene visualizzata una finestra di dialogo che consente di fornire **nome utente** e **password** utilizzare toolog nel portale tooAzure.

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed tooacquire token");
    }
    ```

15. In Esplora soluzioni hello, espandere il progetto di hello: **DataFactoryAPITestApp**, fare doppio clic su **riferimenti**, fare clic su **Aggiungi riferimento**. Selezionare la casella di controllo per l'assembly `System.Configuration` e fare clic su **OK**.
15. Compilare un'applicazione console hello. Fare clic su **compilare** menu hello e fare clic su **Compila soluzione**.
16. Verificare che esista almeno un file nel contenitore adftutorial hello nell'archiviazione blob di Azure. In caso contrario, creare file Emp.txt nel blocco note con hello seguente contenuto e caricarlo toohello adftutorial contenitore.

    ```
    John, Doe
    Jane, Doe
    ```
17. Eseguire l'esempio hello facendo **Debug** -> **Avvia debug** menu hello. Quando viene visualizzato hello **dettagli di una sezione di dati di esecuzione**, attendere qualche minuto e premere **invio**.
18. Utilizzare hello tooverify portale Azure data factory di tale hello **APITutorialFactory** viene creato con hello seguenti elementi:
    * Servizio collegato: **AzureStorageLinkedService**
    * Set di dati: **DatasetBlobSource** e **DatasetBlobDestination**.
    * Pipeline: **PipelineBlobSample**
19. Verificare che un file di output venga creato in hello **apifactoryoutput** cartella hello **adftutorial** contenitore.

## <a name="get-a-list-of-failed-data-slices"></a>Ottenere un elenco di sezioni di dati non riusciti 

```csharp
// Parse hello resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a>Passaggi successivi
Vedere hello di esempio per la creazione di una pipeline mediante .NET SDK che copia i dati da un database di SQL Azure tooan di archiviazione blob di Azure seguente: 

- [Creare una pipeline di dati toocopy da archiviazione Blob tooSQL Database](data-factory-copy-activity-tutorial-using-dotnet-api.md)

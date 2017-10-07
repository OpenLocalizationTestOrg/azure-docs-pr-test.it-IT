---
title: "Asset aaaManaging e le relative entità con Media Services .NET SDK"
description: "Informazioni su come asset toomanage e le entità correlate con hello Media Services SDK per .NET."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1bd8fd42-7306-463d-bfe5-f642802f1906
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: 59a8543ffc6f7f30da2c67a6fcae09bc46da7a52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a>Gestione di asset ed entità correlate con Media Services .NET SDK
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-manage-entities.md)
> * [REST](media-services-rest-manage-entities.md)
> 
> 

In questo argomento viene illustrata la modalità di servizi multimediali di Azure di toomanage entità con .NET. 

>[!NOTE]
> A partire dal 1 aprile 2017, qualsiasi record di processo più vecchi di 90 giorni account vengono eliminate automaticamente, insieme ai relativi record di attività associato, anche se il numero di record hello sotto la quota massima di hello. Ad esempio, il 1° aprile 2017 qualsiasi record di processo nell'account precedente il 31 dicembre 2016 verrà automaticamente eliminato. Se sono necessarie informazioni di processi/attività hello tooarchive, è possibile utilizzare codice hello descritte in questo argomento.

## <a name="prerequisites"></a>Prerequisiti

Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md). 

## <a name="get-an-asset-reference"></a>Ottenere un riferimento a un asset
Un'attività comune consiste tooget un asset esistente tooan di riferimento in servizi multimediali. Hello esempio di codice seguente viene illustrato come ottenere un riferimento a un asset dalla raccolta di risorse hello in server hello oggetto di contesto, in base a un hello ID asset seguente codice viene illustrato come utilizzare una query Linq tooget tooan esistente IAsset oggetto di riferimento.

    static IAsset GetAsset(string assetId)
    {
        // Use a LINQ Select query tooget an asset.
        var assetInstance =
            from a in _context.Assets
            where a.Id == assetId
            select a;
        // Reference hello asset as an IAsset.
        IAsset asset = assetInstance.FirstOrDefault();

        return asset;
    }

## <a name="list-all-assets"></a>Elencare tutti gli asset
Man mano che aumenta il numero di hello degli asset nel servizio di archiviazione, è utile toolist le risorse. Hello esempio di codice seguente viene illustrato come tooiterate tramite hello raccolta di risorse dell'oggetto di contesto server hello. Con ogni asset, esempio di codice hello scrive inoltre alcune delle relative console toohello valori di proprietà. Ogni asset, ad esempio, può includere numerosi file multimediali. esempio di codice Hello scrive tutti i file associati a ogni asset.

    static void ListAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IAsset asset in _context.Assets)
        {
            // Display hello collection of assets.
            builder.AppendLine("");
            builder.AppendLine("******ASSET******");
            builder.AppendLine("Asset ID: " + asset.Id);
            builder.AppendLine("Name: " + asset.Name);
            builder.AppendLine("==============");
            builder.AppendLine("******ASSET FILES******");

            // Display hello files associated with each asset. 
            foreach (IAssetFile fileItem in asset.AssetFiles)
            {
                builder.AppendLine("Name: " + fileItem.Name);
                builder.AppendLine("Size: " + fileItem.ContentFileSize);
                builder.AppendLine("==============");
            }
        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="get-a-job-reference"></a>Ottenere un riferimento a un processo

Quando si lavora con l'elaborazione delle attività nel codice di servizi multimediali, è spesso necessario tooget un processo esistente tooan riferimento in base a un hello ID. esempio di codice seguente viene illustrato come tooget tooan un riferimento IJob oggetto dalla raccolta di processi hello.

Potrebbe necessario tooget riferimento a un processo quando si avvia un processo di codifica di lunga durata e lo stato del processo hello toocheck su un thread necessario. In casi come questo, quando il metodo hello viene restituito da un thread, è necessario un processo di riferimento aggiornato tooa tooretrieve.

    static IJob GetJob(string jobId)
    {
        // Use a Linq select query tooget an updated 
        // reference by Id. 
        var jobInstance =
            from j in _context.Jobs
            where j.Id == jobId
            select j;
        // Return hello job reference as an Ijob. 
        IJob job = jobInstance.FirstOrDefault();

        return job;
    }

## <a name="list-jobs-and-assets"></a>Elencare i processi e gli asset
Un'importante attività correlata è asset toolist con il relativo processo associato in servizi multimediali. Hello esempio di codice seguente illustra come toolist ogni oggetto IJob, per ogni processo, viene quindi visualizzato processo hello, tutte le attività correlate, asset di input tutte le proprietà e tutti gli asset di output. in questo esempio di codice Hello può essere utile per molte altre attività. Ad esempio, se si desidera asset di output di hello toolist da uno o più processi di codifica eseguiti in precedenza, questo codice viene illustrato come hello tooaccess gli asset di output. Quando si dispone di un asset di output tooan di riferimento, è quindi possibile recapitare hello tooother contenuto utenti o applicazioni scaricandolo o specificando gli URL. 

Per ulteriori informazioni sulle opzioni per la distribuzione degli asset, vedere [distribuzione di asset con Media Services SDK per .NET hello](media-services-deliver-streaming-content.md).

    // List all jobs on hello server, and for each job, also list 
    // all tasks, all input assets, all output assets.

    static void ListJobsAndAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IJob job in _context.Jobs)
        {
            // Display hello collection of jobs on hello server.
            builder.AppendLine("");
            builder.AppendLine("******JOB*******");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Name: " + job.Name);
            builder.AppendLine("State: " + job.State);
            builder.AppendLine("Order: " + job.Priority);
            builder.AppendLine("==============");


            // For each job, display hello associated tasks (a job  
            // has one or more tasks). 
            builder.AppendLine("******TASKS*******");
            foreach (ITask task in job.Tasks)
            {
                builder.AppendLine("Task Id: " + task.Id);
                builder.AppendLine("Name: " + task.Name);
                builder.AppendLine("Progress: " + task.Progress);
                builder.AppendLine("Configuration: " + task.Configuration);
                if (task.ErrorDetails != null)
                {
                    builder.AppendLine("Error: " + task.ErrorDetails);
                }
                builder.AppendLine("==============");
            }

            // For each job, display hello list of input media assets.
            builder.AppendLine("******JOB INPUT MEDIA ASSETS*******");
            foreach (IAsset inputAsset in job.InputMediaAssets)
            {

                if (inputAsset != null)
                {
                    builder.AppendLine("Input Asset Id: " + inputAsset.Id);
                    builder.AppendLine("Name: " + inputAsset.Name);
                    builder.AppendLine("==============");
                }
            }

            // For each job, display hello list of output media assets.
            builder.AppendLine("******JOB OUTPUT MEDIA ASSETS*******");
            foreach (IAsset theAsset in job.OutputMediaAssets)
            {
                if (theAsset != null)
                {
                    builder.AppendLine("Output Asset Id: " + theAsset.Id);
                    builder.AppendLine("Name: " + theAsset.Name);
                    builder.AppendLine("==============");
                }
            }

        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="list-all-access-policies"></a>Elencare tutti i criteri di accesso
In Servizi multimediali è possibile definire un criterio di accesso per un asset o i relativi file. Un criterio di accesso definisce le autorizzazioni di hello per un file o una risorsa (il tipo di accesso e la durata di hello). Nel codice di Servizi multimediali, in genere si definisce un criterio di accesso creando un oggetto IAccessPolicy e associandolo a un asset esistente. È quindi necessario creare un oggetto ILocator, che consente di fornire accesso diretto tooassets in servizi multimediali. progetto di Visual Studio Hello che accompagna la serie di documentazione contiene alcuni esempi di codice che illustrano come toocreate e assegnare l'accesso tooassets criteri e i localizzatori.

Hello seguente esempio di codice viene illustrato come toolist tutti i criteri di accesso nel server di hello e Mostra hello tipo di autorizzazioni associati a ognuna. Criteri di accesso di un altro modo utile tooview è toolist tutti gli oggetti ILocator nel server di hello e quindi per ogni localizzatore, è possibile elencare i criteri di accesso associato utilizzando la relativa proprietà AccessPolicy.

    static void ListAllPolicies()
    {
        foreach (IAccessPolicy policy in _context.AccessPolicies)
        {
            Console.WriteLine("");
            Console.WriteLine("Name:  " + policy.Name);
            Console.WriteLine("ID:  " + policy.Id);
            Console.WriteLine("Permissions: " + policy.Permissions);
            Console.WriteLine("==============");

        }
    }
    
## <a name="limit-access-policies"></a>Limitare i criteri di accesso 

>[!NOTE]
> È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy). È consigliabile utilizzare hello stesso ID di criteri, se si utilizza sempre hello stesso giorni accesso le autorizzazioni, ad esempio, i criteri per i localizzatori che sono previsti tooremain sul posto per un lungo periodo (non-caricamento criteri). 

Ad esempio, è possibile creare un insieme generico di criteri con hello seguente di codice che verrebbe eseguito solo una volta nell'applicazione. È possibile registrare i file di log tooa ID per un utilizzo successivo:

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

Quindi, è possibile utilizzare hello esistente ID nel codice simile al seguente:

    const string policy1YearId = "nb:pid:UUID:2a4f0104-51a9-4078-ae26-c730f88d35cf";


    // Get hello standard policy for 1 year read only
    var tempPolicyId = from b in _context.AccessPolicies
                       where b.Id == policy1YearId
                       select b;
    IAccessPolicy policy1Year = tempPolicyId.FirstOrDefault();

    // Get hello existing asset
    var tempAsset = from a in _context.Assets
                where a.Id == assetID
                select a;
    IAsset asset = tempAsset.SingleOrDefault();

    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy1Year,
        DateTime.UtcNow.AddMinutes(-5));
    Console.WriteLine("hello locator base path is " + originLocator.BaseUri.ToString());

## <a name="list-all-locators"></a>Elencare tutti i localizzatori
Un indicatore di posizione è un URL che fornisce un percorso diretto di tooaccess un asset, insieme a asset toohello autorizzazioni come definito dai criteri di accesso associato del localizzatore hello. A ogni asset può essere associata una raccolta di oggetti ILocator per la relativa proprietà Locators. contesto server Hello dispone di una raccolta di indicatori di posizione che contiene tutti i localizzatori.

Hello esempio di codice seguente vengono elencati tutti i localizzatori nel server di hello. Per ogni localizzatore, Mostra hello Id per l'asset correlati hello e criteri di accesso. Visualizza anche il tipo di hello di asset toohello percorso completo di hello, data di scadenza hello e autorizzazioni.

Si noti che un asset di tooan percorso localizzatore è solo un asset base toohello URL. toocreate che tooindividual un percorso diretto di file che un utente o un'applicazione potrebbe accedere, il codice deve aggiungere il percorso localizzatore toohello di hello file specifico percorso. Per ulteriori informazioni su come toodo questa operazione, vedere argomento hello [distribuzione di asset con Media Services SDK per .NET hello](media-services-deliver-streaming-content.md).

    static void ListAllLocators()
    {
        foreach (ILocator locator in _context.Locators)
        {
            Console.WriteLine("***********");
            Console.WriteLine("Locator Id: " + locator.Id);
            Console.WriteLine("Locator asset Id: " + locator.AssetId);
            Console.WriteLine("Locator access policy Id: " + locator.AccessPolicyId);
            Console.WriteLine("Access policy permissions: " + locator.AccessPolicy.Permissions);
            Console.WriteLine("Locator expiration: " + locator.ExpirationDateTime);
            // hello locator path is hello base or parent path (with included permissions) tooaccess  
            // hello media content of an asset. toocreate a full URL tooa specific media file, take 
            // hello locator path and then append a file name and info as needed.  
            Console.WriteLine("Locator base path: " + locator.Path);
            Console.WriteLine("");
        }
    }

## <a name="enumerating-through-large-collections-of-entities"></a>Enumerazione di grandi raccolte di entità
Quando una query sulle entità, è previsto un limite di 1000 entità restituito in una sola volta perché v2 REST pubblici limita risultati too1000 risultati della query. Quando l'enumerazione di raccolte di entità di grandi dimensioni, è necessario toouse Skip e Take. 

Hello seguente funzione scorre tutti i processi di hello hello fornito Account di servizi multimediali. Servizi multimediali restituisce 1000 processi nella raccolta di processi. funzione Hello rende utilizzare ignorare ed eseguire toomake assicurarsi che tutti i processi vengono enumerati (nel caso in cui si dispone di più di 1.000 processi nell'account).

    static void ProcessJobs()
    {
        try
        {

            int skipSize = 0;
            int batchSize = 1000;
            int currentBatch = 0;

            while (true)
            {
                // Loop through all Jobs (1000 at a time) in hello Media Services account
                IQueryable _jobsCollectionQuery = _context.Jobs.Skip(skipSize).Take(batchSize);
                foreach (IJob job in _jobsCollectionQuery)
                {
                    currentBatch++;
                    Console.WriteLine("Processing Job Id:" + job.Id);
                }

                if (currentBatch == batchSize)
                {
                    skipSize += batchSize;
                    currentBatch = 0;
                }
                else
                {
                    break;
                }
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }

## <a name="delete-an-asset"></a>Eliminare un asset
Hello di esempio seguente elimina un asset.

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a>Eliminare un processo
toodelete un processo, è necessario controllare lo stato di hello di hello processo come indicato nella proprietà State hello. I processi completati o annullati possono essere eliminati direttamente, mentre i processi che hanno altri stati, ad esempio che sono accodati, pianificati o in elaborazione, devono essere annullati prima di poter essere eliminati.

Hello esempio di codice seguente viene illustrato un metodo per l'eliminazione di un processo verificandone ed eliminando quindi quando lo stato di hello è completato o annullato. Questo codice dipende dalla sezione precedente di hello in questo argomento per il recupero di un processo di riferimento tooa: ottenere un riferimento a un processo.

    static void DeleteJob(string jobId)
    {
        bool jobDeleted = false;

        while (!jobDeleted)
        {
            // Get an updated job reference.  
            IJob job = GetJob(jobId);

            // Check and handle various possible job states. You can 
            // only delete a job whose state is Finished, Error, or Canceled.   
            // You can cancel jobs that are Queued, Scheduled, or Processing,  
            // and then delete after they are canceled.
            switch (job.State)
            {
                case JobState.Finished:
                case JobState.Canceled:
                case JobState.Error:
                    // Job errors should already be logged by polling or event 
                    // handling methods such as CheckJobProgress or StateChanged.
                    // You can also call job.DeleteAsync toodo async deletes.
                    job.Delete();
                    Console.WriteLine("Job has been deleted.");
                    jobDeleted = true;
                    break;
                case JobState.Canceling:
                    Console.WriteLine("Job is cancelling and will be deleted "
                        + "when finished.");
                    Console.WriteLine("Wait while job finishes canceling...");
                    Thread.Sleep(5000);
                    break;
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                    job.Cancel();
                    Console.WriteLine("Job is scheduled or processing and will "
                        + "be deleted.");
                    break;
                default:
                    break;
            }

        }
    }


## <a name="delete-an-access-policy"></a>Eliminare un criterio di accesso
Hello esempio di codice seguente viene illustrato come tooget un criterio di accesso tooan riferimento basato su un Id del criterio e criteri di hello toodelete.

    static void DeleteAccessPolicy(string existingPolicyId)
    {
        // toodelete a specific access policy, get a reference toohello policy.  
        // based on hello policy Id passed toohello method.
        var policyInstance =
                from p in _context.AccessPolicies
                where p.Id == existingPolicyId
                select p;
        IAccessPolicy policy = policyInstance.FirstOrDefault();

        policy.Delete();

    }



## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


---
title: "Gestione di asset ed entità correlate con Media Services .NET SDK"
description: "Informazioni su come gestire asset ed entità correlate con Media Services SDK for .NET."
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
ms.openlocfilehash: 5efe16a09808267d0797521f9e1df2b60aec9cbb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a><span data-ttu-id="89d90-103">Gestione di asset ed entità correlate con Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="89d90-103">Managing Assets and Related Entities with Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="89d90-104">.NET</span><span class="sxs-lookup"><span data-stu-id="89d90-104">.NET</span></span>](media-services-dotnet-manage-entities.md)
> * [<span data-ttu-id="89d90-105">REST</span><span class="sxs-lookup"><span data-stu-id="89d90-105">REST</span></span>](media-services-rest-manage-entities.md)
> 
> 

<span data-ttu-id="89d90-106">Questo argomento illustra come gestire le entità dei Servizi multimediali di Azure con .NET.</span><span class="sxs-lookup"><span data-stu-id="89d90-106">This topic shows how to manage Azure Media Services entities with .NET.</span></span> 

>[!NOTE]
> <span data-ttu-id="89d90-107">A partire dal 1° aprile 2017, tutti i record di processo presenti nell'account e più vecchi di 90 giorni verranno eliminati automaticamente, insieme ai record attività associati, anche se il numero totale di record è inferiore alla quota massima.</span><span class="sxs-lookup"><span data-stu-id="89d90-107">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if the total number of records is below the maximum quota.</span></span> <span data-ttu-id="89d90-108">Ad esempio, il 1° aprile 2017 qualsiasi record di processo nell'account precedente il 31 dicembre 2016 verrà automaticamente eliminato.</span><span class="sxs-lookup"><span data-stu-id="89d90-108">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="89d90-109">Se è necessario archiviare le informazioni sul processo o sull'attività, è possibile usare il codice descritto in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="89d90-109">If you need to archive the job/task information, you can use the code described in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89d90-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="89d90-110">Prerequisites</span></span>

<span data-ttu-id="89d90-111">Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="89d90-111">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="get-an-asset-reference"></a><span data-ttu-id="89d90-112">Ottenere un riferimento a un asset</span><span class="sxs-lookup"><span data-stu-id="89d90-112">Get an Asset Reference</span></span>
<span data-ttu-id="89d90-113">Un'attività comune consiste nell'ottenere un riferimento a un asset esistente in Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="89d90-113">A frequent task is to get a reference to an existing asset in Media Services.</span></span> <span data-ttu-id="89d90-114">L'esempio di codice seguente mostra come ottenere un riferimento a un asset dalla raccolta Assets sull'oggetto contesto del server, in base all'ID dell'asset. L'esempio di codice seguente usa una query Linq per ottenere un riferimento a un oggetto IAsset.</span><span class="sxs-lookup"><span data-stu-id="89d90-114">The following code example shows how you can get an asset reference from the Assets collection on the server context object, based on an asset Id. The following code example uses a Linq query to get a reference to an existing IAsset object.</span></span>

    static IAsset GetAsset(string assetId)
    {
        // Use a LINQ Select query to get an asset.
        var assetInstance =
            from a in _context.Assets
            where a.Id == assetId
            select a;
        // Reference the asset as an IAsset.
        IAsset asset = assetInstance.FirstOrDefault();

        return asset;
    }

## <a name="list-all-assets"></a><span data-ttu-id="89d90-115">Elencare tutti gli asset</span><span class="sxs-lookup"><span data-stu-id="89d90-115">List All Assets</span></span>
<span data-ttu-id="89d90-116">Man mano che aumenta il numero degli asset archiviati, è utile elencarli tutti.</span><span class="sxs-lookup"><span data-stu-id="89d90-116">As the number of assets you have in storage grows, it is helpful to list your assets.</span></span> <span data-ttu-id="89d90-117">L'esempio di codice seguente mostra come scorrere la raccolta Assets nell'oggetto contesto del server.</span><span class="sxs-lookup"><span data-stu-id="89d90-117">The following code example shows how to iterate through the Assets collection on the server context object.</span></span> <span data-ttu-id="89d90-118">Con ogni asset, l'esempio di codice scrive anche alcuni valori delle relative proprietà nella console.</span><span class="sxs-lookup"><span data-stu-id="89d90-118">With each asset, the code example also writes some of its property values to the console.</span></span> <span data-ttu-id="89d90-119">Ogni asset, ad esempio, può includere numerosi file multimediali.</span><span class="sxs-lookup"><span data-stu-id="89d90-119">For example, each asset can contain many media files.</span></span> <span data-ttu-id="89d90-120">L'esempio di codice elenca tutti i file associati a ogni asset.</span><span class="sxs-lookup"><span data-stu-id="89d90-120">The code example writes out all files associated with each asset.</span></span>

    static void ListAssets()
    {
        string waitMessage = "Building the list. This may take a few "
            + "seconds to a few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder to store the list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IAsset asset in _context.Assets)
        {
            // Display the collection of assets.
            builder.AppendLine("");
            builder.AppendLine("******ASSET******");
            builder.AppendLine("Asset ID: " + asset.Id);
            builder.AppendLine("Name: " + asset.Name);
            builder.AppendLine("==============");
            builder.AppendLine("******ASSET FILES******");

            // Display the files associated with each asset. 
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

## <a name="get-a-job-reference"></a><span data-ttu-id="89d90-121">Ottenere un riferimento a un processo</span><span class="sxs-lookup"><span data-stu-id="89d90-121">Get a Job Reference</span></span>

<span data-ttu-id="89d90-122">Quando si usano attività di elaborazione nel codice di Servizi multimediali, è spesso necessario ottenere un riferimento a un processo esistente in base a un ID. L'esempio di codice seguente mostra come ottenere un riferimento a un oggetto IJob dalla raccolta Jobs.</span><span class="sxs-lookup"><span data-stu-id="89d90-122">When you work with processing tasks in Media Services code, you often need to get a reference to an existing job based on an Id. The following code example shows how to get a reference to an IJob object from the Jobs collection.</span></span>

<span data-ttu-id="89d90-123">Può essere necessario ottenere un riferimento a un processo quando si avvia un processo di codifica di lunga esecuzione e si vuole verificare lo stato del processo su un thread.</span><span class="sxs-lookup"><span data-stu-id="89d90-123">You may need to get a job reference when starting a long-running encoding job, and need to check the job status on a thread.</span></span> <span data-ttu-id="89d90-124">In casi come questo, quando il metodo è restituito da un thread, è necessario recuperare un riferimento aggiornato a un processo.</span><span class="sxs-lookup"><span data-stu-id="89d90-124">In cases like this, when the method returns from a thread, you need to retrieve a refreshed reference to a job.</span></span>

    static IJob GetJob(string jobId)
    {
        // Use a Linq select query to get an updated 
        // reference by Id. 
        var jobInstance =
            from j in _context.Jobs
            where j.Id == jobId
            select j;
        // Return the job reference as an Ijob. 
        IJob job = jobInstance.FirstOrDefault();

        return job;
    }

## <a name="list-jobs-and-assets"></a><span data-ttu-id="89d90-125">Elencare i processi e gli asset</span><span class="sxs-lookup"><span data-stu-id="89d90-125">List Jobs and Assets</span></span>
<span data-ttu-id="89d90-126">Un'importante attività correlata consiste nell'elencare gli asset con il relativo processo associato in Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="89d90-126">An important related task is to list assets with their associated job in Media Services.</span></span> <span data-ttu-id="89d90-127">L'esempio di codice seguente mostra come elencare ogni oggetto IJob e quindi, per ogni processo, visualizzare le proprietà relative al processo, tutte le attività correlate, tutti gli asset di input e tutti gli asset di output.</span><span class="sxs-lookup"><span data-stu-id="89d90-127">The following code example shows you how to list each IJob object, and then for each job, it displays properties about the job, all related tasks, all input assets, and all output assets.</span></span> <span data-ttu-id="89d90-128">Il codice di questo esempio può essere utile per molte altre attività.</span><span class="sxs-lookup"><span data-stu-id="89d90-128">The code in this example can be useful for numerous other tasks.</span></span> <span data-ttu-id="89d90-129">Se ad esempio si vuole elencare gli asset di output di uno o più processi di codifica eseguiti in precedenza, questo codice mostra come accedere agli asset di output.</span><span class="sxs-lookup"><span data-stu-id="89d90-129">For example, if you want to list the output assets from one or more encoding jobs that you ran previously, this code shows how to access the output assets.</span></span> <span data-ttu-id="89d90-130">Quando è disponibile un riferimento a un asset di output, è quindi possibile distribuire il contenuto ad altri utenti o applicazioni scaricandolo o specificando gli URL.</span><span class="sxs-lookup"><span data-stu-id="89d90-130">When you have a reference to an output asset, you can then deliver the content to other users or applications by downloading it, or providing URLs.</span></span> 

<span data-ttu-id="89d90-131">Per altre informazioni sulle opzioni per la distribuzione degli asset, vedere [Distribuire asset con Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="89d90-131">For more information on options for delivering assets, see [Deliver Assets with the Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

    // List all jobs on the server, and for each job, also list 
    // all tasks, all input assets, all output assets.

    static void ListJobsAndAssets()
    {
        string waitMessage = "Building the list. This may take a few "
            + "seconds to a few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder to store the list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IJob job in _context.Jobs)
        {
            // Display the collection of jobs on the server.
            builder.AppendLine("");
            builder.AppendLine("******JOB*******");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Name: " + job.Name);
            builder.AppendLine("State: " + job.State);
            builder.AppendLine("Order: " + job.Priority);
            builder.AppendLine("==============");


            // For each job, display the associated tasks (a job  
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

            // For each job, display the list of input media assets.
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

            // For each job, display the list of output media assets.
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

## <a name="list-all-access-policies"></a><span data-ttu-id="89d90-132">Elencare tutti i criteri di accesso</span><span class="sxs-lookup"><span data-stu-id="89d90-132">List all Access Policies</span></span>
<span data-ttu-id="89d90-133">In Servizi multimediali è possibile definire un criterio di accesso per un asset o i relativi file.</span><span class="sxs-lookup"><span data-stu-id="89d90-133">In Media Services, you can define an access policy on an asset or its files.</span></span> <span data-ttu-id="89d90-134">Un criterio di accesso definisce le autorizzazioni per un file o un asset, ovvero il tipo di accesso e la durata.</span><span class="sxs-lookup"><span data-stu-id="89d90-134">An access policy defines the permissions for a file or an asset (what type of access, and the duration).</span></span> <span data-ttu-id="89d90-135">Nel codice di Servizi multimediali, in genere si definisce un criterio di accesso creando un oggetto IAccessPolicy e associandolo a un asset esistente.</span><span class="sxs-lookup"><span data-stu-id="89d90-135">In your Media Services code, you typically define an access policy by creating an IAccessPolicy object and then associating it with an existing asset.</span></span> <span data-ttu-id="89d90-136">È quindi necessario creare un oggetto ILocator, che permette di fornire l'accesso diretto agli asset in Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="89d90-136">Then you create a ILocator object, which lets you provide direct access to assets in Media Services.</span></span> <span data-ttu-id="89d90-137">Il progetto di Visual Studio fornito con questa serie di argomenti include diversi esempi di codice in cui è illustrato come creare e assegnare criteri di accesso e localizzatori agli asset.</span><span class="sxs-lookup"><span data-stu-id="89d90-137">The Visual Studio project that accompanies this documentation series contains several code examples that show how to create and assign access policies and locators to assets.</span></span>

<span data-ttu-id="89d90-138">L'esempio di codice seguente illustra come elencare tutti i criteri di accesso nel server e mostra il tipo di autorizzazioni associato a ognuno.</span><span class="sxs-lookup"><span data-stu-id="89d90-138">The following code example shows how to list all access policies on the server, and shows the type of permissions associated with each.</span></span> <span data-ttu-id="89d90-139">Un altro modo utile per visualizzare i criteri di accesso consiste nell'elencare tutti gli oggetti ILocator nel server e quindi, per ogni localizzatore, elencare il relativo criterio di accesso associato usando la relativa proprietà AccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="89d90-139">Another useful way to view access policies is to list all ILocator objects on the server, and then for each locator, you can list its associated access policy by using its AccessPolicy property.</span></span>

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
    
## <a name="limit-access-policies"></a><span data-ttu-id="89d90-140">Limitare i criteri di accesso</span><span class="sxs-lookup"><span data-stu-id="89d90-140">Limit Access Policies</span></span> 

>[!NOTE]
> <span data-ttu-id="89d90-141">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="89d90-141">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="89d90-142">Usare lo stesso ID criterio se si usano sempre gli stessi giorni/autorizzazioni di accesso, come nel cado di criteri per i localizzatori che devono rimanere attivi per molto tempo (criteri di non caricamento).</span><span class="sxs-lookup"><span data-stu-id="89d90-142">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> 

<span data-ttu-id="89d90-143">Ad esempio è possibile creare un insieme generico di criteri con il codice seguente che vengono eseguiti una sola volta nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="89d90-143">For example, you can create a generic set of policies with the following code that would only run one time in your application.</span></span> <span data-ttu-id="89d90-144">È possibile registrare gli ID in un file di log per usarli in seguito:</span><span class="sxs-lookup"><span data-stu-id="89d90-144">You can log IDs to a log file for later use:</span></span>

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

<span data-ttu-id="89d90-145">Quindi sarà possibile usare gli ID esistenti nel codice come segue:</span><span class="sxs-lookup"><span data-stu-id="89d90-145">Then, you can use the existing IDs in your code like this:</span></span>

    const string policy1YearId = "nb:pid:UUID:2a4f0104-51a9-4078-ae26-c730f88d35cf";


    // Get the standard policy for 1 year read only
    var tempPolicyId = from b in _context.AccessPolicies
                       where b.Id == policy1YearId
                       select b;
    IAccessPolicy policy1Year = tempPolicyId.FirstOrDefault();

    // Get the existing asset
    var tempAsset = from a in _context.Assets
                where a.Id == assetID
                select a;
    IAsset asset = tempAsset.SingleOrDefault();

    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy1Year,
        DateTime.UtcNow.AddMinutes(-5));
    Console.WriteLine("The locator base path is " + originLocator.BaseUri.ToString());

## <a name="list-all-locators"></a><span data-ttu-id="89d90-146">Elencare tutti i localizzatori</span><span class="sxs-lookup"><span data-stu-id="89d90-146">List All Locators</span></span>
<span data-ttu-id="89d90-147">Un localizzatore è un URL che fornisce un percorso diretto per accedere a un asset, insieme alle autorizzazioni per l'asset definite dal criterio di accesso associato del localizzatore.</span><span class="sxs-lookup"><span data-stu-id="89d90-147">A locator is a URL that provides a direct path to access an asset, along with permissions to the asset as defined by the locator's associated access policy.</span></span> <span data-ttu-id="89d90-148">A ogni asset può essere associata una raccolta di oggetti ILocator per la relativa proprietà Locators.</span><span class="sxs-lookup"><span data-stu-id="89d90-148">Each asset can have a collection of ILocator objects associated with it on its Locators property.</span></span> <span data-ttu-id="89d90-149">Anche nel contesto del server è disponibile una raccolta Locators contenente tutti i localizzatori.</span><span class="sxs-lookup"><span data-stu-id="89d90-149">The server context also has a Locators collection that contains all locators.</span></span>

<span data-ttu-id="89d90-150">Nell'esempio di codice seguente sono elencati tutti i localizzatori nel server.</span><span class="sxs-lookup"><span data-stu-id="89d90-150">The following code example lists all locators on the server.</span></span> <span data-ttu-id="89d90-151">Per ogni localizzatore, sono mostrati l'ID per l'asset e il criterio di accesso correlati.</span><span class="sxs-lookup"><span data-stu-id="89d90-151">For each locator, it shows the Id for the related asset and access policy.</span></span> <span data-ttu-id="89d90-152">Sono anche visualizzati il tipo di autorizzazioni, la data di scadenza e il percorso completo dell'asset.</span><span class="sxs-lookup"><span data-stu-id="89d90-152">It also displays the type of permissions, the expiration date, and the full path to the asset.</span></span>

<span data-ttu-id="89d90-153">Si noti che il percorso localizzatore per un asset è solo un URL di base per l'accesso all'asset.</span><span class="sxs-lookup"><span data-stu-id="89d90-153">Note that a locator path to an asset is only a base URL to the asset.</span></span> <span data-ttu-id="89d90-154">Per creare un percorso diretto per i singoli file a cui un utente o un'applicazione potrebbe accedere, il codice deve aggiungere il percorso del file specifico al percorso localizzatore.</span><span class="sxs-lookup"><span data-stu-id="89d90-154">To create a direct path to individual files that a user or application could browse to, your code must add the specific file path to the locator path.</span></span> <span data-ttu-id="89d90-155">Per altre informazioni su come eseguire questa operazione, vedere l'argomento [Distribuire asset con Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="89d90-155">For more information on how to do this, see the topic [Deliver Assets with the Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

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
            // The locator path is the base or parent path (with included permissions) to access  
            // the media content of an asset. To create a full URL to a specific media file, take 
            // the locator path and then append a file name and info as needed.  
            Console.WriteLine("Locator base path: " + locator.Path);
            Console.WriteLine("");
        }
    }

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="89d90-156">Enumerazione di grandi raccolte di entità</span><span class="sxs-lookup"><span data-stu-id="89d90-156">Enumerating through large collections of entities</span></span>
<span data-ttu-id="89d90-157">Quando si esegue una query di entità, è previsto un limite di 1000 entità restituite in una sola volta perché la versione 2 pubblica di REST limita i risultati della query a 1000 risultati.</span><span class="sxs-lookup"><span data-stu-id="89d90-157">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results to 1000 results.</span></span> <span data-ttu-id="89d90-158">Quando si esegue l'enumerazione di grandi raccolte di entità, è necessario usare la proprietà Skip and Take.</span><span class="sxs-lookup"><span data-stu-id="89d90-158">You need to use Skip and Take when enumerating through large collections of entities.</span></span> 

<span data-ttu-id="89d90-159">La funzione seguente consente di scorrere tutti i processi nell'account di Servizi multimediali specificato.</span><span class="sxs-lookup"><span data-stu-id="89d90-159">The following function loops through all the jobs in the provided Media Services Account.</span></span> <span data-ttu-id="89d90-160">Servizi multimediali restituisce 1000 processi nella raccolta di processi.</span><span class="sxs-lookup"><span data-stu-id="89d90-160">Media Services returns 1000 jobs in Jobs Collection.</span></span> <span data-ttu-id="89d90-161">La funzione usa la proprietà Skip and Take per assicurarsi che tutti i processi vengano enumerati (se si dispone di più di 1000 processi nell'account).</span><span class="sxs-lookup"><span data-stu-id="89d90-161">The function makes use of Skip and Take to make sure that all jobs are enumerated (in case you have more than 1000 jobs in your account).</span></span>

    static void ProcessJobs()
    {
        try
        {

            int skipSize = 0;
            int batchSize = 1000;
            int currentBatch = 0;

            while (true)
            {
                // Loop through all Jobs (1000 at a time) in the Media Services account
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

## <a name="delete-an-asset"></a><span data-ttu-id="89d90-162">Eliminare un asset</span><span class="sxs-lookup"><span data-stu-id="89d90-162">Delete an Asset</span></span>
<span data-ttu-id="89d90-163">Nell'esempio seguente sarà eliminato un asset.</span><span class="sxs-lookup"><span data-stu-id="89d90-163">The following example deletes an asset.</span></span>

    static void DeleteAsset( IAsset asset)
    {
        // delete the asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted the Asset");

    }

## <a name="delete-a-job"></a><span data-ttu-id="89d90-164">Eliminare un processo</span><span class="sxs-lookup"><span data-stu-id="89d90-164">Delete a Job</span></span>
<span data-ttu-id="89d90-165">Per eliminare un processo, è necessario verificarne lo stato indicato nella proprietà State.</span><span class="sxs-lookup"><span data-stu-id="89d90-165">To delete a job, you must check the state of the job as indicated in the State property.</span></span> <span data-ttu-id="89d90-166">I processi completati o annullati possono essere eliminati direttamente, mentre i processi che hanno altri stati, ad esempio che sono accodati, pianificati o in elaborazione, devono essere annullati prima di poter essere eliminati.</span><span class="sxs-lookup"><span data-stu-id="89d90-166">Jobs that are finished or canceled can be deleted, while jobs that are in certain other states, such as queued, scheduled, or processing, must be canceled first, and then they can be deleted.</span></span>

<span data-ttu-id="89d90-167">L'esempio di codice seguente illustra un metodo per eliminare un processo verificandone lo stato e procedendo con l'eliminazione quando lo stato è completato o annullato.</span><span class="sxs-lookup"><span data-stu-id="89d90-167">The following code example shows a method for deleting a job by checking job states and then deleting when the state is finished or canceled.</span></span> <span data-ttu-id="89d90-168">Questo codice dipende dalla sezione precedente di questo argomento per ottenere un riferimento a un processo: Ottenere un riferimento a un processo.</span><span class="sxs-lookup"><span data-stu-id="89d90-168">This code depends on the previous section in this topic for getting a reference to a job: Get a job reference.</span></span>

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
                    // You can also call job.DeleteAsync to do async deletes.
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


## <a name="delete-an-access-policy"></a><span data-ttu-id="89d90-169">Eliminare un criterio di accesso</span><span class="sxs-lookup"><span data-stu-id="89d90-169">Delete an Access Policy</span></span>
<span data-ttu-id="89d90-170">L'esempio di codice seguente illustra come ottenere un riferimento a un criterio di accesso in base all'ID del criterio e quindi come eliminare il criterio.</span><span class="sxs-lookup"><span data-stu-id="89d90-170">The following code example shows how to get a reference to an access policy based on a policy Id, and then to delete the policy.</span></span>

    static void DeleteAccessPolicy(string existingPolicyId)
    {
        // To delete a specific access policy, get a reference to the policy.  
        // based on the policy Id passed to the method.
        var policyInstance =
                from p in _context.AccessPolicies
                where p.Id == existingPolicyId
                select p;
        IAccessPolicy policy = policyInstance.FirstOrDefault();

        policy.Delete();

    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="89d90-171">Percorsi di apprendimento di Media Services</span><span class="sxs-lookup"><span data-stu-id="89d90-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="89d90-172">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="89d90-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


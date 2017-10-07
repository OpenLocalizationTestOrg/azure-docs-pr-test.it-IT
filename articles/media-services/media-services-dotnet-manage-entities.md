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
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a><span data-ttu-id="13e61-103">Gestione di asset ed entità correlate con Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="13e61-103">Managing Assets and Related Entities with Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="13e61-104">.NET</span><span class="sxs-lookup"><span data-stu-id="13e61-104">.NET</span></span>](media-services-dotnet-manage-entities.md)
> * [<span data-ttu-id="13e61-105">REST</span><span class="sxs-lookup"><span data-stu-id="13e61-105">REST</span></span>](media-services-rest-manage-entities.md)
> 
> 

<span data-ttu-id="13e61-106">In questo argomento viene illustrata la modalità di servizi multimediali di Azure di toomanage entità con .NET.</span><span class="sxs-lookup"><span data-stu-id="13e61-106">This topic shows how toomanage Azure Media Services entities with .NET.</span></span> 

>[!NOTE]
> <span data-ttu-id="13e61-107">A partire dal 1 aprile 2017, qualsiasi record di processo più vecchi di 90 giorni account vengono eliminate automaticamente, insieme ai relativi record di attività associato, anche se il numero di record hello sotto la quota massima di hello.</span><span class="sxs-lookup"><span data-stu-id="13e61-107">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if hello total number of records is below hello maximum quota.</span></span> <span data-ttu-id="13e61-108">Ad esempio, il 1° aprile 2017 qualsiasi record di processo nell'account precedente il 31 dicembre 2016 verrà automaticamente eliminato.</span><span class="sxs-lookup"><span data-stu-id="13e61-108">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="13e61-109">Se sono necessarie informazioni di processi/attività hello tooarchive, è possibile utilizzare codice hello descritte in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="13e61-109">If you need tooarchive hello job/task information, you can use hello code described in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13e61-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="13e61-110">Prerequisites</span></span>

<span data-ttu-id="13e61-111">Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="13e61-111">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="get-an-asset-reference"></a><span data-ttu-id="13e61-112">Ottenere un riferimento a un asset</span><span class="sxs-lookup"><span data-stu-id="13e61-112">Get an Asset Reference</span></span>
<span data-ttu-id="13e61-113">Un'attività comune consiste tooget un asset esistente tooan di riferimento in servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="13e61-113">A frequent task is tooget a reference tooan existing asset in Media Services.</span></span> <span data-ttu-id="13e61-114">Hello esempio di codice seguente viene illustrato come ottenere un riferimento a un asset dalla raccolta di risorse hello in server hello oggetto di contesto, in base a un hello ID asset seguente codice viene illustrato come utilizzare una query Linq tooget tooan esistente IAsset oggetto di riferimento.</span><span class="sxs-lookup"><span data-stu-id="13e61-114">hello following code example shows how you can get an asset reference from hello Assets collection on hello server context object, based on an asset Id. hello following code example uses a Linq query tooget a reference tooan existing IAsset object.</span></span>

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

## <a name="list-all-assets"></a><span data-ttu-id="13e61-115">Elencare tutti gli asset</span><span class="sxs-lookup"><span data-stu-id="13e61-115">List All Assets</span></span>
<span data-ttu-id="13e61-116">Man mano che aumenta il numero di hello degli asset nel servizio di archiviazione, è utile toolist le risorse.</span><span class="sxs-lookup"><span data-stu-id="13e61-116">As hello number of assets you have in storage grows, it is helpful toolist your assets.</span></span> <span data-ttu-id="13e61-117">Hello esempio di codice seguente viene illustrato come tooiterate tramite hello raccolta di risorse dell'oggetto di contesto server hello.</span><span class="sxs-lookup"><span data-stu-id="13e61-117">hello following code example shows how tooiterate through hello Assets collection on hello server context object.</span></span> <span data-ttu-id="13e61-118">Con ogni asset, esempio di codice hello scrive inoltre alcune delle relative console toohello valori di proprietà.</span><span class="sxs-lookup"><span data-stu-id="13e61-118">With each asset, hello code example also writes some of its property values toohello console.</span></span> <span data-ttu-id="13e61-119">Ogni asset, ad esempio, può includere numerosi file multimediali.</span><span class="sxs-lookup"><span data-stu-id="13e61-119">For example, each asset can contain many media files.</span></span> <span data-ttu-id="13e61-120">esempio di codice Hello scrive tutti i file associati a ogni asset.</span><span class="sxs-lookup"><span data-stu-id="13e61-120">hello code example writes out all files associated with each asset.</span></span>

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

## <a name="get-a-job-reference"></a><span data-ttu-id="13e61-121">Ottenere un riferimento a un processo</span><span class="sxs-lookup"><span data-stu-id="13e61-121">Get a Job Reference</span></span>

<span data-ttu-id="13e61-122">Quando si lavora con l'elaborazione delle attività nel codice di servizi multimediali, è spesso necessario tooget un processo esistente tooan riferimento in base a un hello ID. esempio di codice seguente viene illustrato come tooget tooan un riferimento IJob oggetto dalla raccolta di processi hello.</span><span class="sxs-lookup"><span data-stu-id="13e61-122">When you work with processing tasks in Media Services code, you often need tooget a reference tooan existing job based on an Id. hello following code example shows how tooget a reference tooan IJob object from hello Jobs collection.</span></span>

<span data-ttu-id="13e61-123">Potrebbe necessario tooget riferimento a un processo quando si avvia un processo di codifica di lunga durata e lo stato del processo hello toocheck su un thread necessario.</span><span class="sxs-lookup"><span data-stu-id="13e61-123">You may need tooget a job reference when starting a long-running encoding job, and need toocheck hello job status on a thread.</span></span> <span data-ttu-id="13e61-124">In casi come questo, quando il metodo hello viene restituito da un thread, è necessario un processo di riferimento aggiornato tooa tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="13e61-124">In cases like this, when hello method returns from a thread, you need tooretrieve a refreshed reference tooa job.</span></span>

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

## <a name="list-jobs-and-assets"></a><span data-ttu-id="13e61-125">Elencare i processi e gli asset</span><span class="sxs-lookup"><span data-stu-id="13e61-125">List Jobs and Assets</span></span>
<span data-ttu-id="13e61-126">Un'importante attività correlata è asset toolist con il relativo processo associato in servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="13e61-126">An important related task is toolist assets with their associated job in Media Services.</span></span> <span data-ttu-id="13e61-127">Hello esempio di codice seguente illustra come toolist ogni oggetto IJob, per ogni processo, viene quindi visualizzato processo hello, tutte le attività correlate, asset di input tutte le proprietà e tutti gli asset di output.</span><span class="sxs-lookup"><span data-stu-id="13e61-127">hello following code example shows you how toolist each IJob object, and then for each job, it displays properties about hello job, all related tasks, all input assets, and all output assets.</span></span> <span data-ttu-id="13e61-128">in questo esempio di codice Hello può essere utile per molte altre attività.</span><span class="sxs-lookup"><span data-stu-id="13e61-128">hello code in this example can be useful for numerous other tasks.</span></span> <span data-ttu-id="13e61-129">Ad esempio, se si desidera asset di output di hello toolist da uno o più processi di codifica eseguiti in precedenza, questo codice viene illustrato come hello tooaccess gli asset di output.</span><span class="sxs-lookup"><span data-stu-id="13e61-129">For example, if you want toolist hello output assets from one or more encoding jobs that you ran previously, this code shows how tooaccess hello output assets.</span></span> <span data-ttu-id="13e61-130">Quando si dispone di un asset di output tooan di riferimento, è quindi possibile recapitare hello tooother contenuto utenti o applicazioni scaricandolo o specificando gli URL.</span><span class="sxs-lookup"><span data-stu-id="13e61-130">When you have a reference tooan output asset, you can then deliver hello content tooother users or applications by downloading it, or providing URLs.</span></span> 

<span data-ttu-id="13e61-131">Per ulteriori informazioni sulle opzioni per la distribuzione degli asset, vedere [distribuzione di asset con Media Services SDK per .NET hello](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="13e61-131">For more information on options for delivering assets, see [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

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

## <a name="list-all-access-policies"></a><span data-ttu-id="13e61-132">Elencare tutti i criteri di accesso</span><span class="sxs-lookup"><span data-stu-id="13e61-132">List all Access Policies</span></span>
<span data-ttu-id="13e61-133">In Servizi multimediali è possibile definire un criterio di accesso per un asset o i relativi file.</span><span class="sxs-lookup"><span data-stu-id="13e61-133">In Media Services, you can define an access policy on an asset or its files.</span></span> <span data-ttu-id="13e61-134">Un criterio di accesso definisce le autorizzazioni di hello per un file o una risorsa (il tipo di accesso e la durata di hello).</span><span class="sxs-lookup"><span data-stu-id="13e61-134">An access policy defines hello permissions for a file or an asset (what type of access, and hello duration).</span></span> <span data-ttu-id="13e61-135">Nel codice di Servizi multimediali, in genere si definisce un criterio di accesso creando un oggetto IAccessPolicy e associandolo a un asset esistente.</span><span class="sxs-lookup"><span data-stu-id="13e61-135">In your Media Services code, you typically define an access policy by creating an IAccessPolicy object and then associating it with an existing asset.</span></span> <span data-ttu-id="13e61-136">È quindi necessario creare un oggetto ILocator, che consente di fornire accesso diretto tooassets in servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="13e61-136">Then you create a ILocator object, which lets you provide direct access tooassets in Media Services.</span></span> <span data-ttu-id="13e61-137">progetto di Visual Studio Hello che accompagna la serie di documentazione contiene alcuni esempi di codice che illustrano come toocreate e assegnare l'accesso tooassets criteri e i localizzatori.</span><span class="sxs-lookup"><span data-stu-id="13e61-137">hello Visual Studio project that accompanies this documentation series contains several code examples that show how toocreate and assign access policies and locators tooassets.</span></span>

<span data-ttu-id="13e61-138">Hello seguente esempio di codice viene illustrato come toolist tutti i criteri di accesso nel server di hello e Mostra hello tipo di autorizzazioni associati a ognuna.</span><span class="sxs-lookup"><span data-stu-id="13e61-138">hello following code example shows how toolist all access policies on hello server, and shows hello type of permissions associated with each.</span></span> <span data-ttu-id="13e61-139">Criteri di accesso di un altro modo utile tooview è toolist tutti gli oggetti ILocator nel server di hello e quindi per ogni localizzatore, è possibile elencare i criteri di accesso associato utilizzando la relativa proprietà AccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="13e61-139">Another useful way tooview access policies is toolist all ILocator objects on hello server, and then for each locator, you can list its associated access policy by using its AccessPolicy property.</span></span>

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
    
## <a name="limit-access-policies"></a><span data-ttu-id="13e61-140">Limitare i criteri di accesso</span><span class="sxs-lookup"><span data-stu-id="13e61-140">Limit Access Policies</span></span> 

>[!NOTE]
> <span data-ttu-id="13e61-141">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="13e61-141">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="13e61-142">È consigliabile utilizzare hello stesso ID di criteri, se si utilizza sempre hello stesso giorni accesso le autorizzazioni, ad esempio, i criteri per i localizzatori che sono previsti tooremain sul posto per un lungo periodo (non-caricamento criteri).</span><span class="sxs-lookup"><span data-stu-id="13e61-142">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> 

<span data-ttu-id="13e61-143">Ad esempio, è possibile creare un insieme generico di criteri con hello seguente di codice che verrebbe eseguito solo una volta nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="13e61-143">For example, you can create a generic set of policies with hello following code that would only run one time in your application.</span></span> <span data-ttu-id="13e61-144">È possibile registrare i file di log tooa ID per un utilizzo successivo:</span><span class="sxs-lookup"><span data-stu-id="13e61-144">You can log IDs tooa log file for later use:</span></span>

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

<span data-ttu-id="13e61-145">Quindi, è possibile utilizzare hello esistente ID nel codice simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="13e61-145">Then, you can use hello existing IDs in your code like this:</span></span>

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

## <a name="list-all-locators"></a><span data-ttu-id="13e61-146">Elencare tutti i localizzatori</span><span class="sxs-lookup"><span data-stu-id="13e61-146">List All Locators</span></span>
<span data-ttu-id="13e61-147">Un indicatore di posizione è un URL che fornisce un percorso diretto di tooaccess un asset, insieme a asset toohello autorizzazioni come definito dai criteri di accesso associato del localizzatore hello.</span><span class="sxs-lookup"><span data-stu-id="13e61-147">A locator is a URL that provides a direct path tooaccess an asset, along with permissions toohello asset as defined by hello locator's associated access policy.</span></span> <span data-ttu-id="13e61-148">A ogni asset può essere associata una raccolta di oggetti ILocator per la relativa proprietà Locators.</span><span class="sxs-lookup"><span data-stu-id="13e61-148">Each asset can have a collection of ILocator objects associated with it on its Locators property.</span></span> <span data-ttu-id="13e61-149">contesto server Hello dispone di una raccolta di indicatori di posizione che contiene tutti i localizzatori.</span><span class="sxs-lookup"><span data-stu-id="13e61-149">hello server context also has a Locators collection that contains all locators.</span></span>

<span data-ttu-id="13e61-150">Hello esempio di codice seguente vengono elencati tutti i localizzatori nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="13e61-150">hello following code example lists all locators on hello server.</span></span> <span data-ttu-id="13e61-151">Per ogni localizzatore, Mostra hello Id per l'asset correlati hello e criteri di accesso.</span><span class="sxs-lookup"><span data-stu-id="13e61-151">For each locator, it shows hello Id for hello related asset and access policy.</span></span> <span data-ttu-id="13e61-152">Visualizza anche il tipo di hello di asset toohello percorso completo di hello, data di scadenza hello e autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="13e61-152">It also displays hello type of permissions, hello expiration date, and hello full path toohello asset.</span></span>

<span data-ttu-id="13e61-153">Si noti che un asset di tooan percorso localizzatore è solo un asset base toohello URL.</span><span class="sxs-lookup"><span data-stu-id="13e61-153">Note that a locator path tooan asset is only a base URL toohello asset.</span></span> <span data-ttu-id="13e61-154">toocreate che tooindividual un percorso diretto di file che un utente o un'applicazione potrebbe accedere, il codice deve aggiungere il percorso localizzatore toohello di hello file specifico percorso.</span><span class="sxs-lookup"><span data-stu-id="13e61-154">toocreate a direct path tooindividual files that a user or application could browse to, your code must add hello specific file path toohello locator path.</span></span> <span data-ttu-id="13e61-155">Per ulteriori informazioni su come toodo questa operazione, vedere argomento hello [distribuzione di asset con Media Services SDK per .NET hello](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="13e61-155">For more information on how toodo this, see hello topic [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

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

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="13e61-156">Enumerazione di grandi raccolte di entità</span><span class="sxs-lookup"><span data-stu-id="13e61-156">Enumerating through large collections of entities</span></span>
<span data-ttu-id="13e61-157">Quando una query sulle entità, è previsto un limite di 1000 entità restituito in una sola volta perché v2 REST pubblici limita risultati too1000 risultati della query.</span><span class="sxs-lookup"><span data-stu-id="13e61-157">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="13e61-158">Quando l'enumerazione di raccolte di entità di grandi dimensioni, è necessario toouse Skip e Take.</span><span class="sxs-lookup"><span data-stu-id="13e61-158">You need toouse Skip and Take when enumerating through large collections of entities.</span></span> 

<span data-ttu-id="13e61-159">Hello seguente funzione scorre tutti i processi di hello hello fornito Account di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="13e61-159">hello following function loops through all hello jobs in hello provided Media Services Account.</span></span> <span data-ttu-id="13e61-160">Servizi multimediali restituisce 1000 processi nella raccolta di processi.</span><span class="sxs-lookup"><span data-stu-id="13e61-160">Media Services returns 1000 jobs in Jobs Collection.</span></span> <span data-ttu-id="13e61-161">funzione Hello rende utilizzare ignorare ed eseguire toomake assicurarsi che tutti i processi vengono enumerati (nel caso in cui si dispone di più di 1.000 processi nell'account).</span><span class="sxs-lookup"><span data-stu-id="13e61-161">hello function makes use of Skip and Take toomake sure that all jobs are enumerated (in case you have more than 1000 jobs in your account).</span></span>

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

## <a name="delete-an-asset"></a><span data-ttu-id="13e61-162">Eliminare un asset</span><span class="sxs-lookup"><span data-stu-id="13e61-162">Delete an Asset</span></span>
<span data-ttu-id="13e61-163">Hello di esempio seguente elimina un asset.</span><span class="sxs-lookup"><span data-stu-id="13e61-163">hello following example deletes an asset.</span></span>

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a><span data-ttu-id="13e61-164">Eliminare un processo</span><span class="sxs-lookup"><span data-stu-id="13e61-164">Delete a Job</span></span>
<span data-ttu-id="13e61-165">toodelete un processo, è necessario controllare lo stato di hello di hello processo come indicato nella proprietà State hello.</span><span class="sxs-lookup"><span data-stu-id="13e61-165">toodelete a job, you must check hello state of hello job as indicated in hello State property.</span></span> <span data-ttu-id="13e61-166">I processi completati o annullati possono essere eliminati direttamente, mentre i processi che hanno altri stati, ad esempio che sono accodati, pianificati o in elaborazione, devono essere annullati prima di poter essere eliminati.</span><span class="sxs-lookup"><span data-stu-id="13e61-166">Jobs that are finished or canceled can be deleted, while jobs that are in certain other states, such as queued, scheduled, or processing, must be canceled first, and then they can be deleted.</span></span>

<span data-ttu-id="13e61-167">Hello esempio di codice seguente viene illustrato un metodo per l'eliminazione di un processo verificandone ed eliminando quindi quando lo stato di hello è completato o annullato.</span><span class="sxs-lookup"><span data-stu-id="13e61-167">hello following code example shows a method for deleting a job by checking job states and then deleting when hello state is finished or canceled.</span></span> <span data-ttu-id="13e61-168">Questo codice dipende dalla sezione precedente di hello in questo argomento per il recupero di un processo di riferimento tooa: ottenere un riferimento a un processo.</span><span class="sxs-lookup"><span data-stu-id="13e61-168">This code depends on hello previous section in this topic for getting a reference tooa job: Get a job reference.</span></span>

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


## <a name="delete-an-access-policy"></a><span data-ttu-id="13e61-169">Eliminare un criterio di accesso</span><span class="sxs-lookup"><span data-stu-id="13e61-169">Delete an Access Policy</span></span>
<span data-ttu-id="13e61-170">Hello esempio di codice seguente viene illustrato come tooget un criterio di accesso tooan riferimento basato su un Id del criterio e criteri di hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="13e61-170">hello following code example shows how tooget a reference tooan access policy based on a policy Id, and then toodelete hello policy.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="13e61-171">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="13e61-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="13e61-172">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="13e61-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


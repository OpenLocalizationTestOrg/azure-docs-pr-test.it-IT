---
title: aaaHow tooencode un asset con Media Encoder Standard Azure | Documenti Microsoft
description: Informazioni su come toouse Media Encoder Standard tooencode multimediali in servizi multimediali di Azure. Negli esempi di codice viene usata l'API REST.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="22c71-104">Come tooencode un asset con Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="22c71-104">How tooencode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="22c71-105">.NET</span><span class="sxs-lookup"><span data-stu-id="22c71-105">.NET</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [<span data-ttu-id="22c71-106">REST</span><span class="sxs-lookup"><span data-stu-id="22c71-106">REST</span></span>](media-services-rest-encode-asset.md)
> * [<span data-ttu-id="22c71-107">Portale</span><span class="sxs-lookup"><span data-stu-id="22c71-107">Portal</span></span>](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="22c71-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="22c71-108">Overview</span></span>
<span data-ttu-id="22c71-109">toodeliver video digitale su hello Internet, è necessario comprimere supporti hello.</span><span class="sxs-lookup"><span data-stu-id="22c71-109">toodeliver digital video over hello Internet, you must compress hello media.</span></span> <span data-ttu-id="22c71-110">File video digitali sono di grandi dimensioni e potrebbero essere troppo grande toodeliver su hello Internet, o per toodisplay dispositivi dei clienti in modo corretto.</span><span class="sxs-lookup"><span data-stu-id="22c71-110">Digital video files are large and may be too big toodeliver over hello Internet, or for your customers’ devices toodisplay properly.</span></span> <span data-ttu-id="22c71-111">La codifica è il processo di hello di compressione di video e audio in modo i clienti possono visualizzare i file multimediali.</span><span class="sxs-lookup"><span data-stu-id="22c71-111">Encoding is hello process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="22c71-112">I processi di codifica sono una delle operazioni di elaborazione più comune di hello in servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="22c71-112">Encoding jobs are one of hello most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="22c71-113">Viene creato codifica file multimediali tooconvert di processi da un tooanother codifica.</span><span class="sxs-lookup"><span data-stu-id="22c71-113">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="22c71-114">Quando si codifica, è possibile utilizzare hello incorporato codificatore di servizi multimediali (Media Encoder Standard).</span><span class="sxs-lookup"><span data-stu-id="22c71-114">When you encode, you can use hello Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="22c71-115">È inoltre possibile usare un codificatore fornito da un partner di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="22c71-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="22c71-116">I codificatori di terze parti sono disponibili tramite hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="22c71-116">Third-party encoders are available through hello Azure Marketplace.</span></span> <span data-ttu-id="22c71-117">È possibile specificare i dettagli di hello attività di codifica usando stringhe di set di impostazioni definite per il codificatore oppure utilizzando i file di configurazione predefinito.</span><span class="sxs-lookup"><span data-stu-id="22c71-117">You can specify hello details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="22c71-118">tipi di hello toosee dei set di impostazioni che sono disponibili, vedere [set di impostazioni di attività per supporti codificatore Standard](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="22c71-118">toosee hello types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="22c71-119">Ogni processo può avere uno o più attività in base al tipo di hello di elaborazione che si desidera tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="22c71-119">Each job can have one or more tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="22c71-120">Tramite hello API REST, è possibile creare processi e le attività correlate in uno dei due modi:</span><span class="sxs-lookup"><span data-stu-id="22c71-120">Through hello REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="22c71-121">Le attività possono essere definite inline mediante proprietà di navigazione attività hello in entità Job.</span><span class="sxs-lookup"><span data-stu-id="22c71-121">Tasks can be defined inline through hello Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="22c71-122">Usare l'elaborazione batch OData.</span><span class="sxs-lookup"><span data-stu-id="22c71-122">Use OData batch processing.</span></span>

<span data-ttu-id="22c71-123">È consigliabile codificare sempre i file di origine in un set MP4 a velocità in bit adattiva e quindi convertire il formato desiderato hello set toohello utilizzando [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="22c71-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert hello set toohello desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="22c71-124">Se l'asset di output è crittografato di archiviazione, è necessario configurare i criteri di distribuzione di asset hello.</span><span class="sxs-lookup"><span data-stu-id="22c71-124">If your output asset is storage encrypted, you must configure hello asset delivery policy.</span></span> <span data-ttu-id="22c71-125">Per altre informazioni, vedere [Configurazione dei criteri di distribuzione degli asset](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="22c71-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="22c71-126">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="22c71-126">Considerations</span></span>

<span data-ttu-id="22c71-127">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="22c71-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="22c71-128">Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="22c71-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

<span data-ttu-id="22c71-129">Prima di avviare che fanno riferimento a processori di contenuti multimediali, verificare che si sono hello corretto processore relativo ID.</span><span class="sxs-lookup"><span data-stu-id="22c71-129">Before you start referencing media processors, verify that you have hello correct media processor ID.</span></span> <span data-ttu-id="22c71-130">Per altre informazioni, vedere [Ottenere processori di contenuti multimediali](media-services-rest-get-media-processor.md).</span><span class="sxs-lookup"><span data-stu-id="22c71-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="22c71-131">Connessione dei servizi tooMedia</span><span class="sxs-lookup"><span data-stu-id="22c71-131">Connect tooMedia Services</span></span>

<span data-ttu-id="22c71-132">Per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="22c71-132">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="22c71-133">Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="22c71-133">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="22c71-134">È necessario effettuare le chiamate successive toohello nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="22c71-134">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="22c71-135">Creare un processo con una singola attività di codifica</span><span class="sxs-lookup"><span data-stu-id="22c71-135">Create a job with a single encoding task</span></span>
> [!NOTE]
> <span data-ttu-id="22c71-136">Quando si lavora con hello API REST di servizi multimediali, hello seguenti considerazioni:</span><span class="sxs-lookup"><span data-stu-id="22c71-136">When you're working with hello Media Services REST API, hello following considerations apply:</span></span>
>
> <span data-ttu-id="22c71-137">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="22c71-137">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="22c71-138">Per altre informazioni, vedere [Configurazione dello sviluppo dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="22c71-138">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span></span>
>
> <span data-ttu-id="22c71-139">Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="22c71-139">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="22c71-140">È necessario effettuare le chiamate successive toohello nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="22c71-140">You must make subsequent calls toohello new URI.</span></span> <span data-ttu-id="22c71-141">Per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="22c71-141">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
>
> <span data-ttu-id="22c71-142">Quando si utilizza JSON e specificando hello toouse **Metadata** (parola chiave) nella richiesta di hello (ad esempio, tooreferences un oggetto collegato), è necessario impostare hello **Accept** intestazione troppo[formato JSON dettagliato ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accettare: application/json; odata = verbose.</span><span class="sxs-lookup"><span data-stu-id="22c71-142">When using JSON and specifying toouse hello **__metadata** keyword in hello request (for example, tooreferences a linked object), you must set hello **Accept** header too[JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span></span>
>
>

<span data-ttu-id="22c71-143">Hello di esempio seguente vengono visualizzati è come toocreate e post un processo con una sola attività tooencode un video a una risoluzione specifico e di qualità.</span><span class="sxs-lookup"><span data-stu-id="22c71-143">hello following example shows you how toocreate and post a job with one task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="22c71-144">Quando si esegue la codifica con Media Encoder Standard, è possibile usare i set di impostazioni di attività specificati [qui](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="22c71-144">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="22c71-145">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="22c71-145">Request:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

<span data-ttu-id="22c71-146">Risposta:</span><span class="sxs-lookup"><span data-stu-id="22c71-146">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-hello-output-assets-name"></a><span data-ttu-id="22c71-147">Impostare il nome dell'asset di output hello</span><span class="sxs-lookup"><span data-stu-id="22c71-147">Set hello output asset's name</span></span>
<span data-ttu-id="22c71-148">Hello di esempio seguente viene illustrato come tooset hello attributo assetName:</span><span class="sxs-lookup"><span data-stu-id="22c71-148">hello following example shows how tooset hello assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="22c71-149">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="22c71-149">Considerations</span></span>
* <span data-ttu-id="22c71-150">Proprietà TaskBody devono usare numero hello toodefine letterale XML di input o output asset utilizzati dall'attività hello.</span><span class="sxs-lookup"><span data-stu-id="22c71-150">TaskBody properties must use literal XML toodefine hello number of input, or output assets that are used by hello task.</span></span> <span data-ttu-id="22c71-151">argomento di attività Hello contiene hello definizione dello Schema XML per hello XML.</span><span class="sxs-lookup"><span data-stu-id="22c71-151">hello task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="22c71-152">In definizione TaskBody hello, valore di ogni interna di <inputAsset> e <outputAsset> deve essere impostato come JobInputAsset(value) o JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="22c71-152">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="22c71-153">Un'attività può avere più asset di output.</span><span class="sxs-lookup"><span data-stu-id="22c71-153">A task can have multiple output assets.</span></span> <span data-ttu-id="22c71-154">Un oggetto JobOutputAsset(x) può essere usato solo una volta come output di un'attività in un processo.</span><span class="sxs-lookup"><span data-stu-id="22c71-154">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="22c71-155">È possibile specificare JobInputAsset o JobOutputAsset come asset di input di un'attività.</span><span class="sxs-lookup"><span data-stu-id="22c71-155">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="22c71-156">Le attività non devono formare un ciclo.</span><span class="sxs-lookup"><span data-stu-id="22c71-156">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="22c71-157">il parametro di valore Hello passato tooJobInputAsset o JobOutputAsset rappresenta il valore di indice hello per un asset.</span><span class="sxs-lookup"><span data-stu-id="22c71-157">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an asset.</span></span> <span data-ttu-id="22c71-158">Asset effettivi Hello sono definiti nel hello InputMediaAssets e OutputMediaAssets le proprietà di navigazione nella definizione di entità processo hello.</span><span class="sxs-lookup"><span data-stu-id="22c71-158">hello actual assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello job entity definition.</span></span>
* <span data-ttu-id="22c71-159">Poiché servizi multimediali si basa su OData versione 3, hello ai singoli asset nelle hello InputMediaAssets e OutputMediaAssets raccolte di proprietà di navigazione vengono fatto riferimento tramite un " Metadata: uri" coppia nome-valore.</span><span class="sxs-lookup"><span data-stu-id="22c71-159">Because Media Services is built on OData v3, hello individual assets in hello InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
* <span data-ttu-id="22c71-160">Proprietà InputMediaAssets è mappata tooone o altre risorse create in servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="22c71-160">InputMediaAssets maps tooone or more assets that you created in Media Services.</span></span> <span data-ttu-id="22c71-161">OutputMediaAssets vengono create dal sistema di hello.</span><span class="sxs-lookup"><span data-stu-id="22c71-161">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="22c71-162">Non fanno riferimento a un asset esistente.</span><span class="sxs-lookup"><span data-stu-id="22c71-162">They don't reference an existing asset.</span></span>
* <span data-ttu-id="22c71-163">È possibile denominare OutputMediaAssets utilizzando l'attributo assetName hello.</span><span class="sxs-lookup"><span data-stu-id="22c71-163">OutputMediaAssets can be named by using hello assetName attribute.</span></span> <span data-ttu-id="22c71-164">Se questo attributo non è presente, il nome di hello di hello Outputmediaassets indipendentemente dal valore di testo interno hello di hello <outputAsset> elemento è con un suffisso del valore del nome di processo hello o valore di Id di processo hello (in caso di hello in hello Nome proprietà non è definita).</span><span class="sxs-lookup"><span data-stu-id="22c71-164">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="22c71-165">Ad esempio, se si imposta un valore per assetName troppo "Esempio", quindi hello Name di Outputmediaassets impostata troppo "Sample."</span><span class="sxs-lookup"><span data-stu-id="22c71-165">For example, if you set a value for assetName too"Sample," then hello OutputMediaAsset Name property is set too"Sample."</span></span> <span data-ttu-id="22c71-166">Tuttavia, se si non è stato impostato un valore per assetName ma è stato impostato il nome di processo hello troppo "NewJob", quindi hello Name di Outputmediaassets sarà "JobOutputAsset (valore) newjob".</span><span class="sxs-lookup"><span data-stu-id="22c71-166">However, if you didn't set a value for assetName, but did set hello job name too"NewJob," then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="22c71-167">Creare un processo con attività concatenate</span><span class="sxs-lookup"><span data-stu-id="22c71-167">Create a job with chained tasks</span></span>
<span data-ttu-id="22c71-168">In molti scenari di applicazione, gli sviluppatori desiderino toocreate una serie di attività di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="22c71-168">In many application scenarios, developers want toocreate a series of processing tasks.</span></span> <span data-ttu-id="22c71-169">In Servizi multimediali è possibile creare una serie di attività concatenate.</span><span class="sxs-lookup"><span data-stu-id="22c71-169">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="22c71-170">Ogni attività esegue diversi passaggi di elaborazione e può usare processori di contenuti multimediali differenti.</span><span class="sxs-lookup"><span data-stu-id="22c71-170">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="22c71-171">attività Hello concatenata possono trasferire un asset da tooanother un'attività, l'esecuzione di una sequenza lineare delle attività su asset hello.</span><span class="sxs-lookup"><span data-stu-id="22c71-171">hello chained tasks can hand off an asset from one task tooanother, performing a linear sequence of tasks on hello asset.</span></span> <span data-ttu-id="22c71-172">Attività hello eseguite in un processo non sono tuttavia toobe richiesto in una sequenza.</span><span class="sxs-lookup"><span data-stu-id="22c71-172">However, hello tasks performed in a job are not required toobe in a sequence.</span></span> <span data-ttu-id="22c71-173">Quando si crea un'attività concatenata, hello concatenate **ITask** gli oggetti vengono creati in una singola **IJob** oggetto.</span><span class="sxs-lookup"><span data-stu-id="22c71-173">When you create a chained task, hello chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> <span data-ttu-id="22c71-174">Attualmente è previsto un limite di 30 attività per processo.</span><span class="sxs-lookup"><span data-stu-id="22c71-174">There is currently a limit of 30 tasks per job.</span></span> <span data-ttu-id="22c71-175">Se è necessario toochain più di 30 attività, creare più di un processo attività hello toocontain.</span><span class="sxs-lookup"><span data-stu-id="22c71-175">If you need toochain more than 30 tasks, create more than one job toocontain hello tasks.</span></span>
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a><span data-ttu-id="22c71-176">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="22c71-176">Considerations</span></span>
<span data-ttu-id="22c71-177">tooenable concatenamenti di attività:</span><span class="sxs-lookup"><span data-stu-id="22c71-177">tooenable task chaining:</span></span>

* <span data-ttu-id="22c71-178">Un processo deve avere almeno due attività.</span><span class="sxs-lookup"><span data-stu-id="22c71-178">A job must have at least two tasks.</span></span>
* <span data-ttu-id="22c71-179">Deve esserci almeno un'attività il cui input è l'output di hello di un'altra attività nel processo di hello.</span><span class="sxs-lookup"><span data-stu-id="22c71-179">There must be at least one task whose input is hello output of another task in hello job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="22c71-180">Utilizzare l'elaborazione batch OData</span><span class="sxs-lookup"><span data-stu-id="22c71-180">Use OData batch processing</span></span>
<span data-ttu-id="22c71-181">Hello di esempio seguente viene illustrato come toouse OData batch toocreate l'elaborazione di un processo e le attività.</span><span class="sxs-lookup"><span data-stu-id="22c71-181">hello following example shows how toouse OData batch processing toocreate a job and tasks.</span></span> <span data-ttu-id="22c71-182">Per informazioni sull'elaborazione batch, vedere l'articolo relativo all' [elaborazione batch OData (Open Data Protocol)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="22c71-182">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="22c71-183">Creare un processo tramite JobTemplate</span><span class="sxs-lookup"><span data-stu-id="22c71-183">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="22c71-184">Quando si elabora più asset usando un set comune di attività, utilizzare che un'attività predefinita di entità JobTemplate toospecify hello predefiniti o ordine hello tooset delle attività.</span><span class="sxs-lookup"><span data-stu-id="22c71-184">When you process multiple assets by using a common set of tasks, use a JobTemplate toospecify hello default task presets, or tooset hello order of tasks.</span></span>

<span data-ttu-id="22c71-185">Hello di esempio seguente viene illustrato come toocreate un'entità JobTemplate con un'entità TaskTemplate che viene definito inline.</span><span class="sxs-lookup"><span data-stu-id="22c71-185">hello following example shows how toocreate a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="22c71-186">Hello entità TaskTemplate Usa hello Media Encoder Standard come file di asset hello tooencode hello entità MediaProcessor.</span><span class="sxs-lookup"><span data-stu-id="22c71-186">hello TaskTemplate uses hello Media Encoder Standard as hello MediaProcessor tooencode hello asset file.</span></span> <span data-ttu-id="22c71-187">Tuttavia, può usare anche altre entità Mediaprocessor.</span><span class="sxs-lookup"><span data-stu-id="22c71-187">However, other MediaProcessors can be used as well.</span></span>

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> <span data-ttu-id="22c71-188">A differenza di altre entità di servizi multimediali, è necessario definire un nuovo identificatore GUID per ogni entità TaskTemplate e posizionarlo nella proprietà hello taskTemplateId e Id nel corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="22c71-188">Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in hello taskTemplateId and Id property in your request body.</span></span> <span data-ttu-id="22c71-189">schema di identificazione del contenuto Hello deve seguire schema hello descritto nell'identificare le entità di Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="22c71-189">hello content identification scheme must follow hello scheme described in Identify Azure Media Services Entities.</span></span> <span data-ttu-id="22c71-190">Inoltre, non è possibile aggiornare le entità JobTemplate.</span><span class="sxs-lookup"><span data-stu-id="22c71-190">Also, JobTemplates cannot be updated.</span></span> <span data-ttu-id="22c71-191">È invece necessario crearne una nuova con le modifiche aggiornate.</span><span class="sxs-lookup"><span data-stu-id="22c71-191">Instead, you must create a new one with your updated changes.</span></span>
>
>

<span data-ttu-id="22c71-192">Se ha esito positivo, viene restituito hello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="22c71-192">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="22c71-193">Hello seguente esempio viene illustrato come un processo che fa riferimento a un Id entità JobTemplate toocreate:</span><span class="sxs-lookup"><span data-stu-id="22c71-193">hello following example shows how toocreate a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="22c71-194">Se ha esito positivo, viene restituito hello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="22c71-194">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a><span data-ttu-id="22c71-195">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="22c71-195">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="22c71-196">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="22c71-196">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="22c71-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="22c71-197">Next steps</span></span>
<span data-ttu-id="22c71-198">Ora che è stato appreso come toocreate tooencode un processo un asset, vedere [come toocheck processo lo stato di avanzamento con servizi multimediali](media-services-rest-check-job-progress.md).</span><span class="sxs-lookup"><span data-stu-id="22c71-198">Now that you know how toocreate a job tooencode an asset, see [How toocheck job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="22c71-199">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="22c71-199">See also</span></span>
[<span data-ttu-id="22c71-200">Ottenere processori di contenuti multimediali</span><span class="sxs-lookup"><span data-stu-id="22c71-200">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)

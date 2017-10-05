---
title: Come codificare un asset di Azure mediante Media Encoder Standard| Microsoft Docs
description: Informazioni su come usare Media Encoder Standard per codificare contenuti multimediali in Servizi multimediali di Azure. Negli esempi di codice viene usata l'API REST.
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
ms.openlocfilehash: 796f3b5a4dd56a0160986600cbbcf38faf8add56
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-encode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="1a2c9-104">Come codificare un asset mediante Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="1a2c9-104">How to encode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1a2c9-105">.NET</span><span class="sxs-lookup"><span data-stu-id="1a2c9-105">.NET</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [<span data-ttu-id="1a2c9-106">REST</span><span class="sxs-lookup"><span data-stu-id="1a2c9-106">REST</span></span>](media-services-rest-encode-asset.md)
> * [<span data-ttu-id="1a2c9-107">Portale</span><span class="sxs-lookup"><span data-stu-id="1a2c9-107">Portal</span></span>](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="1a2c9-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="1a2c9-108">Overview</span></span>
<span data-ttu-id="1a2c9-109">Per distribuire un video digitale in Internet è necessario comprimere il file multimediale.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-109">To deliver digital video over the Internet, you must compress the media.</span></span> <span data-ttu-id="1a2c9-110">I file video digitali hanno dimensioni piuttosto elevate e possono risultare troppo grandi per la distribuzione su Internet o per la visualizzazione corretta sui dispositivi dei clienti.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-110">Digital video files are large and may be too big to deliver over the Internet, or for your customers’ devices to display properly.</span></span> <span data-ttu-id="1a2c9-111">Mediante il processo di codifica è possibile comprimere video e audio per consentire ai clienti di visualizzare i file multimediali.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-111">Encoding is the process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="1a2c9-112">I processi di codifica sono tra le operazioni di elaborazione più frequenti in Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-112">Encoding jobs are one of the most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="1a2c9-113">Questi processi vengono creati per convertire i file multimediali da una codifica all'altra.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-113">You create encoding jobs to convert media files from one encoding to another.</span></span> <span data-ttu-id="1a2c9-114">Durante la codifica è possibile usare il codificatore multimediale incorporato in Servizi multimediali (Media Encoder Standard).</span><span class="sxs-lookup"><span data-stu-id="1a2c9-114">When you encode, you can use the Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="1a2c9-115">È inoltre possibile usare un codificatore fornito da un partner di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="1a2c9-116">I codificatori di terze parti sono disponibili tramite il Marketplace di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-116">Third-party encoders are available through the Azure Marketplace.</span></span> <span data-ttu-id="1a2c9-117">È possibile specificare i dettagli relativi alle attività di codifica usando stringhe di set di impostazioni definite per il codificatore oppure file di configurazione di set di impostazioni.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-117">You can specify the details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="1a2c9-118">Per i tipi di set di impostazioni disponibili, vedere [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960) (Set di impostazioni disponibili per Media Encoder Standard).</span><span class="sxs-lookup"><span data-stu-id="1a2c9-118">To see the types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="1a2c9-119">Ogni processo può includere una o più attività in base al tipo di elaborazione che si desidera eseguire.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-119">Each job can have one or more tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="1a2c9-120">Usando l'API REST è possibile creare i processi e le attività correlate procedendo in due modi diversi:</span><span class="sxs-lookup"><span data-stu-id="1a2c9-120">Through the REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="1a2c9-121">Le Attività possono essere definite in linea mediante la proprietà di navigazione attività nelle entità dei processi.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-121">Tasks can be defined inline through the Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="1a2c9-122">Usare l'elaborazione batch OData.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-122">Use OData batch processing.</span></span>

<span data-ttu-id="1a2c9-123">È consigliabile codificare sempre i file di origine in un set MP4 a velocità in bit adattiva e quindi convertire il set nel formato desiderato mediante la [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1a2c9-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert the set to the desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="1a2c9-124">Se l'asset di output è protetto con crittografia di archiviazione, è necessario configurare i criteri di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-124">If your output asset is storage encrypted, you must configure the asset delivery policy.</span></span> <span data-ttu-id="1a2c9-125">Per altre informazioni, vedere [Configurazione dei criteri di distribuzione degli asset](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="1a2c9-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="1a2c9-126">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="1a2c9-126">Considerations</span></span>

<span data-ttu-id="1a2c9-127">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="1a2c9-128">Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="1a2c9-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

<span data-ttu-id="1a2c9-129">Prima di iniziare a fare riferimento ai supporti multimediali, verificare di avere il corretto processore ID del supporto.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-129">Before you start referencing media processors, verify that you have the correct media processor ID.</span></span> <span data-ttu-id="1a2c9-130">Per altre informazioni, vedere [Ottenere processori di contenuti multimediali](media-services-rest-get-media-processor.md).</span><span class="sxs-lookup"><span data-stu-id="1a2c9-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="1a2c9-131">Connettersi a Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1a2c9-131">Connect to Media Services</span></span>

<span data-ttu-id="1a2c9-132">Per informazioni su come connettersi all'API AMS, vedere [Accedere all'API di Servizi multimediali di Azure con l'autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="1a2c9-132">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="1a2c9-133">Dopo avere stabilito la connessione a https://media.windows.net, si riceverà un reindirizzamento 301 che indica un altro URI di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-133">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="1a2c9-134">Le chiamate successive dovranno essere effettuate al nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-134">You must make subsequent calls to the new URI.</span></span>

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="1a2c9-135">Creare un processo con una singola attività di codifica</span><span class="sxs-lookup"><span data-stu-id="1a2c9-135">Create a job with a single encoding task</span></span>
> [!NOTE]
> <span data-ttu-id="1a2c9-136">Quando si usa l'API REST di Servizi multimediali, tenere presenti le seguenti considerazioni:</span><span class="sxs-lookup"><span data-stu-id="1a2c9-136">When you're working with the Media Services REST API, the following considerations apply:</span></span>
>
> <span data-ttu-id="1a2c9-137">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-137">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="1a2c9-138">Per altre informazioni, vedere [Configurazione dello sviluppo dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="1a2c9-138">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span></span>
>
> <span data-ttu-id="1a2c9-139">Dopo avere stabilito la connessione a https://media.windows.net, si riceverà un reindirizzamento 301 che indica un altro URI di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-139">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="1a2c9-140">Le chiamate successive dovranno essere effettuate al nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-140">You must make subsequent calls to the new URI.</span></span> <span data-ttu-id="1a2c9-141">Per informazioni su come connettersi all'API AMS, vedere [Accedere all'API di Servizi multimediali di Azure con l'autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="1a2c9-141">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
>
> <span data-ttu-id="1a2c9-142">Se si usa JSON e si specifica di usare la parola chiave **__metadata** nella richiesta (ad esempio, per fare riferimento a un oggetto collegato) è necessario impostare l'intestazione **Accetta** sul [formato JSON Verbose](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accetta: application/json;odata=verbose.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-142">When using JSON and specifying to use the **__metadata** keyword in the request (for example, to references a linked object), you must set the **Accept** header to [JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span></span>
>
>

<span data-ttu-id="1a2c9-143">Il seguente esempio mostra come creare e pubblicare un processo con un'attività impostata per codificare un video con determinati valori di risoluzione e qualità.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-143">The following example shows you how to create and post a job with one task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="1a2c9-144">Quando si esegue la codifica con Media Encoder Standard, è possibile usare i set di impostazioni di attività specificati [qui](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="1a2c9-144">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="1a2c9-145">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="1a2c9-145">Request:</span></span>

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

<span data-ttu-id="1a2c9-146">Risposta:</span><span class="sxs-lookup"><span data-stu-id="1a2c9-146">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-the-output-assets-name"></a><span data-ttu-id="1a2c9-147">Impostare il nome dell'asset di output</span><span class="sxs-lookup"><span data-stu-id="1a2c9-147">Set the output asset's name</span></span>
<span data-ttu-id="1a2c9-148">Il seguente esempio mostra impostare l'attributo assetName:</span><span class="sxs-lookup"><span data-stu-id="1a2c9-148">The following example shows how to set the assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="1a2c9-149">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="1a2c9-149">Considerations</span></span>
* <span data-ttu-id="1a2c9-150">Le proprietà TaskBody devono usare codice XML letterale per definire il numero di asset di input o di output che vengono usati dall'attività.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-150">TaskBody properties must use literal XML to define the number of input, or output assets that are used by the task.</span></span> <span data-ttu-id="1a2c9-151">L'argomento Task contiene la definizione dello schema XML per il codice XML.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-151">The task topic contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="1a2c9-152">Nella definizione TaskBody ogni valore interno per <inputAsset> e <outputAsset>deve essere impostato come JobInputAsset(value) o JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="1a2c9-152">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="1a2c9-153">Un'attività può avere più asset di output.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-153">A task can have multiple output assets.</span></span> <span data-ttu-id="1a2c9-154">Un oggetto JobOutputAsset(x) può essere usato solo una volta come output di un'attività in un processo.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-154">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="1a2c9-155">È possibile specificare JobInputAsset o JobOutputAsset come asset di input di un'attività.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-155">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="1a2c9-156">Le attività non devono formare un ciclo.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-156">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="1a2c9-157">Il parametro del valore passato a JobInputAsset o JobOutputAsset rappresenta il valore di indice di un asset.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-157">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an asset.</span></span> <span data-ttu-id="1a2c9-158">Gli asset effettivi vengono definiti nelle proprietà di navigazione InputMediaAssets e OutputMediaAssets nella definizione dell'entità del processo.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-158">The actual assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the job entity definition.</span></span>
* <span data-ttu-id="1a2c9-159">Poiché Servizi multimediali si basa su OData versione 3, i riferimenti ai singoli asset nelle raccolte delle proprietà di navigazione InputMediaAssets e OutputMediaAssets vengono definiti mediante una coppia nome/valore "__metadata : uri".</span><span class="sxs-lookup"><span data-stu-id="1a2c9-159">Because Media Services is built on OData v3, the individual assets in the InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
* <span data-ttu-id="1a2c9-160">InputMediaAssets è mappata a uno o più asset creati in Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-160">InputMediaAssets maps to one or more assets that you created in Media Services.</span></span> <span data-ttu-id="1a2c9-161">Le proprietà OutputMediaAssets vengono create dal sistema.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-161">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="1a2c9-162">Non fanno riferimento a un asset esistente.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-162">They don't reference an existing asset.</span></span>
* <span data-ttu-id="1a2c9-163">Per assegnare un nome a OutputMediaAssets è possibile usare l'attributo assetName.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-163">OutputMediaAssets can be named by using the assetName attribute.</span></span> <span data-ttu-id="1a2c9-164">Se questo attributo non è presente, il nome della proprietà OutputMediaAssets corrisponde al valore del testo interno dell'elemento <outputAsset> preceduto dal nome o dall'ID del processo, nel caso in cui la proprietà Name non sia definita.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-164">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="1a2c9-165">Se ad esempio si è impostato "Sample" come valore di assetName, la proprietà Name di OutputMediaAssets sarà impostata su "Sample".</span><span class="sxs-lookup"><span data-stu-id="1a2c9-165">For example, if you set a value for assetName to "Sample," then the OutputMediaAsset Name property is set to "Sample."</span></span> <span data-ttu-id="1a2c9-166">Se invece non si è impostato un valore per assetName, ma si è impostato "NewJob" come nome del processo, il nome di OutputMediaAssets sarà "JobOutputAsset(value)_NewJob".</span><span class="sxs-lookup"><span data-stu-id="1a2c9-166">However, if you didn't set a value for assetName, but did set the job name to "NewJob," then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="1a2c9-167">Creare un processo con attività concatenate</span><span class="sxs-lookup"><span data-stu-id="1a2c9-167">Create a job with chained tasks</span></span>
<span data-ttu-id="1a2c9-168">In molti scenari di applicazione, gli sviluppatori desiderano creare una serie di attività di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-168">In many application scenarios, developers want to create a series of processing tasks.</span></span> <span data-ttu-id="1a2c9-169">In Servizi multimediali è possibile creare una serie di attività concatenate.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-169">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="1a2c9-170">Ogni attività esegue diversi passaggi di elaborazione e può usare processori di contenuti multimediali differenti.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-170">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="1a2c9-171">Le attività concatenate possono trasferire un asset da un'attività a un'altra e consentono quindi l'esecuzione delle attività dell'asset in sequenza lineare.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-171">The chained tasks can hand off an asset from one task to another, performing a linear sequence of tasks on the asset.</span></span> <span data-ttu-id="1a2c9-172">Tuttavia, non è necessario che le attività eseguite in un processo siano in sequenza.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-172">However, the tasks performed in a job are not required to be in a sequence.</span></span> <span data-ttu-id="1a2c9-173">Quando si crea un'attività concatenata, gli oggetti **ITask** concatenati vengono creati in un singolo oggetto **IJob**.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-173">When you create a chained task, the chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> <span data-ttu-id="1a2c9-174">Attualmente è previsto un limite di 30 attività per processo.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-174">There is currently a limit of 30 tasks per job.</span></span> <span data-ttu-id="1a2c9-175">Se è necessario concatenare più di 30 attività, creare più processi in modo da contenerle tutte.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-175">If you need to chain more than 30 tasks, create more than one job to contain the tasks.</span></span>
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


### <a name="considerations"></a><span data-ttu-id="1a2c9-176">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="1a2c9-176">Considerations</span></span>
<span data-ttu-id="1a2c9-177">Per abilitare il concatenamento di attività:</span><span class="sxs-lookup"><span data-stu-id="1a2c9-177">To enable task chaining:</span></span>

* <span data-ttu-id="1a2c9-178">Un processo deve avere almeno due attività.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-178">A job must have at least two tasks.</span></span>
* <span data-ttu-id="1a2c9-179">Deve essere presente almeno un'attività il cui input viene usato come output di un'altra attività nel processo.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-179">There must be at least one task whose input is the output of another task in the job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="1a2c9-180">Utilizzare l'elaborazione batch OData</span><span class="sxs-lookup"><span data-stu-id="1a2c9-180">Use OData batch processing</span></span>
<span data-ttu-id="1a2c9-181">Nell'esempio seguente viene illustrato come utilizzare l'elaborazione batch OData per creare un processo e un’attività.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-181">The following example shows how to use OData batch processing to create a job and tasks.</span></span> <span data-ttu-id="1a2c9-182">Per informazioni sull'elaborazione batch, vedere l'articolo relativo all' [elaborazione batch OData (Open Data Protocol)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="1a2c9-182">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

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



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="1a2c9-183">Creare un processo tramite JobTemplate</span><span class="sxs-lookup"><span data-stu-id="1a2c9-183">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="1a2c9-184">Quando si elaborano più asset usando un set comune di attività, usare JobTemplate per specificare le impostazioni di attività predefinite o per impostare l'ordine delle attività.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-184">When you process multiple assets by using a common set of tasks, use a JobTemplate to specify the default task presets, or to set the order of tasks.</span></span>

<span data-ttu-id="1a2c9-185">L'esempio seguente mostra come creare JobTemplate con un'entità TaskTemplate definita inline.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-185">The following example shows how to create a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="1a2c9-186">L'entità TaskTemplate usa Media Encoder Standard come entità MediaProcessor per codificare il file di asset.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-186">The TaskTemplate uses the Media Encoder Standard as the MediaProcessor to encode the asset file.</span></span> <span data-ttu-id="1a2c9-187">Tuttavia, può usare anche altre entità Mediaprocessor.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-187">However, other MediaProcessors can be used as well.</span></span>

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
> <span data-ttu-id="1a2c9-188">A differenza di altre entità di Servizi multimediali, è necessario definire un nuovo identificatore GUID per ogni entità TaskTemplate e inserirlo nel corpo della richiesta in taskTemplateId e nella proprietà Id.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-188">Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in the taskTemplateId and Id property in your request body.</span></span> <span data-ttu-id="1a2c9-189">Lo schema di identificazione del contenuto deve seguire lo schema descritto in Identificare le entità di Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-189">The content identification scheme must follow the scheme described in Identify Azure Media Services Entities.</span></span> <span data-ttu-id="1a2c9-190">Inoltre, non è possibile aggiornare le entità JobTemplate.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-190">Also, JobTemplates cannot be updated.</span></span> <span data-ttu-id="1a2c9-191">È invece necessario crearne una nuova con le modifiche aggiornate.</span><span class="sxs-lookup"><span data-stu-id="1a2c9-191">Instead, you must create a new one with your updated changes.</span></span>
>
>

<span data-ttu-id="1a2c9-192">Se l'esito è positivo, viene restituita la seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="1a2c9-192">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="1a2c9-193">L'esempio seguente mostra come creare un processo che fa riferimento all'ID di un'entità JobTemplate:</span><span class="sxs-lookup"><span data-stu-id="1a2c9-193">The following example shows how to create a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="1a2c9-194">Se l'esito è positivo, viene restituita la seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="1a2c9-194">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a><span data-ttu-id="1a2c9-195">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1a2c9-195">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1a2c9-196">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="1a2c9-196">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="1a2c9-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1a2c9-197">Next steps</span></span>
<span data-ttu-id="1a2c9-198">Dopo aver spiegato il processo per la codifica di un asset, si può passare all'argomento [Procedura per controllare lo stato dei processi con Servizi multimediali](media-services-rest-check-job-progress.md).</span><span class="sxs-lookup"><span data-stu-id="1a2c9-198">Now that you know how to create a job to encode an asset, see [How to check job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="1a2c9-199">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a2c9-199">See also</span></span>
[<span data-ttu-id="1a2c9-200">Ottenere processori di contenuti multimediali</span><span class="sxs-lookup"><span data-stu-id="1a2c9-200">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)

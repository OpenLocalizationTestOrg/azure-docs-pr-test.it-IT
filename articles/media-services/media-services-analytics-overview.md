---
title: Analisi Servizi multimediali nella piattaforma Servizi multimediali | Microsoft Docs
description: "Una panoramica dell'anteprima pubblica di Analisi Servizi multimediali, una serie di servizi di riconoscimento vocale e visione artificiale per scalabilità, conformità, sicurezza e copertura globale per le aziende"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: c0bbe6f80370515fa783b12757434897fe2221b6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="media-analytics-on-the-media-services-platform"></a><span data-ttu-id="92cfa-103">Analisi Servizi multimediali nella piattaforma Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="92cfa-103">Media Analytics on the Media Services platform</span></span>
## <a name="overview"></a><span data-ttu-id="92cfa-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="92cfa-104">Overview</span></span>
<span data-ttu-id="92cfa-105">Sempre più organizzazioni adottano i video come mezzo per formare i dipendenti, coinvolgere i clienti e documentare le funzioni aziendali.</span><span class="sxs-lookup"><span data-stu-id="92cfa-105">More organizations are using video as the preferred medium to train their employees, engage their customers, and document business functions.</span></span> <span data-ttu-id="92cfa-106">Il cloud computing consente di archiviare e riprodurre in streaming questi file multimediali di grandi dimensioni, nonché di accedervi.</span><span class="sxs-lookup"><span data-stu-id="92cfa-106">Cloud computing provides a way to store, stream, and access these large media files.</span></span> <span data-ttu-id="92cfa-107">Tuttavia, man mano che la libreria aziendale di contenuti video aumenta, è necessario un mezzo altrettanto efficace per estrarre informazioni dal contenuto.</span><span class="sxs-lookup"><span data-stu-id="92cfa-107">But as a company's library of video content grows, it needs an equally effective means of extracting insights from the content.</span></span> 

<span data-ttu-id="92cfa-108">Per soddisfare questa esigenza in crescita, i Servizi multimediali di Azure offrono Analisi Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="92cfa-108">To address this growing need, Azure Media Services offers Azure Media Analytics.</span></span> <span data-ttu-id="92cfa-109">Analisi Servizi multimediali è una raccolta di componenti per sintesi vocale e visione artificiale che permettono a organizzazioni e aziende di derivare in modo più semplice analisi approfondite di utilità pratica dai loro file video.</span><span class="sxs-lookup"><span data-stu-id="92cfa-109">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises to derive actionable insights from their video files.</span></span> <span data-ttu-id="92cfa-110">Analisi Servizi multimediali, una soluzione creata usando i componenti principali della piattaforma Servizi multimediali, può iniziare fin da subito a elaborare i file multimediali su larga scala.</span><span class="sxs-lookup"><span data-stu-id="92cfa-110">Built by using the core Media Services platform components, Media Analytics can handle media processing at scale on day one.</span></span>

<span data-ttu-id="92cfa-111">Con Analisi Servizi multimediali, gli sviluppatori possono introdurre rapidamente funzionalità video avanzate nelle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="92cfa-111">With Media Analytics, developers can quickly bring advanced video functionality into applications.</span></span> <span data-ttu-id="92cfa-112">Questa soluzione offre agli ambienti aziendali scalabilità, conformità, sicurezza e copertura globale complete necessarie per organizzazioni di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="92cfa-112">It provides enterprise environments with the full scale, compliance, security, and global reach required by large organizations.</span></span>

<span data-ttu-id="92cfa-113">Il diagramma seguente mostra Analisi Servizi multimediali e altre parti importanti della piattaforma Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="92cfa-113">The following diagram shows Media Analytics and other major parts of the Media Services platform.</span></span> 

![Flusso di lavoro VoD](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

<span data-ttu-id="92cfa-115">I processori di contenuti multimediali di Analisi Servizi multimediali producono file MP4 o JSON.</span><span class="sxs-lookup"><span data-stu-id="92cfa-115">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="92cfa-116">Se un processore di contenuti multimediali produce un file MP4, è possibile scaricare progressivamente il file.</span><span class="sxs-lookup"><span data-stu-id="92cfa-116">If a media processor produces an MP4 file, you can progressively download the file.</span></span> <span data-ttu-id="92cfa-117">Se un processore di contenuti multimediali produce un file JSON, è possibile scaricare il file dall'Archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="92cfa-117">If a media processor produces a JSON file, you can download the file from Azure Blob storage.</span></span> 

## <a name="media-analytics-services"></a><span data-ttu-id="92cfa-118">Servizi di Analisi Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="92cfa-118">Media Analytics services</span></span>

### <a name="indexer"></a><span data-ttu-id="92cfa-119">Indexer</span><span class="sxs-lookup"><span data-stu-id="92cfa-119">Indexer</span></span>
<span data-ttu-id="92cfa-120">Azure Media Indexer consente di rendere disponibili per la ricerca i contenuti, oltre a generare tracce per i sottotitoli codificati.</span><span class="sxs-lookup"><span data-stu-id="92cfa-120">With Azure Media Indexer, you can make content searchable and generate closed-captioning tracks.</span></span> <span data-ttu-id="92cfa-121">Rispetto alla versione precedente, Azure Media Indexer 2 Preview offre prestazioni di indicizzazione superiori e un più ampio supporto di lingue.</span><span class="sxs-lookup"><span data-stu-id="92cfa-121">Compared to the previous version, Azure Media Indexer 2 Preview has faster indexing and broader language support.</span></span> <span data-ttu-id="92cfa-122">Le lingue supportate includono inglese, spagnolo, francese, tedesco, italiano, cinese, portoghese e arabo.</span><span class="sxs-lookup"><span data-stu-id="92cfa-122">Supported languages include English, Spanish, French, German, Italian, Chinese, Portuguese, and Arabic.</span></span> <span data-ttu-id="92cfa-123">Per informazioni dettagliate ed esempi, vedere [Elaborare video con Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span><span class="sxs-lookup"><span data-stu-id="92cfa-123">For detailed information and examples, see [Process videos with Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span></span>
### <a name="hyperlapse"></a><span data-ttu-id="92cfa-124">Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="92cfa-124">Hyperlapse</span></span>
<span data-ttu-id="92cfa-125">Microsoft Hyperlapse combina la stabilizzazione video e la funzionalità di time-lapse per creare brevi video visualizzabili partendo da contenuti in formato esteso.</span><span class="sxs-lookup"><span data-stu-id="92cfa-125">Microsoft Hyperlapse combines video stabilization and time-lapse capability to create quick, consumable videos from your long-form content.</span></span> <span data-ttu-id="92cfa-126">Oltre alla creazione di video time-lapse, è anche possibile usare Hyperlapse per creare video stabili da video traballanti girati con telefoni cellulari e videocamere.</span><span class="sxs-lookup"><span data-stu-id="92cfa-126">Besides creating time-lapse video, you can use Hyperlapse to create stable videos from shaky videos captured via cell phones and camcorders.</span></span> <span data-ttu-id="92cfa-127">Per informazioni dettagliate ed esempi, vedere [File multimediali di Hyperlapse con Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span><span class="sxs-lookup"><span data-stu-id="92cfa-127">For detailed information and examples, see [Hyperlapse media files with Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span></span>
### <a name="motion-detector"></a><span data-ttu-id="92cfa-128">Motion Detector</span><span class="sxs-lookup"><span data-stu-id="92cfa-128">Motion Detector</span></span>
<span data-ttu-id="92cfa-129">È possibile usare Motion Detector per rilevare i movimenti in un video con sfondi fissi.</span><span class="sxs-lookup"><span data-stu-id="92cfa-129">You can use Motion Detector to detect motion in a video with stationary backgrounds.</span></span> <span data-ttu-id="92cfa-130">Questo rende possibile per verificare la presenza di falsi positivi in eventi di movimento rilevati da videocamere di sorveglianza.</span><span class="sxs-lookup"><span data-stu-id="92cfa-130">This makes it possible to check for false positives on motion events detected by surveillance cameras.</span></span> <span data-ttu-id="92cfa-131">Per informazioni dettagliate ed esempi, vedere [Rilevamento dei movimenti per Analisi Servizi multimediali di Azure](media-services-motion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="92cfa-131">For detailed information and examples, see [Motion detection for Azure Media Analytics](media-services-motion-detection.md).</span></span>
### <a name="face-detector"></a><span data-ttu-id="92cfa-132">Face Detector</span><span class="sxs-lookup"><span data-stu-id="92cfa-132">Face Detector</span></span>
<span data-ttu-id="92cfa-133">Grazie all'uso di Face Detector, è possibile individuare i volti delle persone e le relative emozioni, ad esempio felicità, tristezza e sorpresa.</span><span class="sxs-lookup"><span data-stu-id="92cfa-133">By using Face Detector, you can detect people’s faces and their emotions, including happiness, sadness, and surprise.</span></span> <span data-ttu-id="92cfa-134">Questa funzionalità vanta numerose applicazioni utili nel settore, descritte di seguito, tra cui l'aggregazione e l'analisi delle reazioni delle persone che partecipano a un evento.</span><span class="sxs-lookup"><span data-stu-id="92cfa-134">This has several useful industry applications, described later, including aggregating and analyzing reactions of people attending an event.</span></span> <span data-ttu-id="92cfa-135">Per informazioni dettagliate ed esempi, vedere [Rilevamento di volti ed emozioni per Analisi Servizi multimediali di Azure](media-services-face-and-emotion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="92cfa-135">For detailed information and examples, see [Face and emotion detection for Azure Media Analytics](media-services-face-and-emotion-detection.md).</span></span>
### <a name="video-summarization"></a><span data-ttu-id="92cfa-136">Riepilogo video</span><span class="sxs-lookup"><span data-stu-id="92cfa-136">Video summarization</span></span>
<span data-ttu-id="92cfa-137">Il riepilogo video consente di creare un riepilogo per video lunghi selezionando in modo automatico frammenti interessanti del video di origine.</span><span class="sxs-lookup"><span data-stu-id="92cfa-137">Video summarization can help you create summaries of long videos by automatically selecting interesting snippets from the source video.</span></span> <span data-ttu-id="92cfa-138">Questa funzione risulta particolarmente utile quando si intende creare una panoramica rapida dei contenuti offerti nella versione più lunga del video.</span><span class="sxs-lookup"><span data-stu-id="92cfa-138">This ability is useful when you want to provide a quick overview of what to expect in a long video.</span></span> <span data-ttu-id="92cfa-139">Per informazioni dettagliate ed esempi, vedere [Uso di Azure Media Video Thumbnails per creare un riepilogo video](media-services-video-summarization.md).</span><span class="sxs-lookup"><span data-stu-id="92cfa-139">For detailed information and examples, see [Use Azure Media Video Thumbnails to create video summarization](media-services-video-summarization.md).</span></span>
### <a name="optical-character-recognition"></a><span data-ttu-id="92cfa-140">Riconoscimento ottico dei caratteri</span><span class="sxs-lookup"><span data-stu-id="92cfa-140">Optical character recognition</span></span>
<span data-ttu-id="92cfa-141">Il riconoscimento ottico dei caratteri (OCR) di Analisi Servizi multimediali di Azure consente di convertire il contenuto di testo dei file video in testo digitale modificabile e sui cui è possibile eseguire ricerche.</span><span class="sxs-lookup"><span data-stu-id="92cfa-141">With Azure Media OCR (optical character recognition), you can convert text content in video files into editable, searchable digital text.</span></span> <span data-ttu-id="92cfa-142">È possibile automatizzare così l'estrazione di metadati importanti dal segnale video del contenuto multimediale.</span><span class="sxs-lookup"><span data-stu-id="92cfa-142">You can then automate the extraction of meaningful metadata from the video signal of your media.</span></span>
### <a name="scalable-face-redaction"></a><span data-ttu-id="92cfa-143">Offuscamento dei volti scalabile</span><span class="sxs-lookup"><span data-stu-id="92cfa-143">Scalable face redaction</span></span>
<span data-ttu-id="92cfa-144">Azure Media Redactor è un processore di contenuti multimediali di Analisi Servizi multimediali di Azure che offre funzionalità scalabili di offuscamento dei volti nel cloud.</span><span class="sxs-lookup"><span data-stu-id="92cfa-144">Azure Media Redactor is a Media Analytics media processor that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="92cfa-145">Usando l'offuscamento dei volti è possibile modificare un video per sfocare i volti di persone selezionate.</span><span class="sxs-lookup"><span data-stu-id="92cfa-145">By using face redaction, you can modify your video to blur faces of selected individuals.</span></span> <span data-ttu-id="92cfa-146">Si potrebbe scegliere di usare tale servizio in scenari di notizie giornalistiche o pubblica sicurezza.</span><span class="sxs-lookup"><span data-stu-id="92cfa-146">You might want to use the face redaction service in news media or when public safety is involved.</span></span> <span data-ttu-id="92cfa-147">Offuscare manualmente alcuni minuti di filmato contenenti più volti può richiedere ore, ma con questo servizio l'offuscamento dei volti richiederà pochi semplici passaggi.</span><span class="sxs-lookup"><span data-stu-id="92cfa-147">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service, face redaction takes just a few simple steps.</span></span> <span data-ttu-id="92cfa-148">Per altre informazioni, vedere l'articolo [Offuscare i volti con Analisi Servizi multimediali di Azure](media-services-face-redaction.md).</span><span class="sxs-lookup"><span data-stu-id="92cfa-148">For more information, see the [Redact faces with Azure Media Analytics](media-services-face-redaction.md) article.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="92cfa-149">Scenari comuni</span><span class="sxs-lookup"><span data-stu-id="92cfa-149">Common scenarios</span></span>
<span data-ttu-id="92cfa-150">Analisi Servii multimediali può aiutare le organizzazioni e le aziende a scoprire nuovi orizzonti nel mondo dei video e gestire più efficacemente grandi volumi di contenuti video.</span><span class="sxs-lookup"><span data-stu-id="92cfa-150">Media Analytics can help organizations and enterprises glean new insights from video and more effectively manage large volumes of video content.</span></span> <span data-ttu-id="92cfa-151">Di seguito sono descritti diversi scenari:</span><span class="sxs-lookup"><span data-stu-id="92cfa-151">Here are several scenarios:</span></span>

* <span data-ttu-id="92cfa-152">**Call center**.</span><span class="sxs-lookup"><span data-stu-id="92cfa-152">**Call centers**.</span></span> <span data-ttu-id="92cfa-153">Anche con l'avvento dei social media, i call center dedicati ai clienti continuano a ospitare un'alta percentuale delle transazioni del servizio clienti.</span><span class="sxs-lookup"><span data-stu-id="92cfa-153">Even with the advent of social media, customer call centers still facilitate a large percentage of customer-service transactions.</span></span> <span data-ttu-id="92cfa-154">In questi dati audio sono codificate numerose informazioni sui clienti che possono essere analizzate per ottenere una maggiore soddisfazione del cliente.</span><span class="sxs-lookup"><span data-stu-id="92cfa-154">Encoded in this audio data is a large amount of customer information that can be analyzed to achieve higher customer satisfaction.</span></span> <span data-ttu-id="92cfa-155">Con Media Indexer, le organizzazioni possono estrarre il testo e creare indici di ricerca e dashboard.</span><span class="sxs-lookup"><span data-stu-id="92cfa-155">By using Media Indexer, organizations can extract text and build search indexes and dashboards.</span></span> <span data-ttu-id="92cfa-156">Possono quindi estrarre informazioni su reclami comuni, origini dei reclami e altri dati rilevanti.</span><span class="sxs-lookup"><span data-stu-id="92cfa-156">Then they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span></span>
* <span data-ttu-id="92cfa-157">**Moderazione dei contenuti generati dall'utente**.</span><span class="sxs-lookup"><span data-stu-id="92cfa-157">**User-generated content moderation**.</span></span> <span data-ttu-id="92cfa-158">Molte organizzazioni, dalle agenzie di stampa ai dipartimenti di polizia, dispongono di portali pubblici che accettano file multimediali generati dagli utenti, ad esempio immagini e video.</span><span class="sxs-lookup"><span data-stu-id="92cfa-158">From news media outlets to police departments, many organizations have public-facing portals that accept user-generated media such as videos and images.</span></span> <span data-ttu-id="92cfa-159">A causa di eventi imprevisti, il volume dei contenuti potrebbe raggiungere il limite.</span><span class="sxs-lookup"><span data-stu-id="92cfa-159">The volume of content can spike due to unexpected events.</span></span> <span data-ttu-id="92cfa-160">In questi scenari è difficile eseguire un efficace controllo manuale sull'adeguatezza dei contenuti.</span><span class="sxs-lookup"><span data-stu-id="92cfa-160">In these scenarios, it is difficult to conduct effective manual reviews of content for appropriateness.</span></span> <span data-ttu-id="92cfa-161">I clienti possono fare affidamento sul servizio di moderazione dei contenuti per concentrare l'attenzione sui contenuti appropriati.</span><span class="sxs-lookup"><span data-stu-id="92cfa-161">Customers can rely on the content-moderation service to focus on content that is appropriate.</span></span>
* <span data-ttu-id="92cfa-162">**Sorveglianza**.</span><span class="sxs-lookup"><span data-stu-id="92cfa-162">**Surveillance**.</span></span> <span data-ttu-id="92cfa-163">L'incremento nell'uso di telecamere IP comporta un aumento nell'inventario dei video di sorveglianza.</span><span class="sxs-lookup"><span data-stu-id="92cfa-163">With the growth in use of IP cameras comes a growing inventory of surveillance video.</span></span> <span data-ttu-id="92cfa-164">Il controllo manuale dei video di sorveglianza richiede molto tempo ed è soggetto a errori umani.</span><span class="sxs-lookup"><span data-stu-id="92cfa-164">Manually reviewing surveillance video is time intensive and prone to human error.</span></span> <span data-ttu-id="92cfa-165">Analisi Servizi multimediali offre servizi come il rilevamento dei movimenti, il rilevamento viso e Hyperlapse per agevolare il processo di controllo, gestione e creazione dei derivati.</span><span class="sxs-lookup"><span data-stu-id="92cfa-165">Media Analytics provides services such as motion detection, face detection, and Hyperlapse to make the process of reviewing, managing, and creating derivatives easier.</span></span>

## <a name="media-analytics-media-processors"></a><span data-ttu-id="92cfa-166">Processori di contenuti multimediali di Analisi Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="92cfa-166">Media Analytics media processors</span></span>
<span data-ttu-id="92cfa-167">Questa sezione elenca tutti i processori di contenuti multimediali di Analisi Servizi multimediali e illustra come usare .NET o REST per ottenere un oggetto dei processori di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="92cfa-167">This section lists the Media Analytics media processors and shows how to use .NET or REST to get a media processor (MP) object.</span></span>

### <a name="mp-names"></a><span data-ttu-id="92cfa-168">Nomi dei processori di contenuti multimediali</span><span class="sxs-lookup"><span data-stu-id="92cfa-168">MP names</span></span>
* <span data-ttu-id="92cfa-169">Azure Media Indexer 2 Preview</span><span class="sxs-lookup"><span data-stu-id="92cfa-169">Azure Media Indexer 2 Preview</span></span>
* <span data-ttu-id="92cfa-170">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="92cfa-170">Azure Media Indexer</span></span>
* <span data-ttu-id="92cfa-171">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="92cfa-171">Azure Media Hyperlapse</span></span>
* <span data-ttu-id="92cfa-172">Rilevamento multimediale volti di Azure</span><span class="sxs-lookup"><span data-stu-id="92cfa-172">Azure Media Face Detector</span></span>
* <span data-ttu-id="92cfa-173">Rilevatore multimediale di movimento Azure</span><span class="sxs-lookup"><span data-stu-id="92cfa-173">Azure Media Motion Detector</span></span>
* <span data-ttu-id="92cfa-174">Anteprime video multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="92cfa-174">Azure Media Video Thumbnails</span></span>
* <span data-ttu-id="92cfa-175">Riconoscimento ottico dei caratteri multimediale di Azure</span><span class="sxs-lookup"><span data-stu-id="92cfa-175">Azure Media OCR</span></span>

### <a name="net"></a><span data-ttu-id="92cfa-176">.NET</span><span class="sxs-lookup"><span data-stu-id="92cfa-176">.NET</span></span>
<span data-ttu-id="92cfa-177">La funzione seguente acquisisce uno dei nomi di processori di contenuti multimediali specificati e restituisce un oggetto.</span><span class="sxs-lookup"><span data-stu-id="92cfa-177">The following function takes one of the specified MP names and returns an MP object.</span></span>

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }


### <a name="rest"></a><span data-ttu-id="92cfa-178">REST</span><span class="sxs-lookup"><span data-stu-id="92cfa-178">REST</span></span>
<span data-ttu-id="92cfa-179">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="92cfa-179">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

<span data-ttu-id="92cfa-180">Risposta:</span><span class="sxs-lookup"><span data-stu-id="92cfa-180">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a><span data-ttu-id="92cfa-181">Demo</span><span class="sxs-lookup"><span data-stu-id="92cfa-181">Demos</span></span>
<span data-ttu-id="92cfa-182">Vedere le [demo di Analisi Servizi multimediali di Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span><span class="sxs-lookup"><span data-stu-id="92cfa-182">See [Azure Media Analytics demos](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="92cfa-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="92cfa-183">Next steps</span></span>
<span data-ttu-id="92cfa-184">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="92cfa-184">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="92cfa-185">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="92cfa-185">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="92cfa-186">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="92cfa-186">Related articles</span></span>
<span data-ttu-id="92cfa-187">Vedere l'[annuncio di Analisi Servizi multimediali di Azure](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span><span class="sxs-lookup"><span data-stu-id="92cfa-187">See [Media Services Analytics announcement](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span></span>

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png

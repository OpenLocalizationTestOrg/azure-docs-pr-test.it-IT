---
title: aaaMedia Analitica nella piattaforma di servizi multimediali hello | Documenti Microsoft
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
ms.openlocfilehash: 7545f0532d7618164ebe65e2f4232c5f63453cfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="media-analytics-on-hello-media-services-platform"></a><span data-ttu-id="f148b-103">Supporto Analitica nella piattaforma di servizi multimediali hello</span><span class="sxs-lookup"><span data-stu-id="f148b-103">Media Analytics on hello Media Services platform</span></span>
## <a name="overview"></a><span data-ttu-id="f148b-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f148b-104">Overview</span></span>
<span data-ttu-id="f148b-105">Altre organizzazioni utilizzano video come hello tootrain medium preferito ai dipendenti, coinvolgere clienti e le funzioni di business di documento.</span><span class="sxs-lookup"><span data-stu-id="f148b-105">More organizations are using video as hello preferred medium tootrain their employees, engage their customers, and document business functions.</span></span> <span data-ttu-id="f148b-106">Il cloud computing offre un modo toostore, flusso e accedere a questi file multimediali di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="f148b-106">Cloud computing provides a way toostore, stream, and access these large media files.</span></span> <span data-ttu-id="f148b-107">Tuttavia, man mano che aumenta la libreria di una società di contenuto video, è necessario un altrettanto efficace di estrarre informazioni dal contenuto hello.</span><span class="sxs-lookup"><span data-stu-id="f148b-107">But as a company's library of video content grows, it needs an equally effective means of extracting insights from hello content.</span></span> 

<span data-ttu-id="f148b-108">tooaddress questa esigenza in crescita, servizi multimediali di Azure offre Analitica multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f148b-108">tooaddress this growing need, Azure Media Services offers Azure Media Analytics.</span></span> <span data-ttu-id="f148b-109">Supporto Analitica è una raccolta di componenti di riconoscimento vocale e visione che rende più semplice per aziende e organizzazioni tooderive ricavare informazioni utili dai propri file video.</span><span class="sxs-lookup"><span data-stu-id="f148b-109">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="f148b-110">Per la compilazione di componenti della piattaforma di servizi multimediali core hello, supporto Analitica può gestire media di elaborazione su larga scala il primo giorno.</span><span class="sxs-lookup"><span data-stu-id="f148b-110">Built by using hello core Media Services platform components, Media Analytics can handle media processing at scale on day one.</span></span>

<span data-ttu-id="f148b-111">Con Analisi Servizi multimediali, gli sviluppatori possono introdurre rapidamente funzionalità video avanzate nelle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="f148b-111">With Media Analytics, developers can quickly bring advanced video functionality into applications.</span></span> <span data-ttu-id="f148b-112">Fornisce gli ambienti aziendali con scala completo hello, conformità, sicurezza e la portata globale richiesto da organizzazioni di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="f148b-112">It provides enterprise environments with hello full scale, compliance, security, and global reach required by large organizations.</span></span>

<span data-ttu-id="f148b-113">Hello seguente diagramma illustra Analitica Media e altre parti principali della piattaforma di servizi multimediali hello.</span><span class="sxs-lookup"><span data-stu-id="f148b-113">hello following diagram shows Media Analytics and other major parts of hello Media Services platform.</span></span> 

![Flusso di lavoro VoD](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

<span data-ttu-id="f148b-115">I processori di contenuti multimediali di Analisi Servizi multimediali producono file MP4 o JSON.</span><span class="sxs-lookup"><span data-stu-id="f148b-115">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="f148b-116">Se un processore di contenuti multimediali produce un file MP4, è possibile scaricare progressivamente file hello.</span><span class="sxs-lookup"><span data-stu-id="f148b-116">If a media processor produces an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="f148b-117">Se un processore di contenuti multimediali produce un file JSON, è possibile scaricare file hello dall'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="f148b-117">If a media processor produces a JSON file, you can download hello file from Azure Blob storage.</span></span> 

## <a name="media-analytics-services"></a><span data-ttu-id="f148b-118">Servizi di Analisi Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="f148b-118">Media Analytics services</span></span>

### <a name="indexer"></a><span data-ttu-id="f148b-119">Indexer</span><span class="sxs-lookup"><span data-stu-id="f148b-119">Indexer</span></span>
<span data-ttu-id="f148b-120">Azure Media Indexer consente di rendere disponibili per la ricerca i contenuti, oltre a generare tracce per i sottotitoli codificati.</span><span class="sxs-lookup"><span data-stu-id="f148b-120">With Azure Media Indexer, you can make content searchable and generate closed-captioning tracks.</span></span> <span data-ttu-id="f148b-121">Versione precedente di toohello confrontati, anteprima di Azure Media Indexer 2 è una lingua più veloce l'indicizzazione e più ampia di supportare.</span><span class="sxs-lookup"><span data-stu-id="f148b-121">Compared toohello previous version, Azure Media Indexer 2 Preview has faster indexing and broader language support.</span></span> <span data-ttu-id="f148b-122">Le lingue supportate includono inglese, spagnolo, francese, tedesco, italiano, cinese, portoghese e arabo.</span><span class="sxs-lookup"><span data-stu-id="f148b-122">Supported languages include English, Spanish, French, German, Italian, Chinese, Portuguese, and Arabic.</span></span> <span data-ttu-id="f148b-123">Per informazioni dettagliate ed esempi, vedere [Elaborare video con Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span><span class="sxs-lookup"><span data-stu-id="f148b-123">For detailed information and examples, see [Process videos with Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span></span>
### <a name="hyperlapse"></a><span data-ttu-id="f148b-124">Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="f148b-124">Hyperlapse</span></span>
<span data-ttu-id="f148b-125">Microsoft Hyperlapse combina stabilizzazione video e video funzionalità personalizzando toocreate rapido, utilizzabile dal contenuto in formato esteso.</span><span class="sxs-lookup"><span data-stu-id="f148b-125">Microsoft Hyperlapse combines video stabilization and time-lapse capability toocreate quick, consumable videos from your long-form content.</span></span> <span data-ttu-id="f148b-126">Oltre a creare personalizzando video, è possibile utilizzare Hyperlapse toocreate video stabili shaky video acquisite tramite telefoni cellulari e di cineprese.</span><span class="sxs-lookup"><span data-stu-id="f148b-126">Besides creating time-lapse video, you can use Hyperlapse toocreate stable videos from shaky videos captured via cell phones and camcorders.</span></span> <span data-ttu-id="f148b-127">Per informazioni dettagliate ed esempi, vedere [File multimediali di Hyperlapse con Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span><span class="sxs-lookup"><span data-stu-id="f148b-127">For detailed information and examples, see [Hyperlapse media files with Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span></span>
### <a name="motion-detector"></a><span data-ttu-id="f148b-128">Motion Detector</span><span class="sxs-lookup"><span data-stu-id="f148b-128">Motion Detector</span></span>
<span data-ttu-id="f148b-129">È possibile utilizzare il movimento toodetect rilevamento movimento in un video con sfondi fermo.</span><span class="sxs-lookup"><span data-stu-id="f148b-129">You can use Motion Detector toodetect motion in a video with stationary backgrounds.</span></span> <span data-ttu-id="f148b-130">Questo rende possibile toocheck per falsi positivi sugli eventi di movimento rilevati da telecamere di sorveglianza.</span><span class="sxs-lookup"><span data-stu-id="f148b-130">This makes it possible toocheck for false positives on motion events detected by surveillance cameras.</span></span> <span data-ttu-id="f148b-131">Per informazioni dettagliate ed esempi, vedere [Rilevamento dei movimenti per Analisi Servizi multimediali di Azure](media-services-motion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="f148b-131">For detailed information and examples, see [Motion detection for Azure Media Analytics](media-services-motion-detection.md).</span></span>
### <a name="face-detector"></a><span data-ttu-id="f148b-132">Face Detector</span><span class="sxs-lookup"><span data-stu-id="f148b-132">Face Detector</span></span>
<span data-ttu-id="f148b-133">Grazie all'uso di Face Detector, è possibile individuare i volti delle persone e le relative emozioni, ad esempio felicità, tristezza e sorpresa.</span><span class="sxs-lookup"><span data-stu-id="f148b-133">By using Face Detector, you can detect people’s faces and their emotions, including happiness, sadness, and surprise.</span></span> <span data-ttu-id="f148b-134">Questa funzionalità vanta numerose applicazioni utili nel settore, descritte di seguito, tra cui l'aggregazione e l'analisi delle reazioni delle persone che partecipano a un evento.</span><span class="sxs-lookup"><span data-stu-id="f148b-134">This has several useful industry applications, described later, including aggregating and analyzing reactions of people attending an event.</span></span> <span data-ttu-id="f148b-135">Per informazioni dettagliate ed esempi, vedere [Rilevamento di volti ed emozioni per Analisi Servizi multimediali di Azure](media-services-face-and-emotion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="f148b-135">For detailed information and examples, see [Face and emotion detection for Azure Media Analytics](media-services-face-and-emotion-detection.md).</span></span>
### <a name="video-summarization"></a><span data-ttu-id="f148b-136">Riepilogo video</span><span class="sxs-lookup"><span data-stu-id="f148b-136">Video summarization</span></span>
<span data-ttu-id="f148b-137">Riepilogo video consentono di creare riepiloghi dei video lunghi selezionando automaticamente interessanti frammenti video di origine hello.</span><span class="sxs-lookup"><span data-stu-id="f148b-137">Video summarization can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="f148b-138">Questa possibilità è utile quando si desidera tooprovide una rapida panoramica delle quali tooexpect in un video di lunga durata.</span><span class="sxs-lookup"><span data-stu-id="f148b-138">This ability is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="f148b-139">Per informazioni dettagliate ed esempi, vedere [riepilogo video di usare Azure Media Video anteprime toocreate](media-services-video-summarization.md).</span><span class="sxs-lookup"><span data-stu-id="f148b-139">For detailed information and examples, see [Use Azure Media Video Thumbnails toocreate video summarization](media-services-video-summarization.md).</span></span>
### <a name="optical-character-recognition"></a><span data-ttu-id="f148b-140">Riconoscimento ottico dei caratteri</span><span class="sxs-lookup"><span data-stu-id="f148b-140">Optical character recognition</span></span>
<span data-ttu-id="f148b-141">Il riconoscimento ottico dei caratteri (OCR) di Analisi Servizi multimediali di Azure consente di convertire il contenuto di testo dei file video in testo digitale modificabile e sui cui è possibile eseguire ricerche.</span><span class="sxs-lookup"><span data-stu-id="f148b-141">With Azure Media OCR (optical character recognition), you can convert text content in video files into editable, searchable digital text.</span></span> <span data-ttu-id="f148b-142">È quindi possibile automatizzare estrazione hello dei metadati significativo da segnale video di hello dei file multimediali.</span><span class="sxs-lookup"><span data-stu-id="f148b-142">You can then automate hello extraction of meaningful metadata from hello video signal of your media.</span></span>
### <a name="scalable-face-redaction"></a><span data-ttu-id="f148b-143">Offuscamento dei volti scalabile</span><span class="sxs-lookup"><span data-stu-id="f148b-143">Scalable face redaction</span></span>
<span data-ttu-id="f148b-144">Azure Media Redactor è un processore di contenuti multimediali Analitica supporti offre redazione faccia scalabile nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="f148b-144">Azure Media Redactor is a Media Analytics media processor that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="f148b-145">Tramite l'adattamento faccia, è possibile modificare i caratteri tipografici tooblur video di tutti i collaboratori.</span><span class="sxs-lookup"><span data-stu-id="f148b-145">By using face redaction, you can modify your video tooblur faces of selected individuals.</span></span> <span data-ttu-id="f148b-146">È possibile toouse hello faccia redazione servizio nel supporto di notizie o quando è coinvolto nella sicurezza pubblica.</span><span class="sxs-lookup"><span data-stu-id="f148b-146">You might want toouse hello face redaction service in news media or when public safety is involved.</span></span> <span data-ttu-id="f148b-147">Pochi minuti di riprese che contiene più caratteri tipografici possono richiedere ore tooredact manualmente, ma con questo servizio, redazione faccia richiede solo pochi semplici passaggi.</span><span class="sxs-lookup"><span data-stu-id="f148b-147">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service, face redaction takes just a few simple steps.</span></span> <span data-ttu-id="f148b-148">Per ulteriori informazioni, vedere hello [redigere facce con Azure Media Analitica](media-services-face-redaction.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="f148b-148">For more information, see hello [Redact faces with Azure Media Analytics](media-services-face-redaction.md) article.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="f148b-149">Scenari comuni</span><span class="sxs-lookup"><span data-stu-id="f148b-149">Common scenarios</span></span>
<span data-ttu-id="f148b-150">Analisi Servii multimediali può aiutare le organizzazioni e le aziende a scoprire nuovi orizzonti nel mondo dei video e gestire più efficacemente grandi volumi di contenuti video.</span><span class="sxs-lookup"><span data-stu-id="f148b-150">Media Analytics can help organizations and enterprises glean new insights from video and more effectively manage large volumes of video content.</span></span> <span data-ttu-id="f148b-151">Di seguito sono descritti diversi scenari:</span><span class="sxs-lookup"><span data-stu-id="f148b-151">Here are several scenarios:</span></span>

* <span data-ttu-id="f148b-152">**Call center**.</span><span class="sxs-lookup"><span data-stu-id="f148b-152">**Call centers**.</span></span> <span data-ttu-id="f148b-153">Anche con l'avvento di hello di social networking, call center semplificano ancora un'alta percentuale delle transazioni di servizio clienti.</span><span class="sxs-lookup"><span data-stu-id="f148b-153">Even with hello advent of social media, customer call centers still facilitate a large percentage of customer-service transactions.</span></span> <span data-ttu-id="f148b-154">In questi dati audio codificato è una grande quantità di informazioni sui clienti che possono essere analizzati tooachieve soddisfazione del cliente.</span><span class="sxs-lookup"><span data-stu-id="f148b-154">Encoded in this audio data is a large amount of customer information that can be analyzed tooachieve higher customer satisfaction.</span></span> <span data-ttu-id="f148b-155">Con Media Indexer, le organizzazioni possono estrarre il testo e creare indici di ricerca e dashboard.</span><span class="sxs-lookup"><span data-stu-id="f148b-155">By using Media Indexer, organizations can extract text and build search indexes and dashboards.</span></span> <span data-ttu-id="f148b-156">Possono quindi estrarre informazioni su reclami comuni, origini dei reclami e altri dati rilevanti.</span><span class="sxs-lookup"><span data-stu-id="f148b-156">Then they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span></span>
* <span data-ttu-id="f148b-157">**Moderazione dei contenuti generati dall'utente**.</span><span class="sxs-lookup"><span data-stu-id="f148b-157">**User-generated content moderation**.</span></span> <span data-ttu-id="f148b-158">Da reparti toopolice prese di notizie, molte organizzazioni utilizzano portali pubblico che accettano supporti generati dall'utente, ad esempio immagini e video.</span><span class="sxs-lookup"><span data-stu-id="f148b-158">From news media outlets toopolice departments, many organizations have public-facing portals that accept user-generated media such as videos and images.</span></span> <span data-ttu-id="f148b-159">volume Hello del contenuto può raggiungere toounexpected gli eventi di scadenza.</span><span class="sxs-lookup"><span data-stu-id="f148b-159">hello volume of content can spike due toounexpected events.</span></span> <span data-ttu-id="f148b-160">In questi scenari, è difficile tooconduct revisioni manuale efficace di contenuto appropriato per.</span><span class="sxs-lookup"><span data-stu-id="f148b-160">In these scenarios, it is difficult tooconduct effective manual reviews of content for appropriateness.</span></span> <span data-ttu-id="f148b-161">I clienti possono basarsi su hello servizio contenuto moderation toofocus contenuto appropriato.</span><span class="sxs-lookup"><span data-stu-id="f148b-161">Customers can rely on hello content-moderation service toofocus on content that is appropriate.</span></span>
* <span data-ttu-id="f148b-162">**Sorveglianza**.</span><span class="sxs-lookup"><span data-stu-id="f148b-162">**Surveillance**.</span></span> <span data-ttu-id="f148b-163">Aumento delle dimensioni in uso di camere hello comporta un aumento inventario del video di sorveglianza.</span><span class="sxs-lookup"><span data-stu-id="f148b-163">With hello growth in use of IP cameras comes a growing inventory of surveillance video.</span></span> <span data-ttu-id="f148b-164">Controllo manuale del video di sorveglianza è toohuman con utilizzo intensivo e soggetta a errore in fase di.</span><span class="sxs-lookup"><span data-stu-id="f148b-164">Manually reviewing surveillance video is time intensive and prone toohuman error.</span></span> <span data-ttu-id="f148b-165">Media Analitica fornisce servizi come il rilevamento di attività, rilevamento viso e processo di hello toomake Hyperlapse esaminare, gestire e più semplice creare derivati.</span><span class="sxs-lookup"><span data-stu-id="f148b-165">Media Analytics provides services such as motion detection, face detection, and Hyperlapse toomake hello process of reviewing, managing, and creating derivatives easier.</span></span>

## <a name="media-analytics-media-processors"></a><span data-ttu-id="f148b-166">Processori di contenuti multimediali di Analisi Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="f148b-166">Media Analytics media processors</span></span>
<span data-ttu-id="f148b-167">In questa sezione vengono processori di contenuti multimediali elenchi hello supporti Analitica e Mostra come toouse .NET o REST tooget un oggetto di supporto del processore (MP).</span><span class="sxs-lookup"><span data-stu-id="f148b-167">This section lists hello Media Analytics media processors and shows how toouse .NET or REST tooget a media processor (MP) object.</span></span>

### <a name="mp-names"></a><span data-ttu-id="f148b-168">Nomi dei processori di contenuti multimediali</span><span class="sxs-lookup"><span data-stu-id="f148b-168">MP names</span></span>
* <span data-ttu-id="f148b-169">Azure Media Indexer 2 Preview</span><span class="sxs-lookup"><span data-stu-id="f148b-169">Azure Media Indexer 2 Preview</span></span>
* <span data-ttu-id="f148b-170">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="f148b-170">Azure Media Indexer</span></span>
* <span data-ttu-id="f148b-171">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="f148b-171">Azure Media Hyperlapse</span></span>
* <span data-ttu-id="f148b-172">Rilevamento multimediale volti di Azure</span><span class="sxs-lookup"><span data-stu-id="f148b-172">Azure Media Face Detector</span></span>
* <span data-ttu-id="f148b-173">Rilevatore multimediale di movimento Azure</span><span class="sxs-lookup"><span data-stu-id="f148b-173">Azure Media Motion Detector</span></span>
* <span data-ttu-id="f148b-174">Anteprime video multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="f148b-174">Azure Media Video Thumbnails</span></span>
* <span data-ttu-id="f148b-175">Riconoscimento ottico dei caratteri multimediale di Azure</span><span class="sxs-lookup"><span data-stu-id="f148b-175">Azure Media OCR</span></span>

### <a name="net"></a><span data-ttu-id="f148b-176">.NET</span><span class="sxs-lookup"><span data-stu-id="f148b-176">.NET</span></span>
<span data-ttu-id="f148b-177">Hello seguente funzione accetta uno di hello specificato MP nomi e restituisce un oggetto Management Pack.</span><span class="sxs-lookup"><span data-stu-id="f148b-177">hello following function takes one of hello specified MP names and returns an MP object.</span></span>

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


### <a name="rest"></a><span data-ttu-id="f148b-178">REST</span><span class="sxs-lookup"><span data-stu-id="f148b-178">REST</span></span>
<span data-ttu-id="f148b-179">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="f148b-179">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

<span data-ttu-id="f148b-180">Risposta:</span><span class="sxs-lookup"><span data-stu-id="f148b-180">Response:</span></span>

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

## <a name="demos"></a><span data-ttu-id="f148b-181">Demo</span><span class="sxs-lookup"><span data-stu-id="f148b-181">Demos</span></span>
<span data-ttu-id="f148b-182">Vedere le [demo di Analisi Servizi multimediali di Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span><span class="sxs-lookup"><span data-stu-id="f148b-182">See [Azure Media Analytics demos](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f148b-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f148b-183">Next steps</span></span>
<span data-ttu-id="f148b-184">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="f148b-184">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f148b-185">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="f148b-185">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="f148b-186">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="f148b-186">Related articles</span></span>
<span data-ttu-id="f148b-187">Vedere l'[annuncio di Analisi Servizi multimediali di Azure](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span><span class="sxs-lookup"><span data-stu-id="f148b-187">See [Media Services Analytics announcement](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span></span>

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png

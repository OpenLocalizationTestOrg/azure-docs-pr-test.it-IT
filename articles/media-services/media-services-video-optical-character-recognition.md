---
title: testo aaaDigitize con Azure Media Analitica OCR | Documenti Microsoft
description: "Azure Media Analitica OCR (OCR) consente di tooconvert contenuto di testo nei file video in testo digitale modificabile, è possibile eseguire ricerca.  Ciò consente l'estrazione di hello tooautomate dei metadati significativo da segnale video di hello del supporto di."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a><span data-ttu-id="1f801-104">Utilizzare il contenuto di testo tooconvert Analitica multimediali di Azure nei file video in testo digitale</span><span class="sxs-lookup"><span data-stu-id="1f801-104">Use Azure Media Analytics tooconvert text content in video files into digital text</span></span>
## <a name="overview"></a><span data-ttu-id="1f801-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="1f801-105">Overview</span></span>
<span data-ttu-id="1f801-106">Testo tooextract contenuto dai file video e di generare un testo modificabile, è possibile eseguire ricerca digitale, è necessario utilizzare Azure Media Analitica OCR (optical il riconoscimento di caratteri).</span><span class="sxs-lookup"><span data-stu-id="1f801-106">If you need tooextract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span></span> <span data-ttu-id="1f801-107">Questo processore di contenuti multimediali di Azure rileva il contenuto di testo nei file video e genera file di testo pronti per l'uso.</span><span class="sxs-lookup"><span data-stu-id="1f801-107">This Azure Media Processor detects text content in your video files and generates text files for your use.</span></span> <span data-ttu-id="1f801-108">OCR consente si tooautomate hello estrazione dei metadati significativo da segnale video di hello del supporto di.</span><span class="sxs-lookup"><span data-stu-id="1f801-108">OCR enables you tooautomate hello extraction of meaningful metadata from hello video signal of your media.</span></span>

<span data-ttu-id="1f801-109">Se utilizzato in combinazione con un motore di ricerca, è possibile indicizzare i file multimediali dal testo facilmente e migliorare il rilevamento di hello del contenuto.</span><span class="sxs-lookup"><span data-stu-id="1f801-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance hello discoverability of your content.</span></span> <span data-ttu-id="1f801-110">Questa funzione risulta molto utile per i video che contengono un porzione importante di testo, ad esempio una registrazione video o l'acquisizione della schermata di una presentazione.</span><span class="sxs-lookup"><span data-stu-id="1f801-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.</span></span> <span data-ttu-id="1f801-111">Processore di contenuti multimediali di Azure OCR Hello è ottimizzato per testo digitale.</span><span class="sxs-lookup"><span data-stu-id="1f801-111">hello Azure OCR Media Processor is optimized for digital text.</span></span>

<span data-ttu-id="1f801-112">Hello **Azure Media OCR** processore di contenuti multimediali è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="1f801-112">hello **Azure Media OCR** media processor is currently in Preview.</span></span>

<span data-ttu-id="1f801-113">In questo argomento fornisce informazioni dettagliate sulle **Azure Media OCR** e Mostra come toouse con Media Services SDK per .NET.</span><span class="sxs-lookup"><span data-stu-id="1f801-113">This topic gives details about  **Azure Media OCR** and shows how toouse it with Media Services SDK for .NET.</span></span> <span data-ttu-id="1f801-114">Per altre informazioni ed esempi, vedere [questo blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span><span class="sxs-lookup"><span data-stu-id="1f801-114">For additional information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span></span>

## <a name="ocr-input-files"></a><span data-ttu-id="1f801-115">File di input OCR</span><span class="sxs-lookup"><span data-stu-id="1f801-115">OCR input files</span></span>
<span data-ttu-id="1f801-116">File video.</span><span class="sxs-lookup"><span data-stu-id="1f801-116">Video files.</span></span> <span data-ttu-id="1f801-117">Attualmente, è supportato i seguenti formati hello: MOV o MP4 e WMV.</span><span class="sxs-lookup"><span data-stu-id="1f801-117">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration"></a><span data-ttu-id="1f801-118">Configurazione delle attività</span><span class="sxs-lookup"><span data-stu-id="1f801-118">Task configuration</span></span>
<span data-ttu-id="1f801-119">Configurazione delle attività (set di impostazioni).</span><span class="sxs-lookup"><span data-stu-id="1f801-119">Task configuration (preset).</span></span> <span data-ttu-id="1f801-120">Quando si crea un'attività con **Azure Media OCR**, è necessario specificare un set di impostazioni di configurazione tramite JSON o XML.</span><span class="sxs-lookup"><span data-stu-id="1f801-120">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span></span> 

>[!NOTE]
><span data-ttu-id="1f801-121">il motore di riconoscimento Hello accetta solo un'area dell'immagine con minimo 40 pixel toomaximum 32000 come un input valido in entrambe altezza e la larghezza.</span><span class="sxs-lookup"><span data-stu-id="1f801-121">hello OCR engine only takes an image region with minimum 40 pixels toomaximum 32000 pixels as a valid input in both height/width.</span></span>
>

### <a name="attribute-descriptions"></a><span data-ttu-id="1f801-122">Descrizioni degli attributi</span><span class="sxs-lookup"><span data-stu-id="1f801-122">Attribute descriptions</span></span>
| <span data-ttu-id="1f801-123">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="1f801-123">Attribute name</span></span> | <span data-ttu-id="1f801-124">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1f801-124">Description</span></span> |
| --- | --- |
|<span data-ttu-id="1f801-125">AdvancedOutput</span><span class="sxs-lookup"><span data-stu-id="1f801-125">AdvancedOutput</span></span>| <span data-ttu-id="1f801-126">Se si imposta AdvancedOutput tootrue, l'output JSON hello conterrà dati posizionali per ogni singola parola (in aggiunta toophrases e le aree).</span><span class="sxs-lookup"><span data-stu-id="1f801-126">If you set AdvancedOutput tootrue, hello JSON output will contain positional data for every single word (in addition toophrases and regions).</span></span> <span data-ttu-id="1f801-127">Se non si desidera toosee questi dettagli set hello flag toofalse.</span><span class="sxs-lookup"><span data-stu-id="1f801-127">If you do not want toosee these details, set hello flag toofalse.</span></span> <span data-ttu-id="1f801-128">valore predefinito di Hello è false.</span><span class="sxs-lookup"><span data-stu-id="1f801-128">hello default value is false.</span></span> <span data-ttu-id="1f801-129">Per altre informazioni, vedere [questo blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span><span class="sxs-lookup"><span data-stu-id="1f801-129">For more information, see [this blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span></span>|
| <span data-ttu-id="1f801-130">Lingua</span><span class="sxs-lookup"><span data-stu-id="1f801-130">Language</span></span> |<span data-ttu-id="1f801-131">(facoltativo) descrive lingua hello del testo per cui toolook.</span><span class="sxs-lookup"><span data-stu-id="1f801-131">(optional) describes hello language of text for which toolook.</span></span> <span data-ttu-id="1f801-132">Uno dei seguenti hello: rilevamento automatico (predefinito), arabo, due lingue, ChineseTraditional, ceco danese, olandese, inglese, finlandese, francese, tedesco, greco, ungherese, italiano, giapponese, coreano, norvegese, polacco, portoghese, Romeno, russo, SerbianCyrillic, SerbianLatin, slovacco, spagnolo, svedese, turco.</span><span class="sxs-lookup"><span data-stu-id="1f801-132">One of hello following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span></span> |
| <span data-ttu-id="1f801-133">TextOrientation</span><span class="sxs-lookup"><span data-stu-id="1f801-133">TextOrientation</span></span> |<span data-ttu-id="1f801-134">(facoltativo) descrive orientamento hello del testo per cui toolook.</span><span class="sxs-lookup"><span data-stu-id="1f801-134">(optional) describes hello orientation of text for which toolook.</span></span>  <span data-ttu-id="1f801-135">Si fa riferimento a "Left" significa che hello parte superiore di tutte le lettere verso sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="1f801-135">"Left" means that hello top of all letters are pointed towards hello left.</span></span>  <span data-ttu-id="1f801-136">Il testo predefinito (simile a quello di un libro) può essere orientato come "Up".</span><span class="sxs-lookup"><span data-stu-id="1f801-136">Default text (like that which can be found in a book) can be called "Up" oriented.</span></span>  <span data-ttu-id="1f801-137">Uno dei seguenti hello: rilevamento automatico (predefinito), verso l'alto, a destra, verso il basso, a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1f801-137">One of hello following: AutoDetect (default), Up, Right, Down, Left.</span></span> |
| <span data-ttu-id="1f801-138">TimeInterval</span><span class="sxs-lookup"><span data-stu-id="1f801-138">TimeInterval</span></span> |<span data-ttu-id="1f801-139">(facoltativo) descrive la frequenza di campionamento hello.</span><span class="sxs-lookup"><span data-stu-id="1f801-139">(optional) describes hello sampling rate.</span></span>  <span data-ttu-id="1f801-140">Il valore predefinito è ogni 1/2 secondo.</span><span class="sxs-lookup"><span data-stu-id="1f801-140">Default is every 1/2 second.</span></span><br/><span data-ttu-id="1f801-141">Formato JSON: HH:mm:ss.SSS (impostazione predefinita 00:00:00.500)</span><span class="sxs-lookup"><span data-stu-id="1f801-141">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span></span><br/><span data-ttu-id="1f801-142">Formato XML – durata primitivi W3C XSD (predefinito PT0.5)</span><span class="sxs-lookup"><span data-stu-id="1f801-142">XML format – W3C XSD duration primitive (default PT0.5)</span></span> |
| <span data-ttu-id="1f801-143">DetectRegions</span><span class="sxs-lookup"><span data-stu-id="1f801-143">DetectRegions</span></span> |<span data-ttu-id="1f801-144">(facoltativo) Una matrice di oggetti DetectRegion specificare aree all'interno di fotogrammi video hello del testo toodetect.</span><span class="sxs-lookup"><span data-stu-id="1f801-144">(optional) An array of DetectRegion objects specifying regions within hello video frame in which toodetect text.</span></span><br/><span data-ttu-id="1f801-145">Un oggetto DetectRegion è costituito da hello seguenti quattro valori integer:</span><span class="sxs-lookup"><span data-stu-id="1f801-145">A DetectRegion object is made of hello following four integer values:</span></span><br/><span data-ttu-id="1f801-146">A sinistra: pixel da hello del margine sinistro</span><span class="sxs-lookup"><span data-stu-id="1f801-146">Left – pixels from hello left-margin</span></span><br/><span data-ttu-id="1f801-147">Alto-pixel da hello per il margine superiore</span><span class="sxs-lookup"><span data-stu-id="1f801-147">Top – pixels from hello top-margin</span></span><br/><span data-ttu-id="1f801-148">Larghezza: la larghezza dell'area di hello in pixel</span><span class="sxs-lookup"><span data-stu-id="1f801-148">Width – width of hello region in pixels</span></span><br/><span data-ttu-id="1f801-149">Height: altezza dell'area di hello in pixel</span><span class="sxs-lookup"><span data-stu-id="1f801-149">Height – height of hello region in pixels</span></span> |

#### <a name="json-preset-example"></a><span data-ttu-id="1f801-150">Esempio di set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="1f801-150">JSON preset example</span></span>

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a><span data-ttu-id="1f801-151">Esempio di set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="1f801-151">XML preset example</span></span>
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a><span data-ttu-id="1f801-152">File di output OCR</span><span class="sxs-lookup"><span data-stu-id="1f801-152">OCR output files</span></span>
<span data-ttu-id="1f801-153">output di Hello del processore di contenuti multimediali OCR hello è un file JSON.</span><span class="sxs-lookup"><span data-stu-id="1f801-153">hello output of hello OCR media processor is a JSON file.</span></span>

### <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="1f801-154">Elementi hello JSON del file di output</span><span class="sxs-lookup"><span data-stu-id="1f801-154">Elements of hello output JSON file</span></span>
<span data-ttu-id="1f801-155">output di Hello OCR Video fornisce i dati segmentati ora sui caratteri hello trovati nel video.</span><span class="sxs-lookup"><span data-stu-id="1f801-155">hello Video OCR output provides time-segmented data on hello characters found in your video.</span></span>  <span data-ttu-id="1f801-156">È possibile utilizzare gli attributi, ad esempio lingua o toohone orientamento esattamente le parole hello che si è interessati, l'analisi.</span><span class="sxs-lookup"><span data-stu-id="1f801-156">You can use attributes such as language or orientation toohone-in on exactly hello words that you are interested in analyzing.</span></span> 

<span data-ttu-id="1f801-157">output di Hello contiene hello gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1f801-157">hello output contains hello following attributes:</span></span>

| <span data-ttu-id="1f801-158">Elemento</span><span class="sxs-lookup"><span data-stu-id="1f801-158">Element</span></span> | <span data-ttu-id="1f801-159">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1f801-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1f801-160">Scala cronologica</span><span class="sxs-lookup"><span data-stu-id="1f801-160">Timescale</span></span> |<span data-ttu-id="1f801-161">"tick" al secondo del video hello</span><span class="sxs-lookup"><span data-stu-id="1f801-161">"ticks" per second of hello video</span></span> |
| <span data-ttu-id="1f801-162">Offset</span><span class="sxs-lookup"><span data-stu-id="1f801-162">Offset</span></span> |<span data-ttu-id="1f801-163">Differenza di orario dei timestamp</span><span class="sxs-lookup"><span data-stu-id="1f801-163">time offset for timestamps.</span></span> <span data-ttu-id="1f801-164">Nella versione 1.0 delle API Video, questo valore è sempre 0.</span><span class="sxs-lookup"><span data-stu-id="1f801-164">In version 1.0 of Video APIs, this will always be 0.</span></span> |
| <span data-ttu-id="1f801-165">Frequenza fotogrammi</span><span class="sxs-lookup"><span data-stu-id="1f801-165">Framerate</span></span> |<span data-ttu-id="1f801-166">Fotogrammi al secondo di hello video</span><span class="sxs-lookup"><span data-stu-id="1f801-166">Frames per second of hello video</span></span> |
| <span data-ttu-id="1f801-167">width</span><span class="sxs-lookup"><span data-stu-id="1f801-167">width</span></span> |<span data-ttu-id="1f801-168">larghezza del video in pixel hello</span><span class="sxs-lookup"><span data-stu-id="1f801-168">width of hello video in pixels</span></span> |
| <span data-ttu-id="1f801-169">height</span><span class="sxs-lookup"><span data-stu-id="1f801-169">height</span></span> |<span data-ttu-id="1f801-170">altezza del video in pixel hello</span><span class="sxs-lookup"><span data-stu-id="1f801-170">height of hello video in pixels</span></span> |
| <span data-ttu-id="1f801-171">Frammenti</span><span class="sxs-lookup"><span data-stu-id="1f801-171">Fragments</span></span> |<span data-ttu-id="1f801-172">Matrice di blocchi basati sull'ora del video in cui hello metadati sono bloccato</span><span class="sxs-lookup"><span data-stu-id="1f801-172">array of time-based chunks of video into which hello metadata is chunked</span></span> |
| <span data-ttu-id="1f801-173">start</span><span class="sxs-lookup"><span data-stu-id="1f801-173">start</span></span> |<span data-ttu-id="1f801-174">Ora di inizio di un frammento in "scatti"</span><span class="sxs-lookup"><span data-stu-id="1f801-174">start time of a fragment in "ticks"</span></span> |
| <span data-ttu-id="1f801-175">duration</span><span class="sxs-lookup"><span data-stu-id="1f801-175">duration</span></span> |<span data-ttu-id="1f801-176">Lunghezza di un frammento in "scatti"</span><span class="sxs-lookup"><span data-stu-id="1f801-176">length of a fragment in "ticks"</span></span> |
| <span data-ttu-id="1f801-177">interval</span><span class="sxs-lookup"><span data-stu-id="1f801-177">interval</span></span> |<span data-ttu-id="1f801-178">intervallo di ogni evento all'interno di hello fornito frammento</span><span class="sxs-lookup"><span data-stu-id="1f801-178">interval of each event within hello given fragment</span></span> |
| <span data-ttu-id="1f801-179">eventi</span><span class="sxs-lookup"><span data-stu-id="1f801-179">events</span></span> |<span data-ttu-id="1f801-180">Matrice contenente le aree</span><span class="sxs-lookup"><span data-stu-id="1f801-180">array containing regions</span></span> |
| <span data-ttu-id="1f801-181">region</span><span class="sxs-lookup"><span data-stu-id="1f801-181">region</span></span> |<span data-ttu-id="1f801-182">Oggetto che rappresenta le parole o le frasi rilevate</span><span class="sxs-lookup"><span data-stu-id="1f801-182">object representing detected words or phrases</span></span> |
| <span data-ttu-id="1f801-183">Linguaggio</span><span class="sxs-lookup"><span data-stu-id="1f801-183">language</span></span> |<span data-ttu-id="1f801-184">lingua del testo hello rilevato all'interno di un'area</span><span class="sxs-lookup"><span data-stu-id="1f801-184">language of hello text detected within a region</span></span> |
| <span data-ttu-id="1f801-185">orientation</span><span class="sxs-lookup"><span data-stu-id="1f801-185">orientation</span></span> |<span data-ttu-id="1f801-186">orientamento del testo hello rilevato all'interno di un'area</span><span class="sxs-lookup"><span data-stu-id="1f801-186">orientation of hello text detected within a region</span></span> |
| <span data-ttu-id="1f801-187">lines</span><span class="sxs-lookup"><span data-stu-id="1f801-187">lines</span></span> |<span data-ttu-id="1f801-188">Matrice di righe del testo rilevato all'interno di un'area</span><span class="sxs-lookup"><span data-stu-id="1f801-188">array of lines of text detected within a region</span></span> |
| <span data-ttu-id="1f801-189">text</span><span class="sxs-lookup"><span data-stu-id="1f801-189">text</span></span> |<span data-ttu-id="1f801-190">testo effettivo Hello</span><span class="sxs-lookup"><span data-stu-id="1f801-190">hello actual text</span></span> |

### <a name="json-output-example"></a><span data-ttu-id="1f801-191">Esempio di output JSON</span><span class="sxs-lookup"><span data-stu-id="1f801-191">JSON output example</span></span>
<span data-ttu-id="1f801-192">Hello seguente esempio di output contiene le informazioni generali video hello e più frammenti video.</span><span class="sxs-lookup"><span data-stu-id="1f801-192">hello following output example contains hello general video information and several video fragments.</span></span> <span data-ttu-id="1f801-193">In ogni frammento video, contiene ogni area in cui viene rilevato da MP OCR con lingua hello e l'orientamento del testo.</span><span class="sxs-lookup"><span data-stu-id="1f801-193">In every video fragment, it contains every region which is detected by OCR MP with hello language and its text orientation.</span></span> <span data-ttu-id="1f801-194">area Hello contiene inoltre ogni riga di word in quest'area con testo della riga hello, la posizione della riga hello e tutte le informazioni di word (il contenuto di word, posizione e confidenza) in questa riga.</span><span class="sxs-lookup"><span data-stu-id="1f801-194">hello region also contains every word line in this region with hello line’s text, hello line’s position, and every word information (word content, position and confidence) in this line.</span></span> <span data-ttu-id="1f801-195">Hello seguito è riportato un esempio e inserire alcuni commenti in linea.</span><span class="sxs-lookup"><span data-stu-id="1f801-195">hello following is an example, and I put some comments inline.</span></span>

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a><span data-ttu-id="1f801-196">Codice di esempio .NET</span><span class="sxs-lookup"><span data-stu-id="1f801-196">.NET sample code</span></span>

<span data-ttu-id="1f801-197">esempio Hello programma mostra come:</span><span class="sxs-lookup"><span data-stu-id="1f801-197">hello following program shows how to:</span></span>

1. <span data-ttu-id="1f801-198">Creare un asset e caricare un file multimediale nell'asset hello.</span><span class="sxs-lookup"><span data-stu-id="1f801-198">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="1f801-199">Creare un processo con un file di configurazione/set di impostazioni OCR.</span><span class="sxs-lookup"><span data-stu-id="1f801-199">Create a job with an OCR configuration/preset file.</span></span>
3. <span data-ttu-id="1f801-200">Scaricare i file JSON di output di hello.</span><span class="sxs-lookup"><span data-stu-id="1f801-200">Download hello output JSON files.</span></span> 
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="1f801-201">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1f801-201">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="1f801-202">Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="1f801-202">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="1f801-203">Esempio</span><span class="sxs-lookup"><span data-stu-id="1f801-203">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace OCR
    {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, hello event handling
                // method for job progress should log errors.  Here we check
                // for error state and exit if needed.
                if (job.State == JobState.Error)
                {
                    ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                    Console.WriteLine(string.Format("Error: {0}. {1}",
                                                    error.Code,
                                                    error.Message));
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

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

            static private void StateChanged(object sender, JobStateChangedEventArgs e)
            {
                Console.WriteLine("Job state changed event:");
                Console.WriteLine("  Previous state: " + e.PreviousState);
                Console.WriteLine("  Current state: " + e.CurrentState);

                switch (e.CurrentState)
                {
                    case JobState.Finished:
                        Console.WriteLine();
                        Console.WriteLine("Job is finished.");
                        Console.WriteLine();
                        break;
                    case JobState.Canceling:
                    case JobState.Queued:
                    case JobState.Scheduled:
                    case JobState.Processing:
                        Console.WriteLine("Please wait...\n");
                        break;
                    case JobState.Canceled:
                    case JobState.Error:
                        // Cast sender as a job.
                        IJob job = (IJob)sender;
                        // Display or log error details as needed.
                        // LogJobStop(job.Id);
                        break;
                    default:
                        break;
                }
            }

        }
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="1f801-204">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1f801-204">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1f801-205">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="1f801-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="1f801-206">Collegamenti correlati</span><span class="sxs-lookup"><span data-stu-id="1f801-206">Related links</span></span>
[<span data-ttu-id="1f801-207">Panoramica di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="1f801-207">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)


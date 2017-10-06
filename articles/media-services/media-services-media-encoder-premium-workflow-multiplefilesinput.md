---
title: "aaaMultiple input i file e le proprietà del componente con il codificatore Premium, Azure | Documenti Microsoft"
description: "In questo argomento viene illustrato toouse setRuntimeProperties toouse input più file e passare processore di contenuti multimediali di flusso di lavoro Premium del codificatore multimediale toohello dati personalizzati."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: 7fb35bdd-9891-4401-a65b-ef3cc8190e8a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: xpouyat;anilmur;juliako
ms.openlocfilehash: e14d10fbf9669e0b88e5ba1c519f1ba5e0bafdd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a><span data-ttu-id="77109-103">Uso di più file di input e proprietà del componente con il codificatore Premium</span><span class="sxs-lookup"><span data-stu-id="77109-103">Using multiple input files and component properties with Premium Encoder</span></span>
## <a name="overview"></a><span data-ttu-id="77109-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="77109-104">Overview</span></span>
<span data-ttu-id="77109-105">Esistono scenari in cui le proprietà del componente toocustomize, potrebbe essere necessario specificare Clip elenco XML contenuto oppure inviare più file di input quando si invia un'attività con hello **flusso di lavoro Premium del codificatore multimediale** processore di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="77109-105">There are scenarios in which you might need toocustomize component properties, specify Clip List XML content, or send multiple input files when you submit a task with hello **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="77109-106">Di seguito sono riportati alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="77109-106">Some examples are:</span></span>

* <span data-ttu-id="77109-107">La sovrapposizione di testo nel video e impostando il valore di testo hello (ad esempio, Buongiorno data corrente) in fase di esecuzione per ogni video di input.</span><span class="sxs-lookup"><span data-stu-id="77109-107">Overlaying text on video and setting hello text value (for example, hello current date) at runtime for each input video.</span></span>
* <span data-ttu-id="77109-108">Personalizzazione hello Clip elenco XML (toospecify uno o più file, con o senza l'eliminazione e così via di origine).</span><span class="sxs-lookup"><span data-stu-id="77109-108">Customizing hello Clip List XML (toospecify one or several source files, with or without trimming, etc.).</span></span>
* <span data-ttu-id="77109-109">La sovrapposizione di un'immagine del logo nel video di input hello mentre video hello è codificato.</span><span class="sxs-lookup"><span data-stu-id="77109-109">Overlaying a logo image on hello input video while hello video is encoded.</span></span>
* <span data-ttu-id="77109-110">Codifica di più lingue per l'audio.</span><span class="sxs-lookup"><span data-stu-id="77109-110">Multiple audio language encoding.</span></span>

<span data-ttu-id="77109-111">hello toolet **flusso di lavoro Premium del codificatore multimediale** che si modificano alcune proprietà nel flusso di lavoro hello quando si creano attività hello o inviano più file di input, si dispone di toouse una stringa di configurazione che contiene  **setRuntimeProperties** e/o **transcodeSource**.</span><span class="sxs-lookup"><span data-stu-id="77109-111">toolet hello **Media Encoder Premium Workflow** know that you are changing some properties in hello workflow when you create hello task or send multiple input files, you have toouse a configuration string that contains **setRuntimeProperties** and/or **transcodeSource**.</span></span> <span data-ttu-id="77109-112">Questo argomento viene illustrato come toouse li.</span><span class="sxs-lookup"><span data-stu-id="77109-112">This topic explains how toouse them.</span></span>

## <a name="configuration-string-syntax"></a><span data-ttu-id="77109-113">Sintassi della stringa di configurazione</span><span class="sxs-lookup"><span data-stu-id="77109-113">Configuration string syntax</span></span>
<span data-ttu-id="77109-114">tooset di stringa di configurazione di Hello in hello codifica attività utilizza un documento XML simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="77109-114">hello configuration string tooset in hello encoding task uses an XML document that looks like this:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<transcodeRequest>
  <transcodeSource>
  </transcodeSource>
  <setRuntimeProperties>
    <property propertyPath="Media File Input/filename" value="VideoFileName.mp4" />
  </setRuntimeProperties>
</transcodeRequest>
```

<span data-ttu-id="77109-115">di seguito Hello è codice hello c# che consente di leggere da un file di configurazione XML hello, aggiornarlo con hello filename destra video e la passa toohello attività in un processo:</span><span class="sxs-lookup"><span data-stu-id="77109-115">hello following is hello C# code that reads hello XML configuration from a file, update it with hello right video filename and passes it toohello task in a job:</span></span>

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass tooit hello name of hello 
// processor toouse for hello specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with hello encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify hello input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset toocontain hello results of hello job. 
// This output is specified as AssetCreationOptions.None, which 
// means hello output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a><span data-ttu-id="77109-116">Personalizzazione delle proprietà del componente</span><span class="sxs-lookup"><span data-stu-id="77109-116">Customizing component properties</span></span>
### <a name="property-with-a-simple-value"></a><span data-ttu-id="77109-117">Proprietà con un valore semplice</span><span class="sxs-lookup"><span data-stu-id="77109-117">Property with a simple value</span></span>
<span data-ttu-id="77109-118">In alcuni casi, è utile toocustomize una proprietà del componente con i file di flusso di lavoro hello che verrà eseguito dal flusso di lavoro Premium del codificatore multimediale toobe.</span><span class="sxs-lookup"><span data-stu-id="77109-118">In some cases, it is useful toocustomize a component property together with hello workflow file that is going toobe executed by Media Encoder Premium Workflow.</span></span>

<span data-ttu-id="77109-119">Si supponga che è progettato un flusso di lavoro che il testo sovrapposizioni sui video e testo hello (ad esempio, Buongiorno data corrente) si suppone che il set di toobe in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="77109-119">Suppose you designed a workflow that overlays text on your videos, and hello text (for example, hello current date) is supposed toobe set at runtime.</span></span> <span data-ttu-id="77109-120">È possibile farlo inviando toobe testo hello configurare come nuovo valore per la proprietà text hello del componente di sovrapposizione hello di hello hello attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="77109-120">You can do this by sending hello text toobe set as hello new value for hello text property of hello overlay component from hello encoding task.</span></span> <span data-ttu-id="77109-121">È possibile utilizzare questo meccanismo toochange altre proprietà di un componente nel flusso di lavoro di hello (ad esempio hello posizione o colore della sovrimpressione hello, velocità in bit hello del codificatore hello AVC, ecc.).</span><span class="sxs-lookup"><span data-stu-id="77109-121">You can use this mechanism toochange other properties of a component in hello workflow (such as hello position or color of hello overlay, hello bitrate of hello AVC encoder, etc.).</span></span>

<span data-ttu-id="77109-122">**setRuntimeProperties** è toooverride utilizzata una proprietà nei componenti hello del flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="77109-122">**setRuntimeProperties** is used toooverride a property in hello components of hello workflow.</span></span>

<span data-ttu-id="77109-123">Esempio:</span><span class="sxs-lookup"><span data-stu-id="77109-123">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text tooImage Converter/text" value="Today is Friday hello 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a><span data-ttu-id="77109-124">Proprietà con un valore XML</span><span class="sxs-lookup"><span data-stu-id="77109-124">Property with an XML value</span></span>
<span data-ttu-id="77109-125">incapsulare una proprietà che prevede un valore XML, tooset utilizzando `<![CDATA[ and ]]>`.</span><span class="sxs-lookup"><span data-stu-id="77109-125">tooset a property that expects an XML value, encapsulate by using `<![CDATA[ and ]]>`.</span></span>

<span data-ttu-id="77109-126">Esempio:</span><span class="sxs-lookup"><span data-stu-id="77109-126">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

> [!NOTE]
> <span data-ttu-id="77109-127">Assicurarsi che non tooput di ritorno a capo restituiscono subito dopo `<![CDATA[`.</span><span class="sxs-lookup"><span data-stu-id="77109-127">Make sure not tooput a carriage return just after `<![CDATA[`.</span></span>

### <a name="propertypath-value"></a><span data-ttu-id="77109-128">Valore di propertyPath</span><span class="sxs-lookup"><span data-stu-id="77109-128">propertyPath value</span></span>
<span data-ttu-id="77109-129">Negli esempi precedenti hello, stato hello propertyPath "file di supporto/nome al file di Input" o "/ inactiveTimeout" o "clipListXml".</span><span class="sxs-lookup"><span data-stu-id="77109-129">In hello previous examples, hello propertyPath was "/Media File Input/filename" or "/inactiveTimeout" or "clipListXml".</span></span>
<span data-ttu-id="77109-130">Si tratta in genere, nome hello del componente di hello, il nome di hello di proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="77109-130">This is, in general, hello name of hello component, then hello name of hello property.</span></span> <span data-ttu-id="77109-131">Hello percorso può essere maggiore o minore di livelli, ad esempio "/ primarySourceFile" (poiché la proprietà hello è alla radice di hello del flusso di lavoro hello) o "/ Video opacità di elaborazione grafica sovrapposizione /" (poiché hello sovrapposta è un gruppo).</span><span class="sxs-lookup"><span data-stu-id="77109-131">hello path can have more or fewer levels, like "/primarySourceFile" (because hello property is at hello root of hello workflow) or "/Video Processing/Graphic Overlay/Opacity" (because hello Overlay is in a group).</span></span>    

<span data-ttu-id="77109-132">toocheck hello percorso e la proprietà nome, utilizzare hello azione pulsante immediatamente accanto a ogni proprietà.</span><span class="sxs-lookup"><span data-stu-id="77109-132">toocheck hello path and property name, use hello action button that is immediately beside each property.</span></span> <span data-ttu-id="77109-133">È possibile fare clic su questo pulsante di azione e selezionare **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="77109-133">You can click this action button and select **Edit**.</span></span> <span data-ttu-id="77109-134">Verranno visualizzati hello effettivo nome di proprietà hello e immediatamente sopra di esso, hello dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="77109-134">This will show you hello actual name of hello property, and immediately above it, hello namespace.</span></span>

![Azione/modifica](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Proprietà](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a><span data-ttu-id="77109-137">Più file di input</span><span class="sxs-lookup"><span data-stu-id="77109-137">Multiple input files</span></span>
<span data-ttu-id="77109-138">Ogni attività che si presentino toohello **flusso di lavoro Premium del codificatore multimediale** richiede due risorse:</span><span class="sxs-lookup"><span data-stu-id="77109-138">Each task that you submit toohello **Media Encoder Premium Workflow** requires two assets:</span></span>

* <span data-ttu-id="77109-139">Hello prima uno è un *del flusso di lavoro Asset* che contiene un file di flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="77109-139">hello first one is a *Workflow Asset* that contains a workflow file.</span></span> <span data-ttu-id="77109-140">È possibile progettare i file del flusso di lavoro utilizzando hello [Progettazione flussi di lavoro](media-services-workflow-designer.md).</span><span class="sxs-lookup"><span data-stu-id="77109-140">You can design workflow files by using hello [Workflow Designer](media-services-workflow-designer.md).</span></span>
* <span data-ttu-id="77109-141">Hello secondo è un *Asset multimediali* che contiene i file di supporto hello che si desidera tooencode.</span><span class="sxs-lookup"><span data-stu-id="77109-141">hello second one is a *Media Asset* that contains hello media file(s) that you want tooencode.</span></span>

<span data-ttu-id="77109-142">Quando si invia più supporti file toohello **flusso di lavoro Premium del codificatore multimediale** codificatore, hello seguenti vincoli applica:</span><span class="sxs-lookup"><span data-stu-id="77109-142">When you're sending multiple media files toohello **Media Encoder Premium Workflow** encoder, hello following constraints apply:</span></span>

* <span data-ttu-id="77109-143">Tutti i supporti di hello file devono trovarsi nel hello stesso *Asset multimediali*.</span><span class="sxs-lookup"><span data-stu-id="77109-143">All hello media files must be in hello same *Media Asset*.</span></span> <span data-ttu-id="77109-144">L'uso di più asset multimediali non è supportato.</span><span class="sxs-lookup"><span data-stu-id="77109-144">Using multiple Media Assets is not supported.</span></span>
* <span data-ttu-id="77109-145">È necessario impostare file primario hello in questo Asset multimediali (idealmente, si tratta di hello file video principale che hello codificatore viene chiesto tooprocess).</span><span class="sxs-lookup"><span data-stu-id="77109-145">You must set hello primary file in this Media Asset (ideally, this is hello main video file that hello encoder is asked tooprocess).</span></span>
* <span data-ttu-id="77109-146">È necessario toopass i dati di configurazione che include hello **setRuntimeProperties** e/o **transcodeSource** processore toohello elemento.</span><span class="sxs-lookup"><span data-stu-id="77109-146">It is necessary toopass configuration data that includes hello **setRuntimeProperties** and/or **transcodeSource** element toohello processor.</span></span>
  * <span data-ttu-id="77109-147">**setRuntimeProperties** è di proprietà filename di hello toooverride usato o un'altra proprietà nei componenti di hello del flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="77109-147">**setRuntimeProperties** is used toooverride hello filename property or another property in hello components of hello workflow.</span></span>
  * <span data-ttu-id="77109-148">**transcodeSource** è usato toospecify hello contenuto Clip elenco XML.</span><span class="sxs-lookup"><span data-stu-id="77109-148">**transcodeSource** is used toospecify hello Clip List XML content.</span></span>

<span data-ttu-id="77109-149">Connessioni nel flusso di lavoro hello:</span><span class="sxs-lookup"><span data-stu-id="77109-149">Connections in hello workflow:</span></span>

* <span data-ttu-id="77109-150">Se si utilizza uno o più componenti di Input di File multimediali e pianificare toouse **setRuntimeProperties** toospecify hello Nome file, quindi non si connettono hello file primario componente pin toothem.</span><span class="sxs-lookup"><span data-stu-id="77109-150">If you use one or several Media File Input components and plan toouse **setRuntimeProperties** toospecify hello file name, then do not connect hello primary file component pin toothem.</span></span> <span data-ttu-id="77109-151">Assicurarsi che non vi sia alcuna connessione tra l'oggetto file primario hello e hello uno o più File di supporto di input.</span><span class="sxs-lookup"><span data-stu-id="77109-151">Make sure that there is no connection between hello primary file object and hello Media File Input(s).</span></span>
* <span data-ttu-id="77109-152">Se si preferisce toouse Clip elenco XML e un componente di origine multimediale, quindi è possibile connettere entrambi.</span><span class="sxs-lookup"><span data-stu-id="77109-152">If you prefer toouse Clip List XML and one Media Source component, then you can connect both together.</span></span>

![Nessuna connessione da File di origine primario tooMedia File di Input](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

<span data-ttu-id="77109-154">*Se si usa proprietà filename di setRuntimeProperties tooset hello non è nessuna connessione dal file primario di hello tooMedia componenti di Input del File.*</span><span class="sxs-lookup"><span data-stu-id="77109-154">*There is no connection from hello primary file tooMedia File Input component(s) if you use setRuntimeProperties tooset hello filename property.*</span></span>

![Connessione da Clip elenco XML tooClip elenco origine](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

<span data-ttu-id="77109-156">*È possibile connettersi tooMedia Clip elenco XML origine e utilizzare transcodeSource.*</span><span class="sxs-lookup"><span data-stu-id="77109-156">*You can connect Clip List XML tooMedia Source and use transcodeSource.*</span></span>

### <a name="clip-list-xml-customization"></a><span data-ttu-id="77109-157">Personalizzazione di Clip List XML</span><span class="sxs-lookup"><span data-stu-id="77109-157">Clip List XML customization</span></span>
<span data-ttu-id="77109-158">È possibile specificare hello Clip elenco XML nel flusso di lavoro hello in fase di esecuzione utilizzando **transcodeSource** in configurazione hello stringa XML.</span><span class="sxs-lookup"><span data-stu-id="77109-158">You can specify hello Clip List XML in hello workflow at runtime by using **transcodeSource** in hello configuration string XML.</span></span> <span data-ttu-id="77109-159">È necessario hello Clip elenco XML pin toobe connesso toohello origine multimediale componente nel flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="77109-159">This requires hello Clip List XML pin toobe connected toohello Media Source component in hello workflow.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <transcodeSource>
      <clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
      </clipList>
    </transcodeSource>
    <setRuntimeProperties>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="77109-160">Se si desidera toospecify /primarySourceFile toouse file di output di hello tooname questa proprietà tramite 'Expressions', si consiglia di passando hello Clip elenco XML come una proprietà *dopo* proprietà /primarySourceFile hello, tooavoid con hello elenco Clip essere sottoposto a override dall'impostazione /primarySourceFile hello.</span><span class="sxs-lookup"><span data-stu-id="77109-160">If you want toospecify /primarySourceFile toouse this property tooname hello output files by using 'Expressions', then we recommend passing hello Clip List XML as a property *after* hello /primarySourceFile property, tooavoid having hello Clip List be overridden by hello /primarySourceFile setting.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="c:\temp\start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="77109-161">Con altro trimming preciso al fotogramma:</span><span class="sxs-lookup"><span data-stu-id="77109-161">With additional frame-accurate trimming:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a><span data-ttu-id="77109-162">Esempio 1: Sovrapposizione un'immagine di sopra hello video</span><span class="sxs-lookup"><span data-stu-id="77109-162">Example 1 : Overlay an image on top of hello video</span></span>

### <a name="presentation"></a><span data-ttu-id="77109-163">Presentazione</span><span class="sxs-lookup"><span data-stu-id="77109-163">Presentation</span></span>
<span data-ttu-id="77109-164">Si consideri un esempio in cui si desidera toooverlay un'immagine del logo nel video di input hello mentre video hello è codificato.</span><span class="sxs-lookup"><span data-stu-id="77109-164">Consider an example in which you want toooverlay a logo image on hello input video while hello video is encoded.</span></span> <span data-ttu-id="77109-165">In questo esempio, i video di input hello è denominato "Microsoft_HoloLens_Possibilities_816p24.mp4" e il logo di hello "logo.png".</span><span class="sxs-lookup"><span data-stu-id="77109-165">In this example, hello input video is named "Microsoft_HoloLens_Possibilities_816p24.mp4" and hello logo is named "logo.png".</span></span> <span data-ttu-id="77109-166">È consigliabile eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="77109-166">You should perform hello following steps:</span></span>

* <span data-ttu-id="77109-167">Creare un Asset del flusso di lavoro con i file di flusso di lavoro hello (vedere il seguente esempio hello).</span><span class="sxs-lookup"><span data-stu-id="77109-167">Create a Workflow Asset with hello workflow file (see hello following example).</span></span>
* <span data-ttu-id="77109-168">Creare una risorsa multimediale, che contiene due file: MyInputVideo.mp4 come hello file primario e MyLogo.png.</span><span class="sxs-lookup"><span data-stu-id="77109-168">Create a Media Asset, which contains two files: MyInputVideo.mp4 as hello primary file and MyLogo.png.</span></span>
* <span data-ttu-id="77109-169">Inviare un supporto di flusso di lavoro Premium del codificatore multimediale di toohello attività asset processore con hello precedente di input e specificare hello seguente stringa di configurazione.</span><span class="sxs-lookup"><span data-stu-id="77109-169">Send a task toohello Media Encoder Premium Workflow media processor with hello above input assets and specify hello following configuration string.</span></span>

<span data-ttu-id="77109-170">Configurazione:</span><span class="sxs-lookup"><span data-stu-id="77109-170">Configuration:</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="77109-171">Nell'esempio hello sopra, il nome di hello di file video hello viene inviato proprietà primarySourceFile componente e hello toohello Input File multimediali.</span><span class="sxs-lookup"><span data-stu-id="77109-171">In hello example above, hello name of hello video file is sent toohello Media File Input component and hello primarySourceFile property.</span></span> <span data-ttu-id="77109-172">nome di Hello del file di logo hello viene inviato tooanother Input del File di supporto che è connesso toohello sovrimpressione grafica componente.</span><span class="sxs-lookup"><span data-stu-id="77109-172">hello name of hello logo file is sent tooanother Media File Input that is connected toohello graphic overlay component.</span></span>

> [!NOTE]
> <span data-ttu-id="77109-173">nome di file video Hello viene inviato toohello primarySourceFile proprietà.</span><span class="sxs-lookup"><span data-stu-id="77109-173">hello video file name is sent toohello primarySourceFile property.</span></span> <span data-ttu-id="77109-174">motivo di Hello è toouse nel flusso di lavoro di hello per la generazione del nome file di output corretto hello utilizzando espressioni, ad esempio questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="77109-174">hello reason for this is toouse this property in hello workflow for building hello correct output file name using Expressions, for example.</span></span>

### <a name="step-by-step-workflow-creation"></a><span data-ttu-id="77109-175">Procedura dettagliata di creazione del flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="77109-175">Step-by-step workflow creation</span></span>
<span data-ttu-id="77109-176">Di seguito è hello passaggi toocreate un flusso di lavoro viene considerato come input due file: un video e un'immagine.</span><span class="sxs-lookup"><span data-stu-id="77109-176">Here are hello steps toocreate a workflow that takes two files as input: a video and an image.</span></span> <span data-ttu-id="77109-177">Sovrapporrà immagine hello di sopra hello video.</span><span class="sxs-lookup"><span data-stu-id="77109-177">It will overlay hello image on top of hello video.</span></span>

<span data-ttu-id="77109-178">Aprire **Progettazione flussi di lavoro** e selezionare **File** > **New Workspace (Nuova area di lavoro)** > **Transcode Blueprint**.</span><span class="sxs-lookup"><span data-stu-id="77109-178">Open **Workflow Designer** and select **File** > **New Workspace** > **Transcode Blueprint**.</span></span>

<span data-ttu-id="77109-179">nuovo flusso di lavoro Hello mostra tre elementi:</span><span class="sxs-lookup"><span data-stu-id="77109-179">hello new workflow shows three elements:</span></span>

* <span data-ttu-id="77109-180">Primary Source File</span><span class="sxs-lookup"><span data-stu-id="77109-180">Primary Source File</span></span>
* <span data-ttu-id="77109-181">Clip List XML</span><span class="sxs-lookup"><span data-stu-id="77109-181">Clip List XML</span></span>
* <span data-ttu-id="77109-182">Output File/Asset</span><span class="sxs-lookup"><span data-stu-id="77109-182">Output File/Asset</span></span>  

![Nuovo flusso di lavoro della codifica](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

<span data-ttu-id="77109-184">*Nuovo flusso di lavoro della codifica*</span><span class="sxs-lookup"><span data-stu-id="77109-184">*New Encoding Workflow*</span></span>

<span data-ttu-id="77109-185">Nel file multimediale di input di ordinamento tooaccept hello, iniziare con l'aggiunta di un componente di Input di File multimediali.</span><span class="sxs-lookup"><span data-stu-id="77109-185">In order tooaccept hello input media file, start with adding a Media File Input component.</span></span> <span data-ttu-id="77109-186">tooadd un componente toohello del flusso di lavoro, cercare nella casella di ricerca Repository hello e trascinare la voce hello desiderato nel riquadro della finestra di progettazione di hello.</span><span class="sxs-lookup"><span data-stu-id="77109-186">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span>

<span data-ttu-id="77109-187">Successivamente, aggiungere hello file video toobe utilizzato per la progettazione del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="77109-187">Next, add hello video file toobe used for designing your workflow.</span></span> <span data-ttu-id="77109-188">toodo in tal caso, fare clic su riquadro sfondo hello nella finestra di progettazione del flusso di lavoro e cercare proprietà File di origine primario hello nel riquadro di destra proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="77109-188">toodo so, click hello background pane in Workflow Designer and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="77109-189">Fare clic sull'icona di cartella hello e selezionare i file video appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="77109-189">Click hello folder icon and select hello appropriate video file.</span></span>

![File di origine primario](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

<span data-ttu-id="77109-191">*File di origine primario*</span><span class="sxs-lookup"><span data-stu-id="77109-191">*Primary File Source*</span></span>

<span data-ttu-id="77109-192">Successivamente, è possibile specificare file video hello nel componente di Input di File multimediali hello.</span><span class="sxs-lookup"><span data-stu-id="77109-192">Next, specify hello video file in hello Media File Input component.</span></span>   

![Origine Media File Input](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

<span data-ttu-id="77109-194">*Origine Media File Input*</span><span class="sxs-lookup"><span data-stu-id="77109-194">*Media File Input Source*</span></span>

<span data-ttu-id="77109-195">Non appena questa operazione viene eseguita, hello Input File multimediali componente esaminare il file hello e popolare il PIN tooreflect hello file di output controllato.</span><span class="sxs-lookup"><span data-stu-id="77109-195">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file that it inspected.</span></span>

<span data-ttu-id="77109-196">passaggio successivo Hello è tooadd un tooRec.709 spazio colore di "Aggiornamento di tipo dati Video" toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="77109-196">hello next step is tooadd a "Video Data Type Updater" toospecify hello color space tooRec.709.</span></span> <span data-ttu-id="77109-197">Aggiungere un convertitore di formato Video"" che è impostato il tipo di Layout/Layout tooData = configurabile planare.</span><span class="sxs-lookup"><span data-stu-id="77109-197">Add a "Video Format Converter" that is set tooData Layout/Layout type = Configurable Planar.</span></span> <span data-ttu-id="77109-198">Questo verrà convertito formato tooa di flusso video hello che può essere eseguita come origine del componente di sovrapposizione hello.</span><span class="sxs-lookup"><span data-stu-id="77109-198">This will convert hello video stream tooa format that can be taken as a source of hello overlay component.</span></span>

![Strumento di aggiornamento tipo dati video e Convertitore formato video](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

<span data-ttu-id="77109-200">*Strumento di aggiornamento tipo dati video e Convertitore formato video*</span><span class="sxs-lookup"><span data-stu-id="77109-200">*Video Data Type Updater and Format Converter*</span></span>

![Layout type = Configurable Planar (Tipo layout = Planare configurabile)](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

<span data-ttu-id="77109-202">*Il tipo di layout è Planare configurabile*</span><span class="sxs-lookup"><span data-stu-id="77109-202">*Layout type is Configurable Planar*</span></span>

<span data-ttu-id="77109-203">Successivamente, aggiungere un componente sovrimpressione Video e connessione hello pin video (non compressa) toohello (non compressa) video del pin di input del file di supporto hello.</span><span class="sxs-lookup"><span data-stu-id="77109-203">Next, add a Video Overlay component and connect hello (uncompressed) video pin toohello (uncompressed) video pin of hello media file input.</span></span>

<span data-ttu-id="77109-204">Aggiungere un altro Input del File di supporto (file del logo tooload hello) fare clic su questo componente e rinominarlo troppo "Supporto di File di Input Logo" e selezionare un'immagine (file con estensione png, ad esempio) nella proprietà di file hello.</span><span class="sxs-lookup"><span data-stu-id="77109-204">Add another Media File Input (tooload hello logo file), click on this component and rename it too"Media File Input Logo", and select an image (a .png file for example) in hello file property.</span></span> <span data-ttu-id="77109-205">Connettersi hello immagine non compressi toohello immagine non compressi spina della sovrimpressione hello.</span><span class="sxs-lookup"><span data-stu-id="77109-205">Connect hello Uncompressed image pin toohello Uncompressed image pin of hello overlay.</span></span>

![Componente della sovrimpressione e origine del file di immagine](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

<span data-ttu-id="77109-207">*Componente della sovrimpressione e origine del file di immagine*</span><span class="sxs-lookup"><span data-stu-id="77109-207">*Overlay component and image file source*</span></span>

<span data-ttu-id="77109-208">Se si desidera toomodify hello posizione del logo hello nel video hello (ad esempio, è possibile tooposition al 10% di fuori di inizio hello era angolo del video hello), deselezionare la casella di controllo "Input manuale" hello.</span><span class="sxs-lookup"><span data-stu-id="77109-208">If you want toomodify hello position of hello logo on hello video (for example, you might want tooposition it at 10 percent off of hello top left corner of hello video), clear hello "Manual Input" check box.</span></span> <span data-ttu-id="77109-209">È possibile farlo perché si sta usando un componente di sovrapposizione di Input di File multimediali tooprovide hello logo file toohello.</span><span class="sxs-lookup"><span data-stu-id="77109-209">You can do this because you are using a Media File Input tooprovide hello logo file toohello overlay component.</span></span>

![Posizione della sovrimpressione](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

<span data-ttu-id="77109-211">*Posizione della sovrimpressione*</span><span class="sxs-lookup"><span data-stu-id="77109-211">*Overlay position*</span></span>

<span data-ttu-id="77109-212">tooencode hello tooH.264 flusso video, aggiungere hello codificatore Video AVC e l'area della finestra di progettazione toohello AAC codificatore componenti.</span><span class="sxs-lookup"><span data-stu-id="77109-212">tooencode hello video stream tooH.264, add hello AVC Video Encoder and AAC encoder components toohello designer surface.</span></span> <span data-ttu-id="77109-213">Connettere i pin hello.</span><span class="sxs-lookup"><span data-stu-id="77109-213">Connect hello pins.</span></span>
<span data-ttu-id="77109-214">Impostare codificatore AAC hello e selezionare conversione formato Audio/impostazione predefinita: 2.0 (L, R).</span><span class="sxs-lookup"><span data-stu-id="77109-214">Set up hello AAC encoder and select Audio Format Conversion/Preset : 2.0 (L, R).</span></span>

![Codificatori audio e video](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

<span data-ttu-id="77109-216">*Codificatori audio e video*</span><span class="sxs-lookup"><span data-stu-id="77109-216">*Audio and Video Encoders*</span></span>

<span data-ttu-id="77109-217">A questo punto aggiungere hello **ISO Mpeg-4 Multiplexer** e **File di Output** componenti e connessione pin hello, come illustrato.</span><span class="sxs-lookup"><span data-stu-id="77109-217">Now add hello **ISO Mpeg-4 Multiplexer** and **File Output** components and connect hello pins as shown.</span></span>

![Multiplexer MP4 e file di output](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

<span data-ttu-id="77109-219">*Multiplexer MP4 e file di output*</span><span class="sxs-lookup"><span data-stu-id="77109-219">*MP4 multiplexer and file output*</span></span>

<span data-ttu-id="77109-220">È necessario tooset hello nome per il file di output di hello.</span><span class="sxs-lookup"><span data-stu-id="77109-220">You need tooset hello name for hello output file.</span></span> <span data-ttu-id="77109-221">Fare clic su hello **File di Output** componente e Modifica espressione hello per file hello:</span><span class="sxs-lookup"><span data-stu-id="77109-221">Click hello **File Output** component and edit hello expression for hello file:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Nome file di output](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

<span data-ttu-id="77109-223">*Nome file di output*</span><span class="sxs-lookup"><span data-stu-id="77109-223">*File output name*</span></span>

<span data-ttu-id="77109-224">È possibile eseguire i flussi di lavoro hello localmente toocheck che venga eseguito correttamente.</span><span class="sxs-lookup"><span data-stu-id="77109-224">You can run hello workflow locally toocheck that it is running correctly.</span></span>

<span data-ttu-id="77109-225">Al termine, è possibile eseguire il flusso di lavoro in Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="77109-225">After it finishes, you can run it in Azure Media Services.</span></span>

<span data-ttu-id="77109-226">Innanzitutto, preparare un asset in servizi multimediali di Azure con due file: file video hello e logo hello.</span><span class="sxs-lookup"><span data-stu-id="77109-226">First, prepare an asset in Azure Media Services with two files in it: hello video file and hello logo.</span></span> <span data-ttu-id="77109-227">È possibile farlo tramite hello .NET o API REST.</span><span class="sxs-lookup"><span data-stu-id="77109-227">You can do this by using hello .NET or REST API.</span></span> <span data-ttu-id="77109-228">È anche possibile farlo tramite hello portale di Azure o [Esplora servizi multimediali di Azure](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span><span class="sxs-lookup"><span data-stu-id="77109-228">You can also do this by using hello Azure portal or [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span></span>

<span data-ttu-id="77109-229">In questa esercitazione illustra come asset toomanage con AMSE.</span><span class="sxs-lookup"><span data-stu-id="77109-229">This tutorial shows you how toomanage assets with AMSE.</span></span> <span data-ttu-id="77109-230">Esistono due tooan asset di modi tooadd file:</span><span class="sxs-lookup"><span data-stu-id="77109-230">There are two ways tooadd files tooan asset:</span></span>

* <span data-ttu-id="77109-231">Creare una cartella locale, copiare i file hello due e trascinamento della selezione hello cartella toohello **Asset** scheda.</span><span class="sxs-lookup"><span data-stu-id="77109-231">Create a local folder, copy hello two files in it, and drag and drop hello folder toohello **Asset** tab.</span></span>
* <span data-ttu-id="77109-232">Caricare file video di hello come asset, visualizzare le informazioni di asset hello, andare toohello file scheda e caricare un file aggiuntivo (logo).</span><span class="sxs-lookup"><span data-stu-id="77109-232">Upload hello video file as an asset, display hello asset information, go toohello files tab, and upload an additional file (logo).</span></span>

> [!NOTE]
> <span data-ttu-id="77109-233">Verificare che tooset un file primario nel asset hello (hello video file principale).</span><span class="sxs-lookup"><span data-stu-id="77109-233">Make sure tooset a primary file in hello asset (hello main video file).</span></span>

![File di asset nello strumento di esplorazione di Servizi multimediali di Azure](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

<span data-ttu-id="77109-235">*File di asset nello strumento di esplorazione di Servizi multimediali di Azure*</span><span class="sxs-lookup"><span data-stu-id="77109-235">*Asset files in AMSE*</span></span>

<span data-ttu-id="77109-236">Selezionare asset hello e scegliere tooencode con codificatore Premium.</span><span class="sxs-lookup"><span data-stu-id="77109-236">Select hello asset and choose tooencode it with Premium Encoder.</span></span> <span data-ttu-id="77109-237">Caricamento del flusso di lavoro hello e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="77109-237">Upload hello workflow and select it.</span></span>

<span data-ttu-id="77109-238">Fare clic su hello pulsante toopass dati toohello processore e aggiungere le proprietà di runtime XML tooset hello seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="77109-238">Click hello button toopass data toohello processor, and add hello following XML tooset hello runtime properties:</span></span>

![Codificatore Premium nello strumento di esplorazione di Servizi multimediali di Azure](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

<span data-ttu-id="77109-240">*Codificatore Premium nello strumento di esplorazione di Servizi multimediali di Azure*</span><span class="sxs-lookup"><span data-stu-id="77109-240">*Premium Encoder in AMSE*</span></span>

<span data-ttu-id="77109-241">Quindi, incollare hello segue i dati XML.</span><span class="sxs-lookup"><span data-stu-id="77109-241">Then, paste hello following XML data.</span></span> <span data-ttu-id="77109-242">È necessario il nome hello toospecify di file video hello per hello Input del File di supporto e primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="77109-242">You need toospecify hello name of hello video file for both hello Media File Input and primarySourceFile.</span></span> <span data-ttu-id="77109-243">Specificare il nome di hello hello del file del logo hello troppo.</span><span class="sxs-lookup"><span data-stu-id="77109-243">Specify hello name of hello file name for hello logo too.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

![setRuntimeProperties](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture20_amsexmldata.png)

<span data-ttu-id="77109-245">*setRuntimeProperties*</span><span class="sxs-lookup"><span data-stu-id="77109-245">*setRuntimeProperties*</span></span>

<span data-ttu-id="77109-246">Se si utilizza toocreate .NET SDK hello e attività hello, passato come stringa di configurazione hello toobe questi dati XML.</span><span class="sxs-lookup"><span data-stu-id="77109-246">If you use hello .NET SDK toocreate and run hello task, this XML data has toobe passed as hello configuration string.</span></span>

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

<span data-ttu-id="77109-247">Dopo aver completato il processo di hello, file MP4 hello in hello output asset Visualizza sovrapposizione hello!</span><span class="sxs-lookup"><span data-stu-id="77109-247">After hello job is complete, hello MP4 file in hello output asset displays hello overlay!</span></span>

![Sovrapporre su hello video](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

<span data-ttu-id="77109-249">*Sovrapporre su hello video*</span><span class="sxs-lookup"><span data-stu-id="77109-249">*Overlay on hello video*</span></span>

<span data-ttu-id="77109-250">È possibile scaricare il flusso di lavoro di hello esempio da [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span><span class="sxs-lookup"><span data-stu-id="77109-250">You can download hello sample workflow from [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span></span>

## <a name="example-2--multiple-audio-language-encoding"></a><span data-ttu-id="77109-251">Esempio 2: Codifica di più lingue per l'audio</span><span class="sxs-lookup"><span data-stu-id="77109-251">Example 2 : Multiple audio language encoding</span></span>

<span data-ttu-id="77109-252">Un esempio di flusso di lavoro per la codifica di più lingue per l'audio è disponibile in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span><span class="sxs-lookup"><span data-stu-id="77109-252">An example of multiple audio language encoding workfkow is available in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span></span>

<span data-ttu-id="77109-253">Questa cartella contiene un flusso di lavoro di esempio che può essere utilizzato tooencode un asset di file MXF file tooa più file MP4 con più tracce audio.</span><span class="sxs-lookup"><span data-stu-id="77109-253">This folder contains a sample workflow which can be used tooencode a MXF file tooa multi MP4 files asset with multiple audio tracks.</span></span>

<span data-ttu-id="77109-254">Questo flusso di lavoro presuppone che Hello MXF contenente una traccia audio; tracce audio aggiuntive Hello devono essere passate come file audio (WAV o MP4...).</span><span class="sxs-lookup"><span data-stu-id="77109-254">This workflow assumes that hello MXF file contains one audio track ; hello additional audio tracks should be passed as seperate audio files (WAV or MP4...).</span></span>

<span data-ttu-id="77109-255">tooencode, effettuare le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="77109-255">tooencode, please follow these steps:</span></span>

* <span data-ttu-id="77109-256">Creare un asset di servizi multimediali con hello e file MXF hello Audio (file 0 too18 audio).</span><span class="sxs-lookup"><span data-stu-id="77109-256">Create a Media Services asset with hello MXF file and hello Audio files (0 too18 audio files).</span></span>
* <span data-ttu-id="77109-257">Verificare che il file MXF hello è impostato come un file primario.</span><span class="sxs-lookup"><span data-stu-id="77109-257">Make sure that hello MXF file is set as a primary file.</span></span>
* <span data-ttu-id="77109-258">Creare un processo e un'attività con il processore di codificatore del flusso di lavoro Premium hello.</span><span class="sxs-lookup"><span data-stu-id="77109-258">Create a job and a task using hello Premium Workflow Encoder processor.</span></span> <span data-ttu-id="77109-259">Utilizzo del flusso di lavoro hello fornito (MultiMP4 1080p-19audio v1.workflow).</span><span class="sxs-lookup"><span data-stu-id="77109-259">Use hello workflow provided (MultiMP4-1080p-19audio-v1.workflow).</span></span>
* <span data-ttu-id="77109-260">Passare l'attività di hello setruntime.xml dati toohello (se si utilizza Esplora servizi multimediali di Azure, utilizzare hello "pass flusso di lavoro toohello dati xml" pulsante).</span><span class="sxs-lookup"><span data-stu-id="77109-260">Pass hello setruntime.xml data toohello task (if you use Azure Media Services Explorer, use hello “pass xml data toohello workflow” button).</span></span>
  * <span data-ttu-id="77109-261">Aggiornare hello dati toospecify hello file corretto linguaggi e i nomi di tag XML.</span><span class="sxs-lookup"><span data-stu-id="77109-261">Please update hello XML data toospecify hello correct file names and languages tags.</span></span>
  * <span data-ttu-id="77109-262">flusso di lavoro Hello include componenti audio denominati 1 Audio tooAudio 18.</span><span class="sxs-lookup"><span data-stu-id="77109-262">hello workflow has audio components named Audio 1 tooAudio 18.</span></span>
  * <span data-ttu-id="77109-263">RFC5646 è supportata per il tag di linguaggio hello.</span><span class="sxs-lookup"><span data-stu-id="77109-263">RFC5646 is supported for hello language tag.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
<transcodeRequest>
  <setRuntimeProperties>
    <property propertyPath="Media File Input Video/filename" value="MainVideo.mxf" />
    <property propertyPath="Language/language_code" value="en" />
    <property propertyPath="/primarySourceFile" value="MainVideo.mxf" />
    <property propertyPath="Audio 1/Media File Input/filename" value="french-audio.wav" />
    <property propertyPath="Audio 1/Language/language_code" value="fr" />
    <property propertyPath="Audio 2/Media File Input/filename" value="german-audio.wav" />
    <property propertyPath="Audio 2/Language/language_code" value="de" />
    <property propertyPath="Audio 3/Media File Input/filename" value="japanese-audio.wav" />
    <property propertyPath="Audio 3/Language/language_code" value="ja" />
  </setRuntimeProperties>
</transcodeRequest>
```

* <span data-ttu-id="77109-264">asset codificato Hello conterrà più tracce audio di linguaggio e queste tracce devono essere selezionabile in Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="77109-264">hello encoded asset will contain multi language audio tracks and these tracks should be selectable in Azure Media Player.</span></span>

## <a name="see-also"></a><span data-ttu-id="77109-265">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="77109-265">See also</span></span>
* [<span data-ttu-id="77109-266">Introduzione alla codifica Premium in Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="77109-266">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="77109-267">Come toouse codifica Premium in servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="77109-267">How toouse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="77109-268">Codifica di contenuti su richiesta con Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="77109-268">Encoding on-demand content with Azure Media Services</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)
* [<span data-ttu-id="77109-269">Codec e formati del flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="77109-269">Media Encoder Premium Workflow formats and codecs</span></span>](media-services-premium-workflow-encoder-formats.md)
* [<span data-ttu-id="77109-270">File del flusso di lavoro di esempio</span><span class="sxs-lookup"><span data-stu-id="77109-270">Sample workflow files</span></span>](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [<span data-ttu-id="77109-271">Strumento di esplorazione di Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="77109-271">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="77109-272">Percorsi di apprendimento di Media Services</span><span class="sxs-lookup"><span data-stu-id="77109-272">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="77109-273">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="77109-273">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

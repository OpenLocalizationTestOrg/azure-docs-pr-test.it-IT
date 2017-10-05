---
title: "Uso di più file di input e proprietà del componente con il codificatore Premium - Azure | Documentazione Microsoft"
description: "Questo argomento illustra come usare setRuntimeProperties per usare più file di input e passare dati personalizzati al processore di contenuti multimediali del flusso di lavoro Premium del codificatore multimediale."
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
ms.openlocfilehash: df1ee5089a0af6ffce1431b658843fcb34a66ce5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a><span data-ttu-id="f7c48-103">Uso di più file di input e proprietà del componente con il codificatore Premium</span><span class="sxs-lookup"><span data-stu-id="f7c48-103">Using multiple input files and component properties with Premium Encoder</span></span>
## <a name="overview"></a><span data-ttu-id="f7c48-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f7c48-104">Overview</span></span>
<span data-ttu-id="f7c48-105">In alcuni scenari potrebbe essere necessario personalizzare le proprietà del componente, specificare contenuto Clip List XML oppure inviare più file di input durante l'invio di un'attività con il processore di contenuti multimediali del **flusso di lavoro Premium del codificatore multimediale** .</span><span class="sxs-lookup"><span data-stu-id="f7c48-105">There are scenarios in which you might need to customize component properties, specify Clip List XML content, or send multiple input files when you submit a task with the **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="f7c48-106">Di seguito sono riportati alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="f7c48-106">Some examples are:</span></span>

* <span data-ttu-id="f7c48-107">Sovrapporre testo sul video e impostare il valore del testo, ad esempio la data corrente, in fase di esecuzione per ogni video di input.</span><span class="sxs-lookup"><span data-stu-id="f7c48-107">Overlaying text on video and setting the text value (for example, the current date) at runtime for each input video.</span></span>
* <span data-ttu-id="f7c48-108">Personalizzare il contenuto Clip List XML per specificare uno o più file di origine, con o senza trimming e così via.</span><span class="sxs-lookup"><span data-stu-id="f7c48-108">Customizing the Clip List XML (to specify one or several source files, with or without trimming, etc.).</span></span>
* <span data-ttu-id="f7c48-109">Sovrapporre un logo al video di input durante la codifica del video.</span><span class="sxs-lookup"><span data-stu-id="f7c48-109">Overlaying a logo image on the input video while the video is encoded.</span></span>
* <span data-ttu-id="f7c48-110">Codifica di più lingue per l'audio.</span><span class="sxs-lookup"><span data-stu-id="f7c48-110">Multiple audio language encoding.</span></span>

<span data-ttu-id="f7c48-111">Per indicare a **Flusso di lavoro Premium del codificatore multimediale** che verranno modificate alcune proprietà nel flusso di lavoro quando si crea l'attività o si inviano più file di input, è necessario usare una stringa di configurazione contenente **setRuntimeProperties** e/o **transcodeSource**.</span><span class="sxs-lookup"><span data-stu-id="f7c48-111">To let the **Media Encoder Premium Workflow** know that you are changing some properties in the workflow when you create the task or send multiple input files, you have to use a configuration string that contains **setRuntimeProperties** and/or **transcodeSource**.</span></span> <span data-ttu-id="f7c48-112">Questo argomento ne illustra l'uso.</span><span class="sxs-lookup"><span data-stu-id="f7c48-112">This topic explains how to use them.</span></span>

## <a name="configuration-string-syntax"></a><span data-ttu-id="f7c48-113">Sintassi della stringa di configurazione</span><span class="sxs-lookup"><span data-stu-id="f7c48-113">Configuration string syntax</span></span>
<span data-ttu-id="f7c48-114">La stringa di configurazione da impostare nell'attività di codifica usa un documento XML simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f7c48-114">The configuration string to set in the encoding task uses an XML document that looks like this:</span></span>

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

<span data-ttu-id="f7c48-115">Di seguito è riportato il codice C# che legge la configurazione XML da un file, la aggiorna con il nome di file video corretto e la passa all'attività di un processo:</span><span class="sxs-lookup"><span data-stu-id="f7c48-115">The following is the C# code that reads the XML configuration from a file, update it with the right video filename and passes it to the task in a job:</span></span>

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass to it the name of the 
// processor to use for the specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with the encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify the input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset to contain the results of the job. 
// This output is specified as AssetCreationOptions.None, which 
// means the output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a><span data-ttu-id="f7c48-116">Personalizzazione delle proprietà del componente</span><span class="sxs-lookup"><span data-stu-id="f7c48-116">Customizing component properties</span></span>
### <a name="property-with-a-simple-value"></a><span data-ttu-id="f7c48-117">Proprietà con un valore semplice</span><span class="sxs-lookup"><span data-stu-id="f7c48-117">Property with a simple value</span></span>
<span data-ttu-id="f7c48-118">In alcuni casi è utile personalizzare una proprietà del componente insieme al file del flusso di lavoro che verrà eseguito dal flusso di lavoro Premium del codificatore multimediale.</span><span class="sxs-lookup"><span data-stu-id="f7c48-118">In some cases, it is useful to customize a component property together with the workflow file that is going to be executed by Media Encoder Premium Workflow.</span></span>

<span data-ttu-id="f7c48-119">Si supponga che sia stato progettato un flusso di lavoro che sovrappone testo ai video e che il testo, ad esempio la data corrente, debba essere impostato in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f7c48-119">Suppose you designed a workflow that overlays text on your videos, and the text (for example, the current date) is supposed to be set at runtime.</span></span> <span data-ttu-id="f7c48-120">Questa operazione può essere eseguita inviando il testo da impostare come nuovo valore della proprietà text del componente di sovrapposizione dell'attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="f7c48-120">You can do this by sending the text to be set as the new value for the text property of the overlay component from the encoding task.</span></span> <span data-ttu-id="f7c48-121">Questo meccanismo consente di modificare altre proprietà di un componente nel flusso di lavoro, ad esempio la posizione o il colore della sovrapposizione, la velocità in bit del codificatore AVC e così via.</span><span class="sxs-lookup"><span data-stu-id="f7c48-121">You can use this mechanism to change other properties of a component in the workflow (such as the position or color of the overlay, the bitrate of the AVC encoder, etc.).</span></span>

<span data-ttu-id="f7c48-122">**setRuntimeProperties** viene usato per sostituire una proprietà nei componenti del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f7c48-122">**setRuntimeProperties** is used to override a property in the components of the workflow.</span></span>

<span data-ttu-id="f7c48-123">Esempio:</span><span class="sxs-lookup"><span data-stu-id="f7c48-123">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text To Image Converter/text" value="Today is Friday the 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a><span data-ttu-id="f7c48-124">Proprietà con un valore XML</span><span class="sxs-lookup"><span data-stu-id="f7c48-124">Property with an XML value</span></span>
<span data-ttu-id="f7c48-125">Per impostare una proprietà che prevede un valore XML, incapsulare usando `<![CDATA[ and ]]>`.</span><span class="sxs-lookup"><span data-stu-id="f7c48-125">To set a property that expects an XML value, encapsulate by using `<![CDATA[ and ]]>`.</span></span>

<span data-ttu-id="f7c48-126">Esempio:</span><span class="sxs-lookup"><span data-stu-id="f7c48-126">Example:</span></span>

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
> <span data-ttu-id="f7c48-127">Non inserire un ritorno a capo subito dopo `<![CDATA[`.</span><span class="sxs-lookup"><span data-stu-id="f7c48-127">Make sure not to put a carriage return just after `<![CDATA[`.</span></span>

### <a name="propertypath-value"></a><span data-ttu-id="f7c48-128">Valore di propertyPath</span><span class="sxs-lookup"><span data-stu-id="f7c48-128">propertyPath value</span></span>
<span data-ttu-id="f7c48-129">Negli esempi precedenti, il valore di propertyPath era "/Media File Input/filename", o "/inactiveTimeout" oppure "clipListXml".</span><span class="sxs-lookup"><span data-stu-id="f7c48-129">In the previous examples, the propertyPath was "/Media File Input/filename" or "/inactiveTimeout" or "clipListXml".</span></span>
<span data-ttu-id="f7c48-130">Si tratta in genere del nome del componente seguito dal nome della proprietà.</span><span class="sxs-lookup"><span data-stu-id="f7c48-130">This is, in general, the name of the component, then the name of the property.</span></span> <span data-ttu-id="f7c48-131">Il percorso può avere più o meno livelli, ad esempio "/primarySourceFile" perché la proprietà è alla radice del flusso di lavoro o "/Video Processing/Graphic Overlay/Opacity" perché la sovrimpressione è in un gruppo.</span><span class="sxs-lookup"><span data-stu-id="f7c48-131">The path can have more or fewer levels, like "/primarySourceFile" (because the property is at the root of the workflow) or "/Video Processing/Graphic Overlay/Opacity" (because the Overlay is in a group).</span></span>    

<span data-ttu-id="f7c48-132">Per verificare il percorso e il nome della proprietà, usare il pulsante di azione immediatamente accanto a ogni proprietà.</span><span class="sxs-lookup"><span data-stu-id="f7c48-132">To check the path and property name, use the action button that is immediately beside each property.</span></span> <span data-ttu-id="f7c48-133">È possibile fare clic su questo pulsante di azione e selezionare **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="f7c48-133">You can click this action button and select **Edit**.</span></span> <span data-ttu-id="f7c48-134">Verrà visualizzato il nome effettivo della proprietà e lo spazio dei nomi immediatamente sopra.</span><span class="sxs-lookup"><span data-stu-id="f7c48-134">This will show you the actual name of the property, and immediately above it, the namespace.</span></span>

![Azione/modifica](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Proprietà](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a><span data-ttu-id="f7c48-137">Più file di input</span><span class="sxs-lookup"><span data-stu-id="f7c48-137">Multiple input files</span></span>
<span data-ttu-id="f7c48-138">Ogni attività inviata al **flusso di lavoro Premium del codificatore multimediale** richiede due asset:</span><span class="sxs-lookup"><span data-stu-id="f7c48-138">Each task that you submit to the **Media Encoder Premium Workflow** requires two assets:</span></span>

* <span data-ttu-id="f7c48-139">il primo è un *asset di flusso di lavoro* che contiene un file di flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f7c48-139">The first one is a *Workflow Asset* that contains a workflow file.</span></span> <span data-ttu-id="f7c48-140">È possibile progettare file di flusso di lavoro usando [Progettazione flussi di lavoro](media-services-workflow-designer.md).</span><span class="sxs-lookup"><span data-stu-id="f7c48-140">You can design workflow files by using the [Workflow Designer](media-services-workflow-designer.md).</span></span>
* <span data-ttu-id="f7c48-141">il secondo è un *asset multimediale* che contiene i file multimediali da codificare.</span><span class="sxs-lookup"><span data-stu-id="f7c48-141">The second one is a *Media Asset* that contains the media file(s) that you want to encode.</span></span>

<span data-ttu-id="f7c48-142">Quando si inviano più file multimediali al **flusso di lavoro Premium del codificatore multimediale** , si applicano i vincoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="f7c48-142">When you're sending multiple media files to the **Media Encoder Premium Workflow** encoder, the following constraints apply:</span></span>

* <span data-ttu-id="f7c48-143">Tutti i file multimediali devono essere nello stesso *asset multimediale*.</span><span class="sxs-lookup"><span data-stu-id="f7c48-143">All the media files must be in the same *Media Asset*.</span></span> <span data-ttu-id="f7c48-144">L'uso di più asset multimediali non è supportato.</span><span class="sxs-lookup"><span data-stu-id="f7c48-144">Using multiple Media Assets is not supported.</span></span>
* <span data-ttu-id="f7c48-145">È necessario impostare il file primario nell'asset multimediale. Si tratta idealmente del file video principale che il codificatore dovrà elaborare.</span><span class="sxs-lookup"><span data-stu-id="f7c48-145">You must set the primary file in this Media Asset (ideally, this is the main video file that the encoder is asked to process).</span></span>
* <span data-ttu-id="f7c48-146">È necessario passare al processore dati di configurazione che includono l'elemento **setRuntimeProperties** e/o **transcodeSource**.</span><span class="sxs-lookup"><span data-stu-id="f7c48-146">It is necessary to pass configuration data that includes the **setRuntimeProperties** and/or **transcodeSource** element to the processor.</span></span>
  * <span data-ttu-id="f7c48-147">**setRuntimeProperties** viene usato per sostituire la proprietà Filename o un'altra proprietà nei componenti del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f7c48-147">**setRuntimeProperties** is used to override the filename property or another property in the components of the workflow.</span></span>
  * <span data-ttu-id="f7c48-148">**transcodeSource** viene usato per specificare il contenuto Clip List XML.</span><span class="sxs-lookup"><span data-stu-id="f7c48-148">**transcodeSource** is used to specify the Clip List XML content.</span></span>

<span data-ttu-id="f7c48-149">Connessioni nel flusso di lavoro:</span><span class="sxs-lookup"><span data-stu-id="f7c48-149">Connections in the workflow:</span></span>

* <span data-ttu-id="f7c48-150">se si usano uno o più componenti Media File Input e si prevede di usare **setRuntimeProperties** per specificare il nome del file, non collegare il pin del componente file primario ai componenti Media File Input.</span><span class="sxs-lookup"><span data-stu-id="f7c48-150">If you use one or several Media File Input components and plan to use **setRuntimeProperties** to specify the file name, then do not connect the primary file component pin to them.</span></span> <span data-ttu-id="f7c48-151">Assicurarsi che non esistano collegamenti tra l'oggetto file primario e i componenti Media File Input.</span><span class="sxs-lookup"><span data-stu-id="f7c48-151">Make sure that there is no connection between the primary file object and the Media File Input(s).</span></span>
* <span data-ttu-id="f7c48-152">Se si preferisce usare Clip List XML e un componente Media Source è possibile collegare entrambi.</span><span class="sxs-lookup"><span data-stu-id="f7c48-152">If you prefer to use Clip List XML and one Media Source component, then you can connect both together.</span></span>

![Nessun collegamento dal file di origine primario a Media File Input](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

<span data-ttu-id="f7c48-154">*Non sono presenti collegamenti dal file primario ai componenti di Media File Input se si usa setRuntimeProperties per impostare la proprietà Filename.*</span><span class="sxs-lookup"><span data-stu-id="f7c48-154">*There is no connection from the primary file to Media File Input component(s) if you use setRuntimeProperties to set the filename property.*</span></span>

![Collegamento da Clip List XML a Clip List Source](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

<span data-ttu-id="f7c48-156">*È possibile collegare Clip List XML a Media Source e usare transcodeSource.*</span><span class="sxs-lookup"><span data-stu-id="f7c48-156">*You can connect Clip List XML to Media Source and use transcodeSource.*</span></span>

### <a name="clip-list-xml-customization"></a><span data-ttu-id="f7c48-157">Personalizzazione di Clip List XML</span><span class="sxs-lookup"><span data-stu-id="f7c48-157">Clip List XML customization</span></span>
<span data-ttu-id="f7c48-158">È possibile specificare contenuto Clip List XML nel flusso di lavoro, in fase di esecuzione, usando **transcodeSource** nel codice XML della stringa di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f7c48-158">You can specify the Clip List XML in the workflow at runtime by using **transcodeSource** in the configuration string XML.</span></span> <span data-ttu-id="f7c48-159">Questa operazione richiede che il pin di Clip List XML sia collegato al componente Media Source nel flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f7c48-159">This requires the Clip List XML pin to be connected to the Media Source component in the workflow.</span></span>

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

<span data-ttu-id="f7c48-160">Per specificare /primarySourceFile per usare questa proprietà per l'assegnazione di un nome ai file di output con espressioni, è consigliabile passare Clip List XML come proprietà, *dopo* la proprietà /primarySourceFile, per evitare che Clip List venga sostituito dall'impostazione di /primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="f7c48-160">If you want to specify /primarySourceFile to use this property to name the output files by using 'Expressions', then we recommend passing the Clip List XML as a property *after* the /primarySourceFile property, to avoid having the Clip List be overridden by the /primarySourceFile setting.</span></span>

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

<span data-ttu-id="f7c48-161">Con altro trimming preciso al fotogramma:</span><span class="sxs-lookup"><span data-stu-id="f7c48-161">With additional frame-accurate trimming:</span></span>

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

## <a name="example-1--overlay-an-image-on-top-of-the-video"></a><span data-ttu-id="f7c48-162">Esempio 1: Sovrapporre un'immagine sul video</span><span class="sxs-lookup"><span data-stu-id="f7c48-162">Example 1 : Overlay an image on top of the video</span></span>

### <a name="presentation"></a><span data-ttu-id="f7c48-163">Presentazione</span><span class="sxs-lookup"><span data-stu-id="f7c48-163">Presentation</span></span>
<span data-ttu-id="f7c48-164">Si consideri un esempio in cui si vuole sovrapporre un logo al video di input durante la codifica del video.</span><span class="sxs-lookup"><span data-stu-id="f7c48-164">Consider an example in which you want to overlay a logo image on the input video while the video is encoded.</span></span> <span data-ttu-id="f7c48-165">In questo esempio, il video di input è denominato "Microsoft_HoloLens_Possibilities_816p24.mp4" e il logo è denominato "logo.png".</span><span class="sxs-lookup"><span data-stu-id="f7c48-165">In this example, the input video is named "Microsoft_HoloLens_Possibilities_816p24.mp4" and the logo is named "logo.png".</span></span> <span data-ttu-id="f7c48-166">Eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f7c48-166">You should perform the following steps:</span></span>

* <span data-ttu-id="f7c48-167">Creare un asset del flusso di lavoro con il file del flusso di lavoro. L'esempio è riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="f7c48-167">Create a Workflow Asset with the workflow file (see the following example).</span></span>
* <span data-ttu-id="f7c48-168">Creare un asset multimediale contenente due file: MyInputVideo.mp4 come file primario e MyLogo.png.</span><span class="sxs-lookup"><span data-stu-id="f7c48-168">Create a Media Asset, which contains two files: MyInputVideo.mp4 as the primary file and MyLogo.png.</span></span>
* <span data-ttu-id="f7c48-169">Inviare un'attività al processore di contenuti multimediali del flusso di lavoro Premium del codificatore multimediale con gli asset di input precedenti e specificare la stringa di configurazione seguente.</span><span class="sxs-lookup"><span data-stu-id="f7c48-169">Send a task to the Media Encoder Premium Workflow media processor with the above input assets and specify the following configuration string.</span></span>

<span data-ttu-id="f7c48-170">Configurazione:</span><span class="sxs-lookup"><span data-stu-id="f7c48-170">Configuration:</span></span>

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

<span data-ttu-id="f7c48-171">Nell'esempio precedente, il nome del file video viene invitato al componente Media File Input e alla proprietà primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="f7c48-171">In the example above, the name of the video file is sent to the Media File Input component and the primarySourceFile property.</span></span> <span data-ttu-id="f7c48-172">Il nome del file di logo viene inviato a un altro componente Media File Input, connesso al componente di sovrimpressione grafica.</span><span class="sxs-lookup"><span data-stu-id="f7c48-172">The name of the logo file is sent to another Media File Input that is connected to the graphic overlay component.</span></span>

> [!NOTE]
> <span data-ttu-id="f7c48-173">Il nome del file video viene inviato alla proprietà primarySourceFile</span><span class="sxs-lookup"><span data-stu-id="f7c48-173">The video file name is sent to the primarySourceFile property.</span></span> <span data-ttu-id="f7c48-174">per usare questa proprietà nel flusso di lavoro, ad esempio per compilare il nome file di output con espressioni.</span><span class="sxs-lookup"><span data-stu-id="f7c48-174">The reason for this is to use this property in the workflow for building the correct output file name using Expressions, for example.</span></span>

### <a name="step-by-step-workflow-creation"></a><span data-ttu-id="f7c48-175">Procedura dettagliata di creazione del flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="f7c48-175">Step-by-step workflow creation</span></span>
<span data-ttu-id="f7c48-176">Di seguito sono descritti i passaggi per creare un flusso di lavoro che ha due file come input: un video e un'immagine.</span><span class="sxs-lookup"><span data-stu-id="f7c48-176">Here are the steps to create a workflow that takes two files as input: a video and an image.</span></span> <span data-ttu-id="f7c48-177">L'immagine verrà sovrapposta sul video.</span><span class="sxs-lookup"><span data-stu-id="f7c48-177">It will overlay the image on top of the video.</span></span>

<span data-ttu-id="f7c48-178">Aprire **Progettazione flussi di lavoro** e selezionare **File** > **New Workspace (Nuova area di lavoro)** > **Transcode Blueprint**.</span><span class="sxs-lookup"><span data-stu-id="f7c48-178">Open **Workflow Designer** and select **File** > **New Workspace** > **Transcode Blueprint**.</span></span>

<span data-ttu-id="f7c48-179">Il nuovo flusso di lavoro visualizzerà 3 elementi:</span><span class="sxs-lookup"><span data-stu-id="f7c48-179">The new workflow shows three elements:</span></span>

* <span data-ttu-id="f7c48-180">Primary Source File</span><span class="sxs-lookup"><span data-stu-id="f7c48-180">Primary Source File</span></span>
* <span data-ttu-id="f7c48-181">Clip List XML</span><span class="sxs-lookup"><span data-stu-id="f7c48-181">Clip List XML</span></span>
* <span data-ttu-id="f7c48-182">Output File/Asset</span><span class="sxs-lookup"><span data-stu-id="f7c48-182">Output File/Asset</span></span>  

![Nuovo flusso di lavoro della codifica](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

<span data-ttu-id="f7c48-184">*Nuovo flusso di lavoro della codifica*</span><span class="sxs-lookup"><span data-stu-id="f7c48-184">*New Encoding Workflow*</span></span>

<span data-ttu-id="f7c48-185">Per accettare il file multimediale di input, iniziare aggiungendo un componente Media File Input.</span><span class="sxs-lookup"><span data-stu-id="f7c48-185">In order to accept the input media file, start with adding a Media File Input component.</span></span> <span data-ttu-id="f7c48-186">Per aggiungere un componente al flusso di lavoro, cercarlo nella casella di ricerca del repository e trascinare la voce desiderata sul riquadro della finestra di progettazione.</span><span class="sxs-lookup"><span data-stu-id="f7c48-186">To add a component to the workflow, look for it in the Repository search box and drag the desired entry onto the designer pane.</span></span>

<span data-ttu-id="f7c48-187">Aggiungere quindi il file video da usare per la progettazione del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f7c48-187">Next, add the video file to be used for designing your workflow.</span></span> <span data-ttu-id="f7c48-188">A questo scopo, fare clic sul riquadro dello sfondo in Progettazione flussi di lavoro e cercare la proprietà Primary Source File (File di origine primario) nel riquadro delle proprietà a destra.</span><span class="sxs-lookup"><span data-stu-id="f7c48-188">To do so, click the background pane in Workflow Designer and look for the Primary Source File property on the right-hand property pane.</span></span> <span data-ttu-id="f7c48-189">Fare clic sull'icona della cartella e selezionare il file video appropriato.</span><span class="sxs-lookup"><span data-stu-id="f7c48-189">Click the folder icon and select the appropriate video file.</span></span>

![File di origine primario](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

<span data-ttu-id="f7c48-191">*File di origine primario*</span><span class="sxs-lookup"><span data-stu-id="f7c48-191">*Primary File Source*</span></span>

<span data-ttu-id="f7c48-192">Specificare quindi il file video nel componente Media File Input.</span><span class="sxs-lookup"><span data-stu-id="f7c48-192">Next, specify the video file in the Media File Input component.</span></span>   

![Origine Media File Input](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

<span data-ttu-id="f7c48-194">*Origine Media File Input*</span><span class="sxs-lookup"><span data-stu-id="f7c48-194">*Media File Input Source*</span></span>

<span data-ttu-id="f7c48-195">Al termine dell'operazione, il componente Media File Input esaminerà il file e popolerà i pin di output per riflettere il file esaminato.</span><span class="sxs-lookup"><span data-stu-id="f7c48-195">As soon as this is done, the Media File Input component will inspect the file and populate its output pins to reflect the file that it inspected.</span></span>

<span data-ttu-id="f7c48-196">Il passaggio successivo consiste nell'aggiungere un componente "Video Data Type Updater" (Strumento di aggiornamento tipo dati video) per specificare lo spazio colore Rec.709.</span><span class="sxs-lookup"><span data-stu-id="f7c48-196">The next step is to add a "Video Data Type Updater" to specify the color space to Rec.709.</span></span> <span data-ttu-id="f7c48-197">Aggiungere un set "Convertitore formato video" impostato per Layout dati/Tipo layout = Planare configurabile.</span><span class="sxs-lookup"><span data-stu-id="f7c48-197">Add a "Video Format Converter" that is set to Data Layout/Layout type = Configurable Planar.</span></span> <span data-ttu-id="f7c48-198">Il flusso video verrà così convertito in un formato che può essere usato come origine del componente di sovrapposizione.</span><span class="sxs-lookup"><span data-stu-id="f7c48-198">This will convert the video stream to a format that can be taken as a source of the overlay component.</span></span>

![Strumento di aggiornamento tipo dati video e Convertitore formato video](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

<span data-ttu-id="f7c48-200">*Strumento di aggiornamento tipo dati video e Convertitore formato video*</span><span class="sxs-lookup"><span data-stu-id="f7c48-200">*Video Data Type Updater and Format Converter*</span></span>

![Layout type = Configurable Planar (Tipo layout = Planare configurabile)](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

<span data-ttu-id="f7c48-202">*Il tipo di layout è Planare configurabile*</span><span class="sxs-lookup"><span data-stu-id="f7c48-202">*Layout type is Configurable Planar*</span></span>

<span data-ttu-id="f7c48-203">Aggiungere quindi un componente di sovrapposizione video e collegare il pin del video non compresso al pin del video non compresso del componente Media File Input.</span><span class="sxs-lookup"><span data-stu-id="f7c48-203">Next, add a Video Overlay component and connect the (uncompressed) video pin to the (uncompressed) video pin of the media file input.</span></span>

<span data-ttu-id="f7c48-204">Aggiungere un altro Media File Input per caricare il file del logo, fare clic sul componente e rinominarlo in "Media File Input Logo", selezionare un'immagine, ad esempio un file con estensione png, nella proprietà del file.</span><span class="sxs-lookup"><span data-stu-id="f7c48-204">Add another Media File Input (to load the logo file), click on this component and rename it to "Media File Input Logo", and select an image (a .png file for example) in the file property.</span></span> <span data-ttu-id="f7c48-205">Collegare il pin dell'immagine non compressa al pin dell'immagine non compressa della sovrimpressione.</span><span class="sxs-lookup"><span data-stu-id="f7c48-205">Connect the Uncompressed image pin to the Uncompressed image pin of the overlay.</span></span>

![Componente della sovrimpressione e origine del file di immagine](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

<span data-ttu-id="f7c48-207">*Componente della sovrimpressione e origine del file di immagine*</span><span class="sxs-lookup"><span data-stu-id="f7c48-207">*Overlay component and image file source*</span></span>

<span data-ttu-id="f7c48-208">Per modificare la posizione del logo sul video, ad esempio per posizionare il logo al 10% di distanza dall'angolo superiore sinistro del video, deselezionare la casella di controllo Input manuale.</span><span class="sxs-lookup"><span data-stu-id="f7c48-208">If you want to modify the position of the logo on the video (for example, you might want to position it at 10 percent off of the top left corner of the video), clear the "Manual Input" check box.</span></span> <span data-ttu-id="f7c48-209">È possibile deselezionare questa opzione perché si usa Media File Input per fornire il file del logo al componente della sovrimpressione.</span><span class="sxs-lookup"><span data-stu-id="f7c48-209">You can do this because you are using a Media File Input to provide the logo file to the overlay component.</span></span>

![Posizione della sovrimpressione](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

<span data-ttu-id="f7c48-211">*Posizione della sovrimpressione*</span><span class="sxs-lookup"><span data-stu-id="f7c48-211">*Overlay position*</span></span>

<span data-ttu-id="f7c48-212">Per codificare il flusso video in H.264, aggiungere i componenti AVC Video Encoder e AAC Encoder all'area di progettazione.</span><span class="sxs-lookup"><span data-stu-id="f7c48-212">To encode the video stream to H.264, add the AVC Video Encoder and AAC encoder components to the designer surface.</span></span> <span data-ttu-id="f7c48-213">Collegare i pin.</span><span class="sxs-lookup"><span data-stu-id="f7c48-213">Connect the pins.</span></span>
<span data-ttu-id="f7c48-214">Configurare il codificatore AAC e selezionare Conversione formato audio/Set di impostazioni: 2.0 - S, D.</span><span class="sxs-lookup"><span data-stu-id="f7c48-214">Set up the AAC encoder and select Audio Format Conversion/Preset : 2.0 (L, R).</span></span>

![Codificatori audio e video](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

<span data-ttu-id="f7c48-216">*Codificatori audio e video*</span><span class="sxs-lookup"><span data-stu-id="f7c48-216">*Audio and Video Encoders*</span></span>

<span data-ttu-id="f7c48-217">Aggiungere ora i componenti **ISO Mpeg-4 Multiplexer** e **File Output** e collegare i pin come illustrato.</span><span class="sxs-lookup"><span data-stu-id="f7c48-217">Now add the **ISO Mpeg-4 Multiplexer** and **File Output** components and connect the pins as shown.</span></span>

![Multiplexer MP4 e file di output](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

<span data-ttu-id="f7c48-219">*Multiplexer MP4 e file di output*</span><span class="sxs-lookup"><span data-stu-id="f7c48-219">*MP4 multiplexer and file output*</span></span>

<span data-ttu-id="f7c48-220">È necessario definire il nome del file di output.</span><span class="sxs-lookup"><span data-stu-id="f7c48-220">You need to set the name for the output file.</span></span> <span data-ttu-id="f7c48-221">Fare clic sul componente **File Output** e modificare l'espressione per il file:</span><span class="sxs-lookup"><span data-stu-id="f7c48-221">Click the **File Output** component and edit the expression for the file:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Nome file di output](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

<span data-ttu-id="f7c48-223">*Nome file di output*</span><span class="sxs-lookup"><span data-stu-id="f7c48-223">*File output name*</span></span>

<span data-ttu-id="f7c48-224">È possibile eseguire il flusso di lavoro in locale per verificare che venga eseguito correttamente.</span><span class="sxs-lookup"><span data-stu-id="f7c48-224">You can run the workflow locally to check that it is running correctly.</span></span>

<span data-ttu-id="f7c48-225">Al termine, è possibile eseguire il flusso di lavoro in Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f7c48-225">After it finishes, you can run it in Azure Media Services.</span></span>

<span data-ttu-id="f7c48-226">Preparare prima un asset in Servizi multimediali di Azure con due file: il file video e il logo.</span><span class="sxs-lookup"><span data-stu-id="f7c48-226">First, prepare an asset in Azure Media Services with two files in it: the video file and the logo.</span></span> <span data-ttu-id="f7c48-227">Usare a tal fine .NET o l'API REST.</span><span class="sxs-lookup"><span data-stu-id="f7c48-227">You can do this by using the .NET or REST API.</span></span> <span data-ttu-id="f7c48-228">È anche possibile eseguire l'operazione con il portale di Azure o nello [strumento di Esplorazione di Servizi multimediali di Azure](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span><span class="sxs-lookup"><span data-stu-id="f7c48-228">You can also do this by using the Azure portal or [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span></span>

<span data-ttu-id="f7c48-229">Questa esercitazione illustra come gestire gli asset con AMSE.</span><span class="sxs-lookup"><span data-stu-id="f7c48-229">This tutorial shows you how to manage assets with AMSE.</span></span> <span data-ttu-id="f7c48-230">Esistono due modi per aggiungere file a un asset:</span><span class="sxs-lookup"><span data-stu-id="f7c48-230">There are two ways to add files to an asset:</span></span>

* <span data-ttu-id="f7c48-231">Creare una cartella locale, copiare i due file al suo interno e trascinare la cartella nella scheda **Asset** .</span><span class="sxs-lookup"><span data-stu-id="f7c48-231">Create a local folder, copy the two files in it, and drag and drop the folder to the **Asset** tab.</span></span>
* <span data-ttu-id="f7c48-232">Caricare il file video come asset, quindi visualizzare le informazioni sull'asset, passare alla scheda File e caricare un altro file (logo).</span><span class="sxs-lookup"><span data-stu-id="f7c48-232">Upload the video file as an asset, display the asset information, go to the files tab, and upload an additional file (logo).</span></span>

> [!NOTE]
> <span data-ttu-id="f7c48-233">Impostare un file primario nell'asset, ovvero il file video principale.</span><span class="sxs-lookup"><span data-stu-id="f7c48-233">Make sure to set a primary file in the asset (the main video file).</span></span>

![File di asset nello strumento di esplorazione di Servizi multimediali di Azure](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

<span data-ttu-id="f7c48-235">*File di asset nello strumento di esplorazione di Servizi multimediali di Azure*</span><span class="sxs-lookup"><span data-stu-id="f7c48-235">*Asset files in AMSE*</span></span>

<span data-ttu-id="f7c48-236">Selezionare l'asset e scegliere di codificarlo con il codificatore Premium.</span><span class="sxs-lookup"><span data-stu-id="f7c48-236">Select the asset and choose to encode it with Premium Encoder.</span></span> <span data-ttu-id="f7c48-237">Caricare il flusso di lavoro e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="f7c48-237">Upload the workflow and select it.</span></span>

<span data-ttu-id="f7c48-238">Fare clic sul pulsante per passare i dati al processore, quindi aggiungere il codice XML seguente per impostare le proprietà di runtime:</span><span class="sxs-lookup"><span data-stu-id="f7c48-238">Click the button to pass data to the processor, and add the following XML to set the runtime properties:</span></span>

![Codificatore Premium nello strumento di esplorazione di Servizi multimediali di Azure](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

<span data-ttu-id="f7c48-240">*Codificatore Premium nello strumento di esplorazione di Servizi multimediali di Azure*</span><span class="sxs-lookup"><span data-stu-id="f7c48-240">*Premium Encoder in AMSE*</span></span>

<span data-ttu-id="f7c48-241">Incollare quindi i dati XML seguenti.</span><span class="sxs-lookup"><span data-stu-id="f7c48-241">Then, paste the following XML data.</span></span> <span data-ttu-id="f7c48-242">È necessario specificare il nome del file video per Media File Input e primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="f7c48-242">You need to specify the name of the video file for both the Media File Input and primarySourceFile.</span></span> <span data-ttu-id="f7c48-243">Specificare anche il nome del file del logo.</span><span class="sxs-lookup"><span data-stu-id="f7c48-243">Specify the name of the file name for the logo too.</span></span>

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

<span data-ttu-id="f7c48-245">*setRuntimeProperties*</span><span class="sxs-lookup"><span data-stu-id="f7c48-245">*setRuntimeProperties*</span></span>

<span data-ttu-id="f7c48-246">Se si usa .NET SDK per creare ed eseguire l'attività, questi dati XML devono essere passati come stringa di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f7c48-246">If you use the .NET SDK to create and run the task, this XML data has to be passed as the configuration string.</span></span>

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

<span data-ttu-id="f7c48-247">Al termine del processo, il file MP4 nell'asset di output visualizzerà la sovrimpressione.</span><span class="sxs-lookup"><span data-stu-id="f7c48-247">After the job is complete, the MP4 file in the output asset displays the overlay!</span></span>

![Sovrimpressione sul video](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

<span data-ttu-id="f7c48-249">*Sovrimpressione sul video*</span><span class="sxs-lookup"><span data-stu-id="f7c48-249">*Overlay on the video*</span></span>

<span data-ttu-id="f7c48-250">È possibile scaricare il flusso di lavoro di esempio da [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span><span class="sxs-lookup"><span data-stu-id="f7c48-250">You can download the sample workflow from [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span></span>

## <a name="example-2--multiple-audio-language-encoding"></a><span data-ttu-id="f7c48-251">Esempio 2: Codifica di più lingue per l'audio</span><span class="sxs-lookup"><span data-stu-id="f7c48-251">Example 2 : Multiple audio language encoding</span></span>

<span data-ttu-id="f7c48-252">Un esempio di flusso di lavoro per la codifica di più lingue per l'audio è disponibile in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span><span class="sxs-lookup"><span data-stu-id="f7c48-252">An example of multiple audio language encoding workfkow is available in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span></span>

<span data-ttu-id="f7c48-253">La cartella contiene un flusso di lavoro di esempio che può essere usato per codificare un file MXF in un asset con più file MP4 con più tracce audio.</span><span class="sxs-lookup"><span data-stu-id="f7c48-253">This folder contains a sample workflow which can be used to encode a MXF file to a multi MP4 files asset with multiple audio tracks.</span></span>

<span data-ttu-id="f7c48-254">Il flusso di lavoro presuppone che il file MXF contenga una traccia audio. Le tracce audio aggiuntive dovranno essere passate come file audio separati (WAV, MP4 e così via).</span><span class="sxs-lookup"><span data-stu-id="f7c48-254">This workflow assumes that the MXF file contains one audio track ; the additional audio tracks should be passed as seperate audio files (WAV or MP4...).</span></span>

<span data-ttu-id="f7c48-255">Per effettuare la codifica, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f7c48-255">To encode, please follow these steps:</span></span>

* <span data-ttu-id="f7c48-256">Creare un asset di Servizi multimediali con il file MXF e i file audio (da 0 a 18).</span><span class="sxs-lookup"><span data-stu-id="f7c48-256">Create a Media Services asset with the MXF file and the Audio files (0 to 18 audio files).</span></span>
* <span data-ttu-id="f7c48-257">Verificare che il file MXF sia impostato come file primario.</span><span class="sxs-lookup"><span data-stu-id="f7c48-257">Make sure that the MXF file is set as a primary file.</span></span>
* <span data-ttu-id="f7c48-258">Creare un processo e un'attività con il processore del codificatore del flusso di lavoro Premium.</span><span class="sxs-lookup"><span data-stu-id="f7c48-258">Create a job and a task using the Premium Workflow Encoder processor.</span></span> <span data-ttu-id="f7c48-259">Usare il flusso di lavoro fornito (MultiMP4-1080p-19audio-v1.workflow).</span><span class="sxs-lookup"><span data-stu-id="f7c48-259">Use the workflow provided (MultiMP4-1080p-19audio-v1.workflow).</span></span>
* <span data-ttu-id="f7c48-260">Passare i dati di setruntime.xml all'attività. Se si usa lo strumento di esplorazione di Servizi multimediali di Azure, usare il pulsante "pass xml data to the workflow" (passa dati xml a flusso di lavoro).</span><span class="sxs-lookup"><span data-stu-id="f7c48-260">Pass the setruntime.xml data to the task (if you use Azure Media Services Explorer, use the “pass xml data to the workflow” button).</span></span>
  * <span data-ttu-id="f7c48-261">Aggiornare i dati XML per specificare i nomi file e i tag di lingua corretti.</span><span class="sxs-lookup"><span data-stu-id="f7c48-261">Please update the XML data to specify the correct file names and languages tags.</span></span>
  * <span data-ttu-id="f7c48-262">Il flusso di lavoro include componenti audio con nome da Audio 1 ad Audio 18.</span><span class="sxs-lookup"><span data-stu-id="f7c48-262">The workflow has audio components named Audio 1 to Audio 18.</span></span>
  * <span data-ttu-id="f7c48-263">Per il tag di lingua è supportata la specifica RFC5646.</span><span class="sxs-lookup"><span data-stu-id="f7c48-263">RFC5646 is supported for the language tag.</span></span>

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

* <span data-ttu-id="f7c48-264">L'asset codificato conterrà tracce audio in più lingue e tali tracce saranno selezionabili in Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="f7c48-264">The encoded asset will contain multi language audio tracks and these tracks should be selectable in Azure Media Player.</span></span>

## <a name="see-also"></a><span data-ttu-id="f7c48-265">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7c48-265">See also</span></span>
* [<span data-ttu-id="f7c48-266">Introduzione alla codifica Premium in Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="f7c48-266">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="f7c48-267">Come usare la codifica Premium in Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="f7c48-267">How to use Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="f7c48-268">Codifica di contenuti su richiesta con Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="f7c48-268">Encoding on-demand content with Azure Media Services</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)
* [<span data-ttu-id="f7c48-269">Codec e formati del flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="f7c48-269">Media Encoder Premium Workflow formats and codecs</span></span>](media-services-premium-workflow-encoder-formats.md)
* [<span data-ttu-id="f7c48-270">File del flusso di lavoro di esempio</span><span class="sxs-lookup"><span data-stu-id="f7c48-270">Sample workflow files</span></span>](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [<span data-ttu-id="f7c48-271">Strumento di esplorazione di Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="f7c48-271">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="f7c48-272">Percorsi di apprendimento di Media Services</span><span class="sxs-lookup"><span data-stu-id="f7c48-272">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f7c48-273">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="f7c48-273">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

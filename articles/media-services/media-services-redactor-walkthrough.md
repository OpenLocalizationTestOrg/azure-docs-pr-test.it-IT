---
title: 'Procedura dettagliata: offuscare i volti con Analisi Servizi multimediali di Azure | Documentazione Microsoft'
description: Questo argomento fornisce istruzioni dettagliate su come eseguire un flusso di lavoro di offuscamento completo usando Azure Media Services Explorer (AMSE) e Azure Media Redactor Visualizer (strumento open source).
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: c0c622237f8cdca65fb6933f14cc21e9eb9ac036
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="f66b0-103">Procedura dettagliata: offuscare i volti con Analisi Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="f66b0-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="f66b0-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f66b0-104">Overview</span></span>

<span data-ttu-id="f66b0-105">**Azure Media Redactor** è un processore di contenuti multimediali di [Analisi Servizi multimediali di Azure](media-services-analytics-overview.md) che offre funzionalità scalabili di offuscamento dei volti nel cloud.</span><span class="sxs-lookup"><span data-stu-id="f66b0-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="f66b0-106">L'offuscamento dei volti consente di modificare un video per sfocare i volti di persone selezionate.</span><span class="sxs-lookup"><span data-stu-id="f66b0-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="f66b0-107">Può essere opportuno usare tale servizio in scenari di pubblica sicurezza e notizie giornalistiche.</span><span class="sxs-lookup"><span data-stu-id="f66b0-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="f66b0-108">Offuscare manualmente alcuni minuti di filmato contenenti più volti può richiedere ore, ma con questo servizio il processo di offuscamento dei volti richiederà pochi semplici passaggi.</span><span class="sxs-lookup"><span data-stu-id="f66b0-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="f66b0-109">Per altre informazioni, vedere [questo](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span><span class="sxs-lookup"><span data-stu-id="f66b0-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="f66b0-110">Per informazioni dettagliate su **Azure Media Redactor**, vedere la [panoramica sull'offuscamento dei volti](media-services-face-redaction.md).</span><span class="sxs-lookup"><span data-stu-id="f66b0-110">For details about  **Azure Media Redactor**, see the [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="f66b0-111">Questo argomento fornisce istruzioni dettagliate su come eseguire un flusso di lavoro di offuscamento completo usando Azure Media Services Explorer (AMSE) e Azure Media Redactor Visualizer (strumento open source).</span><span class="sxs-lookup"><span data-stu-id="f66b0-111">This topic shows step by step instructions on how to run a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="f66b0-112">Il processore di contenuti multimediali **Azure Media Redactor** è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="f66b0-112">The **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="f66b0-113">È disponibile in tutte le aree di Azure pubbliche, nonché nei data center cinesi e del governo degli USA.</span><span class="sxs-lookup"><span data-stu-id="f66b0-113">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="f66b0-114">Al momento questa versione di anteprima è disponibile gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="f66b0-114">This preview is currently free of charge.</span></span> <span data-ttu-id="f66b0-115">Nella versione corrente la durata dei video elaborati è limitata a 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="f66b0-115">In the current release, there is a 10 minute limit on processed video length.</span></span>

<span data-ttu-id="f66b0-116">Per altre informazioni, vedere [questo](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span><span class="sxs-lookup"><span data-stu-id="f66b0-116">For more information, see [this](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="f66b0-117">Flusso di lavoro di Azure Media Services Explorer</span><span class="sxs-lookup"><span data-stu-id="f66b0-117">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="f66b0-118">Il modo più semplice iniziare a usare Azure Media Redactor è usare lo strumento AMSE open source su GitHub.</span><span class="sxs-lookup"><span data-stu-id="f66b0-118">The easiest way to get started with Redactor is to use the open source AMSE tool on github.</span></span> <span data-ttu-id="f66b0-119">Se non occorre accedere al file JSON di annotazioni o alle immagini .JPG dei volti, è possibile eseguire un flusso di lavoro semplificato in modalità **combinata**.</span><span class="sxs-lookup"><span data-stu-id="f66b0-119">You can run a simplified workflow via **combined** mode if you don’t need access to the annotation json or the face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="f66b0-120">Download e installazione</span><span class="sxs-lookup"><span data-stu-id="f66b0-120">Download and setup</span></span>

1. <span data-ttu-id="f66b0-121">Scaricare lo strumento AMSE da [qui](https://github.com/Azure/Azure-Media-Services-Explorer).</span><span class="sxs-lookup"><span data-stu-id="f66b0-121">Download the AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="f66b0-122">Accedere al proprio account di Servizi multimediali usando la chiave del servizio.</span><span class="sxs-lookup"><span data-stu-id="f66b0-122">Log in to your Media Services account using your service key.</span></span>

    <span data-ttu-id="f66b0-123">Per ottenere il nome dell'account e la chiave, accedere al [portale di Azure](https://portal.azure.com/) e selezionare l'account AMS.</span><span class="sxs-lookup"><span data-stu-id="f66b0-123">To obtain the account name and key information, go to the [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="f66b0-124">Dopodiché, selezionare Impostazioni > Chiavi.</span><span class="sxs-lookup"><span data-stu-id="f66b0-124">Then, select Settings > Keys.</span></span> <span data-ttu-id="f66b0-125">Nella finestra Gestisci chiavi sono visualizzati il nome dell'account e le chiavi primaria e secondaria.</span><span class="sxs-lookup"><span data-stu-id="f66b0-125">The Manage keys windows shows the account name and the primary and secondary keys is displayed.</span></span> <span data-ttu-id="f66b0-126">Copiare i valori del nome dell'account e della chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="f66b0-126">Copy values of the account name and the primary key.</span></span>

![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="f66b0-128">Primo passaggio: modalità analisi</span><span class="sxs-lookup"><span data-stu-id="f66b0-128">First pass – analyze mode</span></span>

1. <span data-ttu-id="f66b0-129">Caricare il file multimediale facendo clic su Asset -> Carica oppure trascinandolo.</span><span class="sxs-lookup"><span data-stu-id="f66b0-129">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="f66b0-130">Fare clic sul file multimediale con il pulsante destro del mouse ed elaborarlo usando Analisi Servizi multimediali -> Azure Media Redactor -> Modalità analisi.</span><span class="sxs-lookup"><span data-stu-id="f66b0-130">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="f66b0-133">L'output includerà un file JSON di annotazioni contenente i dati relativi alla posizione del volto, oltre all'immagine di ogni volto rilevato in formato .JPG.</span><span class="sxs-lookup"><span data-stu-id="f66b0-133">The output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a><span data-ttu-id="f66b0-135">Secondo passaggio: modalità offuscamento</span><span class="sxs-lookup"><span data-stu-id="f66b0-135">Second pass – redact mode</span></span>

1. <span data-ttu-id="f66b0-136">Caricare l'asset video originale nell'output del primo passaggio e impostarlo come asset principale.</span><span class="sxs-lookup"><span data-stu-id="f66b0-136">Upload your original video asset to the output from the first pass and set as a primary asset.</span></span> 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="f66b0-138">(Facoltativo) Caricare un file "Dance_idlist.txt" che include un elenco delimitato da nuova riga degli ID che si desidera offuscare.</span><span class="sxs-lookup"><span data-stu-id="f66b0-138">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of the IDs you wish to redact.</span></span> 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="f66b0-140">(Facoltativo) Modificare il file annotations.json, ad esempio aumentando le dimensioni dei rettangoli di selezione.</span><span class="sxs-lookup"><span data-stu-id="f66b0-140">(Optional) Make any edits to the annotations.json file such as increasing the bounding box boundaries.</span></span> 
4. <span data-ttu-id="f66b0-141">Fare clic con il pulsante destro del mouse sull'asset di output del primo passaggio, scegliere Redactor ed eseguirlo in modalità **Redact** (Offusca).</span><span class="sxs-lookup"><span data-stu-id="f66b0-141">Right click the output asset from the first pass, select the Redactor, and run with the **Redact** mode.</span></span> 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="f66b0-143">Scaricare o condividere l'asset di output con l'offuscamento.</span><span class="sxs-lookup"><span data-stu-id="f66b0-143">Download or share the final redacted output asset.</span></span> 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="f66b0-145">Strumento open source Azure Media Redactor Visualizer</span><span class="sxs-lookup"><span data-stu-id="f66b0-145">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="f66b0-146">Il [visualizzatore](https://github.com/Microsoft/azure-media-redactor-visualizer) open source ha lo scopo di introdurre gli sviluppatori al formato delle annotazioni con l'analisi e l'uso dell'output.</span><span class="sxs-lookup"><span data-stu-id="f66b0-146">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed to help developers just starting with the annotations format with parsing and using the output.</span></span>

<span data-ttu-id="f66b0-147">Dopo aver clonato il repository, per eseguire il progetto sarà necessario scaricare FFmpeg dal [sito ufficiale](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="f66b0-147">After you clone the repo, in order to run the project, you will need to download FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="f66b0-148">Se lo sviluppatore tenta di analizzare i dati delle annotazioni JSON, consultare i codici di esempio in Models.MetaData.</span><span class="sxs-lookup"><span data-stu-id="f66b0-148">If you are a developer trying to parse the JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-the-tool"></a><span data-ttu-id="f66b0-149">Impostare lo strumento</span><span class="sxs-lookup"><span data-stu-id="f66b0-149">Set up the tool</span></span>

1.  <span data-ttu-id="f66b0-150">Scaricare e compilare l'intera soluzione.</span><span class="sxs-lookup"><span data-stu-id="f66b0-150">Download and build the entire solution.</span></span> 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="f66b0-152">Scaricare FFmpeg da [qui](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="f66b0-152">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="f66b0-153">Questo progetto è stato originariamente sviluppato con la versione be1d324 (04-10-2016) con il collegamento statico.</span><span class="sxs-lookup"><span data-stu-id="f66b0-153">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="f66b0-154">Copiare ffmpeg.exe e ffprobe.exe nella stessa cartella di output di AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="f66b0-154">Copy ffmpeg.exe and ffprobe.exe to the same output folder as AzureMediaRedactor.exe.</span></span> 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="f66b0-156">Eseguire AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="f66b0-156">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-the-tool"></a><span data-ttu-id="f66b0-157">Usare lo strumento</span><span class="sxs-lookup"><span data-stu-id="f66b0-157">Use the tool</span></span>

1. <span data-ttu-id="f66b0-158">Elaborare il video nell'account di Servizi multimediali di Azure con il Management Pack Redactor in modalità di analisi.</span><span class="sxs-lookup"><span data-stu-id="f66b0-158">Process your video in your Azure Media Services account with the Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="f66b0-159">Scaricare il file video originale e l'output del processo di offuscamento e analisi.</span><span class="sxs-lookup"><span data-stu-id="f66b0-159">Download both the original video file and the output of the Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="f66b0-160">Eseguire l'applicazione del visualizzatore e scegliere i file nella finestra qui sopra.</span><span class="sxs-lookup"><span data-stu-id="f66b0-160">Run the visualizer application and choose the files above.</span></span> 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="f66b0-162">Visualizzare l'anteprima del file.</span><span class="sxs-lookup"><span data-stu-id="f66b0-162">Preview your file.</span></span> <span data-ttu-id="f66b0-163">Selezionare i volti da offuscare usando la barra laterale a destra.</span><span class="sxs-lookup"><span data-stu-id="f66b0-163">Select which faces you'd like to blur via the sidebar on the right.</span></span> 
    
    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="f66b0-165">Il campo di testo in basso verrà aggiornato con gli ID dei volti.</span><span class="sxs-lookup"><span data-stu-id="f66b0-165">The bottom text field will update with the face IDs.</span></span> <span data-ttu-id="f66b0-166">Creare un file denominato "idlist.txt" contenente questi ID come elenco delimitato da nuova riga.</span><span class="sxs-lookup"><span data-stu-id="f66b0-166">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="f66b0-167">Il file idlist.txt deve essere salvato in formato ANSI.</span><span class="sxs-lookup"><span data-stu-id="f66b0-167">The idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="f66b0-168">È possibile usare il Blocco note per il salvataggio in formato ANSI.</span><span class="sxs-lookup"><span data-stu-id="f66b0-168">You can use notepad to save in ANSI.</span></span>
    
6.  <span data-ttu-id="f66b0-169">Caricare questo file nell'output di asset del Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="f66b0-169">Upload this file to the output asset from step 1.</span></span> <span data-ttu-id="f66b0-170">In questo asset caricare anche il video originale e impostarlo come asset principale.</span><span class="sxs-lookup"><span data-stu-id="f66b0-170">Upload the original video to this asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="f66b0-171">Eseguire il processo di offuscamento nell'asset con la modalità "Redact" (Offusca) per ottenere il video finale offuscato.</span><span class="sxs-lookup"><span data-stu-id="f66b0-171">Run Redaction job on this asset with "Redact" mode to get the final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f66b0-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f66b0-172">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f66b0-173">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="f66b0-173">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="f66b0-174">Collegamenti correlati</span><span class="sxs-lookup"><span data-stu-id="f66b0-174">Related links</span></span>
[<span data-ttu-id="f66b0-175">Panoramica di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="f66b0-175">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="f66b0-176">Demo di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="f66b0-176">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[<span data-ttu-id="f66b0-177">Presto sarà disponibile l'offuscamento dei volti per Analisi Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="f66b0-177">Announcing Face Redaction for Azure Media Analytics</span></span>](https://azure.microsoft.com/blog/azure-media-redactor/)

---
title: i caratteri tipografici aaaRedact con questa procedura dettagliata Azure Media Analitica | Documenti Microsoft
description: In questo argomento viene istruzioni dettagliate su come toorun un flusso di lavoro completo redazione usando Azure Media Services Explorer (AMSE) e Azure Media Redactor visualizzatore (strumento open source).
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
ms.openlocfilehash: ab28f4052b73fdb74fcd5766235eab35402a0c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="1ae51-103">Procedura dettagliata: offuscare i volti con Analisi Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="1ae51-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="1ae51-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="1ae51-104">Overview</span></span>

<span data-ttu-id="1ae51-105">**Azure Media Redactor** è un [Azure Media Analitica](media-services-analytics-overview.md) processore di contenuti multimediali (MP) che offre redazione faccia scalabile nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="1ae51-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="1ae51-106">Adattamento faccia consente si toomodify video in facce tooblur ordine dei singoli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="1ae51-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="1ae51-107">È opportuno toouse hello faccia redazione servizio pubblica sicurezza e i supporti di notizie negli scenari in.</span><span class="sxs-lookup"><span data-stu-id="1ae51-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="1ae51-108">Pochi minuti di riprese che contiene più caratteri tipografici possono richiedere ore tooredact manualmente, ma con questa faccia hello servizio processo di adattamento richiederà solo alcuni semplici passaggi.</span><span class="sxs-lookup"><span data-stu-id="1ae51-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="1ae51-109">Per altre informazioni, vedere [questo](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span><span class="sxs-lookup"><span data-stu-id="1ae51-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="1ae51-110">Per informazioni dettagliate su **Azure Media Redactor**, vedere hello [Panoramica redazione faccia](media-services-face-redaction.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="1ae51-110">For details about  **Azure Media Redactor**, see hello [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="1ae51-111">In questo argomento viene istruzioni dettagliate su come toorun un flusso di lavoro completo redazione usando Azure Media Services Explorer (AMSE) e Azure Media Redactor visualizzatore (strumento open source).</span><span class="sxs-lookup"><span data-stu-id="1ae51-111">This topic shows step by step instructions on how toorun a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="1ae51-112">Hello **Azure Media Redactor** Management Pack è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="1ae51-112">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="1ae51-113">È disponibile in tutte le aree di Azure pubbliche, nonché nei data center cinesi e del governo degli USA.</span><span class="sxs-lookup"><span data-stu-id="1ae51-113">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="1ae51-114">Al momento questa versione di anteprima è disponibile gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="1ae51-114">This preview is currently free of charge.</span></span> <span data-ttu-id="1ae51-115">Nella versione corrente di hello, è previsto un limite di 10 minuti lunghezza video elaborato.</span><span class="sxs-lookup"><span data-stu-id="1ae51-115">In hello current release, there is a 10 minute limit on processed video length.</span></span>

<span data-ttu-id="1ae51-116">Per altre informazioni, vedere [questo](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span><span class="sxs-lookup"><span data-stu-id="1ae51-116">For more information, see [this](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="1ae51-117">Flusso di lavoro di Azure Media Services Explorer</span><span class="sxs-lookup"><span data-stu-id="1ae51-117">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="1ae51-118">Hello tooget modo più semplice introduttiva Redactor è toouse strumento AMSE open source di hello su github.</span><span class="sxs-lookup"><span data-stu-id="1ae51-118">hello easiest way tooget started with Redactor is toouse hello open source AMSE tool on github.</span></span> <span data-ttu-id="1ae51-119">È possibile eseguire un flusso di lavoro semplificata tramite **combinati** modalità se non è necessario accedere toohello annotazione json o hello faccia immagini jpg.</span><span class="sxs-lookup"><span data-stu-id="1ae51-119">You can run a simplified workflow via **combined** mode if you don’t need access toohello annotation json or hello face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="1ae51-120">Download e installazione</span><span class="sxs-lookup"><span data-stu-id="1ae51-120">Download and setup</span></span>

1. <span data-ttu-id="1ae51-121">Scaricare lo strumento AMSE hello da [qui](https://github.com/Azure/Azure-Media-Services-Explorer).</span><span class="sxs-lookup"><span data-stu-id="1ae51-121">Download hello AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="1ae51-122">Accedi tooyour account servizi multimediali usando la chiave del servizio.</span><span class="sxs-lookup"><span data-stu-id="1ae51-122">Log in tooyour Media Services account using your service key.</span></span>

    <span data-ttu-id="1ae51-123">tooobtain hello Nome account e informazioni sulla chiave, passa toohello [portale di Azure](https://portal.azure.com/) e selezionare l'account di sistema AMS.</span><span class="sxs-lookup"><span data-stu-id="1ae51-123">tooobtain hello account name and key information, go toohello [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="1ae51-124">Dopodiché, selezionare Impostazioni > Chiavi.</span><span class="sxs-lookup"><span data-stu-id="1ae51-124">Then, select Settings > Keys.</span></span> <span data-ttu-id="1ae51-125">finestre di Hello Gestisci chiavi Mostra nome hello e chiavi primarie e secondarie hello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="1ae51-125">hello Manage keys windows shows hello account name and hello primary and secondary keys is displayed.</span></span> <span data-ttu-id="1ae51-126">Copiare i valori del nome dell'account hello e la chiave primaria hello.</span><span class="sxs-lookup"><span data-stu-id="1ae51-126">Copy values of hello account name and hello primary key.</span></span>

![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="1ae51-128">Primo passaggio: modalità analisi</span><span class="sxs-lookup"><span data-stu-id="1ae51-128">First pass – analyze mode</span></span>

1. <span data-ttu-id="1ae51-129">Caricare il file multimediale facendo clic su Asset -> Carica oppure trascinandolo.</span><span class="sxs-lookup"><span data-stu-id="1ae51-129">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="1ae51-130">Fare clic sul file multimediale con il pulsante destro del mouse ed elaborarlo usando Analisi Servizi multimediali -> Azure Media Redactor -> Modalità analisi.</span><span class="sxs-lookup"><span data-stu-id="1ae51-130">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="1ae51-133">output di Hello includerà un file json di annotazioni con dati di posizione di carattere, nonché in formato jpg di ogni tipo di carattere rilevato.</span><span class="sxs-lookup"><span data-stu-id="1ae51-133">hello output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a><span data-ttu-id="1ae51-135">Secondo passaggio: modalità offuscamento</span><span class="sxs-lookup"><span data-stu-id="1ae51-135">Second pass – redact mode</span></span>

1. <span data-ttu-id="1ae51-136">Caricare il toohello asset video originale dal primo passaggio di hello e impostare come primario asset.</span><span class="sxs-lookup"><span data-stu-id="1ae51-136">Upload your original video asset toohello output from hello first pass and set as a primary asset.</span></span> 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="1ae51-138">(Facoltativo) Caricare un file 'Dance_idlist.txt', che include un elenco di nuova riga delimitato di ID desiderato tooredact hello.</span><span class="sxs-lookup"><span data-stu-id="1ae51-138">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of hello IDs you wish tooredact.</span></span> 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="1ae51-140">(Facoltativo) Verificare qualsiasi file annotations.json toohello di modifiche, ad esempio aumentando hello delimitazione i limiti di casella.</span><span class="sxs-lookup"><span data-stu-id="1ae51-140">(Optional) Make any edits toohello annotations.json file such as increasing hello bounding box boundaries.</span></span> 
4. <span data-ttu-id="1ae51-141">Fare clic con il pulsante destro asset di output di hello dal primo passaggio di hello, selezionare hello Redactor ed eseguire con hello **Redact** modalità.</span><span class="sxs-lookup"><span data-stu-id="1ae51-141">Right click hello output asset from hello first pass, select hello Redactor, and run with hello **Redact** mode.</span></span> 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="1ae51-143">Scaricare o condividere asset di output finale di adattamento hello.</span><span class="sxs-lookup"><span data-stu-id="1ae51-143">Download or share hello final redacted output asset.</span></span> 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="1ae51-145">Strumento open source Azure Media Redactor Visualizer</span><span class="sxs-lookup"><span data-stu-id="1ae51-145">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="1ae51-146">Un open-source [strumento Visualizzatore](https://github.com/Microsoft/azure-media-redactor-visualizer) è sviluppatori toohelp progettato con formato annotazioni hello con l'analisi e l'utilizzo di output di hello.</span><span class="sxs-lookup"><span data-stu-id="1ae51-146">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed toohelp developers just starting with hello annotations format with parsing and using hello output.</span></span>

<span data-ttu-id="1ae51-147">Dopo che clonare il repository di hello, nel progetto di hello toorun ordine, sarà necessario toodownload FFMPEG da loro [sito ufficiale](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="1ae51-147">After you clone hello repo, in order toorun hello project, you will need toodownload FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="1ae51-148">Se si è uno sviluppatore sta tentando di hello tooparse dati annotazione JSON, cercare all'interno di Models.MetaData esempi di codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="1ae51-148">If you are a developer trying tooparse hello JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-hello-tool"></a><span data-ttu-id="1ae51-149">Impostare lo strumento hello</span><span class="sxs-lookup"><span data-stu-id="1ae51-149">Set up hello tool</span></span>

1.  <span data-ttu-id="1ae51-150">Scaricare e compilare hello intera soluzione.</span><span class="sxs-lookup"><span data-stu-id="1ae51-150">Download and build hello entire solution.</span></span> 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="1ae51-152">Scaricare FFmpeg da [qui](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="1ae51-152">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="1ae51-153">Questo progetto è stato originariamente sviluppato con la versione be1d324 (04-10-2016) con il collegamento statico.</span><span class="sxs-lookup"><span data-stu-id="1ae51-153">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="1ae51-154">Copiare toohello ffmpeg.exe e ffprobe.exe stessa cartella di output come AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="1ae51-154">Copy ffmpeg.exe and ffprobe.exe toohello same output folder as AzureMediaRedactor.exe.</span></span> 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="1ae51-156">Eseguire AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="1ae51-156">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-hello-tool"></a><span data-ttu-id="1ae51-157">Utilizzare lo strumento di hello</span><span class="sxs-lookup"><span data-stu-id="1ae51-157">Use hello tool</span></span>

1. <span data-ttu-id="1ae51-158">Elaborare video nell'account di servizi multimediali di Azure con hello Redactor MP in modalità di analisi.</span><span class="sxs-lookup"><span data-stu-id="1ae51-158">Process your video in your Azure Media Services account with hello Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="1ae51-159">Scaricare file video originale hello e output di hello di hello redazione - processo di analisi.</span><span class="sxs-lookup"><span data-stu-id="1ae51-159">Download both hello original video file and hello output of hello Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="1ae51-160">Eseguire un'applicazione hello visualizzatore e selezionare file hello sopra descritti.</span><span class="sxs-lookup"><span data-stu-id="1ae51-160">Run hello visualizer application and choose hello files above.</span></span> 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="1ae51-162">Visualizzare l'anteprima del file.</span><span class="sxs-lookup"><span data-stu-id="1ae51-162">Preview your file.</span></span> <span data-ttu-id="1ae51-163">Selezionare rivolto si sarebbe tooblur tramite la barra laterale hello in hello destra.</span><span class="sxs-lookup"><span data-stu-id="1ae51-163">Select which faces you'd like tooblur via hello sidebar on hello right.</span></span> 
    
    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="1ae51-165">campo di testo Hello nella parte inferiore verrà aggiornato con faccia hello ID.</span><span class="sxs-lookup"><span data-stu-id="1ae51-165">hello bottom text field will update with hello face IDs.</span></span> <span data-ttu-id="1ae51-166">Creare un file denominato "idlist.txt" contenente questi ID come elenco delimitato da nuova riga.</span><span class="sxs-lookup"><span data-stu-id="1ae51-166">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="1ae51-167">Hello idlist.txt deve essere salvato in formato ANSI.</span><span class="sxs-lookup"><span data-stu-id="1ae51-167">hello idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="1ae51-168">È possibile utilizzare il blocco note toosave in ANSI.</span><span class="sxs-lookup"><span data-stu-id="1ae51-168">You can use notepad toosave in ANSI.</span></span>
    
6.  <span data-ttu-id="1ae51-169">Caricare l'asset di output toohello file dal passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="1ae51-169">Upload this file toohello output asset from step 1.</span></span> <span data-ttu-id="1ae51-170">Caricare hello originale toothis video asset nonché e impostare come primario asset.</span><span class="sxs-lookup"><span data-stu-id="1ae51-170">Upload hello original video toothis asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="1ae51-171">Eseguire il processo di adattamento in questo asset con "Redact" modalità tooget hello redatta video finale.</span><span class="sxs-lookup"><span data-stu-id="1ae51-171">Run Redaction job on this asset with "Redact" mode tooget hello final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1ae51-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1ae51-172">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1ae51-173">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="1ae51-173">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="1ae51-174">Collegamenti correlati</span><span class="sxs-lookup"><span data-stu-id="1ae51-174">Related links</span></span>
[<span data-ttu-id="1ae51-175">Panoramica di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="1ae51-175">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="1ae51-176">Demo di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="1ae51-176">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[<span data-ttu-id="1ae51-177">Presto sarà disponibile l'offuscamento dei volti per Analisi Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="1ae51-177">Announcing Face Redaction for Azure Media Analytics</span></span>](https://azure.microsoft.com/blog/azure-media-redactor/)

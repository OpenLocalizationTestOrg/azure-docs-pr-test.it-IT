---
title: gli strumenti Analitica di flusso di Azure per Visual Studio aaaUse | Documenti Microsoft
description: Guida introduttiva di esercitazione per hello Azure flusso Analitica Tools per Visual Studio
keywords: Visual Studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="35704-104">Usare gli strumenti di Analisi di flusso di Azure per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="35704-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="35704-105">Introduzione</span><span class="sxs-lookup"><span data-stu-id="35704-105">Introduction</span></span>
<span data-ttu-id="35704-106">In questa esercitazione, è illustrato come toouse strumenti Analitica flusso di Azure per Visual Studio toocreate, creare, testare localmente, gestire e debug di processi di flusso Analitica.</span><span class="sxs-lookup"><span data-stu-id="35704-106">In this tutorial, you learn how toouse Azure Stream Analytics Tools for Visual Studio toocreate, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="35704-107">Dopo aver completato questa esercitazione, si sarà in grado di:</span><span class="sxs-lookup"><span data-stu-id="35704-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="35704-108">Usare gli strumenti di Analisi di flusso di Azure per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="35704-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="35704-109">Configurare e distribuire un processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="35704-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="35704-110">Testare il processo in locale con dati di esempio locali.</span><span class="sxs-lookup"><span data-stu-id="35704-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="35704-111">Utilizzare Monitoraggio tootroubleshoot problemi.</span><span class="sxs-lookup"><span data-stu-id="35704-111">Use monitoring tootroubleshoot issues.</span></span>
* <span data-ttu-id="35704-112">Esportare tooprojects processi esistenti.</span><span class="sxs-lookup"><span data-stu-id="35704-112">Export existing jobs tooprojects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35704-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="35704-113">Prerequisites</span></span>
<span data-ttu-id="35704-114">toocomplete questa esercitazione, è necessario hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="35704-114">toocomplete this tutorial, you need hello following prerequisites:</span></span>
* <span data-ttu-id="35704-115">Completare i passaggi di hello che precedono "Creazione di un processo di flusso Analitica" in hello [compilare una soluzione IoT utilizzando esercitazione Analitica flusso](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="35704-115">Finish hello steps that precede "Create a Stream Analytics job" in hello [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="35704-116">Usare Visual Studio 2015, Visual Studio 2013 Update 4 oppure Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="35704-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="35704-117">Sono supportate le edizioni Enterprise (Ultimate/Premium), Professional e Community.</span><span class="sxs-lookup"><span data-stu-id="35704-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="35704-118">L'edizione Express non è supportata.</span><span class="sxs-lookup"><span data-stu-id="35704-118">Express edition is not supported.</span></span> <span data-ttu-id="35704-119">Visual Studio 2017 non è supportato.</span><span class="sxs-lookup"><span data-stu-id="35704-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="35704-120">Hello utilizzare Azure SDK per .NET versione 2.7.1 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="35704-120">Use hello Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="35704-121">Installarlo utilizzando hello [installazione guidata piattaforma Web](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="35704-121">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="35704-122">Installare hello [flusso Analitica Tools per Visual Studio](http://aka.ms/asatoolsvs).</span><span class="sxs-lookup"><span data-stu-id="35704-122">Install hello [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="35704-123">Creare un progetto di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="35704-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="35704-124">In Visual Studio, fare clic su hello **File** dal menu **nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="35704-124">In Visual Studio, click hello **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="35704-125">Nell'elenco di modelli hello hello sinistra, selezionare **Analitica flusso** e quindi fare clic su **l'applicazione Azure flusso Analitica**.</span><span class="sxs-lookup"><span data-stu-id="35704-125">In hello templates list on hello left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="35704-126">Immettere hello **nome**, **percorso**, e **Nome soluzione** come avviene per altri progetti.</span><span class="sxs-lookup"><span data-stu-id="35704-126">Enter hello project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![Finestra Nuovo progetto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="35704-128">Verrà generato un progetto **Toll** in **Esplora soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="35704-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![Progetto Toll generato in Esplora soluzioni](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a><span data-ttu-id="35704-130">Scegliere la sottoscrizione corretta hello</span><span class="sxs-lookup"><span data-stu-id="35704-130">Choose hello correct subscription</span></span>
1. <span data-ttu-id="35704-131">In Visual Studio, fare clic su hello **vista** menu e aprire **Esplora Server**.</span><span class="sxs-lookup"><span data-stu-id="35704-131">In Visual Studio, click hello **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="35704-132">Accedere con l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="35704-132">Sign in with your Azure Account.</span></span> 

## <a name="define-hello-input-sources"></a><span data-ttu-id="35704-133">Definire le origini di input hello</span><span class="sxs-lookup"><span data-stu-id="35704-133">Define hello input sources</span></span>
1.  <span data-ttu-id="35704-134">In **Esplora**, espandere hello **input** nodo e rinominare **Input.json** troppo**EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="35704-134">In **Solution Explorer**, expand hello **Inputs** node and rename **Input.json** too**EntryStream.json**.</span></span> <span data-ttu-id="35704-135">Fare doppio clic su **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="35704-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="35704-136">Hello **Alias di Input** è ora **EntryStream**.</span><span class="sxs-lookup"><span data-stu-id="35704-136">hello **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="35704-137">alias di input Hello utilizzato nello script di query hello.</span><span class="sxs-lookup"><span data-stu-id="35704-137">hello input alias is used in hello query script.</span></span> 
3.  <span data-ttu-id="35704-138">In **Tipo di origine** selezionare **Flusso dati**.</span><span class="sxs-lookup"><span data-stu-id="35704-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="35704-139">In **Origine** selezionare **Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="35704-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="35704-140">In **Service Bus Namespace**selezionare hello **TollData** opzione.</span><span class="sxs-lookup"><span data-stu-id="35704-140">In **Service Bus Namespace**, select hello **TollData** option.</span></span>
6.  <span data-ttu-id="35704-141">In **Nome hub eventi** selezionare **voce**.</span><span class="sxs-lookup"><span data-stu-id="35704-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="35704-142">In **nome criterio Hub eventi**selezionare **RootManageSharedAccessKey** (valore predefinito di hello).</span><span class="sxs-lookup"><span data-stu-id="35704-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (hello default value).</span></span>
8.  <span data-ttu-id="35704-143">In **Formato di serializzazione eventi** selezionare **Json**.</span><span class="sxs-lookup"><span data-stu-id="35704-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="35704-144">In **Codifica** selezionare **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="35704-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="35704-145">Le impostazioni dovrebbero essere simile hello seguente schermata:</span><span class="sxs-lookup"><span data-stu-id="35704-145">Your settings should look like hello following screenshot:</span></span>

    ![Finestra di input](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="35704-147">procedura guidata hello toofinish, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="35704-147">toofinish hello wizard, click **Save**.</span></span> <span data-ttu-id="35704-148">È ora possibile aggiungere un altro flusso di uscita hello di toocreate origine di input.</span><span class="sxs-lookup"><span data-stu-id="35704-148">Now you can add another input source toocreate hello exit stream.</span></span> <span data-ttu-id="35704-149">Pulsante destro del mouse hello **input** nodo e selezionare **nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="35704-149">Right-click hello **Inputs** node, and select **New Item**.</span></span>

    ![Nuovo elemento](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="35704-151">Nella finestra hello selezionare **Input Analitica del flusso di Azure**e modificare hello **nome** troppo**ExitStream.json**.</span><span class="sxs-lookup"><span data-stu-id="35704-151">In hello window, select **Azure Stream Analytics Input**, and change hello **Name** too**ExitStream.json**.</span></span> <span data-ttu-id="35704-152">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="35704-152">Click **Add**.</span></span>

    ![Finestra Aggiungi nuovo elemento](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="35704-154">Fare doppio clic su **ExitStream.json** nel progetto hello e seguire hello stessi passaggi per il flusso di voce hello.</span><span class="sxs-lookup"><span data-stu-id="35704-154">Double-click **ExitStream.json** in hello project, and follow hello same steps as you did for hello entry stream.</span></span> <span data-ttu-id="35704-155">Tooenter assicurarsi di essere **uscire** per hello **nome Hub eventi** come illustrato nella seguente schermata hello:</span><span class="sxs-lookup"><span data-stu-id="35704-155">Be sure tooenter **exit** for hello **Event Hub Name** as shown in hello following screenshot:</span></span>

    ![Finestra ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="35704-157">A questo punto sono presenti due flussi di input definiti:</span><span class="sxs-lookup"><span data-stu-id="35704-157">Now you have defined two input streams:</span></span>

    ![Flussi di input di entrata e di uscita](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="35704-159">Successivamente, aggiungere l'input di dati di riferimento per i file blob hello che contiene dati di registrazione dell'automobile.</span><span class="sxs-lookup"><span data-stu-id="35704-159">Next, add reference data input for hello blob file that contains car registration data.</span></span>

13. <span data-ttu-id="35704-160">Pulsante destro del mouse hello **input** nodo nel progetto hello e quindi seguire hello stessi passaggi anche per gli input flusso hello.</span><span class="sxs-lookup"><span data-stu-id="35704-160">Right-click hello **Inputs** node in hello project, and then follow hello same steps as you did for hello stream inputs.</span></span> <span data-ttu-id="35704-161">In **Alias di input** immettere **Registrazione** e in **Tipo di origine** selezionare **Dati di riferimento**.</span><span class="sxs-lookup"><span data-stu-id="35704-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![Finestra Registrazione](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="35704-163">In **Account di archiviazione**selezionare hello **tolldata** opzione.</span><span class="sxs-lookup"><span data-stu-id="35704-163">In **Storage Account**, select hello **tolldata** option.</span></span> <span data-ttu-id="35704-164">In **Contenitore** selezionare **tolldata** e in **Modello percorso** immettere **registration.json**.</span><span class="sxs-lookup"><span data-stu-id="35704-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="35704-165">Il nome file fa distinzione tra maiuscole e minuscole e deve contenere solo lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="35704-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="35704-166">procedura guidata hello toofinish, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="35704-166">toofinish hello wizard, click **Save**.</span></span>

<span data-ttu-id="35704-167">Ora sono definiti tutti gli input hello.</span><span class="sxs-lookup"><span data-stu-id="35704-167">Now all hello inputs are defined.</span></span>

## <a name="define-hello-output"></a><span data-ttu-id="35704-168">Definire l'output di hello</span><span class="sxs-lookup"><span data-stu-id="35704-168">Define hello output</span></span>
1.  <span data-ttu-id="35704-169">In **Esplora**, espandere hello **input** nodo e fare doppio clic su **Output.json**.</span><span class="sxs-lookup"><span data-stu-id="35704-169">In **Solution Explorer**, expand hello **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="35704-170">In **Alias di output** immettere **output**.</span><span class="sxs-lookup"><span data-stu-id="35704-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="35704-171">In **Sink** selezionare **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="35704-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="35704-172">In **Database** selezionare **TollDataDB**.</span><span class="sxs-lookup"><span data-stu-id="35704-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="35704-173">In **Nome utente** immettere **tolladmin**.</span><span class="sxs-lookup"><span data-stu-id="35704-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="35704-174">In **Password** immettere **123toll!**.</span><span class="sxs-lookup"><span data-stu-id="35704-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="35704-175">In **Tabella** immettere **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="35704-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="35704-176">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="35704-176">Click **Save**.</span></span>

    ![Finestra Output](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="35704-178">Creare una query di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="35704-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="35704-179">In questa esercitazione tenta tooanswer diverse domande aziendali tootoll correlate a dati.</span><span class="sxs-lookup"><span data-stu-id="35704-179">This tutorial attempts tooanswer several business questions that are related tootoll data.</span></span> <span data-ttu-id="35704-180">Viene inoltre costruito query Analitica di flusso che può essere usata nelle risposte di flusso Analitica tooprovide pertinente.</span><span class="sxs-lookup"><span data-stu-id="35704-180">It also constructs Stream Analytics queries that can be used in Stream Analytics tooprovide relevant answers.</span></span>
<span data-ttu-id="35704-181">Prima di iniziare il primo processo di flusso Analitica, analizziamo una semplice sintassi di query di scenario e hello.</span><span class="sxs-lookup"><span data-stu-id="35704-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and hello query syntax.</span></span>

### <a name="introduction-toohello-stream-analytics-query-language"></a><span data-ttu-id="35704-182">Introduzione toohello linguaggio di query Analitica di flusso</span><span class="sxs-lookup"><span data-stu-id="35704-182">Introduction toohello Stream Analytics query language</span></span>
<span data-ttu-id="35704-183">Si supponga che è necessario numero hello toocount dei veicoli che immette un casello.</span><span class="sxs-lookup"><span data-stu-id="35704-183">Let’s say that you need toocount hello number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="35704-184">Poiché in questo esempio è un flusso continuo di eventi, occorre toodefine un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="35704-184">Because this example is a continuous stream of events, you have toodefine a period of time.</span></span> <span data-ttu-id="35704-185">Modificare toobe domanda hello "quanti veicoli immettere un casello ogni tre minuti?"</span><span class="sxs-lookup"><span data-stu-id="35704-185">Modify hello question toobe “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="35704-186">Toocount in questo modo sono in genere di dati di cui tooas hello a cascata conteggio.</span><span class="sxs-lookup"><span data-stu-id="35704-186">This way toocount data is commonly referred tooas hello tumbling count.</span></span>

<span data-ttu-id="35704-187">Esaminare query flusso Analitica hello che risponda a questa domanda:</span><span class="sxs-lookup"><span data-stu-id="35704-187">Look at hello Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="35704-188">Flusso Analitica Usa un linguaggio di query che è simile a SQL e aggiunge alcune estensioni toospecify ora aspetti delle query hello.</span><span class="sxs-lookup"><span data-stu-id="35704-188">Stream Analytics uses a query language that's like SQL and adds a few extensions toospecify time-related aspects of hello query.</span></span>

<span data-ttu-id="35704-189">Per ulteriori informazioni, vedere [gestione del tempo](https://msdn.microsoft.com/library/azure/mt582045.aspx) e [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) costrutti utilizzati nella query hello da MSDN.</span><span class="sxs-lookup"><span data-stu-id="35704-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in hello query from MSDN.</span></span>

<span data-ttu-id="35704-190">Ora che è stato scritto della prima query Analitica di flusso, è ora tootest è.</span><span class="sxs-lookup"><span data-stu-id="35704-190">Now that you have written your first Stream Analytics query, it's time tootest it.</span></span> <span data-ttu-id="35704-191">Utilizzare i file di dati di esempio hello si trova nella cartella TollApp nel seguente percorso hello:</span><span class="sxs-lookup"><span data-stu-id="35704-191">Use hello sample data files located in your TollApp folder in hello following path:</span></span>

<span data-ttu-id="35704-192">..\TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="35704-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="35704-193">Questa cartella contiene i seguenti file hello:</span><span class="sxs-lookup"><span data-stu-id="35704-193">This folder contains hello following files:</span></span>
*   <span data-ttu-id="35704-194">Entry.json</span><span class="sxs-lookup"><span data-stu-id="35704-194">Entry.json</span></span>
*   <span data-ttu-id="35704-195">Exit.json</span><span class="sxs-lookup"><span data-stu-id="35704-195">Exit.json</span></span>
*   <span data-ttu-id="35704-196">registration.json</span><span class="sxs-lookup"><span data-stu-id="35704-196">Registration.json</span></span>

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="35704-197">Numero di hello dei veicoli immettendo un casello</span><span class="sxs-lookup"><span data-stu-id="35704-197">Count hello number of vehicles entering a toll booth</span></span>
<span data-ttu-id="35704-198">Nel progetto hello, fare doppio clic su **Script.asaql** tooopen script hello hello **Editor di Query**.</span><span class="sxs-lookup"><span data-stu-id="35704-198">In hello project, double-click **Script.asaql** tooopen hello script in hello **Query Editor**.</span></span> <span data-ttu-id="35704-199">Copiare e incollare script hello nella sezione precedente hello in editor hello.</span><span class="sxs-lookup"><span data-stu-id="35704-199">Copy and paste hello script in hello previous section into hello editor.</span></span> <span data-ttu-id="35704-200">Hello Editor di Query supporta IntelliSense, colorazione della sintassi e indicatore di errore hello.</span><span class="sxs-lookup"><span data-stu-id="35704-200">hello Query Editor supports IntelliSense, syntax coloring, and hello error marker.</span></span>

![Editor di query](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="35704-202">Eseguire test locali delle query di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="35704-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="35704-203">toocompile hello query toosee se si verifica un errore di sintassi, fare clic sul progetto hello e selezionare **compilare**.</span><span class="sxs-lookup"><span data-stu-id="35704-203">toocompile hello query toosee if there is a syntax error, right-click hello project and select **Build**.</span></span> 

2. <span data-ttu-id="35704-204">toovalidate questa query nei dati di esempio, è possibile utilizzare i dati di esempio locale.</span><span class="sxs-lookup"><span data-stu-id="35704-204">toovalidate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="35704-205">Input hello e scegliere **aggiungere input locale**.</span><span class="sxs-lookup"><span data-stu-id="35704-205">Right-click hello input, and select **Add local input**.</span></span>

    ![Add local input (Aggiungi input locale)](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="35704-207">Nella finestra popup hello, selezionare i dati di esempio hello dal percorso locale.</span><span class="sxs-lookup"><span data-stu-id="35704-207">In hello pop-up window, select hello sample data from your local path.</span></span> <span data-ttu-id="35704-208">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="35704-208">Click **Save**.</span></span>

    ![Finestra Add local input (Aggiungi input locale)](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="35704-210">Un file denominato **local_EntryStream.json** viene aggiunto automaticamente tooyour cartella di input.</span><span class="sxs-lookup"><span data-stu-id="35704-210">A file named **local_EntryStream.json** is automatically added tooyour inputs folder.</span></span>

    ![Cartella tooinputs aggiunta di file](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="35704-212">In hello **Editor di Query**, fare clic su **eseguire localmente**.</span><span class="sxs-lookup"><span data-stu-id="35704-212">In hello **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="35704-213">Oppure è possibile premere F5 di hello.</span><span class="sxs-lookup"><span data-stu-id="35704-213">Or you can press hello F5 key.</span></span>

    ![Esecuzione locale](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Output esecuzione locale](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="35704-216">Premere alcun output di hello tooview chiave in hello **il risultato di esecuzione locale** finestra in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="35704-216">Press any key tooview hello output in hello **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![Finestra Risultato esecuzione locale ASA](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="35704-218">Fare clic su **Apri cartella risultato** dei file di output di hello toocheck entrambi in formato CSV e JSON.</span><span class="sxs-lookup"><span data-stu-id="35704-218">Click **Open Result Folder** toocheck hello output files both in CSV and JSON format.</span></span>

    ![Output di Apri cartella risultati](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a><span data-ttu-id="35704-220">Dati di input di esempio hello</span><span class="sxs-lookup"><span data-stu-id="35704-220">Sample hello input data</span></span>
<span data-ttu-id="35704-221">È inoltre possibile dati di input di esempio di file locale tooa di origini di input.</span><span class="sxs-lookup"><span data-stu-id="35704-221">You can also sample input data from input sources tooa local file.</span></span> 
1. <span data-ttu-id="35704-222">Fare clic sul file di configurazione di input hello e selezionare **dati di esempio**.</span><span class="sxs-lookup"><span data-stu-id="35704-222">Right-click hello input config file, and select **Sample Data**.</span></span> 

   ![Dati di esempio](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="35704-224">È possibile campionare solo l'hub eventi o l'hub IoT per ora.</span><span class="sxs-lookup"><span data-stu-id="35704-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="35704-225">Non sono supportate altre origini di input.</span><span class="sxs-lookup"><span data-stu-id="35704-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="35704-226">Nella finestra popup hello immettere dati di esempio hello toosave hello percorso locale utilizzato.</span><span class="sxs-lookup"><span data-stu-id="35704-226">In hello pop-up window, enter hello local path used toosave hello sample data.</span></span> <span data-ttu-id="35704-227">Fare clic su **Esempio**.</span><span class="sxs-lookup"><span data-stu-id="35704-227">Click **Sample**.</span></span>

    ![Finestra Dati di esempio](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="35704-229">È possibile visualizzare lo stato di avanzamento hello in hello **Output** finestra.</span><span class="sxs-lookup"><span data-stu-id="35704-229">You can see hello progress in hello **Output** window.</span></span> 

    ![Finestra Output](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a><span data-ttu-id="35704-231">Inviare un tooAzure query Analitica di flusso</span><span class="sxs-lookup"><span data-stu-id="35704-231">Submit a Stream Analytics query tooAzure</span></span>
1. <span data-ttu-id="35704-232">In hello **Editor di Query**, fare clic su **inviare tooAzure** nell'editor di script hello.</span><span class="sxs-lookup"><span data-stu-id="35704-232">In hello **Query Editor**, click **Submit tooAzure** in hello script editor.</span></span>

    ![Inviare tooAzure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="35704-234">Selezionare **Creare un nuovo processo di analisi di flusso di Azure**.</span><span class="sxs-lookup"><span data-stu-id="35704-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="35704-235">Immettere hello **nome del processo**e seleziona hello corretto **sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="35704-235">Enter hello **Job Name**, and select hello correct **Subscription**.</span></span> <span data-ttu-id="35704-236">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="35704-236">Click **Submit**.</span></span>

    ![Finestra di invio del processo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="35704-238">Avviare un processo</span><span class="sxs-lookup"><span data-stu-id="35704-238">Start a job</span></span>
<span data-ttu-id="35704-239">Dopo aver creato il processo, visualizzazione dei processi hello viene aperto automaticamente.</span><span class="sxs-lookup"><span data-stu-id="35704-239">Now that your job is created, hello job view is automatically opened.</span></span> 
1. <span data-ttu-id="35704-240">hello toostart di processo, fare clic su hello **freccia verde** pulsante.</span><span class="sxs-lookup"><span data-stu-id="35704-240">toostart hello job, click hello **green arrow** button.</span></span>

    ![Avviare un processo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="35704-242">Selezionare l'impostazione predefinita hello e fare clic su **avviare**.</span><span class="sxs-lookup"><span data-stu-id="35704-242">Select hello default setting, and click **Start**.</span></span>
 
    ![Finestra Avvia processo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="35704-244">processo Hello **stato** cambia troppo**esecuzione**, e **gli eventi di Input** e **gli eventi di Output** vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="35704-244">hello job **Status** changes too**Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![Stato In esecuzione in Riepilogo processo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a><span data-ttu-id="35704-246">Controllare i risultati di hello in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="35704-246">Check hello results in Visual Studio</span></span>
1. <span data-ttu-id="35704-247">In Visual Studio, aprire **Esplora Server** rapida hello e **TollDataRefJoin** tabella.</span><span class="sxs-lookup"><span data-stu-id="35704-247">In Visual Studio, open **Server Explorer** and right-click hello **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="35704-248">Selezionare **Mostra dati tabella** toosee output di hello del processo.</span><span class="sxs-lookup"><span data-stu-id="35704-248">Select **Show Table Data** toosee hello output of your job.</span></span>
   
    ![Selezione di Mostra dati tabella in Esplora server](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a><span data-ttu-id="35704-250">Visualizzazione hello processo metriche</span><span class="sxs-lookup"><span data-stu-id="35704-250">View hello job metrics</span></span>
<span data-ttu-id="35704-251">È possibile trovare alcune statistiche di base sul processo in **Job Metrics** (Metriche di processo).</span><span class="sxs-lookup"><span data-stu-id="35704-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![Finestra Job Metrics (Metriche di processo)](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a><span data-ttu-id="35704-253">Processo di hello elenco in Esplora Server</span><span class="sxs-lookup"><span data-stu-id="35704-253">List hello job in Server Explorer</span></span>
<span data-ttu-id="35704-254">In **Esplora server** fare clic su **Processi di Analisi di flusso** e quindi fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="35704-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="35704-255">processo Hello viene visualizzata sotto **i processi di flusso Analitica**.</span><span class="sxs-lookup"><span data-stu-id="35704-255">hello job appears under **Stream Analytics jobs**.</span></span>

![Processi di Analisi di flusso elencati in Esplora server](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a><span data-ttu-id="35704-257">Visualizzazione processo hello aperto</span><span class="sxs-lookup"><span data-stu-id="35704-257">Open hello job view</span></span>
<span data-ttu-id="35704-258">visualizzazione dei processi tooopen hello, espandere il nodo del processo e fare doppio clic su hello **Visualizza processo** nodo.</span><span class="sxs-lookup"><span data-stu-id="35704-258">tooopen hello job view, expand your job node and double-click hello **Job View** node.</span></span>

![Nodo Job View (Visualizzazione processo)](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a><span data-ttu-id="35704-260">Esportare un progetto di tooa processo esistente</span><span class="sxs-lookup"><span data-stu-id="35704-260">Export an existing job tooa project</span></span>
<span data-ttu-id="35704-261">Esistono due modi, è possibile esportare un progetto di tooa processo esistente.</span><span class="sxs-lookup"><span data-stu-id="35704-261">There are two ways you can export an existing job tooa project.</span></span>

<span data-ttu-id="35704-262">In **Esplora Server**, rapida del nodo del processo hello in hello **i processi di flusso Analitica** nodo e selezionare **esportare tooNew flusso Analitica progetto**.</span><span class="sxs-lookup"><span data-stu-id="35704-262">In **Server Explorer**, right-click hello job node in hello **Stream Analytics Jobs** node and select **Export tooNew Stream Analytics Project**.</span></span>

![Esportazione tooNew flusso Analitica progetto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="35704-264">progetto Hello viene generato in **Esplora**.</span><span class="sxs-lookup"><span data-stu-id="35704-264">hello project is generated in **Solution Explorer**.</span></span>

![Progetto generato in Esplora soluzioni](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="35704-266">È inoltre possibile utilizzare la visualizzazione processi hello e fare clic su **generare progetto**.</span><span class="sxs-lookup"><span data-stu-id="35704-266">You also can use hello job view, and click **Generate Project**.</span></span>

![Genera progetto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="35704-268">Problemi noti e limitazioni</span><span class="sxs-lookup"><span data-stu-id="35704-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="35704-269">Non è disponibile alcun supporto per l'output di Power BI e dell'archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="35704-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="35704-270">Non è disponibile alcun supporto dell'editor per l'aggiunta o la modifica di funzioni JavaScript definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="35704-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35704-271">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="35704-271">Next steps</span></span>
* [<span data-ttu-id="35704-272">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="35704-272">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="35704-273">Introduzione all'uso di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="35704-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="35704-274">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="35704-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="35704-275">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="35704-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="35704-276">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="35704-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

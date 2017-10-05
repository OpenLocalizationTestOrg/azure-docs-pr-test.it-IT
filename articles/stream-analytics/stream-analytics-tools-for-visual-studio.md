---
title: Usare gli strumenti di Analisi di flusso di Azure per Visual Studio | Microsoft Docs
description: Esercitazione introduttiva per gli strumenti di Analisi di flusso di Azure per Visual Studio
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
ms.openlocfilehash: 618c1055795a75e0ed71dacddba3e076f81f4946
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="fe0c4-104">Usare gli strumenti di Analisi di flusso di Azure per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fe0c4-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="fe0c4-105">Introduzione</span><span class="sxs-lookup"><span data-stu-id="fe0c4-105">Introduction</span></span>
<span data-ttu-id="fe0c4-106">Questa esercitazione illustra come usare gli strumenti di Analisi di flusso di Azure per Visual Studio per creare, scrivere, testare in locale, gestire ed eseguire il debug dei processi di Analisi di flusso di Azure.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-106">In this tutorial, you learn how to use Azure Stream Analytics Tools for Visual Studio to create, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="fe0c4-107">Dopo aver completato questa esercitazione, si sarà in grado di:</span><span class="sxs-lookup"><span data-stu-id="fe0c4-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="fe0c4-108">Usare gli strumenti di Analisi di flusso di Azure per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="fe0c4-109">Configurare e distribuire un processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="fe0c4-110">Testare il processo in locale con dati di esempio locali.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="fe0c4-111">Usare il monitoraggio per risolvere i problemi.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-111">Use monitoring to troubleshoot issues.</span></span>
* <span data-ttu-id="fe0c4-112">Esportare i processi esistenti nei progetti.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-112">Export existing jobs to projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe0c4-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fe0c4-113">Prerequisites</span></span>
<span data-ttu-id="fe0c4-114">Per completare questa esercitazione è necessario soddisfare i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="fe0c4-114">To complete this tutorial, you need the following prerequisites:</span></span>
* <span data-ttu-id="fe0c4-115">Completare i passaggi che precedono "Creare un processo di Analisi di flusso" nell'esercitazione [Compilare una soluzione IoT con Analisi di flusso](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="fe0c4-115">Finish the steps that precede "Create a Stream Analytics job" in the [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="fe0c4-116">Usare Visual Studio 2015, Visual Studio 2013 Update 4 oppure Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="fe0c4-117">Sono supportate le edizioni Enterprise (Ultimate/Premium), Professional e Community.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="fe0c4-118">L'edizione Express non è supportata.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-118">Express edition is not supported.</span></span> <span data-ttu-id="fe0c4-119">Visual Studio 2017 non è supportato.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="fe0c4-120">Usare Azure SDK per .NET versione 2.7.1 o successiva.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-120">Use the Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="fe0c4-121">Eseguire l'installazione usando [Installazione guidata piattaforma Web](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe0c4-121">Install it by using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="fe0c4-122">Installare gli [strumenti di Analisi di flusso di Azure per Visual Studio](http://aka.ms/asatoolsvs).</span><span class="sxs-lookup"><span data-stu-id="fe0c4-122">Install the [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="fe0c4-123">Creare un progetto di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="fe0c4-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="fe0c4-124">In Visual Studio fare clic sul menu **File** e selezionare **Nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-124">In Visual Studio, click the **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="fe0c4-125">Nell'elenco dei modelli a sinistra selezionare **Analisi di flusso** e quindi fare clic su **Applicazione Analisi di flusso di Azure**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-125">In the templates list on the left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="fe0c4-126">Immettere il **Nome**, il **Percorso** e il **Nome della soluzione** del progetto come per altri progetti.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-126">Enter the project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![Finestra Nuovo progetto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="fe0c4-128">Verrà generato un progetto **Toll** in **Esplora soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![Progetto Toll generato in Esplora soluzioni](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-the-correct-subscription"></a><span data-ttu-id="fe0c4-130">Scegliere la sottoscrizione corretta</span><span class="sxs-lookup"><span data-stu-id="fe0c4-130">Choose the correct subscription</span></span>
1. <span data-ttu-id="fe0c4-131">In Visual Studio fare clic sul menu **Visualizza** e aprire **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-131">In Visual Studio, click the **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="fe0c4-132">Accedere con l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-132">Sign in with your Azure Account.</span></span> 

## <a name="define-the-input-sources"></a><span data-ttu-id="fe0c4-133">Definire le origini di input</span><span class="sxs-lookup"><span data-stu-id="fe0c4-133">Define the input sources</span></span>
1.  <span data-ttu-id="fe0c4-134">In **Esplora soluzioni** espandere il nodo **Inputs** e rinominare **Input.json** in **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-134">In **Solution Explorer**, expand the **Inputs** node and rename **Input.json** to **EntryStream.json**.</span></span> <span data-ttu-id="fe0c4-135">Fare doppio clic su **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="fe0c4-136">L'**Alias di input** è ora **EntryStream**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-136">The **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="fe0c4-137">L'alias di input viene usato nello script di query.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-137">The input alias is used in the query script.</span></span> 
3.  <span data-ttu-id="fe0c4-138">In **Tipo di origine** selezionare **Flusso dati**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="fe0c4-139">In **Origine** selezionare **Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="fe0c4-140">In **Spazio dei nomi del bus di servizio** selezionare l'opzione **TollData**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-140">In **Service Bus Namespace**, select the **TollData** option.</span></span>
6.  <span data-ttu-id="fe0c4-141">In **Nome hub eventi** selezionare **voce**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="fe0c4-142">In **Nome criterio hub eventi** selezionare **RootManageSharedAccessKey** (valore predefinito).</span><span class="sxs-lookup"><span data-stu-id="fe0c4-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (the default value).</span></span>
8.  <span data-ttu-id="fe0c4-143">In **Formato di serializzazione eventi** selezionare **Json**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="fe0c4-144">In **Codifica** selezionare **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="fe0c4-145">Le impostazioni dovrebbero essere simili allo screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="fe0c4-145">Your settings should look like the following screenshot:</span></span>

    ![Finestra di input](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="fe0c4-147">Per completare la procedura guidata fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-147">To finish the wizard, click **Save**.</span></span> <span data-ttu-id="fe0c4-148">A questo punto è possibile aggiungere un'altra origine di input per creare il flusso di uscita.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-148">Now you can add another input source to create the exit stream.</span></span> <span data-ttu-id="fe0c4-149">Fare clic con il pulsante destro del mouse sul nodo **Inputs** e selezionare **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-149">Right-click the **Inputs** node, and select **New Item**.</span></span>

    ![Nuovo elemento](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="fe0c4-151">Nella finestra selezionare **Input di Analisi di flusso di Azure** e modificare il **Nome** in **ExitStream.json**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-151">In the window, select **Azure Stream Analytics Input**, and change the **Name** to **ExitStream.json**.</span></span> <span data-ttu-id="fe0c4-152">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-152">Click **Add**.</span></span>

    ![Finestra Aggiungi nuovo elemento](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="fe0c4-154">Fare doppio clic su **ExitStream.json** nel progetto e seguire gli stessi passaggi del flusso di entrata.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-154">Double-click **ExitStream.json** in the project, and follow the same steps as you did for the entry stream.</span></span> <span data-ttu-id="fe0c4-155">Assicurarsi di immettere **exit** in **Nome hub eventi** come mostrato nella schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="fe0c4-155">Be sure to enter **exit** for the **Event Hub Name** as shown in the following screenshot:</span></span>

    ![Finestra ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="fe0c4-157">A questo punto sono presenti due flussi di input definiti:</span><span class="sxs-lookup"><span data-stu-id="fe0c4-157">Now you have defined two input streams:</span></span>

    ![Flussi di input di entrata e di uscita](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="fe0c4-159">Aggiungere successivamente l'input di dati di riferimento per il file BLOB contenente i dati di registrazione dell'automobile.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-159">Next, add reference data input for the blob file that contains car registration data.</span></span>

13. <span data-ttu-id="fe0c4-160">Fare clic con il pulsante destro del mouse sul nodo **Inputs** nel progetto e quindi seguire gli stessi passaggi degli input di flusso.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-160">Right-click the **Inputs** node in the project, and then follow the same steps as you did for the stream inputs.</span></span> <span data-ttu-id="fe0c4-161">In **Alias di input** immettere **Registrazione** e in **Tipo di origine** selezionare **Dati di riferimento**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![Finestra Registrazione](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="fe0c4-163">In **Account di archiviazione** selezionare l'opzione **tolldata**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-163">In **Storage Account**, select the **tolldata** option.</span></span> <span data-ttu-id="fe0c4-164">In **Contenitore** selezionare **tolldata** e in **Modello percorso** immettere **registration.json**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="fe0c4-165">Il nome file fa distinzione tra maiuscole e minuscole e deve contenere solo lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="fe0c4-166">Per completare la procedura guidata fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-166">To finish the wizard, click **Save**.</span></span>

<span data-ttu-id="fe0c4-167">Tutti gli input sono ora definiti.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-167">Now all the inputs are defined.</span></span>

## <a name="define-the-output"></a><span data-ttu-id="fe0c4-168">Definire l'output</span><span class="sxs-lookup"><span data-stu-id="fe0c4-168">Define the output</span></span>
1.  <span data-ttu-id="fe0c4-169">In **Esplora soluzioni** espandere il nodo **Inputs** e fare doppio clic su **Output.json**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-169">In **Solution Explorer**, expand the **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="fe0c4-170">In **Alias di output** immettere **output**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="fe0c4-171">In **Sink** selezionare **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="fe0c4-172">In **Database** selezionare **TollDataDB**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="fe0c4-173">In **Nome utente** immettere **tolladmin**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="fe0c4-174">In **Password** immettere **123toll!**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="fe0c4-175">In **Tabella** immettere **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="fe0c4-176">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-176">Click **Save**.</span></span>

    ![Finestra Output](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="fe0c4-178">Creare una query di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="fe0c4-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="fe0c4-179">Lo scopo di questa esercitazione è di rispondere a varie domande aziendali correlate ai dati dei caselli.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-179">This tutorial attempts to answer several business questions that are related to toll data.</span></span> <span data-ttu-id="fe0c4-180">Crea anche query di Analisi di flusso che possono essere usate in Analisi di flusso per fornire risposte pertinenti.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-180">It also constructs Stream Analytics queries that can be used in Stream Analytics to provide relevant answers.</span></span>
<span data-ttu-id="fe0c4-181">Prima di iniziare il primo processo di Analisi di flusso, esaminiamo uno scenario semplice e la sintassi delle query.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and the query syntax.</span></span>

### <a name="introduction-to-the-stream-analytics-query-language"></a><span data-ttu-id="fe0c4-182">Introduzione al linguaggio di query di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="fe0c4-182">Introduction to the Stream Analytics query language</span></span>
<span data-ttu-id="fe0c4-183">Si supponga di dover contare il numero di veicoli che entra in un casello.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-183">Let’s say that you need to count the number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="fe0c4-184">Trattandosi di un flusso continuo di eventi, è necessario stabilire un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-184">Because this example is a continuous stream of events, you have to define a period of time.</span></span> <span data-ttu-id="fe0c4-185">La domanda dovrà essere posta come segue: "Quanti veicoli passano un casello ogni tre minuti?"</span><span class="sxs-lookup"><span data-stu-id="fe0c4-185">Modify the question to be “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="fe0c4-186">Questo tipo di conteggio viene detto a cascata.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-186">This way to count data is commonly referred to as the tumbling count.</span></span>

<span data-ttu-id="fe0c4-187">Si osservi la query di Analisi di flusso che risponde a questa domanda:</span><span class="sxs-lookup"><span data-stu-id="fe0c4-187">Look at the Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="fe0c4-188">Analisi di flusso usa un linguaggio di query simile a SQL e aggiunge alcune estensioni per specificare gli aspetti temporali della query.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-188">Stream Analytics uses a query language that's like SQL and adds a few extensions to specify time-related aspects of the query.</span></span>

<span data-ttu-id="fe0c4-189">Per maggiori dettagli, vedere gli articoli di MSDN sui costrutti relativi alla [gestione del tempo](https://msdn.microsoft.com/library/azure/mt582045.aspx) e alla [funzione di windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) usati nella query.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in the query from MSDN.</span></span>

<span data-ttu-id="fe0c4-190">Ora che è stata scritta la prima query di Analisi di flusso, è necessario eseguirne il test.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-190">Now that you have written your first Stream Analytics query, it's time to test it.</span></span> <span data-ttu-id="fe0c4-191">Usare i file di dati di esempio che si trovano nella cartella TollApp nel percorso seguente:</span><span class="sxs-lookup"><span data-stu-id="fe0c4-191">Use the sample data files located in your TollApp folder in the following path:</span></span>

<span data-ttu-id="fe0c4-192">..\TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="fe0c4-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="fe0c4-193">Questa cartella contiene i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="fe0c4-193">This folder contains the following files:</span></span>
*   <span data-ttu-id="fe0c4-194">Entry.json</span><span class="sxs-lookup"><span data-stu-id="fe0c4-194">Entry.json</span></span>
*   <span data-ttu-id="fe0c4-195">Exit.json</span><span class="sxs-lookup"><span data-stu-id="fe0c4-195">Exit.json</span></span>
*   <span data-ttu-id="fe0c4-196">registration.json</span><span class="sxs-lookup"><span data-stu-id="fe0c4-196">Registration.json</span></span>

## <a name="count-the-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="fe0c4-197">Contare il numero di veicoli che passano un casello</span><span class="sxs-lookup"><span data-stu-id="fe0c4-197">Count the number of vehicles entering a toll booth</span></span>
<span data-ttu-id="fe0c4-198">Nel progetto fare doppio clic su **Script.asaql** per aprire lo script nell'**Editor di query**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-198">In the project, double-click **Script.asaql** to open the script in the **Query Editor**.</span></span> <span data-ttu-id="fe0c4-199">Copiare e incollare nell'editor lo script della sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-199">Copy and paste the script in the previous section into the editor.</span></span> <span data-ttu-id="fe0c4-200">L'editor di query supporta IntelliSense, la sintassi colorata e l'indicatore di errore.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-200">The Query Editor supports IntelliSense, syntax coloring, and the error marker.</span></span>

![Editor di query](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="fe0c4-202">Eseguire test locali delle query di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="fe0c4-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="fe0c4-203">Per compilare la query e vedere se sono presenti errori di sintassi, fare clic con il pulsante destro del mouse sul progetto e selezionare **Genera**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-203">To compile the query to see if there is a syntax error, right-click the project and select **Build**.</span></span> 

2. <span data-ttu-id="fe0c4-204">Per convalidare la query rispetto ai dati di esempio, è possibile usare dati di esempio locali.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-204">To validate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="fe0c4-205">Fare clic con il pulsante destro del mouse sull'input e selezionare **Add local input** (Aggiungi input locale).</span><span class="sxs-lookup"><span data-stu-id="fe0c4-205">Right-click the input, and select **Add local input**.</span></span>

    ![Add local input (Aggiungi input locale)](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="fe0c4-207">Nella finestra popup selezionare i dati di esempio dal percorso locale.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-207">In the pop-up window, select the sample data from your local path.</span></span> <span data-ttu-id="fe0c4-208">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-208">Click **Save**.</span></span>

    ![Finestra Add local input (Aggiungi input locale)](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="fe0c4-210">Verrà aggiunto automaticamente un file denominato **local_EntryStream.json** nella cartella degli input.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-210">A file named **local_EntryStream.json** is automatically added to your inputs folder.</span></span>

    ![File aggiunti alla cartella degli input](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="fe0c4-212">Nell'**Editor di query** fare clic su **Esecuzione locale**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-212">In the **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="fe0c4-213">In alternativa premere F5.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-213">Or you can press the F5 key.</span></span>

    ![Esecuzione locale](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Output esecuzione locale](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="fe0c4-216">Premere un tasto qualsiasi per visualizzare l'output nella finestra **Risultato esecuzione locale ASA** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-216">Press any key to view the output in the **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![Finestra Risultato esecuzione locale ASA](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="fe0c4-218">Fare clic su **Apri cartella risultati** per controllare i file di output nel formato sia CSV che JSON.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-218">Click **Open Result Folder** to check the output files both in CSV and JSON format.</span></span>

    ![Output di Apri cartella risultati](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-the-input-data"></a><span data-ttu-id="fe0c4-220">Dati di input di esempio</span><span class="sxs-lookup"><span data-stu-id="fe0c4-220">Sample the input data</span></span>
<span data-ttu-id="fe0c4-221">È possibile anche campionare dati di input da origini di input in un file locale.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-221">You can also sample input data from input sources to a local file.</span></span> 
1. <span data-ttu-id="fe0c4-222">Fare clic con il pulsante destro del mouse sul file di configurazione degli input e selezionare **Dati di esempio**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-222">Right-click the input config file, and select **Sample Data**.</span></span> 

   ![Dati di esempio](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="fe0c4-224">È possibile campionare solo l'hub eventi o l'hub IoT per ora.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="fe0c4-225">Non sono supportate altre origini di input.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="fe0c4-226">Nella finestra popup immettere il percorso locale usato per salvare i dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-226">In the pop-up window, enter the local path used to save the sample data.</span></span> <span data-ttu-id="fe0c4-227">Fare clic su **Esempio**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-227">Click **Sample**.</span></span>

    ![Finestra Dati di esempio](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="fe0c4-229">Nella finestra **Output** viene visualizzato lo stato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-229">You can see the progress in the **Output** window.</span></span> 

    ![Finestra Output](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-to-azure"></a><span data-ttu-id="fe0c4-231">Inviare ad Azure una query di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="fe0c4-231">Submit a Stream Analytics query to Azure</span></span>
1. <span data-ttu-id="fe0c4-232">Nell'**Editor di query** fare clic su **Invia ad Azure** nell'editor di script.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-232">In the **Query Editor**, click **Submit To Azure** in the script editor.</span></span>

    ![Inviare ad Azure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="fe0c4-234">Selezionare **Creare un nuovo processo di analisi di flusso di Azure**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="fe0c4-235">Immettere il **Nome processo** e selezionare la **Sottoscrizione** corretta.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-235">Enter the **Job Name**, and select the correct **Subscription**.</span></span> <span data-ttu-id="fe0c4-236">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-236">Click **Submit**.</span></span>

    ![Finestra di invio del processo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="fe0c4-238">Avviare un processo</span><span class="sxs-lookup"><span data-stu-id="fe0c4-238">Start a job</span></span>
<span data-ttu-id="fe0c4-239">Dopo che il processo è stato creato, viene aperta automaticamente la visualizzazione del processo.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-239">Now that your job is created, the job view is automatically opened.</span></span> 
1. <span data-ttu-id="fe0c4-240">Per avviare il processo fare clic sulla **freccia verde**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-240">To start the job, click the **green arrow** button.</span></span>

    ![Avviare un processo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="fe0c4-242">Selezionare l'impostazione predefinita e fare clic su **Avvia**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-242">Select the default setting, and click **Start**.</span></span>
 
    ![Finestra Avvia processo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="fe0c4-244">Lo **Stato** del processo viene impostato su **In esecuzione** e vengono visualizzati gli **Eventi di input** e gli **Eventi di output**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-244">The job **Status** changes to **Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![Stato In esecuzione in Riepilogo processo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-the-results-in-visual-studio"></a><span data-ttu-id="fe0c4-246">Controllare i risultati in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fe0c4-246">Check the results in Visual Studio</span></span>
1. <span data-ttu-id="fe0c4-247">In Visual Studio aprire **Esplora server** e fare clic con il pulsante destro del mouse sulla tabella **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-247">In Visual Studio, open **Server Explorer** and right-click the **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="fe0c4-248">Selezionare **Mostra dati tabella** per vedere l'output del processo.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-248">Select **Show Table Data** to see the output of your job.</span></span>
   
    ![Selezione di Mostra dati tabella in Esplora server](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-the-job-metrics"></a><span data-ttu-id="fe0c4-250">Visualizzare le metriche del processo</span><span class="sxs-lookup"><span data-stu-id="fe0c4-250">View the job metrics</span></span>
<span data-ttu-id="fe0c4-251">È possibile trovare alcune statistiche di base sul processo in **Job Metrics** (Metriche di processo).</span><span class="sxs-lookup"><span data-stu-id="fe0c4-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![Finestra Job Metrics (Metriche di processo)](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-the-job-in-server-explorer"></a><span data-ttu-id="fe0c4-253">Elencare il processo in Esplora server</span><span class="sxs-lookup"><span data-stu-id="fe0c4-253">List the job in Server Explorer</span></span>
<span data-ttu-id="fe0c4-254">In **Esplora server** fare clic su **Processi di Analisi di flusso** e quindi fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="fe0c4-255">Il processo viene visualizzato in **Processi di Analisi di flusso**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-255">The job appears under **Stream Analytics jobs**.</span></span>

![Processi di Analisi di flusso elencati in Esplora server](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-the-job-view"></a><span data-ttu-id="fe0c4-257">Aprire la visualizzazione del processo</span><span class="sxs-lookup"><span data-stu-id="fe0c4-257">Open the job view</span></span>
<span data-ttu-id="fe0c4-258">Per aprire la visualizzazione del processo, espandere il nodo del processo e fare doppio clic sul nodo **Job View** (Visualizzazione processo).</span><span class="sxs-lookup"><span data-stu-id="fe0c4-258">To open the job view, expand your job node and double-click the **Job View** node.</span></span>

![Nodo Job View (Visualizzazione processo)](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-to-a-project"></a><span data-ttu-id="fe0c4-260">Esportare un processo esistente in un progetto</span><span class="sxs-lookup"><span data-stu-id="fe0c4-260">Export an existing job to a project</span></span>
<span data-ttu-id="fe0c4-261">Esistono due modi per esportare un processo esistente in un progetto.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-261">There are two ways you can export an existing job to a project.</span></span>

<span data-ttu-id="fe0c4-262">In **Esplora server** fare clic con il pulsante destro del mouse sul nodo del processo nel nodo **Processi di Analisi di flusso** e selezionare **Esporta in un nuovo progetto di analisi di flusso**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-262">In **Server Explorer**, right-click the job node in the **Stream Analytics Jobs** node and select **Export to New Stream Analytics Project**.</span></span>

![Esportare in un nuovo progetto di analisi di flusso](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="fe0c4-264">Il progetto viene generato in **Esplora soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-264">The project is generated in **Solution Explorer**.</span></span>

![Progetto generato in Esplora soluzioni](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="fe0c4-266">È inoltre possibile usare la visualizzazione del processo e fare clic su **Genera progetto**.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-266">You also can use the job view, and click **Generate Project**.</span></span>

![Genera progetto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="fe0c4-268">Problemi noti e limitazioni</span><span class="sxs-lookup"><span data-stu-id="fe0c4-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="fe0c4-269">Non è disponibile alcun supporto per l'output di Power BI e dell'archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="fe0c4-270">Non è disponibile alcun supporto dell'editor per l'aggiunta o la modifica di funzioni JavaScript definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="fe0c4-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe0c4-271">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fe0c4-271">Next steps</span></span>
* [<span data-ttu-id="fe0c4-272">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="fe0c4-272">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="fe0c4-273">Introduzione all'uso di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="fe0c4-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="fe0c4-274">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="fe0c4-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="fe0c4-275">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="fe0c4-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="fe0c4-276">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="fe0c4-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

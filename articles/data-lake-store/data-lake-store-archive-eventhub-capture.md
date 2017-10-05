---
title: Acquisire dati da Hub eventi in Azure Data Lake Store | Microsoft Docs
description: Usare Azure Data Lake Store per acquisire dati da Hub eventi
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: a9e69576958ae96d22a4eb03d0df429f0b307298
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-data-lake-store-to-capture-data-from-event-hubs"></a><span data-ttu-id="0e31b-103">Usare Azure Data Lake Store per acquisire dati da Hub eventi</span><span class="sxs-lookup"><span data-stu-id="0e31b-103">Use Azure Data Lake Store to capture data from Event Hubs</span></span>

<span data-ttu-id="0e31b-104">Informazioni su come usare Azure Data Lake Store per acquisire i dati ricevuti da Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e31b-104">Learn how to use Azure Data Lake Store to capture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e31b-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0e31b-105">Prerequisites</span></span>

* <span data-ttu-id="0e31b-106">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-106">**An Azure subscription**.</span></span> <span data-ttu-id="0e31b-107">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e31b-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="0e31b-108">**Un account di Archivio Data Lake di Azure**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-108">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="0e31b-109">Per istruzioni su come crearne uno, vedere [Introduzione ad Azure Data Lake Store](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0e31b-109">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="0e31b-110">**Uno spazio dei nomi di Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="0e31b-111">Per istruzioni, vedere [Creare uno spazio dei nomi di Hub eventi](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span><span class="sxs-lookup"><span data-stu-id="0e31b-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="0e31b-112">Assicurarsi che l'account Data Lake Store e lo spazio dei nomi di Hub eventi si trovino nella stessa sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e31b-112">Make sure the Data Lake Store account and the Event Hubs namespace are in the same Azure subscription.</span></span>


## <a name="assign-permissions-to-event-hubs"></a><span data-ttu-id="0e31b-113">Assegnare autorizzazioni a Hub eventi</span><span class="sxs-lookup"><span data-stu-id="0e31b-113">Assign permissions to Event Hubs</span></span>

<span data-ttu-id="0e31b-114">In questa sezione si crea una cartella nell'account in cui si vuole acquisire i dati da Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="0e31b-114">In this section, you create a folder within the account where you want to capture the data from Event Hubs.</span></span> <span data-ttu-id="0e31b-115">Si assegnano anche le autorizzazioni a Hub eventi, in modo da consentire la scrittura di dati in un account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0e31b-115">You also assign permissions to Event Hubs so that it can write data into a Data Lake Store account.</span></span> 

1. <span data-ttu-id="0e31b-116">Aprire l'account Data Lake Store in cui si vuole acquisire i dati da Hub eventi e quindi fare clic su **Esplora dati**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-116">Open the Data Lake Store account where you want to capture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="0e31b-117">![Esplora dati di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Esplora dati di Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="0e31b-117">![Data Lake Store data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span></span>

2.  <span data-ttu-id="0e31b-118">Fare clic su **Nuova cartella** e quindi immettere un nome per la cartella in cui si vuole acquisire i dati.</span><span class="sxs-lookup"><span data-stu-id="0e31b-118">Click **New Folder** and then enter a name for folder where you want to capture the data.</span></span>

    <span data-ttu-id="0e31b-119">![Creare una nuova cartella in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Creare una nuova cartella in Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="0e31b-119">![Create a new folder in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span></span>

3. <span data-ttu-id="0e31b-120">Assegnare le autorizzazioni alla radice di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0e31b-120">Assign permissions at the root of the Data Lake Store.</span></span> 

    <span data-ttu-id="0e31b-121">a.</span><span class="sxs-lookup"><span data-stu-id="0e31b-121">a.</span></span> <span data-ttu-id="0e31b-122">Fare clic su **Esplora dati**, selezionare la radice dell'account Data Lake Store e quindi fare clic su **Accesso**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-122">Click **Data Explorer**, select the root of the Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="0e31b-123">![Assegnare le autorizzazioni per la radice di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assegnare le autorizzazioni per la radice di Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="0e31b-123">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="0e31b-124">b.</span><span class="sxs-lookup"><span data-stu-id="0e31b-124">b.</span></span> <span data-ttu-id="0e31b-125">In **Accesso** fare clic su **Aggiungi**, fare clic su **Selezionare l'utente o il gruppo** e quindi cercare `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="0e31b-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="0e31b-126">![Assegnare le autorizzazioni per la radice di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assegnare le autorizzazioni per la radice di Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="0e31b-126">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span></span>
    
    <span data-ttu-id="0e31b-127">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-127">Click **Select**.</span></span>

    <span data-ttu-id="0e31b-128">c.</span><span class="sxs-lookup"><span data-stu-id="0e31b-128">c.</span></span> <span data-ttu-id="0e31b-129">In **Assegna autorizzazioni** fare clic su **Selezionare le autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="0e31b-130">Impostare **Autorizzazioni** su **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-130">Set **Permissions** to **Execute**.</span></span> <span data-ttu-id="0e31b-131">Impostare **Aggiungi a** su **Questa cartella e tutti gli elementi figlio**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-131">Set **Add to** to **This folder and all children**.</span></span> <span data-ttu-id="0e31b-132">Impostare **Aggiungi come** su **Una voce di autorizzazione di accesso e una voce di autorizzazione predefinita**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-132">Set **Add as** to **An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="0e31b-133">![Assegnare le autorizzazioni per la radice di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assegnare le autorizzazioni per la radice di Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="0e31b-133">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="0e31b-134">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-134">Click **OK**.</span></span>

4. <span data-ttu-id="0e31b-135">Assegnare le autorizzazioni per la cartella nell'account Data Lake Store in cui si vuole acquisire i dati.</span><span class="sxs-lookup"><span data-stu-id="0e31b-135">Assign permissions for the folder under Data Lake Store account where you want to capture data.</span></span>

    <span data-ttu-id="0e31b-136">a.</span><span class="sxs-lookup"><span data-stu-id="0e31b-136">a.</span></span> <span data-ttu-id="0e31b-137">Fare clic su **Esplora dati**, selezionare la cartella nell'account Data Lake Store e quindi fare clic su **Accesso**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-137">Click **Data Explorer**, select the folder in the Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="0e31b-138">![Assegnare le autorizzazioni per la cartella di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assegnare le autorizzazioni per la cartella di Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="0e31b-138">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span></span>

    <span data-ttu-id="0e31b-139">b.</span><span class="sxs-lookup"><span data-stu-id="0e31b-139">b.</span></span> <span data-ttu-id="0e31b-140">In **Accesso** fare clic su **Aggiungi**, fare clic su **Selezionare l'utente o il gruppo** e quindi cercare `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="0e31b-140">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="0e31b-141">![Assegnare le autorizzazioni per la cartella di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assegnare le autorizzazioni per la cartella di Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="0e31b-141">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="0e31b-142">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-142">Click **Select**.</span></span>

    <span data-ttu-id="0e31b-143">c.</span><span class="sxs-lookup"><span data-stu-id="0e31b-143">c.</span></span> <span data-ttu-id="0e31b-144">In **Assegna autorizzazioni** fare clic su **Selezionare le autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-144">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="0e31b-145">Impostare **Autorizzazioni** su **Leggi, Scrivi** ed **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-145">Set **Permissions** to **Read, Write,** and **Execute**.</span></span> <span data-ttu-id="0e31b-146">Impostare **Aggiungi a** su **Questa cartella e tutti gli elementi figlio**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-146">Set **Add to** to **This folder and all children**.</span></span> <span data-ttu-id="0e31b-147">Impostare infine **Aggiungi come** su **Una voce di autorizzazione di accesso e una voce di autorizzazione predefinita**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-147">Finally, set **Add as** to **An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="0e31b-148">![Assegnare le autorizzazioni per la cartella di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assegnare le autorizzazioni per la cartella di Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="0e31b-148">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="0e31b-149">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-149">Click **OK**.</span></span> 

## <a name="configure-event-hubs-to-capture-data-to-data-lake-store"></a><span data-ttu-id="0e31b-150">Configurare Hub eventi per acquisire i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0e31b-150">Configure Event Hubs to capture data to Data Lake Store</span></span>

<span data-ttu-id="0e31b-151">In questa sezione si crea un hub eventi in uno spazio dei nomi di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="0e31b-151">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="0e31b-152">Si configura anche l'hub eventi per acquisire i dati in un account Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0e31b-152">You also configure the Event Hub to capture data to an Azure Data Lake Store account.</span></span> <span data-ttu-id="0e31b-153">Questa sezione presuppone che sia già stato creato uno spazio dei nomi di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="0e31b-153">This section assumes that you have already created an Event Hubs namespace.</span></span>

2. <span data-ttu-id="0e31b-154">Dal riquadro **Panoramica** dello spazio dei nomi di Hub eventi fare clic su **+ Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-154">From the **Overview** pane of the Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="0e31b-155">![Creare un hub eventi](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Creare un hub eventi")</span><span class="sxs-lookup"><span data-stu-id="0e31b-155">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

3. <span data-ttu-id="0e31b-156">Fornire i valori seguenti per configurare Hub eventi per acquisire i dati in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0e31b-156">Provide the following values to configure Event Hubs to capture data to Data Lake Store.</span></span>

    <span data-ttu-id="0e31b-157">![Creare un hub eventi](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Creare un hub eventi")</span><span class="sxs-lookup"><span data-stu-id="0e31b-157">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="0e31b-158">a.</span><span class="sxs-lookup"><span data-stu-id="0e31b-158">a.</span></span> <span data-ttu-id="0e31b-159">Specificare un nome per l'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="0e31b-159">Provide a name for the Event Hub.</span></span>
    
    <span data-ttu-id="0e31b-160">b.</span><span class="sxs-lookup"><span data-stu-id="0e31b-160">b.</span></span> <span data-ttu-id="0e31b-161">Per questa esercitazione, impostare **Numero di partizioni** e **Conservazione messaggi** sui valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="0e31b-161">For this tutorial, set **Partition Count** and **Message Retention** to the default values.</span></span>
    
    <span data-ttu-id="0e31b-162">c.</span><span class="sxs-lookup"><span data-stu-id="0e31b-162">c.</span></span> <span data-ttu-id="0e31b-163">Impostare **Acquisisci** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-163">Set **Capture** to **On**.</span></span> <span data-ttu-id="0e31b-164">Impostare **Intervallo di tempo** (frequenza di acquisizione) e **Intervallo dimensioni** (dimensioni dei dati da acquisire).</span><span class="sxs-lookup"><span data-stu-id="0e31b-164">Set the **Time Window** (how frequently to capture) and **Size Window** (data size to capture).</span></span> 
    
    <span data-ttu-id="0e31b-165">d.</span><span class="sxs-lookup"><span data-stu-id="0e31b-165">d.</span></span> <span data-ttu-id="0e31b-166">Per **Capture Provider** (Provider di acquisizione) selezionare **Azure Data Lake Store** e quindi selezionare l'istanza di Data Lake Store creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0e31b-166">For **Capture Provider**, select **Azure Data Lake Store** and the select the Data Lake Store you created earlier.</span></span> <span data-ttu-id="0e31b-167">Per **Data Lake Path** (Percorso Data Lake) immettere il nome della cartella creata nell'account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0e31b-167">For **Data Lake Path**, enter the name of the folder you created in the Data Lake Store account.</span></span> <span data-ttu-id="0e31b-168">È sufficiente fornire il percorso relativo della cartella.</span><span class="sxs-lookup"><span data-stu-id="0e31b-168">You only need to provide the relative path to the folder.</span></span>

    <span data-ttu-id="0e31b-169">e.</span><span class="sxs-lookup"><span data-stu-id="0e31b-169">e.</span></span> <span data-ttu-id="0e31b-170">Lasciare il valore predefinito per **Formati dei nomi file di acquisizione di esempio**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-170">Leave the **Sample capture file name formats** to the default value.</span></span> <span data-ttu-id="0e31b-171">Questa opzione controlla la struttura di cartelle che viene creata nella cartella di acquisizione.</span><span class="sxs-lookup"><span data-stu-id="0e31b-171">This option governs the folder structure that is created under the capture folder.</span></span>

    <span data-ttu-id="0e31b-172">f.</span><span class="sxs-lookup"><span data-stu-id="0e31b-172">f.</span></span> <span data-ttu-id="0e31b-173">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0e31b-173">Click **Create**.</span></span>

## <a name="test-the-setup"></a><span data-ttu-id="0e31b-174">Testare la configurazione</span><span class="sxs-lookup"><span data-stu-id="0e31b-174">Test the setup</span></span>

<span data-ttu-id="0e31b-175">È ora possibile testare la soluzione inviando i dati all'hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e31b-175">You can now test the solution by sending data to the Azure Event Hub.</span></span> <span data-ttu-id="0e31b-176">Seguire le istruzioni in [Inviare eventi a Hub eventi di Azure](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span><span class="sxs-lookup"><span data-stu-id="0e31b-176">Follow the instructions at [Send events to Azure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="0e31b-177">Una volta avviato l'invio dei dati, si vedranno i dati riflessi in Data Lake Store con la struttura di cartelle specificata.</span><span class="sxs-lookup"><span data-stu-id="0e31b-177">Once you start sending the data, you see the data reflected in Data Lake Store using the folder structure you specified.</span></span> <span data-ttu-id="0e31b-178">Si vedrà ad esempio in Data Lake Store una struttura di cartelle come quella illustrata nello screenshot seguente.</span><span class="sxs-lookup"><span data-stu-id="0e31b-178">For example, you see a folder structure, as shown in the following screenshot, in your Data Lake Store.</span></span>

<span data-ttu-id="0e31b-179">![Dati dell'hub eventi di esempio in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Dati dell'hub eventi di esempio in Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="0e31b-179">![Sample EventHub data in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span></span>

> [!NOTE]
> <span data-ttu-id="0e31b-180">Anche se non ci sono messaggi in arrivo in Hub eventi, Hub eventi scrive file vuoti con solo le intestazioni nell'account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0e31b-180">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just the headers into the Data Lake Store account.</span></span> <span data-ttu-id="0e31b-181">I file vengono scritti con lo stesso intervallo di tempo specificato durante la creazione di Hub di eventi.</span><span class="sxs-lookup"><span data-stu-id="0e31b-181">The files are written at the same time interval that you provided while creating the Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-store"></a><span data-ttu-id="0e31b-182">Analizzare i dati in Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="0e31b-182">Analyze data in Data Lake Store</span></span>

<span data-ttu-id="0e31b-183">Una volta che i dati si trovano in Data Lake Store, è possibile eseguire processi di analisi per elaborarli ed esaminarli.</span><span class="sxs-lookup"><span data-stu-id="0e31b-183">Once the data is in Data Lake Store, you can run analytical jobs to process and crunch the data.</span></span> <span data-ttu-id="0e31b-184">Vedere l'[esempio USQL Avro](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) relativo a come eseguire questa operazione usando Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0e31b-184">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how to do this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="0e31b-185">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0e31b-185">See also</span></span>
* [<span data-ttu-id="0e31b-186">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0e31b-186">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="0e31b-187">Copiare i dati da BLOB di archiviazione di Azure ad Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="0e31b-187">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)

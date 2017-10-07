---
title: dati aaaCapture dagli hub di eventi in un archivio Azure Data Lake | Documenti Microsoft
description: Dati toocapture archivio Azure Data Lake di uso di hub eventi
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
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a><span data-ttu-id="77373-103">Dati toocapture archivio Azure Data Lake di uso di hub eventi</span><span class="sxs-lookup"><span data-stu-id="77373-103">Use Azure Data Lake Store toocapture data from Event Hubs</span></span>

<span data-ttu-id="77373-104">Informazioni su come dati di archivio Azure Data Lake toocapture toouse ricevuto dall'hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="77373-104">Learn how toouse Azure Data Lake Store toocapture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77373-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="77373-105">Prerequisites</span></span>

* <span data-ttu-id="77373-106">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="77373-106">**An Azure subscription**.</span></span> <span data-ttu-id="77373-107">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77373-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="77373-108">**Un account Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="77373-108">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="77373-109">Per istruzioni su come toocreate uno, vedere [introduzione archivio Azure Data Lake](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="77373-109">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="77373-110">**Uno spazio dei nomi di Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="77373-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="77373-111">Per istruzioni, vedere [Creare uno spazio dei nomi di Hub eventi](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span><span class="sxs-lookup"><span data-stu-id="77373-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="77373-112">Verificare che l'account archivio Data Lake hello e dello spazio dei nomi di hello hub eventi si trovano in hello stessa sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="77373-112">Make sure hello Data Lake Store account and hello Event Hubs namespace are in hello same Azure subscription.</span></span>


## <a name="assign-permissions-tooevent-hubs"></a><span data-ttu-id="77373-113">Assegnare autorizzazioni tooEvent hub</span><span class="sxs-lookup"><span data-stu-id="77373-113">Assign permissions tooEvent Hubs</span></span>

<span data-ttu-id="77373-114">In questa sezione è creare una cartella all'interno di account hello in cui si desidera dati hello toocapture dagli hub eventi.</span><span class="sxs-lookup"><span data-stu-id="77373-114">In this section, you create a folder within hello account where you want toocapture hello data from Event Hubs.</span></span> <span data-ttu-id="77373-115">È anche assegnare autorizzazioni tooEvent hub in modo da consentire la scrittura di dati in un account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="77373-115">You also assign permissions tooEvent Hubs so that it can write data into a Data Lake Store account.</span></span> 

1. <span data-ttu-id="77373-116">Aprire l'account archivio Data Lake di hello in cui si desidera che i dati toocapture dagli hub eventi e quindi fare clic su **Esplora dati**.</span><span class="sxs-lookup"><span data-stu-id="77373-116">Open hello Data Lake Store account where you want toocapture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="77373-117">![Esplora dati di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Esplora dati di Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="77373-117">![Data Lake Store data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span></span>

2.  <span data-ttu-id="77373-118">Fare clic su **nuova cartella** e quindi immettere un nome per la cartella in cui i dati di hello toocapture.</span><span class="sxs-lookup"><span data-stu-id="77373-118">Click **New Folder** and then enter a name for folder where you want toocapture hello data.</span></span>

    <span data-ttu-id="77373-119">![Creare una nuova cartella in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Creare una nuova cartella in Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="77373-119">![Create a new folder in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span></span>

3. <span data-ttu-id="77373-120">Assegnare autorizzazioni nella directory principale di hello di hello archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="77373-120">Assign permissions at hello root of hello Data Lake Store.</span></span> 

    <span data-ttu-id="77373-121">a.</span><span class="sxs-lookup"><span data-stu-id="77373-121">a.</span></span> <span data-ttu-id="77373-122">Fare clic su **Esplora dati**selezionare hello radice di hello account archivio Data Lake e quindi fare clic su **accesso**.</span><span class="sxs-lookup"><span data-stu-id="77373-122">Click **Data Explorer**, select hello root of hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="77373-123">![Assegnare le autorizzazioni per la radice di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assegnare le autorizzazioni per la radice di Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="77373-123">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="77373-124">b.</span><span class="sxs-lookup"><span data-stu-id="77373-124">b.</span></span> <span data-ttu-id="77373-125">In **Accesso** fare clic su **Aggiungi**, fare clic su **Selezionare l'utente o il gruppo** e quindi cercare `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="77373-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="77373-126">![Assegnare le autorizzazioni per la radice di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assegnare le autorizzazioni per la radice di Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="77373-126">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span></span>
    
    <span data-ttu-id="77373-127">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="77373-127">Click **Select**.</span></span>

    <span data-ttu-id="77373-128">c.</span><span class="sxs-lookup"><span data-stu-id="77373-128">c.</span></span> <span data-ttu-id="77373-129">In **Assegna autorizzazioni** fare clic su **Selezionare le autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="77373-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="77373-130">Impostare **autorizzazioni** troppo**Execute**.</span><span class="sxs-lookup"><span data-stu-id="77373-130">Set **Permissions** too**Execute**.</span></span> <span data-ttu-id="77373-131">Impostare **aggiungere** troppo**questa cartella e tutti gli elementi figlio**.</span><span class="sxs-lookup"><span data-stu-id="77373-131">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="77373-132">Impostare **aggiungere come** troppo**una voce di autorizzazione di accesso e una voce di autorizzazione predefinito**.</span><span class="sxs-lookup"><span data-stu-id="77373-132">Set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="77373-133">![Assegnare le autorizzazioni per la radice di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assegnare le autorizzazioni per la radice di Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="77373-133">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="77373-134">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="77373-134">Click **OK**.</span></span>

4. <span data-ttu-id="77373-135">Assegnare le autorizzazioni per la cartella di hello account archivio Data Lake in cui si desidera toocapture dati.</span><span class="sxs-lookup"><span data-stu-id="77373-135">Assign permissions for hello folder under Data Lake Store account where you want toocapture data.</span></span>

    <span data-ttu-id="77373-136">a.</span><span class="sxs-lookup"><span data-stu-id="77373-136">a.</span></span> <span data-ttu-id="77373-137">Fare clic su **Esplora dati**, selezionare la cartella hello hello account archivio Data Lake e quindi fare clic su **accesso**.</span><span class="sxs-lookup"><span data-stu-id="77373-137">Click **Data Explorer**, select hello folder in hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="77373-138">![Assegnare le autorizzazioni per la cartella di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assegnare le autorizzazioni per la cartella di Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="77373-138">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span></span>

    <span data-ttu-id="77373-139">b.</span><span class="sxs-lookup"><span data-stu-id="77373-139">b.</span></span> <span data-ttu-id="77373-140">In **Accesso** fare clic su **Aggiungi**, fare clic su **Selezionare l'utente o il gruppo** e quindi cercare `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="77373-140">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="77373-141">![Assegnare le autorizzazioni per la cartella di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assegnare le autorizzazioni per la cartella di Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="77373-141">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="77373-142">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="77373-142">Click **Select**.</span></span>

    <span data-ttu-id="77373-143">c.</span><span class="sxs-lookup"><span data-stu-id="77373-143">c.</span></span> <span data-ttu-id="77373-144">In **Assegna autorizzazioni** fare clic su **Selezionare le autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="77373-144">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="77373-145">Impostare **autorizzazioni** troppo**lettura, scrittura,** e **Execute**.</span><span class="sxs-lookup"><span data-stu-id="77373-145">Set **Permissions** too**Read, Write,** and **Execute**.</span></span> <span data-ttu-id="77373-146">Impostare **aggiungere** troppo**questa cartella e tutti gli elementi figlio**.</span><span class="sxs-lookup"><span data-stu-id="77373-146">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="77373-147">Infine, impostare **aggiungere come** troppo**una voce di autorizzazione di accesso e una voce di autorizzazione predefinito**.</span><span class="sxs-lookup"><span data-stu-id="77373-147">Finally, set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="77373-148">![Assegnare le autorizzazioni per la cartella di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assegnare le autorizzazioni per la cartella di Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="77373-148">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="77373-149">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="77373-149">Click **OK**.</span></span> 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a><span data-ttu-id="77373-150">Configurare l'archivio di hub eventi toocapture dati tooData Lake</span><span class="sxs-lookup"><span data-stu-id="77373-150">Configure Event Hubs toocapture data tooData Lake Store</span></span>

<span data-ttu-id="77373-151">In questa sezione si crea un hub eventi in uno spazio dei nomi di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="77373-151">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="77373-152">È inoltre possibile configurare hello Hub eventi toocapture dati tooan account archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="77373-152">You also configure hello Event Hub toocapture data tooan Azure Data Lake Store account.</span></span> <span data-ttu-id="77373-153">Questa sezione presuppone che sia già stato creato uno spazio dei nomi di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="77373-153">This section assumes that you have already created an Event Hubs namespace.</span></span>

2. <span data-ttu-id="77373-154">Da hello **Panoramica** riquadro dello spazio dei nomi di hub eventi hello, fare clic su **+ Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="77373-154">From hello **Overview** pane of hello Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="77373-155">![Creare un hub eventi](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Creare un hub eventi")</span><span class="sxs-lookup"><span data-stu-id="77373-155">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

3. <span data-ttu-id="77373-156">Fornire seguente hello valori tooconfigure hub eventi toocapture tooData Lake archivio.</span><span class="sxs-lookup"><span data-stu-id="77373-156">Provide hello following values tooconfigure Event Hubs toocapture data tooData Lake Store.</span></span>

    <span data-ttu-id="77373-157">![Creare un hub eventi](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Creare un hub eventi")</span><span class="sxs-lookup"><span data-stu-id="77373-157">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="77373-158">a.</span><span class="sxs-lookup"><span data-stu-id="77373-158">a.</span></span> <span data-ttu-id="77373-159">Specificare un nome per hello Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="77373-159">Provide a name for hello Event Hub.</span></span>
    
    <span data-ttu-id="77373-160">b.</span><span class="sxs-lookup"><span data-stu-id="77373-160">b.</span></span> <span data-ttu-id="77373-161">Per questa esercitazione, impostare **il numero di partizioni** e **memorizzazione dei messaggi** toohello predefinite.</span><span class="sxs-lookup"><span data-stu-id="77373-161">For this tutorial, set **Partition Count** and **Message Retention** toohello default values.</span></span>
    
    <span data-ttu-id="77373-162">c.</span><span class="sxs-lookup"><span data-stu-id="77373-162">c.</span></span> <span data-ttu-id="77373-163">Impostare **acquisire** troppo**su**.</span><span class="sxs-lookup"><span data-stu-id="77373-163">Set **Capture** too**On**.</span></span> <span data-ttu-id="77373-164">Set hello **finestra temporale** (frequenza toocapture) e **dimensioni finestra** (toocapture dimensioni dati).</span><span class="sxs-lookup"><span data-stu-id="77373-164">Set hello **Time Window** (how frequently toocapture) and **Size Window** (data size toocapture).</span></span> 
    
    <span data-ttu-id="77373-165">d.</span><span class="sxs-lookup"><span data-stu-id="77373-165">d.</span></span> <span data-ttu-id="77373-166">Per **acquisire Provider**selezionare **archivio Azure Data Lake** e selezionare hello hello archivio Data Lake creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="77373-166">For **Capture Provider**, select **Azure Data Lake Store** and hello select hello Data Lake Store you created earlier.</span></span> <span data-ttu-id="77373-167">Per **Data Lake percorso**, immettere il nome di hello della cartella di hello è stato creato in hello account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="77373-167">For **Data Lake Path**, enter hello name of hello folder you created in hello Data Lake Store account.</span></span> <span data-ttu-id="77373-168">È necessario solo cartella toohello di tooprovide hello percorso relativo.</span><span class="sxs-lookup"><span data-stu-id="77373-168">You only need tooprovide hello relative path toohello folder.</span></span>

    <span data-ttu-id="77373-169">e.</span><span class="sxs-lookup"><span data-stu-id="77373-169">e.</span></span> <span data-ttu-id="77373-170">Lasciare hello **formati del nome file acquisizione esempio** toohello predefinita.</span><span class="sxs-lookup"><span data-stu-id="77373-170">Leave hello **Sample capture file name formats** toohello default value.</span></span> <span data-ttu-id="77373-171">Questa opzione determina una struttura di cartelle hello che viene creato nella cartella di acquisizione hello.</span><span class="sxs-lookup"><span data-stu-id="77373-171">This option governs hello folder structure that is created under hello capture folder.</span></span>

    <span data-ttu-id="77373-172">f.</span><span class="sxs-lookup"><span data-stu-id="77373-172">f.</span></span> <span data-ttu-id="77373-173">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="77373-173">Click **Create**.</span></span>

## <a name="test-hello-setup"></a><span data-ttu-id="77373-174">Programma di installazione di prova hello</span><span class="sxs-lookup"><span data-stu-id="77373-174">Test hello setup</span></span>

<span data-ttu-id="77373-175">È ora possibile testare la soluzione hello inviando dati toohello Hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="77373-175">You can now test hello solution by sending data toohello Azure Event Hub.</span></span> <span data-ttu-id="77373-176">Seguire le istruzioni di hello in [inviare eventi di hub di eventi tooAzure](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span><span class="sxs-lookup"><span data-stu-id="77373-176">Follow hello instructions at [Send events tooAzure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="77373-177">Dopo aver iniziato l'invio dei dati di hello, vedrai dati hello riflessi in archivio Data Lake con struttura di cartelle hello specificato.</span><span class="sxs-lookup"><span data-stu-id="77373-177">Once you start sending hello data, you see hello data reflected in Data Lake Store using hello folder structure you specified.</span></span> <span data-ttu-id="77373-178">Ad esempio, è visualizzata una struttura di cartelle, come illustrato nella seguente schermata, nell'archivio Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="77373-178">For example, you see a folder structure, as shown in hello following screenshot, in your Data Lake Store.</span></span>

<span data-ttu-id="77373-179">![Dati dell'hub eventi di esempio in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Dati dell'hub eventi di esempio in Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="77373-179">![Sample EventHub data in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span></span>

> [!NOTE]
> <span data-ttu-id="77373-180">Anche se non si dispone di messaggi in arrivo nell'hub eventi, gli hub di eventi scrive file vuoti con solo le intestazioni di hello in hello account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="77373-180">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just hello headers into hello Data Lake Store account.</span></span> <span data-ttu-id="77373-181">Hello file vengono scritti in hello stesso intervallo di tempo specificato durante la creazione di hub eventi hello.</span><span class="sxs-lookup"><span data-stu-id="77373-181">hello files are written at hello same time interval that you provided while creating hello Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-store"></a><span data-ttu-id="77373-182">Analizzare i dati in Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="77373-182">Analyze data in Data Lake Store</span></span>

<span data-ttu-id="77373-183">Una volta dati hello in archivio Data Lake, è possibile eseguire i processi analitici tooprocess e elaborare dati hello.</span><span class="sxs-lookup"><span data-stu-id="77373-183">Once hello data is in Data Lake Store, you can run analytical jobs tooprocess and crunch hello data.</span></span> <span data-ttu-id="77373-184">Vedere [USQL Avro esempio](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) sulla toodo questo usando Azure Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="77373-184">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how toodo this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="77373-185">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="77373-185">See also</span></span>
* [<span data-ttu-id="77373-186">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="77373-186">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="77373-187">Copiare i dati da un archivio Azure archiviazione BLOB tooData Lake</span><span class="sxs-lookup"><span data-stu-id="77373-187">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)

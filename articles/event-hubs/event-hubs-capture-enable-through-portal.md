---
title: abilitare aaaAzure acquisire gli hub di eventi tramite il portale | Documenti Microsoft
description: "Abilitare funzionalità hello acquisire gli hub di eventi utilizzando hello portale di Azure."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a><span data-ttu-id="792df-103">Abilitare gli hub di eventi Capture utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="792df-103">Enable Event Hubs Capture using hello Azure portal</span></span>

<span data-ttu-id="792df-104">È possibile configurare l'acquisizione al momento della creazione di hello evento hub utilizzando hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="792df-104">You can configure Capture at hello event hub creation time using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="792df-105">È possibile entrambi tooan di dati di acquisizione hello Azure [nell'archiviazione Blob](https://azure.microsoft.com/services/storage/blobs/) contenitore o tooan [archivio Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) account.</span><span class="sxs-lookup"><span data-stu-id="792df-105">You can either capture hello data tooan Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span></span>

## <a name="capture-data-tooan-azure-storage-account"></a><span data-ttu-id="792df-106">Account di archiviazione di Azure tooan dati di acquisizione</span><span class="sxs-lookup"><span data-stu-id="792df-106">Capture data tooan Azure Storage account</span></span>  

<span data-ttu-id="792df-107">Quando si crea un hub eventi, è possibile abilitare l'acquisizione facendo hello **su** pulsante hello **creare Hub eventi** portale pannello.</span><span class="sxs-lookup"><span data-stu-id="792df-107">When you create an event hub, you can enable Capture by clicking hello **On** button in hello **Create Event Hub** portal blade.</span></span> <span data-ttu-id="792df-108">Specificare quindi un Account di archiviazione e un contenitore, fare clic su **di archiviazione di Azure** in hello **acquisire Provider** casella.</span><span class="sxs-lookup"><span data-stu-id="792df-108">You then specify a Storage Account and container by clicking **Azure Storage** in hello **Capture Provider** box.</span></span> <span data-ttu-id="792df-109">Poiché gli hub di eventi acquisire utilizza l'autenticazione di service to service con l'archiviazione, non è necessario toospecify una stringa di connessione di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="792df-109">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need toospecify a storage connection string.</span></span> <span data-ttu-id="792df-110">selezione della risorsa Hello URI della risorsa hello dell'account di archiviazione viene selezionato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="792df-110">hello resource picker selects hello resource URI for your storage account automatically.</span></span> <span data-ttu-id="792df-111">Se si usa Azure Resource Manager, è necessario specificare questo URI in modo esplicito come stringa.</span><span class="sxs-lookup"><span data-stu-id="792df-111">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span></span>

<span data-ttu-id="792df-112">intervallo di tempo predefinito Hello è 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="792df-112">hello default time window is 5 minutes.</span></span> <span data-ttu-id="792df-113">valore minimo di Hello è 1, hello massimo 15.</span><span class="sxs-lookup"><span data-stu-id="792df-113">hello minimum value is 1, hello maximum 15.</span></span> <span data-ttu-id="792df-114">Hello **dimensioni** finestra dispone di un intervallo di 10-500 MB.</span><span class="sxs-lookup"><span data-stu-id="792df-114">hello **Size** window has a range of 10-500 MB.</span></span>

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a><span data-ttu-id="792df-115">Account archivio Azure Data Lake tooan di dati di acquisizione</span><span class="sxs-lookup"><span data-stu-id="792df-115">Capture data tooan Azure Data Lake Store account</span></span>

<span data-ttu-id="792df-116">toocapture dati tooAzure archivio Data Lake, creare un account archivio Data Lake e un hub eventi:</span><span class="sxs-lookup"><span data-stu-id="792df-116">toocapture data tooAzure Data Lake Store, you create a Data Lake Store account, and an event hub:</span></span>

### <a name="create-an-azure-data-lake-store-account-and-folders"></a><span data-ttu-id="792df-117">Creare un account Azure Data Lake Store e le cartelle</span><span class="sxs-lookup"><span data-stu-id="792df-117">Create an Azure Data Lake Store account and folders</span></span>

1. <span data-ttu-id="792df-118">Creare un account archivio Data Lake, attenendosi alle istruzioni hello in [introduzione archivio Azure Data Lake tramite il portale di Azure hello](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="792df-118">Create a Data Lake Store account, following hello instructions in [Get started with Azure Data Lake Store using hello Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span> 
2. <span data-ttu-id="792df-119">Creare una cartella con questo account, attenendosi alle istruzioni hello in hello [creare cartelle nell'account archivio Azure Data Lake](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) sezione.</span><span class="sxs-lookup"><span data-stu-id="792df-119">Create a folder under this account, following hello instructions in hello [Create folders in Azure Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.</span></span>
3. <span data-ttu-id="792df-120">Nel Pannello di account archivio Data Lake hello, fare clic su **Esplora dati**.</span><span class="sxs-lookup"><span data-stu-id="792df-120">In hello Data Lake Store account blade, click **Data Explorer**.</span></span>
4. <span data-ttu-id="792df-121">Fare clic su **Accesso**.</span><span class="sxs-lookup"><span data-stu-id="792df-121">Click **Access**.</span></span>
5. <span data-ttu-id="792df-122">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="792df-122">Click **Add**.</span></span>
6. <span data-ttu-id="792df-123">In hello **ricerca per nome o indirizzo email** digitare **Microsoft.EventHubs** e quindi selezionare questa opzione.</span><span class="sxs-lookup"><span data-stu-id="792df-123">In hello **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span> 
7. <span data-ttu-id="792df-124">Hello **autorizzazioni** verrà visualizzata la scheda.</span><span class="sxs-lookup"><span data-stu-id="792df-124">hello **Permissions** tab appears.</span></span> <span data-ttu-id="792df-125">Impostare le autorizzazioni di hello, come illustrato nella seguente illustrazione hello:</span><span class="sxs-lookup"><span data-stu-id="792df-125">Set hello permissions as shown in hello following figure:</span></span>

    ![][6]

8. <span data-ttu-id="792df-126">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="792df-126">Click **OK**.</span></span>
9. <span data-ttu-id="792df-127">A questo punto, è possibile creare una cartella nella cartella radice hello visualizzando la cartella di destinazione toohello e facendo clic sul nome della cartella hello.</span><span class="sxs-lookup"><span data-stu-id="792df-127">Now, create a folder in hello root folder by browsing toohello target folder and clicking on hello folder name.</span></span>
10. <span data-ttu-id="792df-128">Fare clic su **Accesso**.</span><span class="sxs-lookup"><span data-stu-id="792df-128">Click **Access**.</span></span>
11. <span data-ttu-id="792df-129">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="792df-129">Click **Add**.</span></span>
12. <span data-ttu-id="792df-130">In hello **ricerca per nome o indirizzo email** digitare **Microsoft.EventHubs** e quindi selezionare questa opzione.</span><span class="sxs-lookup"><span data-stu-id="792df-130">In hello **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span>
13. <span data-ttu-id="792df-131">Hello **autorizzazioni** verrà nuovamente visualizzata la scheda.</span><span class="sxs-lookup"><span data-stu-id="792df-131">hello **Permissions** tab appears again.</span></span> <span data-ttu-id="792df-132">Impostare le autorizzazioni di hello, come illustrato nella seguente illustrazione hello:</span><span class="sxs-lookup"><span data-stu-id="792df-132">Set hello permissions as shown in hello following figure:</span></span>

    ![][5]

### <a name="create-an-event-hub"></a><span data-ttu-id="792df-133">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="792df-133">Create an event hub</span></span>

1. <span data-ttu-id="792df-134">Hub eventi hello deve essere in hello stessa sottoscrizione Azure hello archivio Azure Data Lake appena creato.</span><span class="sxs-lookup"><span data-stu-id="792df-134">Note that hello event hub must be in hello same Azure subscription as hello Azure Data Lake Store you just created.</span></span> <span data-ttu-id="792df-135">Hub di eventi hello create, fare clic su hello **su** pulsante sotto **acquisire** in hello **creare Hub eventi** portale pannello.</span><span class="sxs-lookup"><span data-stu-id="792df-135">Create hello event hub, clicking hello **On** button under **Capture** in hello **Create Event Hub** portal blade.</span></span> 
2. <span data-ttu-id="792df-136">In hello **creare Hub eventi** portale pannello seleziona **archivio Azure Data Lake** da hello **acquisire Provider** casella.</span><span class="sxs-lookup"><span data-stu-id="792df-136">In hello **Create Event Hub** portal blade, select **Azure Data Lake Store** from hello **Capture Provider** box.</span></span>
3. <span data-ttu-id="792df-137">In **archivio Data Lake di selezionare**, specificare l'account archivio Data Lake è stato creato in precedenza e hello hello **Data Lake percorso** immettere hello toohello dati cartella creata.</span><span class="sxs-lookup"><span data-stu-id="792df-137">In **Select Data Lake Store**, specify hello Data Lake Store account you created previously, and in hello **Data Lake Path** field, enter hello path toohello data folder you created.</span></span>

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a><span data-ttu-id="792df-138">Aggiungere o configurare l'acquisizione in un hub eventi esistente</span><span class="sxs-lookup"><span data-stu-id="792df-138">Add or configure Capture on an existing event hub</span></span>

<span data-ttu-id="792df-139">È possibile configurare l'acquisizione in hub eventi esistenti che si trovano in spazi dei nomi di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="792df-139">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span></span> <span data-ttu-id="792df-140">tooenable acquisire in un hub eventi, o esistente toochange le impostazioni di acquisizione, fare clic su hello tooload dello spazio dei nomi di hello **Essentials** pannello, quindi fare clic su hub di eventi hello per cui si desidera tooenable o modifica l'impostazione di acquisizione hello.</span><span class="sxs-lookup"><span data-stu-id="792df-140">tooenable Capture on an existing event hub, or toochange your Capture settings, click hello namespace tooload hello **Essentials** blade, then click hello event hub for which you want tooenable or change hello Capture setting.</span></span> <span data-ttu-id="792df-141">Infine, fare clic su hello **proprietà** sezione di hello aprire Pannello e quindi modificare le impostazioni di acquisizione hello, come mostrato nel seguente figure hello:</span><span class="sxs-lookup"><span data-stu-id="792df-141">Finally, click hello **Properties** section of hello open blade and then edit hello Capture settings, as shown in hello following figures:</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="792df-142">Archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="792df-142">Azure Blob Storage</span></span>

![][2]

### <a name="azure-data-lake-store"></a><span data-ttu-id="792df-143">Archivio Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="792df-143">Azure Data Lake Store</span></span>

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a><span data-ttu-id="792df-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="792df-144">Next steps</span></span>

<span data-ttu-id="792df-145">È anche possibile configurare Acquisizione di Hub eventi usando i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="792df-145">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span></span> <span data-ttu-id="792df-146">Per altre informazioni, vedere [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md) (Abilitare Acquisizione usando un modello di Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="792df-146">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span></span>

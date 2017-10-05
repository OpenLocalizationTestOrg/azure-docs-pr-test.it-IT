---
title: Abilitazione di Acquisizione di Hub eventi di Azure tramite il portale | Microsoft Docs
description: "Abilitare la funzionalità Acquisizione di Hub eventi usando il portale di Azure."
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
ms.openlocfilehash: 0cbf45dce922647f2996f929d2c7cf885a2f4db4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="enable-event-hubs-capture-using-the-azure-portal"></a><span data-ttu-id="49718-103">Abilitare Acquisizione di Hub eventi usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="49718-103">Enable Event Hubs Capture using the Azure portal</span></span>

<span data-ttu-id="49718-104">È possibile configurare Acquisizione al momento della creazione dell'hub eventi usando il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="49718-104">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="49718-105">È possibile acquisire i dati in un contenitore di [archiviazione BLOB](https://azure.microsoft.com/services/storage/blobs/) di Azure o in un account [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="49718-105">You can either capture the data to an Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or to an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span></span>

## <a name="capture-data-to-an-azure-storage-account"></a><span data-ttu-id="49718-106">Acquisire i dati in un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="49718-106">Capture data to an Azure Storage account</span></span>  

<span data-ttu-id="49718-107">Quando si crea un hub eventi, è possibile abilitare l'acquisizione facendo il **su** pulsante il **creare Hub eventi** portale pannello.</span><span class="sxs-lookup"><span data-stu-id="49718-107">When you create an event hub, you can enable Capture by clicking the **On** button in the **Create Event Hub** portal blade.</span></span> <span data-ttu-id="49718-108">È quindi possibile specificare un account e un contenitore di archiviazione facendo clic su **Archiviazione di Azure** nella casella **Provider di acquisizione**.</span><span class="sxs-lookup"><span data-stu-id="49718-108">You then specify a Storage Account and container by clicking **Azure Storage** in the **Capture Provider** box.</span></span> <span data-ttu-id="49718-109">Poiché Acquisizione di Hub eventi usa l'autenticazione da servizio a servizio con la risorsa di archiviazione, non è necessario specificare una stringa di connessione di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="49718-109">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need to specify a storage connection string.</span></span> <span data-ttu-id="49718-110">Il selettore risorse seleziona automaticamente l'URI della risorsa per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="49718-110">The resource picker selects the resource URI for your storage account automatically.</span></span> <span data-ttu-id="49718-111">Se si usa Azure Resource Manager, è necessario specificare questo URI in modo esplicito come stringa.</span><span class="sxs-lookup"><span data-stu-id="49718-111">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span></span>

<span data-ttu-id="49718-112">L'intervallo di tempo predefinito è di 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="49718-112">The default time window is 5 minutes.</span></span> <span data-ttu-id="49718-113">Il valore minimo è 1, quello massimo 15.</span><span class="sxs-lookup"><span data-stu-id="49718-113">The minimum value is 1, the maximum 15.</span></span> <span data-ttu-id="49718-114">La finestra **Dimensione** ha un intervallo compreso tra 10 e 500 MB.</span><span class="sxs-lookup"><span data-stu-id="49718-114">The **Size** window has a range of 10-500 MB.</span></span>

![][1]

## <a name="capture-data-to-an-azure-data-lake-store-account"></a><span data-ttu-id="49718-115">Acquisire i dati un account Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="49718-115">Capture data to an Azure Data Lake Store account</span></span>

<span data-ttu-id="49718-116">Per acquisire i dati in Azure Data Lake Store, si creano un account Data Lake Store e un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="49718-116">To capture data to Azure Data Lake Store, you create a Data Lake Store account, and an event hub:</span></span>

### <a name="create-an-azure-data-lake-store-account-and-folders"></a><span data-ttu-id="49718-117">Creare un account Azure Data Lake Store e le cartelle</span><span class="sxs-lookup"><span data-stu-id="49718-117">Create an Azure Data Lake Store account and folders</span></span>

1. <span data-ttu-id="49718-118">Creare un account Data Lake Store seguendo le istruzioni riportate in [Introduzione ad Azure Data Lake Store con il portale di Azure](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="49718-118">Create a Data Lake Store account, following the instructions in [Get started with Azure Data Lake Store using the Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span> 
2. <span data-ttu-id="49718-119">Creare una cartella in tale account seguendo le istruzioni riportate nella sezione relativa alla [creazione di cartelle nell'account Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md#createfolder).</span><span class="sxs-lookup"><span data-stu-id="49718-119">Create a folder under this account, following the instructions in the [Create folders in Azure Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.</span></span>
3. <span data-ttu-id="49718-120">Nel pannello account archivio Data Lake, fare clic su **Esplora dati**.</span><span class="sxs-lookup"><span data-stu-id="49718-120">In the Data Lake Store account blade, click **Data Explorer**.</span></span>
4. <span data-ttu-id="49718-121">Fare clic su **Accesso**.</span><span class="sxs-lookup"><span data-stu-id="49718-121">Click **Access**.</span></span>
5. <span data-ttu-id="49718-122">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="49718-122">Click **Add**.</span></span>
6. <span data-ttu-id="49718-123">Nella casella **Cerca in base al nome o all'indirizzo di posta elettronica** digitare **Microsoft.EventHubs** e quindi selezionare questa opzione.</span><span class="sxs-lookup"><span data-stu-id="49718-123">In the **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span> 
7. <span data-ttu-id="49718-124">Verrà visualizzata la scheda **Autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="49718-124">The **Permissions** tab appears.</span></span> <span data-ttu-id="49718-125">Impostare le autorizzazioni come illustrato nella figura seguente:</span><span class="sxs-lookup"><span data-stu-id="49718-125">Set the permissions as shown in the following figure:</span></span>

    ![][6]

8. <span data-ttu-id="49718-126">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="49718-126">Click **OK**.</span></span>
9. <span data-ttu-id="49718-127">Creare quindi una cartella nella cartella radice passando alla cartella di destinazione e facendo clic sul nome della cartella.</span><span class="sxs-lookup"><span data-stu-id="49718-127">Now, create a folder in the root folder by browsing to the target folder and clicking on the folder name.</span></span>
10. <span data-ttu-id="49718-128">Fare clic su **Accesso**.</span><span class="sxs-lookup"><span data-stu-id="49718-128">Click **Access**.</span></span>
11. <span data-ttu-id="49718-129">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="49718-129">Click **Add**.</span></span>
12. <span data-ttu-id="49718-130">Nella casella **Cerca in base al nome o all'indirizzo di posta elettronica** digitare **Microsoft.EventHubs** e quindi selezionare questa opzione.</span><span class="sxs-lookup"><span data-stu-id="49718-130">In the **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span>
13. <span data-ttu-id="49718-131">Verrà visualizzata di nuovo la scheda **Autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="49718-131">The **Permissions** tab appears again.</span></span> <span data-ttu-id="49718-132">Impostare le autorizzazioni come illustrato nella figura seguente:</span><span class="sxs-lookup"><span data-stu-id="49718-132">Set the permissions as shown in the following figure:</span></span>

    ![][5]

### <a name="create-an-event-hub"></a><span data-ttu-id="49718-133">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="49718-133">Create an event hub</span></span>

1. <span data-ttu-id="49718-134">Si noti che l'hub eventi deve trovarsi nella stessa sottoscrizione di Azure dell'account Azure Data Lake Store appena creato.</span><span class="sxs-lookup"><span data-stu-id="49718-134">Note that the event hub must be in the same Azure subscription as the Azure Data Lake Store you just created.</span></span> <span data-ttu-id="49718-135">Creazione dell'hub di eventi, fare clic sul **su** pulsante sotto **acquisire** nel **creare Hub eventi** portale pannello.</span><span class="sxs-lookup"><span data-stu-id="49718-135">Create the event hub, clicking the **On** button under **Capture** in the **Create Event Hub** portal blade.</span></span> 
2. <span data-ttu-id="49718-136">Nel **creare Hub eventi** portale pannello seleziona **archivio Azure Data Lake** dal **acquisire Provider** casella.</span><span class="sxs-lookup"><span data-stu-id="49718-136">In the **Create Event Hub** portal blade, select **Azure Data Lake Store** from the **Capture Provider** box.</span></span>
3. <span data-ttu-id="49718-137">In **Seleziona Data Lake Store** specificare l'account Data Lake Store creato in precedenza e nel campo **Percorso Data Lake** immettere il percorso della cartella dati creata.</span><span class="sxs-lookup"><span data-stu-id="49718-137">In **Select Data Lake Store**, specify the Data Lake Store account you created previously, and in the **Data Lake Path** field, enter the path to the data folder you created.</span></span>

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a><span data-ttu-id="49718-138">Aggiungere o configurare l'acquisizione in un hub eventi esistente</span><span class="sxs-lookup"><span data-stu-id="49718-138">Add or configure Capture on an existing event hub</span></span>

<span data-ttu-id="49718-139">È possibile configurare l'acquisizione in hub eventi esistenti che si trovano in spazi dei nomi di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="49718-139">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span></span> <span data-ttu-id="49718-140">Per abilitare Acquisizione in un hub eventi esistente o per modificarne le impostazioni, fare clic sullo spazio dei nomi per caricare il pannello **Informazioni di base**, quindi fare clic sull'hub eventi per cui si vuole abilitare o modificare l'impostazione di Acquisizione.</span><span class="sxs-lookup"><span data-stu-id="49718-140">To enable Capture on an existing event hub, or to change your Capture settings, click the namespace to load the **Essentials** blade, then click the event hub for which you want to enable or change the Capture setting.</span></span> <span data-ttu-id="49718-141">Infine, fare clic su di **proprietà** sezione del pannello aperto e quindi modificare le impostazioni di acquisizione, come illustrato nella figura riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="49718-141">Finally, click the **Properties** section of the open blade and then edit the Capture settings, as shown in the following figures:</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="49718-142">Archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="49718-142">Azure Blob Storage</span></span>

![][2]

### <a name="azure-data-lake-store"></a><span data-ttu-id="49718-143">Archivio Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="49718-143">Azure Data Lake Store</span></span>

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a><span data-ttu-id="49718-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="49718-144">Next steps</span></span>

<span data-ttu-id="49718-145">È anche possibile configurare Acquisizione di Hub eventi usando i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="49718-145">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span></span> <span data-ttu-id="49718-146">Per altre informazioni, vedere [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md) (Abilitare Acquisizione usando un modello di Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="49718-146">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span></span>

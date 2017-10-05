---
title: Aggiungere il connettore di archiviazione BLOB di Azure alle app per la logica | Microsoft Docs
description: Iniziare a configurare il connettore di archiviazione BLOB di Azure in un'app per la logica
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: bc7908868828bd1628633cf9e57f8c44f8000827
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-blob-storage-connector-in-a-logic-app"></a><span data-ttu-id="ec57d-103">Usare il connettore di archiviazione BLOB di Azure in un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="ec57d-103">Use the Azure blob storage connector in a logic app</span></span>
<span data-ttu-id="ec57d-104">Usare il connettore di archiviazione BLOB di Azure per caricare, aggiornare, ottenere ed eliminare i BLOB nell'account di archiviazione, il tutto all'interno di un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="ec57d-104">Use the Azure Blob storage connector to upload, update, get, and delete blobs in your storage account, all within a logic app.</span></span>  

<span data-ttu-id="ec57d-105">Con Archiviazione BLOB di Azure:</span><span class="sxs-lookup"><span data-stu-id="ec57d-105">With Azure blob storage, you:</span></span>

* <span data-ttu-id="ec57d-106">Il flusso di lavoro si crea caricando nuovi progetti o recuperando file aggiornati di recente.</span><span class="sxs-lookup"><span data-stu-id="ec57d-106">Build your workflow by uploading new projects, or getting files that have been recently updated.</span></span>
* <span data-ttu-id="ec57d-107">Le azioni consentono di ottenere i metadati del file, eliminare un file, copiare file e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="ec57d-107">Use actions to get file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="ec57d-108">Ad esempio, quando viene aggiornato uno strumento in un sito Web di Azure (trigger), viene aggiornato un file nell'archivio BLOB (azione).</span><span class="sxs-lookup"><span data-stu-id="ec57d-108">For example, when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="ec57d-109">Questo argomento illustra come usare il connettore di archiviazione BLOB in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="ec57d-109">This topic shows you how to use the blob storage connector in a logic app.</span></span>

<span data-ttu-id="ec57d-110">Per altre informazioni sulle app per la logica, vedere [Cosa sono le app per la logica](../logic-apps/logic-apps-what-are-logic-apps.md) e [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ec57d-110">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="ec57d-111">Per altre informazioni sulle app per la logica, vedere [Cosa sono le app per la logica](../logic-apps/logic-apps-what-are-logic-apps.md) e [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ec57d-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-blob-storage"></a><span data-ttu-id="ec57d-112">Connettersi all'archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="ec57d-112">Connect to Azure blob storage</span></span>
<span data-ttu-id="ec57d-113">Prima che l'app per la logica possa accedere a qualsiasi servizio, è necessario creare una *connessione* al servizio.</span><span class="sxs-lookup"><span data-stu-id="ec57d-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="ec57d-114">Una connessione fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="ec57d-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="ec57d-115">Ad esempio, per connettersi a un account di archiviazione, si crea prima una *connessione* all'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="ec57d-115">For example, to connect to a storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="ec57d-116">Per creare una connessione, immettere le credenziali usate normalmente per accedere al servizio a cui connettersi.</span><span class="sxs-lookup"><span data-stu-id="ec57d-116">To create a connection, enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="ec57d-117">Con Archiviazione di Azure immettere quindi le credenziali dell'account di archiviazione per creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="ec57d-117">So with Azure storage, enter the credentials to your storage account to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="ec57d-118">Creare la connessione</span><span class="sxs-lookup"><span data-stu-id="ec57d-118">Create the connection</span></span>
> [!INCLUDE [Create a connection to Azure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a><span data-ttu-id="ec57d-119">Usare un trigger</span><span class="sxs-lookup"><span data-stu-id="ec57d-119">Use a trigger</span></span>
<span data-ttu-id="ec57d-120">Questo connettore non include trigger.</span><span class="sxs-lookup"><span data-stu-id="ec57d-120">This connector does not have any triggers.</span></span> <span data-ttu-id="ec57d-121">Usare altri trigger per avviare l'app per la logica, come un trigger di ricorrenza, un trigger Webhook HTTP, i trigger disponibili con altri connettori e altri ancora.</span><span class="sxs-lookup"><span data-stu-id="ec57d-121">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="ec57d-122">[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md) illustra un esempio.</span><span class="sxs-lookup"><span data-stu-id="ec57d-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="ec57d-123">Usare un'azione</span><span class="sxs-lookup"><span data-stu-id="ec57d-123">Use an action</span></span>
<span data-ttu-id="ec57d-124">Un'azione è un'operazione eseguita dal flusso di lavoro e definita in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="ec57d-124">An action is an operation carried out by the workflow defined in a logic app.</span></span>

1. <span data-ttu-id="ec57d-125">Selezionare il segno più.</span><span class="sxs-lookup"><span data-stu-id="ec57d-125">Select the plus sign.</span></span> <span data-ttu-id="ec57d-126">Sono disponibili varie opzioni: **Aggiungi un'azione**, **Aggiungi una condizione** e le opzioni in **Altro**.</span><span class="sxs-lookup"><span data-stu-id="ec57d-126">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="ec57d-127">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="ec57d-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="ec57d-128">Nella casella di testo digitare "blob" per ottenere l'elenco di tutte le azioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="ec57d-128">In the text box, type “blob” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="ec57d-129">Nell'esempio scegliere **AzureBlob - Ottieni metadati file in base al percorso**.</span><span class="sxs-lookup"><span data-stu-id="ec57d-129">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="ec57d-130">Se esiste già una connessione, fare clic sul pulsante **...** (Mostra selezione) per selezionare un file.</span><span class="sxs-lookup"><span data-stu-id="ec57d-130">If a connection already exists, then select the **...** (Show Picker) button to select a file.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="ec57d-131">Se viene richiesto di inserire le informazioni di connessione, immettere i dettagli per creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="ec57d-131">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="ec57d-132">La sezione [Creare la connessione](connectors-create-api-azureblobstorage.md#create-the-connection) di questo argomento descrive queste proprietà.</span><span class="sxs-lookup"><span data-stu-id="ec57d-132">[Create the connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="ec57d-133">In questo esempio si ottengono i metadati di un file.</span><span class="sxs-lookup"><span data-stu-id="ec57d-133">In this example, we get the metadata of a file.</span></span> <span data-ttu-id="ec57d-134">Per visualizzare i metadati, aggiungere un'altra azione che crea un nuovo file tramite un altro connettore.</span><span class="sxs-lookup"><span data-stu-id="ec57d-134">To see the metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="ec57d-135">Ad esempio, aggiungere un'azione OneDrive che crea un nuovo file "test" in base ai metadati.</span><span class="sxs-lookup"><span data-stu-id="ec57d-135">For example, add a OneDrive action that creates a new "test" file based on the metadata.</span></span> 


5. <span data-ttu-id="ec57d-136">Scegliere **Salva** nell'angolo in alto a sinistra della barra degli strumenti per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="ec57d-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="ec57d-137">L'app per la logica viene salvata e può essere attivata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ec57d-137">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="ec57d-138">[Storage Explorer](http://storageexplorer.com/) è lo strumento ideale per gestire più account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ec57d-138">[Storage Explorer](http://storageexplorer.com/) is a great tool to  manage multiple storage accounts.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="ec57d-139">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="ec57d-139">Connector-specific details</span></span>

<span data-ttu-id="ec57d-140">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/azureblobconnector/).</span><span class="sxs-lookup"><span data-stu-id="ec57d-140">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/azureblobconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ec57d-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ec57d-141">Next steps</span></span>
<span data-ttu-id="ec57d-142">[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ec57d-142">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="ec57d-143">Esplorare gli altri connettori disponibili nelle app per la logica nell' [elenco delle API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="ec57d-143">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>


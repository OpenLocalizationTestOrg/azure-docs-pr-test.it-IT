---
title: hello aaaAdd connettore in App per la logica di archiviazione blob Azure | Documenti Microsoft
description: Avviare e configurare connettore di archiviazione blob di Azure hello in un'app di logica
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
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a><span data-ttu-id="f6dab-103">Utilizzare il connettore di archiviazione blob di Azure hello in una app logica</span><span class="sxs-lookup"><span data-stu-id="f6dab-103">Use hello Azure blob storage connector in a logic app</span></span>
<span data-ttu-id="f6dab-104">Tooupload di connettore archiviazione Blob di Azure hello usare, aggiornare, ottenere ed eliminare BLOB nell'account di archiviazione, tutti in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="f6dab-104">Use hello Azure Blob storage connector tooupload, update, get, and delete blobs in your storage account, all within a logic app.</span></span>  

<span data-ttu-id="f6dab-105">Con Archiviazione BLOB di Azure:</span><span class="sxs-lookup"><span data-stu-id="f6dab-105">With Azure blob storage, you:</span></span>

* <span data-ttu-id="f6dab-106">Il flusso di lavoro si crea caricando nuovi progetti o recuperando file aggiornati di recente.</span><span class="sxs-lookup"><span data-stu-id="f6dab-106">Build your workflow by uploading new projects, or getting files that have been recently updated.</span></span>
* <span data-ttu-id="f6dab-107">Utilizzare i metadati del file tooget azioni, eliminare un file, la copia di file e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="f6dab-107">Use actions tooget file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="f6dab-108">Ad esempio, quando viene aggiornato uno strumento in un sito Web di Azure (trigger), viene aggiornato un file nell'archivio BLOB (azione).</span><span class="sxs-lookup"><span data-stu-id="f6dab-108">For example, when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="f6dab-109">Questo argomento viene illustrato come toouse hello blob connettore di archiviazione in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="f6dab-109">This topic shows you how toouse hello blob storage connector in a logic app.</span></span>

<span data-ttu-id="f6dab-110">toolearn informazioni sulle App per la logica, vedere [quali sono le app logica](../logic-apps/logic-apps-what-are-logic-apps.md) e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f6dab-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="f6dab-111">toolearn informazioni sulle App per la logica, vedere [quali sono le app logica](../logic-apps/logic-apps-what-are-logic-apps.md) e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f6dab-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-blob-storage"></a><span data-ttu-id="f6dab-112">La connessione di archiviazione blob tooAzure</span><span class="sxs-lookup"><span data-stu-id="f6dab-112">Connect tooAzure blob storage</span></span>
<span data-ttu-id="f6dab-113">Prima che la logica app possa accedere a qualsiasi servizio, creare innanzitutto un *connessione* toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="f6dab-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="f6dab-114">Una connessione fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="f6dab-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="f6dab-115">Ad esempio, account di archiviazione tooa tooconnect, creare innanzitutto un'archiviazione blob *connessione*.</span><span class="sxs-lookup"><span data-stu-id="f6dab-115">For example, tooconnect tooa storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="f6dab-116">toocreate una connessione, immettere le credenziali di hello utilizzato normalmente il servizio di hello tooaccess ci si connette a.</span><span class="sxs-lookup"><span data-stu-id="f6dab-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="f6dab-117">Immettere quindi hello credenziali tooyour archiviazione toocreate hello connessione ad account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6dab-117">So with Azure storage, enter hello credentials tooyour storage account toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="f6dab-118">Creare una connessione hello</span><span class="sxs-lookup"><span data-stu-id="f6dab-118">Create hello connection</span></span>
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a><span data-ttu-id="f6dab-119">Usare un trigger</span><span class="sxs-lookup"><span data-stu-id="f6dab-119">Use a trigger</span></span>
<span data-ttu-id="f6dab-120">Questo connettore non include trigger.</span><span class="sxs-lookup"><span data-stu-id="f6dab-120">This connector does not have any triggers.</span></span> <span data-ttu-id="f6dab-121">Usare altri trigger toostart hello logica app, ad esempio un trigger di ricorrenza, un trigger HTTP Webhook, i trigger disponibili con altri connettori e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="f6dab-121">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="f6dab-122">[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md) illustra un esempio.</span><span class="sxs-lookup"><span data-stu-id="f6dab-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="f6dab-123">Usare un'azione</span><span class="sxs-lookup"><span data-stu-id="f6dab-123">Use an action</span></span>
<span data-ttu-id="f6dab-124">Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="f6dab-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span>

1. <span data-ttu-id="f6dab-125">Selezionare hello sul segno più.</span><span class="sxs-lookup"><span data-stu-id="f6dab-125">Select hello plus sign.</span></span> <span data-ttu-id="f6dab-126">Vedrai diverse opzioni: **aggiungere un'azione**, **aggiungere una condizione**, o uno dei hello **più** opzioni.</span><span class="sxs-lookup"><span data-stu-id="f6dab-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="f6dab-127">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="f6dab-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="f6dab-128">Nella casella di testo hello, digitare "blob" tooget un elenco di tutte le azioni disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="f6dab-128">In hello text box, type “blob” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="f6dab-129">Nell'esempio scegliere **AzureBlob - Ottieni metadati file in base al percorso**.</span><span class="sxs-lookup"><span data-stu-id="f6dab-129">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="f6dab-130">Se esiste già una connessione, quindi selezionare hello **...** (Mostra selezione) pulsante tooselect un file.</span><span class="sxs-lookup"><span data-stu-id="f6dab-130">If a connection already exists, then select hello **...** (Show Picker) button tooselect a file.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="f6dab-131">Se viene chiesto di hello informazioni di connessione, quindi immettere connessione hello toocreate dettagli di hello.</span><span class="sxs-lookup"><span data-stu-id="f6dab-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="f6dab-132">[Creare una connessione hello](connectors-create-api-azureblobstorage.md#create-the-connection) in questo argomento vengono descritte queste proprietà.</span><span class="sxs-lookup"><span data-stu-id="f6dab-132">[Create hello connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f6dab-133">In questo esempio è ottenere hello metadati di un file.</span><span class="sxs-lookup"><span data-stu-id="f6dab-133">In this example, we get hello metadata of a file.</span></span> <span data-ttu-id="f6dab-134">toosee hello metadati, aggiungere un'altra operazione che crea un nuovo file usando un altro connettore.</span><span class="sxs-lookup"><span data-stu-id="f6dab-134">toosee hello metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="f6dab-135">Ad esempio, aggiungere un'azione di OneDrive che crea un nuovo file "test" in base ai metadati hello.</span><span class="sxs-lookup"><span data-stu-id="f6dab-135">For example, add a OneDrive action that creates a new "test" file based on hello metadata.</span></span> 


5. <span data-ttu-id="f6dab-136">**Salvare** le modifiche (angolo superiore sinistro della barra degli strumenti hello).</span><span class="sxs-lookup"><span data-stu-id="f6dab-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="f6dab-137">L'app per la logica viene salvata e può essere attivata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f6dab-137">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="f6dab-138">[Esplora archivi](http://storageexplorer.com/) è un ottimo strumento troppo gestire più account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f6dab-138">[Storage Explorer](http://storageexplorer.com/) is a great tool too manage multiple storage accounts.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="f6dab-139">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="f6dab-139">Connector-specific details</span></span>

<span data-ttu-id="f6dab-140">Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/azureblobconnector/).</span><span class="sxs-lookup"><span data-stu-id="f6dab-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/azureblobconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f6dab-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f6dab-141">Next steps</span></span>
<span data-ttu-id="f6dab-142">[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f6dab-142">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="f6dab-143">Esplorare hello altri connettori disponibile in App per la logica nel nostro [elenco API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="f6dab-143">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>


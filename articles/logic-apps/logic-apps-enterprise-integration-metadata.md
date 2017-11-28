---
title: Gestire i metadati degli elementi degli account di integrazione - App per la logica di Azure | Microsoft Docs
description: Aggiungere o recuperare i metadati degli elementi dagli account di integrazione per le app per la logica di Azure
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 28bb8296ddd820ec5aa9793dc0928b4b1e67bf6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a><span data-ttu-id="2570d-103">Gestire i metadati degli elementi dagli account di integrazione per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="2570d-103">Manage artifact metadata in integration accounts for logic apps</span></span>

<span data-ttu-id="2570d-104">È possibile definire i metadati personalizzati per gli elementi negli account di integrazione e recuperarli durante il runtime per l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="2570d-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span></span> <span data-ttu-id="2570d-105">Ad esempio, è possibile specificare i metadati per elementi quali partner, contratti, schemi e mappe; in tutti i casi i metadati vengono archiviati con coppie chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="2570d-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span></span> <span data-ttu-id="2570d-106">Attualmente, gli elementi non possono creare metadati tramite interfaccia utente, ma è possibile usare le API REST per creare i metadati.</span><span class="sxs-lookup"><span data-stu-id="2570d-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs to create metadata.</span></span> <span data-ttu-id="2570d-107">Per aggiungere metadati quando si crea o si seleziona un partner, un contratto o uno schema nel Portale di Azure, scegliere **Modifica come JSON**.</span><span class="sxs-lookup"><span data-stu-id="2570d-107">To add metadata when you create or select a partner, agreement, or schema in the Azure portal, choose **Edit as JSON**.</span></span> <span data-ttu-id="2570d-108">Per recuperare i metadati degli elementi nelle app per la logica, è possibile usare la funzionalità di ricerca elemento dell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="2570d-108">To retrieve artifact metadata in logic apps, you can use the Integration Account Artifact Lookup feature.</span></span>

## <a name="add-metadata-to-artifacts-in-integration-accounts"></a><span data-ttu-id="2570d-109">Aggiungere metadati a elementi negli account di integrazione</span><span class="sxs-lookup"><span data-stu-id="2570d-109">Add metadata to artifacts in integration accounts</span></span>

1. <span data-ttu-id="2570d-110">Creare un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="2570d-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>

2. <span data-ttu-id="2570d-111">Aggiungere un elemento all'account di integrazione, ad esempio, un [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), un [contratto](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements) o uno [schema](logic-apps-enterprise-integration-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="2570d-111">Add an artifact to your integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span></span>

3.  <span data-ttu-id="2570d-112">Selezionare l'elemento, scegliere **Modifica come JSON** e immettere i dettagli dei metadati.</span><span class="sxs-lookup"><span data-stu-id="2570d-112">Select the artifact, choose **Edit as JSON**, and enter metadata details.</span></span>

    ![Immettere i metadati](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a><span data-ttu-id="2570d-114">Recuperare metadati da elementi delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="2570d-114">Retrieve metadata from artifacts for logic apps</span></span>

1. <span data-ttu-id="2570d-115">Creare un'[app per la logica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="2570d-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="2570d-116">Creare un [collegamento dall'app per la logica all'account di integrazione](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span><span class="sxs-lookup"><span data-stu-id="2570d-116">Create a [link from your logic app to your integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span></span> 

3. <span data-ttu-id="2570d-117">Nella finestra di progettazione di app per la logica aggiungere un trigger come *richiesta* o *HTTP* all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="2570d-117">In Logic App Designer, add a trigger like *Request* or *HTTP* to your logic app.</span></span>

4.  <span data-ttu-id="2570d-118">Scegliere **Passaggio successivo** > **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="2570d-118">Choose **Next Step** > **Add an action**.</span></span> <span data-ttu-id="2570d-119">Cercare *integrazione* in modo da trovare e quindi selezionare **Account di integrazione - Ricerca elemento dell'account di integrazione**.</span><span class="sxs-lookup"><span data-stu-id="2570d-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span></span>

    ![Selezionare Ricerca elemento dell'account di integrazione](media/logic-apps-enterprise-integration-metadata/image2.png)

5. <span data-ttu-id="2570d-121">Selezionare il **tipo di elemento** e specificare un **nome elemento**</span><span class="sxs-lookup"><span data-stu-id="2570d-121">Select the **Artifact Type**, and provide the **Artifact Name**.</span></span>

    ![Selezionare il tipo di elemento e specificare un nome elemento](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a><span data-ttu-id="2570d-123">Esempio: recuperare i metadati del partner</span><span class="sxs-lookup"><span data-stu-id="2570d-123">Example: Retrieve partner metadata</span></span>

<span data-ttu-id="2570d-124">I metadati del partner sono caratterizzati dai seguenti dettagli `routingUrl`:</span><span class="sxs-lookup"><span data-stu-id="2570d-124">Partner metadata has these `routingUrl` details:</span></span>

![Cercare i metadati "routingURL" del partner](media/logic-apps-enterprise-integration-metadata/image6.png)

1. <span data-ttu-id="2570d-126">Nell'app per la logica aggiungere, il trigger, un'azione **Account di integrazione - Ricerca elemento dell'account di integrazione** per il partner e un **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="2570d-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span></span>

    ![Aggiungere trigger, ricerca di elementi e "HTTP" all'app per la logica](media/logic-apps-enterprise-integration-metadata/image4.png)

2. <span data-ttu-id="2570d-128">Per recuperare l'URI, passare alla visualizzazione Codice per app per la logica.</span><span class="sxs-lookup"><span data-stu-id="2570d-128">To retrieve the URI, go to Code View for your logic app.</span></span> <span data-ttu-id="2570d-129">La definizione dell'app per la logica dovrebbe essere simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="2570d-129">Your logic app definition should look like this example:</span></span>

    ![Ricerca](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a><span data-ttu-id="2570d-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2570d-131">Next steps</span></span>
* [<span data-ttu-id="2570d-132">Altre informazioni sui contratti</span><span class="sxs-lookup"><span data-stu-id="2570d-132">Learn more about agreements</span></span>](logic-apps-enterprise-integration-agreements.md "Informazioni sui contratti di Enterprise Integration")  

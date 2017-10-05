---
title: Messaggi Encode AS2 - App per la logica di Azure | Documentazione Microsoft
description: Come usare il codificatore AS2 in Enterprise Integration Pack in App per la logica di Azure
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 7889bf9e4e02143b6bb4c797531afa54f8647ce5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="ab151-103">Messaggi Encode AS2 in App per la logica di Azure con Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="ab151-103">Encode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="ab151-104">Per stabilire affidabilità e sicurezza durante la trasmissione dei messaggi, usare il connettore di messaggi Encode AS2.</span><span class="sxs-lookup"><span data-stu-id="ab151-104">To establish security and reliability while transmitting messages, use the Encode AS2 message connector.</span></span> <span data-ttu-id="ab151-105">Questo connettore offre funzionalità di firma digitale, crittografia e riconoscimenti tramite notifiche sulla ricezione di messaggi, con il conseguente supporto del database di non ripudio.</span><span class="sxs-lookup"><span data-stu-id="ab151-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads to support for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="ab151-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="ab151-106">Before you start</span></span>

<span data-ttu-id="ab151-107">Sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ab151-107">Here's the items you need:</span></span>

* <span data-ttu-id="ab151-108">Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="ab151-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="ab151-109">Un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md) già definito e associato alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab151-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="ab151-110">Per usare il connettore di messaggi Encode AS2 è necessario un account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="ab151-110">You must have an integration account to use the Encode AS2 message connector.</span></span>
* <span data-ttu-id="ab151-111">Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="ab151-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="ab151-112">Un [contratto AS2](logic-apps-enterprise-integration-as2.md) già definito nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="ab151-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="ab151-113">Codificare i messaggi AS2</span><span class="sxs-lookup"><span data-stu-id="ab151-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="ab151-114">[Creare un'app per la logica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ab151-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="ab151-115">Il connettore di messaggi Encode AS2 non dispone di trigger, pertanto è necessario aggiungerne uno per avviare l'app per la logica, ad esempio un trigger di richiesta.</span><span class="sxs-lookup"><span data-stu-id="ab151-115">The Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="ab151-116">In Progettazione app per la logica aggiungere un trigger e un'azione all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="ab151-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="ab151-117">Nella casella di ricerca, immettere "AS2" come filtro.</span><span class="sxs-lookup"><span data-stu-id="ab151-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="ab151-118">Selezionare **AS2 - Codifica in un messaggio AS2**.</span><span class="sxs-lookup"><span data-stu-id="ab151-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    ![Cercare "AS2"](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="ab151-120">Se non sono state create in precedenza le connessioni all'account di integrazione, a questo punto viene richiesto di creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="ab151-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="ab151-121">Denominare la connessione e selezionare l'account di integrazione al quale connettersi.</span><span class="sxs-lookup"><span data-stu-id="ab151-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![creare una connessione all'account di integrazione](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="ab151-123">Le proprietà con l'asterisco sono obbligatorie.</span><span class="sxs-lookup"><span data-stu-id="ab151-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="ab151-124">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ab151-124">Property</span></span> | <span data-ttu-id="ab151-125">Dettagli</span><span class="sxs-lookup"><span data-stu-id="ab151-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="ab151-126">Nome connessione *</span><span class="sxs-lookup"><span data-stu-id="ab151-126">Connection Name *</span></span> |<span data-ttu-id="ab151-127">Immettere un nome per la connessione.</span><span class="sxs-lookup"><span data-stu-id="ab151-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="ab151-128">Account di integrazione *</span><span class="sxs-lookup"><span data-stu-id="ab151-128">Integration Account *</span></span> |<span data-ttu-id="ab151-129">Immettere un nome per l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="ab151-129">Enter a name for your integration account.</span></span> <span data-ttu-id="ab151-130">Verificare che l'account di integrazione e l'app per la logica si trovino nella stessa località di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab151-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="ab151-131">Al termine, i dettagli della connessione dovrebbero essere simili a quelli dell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="ab151-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="ab151-132">Per completare la creazione della connessione, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ab151-132">To finish creating your connection, choose **Create**.</span></span>
   
    ![Dettagli della connessione di integrazione](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="ab151-134">Dopo aver creato la connessione, come illustrato nell'esempio, specificare i dettagli per gli identificatori **AS2-From**, **AS2-To** come configurato nel contratto, e **Corpo**, ovvero il payload del messaggio.</span><span class="sxs-lookup"><span data-stu-id="ab151-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-To identifiers** as configured in your agreement, and **Body**, which is the message payload.</span></span>
   
    ![specificare i campi obbligatori](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="ab151-136">Dettagli codificatore AS2</span><span class="sxs-lookup"><span data-stu-id="ab151-136">AS2 encoder details</span></span>

<span data-ttu-id="ab151-137">Il connettore Encode AS2 esegue queste attività:</span><span class="sxs-lookup"><span data-stu-id="ab151-137">The Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="ab151-138">Elabora le intestazioni AS2/HTTP</span><span class="sxs-lookup"><span data-stu-id="ab151-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="ab151-139">Firma i messaggi in uscita (se configurata)</span><span class="sxs-lookup"><span data-stu-id="ab151-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="ab151-140">Crittografa i messaggi in uscita (se configurata)</span><span class="sxs-lookup"><span data-stu-id="ab151-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="ab151-141">Comprime i messaggi (se configurata)</span><span class="sxs-lookup"><span data-stu-id="ab151-141">Compresses the message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="ab151-142">Provare questo esempio</span><span class="sxs-lookup"><span data-stu-id="ab151-142">Try this sample</span></span>

<span data-ttu-id="ab151-143">Per distribuire un'app per la logica completamente operativa e uno scenario AS2 di esempio, vedere il [modello e lo scenario di app per la logica AS2](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="ab151-143">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="ab151-144">Visualizzare il file Swagger</span><span class="sxs-lookup"><span data-stu-id="ab151-144">View the swagger</span></span>
<span data-ttu-id="ab151-145">Vedere i [dettagli del file Swagger](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="ab151-145">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ab151-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ab151-146">Next steps</span></span>
[<span data-ttu-id="ab151-147">Altre informazioni su Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="ab151-147">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Informazioni su Enterprise Integration Pack") 


---
title: Messaggi Decode AS2 - App per la logica di Azure | Documentazione Microsoft
description: Come usare il decodificatore AS2 in Enterprise Integration Pack in App per la logica di Azure
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: a7920b2509fe368c6f7d55e17fe0bf0020c4562c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="50bd9-103">Messaggi Decode AS2 in App per la logica di Azure con Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="50bd9-103">Decode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span> 

<span data-ttu-id="50bd9-104">Per stabilire affidabilità e sicurezza durante la trasmissione dei messaggi, usare il connettore di messaggi Decode AS2.</span><span class="sxs-lookup"><span data-stu-id="50bd9-104">To establish security and reliability while transmitting messages, use the Decode AS2 message connector.</span></span> <span data-ttu-id="50bd9-105">Questo connettore offre funzionalità di firma digitale, decrittografia e riconoscimenti tramite notifiche sulla ricezione di messaggi.</span><span class="sxs-lookup"><span data-stu-id="50bd9-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="50bd9-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="50bd9-106">Before you start</span></span>

<span data-ttu-id="50bd9-107">Sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="50bd9-107">Here's the items you need:</span></span>

* <span data-ttu-id="50bd9-108">Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="50bd9-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="50bd9-109">Un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md) già definito e associato alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="50bd9-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="50bd9-110">Per usare il connettore di messaggi Decode AS2 è necessario un account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="50bd9-110">You must have an integration account to use the Decode AS2 message connector.</span></span>
* <span data-ttu-id="50bd9-111">Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="50bd9-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="50bd9-112">Un [contratto AS2](logic-apps-enterprise-integration-as2.md) già definito nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="50bd9-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="50bd9-113">Decodificare i messaggi AS2</span><span class="sxs-lookup"><span data-stu-id="50bd9-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="50bd9-114">[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="50bd9-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="50bd9-115">Il connettore di messaggi Decode AS2 non dispone di trigger, pertanto è necessario aggiungerne uno per avviare l'app per la logica, ad esempio un trigger di richiesta.</span><span class="sxs-lookup"><span data-stu-id="50bd9-115">The Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="50bd9-116">In Progettazione app per la logica aggiungere un trigger e un'azione all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="50bd9-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="50bd9-117">Nella casella di ricerca, immettere "AS2" come filtro.</span><span class="sxs-lookup"><span data-stu-id="50bd9-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="50bd9-118">Selezionare **AS2 - Decodifica il messaggio AS2**.</span><span class="sxs-lookup"><span data-stu-id="50bd9-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    ![Cercare "AS2"](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="50bd9-120">Se non sono state create in precedenza le connessioni all'account di integrazione, a questo punto viene richiesto di creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="50bd9-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="50bd9-121">Denominare la connessione e selezionare l'account di integrazione al quale connettersi.</span><span class="sxs-lookup"><span data-stu-id="50bd9-121">Name your connection, and select the integration account that you want to connect.</span></span>
   
    ![Create una connessione di integrazione](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="50bd9-123">Le proprietà con l'asterisco sono obbligatorie.</span><span class="sxs-lookup"><span data-stu-id="50bd9-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="50bd9-124">Proprietà</span><span class="sxs-lookup"><span data-stu-id="50bd9-124">Property</span></span> | <span data-ttu-id="50bd9-125">Dettagli</span><span class="sxs-lookup"><span data-stu-id="50bd9-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="50bd9-126">Nome connessione *</span><span class="sxs-lookup"><span data-stu-id="50bd9-126">Connection Name *</span></span> |<span data-ttu-id="50bd9-127">Immettere un nome per la connessione.</span><span class="sxs-lookup"><span data-stu-id="50bd9-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="50bd9-128">Account di integrazione *</span><span class="sxs-lookup"><span data-stu-id="50bd9-128">Integration Account *</span></span> |<span data-ttu-id="50bd9-129">Immettere un nome per l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="50bd9-129">Enter a name for your integration account.</span></span> <span data-ttu-id="50bd9-130">Verificare che l'account di integrazione e l'app per la logica si trovino nella stessa località di Azure.</span><span class="sxs-lookup"><span data-stu-id="50bd9-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="50bd9-131">Al termine, i dettagli della connessione dovrebbero essere simili a quelli dell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="50bd9-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="50bd9-132">Per completare la creazione della connessione, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="50bd9-132">To finish creating your connection, choose **Create**.</span></span>

    ![Dettagli della connessione di integrazione](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="50bd9-134">Dopo aver creato la connessione, come illustrato nell'esempio, selezionare **Corpo** e **Intestazioni** dagli output della richiesta.</span><span class="sxs-lookup"><span data-stu-id="50bd9-134">After your connection is created, as shown in this example, select **Body** and **Headers** from the Request outputs.</span></span>
   
    ![connessione di integrazione creata](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="50bd9-136">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="50bd9-136">For example:</span></span>

    ![Selezionare Corpo e Intestazioni dagli output della richiesta](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="50bd9-138">Dettagli del decodificatore AS2</span><span class="sxs-lookup"><span data-stu-id="50bd9-138">AS2 decoder details</span></span>

<span data-ttu-id="50bd9-139">Il connettore Decode AS2 esegue queste attività:</span><span class="sxs-lookup"><span data-stu-id="50bd9-139">The Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="50bd9-140">Elabora le intestazioni AS2/HTTP</span><span class="sxs-lookup"><span data-stu-id="50bd9-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="50bd9-141">Verifica la firma (se configurata)</span><span class="sxs-lookup"><span data-stu-id="50bd9-141">Verifies the signature (if configured)</span></span>
* <span data-ttu-id="50bd9-142">Decrittografa i messaggi (se configurata)</span><span class="sxs-lookup"><span data-stu-id="50bd9-142">Decrypts the messages (if configured)</span></span>
* <span data-ttu-id="50bd9-143">Decomprime i messaggi (se configurata)</span><span class="sxs-lookup"><span data-stu-id="50bd9-143">Decompresses the message (if configured)</span></span>
* <span data-ttu-id="50bd9-144">Riconcilia una notifica sulla ricezione del messaggio ricevuta con il messaggio in uscita originale</span><span class="sxs-lookup"><span data-stu-id="50bd9-144">Reconciles a received MDN with the original outbound message</span></span>
* <span data-ttu-id="50bd9-145">Aggiorna e mette in correlazione i record nel database di non ripudio</span><span class="sxs-lookup"><span data-stu-id="50bd9-145">Updates and correlates records in the non-repudiation database</span></span>
* <span data-ttu-id="50bd9-146">Scrive i record per la creazione di report di stato su AS2</span><span class="sxs-lookup"><span data-stu-id="50bd9-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="50bd9-147">Il contenuto del payload di output è codificato con codifica Base 64</span><span class="sxs-lookup"><span data-stu-id="50bd9-147">The output payload contents are base64 encoded</span></span>
* <span data-ttu-id="50bd9-148">Determina se una notifica sulla ricezione del messaggio è obbligatoria, se deve essere sincrona o asincrona in base alla configurazione nel contratto AS2</span><span class="sxs-lookup"><span data-stu-id="50bd9-148">Determines whether an MDN is required, and whether the MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="50bd9-149">Genera una notifica sulla ricezione del messaggio sincrona o asincrona, in base alle configurazioni nel contratto</span><span class="sxs-lookup"><span data-stu-id="50bd9-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="50bd9-150">Imposta le proprietà e il token di correlazione nella notifica sulla ricezione del messaggio</span><span class="sxs-lookup"><span data-stu-id="50bd9-150">Sets the correlation tokens and properties on the MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="50bd9-151">Provare questo esempio</span><span class="sxs-lookup"><span data-stu-id="50bd9-151">Try this sample</span></span>

<span data-ttu-id="50bd9-152">Per distribuire un'app per la logica completamente operativa e uno scenario AS2 di esempio, vedere il [modello e lo scenario di app per la logica AS2](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="50bd9-152">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="50bd9-153">Visualizzare il file Swagger</span><span class="sxs-lookup"><span data-stu-id="50bd9-153">View the swagger</span></span>
<span data-ttu-id="50bd9-154">Vedere i [dettagli del file Swagger](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="50bd9-154">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="50bd9-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="50bd9-155">Next steps</span></span>
[<span data-ttu-id="50bd9-156">Altre informazioni su Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="50bd9-156">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 


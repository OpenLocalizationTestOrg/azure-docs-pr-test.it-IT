---
title: Messaggi Encode X12 - App per la logica di Azure | Documentazione Microsoft
description: "Convalidare le proprietà EDI e convertire messaggi con codifica XLM con il codificatore di messaggi X12 in Enterprise Integration Pack in App per la logica di Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 29d19364b9a98e351c95f13e68a2e63b9f6439f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="5e87f-103">Messaggi Encode X12 in App per la logica di Azure con Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="5e87f-103">Encode X12 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="5e87f-104">Il connettore di messaggi Encode X12 convalida le proprietà EDI e specifiche del partner, converte i messaggi con codifica XML in set di transazioni EDI nell'interscambio e richiede un riconoscimento tecnico, funzionale o entrambi.</span><span class="sxs-lookup"><span data-stu-id="5e87f-104">With the Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in the interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="5e87f-105">Per usare questo connettore, è necessario aggiungerlo a un trigger esistente nell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="5e87f-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="5e87f-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="5e87f-106">Before you start</span></span>

<span data-ttu-id="5e87f-107">Sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e87f-107">Here's the items you need:</span></span>

* <span data-ttu-id="5e87f-108">Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="5e87f-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="5e87f-109">Un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md) già definito e associato alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e87f-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="5e87f-110">Per usare il connettore di messaggi Encode X12 è necessario un account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="5e87f-110">You must have an integration account to use the Encode X12 message connector.</span></span>
* <span data-ttu-id="5e87f-111">Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="5e87f-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="5e87f-112">Un [contratto X12](logic-apps-enterprise-integration-x12.md) già definito nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="5e87f-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="5e87f-113">Messaggi Encode X12</span><span class="sxs-lookup"><span data-stu-id="5e87f-113">Encode X12 messages</span></span>

1. <span data-ttu-id="5e87f-114">[Creare un'app per la logica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5e87f-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="5e87f-115">Il connettore di messaggi Encode X12 non dispone di trigger, pertanto è necessario aggiungerne uno per avviare l'app per la logica, ad esempio un trigger di richiesta.</span><span class="sxs-lookup"><span data-stu-id="5e87f-115">The Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="5e87f-116">In Progettazione app per la logica aggiungere un trigger e un'azione all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="5e87f-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="5e87f-117">Nella casella di ricerca, immettere "x12" come filtro.</span><span class="sxs-lookup"><span data-stu-id="5e87f-117">In the search box, enter "x12" for your filter.</span></span> <span data-ttu-id="5e87f-118">Selezionare **X12 - Codifica in un messaggio X12 in base al nome dell'accordo** o **X12 - Codifica in un messaggio X12 in base alle identità**.</span><span class="sxs-lookup"><span data-stu-id="5e87f-118">Select either **X12 - Encode to X12 message by agreement name** or **X12 - Encode to X12 message by identities**.</span></span>
   
    ![Cercare "X12"](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="5e87f-120">Se non sono state create in precedenza le connessioni all'account di integrazione, a questo punto viene richiesto di creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="5e87f-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="5e87f-121">Denominare la connessione e selezionare l'account di integrazione al quale connettersi.</span><span class="sxs-lookup"><span data-stu-id="5e87f-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![connessione all'account di integrazione](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="5e87f-123">Le proprietà con l'asterisco sono obbligatorie.</span><span class="sxs-lookup"><span data-stu-id="5e87f-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="5e87f-124">Proprietà</span><span class="sxs-lookup"><span data-stu-id="5e87f-124">Property</span></span> | <span data-ttu-id="5e87f-125">Dettagli</span><span class="sxs-lookup"><span data-stu-id="5e87f-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="5e87f-126">Nome connessione *</span><span class="sxs-lookup"><span data-stu-id="5e87f-126">Connection Name *</span></span> |<span data-ttu-id="5e87f-127">Immettere un nome per la connessione.</span><span class="sxs-lookup"><span data-stu-id="5e87f-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="5e87f-128">Account di integrazione *</span><span class="sxs-lookup"><span data-stu-id="5e87f-128">Integration Account *</span></span> |<span data-ttu-id="5e87f-129">Immettere un nome per l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="5e87f-129">Enter a name for your integration account.</span></span> <span data-ttu-id="5e87f-130">Verificare che l'account di integrazione e l'app per la logica si trovino nella stessa località di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e87f-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="5e87f-131">Al termine, i dettagli della connessione dovrebbero essere simili a quelli dell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="5e87f-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="5e87f-132">Per completare la creazione della connessione, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5e87f-132">To finish creating your connection, choose **Create**.</span></span>

    ![connessione all'account di integrazione creata](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="5e87f-134">La connessione è stata creata.</span><span class="sxs-lookup"><span data-stu-id="5e87f-134">Your connection is now created.</span></span>

    ![dettagli della connessione all'account di integrazione](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="5e87f-136">Encode X12 Message by agreement name (Messaggio Encode X12 per nome contratto)</span><span class="sxs-lookup"><span data-stu-id="5e87f-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="5e87f-137">Se si sceglie di codificare i messaggi X12 in base al nome del contratto, aprire l'elenco **Nome dell'accordo X12** e digitare o selezionare il contratto X12 esistente.</span><span class="sxs-lookup"><span data-stu-id="5e87f-137">If you chose to encode X12 messages by agreement name, open the **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="5e87f-138">Immettere il messaggio XML da codificare.</span><span class="sxs-lookup"><span data-stu-id="5e87f-138">Enter the XML message to encode.</span></span>

![Immettere il nome del contratto X12 e il messaggio XML da codificare.](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="5e87f-140">Encode X12 Message by identities (Messaggio Encode X12 per identità)</span><span class="sxs-lookup"><span data-stu-id="5e87f-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="5e87f-141">Se si sceglie di codificare i messaggi X12 in base alle identità, inserire l'identificatore del mittente, il qualificatore del mittente, l'identificatore del destinatario e il qualificatore del destinatario come configurati nel contratto X12.</span><span class="sxs-lookup"><span data-stu-id="5e87f-141">If you choose to encode X12 messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="5e87f-142">Selezionare il messaggio XML da codificare.</span><span class="sxs-lookup"><span data-stu-id="5e87f-142">Select the XML message to encode.</span></span>
   
![Fornire le identità del mittente e del destinatario e selezionare il messaggio XML da codificare](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="5e87f-144">Dettagli di Encode X12</span><span class="sxs-lookup"><span data-stu-id="5e87f-144">X12 Encode details</span></span>

<span data-ttu-id="5e87f-145">Il connettore Encode X12 esegue queste attività:</span><span class="sxs-lookup"><span data-stu-id="5e87f-145">The X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="5e87f-146">Risoluzione del contratto associando le proprietà del contesto di mittente e del destinatario.</span><span class="sxs-lookup"><span data-stu-id="5e87f-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="5e87f-147">Serializza l'interscambio EDI, conversione dei messaggi con codifica XML in set di transazioni EDI nell'interscambio.</span><span class="sxs-lookup"><span data-stu-id="5e87f-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="5e87f-148">Si applica ai segmenti di intestazione e finali del set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="5e87f-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="5e87f-149">Genera un numero di controllo di interscambio, un numero di controllo di gruppo e un numero di controllo del set di transazioni per ogni interscambio in uscita.</span><span class="sxs-lookup"><span data-stu-id="5e87f-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="5e87f-150">Sostituisce i separatori nei dati del payload.</span><span class="sxs-lookup"><span data-stu-id="5e87f-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="5e87f-151">Convalida le proprietà EDI e specifiche del partner.</span><span class="sxs-lookup"><span data-stu-id="5e87f-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="5e87f-152">Convalida dello schema degli elementi dati del set di transazioni rispetto allo schema del messaggio.</span><span class="sxs-lookup"><span data-stu-id="5e87f-152">Schema validation of the transaction-set data elements against the message Schema</span></span>
  * <span data-ttu-id="5e87f-153">Convalida EDI eseguita sugli elementi dati del set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="5e87f-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="5e87f-154">Convalida estesa eseguita sugli elementi dati del set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="5e87f-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="5e87f-155">Richiede un riconoscimento tecnico e/o funzionale (se configurata).</span><span class="sxs-lookup"><span data-stu-id="5e87f-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="5e87f-156">Un riconoscimento tecnico viene generato in seguito alla convalida dell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="5e87f-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="5e87f-157">Il riconoscimento tecnico segnala lo stato dell'elaborazione di un'intestazione e finale di interscambio in base all'indirizzo del ricevitore.</span><span class="sxs-lookup"><span data-stu-id="5e87f-157">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver</span></span>
  * <span data-ttu-id="5e87f-158">Un riconoscimento funzionale viene generato in seguito alla convalida del corpo.</span><span class="sxs-lookup"><span data-stu-id="5e87f-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="5e87f-159">Il riconoscimento funzionale segnala ogni errore rilevato durante l'elaborazione del documento ricevuto.</span><span class="sxs-lookup"><span data-stu-id="5e87f-159">The functional acknowledgment reports each error encountered while processing the received document</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="5e87f-160">Visualizzare il file Swagger</span><span class="sxs-lookup"><span data-stu-id="5e87f-160">View the swagger</span></span>
<span data-ttu-id="5e87f-161">Vedere i [dettagli del file Swagger](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="5e87f-161">See the [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5e87f-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5e87f-162">Next steps</span></span>
[<span data-ttu-id="5e87f-163">Altre informazioni su Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="5e87f-163">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Informazioni su Enterprise Integration Pack") 


---
title: Messaggi Decode X12 - App per la logica di Azure | Documentazione Microsoft
description: "Convalidare le proprietà EDI e generare i riconoscimenti con il decodificatore di messaggi X12 in Enterprise Integration Pack in App per la logica di Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 4fd48d2d-2008-4080-b6a1-8ae183b48131
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 18719a8f49c74973947517161f7306c233a9323f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="7dfbe-103">Messaggi Decode X12 in App per la logica di Azure con Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="7dfbe-103">Decode X12 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="7dfbe-104">Il connettore di messaggi Decode X12 convalida la busta in base all'accordo tra partner commerciali, convalida le proprietà EDI e specifiche del partner, suddivide gli interscambi in set di transazioni o mantiene gli interscambi interi, nonché genera riconoscimenti per le transazioni elaborate.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-104">With the Decode X12 message connector, you can validate the envelope against a trading partner agreement, validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="7dfbe-105">Per usare questo connettore, è necessario aggiungerlo a un trigger esistente nell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="7dfbe-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="7dfbe-106">Before you start</span></span>

<span data-ttu-id="7dfbe-107">Sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7dfbe-107">Here's the items you need:</span></span>

* <span data-ttu-id="7dfbe-108">Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="7dfbe-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="7dfbe-109">Un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md) già definito e associato alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="7dfbe-110">Per usare il connettore di messaggi Decode X12 è necessario un account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-110">You must have an integration account to use the Decode X12 message connector.</span></span>
* <span data-ttu-id="7dfbe-111">Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="7dfbe-112">Un [contratto X12](logic-apps-enterprise-integration-x12.md) già definito nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="decode-x12-messages"></a><span data-ttu-id="7dfbe-113">Messaggi Decode X12</span><span class="sxs-lookup"><span data-stu-id="7dfbe-113">Decode X12 messages</span></span>

1. <span data-ttu-id="7dfbe-114">[Creare un'app per la logica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="7dfbe-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="7dfbe-115">Il connettore di messaggi Decode X12 non dispone di trigger, pertanto è necessario aggiungerne uno per avviare l'app per la logica, ad esempio un trigger di richiesta.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-115">The Decode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="7dfbe-116">In Progettazione app per la logica aggiungere un trigger e un'azione all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="7dfbe-117">Nella casella di ricerca, immettere "x12" come filtro.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-117">In the search box, enter "x12" for your filter.</span></span> <span data-ttu-id="7dfbe-118">Selezionare **X12 - Decodifica il messaggio X12**.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-118">Select **X12 - Decode X12 message**.</span></span>
   
    ![Cercare "X12"](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. <span data-ttu-id="7dfbe-120">Se non sono state create in precedenza le connessioni all'account di integrazione, a questo punto viene richiesto di creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="7dfbe-121">Denominare la connessione e selezionare l'account di integrazione al quale connettersi.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-121">Name your connection, and select the integration account that you want to connect.</span></span> 

    ![Fornire i dettagli della connessione all'account di integrazione](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    <span data-ttu-id="7dfbe-123">Le proprietà con l'asterisco sono obbligatorie.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="7dfbe-124">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7dfbe-124">Property</span></span> | <span data-ttu-id="7dfbe-125">Dettagli</span><span class="sxs-lookup"><span data-stu-id="7dfbe-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="7dfbe-126">Nome connessione *</span><span class="sxs-lookup"><span data-stu-id="7dfbe-126">Connection Name *</span></span> |<span data-ttu-id="7dfbe-127">Immettere un nome per la connessione.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="7dfbe-128">Account di integrazione *</span><span class="sxs-lookup"><span data-stu-id="7dfbe-128">Integration Account *</span></span> |<span data-ttu-id="7dfbe-129">Immettere un nome per l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-129">Enter a name for your integration account.</span></span> <span data-ttu-id="7dfbe-130">Verificare che l'account di integrazione e l'app per la logica si trovino nella stessa località di Azure.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="7dfbe-131">Al termine, i dettagli della connessione dovrebbero essere simili a quelli dell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="7dfbe-132">Per completare la creazione della connessione, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-132">To finish creating your connection, choose **Create**.</span></span>
   
    ![dettagli della connessione all'account di integrazione](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. <span data-ttu-id="7dfbe-134">Dopo aver creato la connessione, come illustrato in questo esempio, selezionare il messaggio con file flat X12 da decodificare.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-134">After your connection is created, as shown in this example, select the X12 flat file message to decode.</span></span>

    ![connessione all'account di integrazione creata](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    <span data-ttu-id="7dfbe-136">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7dfbe-136">For example:</span></span>

    ![Selezionare il messaggio con il file flat X12 da decodificare](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a><span data-ttu-id="7dfbe-138">Dettagli Decode X12</span><span class="sxs-lookup"><span data-stu-id="7dfbe-138">X12 Decode details</span></span>

<span data-ttu-id="7dfbe-139">Il connettore Decode X12 esegue queste attività:</span><span class="sxs-lookup"><span data-stu-id="7dfbe-139">The X12 Decode connector performs these tasks:</span></span>

* <span data-ttu-id="7dfbe-140">Convalida la busta in base all'accordo tra partner commerciali.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-140">Validates the envelope against trading partner agreement</span></span>
* <span data-ttu-id="7dfbe-141">Convalida le proprietà EDI e specifiche del partner.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-141">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="7dfbe-142">Convalida strutturale EDI e convalida estesa dello schema.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-142">EDI structural validation, and extended schema validation</span></span>
  * <span data-ttu-id="7dfbe-143">Convalida della struttura della busta dell'interscambio.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-143">Validation of the structure of the interchange envelope.</span></span>
  * <span data-ttu-id="7dfbe-144">Convalida dello schema della busta in base allo schema di controllo.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-144">Schema validation of the envelope against the control schema.</span></span>
  * <span data-ttu-id="7dfbe-145">Convalida dello schema degli elementi dati del set di transazioni rispetto allo schema del messaggio.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-145">Schema validation of the transaction-set data elements against the message schema.</span></span>
  * <span data-ttu-id="7dfbe-146">Convalida EDI eseguita sugli elementi dati del set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-146">EDI validation performed on transaction-set data elements</span></span> 
* <span data-ttu-id="7dfbe-147">Verifica che i numeri di controllo di un set di interscambio, gruppo e di transazioni non siano duplicati.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-147">Verifies that the interchange, group, and transaction set control numbers are not duplicates</span></span>
  * <span data-ttu-id="7dfbe-148">Controlla il numero di controllo dell'interscambio rispetto agli interscambi ricevuti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-148">Checks the interchange control number against previously received interchanges.</span></span>
  * <span data-ttu-id="7dfbe-149">Controlla il numero di controllo del gruppo con gli altri numeri di controllo del gruppo dell'interscambio.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-149">Checks the group control number against other group control numbers in the interchange.</span></span>
  * <span data-ttu-id="7dfbe-150">Controlla il numero di controllo del set di transazioni con gli altri numeri di controllo del set transazioni in tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-150">Checks the transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="7dfbe-151">Suddivide l'interscambio in set di transazioni o mantiene l'intero interscambio:</span><span class="sxs-lookup"><span data-stu-id="7dfbe-151">Splits the interchange into transaction sets, or preserves the entire interchange:</span></span>
  * <span data-ttu-id="7dfbe-152">Suddivide l'interscambio in set di transazioni - sospende i set di transazioni in caso di errore: suddivide l'interscambio in set di transazioni e analizza ogni set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-152">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="7dfbe-153">L'azione X12 Decode restituisce solo i set di transazioni che non sono stati convalidati in `badMessages` e restituisce i restanti set di transazioni in `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-153">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="7dfbe-154">Suddivide l'interscambio in set di transazioni - sospende l'interscambio in caso di errore: suddivide l'interscambio in set di transazioni e analizza ogni set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-154">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="7dfbe-155">Se la convalida di uno o più set di transazioni dell'interscambio non riesce, l'azione X12 Decode restituisce tutti i set di transazioni in quell'interscambio in `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-155">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
  * <span data-ttu-id="7dfbe-156">Mantiene l'interscambio - sospende i set transazioni in caso di errore: mantiene l'interscambio ed elabora l'intero interscambio in batch.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-156">Preserve Interchange - suspend transaction sets on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="7dfbe-157">L'azione X12 Decode restituisce solo i set di transazioni che non sono stati convalidati in `badMessages` e restituisce i restanti set di transazioni in `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-157">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="7dfbe-158">Mantiene l'interscambio - sospende l'interscambio in caso di errore: mantiene l'interscambio ed elabora l'intero interscambio in batch.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-158">Preserve Interchange - suspend interchange on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="7dfbe-159">Se la convalida di uno o più set di transazioni dell'interscambio non riesce, l'azione X12 Decode restituisce tutti i set di transazioni in quell'interscambio in `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-159">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span> 
* <span data-ttu-id="7dfbe-160">Genera un riconoscimento tecnico e/o funzionale (se configurata).</span><span class="sxs-lookup"><span data-stu-id="7dfbe-160">Generates a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="7dfbe-161">Un riconoscimento tecnico viene generato in seguito alla convalida dell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-161">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="7dfbe-162">Il riconoscimento tecnico segnala lo stato dell'elaborazione di un'intestazione e finale di interscambio in base all'indirizzo del ricevitore.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-162">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver.</span></span>
  * <span data-ttu-id="7dfbe-163">Un riconoscimento funzionale viene generato in seguito alla convalida del corpo.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-163">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="7dfbe-164">Il riconoscimento funzionale segnala ogni errore rilevato durante l'elaborazione del documento ricevuto.</span><span class="sxs-lookup"><span data-stu-id="7dfbe-164">The functional acknowledgment reports each error encountered while processing the received document</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="7dfbe-165">Visualizzare il file Swagger</span><span class="sxs-lookup"><span data-stu-id="7dfbe-165">View the swagger</span></span>
<span data-ttu-id="7dfbe-166">Vedere i [dettagli del file Swagger](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="7dfbe-166">See the [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7dfbe-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7dfbe-167">Next steps</span></span>
[<span data-ttu-id="7dfbe-168">Altre informazioni su Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="7dfbe-168">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Informazioni su Enterprise Integration Pack") 


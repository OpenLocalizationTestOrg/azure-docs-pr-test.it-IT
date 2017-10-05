---
title: Decodificare messaggi EDIFACT - App per la logica di Azure | Documentazione Microsoft
description: "Convalidare le proprietà EDI e generare i riconoscimenti con il decodificatore di messaggi EDIFACT in Enterprise Integration Pack in App per la logica di Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e3787b48037360bf6066ddce2bacba6842213b2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="0854a-103">Messaggi Decode EDIFACT in App per la logica di Azure con Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="0854a-103">Decode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="0854a-104">Il connettore di messaggi EDIFACT convalida le proprietà EDI e specifiche del partner, suddivide gli interscambi in set di transazioni o mantiene gli interscambi interi, nonché genera riconoscimenti per le transazioni elaborate.</span><span class="sxs-lookup"><span data-stu-id="0854a-104">With the Decode EDIFACT message connector, you can validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="0854a-105">Per usare questo connettore, è necessario aggiungerlo a un trigger esistente nell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="0854a-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="0854a-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="0854a-106">Before you start</span></span>

<span data-ttu-id="0854a-107">Sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0854a-107">Here's the items you need:</span></span>

* <span data-ttu-id="0854a-108">Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="0854a-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="0854a-109">Un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md) già definito e associato alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0854a-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="0854a-110">Per usare il connettore di messaggi Decode EDIFACT è necessario un account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="0854a-110">You must have an integration account to use the Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="0854a-111">Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="0854a-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="0854a-112">Un [contratto EDIFACT](logic-apps-enterprise-integration-edifact.md) già definito nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="0854a-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="0854a-113">Decodificare messaggi EDIFACT</span><span class="sxs-lookup"><span data-stu-id="0854a-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="0854a-114">[Creare un'app per la logica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0854a-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="0854a-115">Il connettore di messaggi Decode EDIFACT non dispone di trigger, pertanto è necessario aggiungerne uno per avviare l'app per la logica, ad esempio un trigger di richiesta.</span><span class="sxs-lookup"><span data-stu-id="0854a-115">The Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="0854a-116">In Progettazione app per la logica aggiungere un trigger e un'azione all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="0854a-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3. <span data-ttu-id="0854a-117">Nella casella di ricerca, digitare "EDIFACT" come filtro.</span><span class="sxs-lookup"><span data-stu-id="0854a-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="0854a-118">Selezionare **Decodifica il messaggio EDIFACT**.</span><span class="sxs-lookup"><span data-stu-id="0854a-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![ricerca di EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="0854a-120">Se non sono state create in precedenza le connessioni all'account di integrazione, a questo punto viene richiesto di creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="0854a-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="0854a-121">Denominare la connessione e selezionare l'account di integrazione al quale connettersi.</span><span class="sxs-lookup"><span data-stu-id="0854a-121">Name your connection, and select the integration account that you want to connect.</span></span>
   
    ![creare un account di integrazione](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="0854a-123">Le proprietà con l'asterisco sono obbligatorie.</span><span class="sxs-lookup"><span data-stu-id="0854a-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="0854a-124">Proprietà</span><span class="sxs-lookup"><span data-stu-id="0854a-124">Property</span></span> | <span data-ttu-id="0854a-125">Dettagli</span><span class="sxs-lookup"><span data-stu-id="0854a-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="0854a-126">Nome connessione *</span><span class="sxs-lookup"><span data-stu-id="0854a-126">Connection Name *</span></span> |<span data-ttu-id="0854a-127">Immettere un nome per la connessione.</span><span class="sxs-lookup"><span data-stu-id="0854a-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="0854a-128">Account di integrazione *</span><span class="sxs-lookup"><span data-stu-id="0854a-128">Integration Account *</span></span> |<span data-ttu-id="0854a-129">Immettere un nome per l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="0854a-129">Enter a name for your integration account.</span></span> <span data-ttu-id="0854a-130">Verificare che l'account di integrazione e l'app per la logica si trovino nella stessa località di Azure.</span><span class="sxs-lookup"><span data-stu-id="0854a-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

4. <span data-ttu-id="0854a-131">Dopo aver completato la creazione della connessione, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0854a-131">When you're done to finish creating your connection, choose **Create**.</span></span> <span data-ttu-id="0854a-132">I dettagli della connessione dovrebbero essere simili a quelli dell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="0854a-132">Your connection details should look similar to this example:</span></span>

    ![dettagli dell'account di integrazione](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="0854a-134">Dopo aver creato la connessione, come illustrato in questo esempio, selezionare il messaggio con file flat EDIFACT da decodificare.</span><span class="sxs-lookup"><span data-stu-id="0854a-134">After your connection is created, as shown in this example, select the EDIFACT flat file message to decode.</span></span>

    ![connessione all'account di integrazione creata](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="0854a-136">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0854a-136">For example:</span></span>

    ![Selezionare il messaggio con il file flat EDIFACT da decodificare](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="0854a-138">Dettagli decodificatore EDIFACT</span><span class="sxs-lookup"><span data-stu-id="0854a-138">EDIFACT decoder details</span></span>

<span data-ttu-id="0854a-139">Il connettore Decode EDIFACT esegue queste attività:</span><span class="sxs-lookup"><span data-stu-id="0854a-139">The Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="0854a-140">Convalida la busta in base all'accordo tra partner commerciali.</span><span class="sxs-lookup"><span data-stu-id="0854a-140">Validates the envelope against trading partner agreement.</span></span>
* <span data-ttu-id="0854a-141">Risolve il contratto associando qualificatore del mittente e identificatore e qualificatore del ricevitore e identificatore.</span><span class="sxs-lookup"><span data-stu-id="0854a-141">Resolves the agreement by matching the sender qualifier & identifier and receiver qualifier & identifier.</span></span>
* <span data-ttu-id="0854a-142">Suddivide un interscambio in più transazioni quando l'interscambio ha più di una transazione basata sulla configurazione delle impostazioni di ricezione dell'accordo.</span><span class="sxs-lookup"><span data-stu-id="0854a-142">Splits an interchange into multiple transactions when the interchange has more than one transaction based on the agreement's receive settings configuration.</span></span>
* <span data-ttu-id="0854a-143">Disassembla l'interscambio.</span><span class="sxs-lookup"><span data-stu-id="0854a-143">Disassembles the interchange.</span></span>
* <span data-ttu-id="0854a-144">Convalida le proprietà EDI e specifiche del partner, comprese:</span><span class="sxs-lookup"><span data-stu-id="0854a-144">Validates EDI and partner-specific properties including:</span></span>
  * <span data-ttu-id="0854a-145">Convalida della struttura della busta dell'interscambio</span><span class="sxs-lookup"><span data-stu-id="0854a-145">Validation of the interchange envelope structure</span></span>
  * <span data-ttu-id="0854a-146">Convalida dello schema della busta in base allo schema di controllo</span><span class="sxs-lookup"><span data-stu-id="0854a-146">Schema validation of the envelope against the control schema</span></span>
  * <span data-ttu-id="0854a-147">Convalida dello schema degli elementi dati del set di transazioni rispetto allo schema del messaggio</span><span class="sxs-lookup"><span data-stu-id="0854a-147">Schema validation of the transaction-set data elements against the message schema</span></span>
  * <span data-ttu-id="0854a-148">Convalida EDI eseguita sugli elementi dati del set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="0854a-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="0854a-149">Verifica che i numeri di controllo di un set di interscambio, gruppo e di transazioni non siano duplicati (se configurata).</span><span class="sxs-lookup"><span data-stu-id="0854a-149">Verifies that the interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="0854a-150">Controlla il numero di controllo dell'interscambio rispetto agli interscambi ricevuti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0854a-150">Checks the interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="0854a-151">Controlla il numero di controllo del gruppo con gli altri numeri di controllo del gruppo dell'interscambio.</span><span class="sxs-lookup"><span data-stu-id="0854a-151">Checks the group control number against other group control numbers in the interchange.</span></span> 
  * <span data-ttu-id="0854a-152">Controlla il numero di controllo del set di transazioni con gli altri numeri di controllo del set transazioni in tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="0854a-152">Checks the transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="0854a-153">Suddivide l'interscambio in set di transazioni o mantiene l'intero interscambio:</span><span class="sxs-lookup"><span data-stu-id="0854a-153">Splits the interchange into transaction sets, or preserves the entire interchange:</span></span>
  * <span data-ttu-id="0854a-154">Suddivide l'interscambio in set di transazioni - sospende i set di transazioni in caso di errore: suddivide l'interscambio in set di transazioni e analizza ogni set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="0854a-154">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="0854a-155">L'azione X12 Decode restituisce solo i set di transazioni che non sono stati convalidati in `badMessages` e restituisce i restanti set di transazioni in `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="0854a-155">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="0854a-156">Suddivide l'interscambio in set di transazioni - sospende l'interscambio in caso di errore: suddivide l'interscambio in set di transazioni e analizza ogni set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="0854a-156">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="0854a-157">Se la convalida di uno o più set di transazioni dell'interscambio non riesce, l'azione X12 Decode restituisce tutti i set di transazioni in quell'interscambio in `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="0854a-157">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
  * <span data-ttu-id="0854a-158">Mantiene l'interscambio - sospende i set transazioni in caso di errore: mantiene l'interscambio ed elabora l'intero interscambio in batch.</span><span class="sxs-lookup"><span data-stu-id="0854a-158">Preserve Interchange - suspend transaction sets on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="0854a-159">L'azione X12 Decode restituisce solo i set di transazioni che non sono stati convalidati in `badMessages` e restituisce i restanti set di transazioni in `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="0854a-159">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="0854a-160">Mantiene l'interscambio - sospende l'interscambio in caso di errore: mantiene l'interscambio ed elabora l'intero interscambio in batch.</span><span class="sxs-lookup"><span data-stu-id="0854a-160">Preserve Interchange - suspend interchange on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="0854a-161">Se la convalida di uno o più set di transazioni dell'interscambio non riesce, l'azione X12 Decode restituisce tutti i set di transazioni in quell'interscambio in `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="0854a-161">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
* <span data-ttu-id="0854a-162">Genera un riconoscimento tecnico (controllo) e/o funzionale (se configurata).</span><span class="sxs-lookup"><span data-stu-id="0854a-162">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="0854a-163">Un riconoscimento tecnico o CONTRL ACK segnala i risultati di un controllo sintattico dell'interscambio completo ricevuto.</span><span class="sxs-lookup"><span data-stu-id="0854a-163">A Technical Acknowledgment or the CONTRL ACK reports the results of a syntactical check of the complete received interchange.</span></span>
  * <span data-ttu-id="0854a-164">Un riconoscimento funzionale riconosce l'accettazione o il rifiuto di un interscambio o un gruppo ricevuto.</span><span class="sxs-lookup"><span data-stu-id="0854a-164">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="0854a-165">Visualizzare il file Swagger</span><span class="sxs-lookup"><span data-stu-id="0854a-165">View Swagger file</span></span>
<span data-ttu-id="0854a-166">Per visualizzare i dettagli di Swagger per il connettore EDIFACT, vedere [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="0854a-166">To view the Swagger details for the EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0854a-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0854a-167">Next steps</span></span>
[<span data-ttu-id="0854a-168">Altre informazioni su Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="0854a-168">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Informazioni su Enterprise Integration Pack") 


---
title: i messaggi EDIFACT aaaDecode - App Azure per la logica | Documenti Microsoft
description: Convalida EDI e generare i riconoscimenti con decodificatore messaggio EDIFACT di hello in hello Enterprise Integration Pack per le app di logica di Azure
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
ms.openlocfilehash: 94faebdec4e4ffc8ad76ad1609495ddf9f002250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="60e69-103">Decodificare i messaggi EDIFACT per le app di Azure logica con hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="60e69-103">Decode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="60e69-104">Con connettore di messaggi hello decodificare EDIFACT, si può convalidare EDI e proprietà specifiche del partner, suddividere gli interscambi in set di transazioni o mantenere gli interscambi intera e generare riconoscimenti per transazioni elaborate.</span><span class="sxs-lookup"><span data-stu-id="60e69-104">With hello Decode EDIFACT message connector, you can validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="60e69-105">toouse questo connettore, è necessario aggiungere hello connettore tooan trigger nell'app logica esistente.</span><span class="sxs-lookup"><span data-stu-id="60e69-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="60e69-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="60e69-106">Before you start</span></span>

<span data-ttu-id="60e69-107">Ecco gli elementi di hello che è necessario:</span><span class="sxs-lookup"><span data-stu-id="60e69-107">Here's hello items you need:</span></span>

* <span data-ttu-id="60e69-108">Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="60e69-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="60e69-109">Un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md) già definito e associato alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="60e69-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="60e69-110">È necessario disporre di un connettore di messaggio integrazione account toouse hello decodificare EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="60e69-110">You must have an integration account toouse hello Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="60e69-111">Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="60e69-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="60e69-112">Un [contratto EDIFACT](logic-apps-enterprise-integration-edifact.md) già definito nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="60e69-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="60e69-113">Decodificare messaggi EDIFACT</span><span class="sxs-lookup"><span data-stu-id="60e69-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="60e69-114">[Creare un'app per la logica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="60e69-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="60e69-115">connettore di messaggi Hello decodificare EDIFACT non dispone di trigger, pertanto è necessario aggiungere un trigger per avviare l'app di logica, ad esempio un trigger di richiesta.</span><span class="sxs-lookup"><span data-stu-id="60e69-115">hello Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="60e69-116">Nella finestra di progettazione logica App hello, aggiungere un trigger e quindi aggiungere un'app di logica di azione tooyour.</span><span class="sxs-lookup"><span data-stu-id="60e69-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3. <span data-ttu-id="60e69-117">Nella casella di ricerca hello, immettere "EDIFACT" come filtro.</span><span class="sxs-lookup"><span data-stu-id="60e69-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="60e69-118">Selezionare **Decodifica il messaggio EDIFACT**.</span><span class="sxs-lookup"><span data-stu-id="60e69-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![ricerca di EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="60e69-120">Se è stato creato in precedenza tutte le connessioni tooyour account di integrazione, viene chiesto toocreate ora tale connessione.</span><span class="sxs-lookup"><span data-stu-id="60e69-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="60e69-121">Nome della connessione, quindi selezionare account di integrazione hello che si desidera tooconnect.</span><span class="sxs-lookup"><span data-stu-id="60e69-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![creare un account di integrazione](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="60e69-123">Le proprietà con l'asterisco sono obbligatorie.</span><span class="sxs-lookup"><span data-stu-id="60e69-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="60e69-124">Proprietà</span><span class="sxs-lookup"><span data-stu-id="60e69-124">Property</span></span> | <span data-ttu-id="60e69-125">Dettagli</span><span class="sxs-lookup"><span data-stu-id="60e69-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="60e69-126">Nome connessione *</span><span class="sxs-lookup"><span data-stu-id="60e69-126">Connection Name *</span></span> |<span data-ttu-id="60e69-127">Immettere un nome per la connessione.</span><span class="sxs-lookup"><span data-stu-id="60e69-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="60e69-128">Account di integrazione *</span><span class="sxs-lookup"><span data-stu-id="60e69-128">Integration Account *</span></span> |<span data-ttu-id="60e69-129">Immettere un nome per l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="60e69-129">Enter a name for your integration account.</span></span> <span data-ttu-id="60e69-130">Assicurarsi che l'app di account e la logica di integrazione siano hello nello stesso percorso di Azure.</span><span class="sxs-lookup"><span data-stu-id="60e69-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

4. <span data-ttu-id="60e69-131">Al termine della creazione della connessione toofinish, scegliere **crea**.</span><span class="sxs-lookup"><span data-stu-id="60e69-131">When you're done toofinish creating your connection, choose **Create**.</span></span> <span data-ttu-id="60e69-132">Dettagli relativi alla connessione dovrebbero essere simile toothis esempio:</span><span class="sxs-lookup"><span data-stu-id="60e69-132">Your connection details should look similar toothis example:</span></span>

    ![dettagli dell'account di integrazione](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="60e69-134">Dopo aver creata la connessione, come illustrato in questo esempio, selezionare toodecode messaggio file flat di hello EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="60e69-134">After your connection is created, as shown in this example, select hello EDIFACT flat file message toodecode.</span></span>

    ![connessione all'account di integrazione creata](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="60e69-136">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="60e69-136">For example:</span></span>

    ![Selezionare il messaggio con il file flat EDIFACT da decodificare](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="60e69-138">Dettagli decodificatore EDIFACT</span><span class="sxs-lookup"><span data-stu-id="60e69-138">EDIFACT decoder details</span></span>

<span data-ttu-id="60e69-139">connettore di decodificare EDIFACT Hello esegue queste attività:</span><span class="sxs-lookup"><span data-stu-id="60e69-139">hello Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="60e69-140">Convalida la busta hello contro l'accordo tra partner commerciali.</span><span class="sxs-lookup"><span data-stu-id="60e69-140">Validates hello envelope against trading partner agreement.</span></span>
* <span data-ttu-id="60e69-141">Risolve l'accordo hello associando qualificatore mittente hello & identificatore qualificatore ricevitore e identificatore.</span><span class="sxs-lookup"><span data-stu-id="60e69-141">Resolves hello agreement by matching hello sender qualifier & identifier and receiver qualifier & identifier.</span></span>
* <span data-ttu-id="60e69-142">Suddivide un interscambio in più transazioni quando interscambio hello ha più di una transazione in base hello del contratto di configurazione delle impostazioni di ricezione.</span><span class="sxs-lookup"><span data-stu-id="60e69-142">Splits an interchange into multiple transactions when hello interchange has more than one transaction based on hello agreement's receive settings configuration.</span></span>
* <span data-ttu-id="60e69-143">Disassembla l'interscambio hello.</span><span class="sxs-lookup"><span data-stu-id="60e69-143">Disassembles hello interchange.</span></span>
* <span data-ttu-id="60e69-144">Convalida le proprietà EDI e specifiche del partner, comprese:</span><span class="sxs-lookup"><span data-stu-id="60e69-144">Validates EDI and partner-specific properties including:</span></span>
  * <span data-ttu-id="60e69-145">Convalida della struttura di busta interscambio hello</span><span class="sxs-lookup"><span data-stu-id="60e69-145">Validation of hello interchange envelope structure</span></span>
  * <span data-ttu-id="60e69-146">Convalida dello schema della busta hello rispetto allo schema di controllo hello</span><span class="sxs-lookup"><span data-stu-id="60e69-146">Schema validation of hello envelope against hello control schema</span></span>
  * <span data-ttu-id="60e69-147">Convalida dello schema di elementi di dati di set di transazioni hello rispetto allo schema di messaggio hello</span><span class="sxs-lookup"><span data-stu-id="60e69-147">Schema validation of hello transaction-set data elements against hello message schema</span></span>
  * <span data-ttu-id="60e69-148">Convalida EDI eseguita sugli elementi dati del set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="60e69-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="60e69-149">Verifica che hello interscambio, gruppo e transazioni set di numeri di controllo non siano duplicati (se configurata)</span><span class="sxs-lookup"><span data-stu-id="60e69-149">Verifies that hello interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="60e69-150">Verifica numero di controllo di interscambio hello con gli interscambi ricevuti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="60e69-150">Checks hello interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="60e69-151">Verifica numero di controllo gruppo hello con gli altri numeri di controllo di gruppo nell'interscambio hello.</span><span class="sxs-lookup"><span data-stu-id="60e69-151">Checks hello group control number against other group control numbers in hello interchange.</span></span> 
  * <span data-ttu-id="60e69-152">Controlla il numero di controllo del set di transazioni hello con gli altri numeri di controllo set transazioni in tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="60e69-152">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="60e69-153">Suddivide hello interscambio in set di transazioni o mantiene hello intero interscambio:</span><span class="sxs-lookup"><span data-stu-id="60e69-153">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="60e69-154">Suddivide l'interscambio in set di transazioni - sospende i set di transazioni in caso di errore: suddivide l'interscambio in set di transazioni e analizza ogni set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="60e69-154">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="60e69-155">azione di decodifica Hello X12 restituisce solo i set di transazioni che non superano la convalida troppo`badMessages`e restituisce hello transazioni rimanenti imposta troppo`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="60e69-155">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="60e69-156">Suddivide l'interscambio in set di transazioni - sospende l'interscambio in caso di errore: suddivide l'interscambio in set di transazioni e analizza ogni set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="60e69-156">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="60e69-157">Se i set di convalida non riuscita di interscambio hello uno o più transazioni, l'azione Decode hello X12 output tutti hello set di transazioni nell'interscambio troppo`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="60e69-157">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="60e69-158">Mantieni interscambio - Sospendi set transazioni in caso di errore: interscambio hello Preserve e processo hello intero interscambio in batch.</span><span class="sxs-lookup"><span data-stu-id="60e69-158">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="60e69-159">azione di decodifica Hello X12 restituisce solo i set di transazioni che non superano la convalida troppo`badMessages`e restituisce hello transazioni rimanenti imposta troppo`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="60e69-159">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="60e69-160">Mantieni interscambio - Sospendi interscambio in caso di errore: interscambio hello Preserve e processo hello intero interscambio in batch.</span><span class="sxs-lookup"><span data-stu-id="60e69-160">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="60e69-161">Se i set di convalida non riuscita di interscambio hello uno o più transazioni, l'azione Decode hello X12 output tutti hello set di transazioni nell'interscambio troppo`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="60e69-161">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
* <span data-ttu-id="60e69-162">Genera un riconoscimento tecnico (controllo) e/o funzionale (se configurata).</span><span class="sxs-lookup"><span data-stu-id="60e69-162">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="60e69-163">Un riconoscimento tecnico o hello ACK CONTRL segnala i risultati di hello di un controllo sintattico dell'interscambio ricevuto hello completo.</span><span class="sxs-lookup"><span data-stu-id="60e69-163">A Technical Acknowledgment or hello CONTRL ACK reports hello results of a syntactical check of hello complete received interchange.</span></span>
  * <span data-ttu-id="60e69-164">Un riconoscimento funzionale riconosce l'accettazione o il rifiuto di un interscambio o un gruppo ricevuto.</span><span class="sxs-lookup"><span data-stu-id="60e69-164">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="60e69-165">Visualizzare il file Swagger</span><span class="sxs-lookup"><span data-stu-id="60e69-165">View Swagger file</span></span>
<span data-ttu-id="60e69-166">vedere i dettagli di Swagger hello tooview per connettore EDIFACT hello, [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="60e69-166">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="60e69-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="60e69-167">Next steps</span></span>
[<span data-ttu-id="60e69-168">Altre informazioni su Enterprise Integration Pack hello</span><span class="sxs-lookup"><span data-stu-id="60e69-168">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack") 


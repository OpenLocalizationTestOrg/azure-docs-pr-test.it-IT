---
title: i messaggi X12 aaaDecode - App Azure per la logica | Documenti Microsoft
description: Convalida EDI e generare i riconoscimenti con decodificatore messaggio hello X12 in hello Enterprise Integration Pack per le app di logica di Azure
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
ms.openlocfilehash: 1ffececca1ff835b319b64c85f86c421395833c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="2f35f-103">Decodificare X12 messaggi per le app di Azure logica con hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="2f35f-103">Decode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="2f35f-104">Con connettore di messaggi hello Decode X12, è possibile convalidare la busta hello contro un accordo tra partner commerciali, la convalida EDI e proprietà specifiche del partner, suddividere gli interscambi in set di transazioni o mantenere gli interscambi intera e generare Riconoscimenti per transazioni elaborate.</span><span class="sxs-lookup"><span data-stu-id="2f35f-104">With hello Decode X12 message connector, you can validate hello envelope against a trading partner agreement, validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="2f35f-105">toouse questo connettore, è necessario aggiungere hello connettore tooan trigger nell'app logica esistente.</span><span class="sxs-lookup"><span data-stu-id="2f35f-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="2f35f-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="2f35f-106">Before you start</span></span>

<span data-ttu-id="2f35f-107">Ecco gli elementi di hello che è necessario:</span><span class="sxs-lookup"><span data-stu-id="2f35f-107">Here's hello items you need:</span></span>

* <span data-ttu-id="2f35f-108">Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="2f35f-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="2f35f-109">Un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md) già definito e associato alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2f35f-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="2f35f-110">È necessario disporre di un connettore di messaggio integrazione account toouse hello Decode X12.</span><span class="sxs-lookup"><span data-stu-id="2f35f-110">You must have an integration account toouse hello Decode X12 message connector.</span></span>
* <span data-ttu-id="2f35f-111">Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="2f35f-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="2f35f-112">Un [contratto X12](logic-apps-enterprise-integration-x12.md) già definito nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="2f35f-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="decode-x12-messages"></a><span data-ttu-id="2f35f-113">Messaggi Decode X12</span><span class="sxs-lookup"><span data-stu-id="2f35f-113">Decode X12 messages</span></span>

1. <span data-ttu-id="2f35f-114">[Creare un'app per la logica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="2f35f-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="2f35f-115">connettore di messaggi Hello Decode X12 non dispone di trigger, pertanto è necessario aggiungere un trigger per avviare l'app di logica, ad esempio un trigger di richiesta.</span><span class="sxs-lookup"><span data-stu-id="2f35f-115">hello Decode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="2f35f-116">Nella finestra di progettazione logica App hello, aggiungere un trigger e quindi aggiungere un'app di logica di azione tooyour.</span><span class="sxs-lookup"><span data-stu-id="2f35f-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="2f35f-117">Nella casella di ricerca hello, immettere "x12" per il filtro.</span><span class="sxs-lookup"><span data-stu-id="2f35f-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="2f35f-118">Selezionare **X12 - Decodifica il messaggio X12**.</span><span class="sxs-lookup"><span data-stu-id="2f35f-118">Select **X12 - Decode X12 message**.</span></span>
   
    ![Cercare "X12"](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. <span data-ttu-id="2f35f-120">Se è stato creato in precedenza tutte le connessioni tooyour account di integrazione, viene chiesto toocreate ora tale connessione.</span><span class="sxs-lookup"><span data-stu-id="2f35f-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="2f35f-121">Nome della connessione, quindi selezionare account di integrazione hello che si desidera tooconnect.</span><span class="sxs-lookup"><span data-stu-id="2f35f-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 

    ![Fornire i dettagli della connessione all'account di integrazione](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    <span data-ttu-id="2f35f-123">Le proprietà con l'asterisco sono obbligatorie.</span><span class="sxs-lookup"><span data-stu-id="2f35f-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="2f35f-124">Proprietà</span><span class="sxs-lookup"><span data-stu-id="2f35f-124">Property</span></span> | <span data-ttu-id="2f35f-125">Dettagli</span><span class="sxs-lookup"><span data-stu-id="2f35f-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="2f35f-126">Nome connessione *</span><span class="sxs-lookup"><span data-stu-id="2f35f-126">Connection Name *</span></span> |<span data-ttu-id="2f35f-127">Immettere un nome per la connessione.</span><span class="sxs-lookup"><span data-stu-id="2f35f-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="2f35f-128">Account di integrazione *</span><span class="sxs-lookup"><span data-stu-id="2f35f-128">Integration Account *</span></span> |<span data-ttu-id="2f35f-129">Immettere un nome per l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="2f35f-129">Enter a name for your integration account.</span></span> <span data-ttu-id="2f35f-130">Assicurarsi che l'app di account e la logica di integrazione siano hello nello stesso percorso di Azure.</span><span class="sxs-lookup"><span data-stu-id="2f35f-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="2f35f-131">Al termine, i dettagli relativi alla connessione dovrebbero essere simile toothis esempio.</span><span class="sxs-lookup"><span data-stu-id="2f35f-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="2f35f-132">toofinish della creazione della connessione, scegliere **crea**.</span><span class="sxs-lookup"><span data-stu-id="2f35f-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![dettagli della connessione all'account di integrazione](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. <span data-ttu-id="2f35f-134">Dopo aver creata la connessione, come illustrato in questo esempio, selezionare toodecode messaggio file flat di hello X12.</span><span class="sxs-lookup"><span data-stu-id="2f35f-134">After your connection is created, as shown in this example, select hello X12 flat file message toodecode.</span></span>

    ![connessione all'account di integrazione creata](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    <span data-ttu-id="2f35f-136">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2f35f-136">For example:</span></span>

    ![Selezionare il messaggio con il file flat X12 da decodificare](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a><span data-ttu-id="2f35f-138">Dettagli Decode X12</span><span class="sxs-lookup"><span data-stu-id="2f35f-138">X12 Decode details</span></span>

<span data-ttu-id="2f35f-139">connettore Decode Hello X12 esegue queste attività:</span><span class="sxs-lookup"><span data-stu-id="2f35f-139">hello X12 Decode connector performs these tasks:</span></span>

* <span data-ttu-id="2f35f-140">Convalida la busta hello contro l'accordo tra partner commerciali</span><span class="sxs-lookup"><span data-stu-id="2f35f-140">Validates hello envelope against trading partner agreement</span></span>
* <span data-ttu-id="2f35f-141">Convalida le proprietà EDI e specifiche del partner.</span><span class="sxs-lookup"><span data-stu-id="2f35f-141">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="2f35f-142">Convalida strutturale EDI e convalida estesa dello schema.</span><span class="sxs-lookup"><span data-stu-id="2f35f-142">EDI structural validation, and extended schema validation</span></span>
  * <span data-ttu-id="2f35f-143">Convalida della struttura di hello della busta dell'interscambio hello.</span><span class="sxs-lookup"><span data-stu-id="2f35f-143">Validation of hello structure of hello interchange envelope.</span></span>
  * <span data-ttu-id="2f35f-144">Convalida dello schema della busta hello rispetto allo schema di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="2f35f-144">Schema validation of hello envelope against hello control schema.</span></span>
  * <span data-ttu-id="2f35f-145">Convalida dello schema di elementi di dati di set di transazioni hello rispetto allo schema di messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="2f35f-145">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="2f35f-146">Convalida EDI eseguita sugli elementi dati del set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="2f35f-146">EDI validation performed on transaction-set data elements</span></span> 
* <span data-ttu-id="2f35f-147">Verifica che hello interscambio, gruppo e transazioni set di numeri di controllo non siano duplicati</span><span class="sxs-lookup"><span data-stu-id="2f35f-147">Verifies that hello interchange, group, and transaction set control numbers are not duplicates</span></span>
  * <span data-ttu-id="2f35f-148">Verifica numero di controllo di interscambio hello con gli interscambi ricevuti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f35f-148">Checks hello interchange control number against previously received interchanges.</span></span>
  * <span data-ttu-id="2f35f-149">Verifica numero di controllo gruppo hello con gli altri numeri di controllo di gruppo nell'interscambio hello.</span><span class="sxs-lookup"><span data-stu-id="2f35f-149">Checks hello group control number against other group control numbers in hello interchange.</span></span>
  * <span data-ttu-id="2f35f-150">Controlla il numero di controllo del set di transazioni hello con gli altri numeri di controllo set transazioni in tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="2f35f-150">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="2f35f-151">Suddivide hello interscambio in set di transazioni o mantiene hello intero interscambio:</span><span class="sxs-lookup"><span data-stu-id="2f35f-151">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="2f35f-152">Suddivide l'interscambio in set di transazioni - sospende i set di transazioni in caso di errore: suddivide l'interscambio in set di transazioni e analizza ogni set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="2f35f-152">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="2f35f-153">azione di decodifica Hello X12 restituisce solo i set di transazioni che non superano la convalida troppo`badMessages`e restituisce hello transazioni rimanenti imposta troppo`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="2f35f-153">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="2f35f-154">Suddivide l'interscambio in set di transazioni - sospende l'interscambio in caso di errore: suddivide l'interscambio in set di transazioni e analizza ogni set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="2f35f-154">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="2f35f-155">Se i set di convalida non riuscita di interscambio hello uno o più transazioni, l'azione Decode hello X12 output tutti hello set di transazioni nell'interscambio troppo`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="2f35f-155">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="2f35f-156">Mantieni interscambio - Sospendi set transazioni in caso di errore: interscambio hello Preserve e processo hello intero interscambio in batch.</span><span class="sxs-lookup"><span data-stu-id="2f35f-156">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="2f35f-157">azione di decodifica Hello X12 restituisce solo i set di transazioni che non superano la convalida troppo`badMessages`e restituisce hello transazioni rimanenti imposta troppo`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="2f35f-157">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="2f35f-158">Mantieni interscambio - Sospendi interscambio in caso di errore: interscambio hello Preserve e processo hello intero interscambio in batch.</span><span class="sxs-lookup"><span data-stu-id="2f35f-158">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="2f35f-159">Se i set di convalida non riuscita di interscambio hello uno o più transazioni, l'azione Decode hello X12 output tutti hello set di transazioni nell'interscambio troppo`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="2f35f-159">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span> 
* <span data-ttu-id="2f35f-160">Genera un riconoscimento tecnico e/o funzionale (se configurata).</span><span class="sxs-lookup"><span data-stu-id="2f35f-160">Generates a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="2f35f-161">Un riconoscimento tecnico viene generato in seguito alla convalida dell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="2f35f-161">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="2f35f-162">Hello riconoscimento tecnico segnala hello lo stato di elaborazione hello di un'intestazione di interscambio e trailer da ricevitore dell'indirizzo hello.</span><span class="sxs-lookup"><span data-stu-id="2f35f-162">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver.</span></span>
  * <span data-ttu-id="2f35f-163">Un riconoscimento funzionale viene generato in seguito alla convalida del corpo.</span><span class="sxs-lookup"><span data-stu-id="2f35f-163">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="2f35f-164">riconoscimento funzionale Hello segnala ogni errore rilevato durante l'elaborazione di hello ricevuto documento</span><span class="sxs-lookup"><span data-stu-id="2f35f-164">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="2f35f-165">Swagger hello vista</span><span class="sxs-lookup"><span data-stu-id="2f35f-165">View hello swagger</span></span>
<span data-ttu-id="2f35f-166">Vedere hello [swagger dettagli](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="2f35f-166">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2f35f-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2f35f-167">Next steps</span></span>
[<span data-ttu-id="2f35f-168">Altre informazioni su Enterprise Integration Pack hello</span><span class="sxs-lookup"><span data-stu-id="2f35f-168">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack") 


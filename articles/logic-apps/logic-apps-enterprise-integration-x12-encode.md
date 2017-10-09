---
title: i messaggi X12 aaaEncode - App Azure per la logica | Documenti Microsoft
description: Convalida EDI e convertire codificata in formato XML con X12 di messaggio del codificatore in hello Enterprise Integration Pack per le app di logica di Azure
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
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="232c9-103">La codifica X12 i messaggi per le app di Azure logica con hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="232c9-103">Encode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="232c9-104">Con connettore di messaggi hello codifica X12, è possibile convalidare EDI e proprietà specifiche del partner, convertire i messaggi con codifica XML in set di transazioni EDI nell'interscambio hello e richiedere un riconoscimento tecnico, il riconoscimento funzionale o entrambi.</span><span class="sxs-lookup"><span data-stu-id="232c9-104">With hello Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in hello interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="232c9-105">toouse questo connettore, è necessario aggiungere hello connettore tooan trigger nell'app logica esistente.</span><span class="sxs-lookup"><span data-stu-id="232c9-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="232c9-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="232c9-106">Before you start</span></span>

<span data-ttu-id="232c9-107">Ecco gli elementi di hello che è necessario:</span><span class="sxs-lookup"><span data-stu-id="232c9-107">Here's hello items you need:</span></span>

* <span data-ttu-id="232c9-108">Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="232c9-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="232c9-109">Un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md) già definito e associato alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="232c9-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="232c9-110">È necessario disporre di un connettore di messaggio integrazione account toouse hello codifica X12.</span><span class="sxs-lookup"><span data-stu-id="232c9-110">You must have an integration account toouse hello Encode X12 message connector.</span></span>
* <span data-ttu-id="232c9-111">Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="232c9-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="232c9-112">Un [contratto X12](logic-apps-enterprise-integration-x12.md) già definito nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="232c9-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="232c9-113">Messaggi Encode X12</span><span class="sxs-lookup"><span data-stu-id="232c9-113">Encode X12 messages</span></span>

1. <span data-ttu-id="232c9-114">[Creare un'app per la logica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="232c9-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="232c9-115">connettore di messaggi Hello codifica X12 non dispone di trigger, pertanto è necessario aggiungere un trigger per avviare l'app di logica, ad esempio un trigger di richiesta.</span><span class="sxs-lookup"><span data-stu-id="232c9-115">hello Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="232c9-116">Nella finestra di progettazione logica App hello, aggiungere un trigger e quindi aggiungere un'app di logica di azione tooyour.</span><span class="sxs-lookup"><span data-stu-id="232c9-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="232c9-117">Nella casella di ricerca hello, immettere "x12" per il filtro.</span><span class="sxs-lookup"><span data-stu-id="232c9-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="232c9-118">Selezionare l'opzione **X12-codificare tooX12 messaggio in base al nome di contratto** o **X12-codificare il messaggio tooX12 dalle identità**.</span><span class="sxs-lookup"><span data-stu-id="232c9-118">Select either **X12 - Encode tooX12 message by agreement name** or **X12 - Encode tooX12 message by identities**.</span></span>
   
    ![Cercare "X12"](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="232c9-120">Se è stato creato in precedenza tutte le connessioni tooyour account di integrazione, viene chiesto toocreate ora tale connessione.</span><span class="sxs-lookup"><span data-stu-id="232c9-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="232c9-121">Nome della connessione, quindi selezionare account di integrazione hello che si desidera tooconnect.</span><span class="sxs-lookup"><span data-stu-id="232c9-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![connessione all'account di integrazione](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="232c9-123">Le proprietà con l'asterisco sono obbligatorie.</span><span class="sxs-lookup"><span data-stu-id="232c9-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="232c9-124">Proprietà</span><span class="sxs-lookup"><span data-stu-id="232c9-124">Property</span></span> | <span data-ttu-id="232c9-125">Dettagli</span><span class="sxs-lookup"><span data-stu-id="232c9-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="232c9-126">Nome connessione *</span><span class="sxs-lookup"><span data-stu-id="232c9-126">Connection Name *</span></span> |<span data-ttu-id="232c9-127">Immettere un nome per la connessione.</span><span class="sxs-lookup"><span data-stu-id="232c9-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="232c9-128">Account di integrazione *</span><span class="sxs-lookup"><span data-stu-id="232c9-128">Integration Account *</span></span> |<span data-ttu-id="232c9-129">Immettere un nome per l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="232c9-129">Enter a name for your integration account.</span></span> <span data-ttu-id="232c9-130">Assicurarsi che l'app di account e la logica di integrazione siano hello nello stesso percorso di Azure.</span><span class="sxs-lookup"><span data-stu-id="232c9-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="232c9-131">Al termine, i dettagli relativi alla connessione dovrebbero essere simile toothis esempio.</span><span class="sxs-lookup"><span data-stu-id="232c9-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="232c9-132">toofinish della creazione della connessione, scegliere **crea**.</span><span class="sxs-lookup"><span data-stu-id="232c9-132">toofinish creating your connection, choose **Create**.</span></span>

    ![connessione all'account di integrazione creata](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="232c9-134">La connessione è stata creata.</span><span class="sxs-lookup"><span data-stu-id="232c9-134">Your connection is now created.</span></span>

    ![dettagli della connessione all'account di integrazione](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="232c9-136">Encode X12 Message by agreement name (Messaggio Encode X12 per nome contratto)</span><span class="sxs-lookup"><span data-stu-id="232c9-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="232c9-137">Se si sceglie tooencode X12 messaggi in base al nome di contratto, aprire hello **nome X12 contratto** elenco, immettere o selezionare il X12 esistente contratto.</span><span class="sxs-lookup"><span data-stu-id="232c9-137">If you chose tooencode X12 messages by agreement name, open hello **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="232c9-138">Immettere tooencode di messaggio hello XML.</span><span class="sxs-lookup"><span data-stu-id="232c9-138">Enter hello XML message tooencode.</span></span>

![Immettere X12 tooencode dei messaggi XML e nome contratto](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="232c9-140">Encode X12 Message by identities (Messaggio Encode X12 per identità)</span><span class="sxs-lookup"><span data-stu-id="232c9-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="232c9-141">Se si sceglie tooencode X12 messaggi dalle identità, immettere l'identificatore hello del mittente, qualificatore mittente, identificatore del ricevitore e qualificatore ricevitore come configurato nel X12 contratto.</span><span class="sxs-lookup"><span data-stu-id="232c9-141">If you choose tooencode X12 messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="232c9-142">Selezionare tooencode di messaggio hello XML.</span><span class="sxs-lookup"><span data-stu-id="232c9-142">Select hello XML message tooencode.</span></span>
   
![Fornire le identità per il mittente e destinatario, selezionare tooencode messaggio XML](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="232c9-144">Dettagli di Encode X12</span><span class="sxs-lookup"><span data-stu-id="232c9-144">X12 Encode details</span></span>

<span data-ttu-id="232c9-145">connettore di codifica X12 Hello esegue queste attività:</span><span class="sxs-lookup"><span data-stu-id="232c9-145">hello X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="232c9-146">Risoluzione del contratto associando le proprietà del contesto di mittente e del destinatario.</span><span class="sxs-lookup"><span data-stu-id="232c9-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="232c9-147">Serializza l'interscambio EDI hello, conversione dei messaggi con codifica XML in set di transazioni EDI nell'interscambio hello.</span><span class="sxs-lookup"><span data-stu-id="232c9-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="232c9-148">Si applica ai segmenti di intestazione e finali del set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="232c9-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="232c9-149">Genera un numero di controllo di interscambio, un numero di controllo di gruppo e un numero di controllo del set di transazioni per ogni interscambio in uscita.</span><span class="sxs-lookup"><span data-stu-id="232c9-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="232c9-150">Sostituisce i separatori nei dati di payload hello</span><span class="sxs-lookup"><span data-stu-id="232c9-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="232c9-151">Convalida le proprietà EDI e specifiche del partner.</span><span class="sxs-lookup"><span data-stu-id="232c9-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="232c9-152">Convalida dello schema di elementi di dati di set di transazioni hello rispetto al messaggio hello dello Schema</span><span class="sxs-lookup"><span data-stu-id="232c9-152">Schema validation of hello transaction-set data elements against hello message Schema</span></span>
  * <span data-ttu-id="232c9-153">Convalida EDI eseguita sugli elementi dati del set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="232c9-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="232c9-154">Convalida estesa eseguita sugli elementi dati del set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="232c9-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="232c9-155">Richiede un riconoscimento tecnico e/o funzionale (se configurata).</span><span class="sxs-lookup"><span data-stu-id="232c9-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="232c9-156">Un riconoscimento tecnico viene generato in seguito alla convalida dell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="232c9-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="232c9-157">Hello riconoscimento tecnico segnala hello lo stato di elaborazione hello di un'intestazione di interscambio e trailer da ricevitore dell'indirizzo hello</span><span class="sxs-lookup"><span data-stu-id="232c9-157">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver</span></span>
  * <span data-ttu-id="232c9-158">Un riconoscimento funzionale viene generato in seguito alla convalida del corpo.</span><span class="sxs-lookup"><span data-stu-id="232c9-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="232c9-159">riconoscimento funzionale Hello segnala ogni errore rilevato durante l'elaborazione di hello ricevuto documento</span><span class="sxs-lookup"><span data-stu-id="232c9-159">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="232c9-160">Swagger hello vista</span><span class="sxs-lookup"><span data-stu-id="232c9-160">View hello swagger</span></span>
<span data-ttu-id="232c9-161">Vedere hello [swagger dettagli](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="232c9-161">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="232c9-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="232c9-162">Next steps</span></span>
[<span data-ttu-id="232c9-163">Altre informazioni su Enterprise Integration Pack hello</span><span class="sxs-lookup"><span data-stu-id="232c9-163">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack") 


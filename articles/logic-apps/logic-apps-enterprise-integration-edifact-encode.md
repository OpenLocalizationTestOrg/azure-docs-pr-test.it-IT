---
title: i messaggi EDIFACT aaaEncode - App Azure per la logica | Documenti Microsoft
description: Convalida EDI e generare codice XML con il codificatore di messaggi EDIFACT in hello Enterprise Integration Pack per le app di logica di Azure
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: b3799dbd2492adef597022d017cf28f5ceb1085c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="31298-103">Codificare i messaggi EDIFACT per le app di Azure logica con hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="31298-103">Encode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="31298-104">Con connettore di messaggi hello codifica EDIFACT, è possibile convalidare EDI e proprietà specifiche del partner, generare un documento XML per ogni set di transazioni e richiedere un riconoscimento tecnico, il riconoscimento funzionale o entrambi.</span><span class="sxs-lookup"><span data-stu-id="31298-104">With hello Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="31298-105">toouse questo connettore, è necessario aggiungere hello connettore tooan trigger nell'app logica esistente.</span><span class="sxs-lookup"><span data-stu-id="31298-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="31298-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="31298-106">Before you start</span></span>

<span data-ttu-id="31298-107">Ecco gli elementi di hello che è necessario:</span><span class="sxs-lookup"><span data-stu-id="31298-107">Here's hello items you need:</span></span>

* <span data-ttu-id="31298-108">Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="31298-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="31298-109">Un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md) già definito e associato alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="31298-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="31298-110">È necessario disporre di un connettore di messaggio integrazione account toouse hello codifica EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="31298-110">You must have an integration account toouse hello Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="31298-111">Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="31298-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="31298-112">Un [contratto EDIFACT](logic-apps-enterprise-integration-edifact.md) già definito nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="31298-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="31298-113">Codificare messaggi EDIFACT</span><span class="sxs-lookup"><span data-stu-id="31298-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="31298-114">[Creare un'app per la logica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="31298-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="31298-115">connettore di messaggi Hello codifica EDIFACT non dispone di trigger, pertanto è necessario aggiungere un trigger per avviare l'app di logica, ad esempio un trigger di richiesta.</span><span class="sxs-lookup"><span data-stu-id="31298-115">hello Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="31298-116">Nella finestra di progettazione logica App hello, aggiungere un trigger e quindi aggiungere un'app di logica di azione tooyour.</span><span class="sxs-lookup"><span data-stu-id="31298-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="31298-117">Nella casella di ricerca hello, immettere "EDIFACT" come filtro.</span><span class="sxs-lookup"><span data-stu-id="31298-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="31298-118">Selezionare l'opzione **codificare messaggio EDIFACT in base al nome di contratto** o **Encode tooEDIFACT messaggio dalle identità**.</span><span class="sxs-lookup"><span data-stu-id="31298-118">Select either **Encode EDIFACT Message by agreement name** or **Encode tooEDIFACT message by identities**.</span></span>
   
    ![ricerca di EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="31298-120">Se è stato creato in precedenza tutte le connessioni tooyour account di integrazione, viene chiesto toocreate ora tale connessione.</span><span class="sxs-lookup"><span data-stu-id="31298-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="31298-121">Nome della connessione, quindi selezionare account di integrazione hello che si desidera tooconnect.</span><span class="sxs-lookup"><span data-stu-id="31298-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>

    ![creare connessione all'account di integrazione](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="31298-123">Le proprietà con l'asterisco sono obbligatorie.</span><span class="sxs-lookup"><span data-stu-id="31298-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="31298-124">Proprietà</span><span class="sxs-lookup"><span data-stu-id="31298-124">Property</span></span> | <span data-ttu-id="31298-125">Dettagli</span><span class="sxs-lookup"><span data-stu-id="31298-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="31298-126">Nome connessione *</span><span class="sxs-lookup"><span data-stu-id="31298-126">Connection Name *</span></span> |<span data-ttu-id="31298-127">Immettere un nome per la connessione.</span><span class="sxs-lookup"><span data-stu-id="31298-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="31298-128">Account di integrazione *</span><span class="sxs-lookup"><span data-stu-id="31298-128">Integration Account *</span></span> |<span data-ttu-id="31298-129">Immettere un nome per l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="31298-129">Enter a name for your integration account.</span></span> <span data-ttu-id="31298-130">Assicurarsi che l'app di account e la logica di integrazione siano hello nello stesso percorso di Azure.</span><span class="sxs-lookup"><span data-stu-id="31298-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="31298-131">Al termine, i dettagli relativi alla connessione dovrebbero essere simile toothis esempio.</span><span class="sxs-lookup"><span data-stu-id="31298-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="31298-132">toofinish della creazione della connessione, scegliere **crea**.</span><span class="sxs-lookup"><span data-stu-id="31298-132">toofinish creating your connection, choose **Create**.</span></span>

    ![dettagli della connessione all'account di integrazione](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="31298-134">La connessione è stata creata.</span><span class="sxs-lookup"><span data-stu-id="31298-134">Your connection is now created.</span></span>

    ![connessione all'account di integrazione creata](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="31298-136">Encode EDIFACT Message by agreement name</span><span class="sxs-lookup"><span data-stu-id="31298-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="31298-137">Se si sceglie tooencode messaggi EDIFACT in base al nome di contratto, aprire hello **contratto nome di EDIFACT** elenco, immettere o selezionare il nome del contratto EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="31298-137">If you chose tooencode EDIFACT messages by agreement name, open hello **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="31298-138">Immettere tooencode di messaggio hello XML.</span><span class="sxs-lookup"><span data-stu-id="31298-138">Enter hello XML message tooencode.</span></span>

![Immettere il nome di contratto EDIFACT e tooencode messaggio XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="31298-140">Encode EDIFACT Message by identities</span><span class="sxs-lookup"><span data-stu-id="31298-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="31298-141">Se si sceglie tooencode messaggi EDIFACT per le identità, immettere l'identificatore hello del mittente, qualificatore mittente, identificatore del ricevitore e qualificatore ricevitore come configurato nel contratto EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="31298-141">If you choose tooencode EDIFACT messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="31298-142">Selezionare tooencode di messaggio hello XML.</span><span class="sxs-lookup"><span data-stu-id="31298-142">Select hello XML message tooencode.</span></span>

![Fornire le identità per il mittente e destinatario, selezionare tooencode messaggio XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="31298-144">Dettagli della codifica EDIFACT</span><span class="sxs-lookup"><span data-stu-id="31298-144">EDIFACT Encode details</span></span>

<span data-ttu-id="31298-145">connettore di codifica EDIFACT Hello esegue queste attività:</span><span class="sxs-lookup"><span data-stu-id="31298-145">hello Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="31298-146">Risoluzione hello accordo mediante corrispondenza hello qualificatore e identificatore e qualificatore ricevitore e identificatore mittente</span><span class="sxs-lookup"><span data-stu-id="31298-146">Resolve hello agreement by matching hello sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="31298-147">Serializza l'interscambio EDI hello, conversione dei messaggi con codifica XML in set di transazioni EDI nell'interscambio hello.</span><span class="sxs-lookup"><span data-stu-id="31298-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="31298-148">Si applica ai segmenti di intestazione e finali del set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="31298-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="31298-149">Genera un numero di controllo di interscambio, un numero di controllo di gruppo e un numero di controllo del set di transazioni per ogni interscambio in uscita.</span><span class="sxs-lookup"><span data-stu-id="31298-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="31298-150">Sostituisce i separatori nei dati di payload hello</span><span class="sxs-lookup"><span data-stu-id="31298-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="31298-151">Convalida le proprietà EDI e specifiche del partner.</span><span class="sxs-lookup"><span data-stu-id="31298-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="31298-152">Convalida dello schema di elementi di dati di set di transazioni hello rispetto allo schema di messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="31298-152">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="31298-153">Convalida EDI eseguita sugli elementi dati del set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="31298-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="31298-154">Convalida estesa eseguita sugli elementi dati del set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="31298-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="31298-155">Genera un documento XML per ogni set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="31298-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="31298-156">Richiede un riconoscimento tecnico e/o funzionale (se configurata).</span><span class="sxs-lookup"><span data-stu-id="31298-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="31298-157">Riconoscimento tecnico, il messaggio CONTRL hello indica ricezione di un interscambio.</span><span class="sxs-lookup"><span data-stu-id="31298-157">As a technical acknowledgment, hello CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="31298-158">Come un riconoscimento funzionale, il messaggio CONTRL hello indica l'accettazione o rifiuto dell'interscambio ricevuto hello, gruppo o messaggio, con un elenco di errori o funzionalità non supportate</span><span class="sxs-lookup"><span data-stu-id="31298-158">As a functional acknowledgment, hello CONTRL message indicates acceptance or rejection of hello received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="31298-159">Visualizzare il file Swagger</span><span class="sxs-lookup"><span data-stu-id="31298-159">View Swagger file</span></span>
<span data-ttu-id="31298-160">vedere i dettagli di Swagger hello tooview per connettore EDIFACT hello, [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="31298-160">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31298-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="31298-161">Next steps</span></span>
[<span data-ttu-id="31298-162">Altre informazioni su Enterprise Integration Pack hello</span><span class="sxs-lookup"><span data-stu-id="31298-162">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack") 


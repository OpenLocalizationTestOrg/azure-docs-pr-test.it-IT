---
title: Codificare messaggi EDIFACT - App per la logica di Azure | Documentazione Microsoft
description: "Convalidare le proprietà EDI e generare codice XML con il codificatore di messaggi EDIFACT in Enterprise Integration Pack in App per la logica di Azure"
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
ms.openlocfilehash: b8d577326d23ec45cb4a9ec0e450ebf7afd945f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="d2003-103">Messaggi Encode EDIFACT in App per la logica di Azure con Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="d2003-103">Encode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="d2003-104">Il connettore di messaggi Encode EDIFACT convalida le proprietà EDI e specifiche del partner e genera un documento XML per ogni set di transazioni e richiede un riconoscimento tecnico, funzionale o entrambi.</span><span class="sxs-lookup"><span data-stu-id="d2003-104">With the Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="d2003-105">Per usare questo connettore, è necessario aggiungerlo a un trigger esistente nell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="d2003-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="d2003-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="d2003-106">Before you start</span></span>

<span data-ttu-id="d2003-107">Sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d2003-107">Here's the items you need:</span></span>

* <span data-ttu-id="d2003-108">Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="d2003-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="d2003-109">Un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md) già definito e associato alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2003-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="d2003-110">Per usare il connettore di messaggi Encode EDIFACT è necessario un account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="d2003-110">You must have an integration account to use the Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="d2003-111">Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="d2003-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="d2003-112">Un [contratto EDIFACT](logic-apps-enterprise-integration-edifact.md) già definito nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="d2003-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="d2003-113">Codificare messaggi EDIFACT</span><span class="sxs-lookup"><span data-stu-id="d2003-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="d2003-114">[Creare un'app per la logica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d2003-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="d2003-115">Il connettore di messaggi Encode EDIFACT non dispone di trigger, pertanto è necessario aggiungerne uno per avviare l'app per la logica, ad esempio un trigger di richiesta.</span><span class="sxs-lookup"><span data-stu-id="d2003-115">The Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="d2003-116">In Progettazione app per la logica aggiungere un trigger e un'azione all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="d2003-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="d2003-117">Nella casella di ricerca, digitare "EDIFACT" come filtro.</span><span class="sxs-lookup"><span data-stu-id="d2003-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="d2003-118">Selezionare **Codifica in un messaggio EDIFACT in base al nome dell'accordo** o **Codifica in un messaggio EDIFACT in base alle identità**.</span><span class="sxs-lookup"><span data-stu-id="d2003-118">Select either **Encode EDIFACT Message by agreement name** or **Encode to EDIFACT message by identities**.</span></span>
   
    ![ricerca di EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="d2003-120">Se non sono state create in precedenza le connessioni all'account di integrazione, a questo punto viene richiesto di creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="d2003-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="d2003-121">Denominare la connessione e selezionare l'account di integrazione al quale connettersi.</span><span class="sxs-lookup"><span data-stu-id="d2003-121">Name your connection, and select the integration account that you want to connect.</span></span>

    ![creare connessione all'account di integrazione](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="d2003-123">Le proprietà con l'asterisco sono obbligatorie.</span><span class="sxs-lookup"><span data-stu-id="d2003-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="d2003-124">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d2003-124">Property</span></span> | <span data-ttu-id="d2003-125">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2003-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="d2003-126">Nome connessione *</span><span class="sxs-lookup"><span data-stu-id="d2003-126">Connection Name *</span></span> |<span data-ttu-id="d2003-127">Immettere un nome per la connessione.</span><span class="sxs-lookup"><span data-stu-id="d2003-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="d2003-128">Account di integrazione *</span><span class="sxs-lookup"><span data-stu-id="d2003-128">Integration Account *</span></span> |<span data-ttu-id="d2003-129">Immettere un nome per l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="d2003-129">Enter a name for your integration account.</span></span> <span data-ttu-id="d2003-130">Verificare che l'account di integrazione e l'app per la logica si trovino nella stessa località di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2003-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="d2003-131">Al termine, i dettagli della connessione dovrebbero essere simili a quelli dell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="d2003-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="d2003-132">Per completare la creazione della connessione, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d2003-132">To finish creating your connection, choose **Create**.</span></span>

    ![dettagli della connessione all'account di integrazione](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="d2003-134">La connessione è stata creata.</span><span class="sxs-lookup"><span data-stu-id="d2003-134">Your connection is now created.</span></span>

    ![connessione all'account di integrazione creata](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="d2003-136">Encode EDIFACT Message by agreement name</span><span class="sxs-lookup"><span data-stu-id="d2003-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="d2003-137">Se si sceglie di codificare i messaggi EDIFACT in base al nome del contratto, aprire l'elenco **Nome dell'accordo EDIFACT** e digitare o selezionare il nome del contratto EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="d2003-137">If you chose to encode EDIFACT messages by agreement name, open the **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="d2003-138">Immettere il messaggio XML da codificare.</span><span class="sxs-lookup"><span data-stu-id="d2003-138">Enter the XML message to encode.</span></span>

![Immettere il nome del contratto EDIFACT e un messaggio XML da codificare](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="d2003-140">Encode EDIFACT Message by identities</span><span class="sxs-lookup"><span data-stu-id="d2003-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="d2003-141">Se si sceglie di codificare i messaggi EDIFACT in base alle identità, inserire l'identificatore del mittente, il qualificatore del mittente, l'identificatore del destinatario e il qualificatore del destinatario come configurati nel contratto EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="d2003-141">If you choose to encode EDIFACT messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="d2003-142">Selezionare il messaggio XML da codificare.</span><span class="sxs-lookup"><span data-stu-id="d2003-142">Select the XML message to encode.</span></span>

![Fornire le identità del mittente e del destinatario e selezionare il messaggio XML da codificare](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="d2003-144">Dettagli della codifica EDIFACT</span><span class="sxs-lookup"><span data-stu-id="d2003-144">EDIFACT Encode details</span></span>

<span data-ttu-id="d2003-145">Il connettore Encode EDIFACT esegue queste attività:</span><span class="sxs-lookup"><span data-stu-id="d2003-145">The Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="d2003-146">Risolvere il contratto associando il qualificatore e l'identificatore del mittente e il qualificatore e l'identificatore del ricevitore.</span><span class="sxs-lookup"><span data-stu-id="d2003-146">Resolve the agreement by matching the sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="d2003-147">Serializza l'interscambio EDI, conversione dei messaggi con codifica XML in set di transazioni EDI nell'interscambio.</span><span class="sxs-lookup"><span data-stu-id="d2003-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="d2003-148">Si applica ai segmenti di intestazione e finali del set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="d2003-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="d2003-149">Genera un numero di controllo di interscambio, un numero di controllo di gruppo e un numero di controllo del set di transazioni per ogni interscambio in uscita.</span><span class="sxs-lookup"><span data-stu-id="d2003-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="d2003-150">Sostituisce i separatori nei dati del payload.</span><span class="sxs-lookup"><span data-stu-id="d2003-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="d2003-151">Convalida le proprietà EDI e specifiche del partner.</span><span class="sxs-lookup"><span data-stu-id="d2003-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="d2003-152">Convalida dello schema degli elementi dati del set di transazioni rispetto allo schema del messaggio.</span><span class="sxs-lookup"><span data-stu-id="d2003-152">Schema validation of the transaction-set data elements against the message schema.</span></span>
  * <span data-ttu-id="d2003-153">Convalida EDI eseguita sugli elementi dati del set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="d2003-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="d2003-154">Convalida estesa eseguita sugli elementi dati del set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="d2003-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="d2003-155">Genera un documento XML per ogni set di transazioni.</span><span class="sxs-lookup"><span data-stu-id="d2003-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="d2003-156">Richiede un riconoscimento tecnico e/o funzionale (se configurata).</span><span class="sxs-lookup"><span data-stu-id="d2003-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="d2003-157">Come riconoscimento tecnico, il messaggio CONTRL indica la ricezione di un interscambio.</span><span class="sxs-lookup"><span data-stu-id="d2003-157">As a technical acknowledgment, the CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="d2003-158">Come riconoscimento funzionale, il messaggio CONTRL indica l'accettazione o il rifiuto dell'interscambio, del gruppo o del messaggio ricevuto, con un elenco di errori o funzionalità non supportate.</span><span class="sxs-lookup"><span data-stu-id="d2003-158">As a functional acknowledgment, the CONTRL message indicates acceptance or rejection of the received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="d2003-159">Visualizzare il file Swagger</span><span class="sxs-lookup"><span data-stu-id="d2003-159">View Swagger file</span></span>
<span data-ttu-id="d2003-160">Per visualizzare i dettagli di Swagger per il connettore EDIFACT, vedere [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="d2003-160">To view the Swagger details for the EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2003-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d2003-161">Next steps</span></span>
[<span data-ttu-id="d2003-162">Altre informazioni su Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="d2003-162">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Informazioni su Enterprise Integration Pack") 


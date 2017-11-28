---
title: i messaggi AS2 aaaDecode - App Azure per la logica | Documenti Microsoft
description: Come toouse hello decodificatore AS2 nella hello Enterprise Integration Pack per le app di logica di Azure
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
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="1a4a3-103">Decodificare i messaggi AS2 per le app di Azure logica con hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="1a4a3-103">Decode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span> 

<span data-ttu-id="1a4a3-104">tooestablish protezione e affidabilità durante la trasmissione di messaggi, utilizzare connettore di messaggi hello decodifica AS2.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-104">tooestablish security and reliability while transmitting messages, use hello Decode AS2 message connector.</span></span> <span data-ttu-id="1a4a3-105">Questo connettore offre funzionalità di firma digitale, decrittografia e riconoscimenti tramite notifiche sulla ricezione di messaggi.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="1a4a3-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="1a4a3-106">Before you start</span></span>

<span data-ttu-id="1a4a3-107">Ecco gli elementi di hello che è necessario:</span><span class="sxs-lookup"><span data-stu-id="1a4a3-107">Here's hello items you need:</span></span>

* <span data-ttu-id="1a4a3-108">Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="1a4a3-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="1a4a3-109">Un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md) già definito e associato alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="1a4a3-110">È necessario disporre di un connettore di messaggio integrazione account toouse hello decodifica AS2.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-110">You must have an integration account toouse hello Decode AS2 message connector.</span></span>
* <span data-ttu-id="1a4a3-111">Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="1a4a3-112">Un [contratto AS2](logic-apps-enterprise-integration-as2.md) già definito nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="1a4a3-113">Decodificare i messaggi AS2</span><span class="sxs-lookup"><span data-stu-id="1a4a3-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="1a4a3-114">[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1a4a3-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="1a4a3-115">connettore di messaggi Hello decodifica AS2 non dispone di trigger, pertanto è necessario aggiungere un trigger per avviare l'app di logica, ad esempio un trigger di richiesta.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-115">hello Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="1a4a3-116">Nella finestra di progettazione logica App hello, aggiungere un trigger e quindi aggiungere un'app di logica di azione tooyour.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="1a4a3-117">Nella casella di ricerca hello, immettere "AS2" per il filtro.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="1a4a3-118">Selezionare **AS2 - Decodifica il messaggio AS2**.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    ![Cercare "AS2"](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="1a4a3-120">Se è stato creato in precedenza tutte le connessioni tooyour account di integrazione, viene chiesto toocreate ora tale connessione.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="1a4a3-121">Nome della connessione, quindi selezionare account di integrazione hello che si desidera tooconnect.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![Create una connessione di integrazione](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="1a4a3-123">Le proprietà con l'asterisco sono obbligatorie.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="1a4a3-124">Proprietà</span><span class="sxs-lookup"><span data-stu-id="1a4a3-124">Property</span></span> | <span data-ttu-id="1a4a3-125">Dettagli</span><span class="sxs-lookup"><span data-stu-id="1a4a3-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="1a4a3-126">Nome connessione *</span><span class="sxs-lookup"><span data-stu-id="1a4a3-126">Connection Name *</span></span> |<span data-ttu-id="1a4a3-127">Immettere un nome per la connessione.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="1a4a3-128">Account di integrazione *</span><span class="sxs-lookup"><span data-stu-id="1a4a3-128">Integration Account *</span></span> |<span data-ttu-id="1a4a3-129">Immettere un nome per l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-129">Enter a name for your integration account.</span></span> <span data-ttu-id="1a4a3-130">Assicurarsi che l'app di account e la logica di integrazione siano hello nello stesso percorso di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="1a4a3-131">Al termine, i dettagli relativi alla connessione dovrebbero essere simile toothis esempio.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="1a4a3-132">toofinish della creazione della connessione, scegliere **crea**.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-132">toofinish creating your connection, choose **Create**.</span></span>

    ![Dettagli della connessione di integrazione](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="1a4a3-134">Dopo aver creata la connessione, come illustrato in questo esempio, selezionare **corpo** e **intestazioni** hello richiedere output.</span><span class="sxs-lookup"><span data-stu-id="1a4a3-134">After your connection is created, as shown in this example, select **Body** and **Headers** from hello Request outputs.</span></span>
   
    ![connessione di integrazione creata](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="1a4a3-136">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1a4a3-136">For example:</span></span>

    ![Selezionare Corpo e Intestazioni dagli output della richiesta](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="1a4a3-138">Dettagli del decodificatore AS2</span><span class="sxs-lookup"><span data-stu-id="1a4a3-138">AS2 decoder details</span></span>

<span data-ttu-id="1a4a3-139">connettore di decodifica AS2 Hello esegue queste attività:</span><span class="sxs-lookup"><span data-stu-id="1a4a3-139">hello Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="1a4a3-140">Elabora le intestazioni AS2/HTTP</span><span class="sxs-lookup"><span data-stu-id="1a4a3-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="1a4a3-141">Verifica firma hello (se configurata)</span><span class="sxs-lookup"><span data-stu-id="1a4a3-141">Verifies hello signature (if configured)</span></span>
* <span data-ttu-id="1a4a3-142">Consente di decrittografare i messaggi hello (se configurata)</span><span class="sxs-lookup"><span data-stu-id="1a4a3-142">Decrypts hello messages (if configured)</span></span>
* <span data-ttu-id="1a4a3-143">Decomprime il messaggio hello (se configurata)</span><span class="sxs-lookup"><span data-stu-id="1a4a3-143">Decompresses hello message (if configured)</span></span>
* <span data-ttu-id="1a4a3-144">Riconcilia un MDN ricevuto con un messaggio in uscita originale hello</span><span class="sxs-lookup"><span data-stu-id="1a4a3-144">Reconciles a received MDN with hello original outbound message</span></span>
* <span data-ttu-id="1a4a3-145">Aggiorna e correla i record nel database di non ripudio hello</span><span class="sxs-lookup"><span data-stu-id="1a4a3-145">Updates and correlates records in hello non-repudiation database</span></span>
* <span data-ttu-id="1a4a3-146">Scrive i record per la creazione di report di stato su AS2</span><span class="sxs-lookup"><span data-stu-id="1a4a3-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="1a4a3-147">il contenuto del payload di output hello è con codificata base64</span><span class="sxs-lookup"><span data-stu-id="1a4a3-147">hello output payload contents are base64 encoded</span></span>
* <span data-ttu-id="1a4a3-148">Determina se un messaggio MDN è obbligatorio, se hello MDN deve essere sincrona o asincrona in base alla configurazione nell'accordo AS2</span><span class="sxs-lookup"><span data-stu-id="1a4a3-148">Determines whether an MDN is required, and whether hello MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="1a4a3-149">Genera una notifica sulla ricezione del messaggio sincrona o asincrona, in base alle configurazioni nel contratto</span><span class="sxs-lookup"><span data-stu-id="1a4a3-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="1a4a3-150">Imposta proprietà e i token di correlazione hello in hello MDN</span><span class="sxs-lookup"><span data-stu-id="1a4a3-150">Sets hello correlation tokens and properties on hello MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="1a4a3-151">Provare questo esempio</span><span class="sxs-lookup"><span data-stu-id="1a4a3-151">Try this sample</span></span>

<span data-ttu-id="1a4a3-152">tootry la distribuzione di uno scenario di AS2 app ed esempio logica completamente operativo, vedere hello [AS2 scenario e il modello di applicazione logica](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="1a4a3-152">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="1a4a3-153">Swagger hello vista</span><span class="sxs-lookup"><span data-stu-id="1a4a3-153">View hello swagger</span></span>
<span data-ttu-id="1a4a3-154">Vedere hello [swagger dettagli](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="1a4a3-154">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1a4a3-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1a4a3-155">Next steps</span></span>
[<span data-ttu-id="1a4a3-156">Altre informazioni su hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="1a4a3-156">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 


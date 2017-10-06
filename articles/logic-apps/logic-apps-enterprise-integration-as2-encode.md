---
title: i messaggi AS2 aaaEncode - App Azure per la logica | Documenti Microsoft
description: Come toouse hello codificatore AS2 in hello Enterprise Integration Pack per le app di logica di Azure
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="4d13d-103">Codificare i messaggi AS2 per App di Azure logica con hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="4d13d-103">Encode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="4d13d-104">tooestablish protezione e affidabilità durante la trasmissione di messaggi, utilizzare connettore di messaggi hello codificare AS2.</span><span class="sxs-lookup"><span data-stu-id="4d13d-104">tooestablish security and reliability while transmitting messages, use hello Encode AS2 message connector.</span></span> <span data-ttu-id="4d13d-105">Questo connettore consente la firma digitale, crittografia e riconoscimenti tramite notifiche MDN (Message Disposition), che comporta anche la toosupport per il Non ripudio.</span><span class="sxs-lookup"><span data-stu-id="4d13d-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads toosupport for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="4d13d-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="4d13d-106">Before you start</span></span>

<span data-ttu-id="4d13d-107">Ecco gli elementi di hello che è necessario:</span><span class="sxs-lookup"><span data-stu-id="4d13d-107">Here's hello items you need:</span></span>

* <span data-ttu-id="4d13d-108">Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="4d13d-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="4d13d-109">Un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md) già definito e associato alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d13d-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="4d13d-110">È necessario disporre di un connettore di messaggi AS2 codificare integrazione account toouse hello.</span><span class="sxs-lookup"><span data-stu-id="4d13d-110">You must have an integration account toouse hello Encode AS2 message connector.</span></span>
* <span data-ttu-id="4d13d-111">Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="4d13d-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="4d13d-112">Un [contratto AS2](logic-apps-enterprise-integration-as2.md) già definito nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="4d13d-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="4d13d-113">Codificare i messaggi AS2</span><span class="sxs-lookup"><span data-stu-id="4d13d-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="4d13d-114">[Creare un'app per la logica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4d13d-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="4d13d-115">connettore di messaggi AS2 codificare Hello non dispone di trigger, pertanto è necessario aggiungere un trigger per avviare l'app di logica, ad esempio un trigger di richiesta.</span><span class="sxs-lookup"><span data-stu-id="4d13d-115">hello Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="4d13d-116">Nella finestra di progettazione logica App hello, aggiungere un trigger e quindi aggiungere un'app di logica di azione tooyour.</span><span class="sxs-lookup"><span data-stu-id="4d13d-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="4d13d-117">Nella casella di ricerca hello, immettere "AS2" per il filtro.</span><span class="sxs-lookup"><span data-stu-id="4d13d-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="4d13d-118">Selezionare **AS2 - Codifica in un messaggio AS2**.</span><span class="sxs-lookup"><span data-stu-id="4d13d-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    ![Cercare "AS2"](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="4d13d-120">Se è stato creato in precedenza tutte le connessioni tooyour account di integrazione, viene chiesto toocreate ora tale connessione.</span><span class="sxs-lookup"><span data-stu-id="4d13d-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="4d13d-121">Nome della connessione, quindi selezionare account di integrazione hello che si desidera tooconnect.</span><span class="sxs-lookup"><span data-stu-id="4d13d-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![creare account di connessione toointegration](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="4d13d-123">Le proprietà con l'asterisco sono obbligatorie.</span><span class="sxs-lookup"><span data-stu-id="4d13d-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="4d13d-124">Proprietà</span><span class="sxs-lookup"><span data-stu-id="4d13d-124">Property</span></span> | <span data-ttu-id="4d13d-125">Dettagli</span><span class="sxs-lookup"><span data-stu-id="4d13d-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="4d13d-126">Nome connessione *</span><span class="sxs-lookup"><span data-stu-id="4d13d-126">Connection Name *</span></span> |<span data-ttu-id="4d13d-127">Immettere un nome per la connessione.</span><span class="sxs-lookup"><span data-stu-id="4d13d-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="4d13d-128">Account di integrazione *</span><span class="sxs-lookup"><span data-stu-id="4d13d-128">Integration Account *</span></span> |<span data-ttu-id="4d13d-129">Immettere un nome per l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="4d13d-129">Enter a name for your integration account.</span></span> <span data-ttu-id="4d13d-130">Assicurarsi che l'app di account e la logica di integrazione siano hello nello stesso percorso di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d13d-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="4d13d-131">Al termine, i dettagli relativi alla connessione dovrebbero essere simile toothis esempio.</span><span class="sxs-lookup"><span data-stu-id="4d13d-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="4d13d-132">toofinish della creazione della connessione, scegliere **crea**.</span><span class="sxs-lookup"><span data-stu-id="4d13d-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![Dettagli della connessione di integrazione](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="4d13d-134">Dopo aver creata la connessione, come illustrato in questo esempio, fornire i dettagli per **AS2-da**, **AS2 tooidentifiers** come configurato nel contratto, e **corpo**, ovvero payload del messaggio Hello.</span><span class="sxs-lookup"><span data-stu-id="4d13d-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-tooidentifiers** as configured in your agreement, and **Body**, which is hello message payload.</span></span>
   
    ![specificare i campi obbligatori](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="4d13d-136">Dettagli codificatore AS2</span><span class="sxs-lookup"><span data-stu-id="4d13d-136">AS2 encoder details</span></span>

<span data-ttu-id="4d13d-137">connettore di codifica AS2 Hello esegue queste attività:</span><span class="sxs-lookup"><span data-stu-id="4d13d-137">hello Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="4d13d-138">Elabora le intestazioni AS2/HTTP</span><span class="sxs-lookup"><span data-stu-id="4d13d-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="4d13d-139">Firma i messaggi in uscita (se configurata)</span><span class="sxs-lookup"><span data-stu-id="4d13d-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="4d13d-140">Crittografa i messaggi in uscita (se configurata)</span><span class="sxs-lookup"><span data-stu-id="4d13d-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="4d13d-141">Comprime il messaggio hello (se configurata)</span><span class="sxs-lookup"><span data-stu-id="4d13d-141">Compresses hello message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="4d13d-142">Provare questo esempio</span><span class="sxs-lookup"><span data-stu-id="4d13d-142">Try this sample</span></span>

<span data-ttu-id="4d13d-143">tootry la distribuzione di uno scenario di AS2 app ed esempio logica completamente operativo, vedere hello [AS2 scenario e il modello di applicazione logica](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="4d13d-143">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="4d13d-144">Swagger hello vista</span><span class="sxs-lookup"><span data-stu-id="4d13d-144">View hello swagger</span></span>
<span data-ttu-id="4d13d-145">Vedere hello [swagger dettagli](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="4d13d-145">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4d13d-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4d13d-146">Next steps</span></span>
[<span data-ttu-id="4d13d-147">Altre informazioni su Enterprise Integration Pack hello</span><span class="sxs-lookup"><span data-stu-id="4d13d-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack") 


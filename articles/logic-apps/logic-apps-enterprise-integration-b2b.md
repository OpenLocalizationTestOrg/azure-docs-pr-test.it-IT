---
title: soluzioni aaaCreate B2B - App Azure per la logica | Documenti Microsoft
description: "Ricevere i dati nella logica App usando le funzionalità di hello B2B di hello Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a><span data-ttu-id="50608-103">La ricezione dei dati nella logica di applicazioni con funzionalità B2B hello hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="50608-103">Receive data in logic apps with hello B2B features in hello Enterprise Integration Pack</span></span>

<span data-ttu-id="50608-104">Dopo aver creato un account di integrazione con partner e contratti, si è pronti toocreate un flusso di lavoro di business (B2B) toobusiness per l'app logica con hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="50608-104">After you create an integration account that has partners and agreements, you are ready toocreate a business toobusiness (B2B) workflow for your logic app with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50608-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="50608-105">Prerequisites</span></span>

<span data-ttu-id="50608-106">toouse hello X12 e AS2 azioni, è necessario disporre di un Account di integrazione aziendale.</span><span class="sxs-lookup"><span data-stu-id="50608-106">toouse hello AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="50608-107">Informazioni su [come toocreate un'integrazione Enterprise Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="50608-107">Learn [how toocreate an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="50608-108">Creare un'app per la logica con connettori B2B</span><span class="sxs-lookup"><span data-stu-id="50608-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="50608-109">Seguire queste app per la logica toocreate un B2B passaggi che utilizza hello AS2 e X12 dati tooreceive azioni da un partner commerciale:</span><span class="sxs-lookup"><span data-stu-id="50608-109">Follow these steps toocreate a B2B logic app that uses hello AS2 and X12 actions tooreceive data from a trading partner:</span></span>

1. <span data-ttu-id="50608-110">Creare un'applicazione di logica, quindi [collegare l'account di integrazione di app tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="50608-110">Create a logic app, then [link your app tooyour integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="50608-111">Aggiungere un **richiesta - viene ricevuta la richiesta HTTP quando** trigger tooyour logica app.</span><span class="sxs-lookup"><span data-stu-id="50608-111">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="50608-112">hello tooadd **decodifica AS2** azione, selezionare **aggiungere un'azione**.</span><span class="sxs-lookup"><span data-stu-id="50608-112">tooadd hello **Decode AS2** action, select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="50608-113">toofilter toohello azioni tutto quello che si desidera, immettere la parola hello **as2** nella casella di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="50608-113">toofilter all actions toohello one that you want, enter hello word **as2** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="50608-114">Seleziona hello **AS2 - messaggio AS2 decodificare** azione.</span><span class="sxs-lookup"><span data-stu-id="50608-114">Select hello **AS2 - Decode AS2 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="50608-115">Aggiungere hello **corpo** che si desidera toouse come input.</span><span class="sxs-lookup"><span data-stu-id="50608-115">Add hello **Body** that you want toouse as input.</span></span> <span data-ttu-id="50608-116">In questo esempio, selezionare corpo hello della richiesta HTTP hello che trigger hello logica app.</span><span class="sxs-lookup"><span data-stu-id="50608-116">In this example, select hello body of hello HTTP request that triggers hello logic app.</span></span> <span data-ttu-id="50608-117">Oppure immettere un'espressione che inserisce le intestazioni di hello in hello **intestazioni** campo:</span><span class="sxs-lookup"><span data-stu-id="50608-117">Or enter an expression that inputs hello headers in hello **HEADERS** field:</span></span>

    <span data-ttu-id="50608-118">@triggerOutputs()['headers']</span><span class="sxs-lookup"><span data-stu-id="50608-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="50608-119">Aggiungere hello necessario **intestazioni** per AS2, è possibile trovare nelle intestazioni di richiesta HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="50608-119">Add hello required **Headers** for AS2, which you can find in hello HTTP request headers.</span></span> <span data-ttu-id="50608-120">In questo esempio, selezionare le intestazioni di hello della richiesta HTTP hello trigger hello logica app.</span><span class="sxs-lookup"><span data-stu-id="50608-120">In this example, select hello headers of hello HTTP request that trigger hello logic app.</span></span>

8. <span data-ttu-id="50608-121">Ora aggiungere l'azione del messaggio hello Decode X12.</span><span class="sxs-lookup"><span data-stu-id="50608-121">Now add hello Decode X12 message action.</span></span> <span data-ttu-id="50608-122">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="50608-122">Select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="50608-123">toofilter toohello azioni tutto quello che si desidera, immettere la parola hello **x12** nella casella di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="50608-123">toofilter all actions toohello one that you want, enter hello word **x12** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="50608-124">Seleziona hello **X12-decodificare X12 messaggio** azione.</span><span class="sxs-lookup"><span data-stu-id="50608-124">Select hello **X12 - Decode X12 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="50608-125">Ora è necessario specificare l'azione di input toothis hello.</span><span class="sxs-lookup"><span data-stu-id="50608-125">Now you must specify hello input toothis action.</span></span> <span data-ttu-id="50608-126">Questo input è l'output di hello dall'azione AS2 precedente hello.</span><span class="sxs-lookup"><span data-stu-id="50608-126">This input is hello output from hello previous AS2 action.</span></span>

    <span data-ttu-id="50608-127">contenuto del messaggio effettivo Hello è in un oggetto JSON e codificato in base64, pertanto è necessario specificare un'espressione come input hello.</span><span class="sxs-lookup"><span data-stu-id="50608-127">hello actual message content is in a JSON object and is base64 encoded, so you must specify an expression as hello input.</span></span> 
    <span data-ttu-id="50608-128">Immettere l'espressione in hello seguente hello **X12 FLAT FILE messaggio tooDECODE** campo di input:</span><span class="sxs-lookup"><span data-stu-id="50608-128">Enter hello following expression in hello **X12 FLAT FILE MESSAGE tooDECODE** input field:</span></span>
    
    <span data-ttu-id="50608-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="50608-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="50608-130">Aggiungere i passaggi dati hello X12 toodecode ricevuto dal partner commerciale hello e gli elementi in un oggetto JSON di output.</span><span class="sxs-lookup"><span data-stu-id="50608-130">Now add steps toodecode hello X12 data received from hello trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="50608-131">partner hello toonotify hello dati è stato ricevuto, è possibile restituire una risposta contenente hello AS2 notifica MDN (Message Disposition) in un'azione di risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="50608-131">toonotify hello partner that hello data was received, you can send back a response containing hello AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="50608-132">hello tooadd **risposta** azione, scegliere **aggiungere un'azione**.</span><span class="sxs-lookup"><span data-stu-id="50608-132">tooadd hello **Response** action, choose **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="50608-133">toofilter toohello azioni tutto quello che si desidera, immettere la parola hello **risposta** nella casella di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="50608-133">toofilter all actions toohello one that you want, enter hello word **response** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="50608-134">Seleziona hello **risposta** azione.</span><span class="sxs-lookup"><span data-stu-id="50608-134">Select hello **Response** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="50608-135">tooaccess hello MDN dall'output di hello di hello **messaggio X12 Decode** azione, set hello risposta **corpo** campo con questa espressione:</span><span class="sxs-lookup"><span data-stu-id="50608-135">tooaccess hello MDN from hello output of hello **Decode X12 message** action, set hello response **BODY** field with this expression:</span></span>

    <span data-ttu-id="50608-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="50608-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="50608-137">Salvare il lavoro.</span><span class="sxs-lookup"><span data-stu-id="50608-137">Save your work.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="50608-138">La configurazione dell'app per la logica B2B è completata.</span><span class="sxs-lookup"><span data-stu-id="50608-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="50608-139">In un'applicazione reale, è opportuno toostore hello decodificati X12 dati in un archivio line-of-business (LOB) app o i dati.</span><span class="sxs-lookup"><span data-stu-id="50608-139">In a real world application, you might want toostore hello decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="50608-140">tooconnect delle applicazioni LOB e usare queste API nell'app logica, è possibile aggiungere ulteriori azioni o le API personalizzate di scrittura.</span><span class="sxs-lookup"><span data-stu-id="50608-140">tooconnect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="50608-141">Funzionalità e casi d'uso</span><span class="sxs-lookup"><span data-stu-id="50608-141">Features and use cases</span></span>

* <span data-ttu-id="50608-142">Hello AS2 e X12 decodificare e codificare azioni consentono scambiare dati tra partner commerciali tramite protocolli standard del settore in App per la logica.</span><span class="sxs-lookup"><span data-stu-id="50608-142">hello AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="50608-143">dati tooexchange con partner commerciali, è possibile utilizzare AS2 e X12 con o senza di loro.</span><span class="sxs-lookup"><span data-stu-id="50608-143">tooexchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="50608-144">azioni B2B Hello consentono di creare facilmente i partner e contratti nell'account di integrazione e utilizzarli in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="50608-144">hello B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="50608-145">Quando si estende la propria app per la logica con altre azioni, è possibile inviare e ricevere dati tra altre applicazioni e altri servizi come SalesForce.</span><span class="sxs-lookup"><span data-stu-id="50608-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="50608-146">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="50608-146">Learn more</span></span>
[<span data-ttu-id="50608-147">Altre informazioni su hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="50608-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)

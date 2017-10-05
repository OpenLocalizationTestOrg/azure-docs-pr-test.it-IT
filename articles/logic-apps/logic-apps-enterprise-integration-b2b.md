---
title: Creare soluzioni B2B - App per la logica di Azure | Microsoft Docs
description: "Ricevere dati in app per la logica usando le funzionalità B2B in Enterprise Integration Pack"
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
ms.openlocfilehash: 0625787ddcbc0091e70b111f687e25929720ad15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="receive-data-in-logic-apps-with-the-b2b-features-in-the-enterprise-integration-pack"></a><span data-ttu-id="79e26-103">Ricevere dati in app per la logica con le funzionalità B2B in Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="79e26-103">Receive data in logic apps with the B2B features in the Enterprise Integration Pack</span></span>

<span data-ttu-id="79e26-104">Dopo aver creato un account di integrazione con partner e contratti, si è pronti per creare un flusso di lavoro Business to Business (B2B) per l'app per la logica con [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="79e26-104">After you create an integration account that has partners and agreements, you are ready to create a business to business (B2B) workflow for your logic app with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79e26-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="79e26-105">Prerequisites</span></span>

<span data-ttu-id="79e26-106">Per usare le azioni AS2 e X12, è necessario un account Enterprise Integration.</span><span class="sxs-lookup"><span data-stu-id="79e26-106">To use the AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="79e26-107">Informazioni sulla [creazione di un account Enterprise Integration](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="79e26-107">Learn [how to create an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="79e26-108">Creare un'app per la logica con connettori B2B</span><span class="sxs-lookup"><span data-stu-id="79e26-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="79e26-109">Seguire questa procedura per creare un'app per la logica B2B che usi le azioni AS2 e X12 per ricevere dati da un partner commerciale:</span><span class="sxs-lookup"><span data-stu-id="79e26-109">Follow these steps to create a B2B logic app that uses the AS2 and X12 actions to receive data from a trading partner:</span></span>

1. <span data-ttu-id="79e26-110">Creare un'app per la logica, quindi [collegare l'app al proprio account di integrazione](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="79e26-110">Create a logic app, then [link your app to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="79e26-111">Aggiungere un trigger **Richiesta - Alla ricezione di una richiesta HTTP** all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="79e26-111">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="79e26-112">Per aggiungere l'azione **Decodifica AS2**, selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="79e26-112">To add the **Decode AS2** action, select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="79e26-113">Per filtrare tutte le azioni e trovare quella desiderata, immettere **as2** nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="79e26-113">To filter all actions to the one that you want, enter the word **as2** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="79e26-114">Selezionare l'azione **AS2 - Decode AS2 message** (AS2 - Decodifica messaggio AS2).</span><span class="sxs-lookup"><span data-stu-id="79e26-114">Select the **AS2 - Decode AS2 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="79e26-115">Aggiungere il **corpo** che si desidera usare come input.</span><span class="sxs-lookup"><span data-stu-id="79e26-115">Add the **Body** that you want to use as input.</span></span> <span data-ttu-id="79e26-116">In questo esempio selezionare il corpo della richiesta HTTP che attiva l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="79e26-116">In this example, select the body of the HTTP request that triggers the logic app.</span></span> <span data-ttu-id="79e26-117">Oppure, immettere un'espressione che inserisce le intestazioni nel campo **INTESTAZIONI**:</span><span class="sxs-lookup"><span data-stu-id="79e26-117">Or enter an expression that inputs the headers in the **HEADERS** field:</span></span>

    <span data-ttu-id="79e26-118">@triggerOutputs()['headers']</span><span class="sxs-lookup"><span data-stu-id="79e26-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="79e26-119">Aggiungere le **intestazioni** necessarie per AS2, che è possibile trovare nelle intestazioni della richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="79e26-119">Add the required **Headers** for AS2, which you can find in the HTTP request headers.</span></span> <span data-ttu-id="79e26-120">In questo esempio selezionare le intestazioni della richiesta HTTP che attivano l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="79e26-120">In this example, select the headers of the HTTP request that trigger the logic app.</span></span>

8. <span data-ttu-id="79e26-121">A questo punto aggiungere l'azione del messaggio Decode X12.</span><span class="sxs-lookup"><span data-stu-id="79e26-121">Now add the Decode X12 message action.</span></span> <span data-ttu-id="79e26-122">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="79e26-122">Select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="79e26-123">Per filtrare tutte le azioni e trovare quella desiderata, immettere **x12** nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="79e26-123">To filter all actions to the one that you want, enter the word **x12** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="79e26-124">Selezionare l'azione **X12 - Decode X12 message** (X12 - Decodifica messaggio X12).</span><span class="sxs-lookup"><span data-stu-id="79e26-124">Select the **X12 - Decode X12 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="79e26-125">A questo punto è necessario specificare l'input per questa azione.</span><span class="sxs-lookup"><span data-stu-id="79e26-125">Now you must specify the input to this action.</span></span> <span data-ttu-id="79e26-126">Questo input è l'output dell'azione AS2 precedente.</span><span class="sxs-lookup"><span data-stu-id="79e26-126">This input is the output from the previous AS2 action.</span></span>

    <span data-ttu-id="79e26-127">Il contenuto effettivo del messaggio è in un oggetto JSON e codificato in base64, pertanto è necessario specificare un'espressione come input.</span><span class="sxs-lookup"><span data-stu-id="79e26-127">The actual message content is in a JSON object and is base64 encoded, so you must specify an expression as the input.</span></span> 
    <span data-ttu-id="79e26-128">Immettere l'espressione seguente nel campo di input **X12 FLAT FILE MESSAGE TO DECODE** (MESSAGGIO FILE FLAT X12 DA DECODIFICARE):</span><span class="sxs-lookup"><span data-stu-id="79e26-128">Enter the following expression in the **X12 FLAT FILE MESSAGE TO DECODE** input field:</span></span>
    
    <span data-ttu-id="79e26-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="79e26-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="79e26-130">A questo punto aggiungere i passaggi per decodificare i dati X12 ricevuti dal partner commerciale e gli elementi di output in un oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="79e26-130">Now add steps to decode the X12 data received from the trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="79e26-131">Per comunicare al partner che i dati sono stati ricevuti, è possibile inviare una risposta contenente la notifica sulla ricezione del messaggio (MDN, Message Disposition Notification) AS2 in un'azione di risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="79e26-131">To notify the partner that the data was received, you can send back a response containing the AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="79e26-132">Per aggiungere l'azione **Risposta**, scegliere **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="79e26-132">To add the **Response** action, choose **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="79e26-133">Per filtrare tutte le azioni e trovare quella desiderata, immettere **response** nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="79e26-133">To filter all actions to the one that you want, enter the word **response** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="79e26-134">Selezionare l'azione **Risposta**.</span><span class="sxs-lookup"><span data-stu-id="79e26-134">Select the **Response** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="79e26-135">Per accedere all'MDN dall'output dell'azione **Decode X12 message** (Decodifica messaggio X12), impostare il campo **CORPO** ella risposta usando l'espressione seguente:</span><span class="sxs-lookup"><span data-stu-id="79e26-135">To access the MDN from the output of the **Decode X12 message** action, set the response **BODY** field with this expression:</span></span>

    <span data-ttu-id="79e26-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="79e26-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="79e26-137">Salvare il lavoro.</span><span class="sxs-lookup"><span data-stu-id="79e26-137">Save your work.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="79e26-138">La configurazione dell'app per la logica B2B è completata.</span><span class="sxs-lookup"><span data-stu-id="79e26-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="79e26-139">In un'applicazione reale, si potrebbe voler archiviare i dati X12 decodificati in un'app line-of-business (LOB) o in un archivio dati.</span><span class="sxs-lookup"><span data-stu-id="79e26-139">In a real world application, you might want to store the decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="79e26-140">Per connettere le proprie app LOB e usare queste API nell'app per la logica, è possibile aggiungere altre azioni o scrivere API personalizzate.</span><span class="sxs-lookup"><span data-stu-id="79e26-140">To connect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="79e26-141">Funzionalità e casi d'uso</span><span class="sxs-lookup"><span data-stu-id="79e26-141">Features and use cases</span></span>

* <span data-ttu-id="79e26-142">Le azioni di decodifica e codifica AS2 e X12 consentono di scambiare dati tra partner commerciali tramite protocolli standard del settore in app per la logica.</span><span class="sxs-lookup"><span data-stu-id="79e26-142">The AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="79e26-143">È possibile usare AS2 e X12, da soli o combinati, per scambiare dati con i partner commerciali.</span><span class="sxs-lookup"><span data-stu-id="79e26-143">To exchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="79e26-144">Le azioni B2B aiutano a creare facilmente partner e contratti nell'account di integrazione e a usarli in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="79e26-144">The B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="79e26-145">Quando si estende la propria app per la logica con altre azioni, è possibile inviare e ricevere dati tra altre applicazioni e altri servizi come SalesForce.</span><span class="sxs-lookup"><span data-stu-id="79e26-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="79e26-146">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="79e26-146">Learn more</span></span>
[<span data-ttu-id="79e26-147">Altre informazioni su Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="79e26-147">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)

---
title: Contratti per la comunicazione B2B - App per la logica di Azure | Microsoft Docs
description: Creare accordi per consentire ai partner di comunicare in scenari B2B per App per la logica di Azure ed Enterprise Integration Pack
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 447ffb8e-3e91-4403-872b-2f496495899d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: LADocs
ms.openlocfilehash: 7ce0860272901f3b4e4cf3d63f7361d539f64741
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="partner-agreements-for-b2b-communication-with-azure-logic-apps-and-enterprise-integration-pack"></a><span data-ttu-id="2bb93-103">Accordi tra partner per la comunicazione B2B con App per la logica di Azure ed Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="2bb93-103">Partner agreements for B2B communication with Azure Logic Apps and Enterprise Integration Pack</span></span>

<span data-ttu-id="2bb93-104">Gli accordi consentono alle entità business di comunicare in modo ottimale mediante i protocolli standard di settore e sono il fulcro delle comunicazioni Business to Business (B2B).</span><span class="sxs-lookup"><span data-stu-id="2bb93-104">Agreements let business entities communicate seamlessly using industry standard protocols and are the cornerstone for business-to-business (B2B) communication.</span></span> <span data-ttu-id="2bb93-105">Quando si abilitano scenari B2B per app per la logica con Enterprise Integration Pack, un accordo è un contratto di comunicazione fra partner commerciali B2B.</span><span class="sxs-lookup"><span data-stu-id="2bb93-105">When enabling B2B scenarios for logic apps with the Enterprise Integration Pack, an agreement is a communications arrangement between B2B trading partners.</span></span> <span data-ttu-id="2bb93-106">Questo accordo si basa sulle comunicazioni che i partner vogliono stabilire ed è specifico del protocollo o del trasporto.</span><span class="sxs-lookup"><span data-stu-id="2bb93-106">This agreement is based on the communications that the partners want to establish and is protocol or transport-specific.</span></span>

<span data-ttu-id="2bb93-107">Enterprise Integration supporta questi standard di protocollo o di trasporto:</span><span class="sxs-lookup"><span data-stu-id="2bb93-107">Enterprise integration supports these protocol or transport standards:</span></span>

* [<span data-ttu-id="2bb93-108">AS2</span><span class="sxs-lookup"><span data-stu-id="2bb93-108">AS2</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="2bb93-109">X12</span><span class="sxs-lookup"><span data-stu-id="2bb93-109">X12</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="2bb93-110">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="2bb93-110">EDIFACT</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="why-use-agreements"></a><span data-ttu-id="2bb93-111">Perché usare i contratti</span><span class="sxs-lookup"><span data-stu-id="2bb93-111">Why use agreements</span></span>

<span data-ttu-id="2bb93-112">Di seguito sono riportati alcuni dei vantaggi più comuni legati all'uso degli accordi:</span><span class="sxs-lookup"><span data-stu-id="2bb93-112">Here are some common benefits when using agreements:</span></span>

* <span data-ttu-id="2bb93-113">Consentono alle aziende di scambiare informazioni in un formato noto.</span><span class="sxs-lookup"><span data-stu-id="2bb93-113">Enables different organizations and businesses to exchange information in a well-known format.</span></span>
* <span data-ttu-id="2bb93-114">Migliorano l'efficienza delle transazioni B2B</span><span class="sxs-lookup"><span data-stu-id="2bb93-114">Improves efficiency when conducting B2B transactions</span></span>
* <span data-ttu-id="2bb93-115">È facile crearli, gestirli e usarli quando si creano app di integrazione aziendali</span><span class="sxs-lookup"><span data-stu-id="2bb93-115">Easy to create, manage, and use when creating enterprise integration apps</span></span>

## <a name="how-to-create-agreements"></a><span data-ttu-id="2bb93-116">Come creare contratti</span><span class="sxs-lookup"><span data-stu-id="2bb93-116">How to create agreements</span></span>

* [<span data-ttu-id="2bb93-117">Creare un contratto AS2</span><span class="sxs-lookup"><span data-stu-id="2bb93-117">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="2bb93-118">Creare un contratto X12</span><span class="sxs-lookup"><span data-stu-id="2bb93-118">Create an X12 agreement</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="2bb93-119">Creare un contratto EDIFACT</span><span class="sxs-lookup"><span data-stu-id="2bb93-119">Create an EDIFACT agreement</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="how-to-use-an-agreement"></a><span data-ttu-id="2bb93-120">Come usare un contratto</span><span class="sxs-lookup"><span data-stu-id="2bb93-120">How to use an agreement</span></span>

<span data-ttu-id="2bb93-121">È possibile creare [app per la logica](logic-apps-what-are-logic-apps.md "Informazioni sulle app per la logica") con funzionalità B2B tramite un accordo che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="2bb93-121">You can create [logic apps](logic-apps-what-are-logic-apps.md "Learn about Logic apps") with B2B capabilities by using an agreement that you created.</span></span>

## <a name="how-to-edit-an-agreement"></a><span data-ttu-id="2bb93-122">Come modificare un contratto</span><span class="sxs-lookup"><span data-stu-id="2bb93-122">How to edit an agreement</span></span>

<span data-ttu-id="2bb93-123">È possibile modificare qualsiasi contratto seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2bb93-123">You can edit any agreement by following these steps:</span></span>

1. <span data-ttu-id="2bb93-124">Selezionare l'account di integrazione con l'accordo da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="2bb93-124">Select the integration account that has the agreement you want to update.</span></span>

2. <span data-ttu-id="2bb93-125">Selezionare il riquadro **Accordi**.</span><span class="sxs-lookup"><span data-stu-id="2bb93-125">Choose the **Agreements** tile.</span></span>

3. <span data-ttu-id="2bb93-126">Nel pannello **Accordi** selezionare l'accordo.</span><span class="sxs-lookup"><span data-stu-id="2bb93-126">On the **Agreements** blade, select the agreement.</span></span>

4. <span data-ttu-id="2bb93-127">Scegliere **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="2bb93-127">Choose **Edit**.</span></span> <span data-ttu-id="2bb93-128">Apportare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="2bb93-128">Make your changes.</span></span>

5. <span data-ttu-id="2bb93-129">Per salvare le modifiche, scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="2bb93-129">To save your changes, choose **OK**.</span></span>

## <a name="how-to-delete-an-agreement"></a><span data-ttu-id="2bb93-130">Come eliminare un contratto</span><span class="sxs-lookup"><span data-stu-id="2bb93-130">How to delete an agreement</span></span>

<span data-ttu-id="2bb93-131">È possibile eliminare qualsiasi accordo seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2bb93-131">You can delete any agreement by following these steps:</span></span>

1. <span data-ttu-id="2bb93-132">Selezionare l'account di integrazione con l'accordo da eliminare.</span><span class="sxs-lookup"><span data-stu-id="2bb93-132">Select the integration account that has the agreement you want to delete.</span></span>
2. <span data-ttu-id="2bb93-133">Selezionare il riquadro **Accordi**.</span><span class="sxs-lookup"><span data-stu-id="2bb93-133">Choose the **Agreements** tile.</span></span>
3. <span data-ttu-id="2bb93-134">Nel pannello **Accordi** selezionare l'accordo.</span><span class="sxs-lookup"><span data-stu-id="2bb93-134">On the **Agreements** blade, select the agreement.</span></span>
4. <span data-ttu-id="2bb93-135">Scegliere **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="2bb93-135">Choose **Delete**.</span></span>
5. <span data-ttu-id="2bb93-136">Confermare che si desidera eliminare l'accordo selezionato.</span><span class="sxs-lookup"><span data-stu-id="2bb93-136">Confirm that you want to delete the selected agreement.</span></span>

    <span data-ttu-id="2bb93-137">Nel pannello Accordi non viene più visualizzato l'accordo eliminato.</span><span class="sxs-lookup"><span data-stu-id="2bb93-137">The Agreements blade no longer shows the deleted agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bb93-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2bb93-138">Next steps</span></span>
* [<span data-ttu-id="2bb93-139">Creare un contratto AS2</span><span class="sxs-lookup"><span data-stu-id="2bb93-139">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)

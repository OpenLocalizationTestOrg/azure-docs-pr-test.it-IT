---
title: i partner aaaCreate per i messaggi di business-to-business (B2B) - App Azure per la logica | Documenti Microsoft
description: Informazioni su come integrazione di tooyour tooadd partner account con Enterprise Integration Pack hello e App per la logica
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8dc70a8f441fcf228ed178029dcdbac940d794b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="b1e69-103">Aggiungere o aggiornare i partner nei contratti Business to Business nel proprio flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="b1e69-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="b1e69-104">I partner sono le entità che partecipano alle transazioni e allo scambio di messaggi Business-To-Business (B2B).</span><span class="sxs-lookup"><span data-stu-id="b1e69-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="b1e69-105">Prima di poter creare i partner che rappresentano l'utente e l'altra organizzazione nelle transazioni, è necessario che entrambe le parti condividano le informazioni che identificano e convalidano i messaggi inviati.</span><span class="sxs-lookup"><span data-stu-id="b1e69-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="b1e69-106">Dopo aver discuterne i dettagli e sono pronti toostart la relazione di business, è possibile creare partner il toorepresent di account di integrazione da entrambi.</span><span class="sxs-lookup"><span data-stu-id="b1e69-106">After you discuss these details and are ready toostart your business relationship, you can create partners in your integration account toorepresent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="b1e69-107">Che ruoli hanno i partner nell'account di integrazione?</span><span class="sxs-lookup"><span data-stu-id="b1e69-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="b1e69-108">toodefine informazioni dettagliate relative ai messaggi hello scambiati tra i partner, creare contratti tra tali partner.</span><span class="sxs-lookup"><span data-stu-id="b1e69-108">toodefine details about hello messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="b1e69-109">Tuttavia, prima di poter creare un accordo, è necessario aver aggiunto account di integrazione tooyour almeno due partner.</span><span class="sxs-lookup"><span data-stu-id="b1e69-109">However, before you can create an agreement, you must have added at least two partners tooyour integration account.</span></span> <span data-ttu-id="b1e69-110">L'organizzazione deve far parte del contratto di hello hello **partner host**.</span><span class="sxs-lookup"><span data-stu-id="b1e69-110">Your organization must be part of hello agreement as hello **host partner**.</span></span> <span data-ttu-id="b1e69-111">Hello altri partner, o **partner guest** rappresenta hello organizzazione che scambia messaggi con l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="b1e69-111">hello other partner, or **guest partner** represents hello organization that exchanges messages with your organization.</span></span> <span data-ttu-id="b1e69-112">partner guest Hello può essere un'altra società, o anche un reparto dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="b1e69-112">hello guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="b1e69-113">Dopo aver aggiunto i partner, è possibile creare un contratto.</span><span class="sxs-lookup"><span data-stu-id="b1e69-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="b1e69-114">Ricevere e inviare le impostazioni sono orientate da hello punto di vista di hello Partner ospitato.</span><span class="sxs-lookup"><span data-stu-id="b1e69-114">Receive and Send settings are oriented from hello point of view of hello Hosted Partner.</span></span> <span data-ttu-id="b1e69-115">Ad esempio, hello impostazioni di ricezione in un contratto di determinare come partner di hello ospitato riceve i messaggi inviati da un partner guest.</span><span class="sxs-lookup"><span data-stu-id="b1e69-115">For example, hello receive settings in an agreement determine how hello hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="b1e69-116">Analogamente, le impostazioni di invio hello contratto hello indicano come partner ospitato hello invia al partner guest toohello di messaggi.</span><span class="sxs-lookup"><span data-stu-id="b1e69-116">Likewise, hello send settings on hello agreement indicate how hello hosted partner sends messages toohello guest partner.</span></span>

## <a name="how-toocreate-a-partner"></a><span data-ttu-id="b1e69-117">Come toocreate un partner?</span><span class="sxs-lookup"><span data-stu-id="b1e69-117">How toocreate a partner?</span></span>

1. <span data-ttu-id="b1e69-118">Nel portale di Azure hello, selezionare **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="b1e69-118">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="b1e69-119">Nella casella di ricerca hello filtro immettere **integrazione**, quindi selezionare **account di integrazione** nell'elenco risultati hello.</span><span class="sxs-lookup"><span data-stu-id="b1e69-119">In hello filter search box, enter **integration**, then select **Integration Accounts** in hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="b1e69-120">Selezionare l'account di integrazione hello in cui si desidera tooadd i partner.</span><span class="sxs-lookup"><span data-stu-id="b1e69-120">Select hello integration account where you want tooadd your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="b1e69-121">Seleziona hello **partner** riquadro.</span><span class="sxs-lookup"><span data-stu-id="b1e69-121">Select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="b1e69-122">Nel Pannello di partner hello, scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b1e69-122">In hello Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="b1e69-123">Immettere il nome del partner, quindi selezionare un **Qualificatore**.</span><span class="sxs-lookup"><span data-stu-id="b1e69-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="b1e69-124">Infine, immettere un **valore** toohelp identificare documenti che entrano in App.</span><span class="sxs-lookup"><span data-stu-id="b1e69-124">Finally, enter a **Value** toohelp identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="b1e69-125">stato di avanzamento hello toosee per il processo di creazione di partner, seleziona hello *campanello* icona di notifica.</span><span class="sxs-lookup"><span data-stu-id="b1e69-125">toosee hello progress for your partner creation process, select hello *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="b1e69-126">tooconfirm che nuovo partner sono stati aggiunti, seleziona hello **partner** riquadro.</span><span class="sxs-lookup"><span data-stu-id="b1e69-126">tooconfirm that your new partners were successfully added, select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="b1e69-127">Dopo aver selezionato il riquadro di partner hello, si noterà anche partner appena aggiunto nel Pannello di hello partner.</span><span class="sxs-lookup"><span data-stu-id="b1e69-127">After you select hello Partners tile, you'll also see  newly added partners in hello Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-tooedit-existing-partners-in-your-integration-account"></a><span data-ttu-id="b1e69-128">Tooedit esistente come partner nell'account di integrazione</span><span class="sxs-lookup"><span data-stu-id="b1e69-128">How tooedit existing partners in your integration account</span></span>

1. <span data-ttu-id="b1e69-129">Seleziona hello **partner** riquadro.</span><span class="sxs-lookup"><span data-stu-id="b1e69-129">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="b1e69-130">Dopo l'apertura di blade partner hello, selezionare il partner di hello desiderato tooedit.</span><span class="sxs-lookup"><span data-stu-id="b1e69-130">After hello Partners blade opens, select hello partner you want tooedit.</span></span>
3. <span data-ttu-id="b1e69-131">In hello **aggiornamento Partner** riquadro, apportare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="b1e69-131">On hello **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="b1e69-132">Al termine, scegliere **salvare**, o selezionare le modifiche, toocancel **ignorare**.</span><span class="sxs-lookup"><span data-stu-id="b1e69-132">After you're done, choose **Save**, or toocancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-toodelete-a-partner"></a><span data-ttu-id="b1e69-133">Come toodelete un partner</span><span class="sxs-lookup"><span data-stu-id="b1e69-133">How toodelete a partner</span></span>

1. <span data-ttu-id="b1e69-134">Seleziona hello **partner** riquadro.</span><span class="sxs-lookup"><span data-stu-id="b1e69-134">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="b1e69-135">Dopo l'apertura di blade Partner hello, selezionare il partner di hello che si desidera toodelete.</span><span class="sxs-lookup"><span data-stu-id="b1e69-135">After hello Partner blade opens, select hello partner that you want toodelete.</span></span>
3. <span data-ttu-id="b1e69-136">Scegliere **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="b1e69-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="b1e69-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b1e69-137">Next steps</span></span>
* [<span data-ttu-id="b1e69-138">Altre informazioni sui contratti</span><span class="sxs-lookup"><span data-stu-id="b1e69-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Informazioni sui contratti di Enterprise Integration")  


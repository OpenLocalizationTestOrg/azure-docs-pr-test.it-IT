---
title: Creare partner per i messaggi Business to Business (B2B) - App per la logica di Azure | Documentazione Microsoft
description: Informazioni su come aggiungere partner al proprio account di integrazione con Enterprise Integration Pack e App per la logica
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
ms.openlocfilehash: 950cb449b53f400f0f0f860caf5415bbb5212269
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="fc9b6-103">Aggiungere o aggiornare i partner nei contratti Business to Business nel proprio flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="fc9b6-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="fc9b6-104">I partner sono le entità che partecipano alle transazioni e allo scambio di messaggi Business-To-Business (B2B).</span><span class="sxs-lookup"><span data-stu-id="fc9b6-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="fc9b6-105">Prima di poter creare i partner che rappresentano l'utente e l'altra organizzazione nelle transazioni, è necessario che entrambe le parti condividano le informazioni che identificano e convalidano i messaggi inviati.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="fc9b6-106">Dopo aver definito questi dettagli e quando si è pronti per avviare una relazione commerciale, è possibile creare i partner nell'account di integrazione che rappresentino entrambe le parti.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-106">After you discuss these details and are ready to start your business relationship, you can create partners in your integration account to represent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="fc9b6-107">Che ruoli hanno i partner nell'account di integrazione?</span><span class="sxs-lookup"><span data-stu-id="fc9b6-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="fc9b6-108">Per definire i dettagli dello scambio di messaggi tra i partner, è necessario creare contratti tra i partner.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-108">To define details about the messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="fc9b6-109">Tuttavia, prima di creare un contratto è necessario aggiungere almeno due partner all'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-109">However, before you can create an agreement, you must have added at least two partners to your integration account.</span></span> <span data-ttu-id="fc9b6-110">L'organizzazione deve far parte del contratto in qualità di **partner host**.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-110">Your organization must be part of the agreement as the **host partner**.</span></span> <span data-ttu-id="fc9b6-111">L'altro partner, o **partner guest**, rappresenta l'organizzazione che scambia i messaggi con l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-111">The other partner, or **guest partner** represents the organization that exchanges messages with your organization.</span></span> <span data-ttu-id="fc9b6-112">Il partner guest può essere un'altra società o anche un reparto all'interno della stessa organizzazione.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-112">The guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="fc9b6-113">Dopo aver aggiunto i partner, è possibile creare un contratto.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="fc9b6-114">Le impostazioni per la ricezione e l'invio sono configurate dal punto di vista del partner host.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-114">Receive and Send settings are oriented from the point of view of the Hosted Partner.</span></span> <span data-ttu-id="fc9b6-115">Le impostazioni di ricezione del contratto, ad esempio, determinano la modalità con cui il partner host riceve i messaggi inviati da un partner guest.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-115">For example, the receive settings in an agreement determine how the hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="fc9b6-116">Analogamente, le impostazioni di invio del contratto indicano in che modo il partner host invia messaggi al partner guest.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-116">Likewise, the send settings on the agreement indicate how the hosted partner sends messages to the guest partner.</span></span>

## <a name="how-to-create-a-partner"></a><span data-ttu-id="fc9b6-117">Procedura: Creare un partner</span><span class="sxs-lookup"><span data-stu-id="fc9b6-117">How to create a partner?</span></span>

1. <span data-ttu-id="fc9b6-118">Nel Portale di Azure selezionare **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-118">In the Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="fc9b6-119">Nella casella di ricerca per filtro immettere **integrazione**, quindi selezionare **Account di integrazione** dall'elenco dei risultati.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-119">In the filter search box, enter **integration**, then select **Integration Accounts** in the results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="fc9b6-120">Selezionare l'account di integrazione a cui si desidera aggiungere i partner.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-120">Select the integration account where you want to add your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="fc9b6-121">Selezionare il riquadro **Partner** .</span><span class="sxs-lookup"><span data-stu-id="fc9b6-121">Select the **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="fc9b6-122">Nel pannello dei partner, scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-122">In the Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="fc9b6-123">Immettere il nome del partner, quindi selezionare un **Qualificatore**.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="fc9b6-124">Infine, inserire un **valore** per identificare i documenti ricevuti dalle app.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-124">Finally, enter a **Value** to help identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="fc9b6-125">Selezionare l'icona di notifica a forma di *campana* per visualizzare lo stato di avanzamento del processo di creazione del partner.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-125">To see the progress for your partner creation process, select the *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="fc9b6-126">Per verificare che i nuovi partner sono stati aggiunti correttamente, selezionare il riquadro **Partner**.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-126">To confirm that your new partners were successfully added, select the **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="fc9b6-127">Dopo aver selezionato il riquadro Partner, anche i partner appena aggiunti vengono visualizzati nel pannello Partner.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-127">After you select the Partners tile, you'll also see  newly added partners in the Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-to-edit-existing-partners-in-your-integration-account"></a><span data-ttu-id="fc9b6-128">Come modificare i partner esistenti nell'account di integrazione</span><span class="sxs-lookup"><span data-stu-id="fc9b6-128">How to edit existing partners in your integration account</span></span>

1. <span data-ttu-id="fc9b6-129">Selezionare il riquadro **Partner** .</span><span class="sxs-lookup"><span data-stu-id="fc9b6-129">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="fc9b6-130">Selezionare il partner che si desidera modificare quando si apre il pannello Partner.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-130">After the Partners blade opens, select the partner you want to edit.</span></span>
3. <span data-ttu-id="fc9b6-131">Nel riquadro **Aggiorna partner** apportare le modifiche necessarie.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-131">On the **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="fc9b6-132">Al termine, scegliere **Salva** o **Ignora** per annullare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-132">After you're done, choose **Save**, or to cancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-to-delete-a-partner"></a><span data-ttu-id="fc9b6-133">Procedura: Eliminare un partner</span><span class="sxs-lookup"><span data-stu-id="fc9b6-133">How to delete a partner</span></span>

1. <span data-ttu-id="fc9b6-134">Selezionare il riquadro **Partner** .</span><span class="sxs-lookup"><span data-stu-id="fc9b6-134">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="fc9b6-135">Selezionare il partner che si desidera eliminare quando si apre il pannello Partner.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-135">After the Partner blade opens, select the partner that you want to delete.</span></span>
3. <span data-ttu-id="fc9b6-136">Scegliere **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="fc9b6-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="fc9b6-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fc9b6-137">Next steps</span></span>
* [<span data-ttu-id="fc9b6-138">Altre informazioni sui contratti</span><span class="sxs-lookup"><span data-stu-id="fc9b6-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Informazioni sui contratti di Enterprise Integration")  


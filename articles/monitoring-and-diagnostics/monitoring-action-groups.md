---
title: Creare e gestire gruppi di azione nel portale di Azure | Microsoft Docs
description: Informazioni su come creare e gestire gruppi di azione nel portale di Azure.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: ea15705bf02d9773507c6cb59f2da4c1dd0f9d77
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-action-groups-in-the-azure-portal"></a><span data-ttu-id="2b6ef-103">Creare e gestire gruppi di azione nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2b6ef-103">Create and manage action groups in the Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="2b6ef-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2b6ef-104">Overview</span></span> ##
<span data-ttu-id="2b6ef-105">Questo articolo illustra come creare e gestire gruppi di azione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-105">This article shows you how to create and manage action groups in the Azure portal.</span></span>

<span data-ttu-id="2b6ef-106">I gruppi di azione consentono di configurare un elenco di azioni.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="2b6ef-107">È possibile usare questi gruppi quando si definiscono gli avvisi del log attività.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="2b6ef-108">Questi gruppi possono essere riusati da ogni avviso del log attività definito, assicurando che vengono eseguite le stesse azioni ogni volta che viene generato l'avviso del log attività.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-108">These groups can then be reused by each activity log alert you define, ensuring that the same actions are taken each time the activity log alert is triggered.</span></span>

<span data-ttu-id="2b6ef-109">Un gruppo di azione può avere fino a 10 tipi di azioni.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-109">An action group can have up to 10 of each action type.</span></span> <span data-ttu-id="2b6ef-110">Ogni azione è composta dalle seguenti proprietà:</span><span class="sxs-lookup"><span data-stu-id="2b6ef-110">Each action is made up of the following properties:</span></span>

* <span data-ttu-id="2b6ef-111">**Nome:** un identificatore univoco all'interno del gruppo di azione.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-111">**Name**: A unique identifier within the action group.</span></span>  
* <span data-ttu-id="2b6ef-112">**Tipo di azione**: inviare un SMS, un messaggio di posta elettronica o chiamare un webhook.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="2b6ef-113">**Dettagli**: l'URI del webhook, il numero di telefono o l'indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-113">**Details**: The corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="2b6ef-114">Per informazioni sull'uso dei modelli di Azure Resource Manager per configurare i gruppi di azione: [Modelli di Resource Manager per il gruppo di azione](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="2b6ef-114">For information on how to use Azure Resource Manager templates to configure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-the-azure-portal"></a><span data-ttu-id="2b6ef-115">Creare un gruppo di azione usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2b6ef-115">Create an action group by using the Azure portal</span></span> ##
1. <span data-ttu-id="2b6ef-116">Nel [portale](https://portal.azure.com)selezionare **Monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-116">In the [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="2b6ef-117">Il pannello **Monitoraggio** consolida tutte le impostazioni e i dati di monitoraggio in una vista.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-117">The **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    ![Servizio "Monitoraggio"](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="2b6ef-119">Nella sezione **Log attività** selezionare **Gruppi di azione**.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-119">In the **Activity log** section, select **Action groups**.</span></span>

    ![Scheda "Gruppi di azione"](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="2b6ef-121">Selezionare **Aggiungi gruppo di azione** e compilare i campi.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-121">Select **Add action group**, and fill in the fields.</span></span>

    ![Comando "Aggiungi gruppo di azione"](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="2b6ef-123">Immettere un nome nella casella **Nome gruppo di azione** e un nome nella casella **Nome breve gruppo di azione**.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-123">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="2b6ef-124">Il nome breve viene usato al posto del nome completo di un gruppo di azione quando le notifiche vengono inviate usando questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-124">The short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![Finestra di dialogo "Aggiungi gruppo di azione"](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="2b6ef-126">Nella casella **Sottoscrizione** viene inserita automaticamente la sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-126">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="2b6ef-127">Il gruppo di azione verrà salvato in questa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-127">This subscription is the one in which the action group is saved.</span></span>

6. <span data-ttu-id="2b6ef-128">Selezionare il **gruppo di risorse** in cui verrà salvato il gruppo di azione.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-128">Select the **Resource group** in which the action group is saved.</span></span>

7. <span data-ttu-id="2b6ef-129">Definire un elenco di azioni fornendo i dati di ogni azione:</span><span class="sxs-lookup"><span data-stu-id="2b6ef-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="2b6ef-130">a.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-130">a.</span></span> <span data-ttu-id="2b6ef-131">**Nome**: immettere un identificatore univoco per questa azione.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="2b6ef-132">b.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-132">b.</span></span> <span data-ttu-id="2b6ef-133">**Tipo di azione**: selezionare webhook, posta elettronica o SMS.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="2b6ef-134">c.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-134">c.</span></span> <span data-ttu-id="2b6ef-135">**Dettagli**: in base al tipo di azione immettere un numero di telefono, un indirizzo di posta elettronica o l'URI del webhook.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-135">**Details**: Based on the action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="2b6ef-136">Fare clic su **OK** per creare il gruppo di azione.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-136">Select **OK** to create the action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="2b6ef-137">Gestire i gruppi di azione</span><span class="sxs-lookup"><span data-stu-id="2b6ef-137">Manage your action groups</span></span> ##
<span data-ttu-id="2b6ef-138">Dopo la creazione, il gruppo di azione sarà visibile nella sezione **Gruppi di azione** del pannello **Monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-138">After you create an action group, it's visible in the **Action groups** section of the **Monitor** blade.</span></span> <span data-ttu-id="2b6ef-139">Selezionare il gruppo di azione da gestire per:</span><span class="sxs-lookup"><span data-stu-id="2b6ef-139">Select the action group you want to manage to:</span></span>

* <span data-ttu-id="2b6ef-140">Aggiungere, modificare o rimuovere azioni.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="2b6ef-141">Eliminare il gruppo di azione.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-141">Delete the action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b6ef-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2b6ef-142">Next steps</span></span> ##
* <span data-ttu-id="2b6ef-143">Altre informazioni sul [Comportamento degli avvisi SMS](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="2b6ef-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="2b6ef-144">Leggere le [informazioni sullo schema webhook degli avvisi del log attività](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="2b6ef-144">Gain an [understanding of the activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="2b6ef-145">Altre informazioni sulla [limitazione della frequenza](monitoring-alerts-rate-limiting.md) degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="2b6ef-146">Leggere una [panoramica degli avvisi del log attività](monitoring-overview-alerts.md) e informazioni su come ricevere gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="2b6ef-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span>  
* <span data-ttu-id="2b6ef-147">Informazioni su come [configurare gli avvisi ogni volta che viene inviata una notifica sull'integrità del servizio](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="2b6ef-147">Learn how to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>

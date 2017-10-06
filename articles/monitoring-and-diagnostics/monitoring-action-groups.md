---
title: aaaCreate e gestire gruppi di azioni di hello portale di Azure | Documenti Microsoft
description: Informazioni su come toocreate e gestire gruppi di azioni di hello portale di Azure.
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
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a><span data-ttu-id="94e53-103">Creare e gestire gruppi di azioni di hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="94e53-103">Create and manage action groups in hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="94e53-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="94e53-104">Overview</span></span> ##
<span data-ttu-id="94e53-105">In questo articolo illustra come toocreate e gestire gruppi di azioni di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="94e53-105">This article shows you how toocreate and manage action groups in hello Azure portal.</span></span>

<span data-ttu-id="94e53-106">I gruppi di azione consentono di configurare un elenco di azioni.</span><span class="sxs-lookup"><span data-stu-id="94e53-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="94e53-107">È possibile usare questi gruppi quando si definiscono gli avvisi del log attività.</span><span class="sxs-lookup"><span data-stu-id="94e53-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="94e53-108">Questi gruppi possono essere riutilizzati da definire, assicurando che hello stesse azioni vengono eseguite ogni volta che viene attivato l'avviso di log attività hello ogni avviso di log attività.</span><span class="sxs-lookup"><span data-stu-id="94e53-108">These groups can then be reused by each activity log alert you define, ensuring that hello same actions are taken each time hello activity log alert is triggered.</span></span>

<span data-ttu-id="94e53-109">Un gruppo di azioni può esistere fino a too10 di ogni tipo di azione.</span><span class="sxs-lookup"><span data-stu-id="94e53-109">An action group can have up too10 of each action type.</span></span> <span data-ttu-id="94e53-110">Ogni azione è costituito da hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="94e53-110">Each action is made up of hello following properties:</span></span>

* <span data-ttu-id="94e53-111">**Nome**: un identificatore univoco all'interno di gruppo di azioni di hello.</span><span class="sxs-lookup"><span data-stu-id="94e53-111">**Name**: A unique identifier within hello action group.</span></span>  
* <span data-ttu-id="94e53-112">**Tipo di azione**: inviare un SMS, un messaggio di posta elettronica o chiamare un webhook.</span><span class="sxs-lookup"><span data-stu-id="94e53-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="94e53-113">**Dettagli**: hello corrispondente numero di telefono, indirizzo di posta elettronica o webhook URI.</span><span class="sxs-lookup"><span data-stu-id="94e53-113">**Details**: hello corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="94e53-114">Per informazioni su come toouse gruppi di azioni di gestione risorse di Azure modelli tooconfigure, vedere [modelli di gestione risorse di gruppo azione](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="94e53-114">For information on how toouse Azure Resource Manager templates tooconfigure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="94e53-115">Creare un gruppo di azioni tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="94e53-115">Create an action group by using hello Azure portal</span></span> ##
1. <span data-ttu-id="94e53-116">In hello [portale](https://portal.azure.com)selezionare **monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="94e53-116">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="94e53-117">Hello **monitoraggio** pannello consolida tutte le impostazioni e dati in una visualizzazione monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="94e53-117">hello **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    ![Hello "Monitoraggio" del servizio](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="94e53-119">In hello **log attività** selezionare **gruppi di azioni**.</span><span class="sxs-lookup"><span data-stu-id="94e53-119">In hello **Activity log** section, select **Action groups**.</span></span>

    ![scheda "Gruppi di azioni" Hello](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="94e53-121">Selezionare **Aggiungi gruppo di azioni**e compilare i campi di hello.</span><span class="sxs-lookup"><span data-stu-id="94e53-121">Select **Add action group**, and fill in hello fields.</span></span>

    ![comando "Aggiungi gruppo di azioni di" Hello](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="94e53-123">Immettere un nome in hello **nome del gruppo di azione** e immettere un nome in hello **nome breve** casella.</span><span class="sxs-lookup"><span data-stu-id="94e53-123">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="94e53-124">nome breve Hello viene utilizzato al posto di un nome di un gruppo completo azione quando le notifiche vengono inviate utilizzando questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="94e53-124">hello short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![la finestra di dialogo gruppo di azioni Aggiungi Hello"](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="94e53-126">Hello **sottoscrizione** casella autofills con la sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="94e53-126">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="94e53-127">Questa sottoscrizione è hello uno nel gruppo di azioni quali hello viene salvato.</span><span class="sxs-lookup"><span data-stu-id="94e53-127">This subscription is hello one in which hello action group is saved.</span></span>

6. <span data-ttu-id="94e53-128">Seleziona hello **gruppo di risorse** in cui azione hello gruppo viene salvato.</span><span class="sxs-lookup"><span data-stu-id="94e53-128">Select hello **Resource group** in which hello action group is saved.</span></span>

7. <span data-ttu-id="94e53-129">Definire un elenco di azioni fornendo i dati di ogni azione:</span><span class="sxs-lookup"><span data-stu-id="94e53-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="94e53-130">a.</span><span class="sxs-lookup"><span data-stu-id="94e53-130">a.</span></span> <span data-ttu-id="94e53-131">**Nome**: immettere un identificatore univoco per questa azione.</span><span class="sxs-lookup"><span data-stu-id="94e53-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="94e53-132">b.</span><span class="sxs-lookup"><span data-stu-id="94e53-132">b.</span></span> <span data-ttu-id="94e53-133">**Tipo di azione**: selezionare webhook, posta elettronica o SMS.</span><span class="sxs-lookup"><span data-stu-id="94e53-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="94e53-134">c.</span><span class="sxs-lookup"><span data-stu-id="94e53-134">c.</span></span> <span data-ttu-id="94e53-135">**Dettagli**: basato sul tipo di azione hello, immettere un numero di telefono, indirizzo di posta elettronica o webhook URI.</span><span class="sxs-lookup"><span data-stu-id="94e53-135">**Details**: Based on hello action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="94e53-136">Selezionare **OK** toocreate gruppo di azioni hello.</span><span class="sxs-lookup"><span data-stu-id="94e53-136">Select **OK** toocreate hello action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="94e53-137">Gestire i gruppi di azione</span><span class="sxs-lookup"><span data-stu-id="94e53-137">Manage your action groups</span></span> ##
<span data-ttu-id="94e53-138">Dopo aver creato un gruppo di azioni, è visibile in hello **gruppi di azioni** sezione di hello **monitoraggio** blade.</span><span class="sxs-lookup"><span data-stu-id="94e53-138">After you create an action group, it's visible in hello **Action groups** section of hello **Monitor** blade.</span></span> <span data-ttu-id="94e53-139">Selezionare il gruppo di azioni hello desiderato toomanage per:</span><span class="sxs-lookup"><span data-stu-id="94e53-139">Select hello action group you want toomanage to:</span></span>

* <span data-ttu-id="94e53-140">Aggiungere, modificare o rimuovere azioni.</span><span class="sxs-lookup"><span data-stu-id="94e53-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="94e53-141">Eliminare il gruppo di azioni di hello.</span><span class="sxs-lookup"><span data-stu-id="94e53-141">Delete hello action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94e53-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="94e53-142">Next steps</span></span> ##
* <span data-ttu-id="94e53-143">Altre informazioni sul [Comportamento degli avvisi SMS](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="94e53-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="94e53-144">Ottenere un [informazioni dello schema di avviso webhook log attività hello](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="94e53-144">Gain an [understanding of hello activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="94e53-145">Altre informazioni sulla [limitazione della frequenza](monitoring-alerts-rate-limiting.md) degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="94e53-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="94e53-146">Ottenere un [panoramica degli avvisi di log attività](monitoring-overview-alerts.md)e informazioni su come tooreceive avvisi.</span><span class="sxs-lookup"><span data-stu-id="94e53-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="94e53-147">Informazioni su come troppo[configurare gli avvisi ogni volta che viene registrata una notifica di integrità del servizio](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="94e53-147">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>

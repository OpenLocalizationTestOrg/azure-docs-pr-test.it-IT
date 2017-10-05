---
title: "Ricevere gli avvisi del log attività nelle notifiche del servizio | Microsoft Docs"
description: Ricevere le notifiche tramite SMS, posta elettronica o webhook nel servizio di Azure.
author: johnkemnetz
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
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: bf6a98fd7e7e11764bef174f9efd0635fa7efe9a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="c2196-103">Creare gli avvisi del log attività per le notifiche del servizio</span><span class="sxs-lookup"><span data-stu-id="c2196-103">Create activity log alerts on service notifications</span></span>
## <a name="overview"></a><span data-ttu-id="c2196-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c2196-104">Overview</span></span>
<span data-ttu-id="c2196-105">Questo articolo descrive come impostare gli avvisi del log attività per le notifiche sull'integrità del servizio usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2196-105">This article shows you how to set up activity log alerts for service health notifications by using the Azure portal.</span></span>  

<span data-ttu-id="c2196-106">È possibile ricevere un avviso quando Azure invia le notifiche sull'integrità del servizio alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2196-106">You can receive an alert when Azure sends service health notifications to your Azure subscription.</span></span> <span data-ttu-id="c2196-107">È possibile configurare l'avviso in base a:</span><span class="sxs-lookup"><span data-stu-id="c2196-107">You can configure the alert based on:</span></span>

- <span data-ttu-id="c2196-108">La classe di notifica sull'integrità del servizio, ad esempio evento imprevisto, manutenzione, informazioni.</span><span class="sxs-lookup"><span data-stu-id="c2196-108">The class of service health notification (incident, maintenance, information, etc.).</span></span>
- <span data-ttu-id="c2196-109">I servizi interessati.</span><span class="sxs-lookup"><span data-stu-id="c2196-109">The service(s) affected.</span></span>
- <span data-ttu-id="c2196-110">Le aree interessate.</span><span class="sxs-lookup"><span data-stu-id="c2196-110">The region(s) affected.</span></span>
- <span data-ttu-id="c2196-111">Lo stato della notifica (attivo o risolto).</span><span class="sxs-lookup"><span data-stu-id="c2196-111">The status of the notification (active vs. resolved).</span></span>
- <span data-ttu-id="c2196-112">Il livello delle notifiche (informativo, avviso, errore).</span><span class="sxs-lookup"><span data-stu-id="c2196-112">The level of the notifications (informational, warning, error).</span></span>

<span data-ttu-id="c2196-113">È anche possibile configurare l'utente a cui deve essere inviato l'avviso:</span><span class="sxs-lookup"><span data-stu-id="c2196-113">You also can configure who the alert should be sent to:</span></span>

- <span data-ttu-id="c2196-114">Selezionare un gruppo di azione esistente.</span><span class="sxs-lookup"><span data-stu-id="c2196-114">Select an existing action group.</span></span>
- <span data-ttu-id="c2196-115">Creare un nuovo gruppo di azione che può essere usato per avvisi futuri.</span><span class="sxs-lookup"><span data-stu-id="c2196-115">Create a new action group (that can be used for future alerts).</span></span>

<span data-ttu-id="c2196-116">Per altre informazioni sui gruppi di azioni, vedere [Creare e gestire gruppi di azioni](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="c2196-116">To learn more about action groups, see [Create and manage action groups](monitoring-action-groups.md).</span></span>

<span data-ttu-id="c2196-117">Per informazioni su come configurare gli avvisi di notifica sull'integrità del servizio usando i modelli Azure Resource Manager, vedere [Modelli di Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="c2196-117">For information on how to configure service health notification alerts by using Azure Resource Manager templates, see [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-the-azure-portal"></a><span data-ttu-id="c2196-118">Creare un avviso per una notifica sull'integrità del servizio per un nuovo gruppo di azione usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c2196-118">Create an alert on a service health notification for a new action group by using the Azure portal</span></span>
1. <span data-ttu-id="c2196-119">Nel [portale](https://portal.azure.com)selezionare **Monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="c2196-119">In the [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Servizio "Monitoraggio"](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. <span data-ttu-id="c2196-121">Nella sezione **Log attività** selezionare **Avvisi**.</span><span class="sxs-lookup"><span data-stu-id="c2196-121">In the **Activity log** section, select **Alerts**.</span></span>

    ![Scheda "Avvisi"](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. <span data-ttu-id="c2196-123">Selezionare il comando **Aggiungi avviso del log attività** e compilare i campi.</span><span class="sxs-lookup"><span data-stu-id="c2196-123">Select **Add activity log alert**, and fill in the fields.</span></span>

    ![Comando "Aggiungi avviso del log attività"](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. <span data-ttu-id="c2196-125">Immettere un nome nella casella **Nome avviso del log attività** e specificare una **descrizione**.</span><span class="sxs-lookup"><span data-stu-id="c2196-125">Enter a name in the **Activity log alert name** box, and provide a **Description**.</span></span>

    ![Finestra di dialogo "Aggiungi avviso del log attività"](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. <span data-ttu-id="c2196-127">Nella casella **Sottoscrizione** viene inserita automaticamente la sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="c2196-127">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="c2196-128">Questa sottoscrizione viene usata per salvare l'avviso del log attività.</span><span class="sxs-lookup"><span data-stu-id="c2196-128">This subscription is used to save the activity log alert.</span></span> <span data-ttu-id="c2196-129">Questa è la sottoscrizione in cui verrà distribuita la risorsa di avviso e in cui verranno monitorati gli eventi nel log attività.</span><span class="sxs-lookup"><span data-stu-id="c2196-129">The alert resource is deployed to this subscription and monitors events in the activity log for it.</span></span>

6. <span data-ttu-id="c2196-130">Selezionare il **gruppo di risorse** in cui verrà creata la risorsa di avviso.</span><span class="sxs-lookup"><span data-stu-id="c2196-130">Select the **Resource group** in which the alert resource is created.</span></span> <span data-ttu-id="c2196-131">Non è il gruppo di risorse che viene monitorato dall'avviso,</span><span class="sxs-lookup"><span data-stu-id="c2196-131">This isn't the resource group that's monitored by the alert.</span></span> <span data-ttu-id="c2196-132">ma è quello in cui si trova la risorsa di avviso.</span><span class="sxs-lookup"><span data-stu-id="c2196-132">Instead, it's the resource group where the alert resource is located.</span></span>

7. <span data-ttu-id="c2196-133">Nella casella **Categoria di eventi** , selezionare **Integrità dei servizi**.</span><span class="sxs-lookup"><span data-stu-id="c2196-133">In the **Event category** box, select **Service Health**.</span></span> <span data-ttu-id="c2196-134">Facoltativamente, selezionare **Servizio**, **Area**, **Tipo**, **Stato** e **Livello** delle notifiche sull'integrità del servizio che si vuole ricevere.</span><span class="sxs-lookup"><span data-stu-id="c2196-134">Optionally, select the **Service**, **Region**, **Type**, **Status**, and **Level** of service health notifications that you want to receive.</span></span>

8. <span data-ttu-id="c2196-135">In **Avvisi tramite** selezionare il pulsante **Nuovo** gruppo di azione.</span><span class="sxs-lookup"><span data-stu-id="c2196-135">Under **Alert via**, select the **New** action group button.</span></span> <span data-ttu-id="c2196-136">Immettere un nome nella casella **Nome gruppo di azione** e un nome nella casella **Nome breve gruppo di azione**.</span><span class="sxs-lookup"><span data-stu-id="c2196-136">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="c2196-137">Viene fatto riferimento al nome breve nelle notifiche inviate all'attivazione dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="c2196-137">The short name is referenced in the notifications that are sent when this alert fires.</span></span>

9. <span data-ttu-id="c2196-138">Definire un elenco di ricevitori specificando i dati seguenti relativi al ricevitore:</span><span class="sxs-lookup"><span data-stu-id="c2196-138">Define a list of receivers by providing the receiver's:</span></span>

    <span data-ttu-id="c2196-139">a.</span><span class="sxs-lookup"><span data-stu-id="c2196-139">a.</span></span> <span data-ttu-id="c2196-140">**Nome**: immettere il nome, l'alias o l'identificatore del ricevitore.</span><span class="sxs-lookup"><span data-stu-id="c2196-140">**Name**: Enter the receiver’s name, alias, or identifier.</span></span>

    <span data-ttu-id="c2196-141">b.</span><span class="sxs-lookup"><span data-stu-id="c2196-141">b.</span></span> <span data-ttu-id="c2196-142">**Tipo di azione**: selezionare webhook, posta elettronica o SMS.</span><span class="sxs-lookup"><span data-stu-id="c2196-142">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="c2196-143">c.</span><span class="sxs-lookup"><span data-stu-id="c2196-143">c.</span></span> <span data-ttu-id="c2196-144">**Dettagli:** in base al tipo di azione selezionato, immettere un numero di telefono, un indirizzo di posta elettronica o l'URI del webhook.</span><span class="sxs-lookup"><span data-stu-id="c2196-144">**Details**: Based on the action type chosen, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="c2196-145">Fare clic su **OK** per creare l'avviso.</span><span class="sxs-lookup"><span data-stu-id="c2196-145">Select **OK** to create the alert.</span></span>

<span data-ttu-id="c2196-146">Entro pochi minuti, l'avviso diventa attivo e inizia ad attivarsi in base alle condizioni specificate al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="c2196-146">Within a few minutes, the alert is active and begins to trigger based on the conditions you specified during creation.</span></span>

<span data-ttu-id="c2196-147">Per informazioni sullo schema webhook per gli avvisi del log attività, vedere [Webhook per gli avvisi del log attività di Azure](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="c2196-147">For information on the webhook schema for activity log alerts, see [Webhooks for Azure activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="c2196-148">Il gruppo di azione definito in questi passaggi è riutilizzabile come gruppo di azione esistente per tutte le future definizioni di avviso.</span><span class="sxs-lookup"><span data-stu-id="c2196-148">The action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-the-azure-portal"></a><span data-ttu-id="c2196-149">Creare un avviso per una notifica sull'integrità del servizio per un gruppo di azione esistente usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c2196-149">Create an alert on a service health notification for an existing action group by using the Azure portal</span></span>

1. <span data-ttu-id="c2196-150">Seguire i passaggi da 1 a 7 nella sezione precedente per creare una notifica sull'integrità del servizio.</span><span class="sxs-lookup"><span data-stu-id="c2196-150">Follow steps 1 through 7 in the previous section to create your service health notification.</span></span> 

2. <span data-ttu-id="c2196-151">In **Avvisi tramite** selezionare il pulsante Gruppo di azione **esistente**.</span><span class="sxs-lookup"><span data-stu-id="c2196-151">Under **Alert via**, select the **Existing** action group button.</span></span> <span data-ttu-id="c2196-152">Selezionare il gruppo di azioni appropriato.</span><span class="sxs-lookup"><span data-stu-id="c2196-152">Select the appropriate action group.</span></span>

3. <span data-ttu-id="c2196-153">Fare clic su **OK** per creare l'avviso.</span><span class="sxs-lookup"><span data-stu-id="c2196-153">Select **OK** to create the alert.</span></span>

<span data-ttu-id="c2196-154">Entro pochi minuti, l'avviso diventa attivo e inizia ad attivarsi in base alle condizioni specificate al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="c2196-154">Within a few minutes, the alert is active and begins to trigger based on the conditions you specified during creation.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="c2196-155">Gestire gli avvisi</span><span class="sxs-lookup"><span data-stu-id="c2196-155">Manage your alerts</span></span>

<span data-ttu-id="c2196-156">Dopo la creazione, l'avviso sarà visibile nella sezione **Avvisi** del pannello **Monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="c2196-156">After you create an alert, it's visible in the **Alerts** section of the **Monitor** blade.</span></span> <span data-ttu-id="c2196-157">Selezionare l'avviso da gestire per:</span><span class="sxs-lookup"><span data-stu-id="c2196-157">Select the alert you want to manage to:</span></span>

* <span data-ttu-id="c2196-158">Modificarlo.</span><span class="sxs-lookup"><span data-stu-id="c2196-158">Edit it.</span></span>
* <span data-ttu-id="c2196-159">Eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="c2196-159">Delete it.</span></span>
* <span data-ttu-id="c2196-160">Disabilitarlo o abilitarlo per interrompere temporaneamente o riprendere la ricezione delle notifiche relative all'avviso.</span><span class="sxs-lookup"><span data-stu-id="c2196-160">Disable or enable it, if you want to temporarily stop or resume receiving notifications for the alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2196-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c2196-161">Next steps</span></span>
- <span data-ttu-id="c2196-162">Informazioni sulle [notifiche per l'integrità del servizio](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="c2196-162">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="c2196-163">Informazioni sulla [limitazione della frequenza delle notifiche](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="c2196-163">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="c2196-164">Esaminare lo [schema webhook degli avvisi del log attività](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="c2196-164">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="c2196-165">Leggere una [panoramica degli avvisi del log attività](monitoring-overview-alerts.md) e informazioni su come ricevere gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="c2196-165">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span> 
- <span data-ttu-id="c2196-166">Altre informazioni sui [gruppi di azione](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="c2196-166">Learn more about [action groups](monitoring-action-groups.md).</span></span>

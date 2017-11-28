---
title: "gli avvisi del registro attività aaaReceive sulle notifiche di servizio | Documenti Microsoft"
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
ms.openlocfilehash: dd35e8f39d2a522efdae4dfed20779c992c1dd27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="c0506-103">Creare gli avvisi del log attività per le notifiche del servizio</span><span class="sxs-lookup"><span data-stu-id="c0506-103">Create activity log alerts on service notifications</span></span>
## <a name="overview"></a><span data-ttu-id="c0506-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c0506-104">Overview</span></span>
<span data-ttu-id="c0506-105">Questo articolo illustra come tooset backup log delle attività degli avvisi per le notifiche di integrità del servizio tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0506-105">This article shows you how tooset up activity log alerts for service health notifications by using hello Azure portal.</span></span>  

<span data-ttu-id="c0506-106">È possibile ricevere un avviso quando Azure invia servizio integrità notifiche tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0506-106">You can receive an alert when Azure sends service health notifications tooyour Azure subscription.</span></span> <span data-ttu-id="c0506-107">È possibile configurare l'avviso hello in base a:</span><span class="sxs-lookup"><span data-stu-id="c0506-107">You can configure hello alert based on:</span></span>

- <span data-ttu-id="c0506-108">classe Hello di notifica del servizio integrità (evento imprevisto, manutenzione, le informazioni e così via).</span><span class="sxs-lookup"><span data-stu-id="c0506-108">hello class of service health notification (incident, maintenance, information, etc.).</span></span>
- <span data-ttu-id="c0506-109">Hello servizi interessati.</span><span class="sxs-lookup"><span data-stu-id="c0506-109">hello service(s) affected.</span></span>
- <span data-ttu-id="c0506-110">aree di Hello interessate.</span><span class="sxs-lookup"><span data-stu-id="c0506-110">hello region(s) affected.</span></span>
- <span data-ttu-id="c0506-111">stato Hello della notifica di hello (attivo e risolti).</span><span class="sxs-lookup"><span data-stu-id="c0506-111">hello status of hello notification (active vs. resolved).</span></span>
- <span data-ttu-id="c0506-112">livello di Hello di notifiche di hello (errore, avviso, informativo).</span><span class="sxs-lookup"><span data-stu-id="c0506-112">hello level of hello notifications (informational, warning, error).</span></span>

<span data-ttu-id="c0506-113">È anche possibile configurare che deve essere inviato avviso hello:</span><span class="sxs-lookup"><span data-stu-id="c0506-113">You also can configure who hello alert should be sent to:</span></span>

- <span data-ttu-id="c0506-114">Selezionare un gruppo di azione esistente.</span><span class="sxs-lookup"><span data-stu-id="c0506-114">Select an existing action group.</span></span>
- <span data-ttu-id="c0506-115">Creare un nuovo gruppo di azione che può essere usato per avvisi futuri.</span><span class="sxs-lookup"><span data-stu-id="c0506-115">Create a new action group (that can be used for future alerts).</span></span>

<span data-ttu-id="c0506-116">toolearn ulteriori informazioni sui gruppi di azioni, vedere [creare e gestire gruppi di azioni](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="c0506-116">toolearn more about action groups, see [Create and manage action groups](monitoring-action-groups.md).</span></span>

<span data-ttu-id="c0506-117">Per informazioni su come tooconfigure notifica relativa all'integrità del servizio avvisi utilizzando i modelli di gestione risorse di Azure, vedere [modelli di gestione risorse](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="c0506-117">For information on how tooconfigure service health notification alerts by using Azure Resource Manager templates, see [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="c0506-118">Creare un avviso per una notifica di integrità del servizio per un nuovo gruppo di azione utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c0506-118">Create an alert on a service health notification for a new action group by using hello Azure portal</span></span>
1. <span data-ttu-id="c0506-119">In hello [portale](https://portal.azure.com)selezionare **monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="c0506-119">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Hello "Monitoraggio" del servizio](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. <span data-ttu-id="c0506-121">In hello **log attività** selezionare **avvisi**.</span><span class="sxs-lookup"><span data-stu-id="c0506-121">In hello **Activity log** section, select **Alerts**.</span></span>

    ![Nella scheda "Avvisi" Hello](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. <span data-ttu-id="c0506-123">Selezionare **Aggiungi avviso di log attività**e compilare i campi di hello.</span><span class="sxs-lookup"><span data-stu-id="c0506-123">Select **Add activity log alert**, and fill in hello fields.</span></span>

    ![comando "Aggiungi avviso registro attività" Hello](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. <span data-ttu-id="c0506-125">Immettere un nome in hello **nome dell'avviso log attività** e specificare un **descrizione**.</span><span class="sxs-lookup"><span data-stu-id="c0506-125">Enter a name in hello **Activity log alert name** box, and provide a **Description**.</span></span>

    ![finestra di dialogo "Aggiungi avviso registro attività" Hello](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. <span data-ttu-id="c0506-127">Hello **sottoscrizione** casella autofills con la sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="c0506-127">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="c0506-128">Questa sottoscrizione è di avviso di log attività hello toosave utilizzato.</span><span class="sxs-lookup"><span data-stu-id="c0506-128">This subscription is used toosave hello activity log alert.</span></span> <span data-ttu-id="c0506-129">risorsa avviso Hello è toothis distribuito gli eventi di sottoscrizione e i monitoraggi nel registro attività hello relativo.</span><span class="sxs-lookup"><span data-stu-id="c0506-129">hello alert resource is deployed toothis subscription and monitors events in hello activity log for it.</span></span>

6. <span data-ttu-id="c0506-130">Seleziona hello **gruppo di risorse** in cui hello avviso risorsa sono stati creati.</span><span class="sxs-lookup"><span data-stu-id="c0506-130">Select hello **Resource group** in which hello alert resource is created.</span></span> <span data-ttu-id="c0506-131">Gruppo di risorse hello monitorato dall'avviso hello non.</span><span class="sxs-lookup"><span data-stu-id="c0506-131">This isn't hello resource group that's monitored by hello alert.</span></span> <span data-ttu-id="c0506-132">In alternativa, è il gruppo di risorse hello risorse avviso hello in cui si trova.</span><span class="sxs-lookup"><span data-stu-id="c0506-132">Instead, it's hello resource group where hello alert resource is located.</span></span>

7. <span data-ttu-id="c0506-133">In hello **categoria di eventi** , quindi selezionare **servizio integrità**.</span><span class="sxs-lookup"><span data-stu-id="c0506-133">In hello **Event category** box, select **Service Health**.</span></span> <span data-ttu-id="c0506-134">Facoltativamente, selezionare hello **servizio**, **area**, **tipo**, **stato**, e **livello** del servizio notifiche di integrità che si desidera tooreceive.</span><span class="sxs-lookup"><span data-stu-id="c0506-134">Optionally, select hello **Service**, **Region**, **Type**, **Status**, and **Level** of service health notifications that you want tooreceive.</span></span>

8. <span data-ttu-id="c0506-135">In **avviso tramite**selezionare hello **New** pulsante di azione di gruppo.</span><span class="sxs-lookup"><span data-stu-id="c0506-135">Under **Alert via**, select hello **New** action group button.</span></span> <span data-ttu-id="c0506-136">Immettere un nome in hello **nome del gruppo di azione** e immettere un nome in hello **nome breve** casella.</span><span class="sxs-lookup"><span data-stu-id="c0506-136">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="c0506-137">nome breve Hello viene fatto riferimento nelle notifiche hello che vengono inviate quando viene generato questo avviso.</span><span class="sxs-lookup"><span data-stu-id="c0506-137">hello short name is referenced in hello notifications that are sent when this alert fires.</span></span>

9. <span data-ttu-id="c0506-138">Definire un elenco di destinatari fornendo del ricevitore hello:</span><span class="sxs-lookup"><span data-stu-id="c0506-138">Define a list of receivers by providing hello receiver's:</span></span>

    <span data-ttu-id="c0506-139">a.</span><span class="sxs-lookup"><span data-stu-id="c0506-139">a.</span></span> <span data-ttu-id="c0506-140">**Nome**: immettere il nome del destinatario hello, alias o identificatore.</span><span class="sxs-lookup"><span data-stu-id="c0506-140">**Name**: Enter hello receiver’s name, alias, or identifier.</span></span>

    <span data-ttu-id="c0506-141">b.</span><span class="sxs-lookup"><span data-stu-id="c0506-141">b.</span></span> <span data-ttu-id="c0506-142">**Tipo di azione**: selezionare webhook, posta elettronica o SMS.</span><span class="sxs-lookup"><span data-stu-id="c0506-142">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="c0506-143">c.</span><span class="sxs-lookup"><span data-stu-id="c0506-143">c.</span></span> <span data-ttu-id="c0506-144">**Dettagli**: basato sul tipo di azione hello scelto, immettere un numero di telefono, indirizzo di posta elettronica o webhook URI.</span><span class="sxs-lookup"><span data-stu-id="c0506-144">**Details**: Based on hello action type chosen, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="c0506-145">Selezionare **OK** avviso hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="c0506-145">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="c0506-146">Entro pochi minuti, avviso hello è attiva e avvia tootrigger in base alle condizioni di hello specificato durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="c0506-146">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

<span data-ttu-id="c0506-147">Per informazioni sullo schema webhook hello per gli avvisi del registro attività, vedere [Webhook per attività di Azure registra avvisi](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="c0506-147">For information on hello webhook schema for activity log alerts, see [Webhooks for Azure activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="c0506-148">gruppo di azioni Hello definito in questa procedura è riutilizzabile come un gruppo di azioni esistenti per tutte le definizioni di avviso futuri.</span><span class="sxs-lookup"><span data-stu-id="c0506-148">hello action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="c0506-149">Creare un avviso per una notifica di integrità del servizio per un gruppo di azioni esistenti utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c0506-149">Create an alert on a service health notification for an existing action group by using hello Azure portal</span></span>

1. <span data-ttu-id="c0506-150">Seguire i passaggi da 1 a 7 hello precedente sezione toocreate la notifica del servizio di integrità.</span><span class="sxs-lookup"><span data-stu-id="c0506-150">Follow steps 1 through 7 in hello previous section toocreate your service health notification.</span></span> 

2. <span data-ttu-id="c0506-151">In **avviso tramite**selezionare hello **esistente** pulsante di azione di gruppo.</span><span class="sxs-lookup"><span data-stu-id="c0506-151">Under **Alert via**, select hello **Existing** action group button.</span></span> <span data-ttu-id="c0506-152">Selezionare il gruppo di azioni appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="c0506-152">Select hello appropriate action group.</span></span>

3. <span data-ttu-id="c0506-153">Selezionare **OK** avviso hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="c0506-153">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="c0506-154">Entro pochi minuti, avviso hello è attiva e avvia tootrigger in base alle condizioni di hello specificato durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="c0506-154">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="c0506-155">Gestire gli avvisi</span><span class="sxs-lookup"><span data-stu-id="c0506-155">Manage your alerts</span></span>

<span data-ttu-id="c0506-156">Dopo aver creato un avviso, è visibile in hello **avvisi** sezione di hello **monitoraggio** blade.</span><span class="sxs-lookup"><span data-stu-id="c0506-156">After you create an alert, it's visible in hello **Alerts** section of hello **Monitor** blade.</span></span> <span data-ttu-id="c0506-157">Selezionare l'avviso di hello da toomanage per:</span><span class="sxs-lookup"><span data-stu-id="c0506-157">Select hello alert you want toomanage to:</span></span>

* <span data-ttu-id="c0506-158">Modificarlo.</span><span class="sxs-lookup"><span data-stu-id="c0506-158">Edit it.</span></span>
* <span data-ttu-id="c0506-159">Eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="c0506-159">Delete it.</span></span>
* <span data-ttu-id="c0506-160">Disabilitare o abilitare, se si desidera tootemporarily arrestare o riprendere la ricezione di notifiche di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="c0506-160">Disable or enable it, if you want tootemporarily stop or resume receiving notifications for hello alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0506-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c0506-161">Next steps</span></span>
- <span data-ttu-id="c0506-162">Informazioni sulle [notifiche per l'integrità del servizio](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="c0506-162">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="c0506-163">Informazioni sulla [limitazione della frequenza delle notifiche](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="c0506-163">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="c0506-164">Hello revisione [schema webhook avvisi del registro attività](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="c0506-164">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="c0506-165">Ottenere un [panoramica degli avvisi di log attività](monitoring-overview-alerts.md)e informazioni su come tooreceive avvisi.</span><span class="sxs-lookup"><span data-stu-id="c0506-165">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span> 
- <span data-ttu-id="c0506-166">Altre informazioni sui [gruppi di azione](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="c0506-166">Learn more about [action groups](monitoring-action-groups.md).</span></span>

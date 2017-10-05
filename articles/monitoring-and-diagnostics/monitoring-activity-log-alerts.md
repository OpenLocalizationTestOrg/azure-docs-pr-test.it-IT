---
title: "Creare avvisi del log attività | Microsoft Docs"
description: "Ricevere una notifica tramite SMS, webhook e posta elettronica quando si verificano determinati eventi nel log attività."
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
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: 3885469ec0e1fcc31386dd0ad7fe6cb5d03ab28e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-activity-log-alerts"></a><span data-ttu-id="0d86f-103">Creare avvisi del log attività</span><span class="sxs-lookup"><span data-stu-id="0d86f-103">Create activity log alerts</span></span>

## <a name="overview"></a><span data-ttu-id="0d86f-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0d86f-104">Overview</span></span>
<span data-ttu-id="0d86f-105">Gli avvisi del log attività vengono attivati quando si verifica un nuovo evento del log attività che corrisponde alle condizioni specificate nell'avviso.</span><span class="sxs-lookup"><span data-stu-id="0d86f-105">Activity log alerts are alerts that activate when a new activity log event occurs that matches the conditions specified in the alert.</span></span> <span data-ttu-id="0d86f-106">Si tratta di risorse di Azure e possono essere create usando un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0d86f-106">They are Azure resources, so they can be created by using an Azure Resource Manager template.</span></span> <span data-ttu-id="0d86f-107">Possono essere create, aggiornate o eliminate anche nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d86f-107">They also can be created, updated, or deleted in the Azure portal.</span></span> <span data-ttu-id="0d86f-108">In questo articolo vengono presentati i concetti alla base degli avvisi del log attività.</span><span class="sxs-lookup"><span data-stu-id="0d86f-108">This article introduces the concepts behind activity log alerts.</span></span> <span data-ttu-id="0d86f-109">Questo articolo illustra come usare il portale di Azure per configurare un avviso sugli eventi del log attività.</span><span class="sxs-lookup"><span data-stu-id="0d86f-109">It then shows you how to use the Azure portal to set up an alert on activity log events.</span></span>

<span data-ttu-id="0d86f-110">In genere, si creano avvisi del log attività per ricevere notifiche quando:</span><span class="sxs-lookup"><span data-stu-id="0d86f-110">Typically, you create activity log alerts to receive notifications when:</span></span>

* <span data-ttu-id="0d86f-111">Si verificano modifiche specifiche nelle risorse nella sottoscrizione di Azure. Questi avvisi sono spesso limitati a risorse o gruppi di risorse specifici.</span><span class="sxs-lookup"><span data-stu-id="0d86f-111">Specific changes occur on resources in your Azure subscription, often scoped to particular resource groups or resources.</span></span> <span data-ttu-id="0d86f-112">Potrebbe ad esempio essere utile ricevere una notifica quando viene eliminata una macchina virtuale in myProductionResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0d86f-112">For example, you might want to be notified when any virtual machine in myProductionResourceGroup is deleted.</span></span> <span data-ttu-id="0d86f-113">o se vengono assegnati nuovi ruoli a un utente nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0d86f-113">Or, you might want to be notified if any new roles are assigned to a user in your subscription.</span></span>
* <span data-ttu-id="0d86f-114">Si verifica un evento di integrità del servizio.</span><span class="sxs-lookup"><span data-stu-id="0d86f-114">A service health event occurs.</span></span> <span data-ttu-id="0d86f-115">Gli eventi di integrità del servizio includono la notifica di eventi imprevisti e di manutenzione che si applicano alle risorse nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0d86f-115">Service health events include notification of incidents and maintenance events that apply to resources in your subscription.</span></span>

<span data-ttu-id="0d86f-116">In ogni caso, un avviso del log attività monitora solo degli eventi nella sottoscrizione in cui è stato creato l'evento.</span><span class="sxs-lookup"><span data-stu-id="0d86f-116">In either case, an activity log alert monitors only for events in the subscription in which the alert is created.</span></span>

<span data-ttu-id="0d86f-117">È possibile configurare un avviso del log attività in base a qualsiasi proprietà di primo livello nell'oggetto JSON per un evento del log attività.</span><span class="sxs-lookup"><span data-stu-id="0d86f-117">You can configure an activity log alert based on any top-level property in the JSON object for an activity log event.</span></span> <span data-ttu-id="0d86f-118">Tuttavia il portale mostra le opzioni più comuni:</span><span class="sxs-lookup"><span data-stu-id="0d86f-118">However, the portal shows the most common options:</span></span>

- <span data-ttu-id="0d86f-119">**Categoria**: amministrazione, integrità del servizio, scalabilità automatica e indicazione.</span><span class="sxs-lookup"><span data-stu-id="0d86f-119">**Category**: Administrative, Service Health, Autoscale, and Recommendation.</span></span> <span data-ttu-id="0d86f-120">Per altre informazioni, vedere [Panoramica del log attività di Azure](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span><span class="sxs-lookup"><span data-stu-id="0d86f-120">For more information, see [Overview of the Azure activity log](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span></span> <span data-ttu-id="0d86f-121">Per altre informazioni sugli eventi di integrità del servizio, vedere [Ricevere gli avvisi del log attività sulle notifiche del servizio](./monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="0d86f-121">To learn more about service health events, see [Receive activity log alerts on service notifications](./monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
- <span data-ttu-id="0d86f-122">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="0d86f-122">**Resource group**</span></span>
- <span data-ttu-id="0d86f-123">**Risorsa**</span><span class="sxs-lookup"><span data-stu-id="0d86f-123">**Resource**</span></span>
- <span data-ttu-id="0d86f-124">**Tipo di risorsa**</span><span class="sxs-lookup"><span data-stu-id="0d86f-124">**Resource type**</span></span>
- <span data-ttu-id="0d86f-125">**Nome operazione**: il nome dell'operazione del controllo degli accessi in base al ruolo di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0d86f-125">**Operation name**: The Resource Manager Role-Based Access Control operation name.</span></span>
- <span data-ttu-id="0d86f-126">**Livello**: il livello di gravità dell'evento (dettagliato, informativo, avvertenza, errore o critico).</span><span class="sxs-lookup"><span data-stu-id="0d86f-126">**Level**: The severity level of the event (Verbose, Informational, Warning, Error, or Critical).</span></span>
- <span data-ttu-id="0d86f-127">**Stato**: lo stato dell'evento, in genere Avviato, Non riuscito o Riuscito.</span><span class="sxs-lookup"><span data-stu-id="0d86f-127">**Status**: The status of the event, typically Started, Failed, or Succeeded.</span></span>
- <span data-ttu-id="0d86f-128">**Evento avviato da**: noto anche come "chiamante".</span><span class="sxs-lookup"><span data-stu-id="0d86f-128">**Event initiated by**: Also known as the "caller."</span></span> <span data-ttu-id="0d86f-129">L'indirizzo di posta elettronica o un identificatore di Azure Active Directory dell'utente che ha eseguito l'operazione.</span><span class="sxs-lookup"><span data-stu-id="0d86f-129">The email address or Azure Active Directory identifier of the user who performed the operation.</span></span>

>[!NOTE]
><span data-ttu-id="0d86f-130">È necessario specificare nell'avviso almeno due dei criteri precedenti e uno di questi deve rappresentare la categoria.</span><span class="sxs-lookup"><span data-stu-id="0d86f-130">You must specify at least two of the preceding criteria in your alert, with one being the category.</span></span> <span data-ttu-id="0d86f-131">Non è possibile creare un avviso che viene attivato ogni volta che si crea un evento nei log attività.</span><span class="sxs-lookup"><span data-stu-id="0d86f-131">You may not create an alert that activates every time an event is created in the activity logs.</span></span>
>
>

<span data-ttu-id="0d86f-132">Quando un avviso del log di attività viene attivato, usa un gruppo di azione per generare azioni o notifiche.</span><span class="sxs-lookup"><span data-stu-id="0d86f-132">When an activity log alert is activated, it uses an action group to generate actions or notifications.</span></span> <span data-ttu-id="0d86f-133">Un gruppo di azione è un set riutilizzabile di ricevitori di notifica, ad esempio gli indirizzi di posta elettronica, gli URL webhook o i numeri di telefono di SMS.</span><span class="sxs-lookup"><span data-stu-id="0d86f-133">An action group is a reusable set of notification receivers, such as email addresses, webhook URLs, or SMS phone numbers.</span></span> <span data-ttu-id="0d86f-134">Più avvisi possono fare riferimento ai ricevitori per centralizzare e raggruppare i canali di notifica.</span><span class="sxs-lookup"><span data-stu-id="0d86f-134">The receivers can be referenced from multiple alerts to centralize and group your notification channels.</span></span> <span data-ttu-id="0d86f-135">Quando si definisce l'avviso del log di attività, sono disponibili due opzioni.</span><span class="sxs-lookup"><span data-stu-id="0d86f-135">When you define your activity log alert, you have two options.</span></span> <span data-ttu-id="0d86f-136">È possibile:</span><span class="sxs-lookup"><span data-stu-id="0d86f-136">You can:</span></span>

* <span data-ttu-id="0d86f-137">Usare un gruppo di azione esistente nell'avviso del log attività.</span><span class="sxs-lookup"><span data-stu-id="0d86f-137">Use an existing action group in your activity log alert.</span></span> 
* <span data-ttu-id="0d86f-138">Creare un nuovo gruppo di azione.</span><span class="sxs-lookup"><span data-stu-id="0d86f-138">Create a new action group.</span></span> 

<span data-ttu-id="0d86f-139">Per altre informazioni sui gruppi di azione, vedere [Creare e gestire gruppi di azione nel portale di Azure](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="0d86f-139">To learn more about action groups, see [Create and manage action groups in the Azure portal](monitoring-action-groups.md).</span></span>

<span data-ttu-id="0d86f-140">Per altre informazioni sulle notifiche sull'integrità del servizio, vedere [Ricevere gli avvisi del log attività per le notifiche sull'integrità del servizio](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="0d86f-140">To learn more about service health notifications, see [Receive activity log alerts on service health notifications](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-the-azure-portal"></a><span data-ttu-id="0d86f-141">Creare un avviso per un evento del log attività con un nuovo gruppo di azione usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0d86f-141">Create an alert on an activity log event with a new action group by using the Azure portal</span></span>
1. <span data-ttu-id="0d86f-142">Nel [portale](https://portal.azure.com)selezionare **Monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="0d86f-142">In the [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Servizio "Monitoraggio"](./media/monitoring-activity-log-alerts/home-monitor.png)
2. <span data-ttu-id="0d86f-144">Nella sezione **Log attività** selezionare **Avvisi**.</span><span class="sxs-lookup"><span data-stu-id="0d86f-144">In the **Activity log** section, select **Alerts**.</span></span>

    ![Scheda "Avvisi"](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. <span data-ttu-id="0d86f-146">Selezionare il comando **Aggiungi avviso del log attività** e compilare i campi.</span><span class="sxs-lookup"><span data-stu-id="0d86f-146">Select **Add activity log alert**, and fill in the fields.</span></span>

4. <span data-ttu-id="0d86f-147">Immettere un nome per la casella **Nome avviso del log attività** e selezionare una **descrizione**.</span><span class="sxs-lookup"><span data-stu-id="0d86f-147">Enter a name in the **Activity log alert name** box, and select a **Description**.</span></span>

    ![Comando "Aggiungi avviso del log attività"](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. <span data-ttu-id="0d86f-149">Nella casella **Sottoscrizione** viene inserita automaticamente la sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="0d86f-149">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="0d86f-150">Il gruppo di azione verrà salvato in questa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0d86f-150">This subscription is the one in which the action group is saved.</span></span> <span data-ttu-id="0d86f-151">Questa è la sottoscrizione in cui verrà distribuita la risorsa di avviso e in cui verranno monitorati gli eventi del log attività.</span><span class="sxs-lookup"><span data-stu-id="0d86f-151">The alert resource is deployed to this subscription and monitors activity log events from it.</span></span>

    ![Finestra di dialogo "Aggiungi avviso del log attività"](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. <span data-ttu-id="0d86f-153">Selezionare il **gruppo di risorse** in cui verrà creata la risorsa di avviso.</span><span class="sxs-lookup"><span data-stu-id="0d86f-153">Select the **Resource group** in which the alert resource is created.</span></span> <span data-ttu-id="0d86f-154">Non è il gruppo di risorse che viene monitorato dall'avviso,</span><span class="sxs-lookup"><span data-stu-id="0d86f-154">This is not the resource group that's monitored by the alert.</span></span> <span data-ttu-id="0d86f-155">ma è quello in cui si trova la risorsa di avviso.</span><span class="sxs-lookup"><span data-stu-id="0d86f-155">Instead, it's the resource group where the alert resource is located.</span></span>

7. <span data-ttu-id="0d86f-156">Selezionare facoltativamente una **categoria di eventi** per modificare i filtri aggiuntivi visualizzati.</span><span class="sxs-lookup"><span data-stu-id="0d86f-156">Optionally, select an **Event category** to modify the additional filters that are shown.</span></span> <span data-ttu-id="0d86f-157">Per gli eventi amministrativi, i filtri includono **Gruppo di risorse**, **Risorse**, **Tipo di risorsa**, **Nome dell'operazione**, **Livello**, **Stato** ed **Evento avviato da**.</span><span class="sxs-lookup"><span data-stu-id="0d86f-157">For Administrative events, the filters include **Resource group**, **Resource**, **Resource type**, **Operation name**, **Level**, **Status**, and **Event initiated by**.</span></span> <span data-ttu-id="0d86f-158">Questi valori identificano gli eventi che devono essere monitorati da questo avviso.</span><span class="sxs-lookup"><span data-stu-id="0d86f-158">These values identify which events this alert should monitor.</span></span>

    >[!NOTE]
    ><span data-ttu-id="0d86f-159">È necessario specificare nell'avviso almeno uno dei criteri precedenti.</span><span class="sxs-lookup"><span data-stu-id="0d86f-159">You must specify at least one of the preceding criteria in your alert.</span></span> <span data-ttu-id="0d86f-160">Non è possibile creare un avviso che viene attivato ogni volta che si crea un evento nei log attività.</span><span class="sxs-lookup"><span data-stu-id="0d86f-160">You may not create an alert that activates every time an event is created in the activity logs.</span></span>
    >
    >

8. <span data-ttu-id="0d86f-161">Immettere un nome nella casella **Nome gruppo di azione** e un nome nella casella **Nome breve gruppo di azione**.</span><span class="sxs-lookup"><span data-stu-id="0d86f-161">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="0d86f-162">Il nome breve viene usato al posto del nome completo di un gruppo di azione quando le notifiche vengono inviate usando questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="0d86f-162">The short name is used in place of a full action group name when notifications are sent using this group.</span></span>

9.  <span data-ttu-id="0d86f-163">Definire un elenco di azioni, fornendo i dati dell'azione seguenti:</span><span class="sxs-lookup"><span data-stu-id="0d86f-163">Define a list of actions by providing the action’s:</span></span>

    <span data-ttu-id="0d86f-164">a.</span><span class="sxs-lookup"><span data-stu-id="0d86f-164">a.</span></span> <span data-ttu-id="0d86f-165">**Nome:**: immettere il nome, l'alias o l'identificatore dell'azione.</span><span class="sxs-lookup"><span data-stu-id="0d86f-165">**Name**: Enter the action’s name, alias, or identifier.</span></span>

    <span data-ttu-id="0d86f-166">b.</span><span class="sxs-lookup"><span data-stu-id="0d86f-166">b.</span></span> <span data-ttu-id="0d86f-167">**Tipo di azione**: selezionare webhook, posta elettronica o SMS.</span><span class="sxs-lookup"><span data-stu-id="0d86f-167">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="0d86f-168">c.</span><span class="sxs-lookup"><span data-stu-id="0d86f-168">c.</span></span> <span data-ttu-id="0d86f-169">**Dettagli**: in base al tipo di azione immettere un numero di telefono, un indirizzo di posta elettronica o l'URI del webhook.</span><span class="sxs-lookup"><span data-stu-id="0d86f-169">**Details**: Based on the action type, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="0d86f-170">Fare clic su **OK** per creare l'avviso.</span><span class="sxs-lookup"><span data-stu-id="0d86f-170">Select **OK** to create the alert.</span></span>

<span data-ttu-id="0d86f-171">La propagazione completa dell'avviso richiede alcuni minuti, quindi l'avviso diventa attivo.</span><span class="sxs-lookup"><span data-stu-id="0d86f-171">The alert takes a few minutes to fully propagate and then become active.</span></span> <span data-ttu-id="0d86f-172">Si attiva quando nuovi eventi corrispondono ai criteri dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="0d86f-172">It triggers when new events match the alert's criteria.</span></span>

<span data-ttu-id="0d86f-173">Per altre informazioni, vedere [Informazioni sullo schema webhook degli avvisi del log attività](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="0d86f-173">For more information, see [Understand the webhook schema used in activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="0d86f-174">Il gruppo di azione definito in questi passaggi è riutilizzabile come gruppo di azione esistente per tutte le future definizioni di avviso.</span><span class="sxs-lookup"><span data-stu-id="0d86f-174">The action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-the-azure-portal"></a><span data-ttu-id="0d86f-175">Creare un avviso per un evento del log attività con un gruppo di azione esistente usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0d86f-175">Create an alert on an activity log event for an existing action group by using the Azure portal</span></span>
1. <span data-ttu-id="0d86f-176">Seguire i passaggi da 1 a 7 nella sezione precedente per creare l'avviso del log attività.</span><span class="sxs-lookup"><span data-stu-id="0d86f-176">Follow steps 1 through 7 in the previous section to create your activity log alert.</span></span>

2. <span data-ttu-id="0d86f-177">In **Notifica tramite** selezionare il pulsante Gruppo di azione **esistente**.</span><span class="sxs-lookup"><span data-stu-id="0d86f-177">Under **Notify via**, select the **Existing** action group button.</span></span> <span data-ttu-id="0d86f-178">Selezionare un gruppo di azione esistente dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="0d86f-178">Select an existing action group from the list.</span></span>

3. <span data-ttu-id="0d86f-179">Fare clic su **OK** per creare l'avviso.</span><span class="sxs-lookup"><span data-stu-id="0d86f-179">Select **OK** to create the alert.</span></span>

<span data-ttu-id="0d86f-180">La propagazione completa dell'avviso richiede alcuni minuti, quindi l'avviso diventa attivo.</span><span class="sxs-lookup"><span data-stu-id="0d86f-180">The alert takes a few minutes to fully propagate and then become active.</span></span> <span data-ttu-id="0d86f-181">Si attiva quando nuovi eventi corrispondono ai criteri dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="0d86f-181">It triggers when new events match the alert's criteria.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="0d86f-182">Gestire gli avvisi</span><span class="sxs-lookup"><span data-stu-id="0d86f-182">Manage your alerts</span></span>

<span data-ttu-id="0d86f-183">Dopo la creazione, l'avviso sarà visibile nella sezione Avvisi del pannello Monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="0d86f-183">After you create an alert, it's visible in the Alerts section of the Monitor blade.</span></span> <span data-ttu-id="0d86f-184">Selezionare l'avviso da gestire per:</span><span class="sxs-lookup"><span data-stu-id="0d86f-184">Select the alert you want to manage to:</span></span>

* <span data-ttu-id="0d86f-185">Modificarlo.</span><span class="sxs-lookup"><span data-stu-id="0d86f-185">Edit it.</span></span>
* <span data-ttu-id="0d86f-186">Eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="0d86f-186">Delete it.</span></span>
* <span data-ttu-id="0d86f-187">Disabilitarlo o abilitarlo per interrompere temporaneamente o riprendere la ricezione delle notifiche relative all'avviso.</span><span class="sxs-lookup"><span data-stu-id="0d86f-187">Disable or enable it, if you want to temporarily stop or resume receiving notifications for the alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d86f-188">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0d86f-188">Next steps</span></span>
- <span data-ttu-id="0d86f-189">Ottenere una [panoramica degli avvisi](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="0d86f-189">Get an [overview of alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="0d86f-190">Informazioni sulla [limitazione della frequenza delle notifiche](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="0d86f-190">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="0d86f-191">Esaminare lo [schema webhook degli avvisi del log attività](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="0d86f-191">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="0d86f-192">Altre informazioni sui [gruppi di azione](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="0d86f-192">Learn more about [action groups](monitoring-action-groups.md).</span></span>  
- <span data-ttu-id="0d86f-193">Informazioni sulle [notifiche per l'integrità del servizio](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="0d86f-193">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="0d86f-194">Creare un [avviso del log attività per monitorare tutte le operazioni del motore di scalabilità automatica della sottoscrizione](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="0d86f-194">Create an [activity log alert to monitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="0d86f-195">Creare un [avviso del log attività per monitorare tutte le operazioni di scalabilità automatica in riduzione e in aumento non riuscite per la sottoscrizione](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="0d86f-195">Create an [activity log alert to monitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>

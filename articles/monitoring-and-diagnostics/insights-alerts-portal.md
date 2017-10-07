---
title: gli avvisi aaaCreate per servizi di Azure - portale di Azure | Documenti Microsoft
description: Attivare l'automazione, notifiche, gli URL di siti Web di chiamata (webhook) o messaggi di posta elettronica quando vengono soddisfatte le condizioni di hello specificate.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: 78d862d25255cda9fdfe347329e908a471c39846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a><span data-ttu-id="66990-103">Creare avvisi sulle metriche in Monitoraggio di Azure per i servizi di Azure: portale di Azure</span><span class="sxs-lookup"><span data-stu-id="66990-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="66990-104">Portale</span><span class="sxs-lookup"><span data-stu-id="66990-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="66990-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="66990-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="66990-106">CLI</span><span class="sxs-lookup"><span data-stu-id="66990-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="66990-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="66990-107">Overview</span></span>
<span data-ttu-id="66990-108">Questo articolo illustra come tooset di Azure avvisi metrica utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="66990-108">This article shows you how tooset up Azure metric alerts using hello Azure portal.</span></span>   

<span data-ttu-id="66990-109">È possibile ricevere avvisi basati su metriche di monitoraggio o eventi nei servizi Azure.</span><span class="sxs-lookup"><span data-stu-id="66990-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="66990-110">**Valori della metrica** : hello trigger un avviso quando il valore di hello di una specifica metrica supera una soglia è assegnare in entrambe le direzioni.</span><span class="sxs-lookup"><span data-stu-id="66990-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="66990-111">Ovvero, entrambi attiva quando hello prima condizione e quindi successivamente non condizione when che è non è più in grado di soddisfare.</span><span class="sxs-lookup"><span data-stu-id="66990-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="66990-112">**Eventi del log attività**: è possibile attivare un avviso per *ogni* evento o solo quando si verifica un determinato evento.</span><span class="sxs-lookup"><span data-stu-id="66990-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="66990-113">ulteriori informazioni sugli avvisi di log attività toolearn [fare clic qui](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="66990-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="66990-114">È possibile configurare una metrica toodo avviso hello seguenti attiva:</span><span class="sxs-lookup"><span data-stu-id="66990-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="66990-115">inviare coamministratore e amministratore del servizio toohello le notifiche tramite posta elettronica</span><span class="sxs-lookup"><span data-stu-id="66990-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="66990-116">Invia messaggio di posta elettronica tooadditional messaggi di posta elettronica specificato.</span><span class="sxs-lookup"><span data-stu-id="66990-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="66990-117">chiamare un webhook</span><span class="sxs-lookup"><span data-stu-id="66990-117">call a webhook</span></span>
* <span data-ttu-id="66990-118">avviare l'esecuzione di un runbook di Azure (solo da hello portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="66990-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="66990-119">È possibile configurare e ottenere informazioni sulle regole degli avvisi sulle metriche tramite</span><span class="sxs-lookup"><span data-stu-id="66990-119">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="66990-120">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="66990-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="66990-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="66990-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="66990-122">interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="66990-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="66990-123">API REST di Monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="66990-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a><span data-ttu-id="66990-124">Creare una regola di avviso su una metrica con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="66990-124">Create an alert rule on a metric with hello Azure portal</span></span>
1. <span data-ttu-id="66990-125">In hello [portale](https://portal.azure.com/)individuare risorse hello si è interessati a monitoraggio e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="66990-125">In hello [portal](https://portal.azure.com/), locate hello resource you are interested in monitoring and select it.</span></span>

2. <span data-ttu-id="66990-126">Selezionare **avvisi** o **regole di avviso** nella sezione monitoraggio hello.</span><span class="sxs-lookup"><span data-stu-id="66990-126">Select **Alerts** or **Alert rules** under hello MONITORING section.</span></span> <span data-ttu-id="66990-127">icona e il testo hello possono variare leggermente a diverse risorse.</span><span class="sxs-lookup"><span data-stu-id="66990-127">hello text and icon may vary slightly for different resources.</span></span>  

    ![Monitoraggio](./media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="66990-129">Seleziona hello **Aggiungi avviso** comando e compilare i campi di hello.</span><span class="sxs-lookup"><span data-stu-id="66990-129">Select hello **Add alert** command and fill in hello fields.</span></span>

    ![Aggiungi avviso](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="66990-131">Assegnare alla regola di avviso un **Nome** e scegliere una **Descrizione**, che viene visualizzata anche nella notifica inviata tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="66990-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span></span>

5. <span data-ttu-id="66990-132">Seleziona hello **metrica** toomonitor desiderato, quindi scegliere un **condizione** e **soglia** valore per la misurazione hello.</span><span class="sxs-lookup"><span data-stu-id="66990-132">Select hello **Metric** you want toomonitor, then choose a **Condition** and **Threshold** value for hello metric.</span></span> <span data-ttu-id="66990-133">Anche scelta hello **periodo** di tempo che hello metrica regola deve essere soddisfatti prima di allarmi hello.</span><span class="sxs-lookup"><span data-stu-id="66990-133">Also chose hello **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span> <span data-ttu-id="66990-134">Ad esempio, se si utilizza il periodo di hello "PT5M" e l'avviso Cerca della CPU superiore all'80%, avviso hello attiva quando hello della CPU è stata costantemente sopra l'80% per 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="66990-134">So for example, if you use hello period "PT5M" and your alert looks for CPU above 80%, hello alert triggers when hello CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="66990-135">Quando si verifica primo trigger hello, nuovamente attiva quando hello della CPU rimane sotto l'80% per 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="66990-135">Once hello first trigger occurs, it again triggers when hello CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="66990-136">Hello misura della CPU si verifica a intervalli di 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="66990-136">hello CPU measurement occurs every 1 minute.</span></span>   

6. <span data-ttu-id="66990-137">Controllare **proprietari di posta elettronica...**  se si desidera che gli amministratori e i coamministratori toobe inviato tramite posta elettronica quando hello avviso generato.</span><span class="sxs-lookup"><span data-stu-id="66990-137">Check **Email owners...** if you want administrators and co-administrators toobe emailed when hello alert fires.</span></span>

7. <span data-ttu-id="66990-138">Se si desidera che altri messaggi di posta elettronica tooreceive una notifica quando hello viene generato un avviso, aggiungerle in hello **email(s) amministratore aggiuntive** campo.</span><span class="sxs-lookup"><span data-stu-id="66990-138">If you want additional emails tooreceive a notification when hello alert fires, add them in hello **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="66990-139">Separare gli indirizzi di posta elettronica con punti e virgola: *email@contoso.com;email2@contoso.com*</span><span class="sxs-lookup"><span data-stu-id="66990-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

8. <span data-ttu-id="66990-140">Inserire in un URI valido in hello **Webhook** campo se si desidera che chiamato hello quando avviso generato.</span><span class="sxs-lookup"><span data-stu-id="66990-140">Put in a valid URI in hello **Webhook** field if you want it called when hello alert fires.</span></span>

9. <span data-ttu-id="66990-141">Se si utilizza l'automazione di Azure, è possibile selezionare un toobe Runbook eseguito quando viene generato l'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="66990-141">If you use Azure Automation, you can select a Runbook toobe run when hello alert fires.</span></span>

10. <span data-ttu-id="66990-142">Selezionare **OK** quando toocreate done hello avviso.</span><span class="sxs-lookup"><span data-stu-id="66990-142">Select **OK** when done toocreate hello alert.</span></span>   

<span data-ttu-id="66990-143">Entro pochi minuti, l'avviso hello è attivo e attiva come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="66990-143">Within a few minutes, hello alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="66990-144">Gestione degli avvisi</span><span class="sxs-lookup"><span data-stu-id="66990-144">Managing your alerts</span></span>
<span data-ttu-id="66990-145">Dopo aver creato un avviso, è possibile selezionarlo e:</span><span class="sxs-lookup"><span data-stu-id="66990-145">Once you have created an alert, you can select it and:</span></span>

* <span data-ttu-id="66990-146">Consente di visualizzare un grafico che mostra soglia hello per le metriche e i valori effettivi da hello hello giorno precedente.</span><span class="sxs-lookup"><span data-stu-id="66990-146">View a graph showing hello metric threshold and hello actual values from hello previous day.</span></span>
* <span data-ttu-id="66990-147">Modificarlo o eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="66990-147">Edit or delete it.</span></span>
* <span data-ttu-id="66990-148">**Disabilitare** o **abilitare** se si desidera tootemporarily arrestare o riprendere la ricezione di notifiche relative a questo avviso.</span><span class="sxs-lookup"><span data-stu-id="66990-148">**Disable** or **Enable** it if you want tootemporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66990-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="66990-149">Next steps</span></span>
* <span data-ttu-id="66990-150">[Panoramica di Azure monitoring](monitoring-overview.md) inclusi i tipi di informazioni è possibile raccogliere e monitorare hello.</span><span class="sxs-lookup"><span data-stu-id="66990-150">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="66990-151">Altre informazioni sulla [configurazione dei webhook negli avvisi](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="66990-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="66990-152">Altre informazioni sulla [configurazione di avvisi sugli eventi del log attività](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="66990-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="66990-153">Altre informazioni sui [runbook di automazione di Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="66990-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="66990-154">Leggere una [panoramica dei log di diagnostica](monitoring-overview-of-diagnostic-logs.md) e sulla raccolta di metriche dettagliate e ad alta frequenza sul servizio.</span><span class="sxs-lookup"><span data-stu-id="66990-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="66990-155">Ottenere un [Panoramica della raccolta di metriche](insights-how-to-customize-monitoring.md) toomake che il servizio sia disponibile e reattiva.</span><span class="sxs-lookup"><span data-stu-id="66990-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>

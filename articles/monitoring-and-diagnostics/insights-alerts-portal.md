---
title: Creare avvisi per i servizi di Azure - Portale di Azure | Documentazione Microsoft
description: Attivare messaggi di posta elettronica o notifiche, chiamare URL di siti Web (webhook) o usare l'automazione quando vengono soddisfatte le condizioni specificate.
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
ms.openlocfilehash: 745a9c016bd037f1051025a2c5a468c3935e4550
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a><span data-ttu-id="e29a2-103">Creare avvisi sulle metriche in Monitoraggio di Azure per i servizi di Azure: portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e29a2-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e29a2-104">Portale</span><span class="sxs-lookup"><span data-stu-id="e29a2-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="e29a2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e29a2-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="e29a2-106">CLI</span><span class="sxs-lookup"><span data-stu-id="e29a2-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="e29a2-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e29a2-107">Overview</span></span>
<span data-ttu-id="e29a2-108">Questo articolo descrive come impostare gli avvisi sulle metriche di Azure tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e29a2-108">This article shows you how to set up Azure metric alerts using the Azure portal.</span></span>   

<span data-ttu-id="e29a2-109">È possibile ricevere avvisi basati su metriche di monitoraggio o eventi nei servizi Azure.</span><span class="sxs-lookup"><span data-stu-id="e29a2-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="e29a2-110">**Valori metrici** : l'avviso si attiva quando il valore di una specifica metrica supera una soglia assegnata per eccesso o difetto.</span><span class="sxs-lookup"><span data-stu-id="e29a2-110">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="e29a2-111">Vale a dire che si attiva sia quando la condizione viene inizialmente soddisfatta e successivamente quando tale condizione non è più soddisfatta.</span><span class="sxs-lookup"><span data-stu-id="e29a2-111">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="e29a2-112">**Eventi del log attività**: è possibile attivare un avviso per *ogni* evento o solo quando si verifica un determinato evento.</span><span class="sxs-lookup"><span data-stu-id="e29a2-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="e29a2-113">Per altre informazioni sugli avvisi sui log attività [fare clic qui](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="e29a2-113">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="e29a2-114">È possibile configurare un avviso sulle metriche affinché esegua queste operazioni al momento dell'attivazione:</span><span class="sxs-lookup"><span data-stu-id="e29a2-114">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="e29a2-115">inviare un messaggio di posta elettronica all'amministratore e ai coamministratori del servizio</span><span class="sxs-lookup"><span data-stu-id="e29a2-115">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="e29a2-116">inviare un messaggio di posta elettronica ad altri indirizzi specificati</span><span class="sxs-lookup"><span data-stu-id="e29a2-116">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="e29a2-117">chiamare un webhook</span><span class="sxs-lookup"><span data-stu-id="e29a2-117">call a webhook</span></span>
* <span data-ttu-id="e29a2-118">avviare l'esecuzione di un runbook di Azure (solo dal portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="e29a2-118">start execution of an Azure runbook (only from the Azure portal)</span></span>

<span data-ttu-id="e29a2-119">È possibile configurare e ottenere informazioni sulle regole degli avvisi sulle metriche tramite</span><span class="sxs-lookup"><span data-stu-id="e29a2-119">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="e29a2-120">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e29a2-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="e29a2-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e29a2-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="e29a2-122">interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="e29a2-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="e29a2-123">API REST di Monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="e29a2-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-the-azure-portal"></a><span data-ttu-id="e29a2-124">Creare una regola di avviso in base a una metrica con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e29a2-124">Create an alert rule on a metric with the Azure portal</span></span>
1. <span data-ttu-id="e29a2-125">Nel [portale](https://portal.azure.com/), individuare la risorsa da monitorare e selezionarla.</span><span class="sxs-lookup"><span data-stu-id="e29a2-125">In the [portal](https://portal.azure.com/), locate the resource you are interested in monitoring and select it.</span></span>

2. <span data-ttu-id="e29a2-126">Selezionare **Avvisi** o **Regole di avviso** nella sezione MONITORAGGIO.</span><span class="sxs-lookup"><span data-stu-id="e29a2-126">Select **Alerts** or **Alert rules** under the MONITORING section.</span></span> <span data-ttu-id="e29a2-127">Il testo e l'icona possono lievemente variare per le diverse risorse.</span><span class="sxs-lookup"><span data-stu-id="e29a2-127">The text and icon may vary slightly for different resources.</span></span>  

    ![Monitoraggio](./media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="e29a2-129">Selezionare il comando **Aggiungi avviso** e compilare i campi.</span><span class="sxs-lookup"><span data-stu-id="e29a2-129">Select the **Add alert** command and fill in the fields.</span></span>

    ![Aggiungi avviso](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="e29a2-131">Assegnare alla regola di avviso un **Nome** e scegliere una **Descrizione**, che viene visualizzata anche nella notifica inviata tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="e29a2-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span></span>

5. <span data-ttu-id="e29a2-132">Selezionare la **Metrica** da monitorare e quindi scegliere una **Condizione** e un valore **Soglia**.</span><span class="sxs-lookup"><span data-stu-id="e29a2-132">Select the **Metric** you want to monitor, then choose a **Condition** and **Threshold** value for the metric.</span></span> <span data-ttu-id="e29a2-133">Scegliere inoltre il **Periodo** di tempo entro il quale la metrica deve essere soddisfatta prima dell'attivazione dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="e29a2-133">Also chose the **Period** of time that the metric rule must be satisfied before the alert triggers.</span></span> <span data-ttu-id="e29a2-134">Ad esempio, se si usa il periodo "PT5M" e l'avviso deve rilevare una CPU superiore all'80%, l'avviso si attiva quando la CPU resta costantemente sopra all'80% per 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="e29a2-134">So for example, if you use the period "PT5M" and your alert looks for CPU above 80%, the alert triggers when the CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="e29a2-135">Dopo la prima attivazione, l'avviso si attiverà di nuovo quando la CPU resta al di sotto dell'80% per 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="e29a2-135">Once the first trigger occurs, it again triggers when the CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="e29a2-136">La CPU viene misurata ogni minuto.</span><span class="sxs-lookup"><span data-stu-id="e29a2-136">The CPU measurement occurs every 1 minute.</span></span>   

6. <span data-ttu-id="e29a2-137">Selezionare la casella di controllo **Invia messaggio a proprietari, collaboratori e lettori** se si desidera che gli amministratori e i coamministratori ricevano un messaggio di posta elettronica quando si attiva l'avviso.</span><span class="sxs-lookup"><span data-stu-id="e29a2-137">Check **Email owners...** if you want administrators and co-administrators to be emailed when the alert fires.</span></span>

7. <span data-ttu-id="e29a2-138">Per aggiungere altri indirizzi di posta elettronica ai quali inviare una notifica quando viene attivato l'avviso, completare il campo **E-mail dell'amministratore aggiuntivo** .</span><span class="sxs-lookup"><span data-stu-id="e29a2-138">If you want additional emails to receive a notification when the alert fires, add them in the **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="e29a2-139">Separare gli indirizzi di posta elettronica con punti e virgola: *email@contoso.com;email2@contoso.com*</span><span class="sxs-lookup"><span data-stu-id="e29a2-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

8. <span data-ttu-id="e29a2-140">Inserire un URI valido nel campo **Webhook** per eseguire la chiamata quando viene attivato l'avviso.</span><span class="sxs-lookup"><span data-stu-id="e29a2-140">Put in a valid URI in the **Webhook** field if you want it called when the alert fires.</span></span>

9. <span data-ttu-id="e29a2-141">Se si usa l'automazione di Azure, è possibile selezionare il runbook da eseguire quando viene generato l'avviso.</span><span class="sxs-lookup"><span data-stu-id="e29a2-141">If you use Azure Automation, you can select a Runbook to be run when the alert fires.</span></span>

10. <span data-ttu-id="e29a2-142">Al termine fare clic su **OK** per creare l'avviso.</span><span class="sxs-lookup"><span data-stu-id="e29a2-142">Select **OK** when done to create the alert.</span></span>   

<span data-ttu-id="e29a2-143">Dopo pochi minuti l'avviso è funzionante e si attiva come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e29a2-143">Within a few minutes, the alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="e29a2-144">Gestione degli avvisi</span><span class="sxs-lookup"><span data-stu-id="e29a2-144">Managing your alerts</span></span>
<span data-ttu-id="e29a2-145">Dopo aver creato un avviso, è possibile selezionarlo e:</span><span class="sxs-lookup"><span data-stu-id="e29a2-145">Once you have created an alert, you can select it and:</span></span>

* <span data-ttu-id="e29a2-146">Visualizzare un grafico che mostra la soglia della metrica e i valori effettivi del giorno precedente.</span><span class="sxs-lookup"><span data-stu-id="e29a2-146">View a graph showing the metric threshold and the actual values from the previous day.</span></span>
* <span data-ttu-id="e29a2-147">Modificarlo o eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="e29a2-147">Edit or delete it.</span></span>
* <span data-ttu-id="e29a2-148">**Disabilitarlo** o **abilitarlo** per interrompere temporaneamente o riprendere la ricezione delle notifiche relative all'avviso.</span><span class="sxs-lookup"><span data-stu-id="e29a2-148">**Disable** or **Enable** it if you want to temporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e29a2-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e29a2-149">Next steps</span></span>
* <span data-ttu-id="e29a2-150">[Leggere una panoramica del monitoraggio di Azure](monitoring-overview.md) che include anche i tipi di informazioni che è possibile raccogliere e monitorare.</span><span class="sxs-lookup"><span data-stu-id="e29a2-150">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="e29a2-151">Altre informazioni sulla [configurazione dei webhook negli avvisi](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="e29a2-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="e29a2-152">Altre informazioni sulla [configurazione di avvisi sugli eventi del log attività](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="e29a2-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="e29a2-153">Altre informazioni sui [runbook di automazione di Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="e29a2-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="e29a2-154">Leggere una [panoramica dei log di diagnostica](monitoring-overview-of-diagnostic-logs.md) e sulla raccolta di metriche dettagliate e ad alta frequenza sul servizio.</span><span class="sxs-lookup"><span data-stu-id="e29a2-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="e29a2-155">Leggere una [panoramica della raccolta di metriche](insights-how-to-customize-monitoring.md) per verificare che il servizio sia disponibile e reattivo.</span><span class="sxs-lookup"><span data-stu-id="e29a2-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>

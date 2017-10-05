---
title: Ricerche salvate e avvisi nelle soluzioni OMS | Microsoft Docs
description: Le soluzioni in OMS includeranno in genere ricerche salvate di Log Analytics per l'analisi dei dati raccolti dalla soluzione.  Potranno anche definire avvisi per la notifica all'utente o per eseguire automaticamente un'azione in risposta a un problema critico.  Questo articolo descrive come definire le ricerche salvate e gli avvisi di Log Analytics in un modello di Azure Resource Manager in modo da consentirne l'inclusione nelle soluzioni di gestione.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 21c42a747a08c5386c65d10190baf0054a7adef8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-to-oms-management-solution-preview"></a><span data-ttu-id="1c0e8-105">Aggiunta di avvisi e di ricerche salvate di Log Analytics alla soluzione di gestione in OMS (anteprima)</span><span class="sxs-lookup"><span data-stu-id="1c0e8-105">Adding Log Analytics saved searches and alerts to OMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="1c0e8-106">Questa è una documentazione preliminare per la creazione di soluzioni di gestione in OMS attualmente disponibili in versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="1c0e8-107">Qualsiasi schema descritto di seguito è soggetto a modifiche.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-107">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="1c0e8-108">Le [soluzioni di gestione in OMS](operations-management-suite-solutions.md) includeranno in genere [ricerche salvate](../log-analytics/log-analytics-log-searches.md) di Log Analytics per l'analisi dei dati raccolti dalla soluzione.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics to analyze data collected by the solution.</span></span>  <span data-ttu-id="1c0e8-109">Potranno anche definire [avvisi](../log-analytics/log-analytics-alerts.md) per la notifica all'utente o per eseguire automaticamente un'azione in risposta a un problema critico.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) to notify the user or automatically take action in response to a critical issue.</span></span>  <span data-ttu-id="1c0e8-110">Questo articolo descrive come definire le ricerche salvate e gli avvisi di Log Analytics in un [modello di Resource Manager](../resource-manager-template-walkthrough.md) in modo da consentirne l'inclusione nelle [soluzioni di gestione](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="1c0e8-110">This article describes how to define Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1c0e8-111">Gli esempi in questo articolo usano parametri e variabili che sono richiesti o comuni nelle soluzioni di gestione e che sono descritti in [Creazione di soluzioni di gestione in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="1c0e8-111">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="1c0e8-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1c0e8-112">Prerequisites</span></span>
<span data-ttu-id="1c0e8-113">Questo articolo presuppone che si abbia già familiarità con la [creazione di una soluzione di gestione](operations-management-suite-solutions-creating.md) e la struttura di un [modello di Azure Resource Manager](../resource-group-authoring-templates.md) e un file di soluzione.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-113">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="1c0e8-114">Area di lavoro di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1c0e8-114">Log Analytics Workspace</span></span>
<span data-ttu-id="1c0e8-115">Tutte le risorse in Log Analytics sono contenute in un'[area di lavoro](../log-analytics/log-analytics-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="1c0e8-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="1c0e8-116">Come descritto in [Area di lavoro OMS e account di Automazione](operations-management-suite-solutions.md#oms-workspace-and-automation-account), l'area di lavoro non è inclusa nella soluzione di gestione, ma deve essere presente prima che la soluzione venga installata.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the workspace isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="1c0e8-117">Se non è disponibile, l'installazione della soluzione non riuscirà.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-117">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="1c0e8-118">Il nome dell'area di lavoro è il nome di ogni risorsa di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-118">The name of the workspace is in the name of each Log Analytics resource.</span></span>  <span data-ttu-id="1c0e8-119">A questo scopo, nella soluzione viene usato il parametro **workspace** come nell'esempio seguente di una risorsa savedsearch.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-119">This is done in the solution with the **workspace** parameter as in the following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="1c0e8-120">Ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="1c0e8-120">Saved Searches</span></span>
<span data-ttu-id="1c0e8-121">Includere [ricerche salvate](../log-analytics/log-analytics-log-searches.md) in una soluzione per consentire agli utenti di eseguire query sui dati raccolti dalla soluzione.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution to allow users to query data collected by your solution.</span></span>  <span data-ttu-id="1c0e8-122">Le ricerche salvate verranno visualizzate in **Preferiti** nel portale di OMS e in **Ricerche salvate** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-122">Saved searches will appear under **Favorites** in the OMS portal and **Saved Searches** in the Azure portal .</span></span>  <span data-ttu-id="1c0e8-123">È necessaria una ricerca salvata anche per ogni avviso.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="1c0e8-124">Le risorse [ricerca salvata di Log Analytics](../log-analytics/log-analytics-log-searches.md) sono di tipo `Microsoft.OperationalInsights/workspaces/savedSearches` e hanno la struttura seguente.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have the following structure.</span></span>  <span data-ttu-id="1c0e8-125">Nella struttura sono inclusi parametri e variabili comuni ed è quindi possibile copiare e incollare questo frammento di codice nel file della soluzione e, se necessario, modificare i nomi dei parametri.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-125">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



<span data-ttu-id="1c0e8-126">Le singole proprietà di una ricerca salvata sono descritte nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-126">Each of the properties of a saved search are described in the following table.</span></span> 

| <span data-ttu-id="1c0e8-127">Proprietà</span><span class="sxs-lookup"><span data-stu-id="1c0e8-127">Property</span></span> | <span data-ttu-id="1c0e8-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1c0e8-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1c0e8-129">category</span><span class="sxs-lookup"><span data-stu-id="1c0e8-129">category</span></span> | <span data-ttu-id="1c0e8-130">Categoria della ricerca salvata.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-130">The category for the saved search.</span></span>  <span data-ttu-id="1c0e8-131">Tutte le ricerche salvate nella stessa soluzione condivideranno in genere una singola categoria in modo da essere raggruppate nella console.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-131">Any saved searches in the same solution will often share a single category so they are grouped together in the console.</span></span> |
| <span data-ttu-id="1c0e8-132">displayname</span><span class="sxs-lookup"><span data-stu-id="1c0e8-132">displayname</span></span> | <span data-ttu-id="1c0e8-133">Nome da visualizzare per la ricerca salvata nel portale.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-133">Name to display for the saved search in the portal.</span></span> |
| <span data-ttu-id="1c0e8-134">query</span><span class="sxs-lookup"><span data-stu-id="1c0e8-134">query</span></span> | <span data-ttu-id="1c0e8-135">Query da eseguire.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-135">Query to run.</span></span> |

> [!NOTE]
> <span data-ttu-id="1c0e8-136">Potrebbe essere necessario usare caratteri di escape, se la query include caratteri che potrebbero essere interpretati come JSON.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-136">You may need to use escape characters in the query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="1c0e8-137">La query **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, ad esempio, dovrà essere scritta nel file di soluzione nel modo seguente: **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-137">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in the solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="1c0e8-138">Avvisi</span><span class="sxs-lookup"><span data-stu-id="1c0e8-138">Alerts</span></span>
<span data-ttu-id="1c0e8-139">Gli [avvisi di Log Analytics](../log-analytics/log-analytics-alerts.md) vengono creati da regole di avviso che eseguono una ricerca salvata a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-139">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="1c0e8-140">Se i risultati della query corrispondono ai criteri specificati, viene creato un record di avviso e vengono eseguite una o più azioni.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-140">If the results of the query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="1c0e8-141">Le regole di avviso in una soluzione di gestione sono costituite dalle tre diverse risorse riportate di seguito.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-141">Alert rules in a management solution are made up of the following three different resources.</span></span>

- <span data-ttu-id="1c0e8-142">**Ricerca salvata.**</span><span class="sxs-lookup"><span data-stu-id="1c0e8-142">**Saved search.**</span></span>  <span data-ttu-id="1c0e8-143">Definisce la ricerca nei log che verrà eseguita.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-143">Defines the log search that will be run.</span></span>  <span data-ttu-id="1c0e8-144">Una singola ricerca salvata può essere condivisa da più regole di avviso.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-144">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="1c0e8-145">**Pianificazione.**</span><span class="sxs-lookup"><span data-stu-id="1c0e8-145">**Schedule.**</span></span>  <span data-ttu-id="1c0e8-146">Definisce la frequenza con cui verrà eseguita la ricerca nei log.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-146">Defines how often the log search will be run.</span></span>  <span data-ttu-id="1c0e8-147">Ogni regola di avviso avrà una sola pianificazione.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-147">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="1c0e8-148">**Azione di avviso.**</span><span class="sxs-lookup"><span data-stu-id="1c0e8-148">**Alert action.**</span></span>  <span data-ttu-id="1c0e8-149">Ogni regola di avviso avrà una risorsa azione di tipo **Alert** che definisce dettagli dell'avviso come i criteri per la creazione di un record di avviso e la gravità.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-149">Each alert rule will have one action resource with a type of **Alert** that defines the details of the alert such as the criteria for when an alert record will be created and the alert's severity.</span></span>  <span data-ttu-id="1c0e8-150">La risorsa azione definirà facoltativamente una risposta tramite posta elettronica e runbook.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-150">The action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="1c0e8-151">**Azione webhook (facoltativa).**</span><span class="sxs-lookup"><span data-stu-id="1c0e8-151">**Webhook action (optional).**</span></span>  <span data-ttu-id="1c0e8-152">Se la regola di avviso chiamerà un webhook, è necessaria una risorsa azione aggiuntiva di tipo **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-152">If the alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="1c0e8-153">Le risorse ricerca salvata sono illustrate sopra.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-153">Saved search resources are described above.</span></span>  <span data-ttu-id="1c0e8-154">Di seguito sono descritte le altre risorse.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-154">The other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="1c0e8-155">Risorsa pianificazione</span><span class="sxs-lookup"><span data-stu-id="1c0e8-155">Schedule resource</span></span>

<span data-ttu-id="1c0e8-156">Una ricerca salvata può avere una o più pianificazioni, ognuna delle quali rappresenta una regola di avviso separata.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-156">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="1c0e8-157">La pianificazione definisce la frequenza con cui viene eseguita la ricerca e l'intervallo di tempo per cui vengono recuperati i dati.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-157">The schedule defines how often the search is run and the time interval over which the data is retrieved.</span></span>  <span data-ttu-id="1c0e8-158">Le risorse pianificazione sono di tipo `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` e hanno la struttura seguente.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-158">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have the following structure.</span></span> <span data-ttu-id="1c0e8-159">Nella struttura sono inclusi parametri e variabili comuni ed è quindi possibile copiare e incollare questo frammento di codice nel file della soluzione e, se necessario, modificare i nomi dei parametri.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-159">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



<span data-ttu-id="1c0e8-160">Le proprietà delle risorse pianificazione sono descritte nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-160">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="1c0e8-161">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="1c0e8-161">Element name</span></span> | <span data-ttu-id="1c0e8-162">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1c0e8-162">Required</span></span> | <span data-ttu-id="1c0e8-163">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1c0e8-163">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="1c0e8-164">Enabled</span><span class="sxs-lookup"><span data-stu-id="1c0e8-164">enabled</span></span>       | <span data-ttu-id="1c0e8-165">Sì</span><span class="sxs-lookup"><span data-stu-id="1c0e8-165">Yes</span></span> | <span data-ttu-id="1c0e8-166">Specifica se l'avviso viene abilitato al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-166">Specifies whether the alert is enabled when it's created.</span></span> |
| <span data-ttu-id="1c0e8-167">interval</span><span class="sxs-lookup"><span data-stu-id="1c0e8-167">interval</span></span>      | <span data-ttu-id="1c0e8-168">Sì</span><span class="sxs-lookup"><span data-stu-id="1c0e8-168">Yes</span></span> | <span data-ttu-id="1c0e8-169">Frequenza, in minuti, con cui viene eseguita la query.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-169">How often the query runs in minutes.</span></span> |
| <span data-ttu-id="1c0e8-170">queryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="1c0e8-170">queryTimeSpan</span></span> | <span data-ttu-id="1c0e8-171">Sì</span><span class="sxs-lookup"><span data-stu-id="1c0e8-171">Yes</span></span> | <span data-ttu-id="1c0e8-172">Periodo di tempo, in minuti, per cui verranno valutati i risultati.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-172">Length of time in minutes over which to evaluate results.</span></span> |

<span data-ttu-id="1c0e8-173">La risorsa pianificazione dipenderà dalla ricerca salvata, che verrà quindi creata prima della pianificazione.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-173">The schedule resource should depend on the saved search so that it's created before the schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="1c0e8-174">Azioni</span><span class="sxs-lookup"><span data-stu-id="1c0e8-174">Actions</span></span>
<span data-ttu-id="1c0e8-175">La proprietà **Type** specifica due tipi di risorsa azione.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-175">There are two types of action resource specified by the **Type** property.</span></span>  <span data-ttu-id="1c0e8-176">Una pianificazione richiede un'azione **Alert** che definisce i dettagli della regola di avviso e le azioni da eseguire quando viene creato un avviso.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-176">A schedule requires one **Alert** action which defines the details of the alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="1c0e8-177">Può includere anche un'azione **Webhook**, se dall'avviso verrà chiamato un webhook.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-177">It may also include a **Webhook** action if a webhook should be called from the alert.</span></span>  

<span data-ttu-id="1c0e8-178">Le risorse azione sono di tipo `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-178">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="1c0e8-179">Azioni di avviso</span><span class="sxs-lookup"><span data-stu-id="1c0e8-179">Alert actions</span></span>

<span data-ttu-id="1c0e8-180">Ogni pianificazione avrà un'azione **Alert**,</span><span class="sxs-lookup"><span data-stu-id="1c0e8-180">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="1c0e8-181">che definisce i dettagli dell'avviso e, facoltativamente, le azioni di notifica e correzione.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-181">This defines the details of the alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="1c0e8-182">Una notifica invia un messaggio di posta elettronica a uno o più indirizzi.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-182">A notification sends an email to one or more addresses.</span></span>  <span data-ttu-id="1c0e8-183">Una correzione avvia un runbook in Automazione di Azure per provare a risolvere il problema rilevato.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-183">A remediation starts a runbook in Azure Automation to attempt to remediate the detected issue.</span></span>

<span data-ttu-id="1c0e8-184">Le azioni di avviso hanno la struttura seguente.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-184">Alert actions have the following structure.</span></span>  <span data-ttu-id="1c0e8-185">Nella struttura sono inclusi parametri e variabili comuni ed è quindi possibile copiare e incollare questo frammento di codice nel file della soluzione e, se necessario, modificare i nomi dei parametri.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-185">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

<span data-ttu-id="1c0e8-186">Le proprietà delle risorse azione di avviso sono descritte nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-186">The properties for Alert action resources are described in the following tables.</span></span>

| <span data-ttu-id="1c0e8-187">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="1c0e8-187">Element name</span></span> | <span data-ttu-id="1c0e8-188">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1c0e8-188">Required</span></span> | <span data-ttu-id="1c0e8-189">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1c0e8-189">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="1c0e8-190">Type</span><span class="sxs-lookup"><span data-stu-id="1c0e8-190">Type</span></span> | <span data-ttu-id="1c0e8-191">Sì</span><span class="sxs-lookup"><span data-stu-id="1c0e8-191">Yes</span></span> | <span data-ttu-id="1c0e8-192">Tipo di azione.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-192">Type of the action.</span></span>  <span data-ttu-id="1c0e8-193">Per le azioni di avviso, sarà **Alert**.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-193">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="1c0e8-194">Nome</span><span class="sxs-lookup"><span data-stu-id="1c0e8-194">Name</span></span> | <span data-ttu-id="1c0e8-195">Sì</span><span class="sxs-lookup"><span data-stu-id="1c0e8-195">Yes</span></span> | <span data-ttu-id="1c0e8-196">Nome visualizzato per l'avviso.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-196">Display name for the alert.</span></span>  <span data-ttu-id="1c0e8-197">È il nome visualizzato nella console per la regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-197">This is the name that's displayed in the console for the alert rule.</span></span> |
| <span data-ttu-id="1c0e8-198">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1c0e8-198">Description</span></span> | <span data-ttu-id="1c0e8-199">No</span><span class="sxs-lookup"><span data-stu-id="1c0e8-199">No</span></span> | <span data-ttu-id="1c0e8-200">Descrizione facoltativa dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-200">Optional description of the alert.</span></span> |
| <span data-ttu-id="1c0e8-201">Severity</span><span class="sxs-lookup"><span data-stu-id="1c0e8-201">Severity</span></span> | <span data-ttu-id="1c0e8-202">Sì</span><span class="sxs-lookup"><span data-stu-id="1c0e8-202">Yes</span></span> | <span data-ttu-id="1c0e8-203">Gravità del record di avviso tra i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="1c0e8-203">Severity of the alert record from the following values:</span></span><br><br> <span data-ttu-id="1c0e8-204">**Critical**</span><span class="sxs-lookup"><span data-stu-id="1c0e8-204">**Critical**</span></span><br><span data-ttu-id="1c0e8-205">**Warning**</span><span class="sxs-lookup"><span data-stu-id="1c0e8-205">**Warning**</span></span><br><span data-ttu-id="1c0e8-206">**Informational**</span><span class="sxs-lookup"><span data-stu-id="1c0e8-206">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="1c0e8-207">Soglia</span><span class="sxs-lookup"><span data-stu-id="1c0e8-207">Threshold</span></span>
<span data-ttu-id="1c0e8-208">Questa sezione è obbligatoria</span><span class="sxs-lookup"><span data-stu-id="1c0e8-208">This section is required.</span></span>  <span data-ttu-id="1c0e8-209">e definisce le proprietà della soglia dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-209">It defines the properties for the alert threshold.</span></span>

| <span data-ttu-id="1c0e8-210">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="1c0e8-210">Element name</span></span> | <span data-ttu-id="1c0e8-211">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1c0e8-211">Required</span></span> | <span data-ttu-id="1c0e8-212">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1c0e8-212">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="1c0e8-213">Operatore</span><span class="sxs-lookup"><span data-stu-id="1c0e8-213">Operator</span></span> | <span data-ttu-id="1c0e8-214">Sì</span><span class="sxs-lookup"><span data-stu-id="1c0e8-214">Yes</span></span> | <span data-ttu-id="1c0e8-215">Operatore di confronto tra i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="1c0e8-215">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="1c0e8-216">**gt = maggiore di<br>lt = minore di**</span><span class="sxs-lookup"><span data-stu-id="1c0e8-216">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="1c0e8-217">Valore</span><span class="sxs-lookup"><span data-stu-id="1c0e8-217">Value</span></span> | <span data-ttu-id="1c0e8-218">Sì</span><span class="sxs-lookup"><span data-stu-id="1c0e8-218">Yes</span></span> | <span data-ttu-id="1c0e8-219">Valore per il confronto dei risultati.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-219">The value to compare the results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="1c0e8-220">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="1c0e8-220">MetricsTrigger</span></span>
<span data-ttu-id="1c0e8-221">Questa sezione è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-221">This section is optional.</span></span>  <span data-ttu-id="1c0e8-222">Includere la sezione per un avviso di misurazione delle metriche.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-222">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="1c0e8-223">Gli avvisi di misurazione delle metriche sono attualmente disponibili in anteprima pubblica.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-223">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="1c0e8-224">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="1c0e8-224">Element name</span></span> | <span data-ttu-id="1c0e8-225">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1c0e8-225">Required</span></span> | <span data-ttu-id="1c0e8-226">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1c0e8-226">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="1c0e8-227">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="1c0e8-227">TriggerCondition</span></span> | <span data-ttu-id="1c0e8-228">Sì</span><span class="sxs-lookup"><span data-stu-id="1c0e8-228">Yes</span></span> | <span data-ttu-id="1c0e8-229">Specifica se la soglia riguarda il numero totale di violazioni o le violazioni consecutive, con i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="1c0e8-229">Specifies whether the threshold is for total number of breaches or consecutive breaches from the following values:</span></span><br><br><span data-ttu-id="1c0e8-230">**Total<br>Consecutive**</span><span class="sxs-lookup"><span data-stu-id="1c0e8-230">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="1c0e8-231">Operatore</span><span class="sxs-lookup"><span data-stu-id="1c0e8-231">Operator</span></span> | <span data-ttu-id="1c0e8-232">Sì</span><span class="sxs-lookup"><span data-stu-id="1c0e8-232">Yes</span></span> | <span data-ttu-id="1c0e8-233">Operatore di confronto tra i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="1c0e8-233">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="1c0e8-234">**gt = maggiore di<br>lt = minore di**</span><span class="sxs-lookup"><span data-stu-id="1c0e8-234">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="1c0e8-235">Valore</span><span class="sxs-lookup"><span data-stu-id="1c0e8-235">Value</span></span> | <span data-ttu-id="1c0e8-236">Sì</span><span class="sxs-lookup"><span data-stu-id="1c0e8-236">Yes</span></span> | <span data-ttu-id="1c0e8-237">Numero di volte in cui i criteri devono essere soddisfatti per attivare l'avviso.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-237">Number of the times the criteria must be met to trigger the alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="1c0e8-238">Limitazione</span><span class="sxs-lookup"><span data-stu-id="1c0e8-238">Throttling</span></span>
<span data-ttu-id="1c0e8-239">Questa sezione è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-239">This section is optional.</span></span>  <span data-ttu-id="1c0e8-240">Includere la sezione se si vogliono eliminare gli avvisi generati dalla stessa regola per un determinato intervallo di tempo dopo la creazione di un avviso.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-240">Include this section if you want to suppress alerts from the same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="1c0e8-241">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="1c0e8-241">Element name</span></span> | <span data-ttu-id="1c0e8-242">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1c0e8-242">Required</span></span> | <span data-ttu-id="1c0e8-243">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1c0e8-243">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="1c0e8-244">DurationInMinutes</span><span class="sxs-lookup"><span data-stu-id="1c0e8-244">DurationInMinutes</span></span> | <span data-ttu-id="1c0e8-245">Sì, se è incluso l'elemento Throttling</span><span class="sxs-lookup"><span data-stu-id="1c0e8-245">Yes if Throttling element included</span></span> | <span data-ttu-id="1c0e8-246">Numero di minuti in cui verranno eliminati gli avvisi dopo che ne è stato creato uno dalla stessa regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-246">Number of minutes to suppress alerts after one from the same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="1c0e8-247">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="1c0e8-247">EmailNotification</span></span>
 <span data-ttu-id="1c0e8-248">Questa sezione è facoltativa. Includere la sezione se si vuole inviare un messaggio di posta elettronica a uno o più destinatari.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-248">This section is optional  Include it if you want the alert to send mail to one or more recipients.</span></span>

| <span data-ttu-id="1c0e8-249">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="1c0e8-249">Element name</span></span> | <span data-ttu-id="1c0e8-250">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1c0e8-250">Required</span></span> | <span data-ttu-id="1c0e8-251">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1c0e8-251">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="1c0e8-252">Destinatari</span><span class="sxs-lookup"><span data-stu-id="1c0e8-252">Recipients</span></span> | <span data-ttu-id="1c0e8-253">Sì</span><span class="sxs-lookup"><span data-stu-id="1c0e8-253">Yes</span></span> | <span data-ttu-id="1c0e8-254">Elenco delimitato da virgole di indirizzi di posta elettronica a cui inviare una notifica quando viene creato un avviso, come nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-254">Comma delimited list of email addresses to send notification when an alert is created such as in the following example.</span></span><br><br><span data-ttu-id="1c0e8-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="1c0e8-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="1c0e8-256">Oggetto</span><span class="sxs-lookup"><span data-stu-id="1c0e8-256">Subject</span></span> | <span data-ttu-id="1c0e8-257">Sì</span><span class="sxs-lookup"><span data-stu-id="1c0e8-257">Yes</span></span> | <span data-ttu-id="1c0e8-258">Riga dell'oggetto del messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-258">Subject line of the mail.</span></span> |
| <span data-ttu-id="1c0e8-259">Attachment</span><span class="sxs-lookup"><span data-stu-id="1c0e8-259">Attachment</span></span> | <span data-ttu-id="1c0e8-260">No</span><span class="sxs-lookup"><span data-stu-id="1c0e8-260">No</span></span> | <span data-ttu-id="1c0e8-261">Gli allegati non sono attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-261">Attachments are not currently supported.</span></span>  <span data-ttu-id="1c0e8-262">Se questo elemento è incluso, il valore dovrà essere **None**.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-262">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="1c0e8-263">Correzione</span><span class="sxs-lookup"><span data-stu-id="1c0e8-263">Remediation</span></span>
<span data-ttu-id="1c0e8-264">Questa sezione è facoltativa. Includere la sezione se si vuole avviare un runbook in risposta all'avviso.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-264">This section is optional  Include it if you want a runbook to start in response to the alert.</span></span> |

| <span data-ttu-id="1c0e8-265">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="1c0e8-265">Element name</span></span> | <span data-ttu-id="1c0e8-266">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1c0e8-266">Required</span></span> | <span data-ttu-id="1c0e8-267">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1c0e8-267">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="1c0e8-268">RunbookName</span><span class="sxs-lookup"><span data-stu-id="1c0e8-268">RunbookName</span></span> | <span data-ttu-id="1c0e8-269">Sì</span><span class="sxs-lookup"><span data-stu-id="1c0e8-269">Yes</span></span> | <span data-ttu-id="1c0e8-270">Nome del runbook da avviare.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-270">Name of the runbook to start.</span></span> |
| <span data-ttu-id="1c0e8-271">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="1c0e8-271">WebhookUri</span></span> | <span data-ttu-id="1c0e8-272">Sì</span><span class="sxs-lookup"><span data-stu-id="1c0e8-272">Yes</span></span> | <span data-ttu-id="1c0e8-273">URI del webhook per il runbook.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-273">Uri of the webhook for the runbook.</span></span> |
| <span data-ttu-id="1c0e8-274">Expiry</span><span class="sxs-lookup"><span data-stu-id="1c0e8-274">Expiry</span></span> | <span data-ttu-id="1c0e8-275">No</span><span class="sxs-lookup"><span data-stu-id="1c0e8-275">No</span></span> | <span data-ttu-id="1c0e8-276">Data e ora di scadenza della correzione.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-276">Date and time that the remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="1c0e8-277">Azioni webhook</span><span class="sxs-lookup"><span data-stu-id="1c0e8-277">Webhook actions</span></span>

<span data-ttu-id="1c0e8-278">Le azioni webhook avviano un processo chiamando un URL e, facoltativamente, fornendo un payload da inviare.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-278">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span> <span data-ttu-id="1c0e8-279">Simili alle azioni correttive, sono destinate a webhook che possono richiamare processi diversi dai runbook di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-279">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="1c0e8-280">Hanno inoltre l'opzione aggiuntiva di fornire un payload da recapitare al processo remoto.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-280">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="1c0e8-281">Se l'avviso chiamerà un webhook, sarà necessaria una risorsa azione di tipo **Webhook** in aggiunta alla risorsa azione **Alert**.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-281">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition to the **Alert** action resource.</span></span>  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

<span data-ttu-id="1c0e8-282">Le proprietà delle risorse azione webhook sono descritte nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-282">The properties for Webhook action resources are described in the following tables.</span></span>

| <span data-ttu-id="1c0e8-283">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="1c0e8-283">Element name</span></span> | <span data-ttu-id="1c0e8-284">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1c0e8-284">Required</span></span> | <span data-ttu-id="1c0e8-285">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1c0e8-285">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="1c0e8-286">type</span><span class="sxs-lookup"><span data-stu-id="1c0e8-286">type</span></span> | <span data-ttu-id="1c0e8-287">Sì</span><span class="sxs-lookup"><span data-stu-id="1c0e8-287">Yes</span></span> | <span data-ttu-id="1c0e8-288">Tipo di azione.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-288">Type of the action.</span></span>  <span data-ttu-id="1c0e8-289">Per le azioni webhook, sarà **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-289">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="1c0e8-290">name</span><span class="sxs-lookup"><span data-stu-id="1c0e8-290">name</span></span> | <span data-ttu-id="1c0e8-291">Sì</span><span class="sxs-lookup"><span data-stu-id="1c0e8-291">Yes</span></span> | <span data-ttu-id="1c0e8-292">Nome visualizzato per l'azione.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-292">Display name for the action.</span></span>  <span data-ttu-id="1c0e8-293">Non viene visualizzato nella console.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-293">This is not displayed in the console.</span></span> |
| <span data-ttu-id="1c0e8-294">wehookUri</span><span class="sxs-lookup"><span data-stu-id="1c0e8-294">wehookUri</span></span> | <span data-ttu-id="1c0e8-295">Sì</span><span class="sxs-lookup"><span data-stu-id="1c0e8-295">Yes</span></span> | <span data-ttu-id="1c0e8-296">URI del webhook.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-296">Uri for the webhook.</span></span> |
| <span data-ttu-id="1c0e8-297">customPayload</span><span class="sxs-lookup"><span data-stu-id="1c0e8-297">customPayload</span></span> | <span data-ttu-id="1c0e8-298">No</span><span class="sxs-lookup"><span data-stu-id="1c0e8-298">No</span></span> | <span data-ttu-id="1c0e8-299">Payload personalizzato da inviare al webhook.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-299">Custom payload to be sent to the webhook.</span></span> <span data-ttu-id="1c0e8-300">Il formato dipenderà dalle previsioni del webhook.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-300">The format will depend on what the webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="1c0e8-301">Esempio</span><span class="sxs-lookup"><span data-stu-id="1c0e8-301">Sample</span></span>

<span data-ttu-id="1c0e8-302">Di seguito è riportato un esempio di soluzione che include le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="1c0e8-302">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="1c0e8-303">Ricerca salvata</span><span class="sxs-lookup"><span data-stu-id="1c0e8-303">Saved search</span></span>
- <span data-ttu-id="1c0e8-304">Pianificazione</span><span class="sxs-lookup"><span data-stu-id="1c0e8-304">Schedule</span></span>
- <span data-ttu-id="1c0e8-305">Azione di avviso</span><span class="sxs-lookup"><span data-stu-id="1c0e8-305">Alert action</span></span>
- <span data-ttu-id="1c0e8-306">Azione webhook</span><span class="sxs-lookup"><span data-stu-id="1c0e8-306">Webhook action</span></span>

<span data-ttu-id="1c0e8-307">L'esempio usa variabili dei [parametri di soluzione standard](operations-management-suite-solutions-solution-file.md#parameters) comunemente usate in una soluzione, anziché impostare i valori come hardcoded nelle definizioni delle risorse.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-307">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for the email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


<span data-ttu-id="1c0e8-308">Il file di parametri seguente offre valori di esempio per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-308">The following parameter file provides samples values for this solution.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="1c0e8-309">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1c0e8-309">Next steps</span></span>
* <span data-ttu-id="1c0e8-310">[Aggiungere viste](operations-management-suite-solutions-resources-views.md) alla soluzione di gestione.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-310">[Add views](operations-management-suite-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="1c0e8-311">[Aggiungere runbook di automazione e altre risorse](operations-management-suite-solutions-resources-automation.md) alla soluzione di gestione.</span><span class="sxs-lookup"><span data-stu-id="1c0e8-311">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) to your management solution.</span></span>


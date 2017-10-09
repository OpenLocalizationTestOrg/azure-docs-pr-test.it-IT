---
title: aaaSaved ricerche e avvisi in soluzioni OMS | Documenti Microsoft
description: "Soluzioni in OMS in genere comprendono le ricerche salvate nei dati tooanalyze Analitica Log raccolti dalla soluzione hello.  Si può anche definire utente hello toonotify di avvisi o automaticamente intervenire in problema grave di risposta tooa.  In questo articolo viene descritto come toodefine Analitica registro salvato avvisi e ricerche in un modello ARM in modo che possano essere incluse nelle soluzioni di gestione."
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
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a><span data-ttu-id="574d9-105">Aggiunta Log Analitica salvato tooOMS ricerche e gli avvisi la soluzione di gestione (anteprima)</span><span class="sxs-lookup"><span data-stu-id="574d9-105">Adding Log Analytics saved searches and alerts tooOMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="574d9-106">Questa è una documentazione preliminare per la creazione di soluzioni di gestione in OMS attualmente disponibili in versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="574d9-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="574d9-107">Qualsiasi schema descritto di seguito è soggetto toochange.</span><span class="sxs-lookup"><span data-stu-id="574d9-107">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="574d9-108">[Soluzioni di gestione in OMS](operations-management-suite-solutions.md) includerà in genere [ricerche salvate](../log-analytics/log-analytics-log-searches.md) nei dati tooanalyze Analitica Log raccolti dalla soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics tooanalyze data collected by hello solution.</span></span>  <span data-ttu-id="574d9-109">Possono anche definire [avvisi](../log-analytics/log-analytics-alerts.md) toonotify hello utente o eseguire automaticamente azioni problema critico tooa di risposta.</span><span class="sxs-lookup"><span data-stu-id="574d9-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) toonotify hello user or automatically take action in response tooa critical issue.</span></span>  <span data-ttu-id="574d9-110">In questo articolo viene descritto come toodefine Analitica Log salvate ricerche e avvisi in un [modello di gestione delle risorse](../resource-manager-template-walkthrough.md) in modo che possano essere incluse [soluzioni di gestione](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="574d9-110">This article describes how toodefine Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="574d9-111">Hello esempi in questo articolo utilizzano parametri e variabili che sono entrambe soluzioni toomanagement necessarie o comuni e descritte in [la creazione di soluzioni di gestione in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="574d9-111">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="574d9-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="574d9-112">Prerequisites</span></span>
<span data-ttu-id="574d9-113">Questo articolo si presuppone che si ha già familiarità con come troppo[creare una soluzione di gestione](operations-management-suite-solutions-creating.md) e la struttura di hello di un [modello ARM](../resource-group-authoring-templates.md) e file di soluzione.</span><span class="sxs-lookup"><span data-stu-id="574d9-113">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="574d9-114">Area di lavoro di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="574d9-114">Log Analytics Workspace</span></span>
<span data-ttu-id="574d9-115">Tutte le risorse in Log Analytics sono contenute in un'[area di lavoro](../log-analytics/log-analytics-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="574d9-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="574d9-116">Come descritto in [OMS dell'area di lavoro e account di automazione](operations-management-suite-solutions.md#oms-workspace-and-automation-account) dell'area di lavoro di hello non è incluso nella soluzione di gestione di hello ma deve essere presente prima di installata la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello workspace isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="574d9-117">Se non è disponibile, l'installazione di soluzioni hello avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="574d9-117">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="574d9-118">nome Hello dell'area di lavoro hello è nome hello di ogni risorsa Analitica di Log.</span><span class="sxs-lookup"><span data-stu-id="574d9-118">hello name of hello workspace is in hello name of each Log Analytics resource.</span></span>  <span data-ttu-id="574d9-119">Questa operazione viene eseguita nella soluzione hello con hello **dell'area di lavoro** parametro come hello seguente esempio di una risorsa savedsearch.</span><span class="sxs-lookup"><span data-stu-id="574d9-119">This is done in hello solution with hello **workspace** parameter as in hello following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="574d9-120">Ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="574d9-120">Saved Searches</span></span>
<span data-ttu-id="574d9-121">Includere [ricerche salvate](../log-analytics/log-analytics-log-searches.md) in una soluzione tooallow utenti tooquery di dati raccolti dalla soluzione.</span><span class="sxs-lookup"><span data-stu-id="574d9-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution tooallow users tooquery data collected by your solution.</span></span>  <span data-ttu-id="574d9-122">Ricerche salvate verranno visualizzato in **Preferiti** nel portale OMS hello e **ricerche salvate** in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="574d9-122">Saved searches will appear under **Favorites** in hello OMS portal and **Saved Searches** in hello Azure portal .</span></span>  <span data-ttu-id="574d9-123">È necessaria una ricerca salvata anche per ogni avviso.</span><span class="sxs-lookup"><span data-stu-id="574d9-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="574d9-124">[Ricerca salvata Analitica log](../log-analytics/log-analytics-log-searches.md) risorse hanno un tipo di `Microsoft.OperationalInsights/workspaces/savedSearches` e hello seguente struttura.</span><span class="sxs-lookup"><span data-stu-id="574d9-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have hello following structure.</span></span>  <span data-ttu-id="574d9-125">Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-125">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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



<span data-ttu-id="574d9-126">Ogni proprietà hello di una ricerca salvata sono descritti nella seguente tabella hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-126">Each of hello properties of a saved search are described in hello following table.</span></span> 

| <span data-ttu-id="574d9-127">Proprietà</span><span class="sxs-lookup"><span data-stu-id="574d9-127">Property</span></span> | <span data-ttu-id="574d9-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="574d9-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="574d9-129">category</span><span class="sxs-lookup"><span data-stu-id="574d9-129">category</span></span> | <span data-ttu-id="574d9-130">categoria di Hello per la ricerca salvata hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-130">hello category for hello saved search.</span></span>  <span data-ttu-id="574d9-131">Le ricerche salvate nella stessa soluzione spesso condividono hello un'unica categoria pertanto vengono raggruppati insieme nella console di hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-131">Any saved searches in hello same solution will often share a single category so they are grouped together in hello console.</span></span> |
| <span data-ttu-id="574d9-132">displayname</span><span class="sxs-lookup"><span data-stu-id="574d9-132">displayname</span></span> | <span data-ttu-id="574d9-133">Nome toodisplay per hello ricerca salvata nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-133">Name toodisplay for hello saved search in hello portal.</span></span> |
| <span data-ttu-id="574d9-134">query</span><span class="sxs-lookup"><span data-stu-id="574d9-134">query</span></span> | <span data-ttu-id="574d9-135">Eseguire una query toorun.</span><span class="sxs-lookup"><span data-stu-id="574d9-135">Query toorun.</span></span> |

> [!NOTE]
> <span data-ttu-id="574d9-136">Caratteri di escape toouse nella query hello potrebbe essere necessario se include caratteri che potrebbero essere interpretati come JSON.</span><span class="sxs-lookup"><span data-stu-id="574d9-136">You may need toouse escape characters in hello query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="574d9-137">Ad esempio, se la query è stata **OperationName:"Microsoft.Compute/virtualMachines/write tipo: AzureActivity"**, devono essere scritti nel file di soluzione hello come **OperationName tipo: AzureActivity:\" Microsoft.Compute/virtualMachines/write\"**.</span><span class="sxs-lookup"><span data-stu-id="574d9-137">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in hello solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="574d9-138">Avvisi</span><span class="sxs-lookup"><span data-stu-id="574d9-138">Alerts</span></span>
<span data-ttu-id="574d9-139">Gli [avvisi di Log Analytics](../log-analytics/log-analytics-alerts.md) vengono creati da regole di avviso che eseguono una ricerca salvata a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="574d9-139">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="574d9-140">Se i risultati di hello di hello query corrispondono ai criteri specificati, viene creato un record di avviso e vengono eseguite uno o più azioni.</span><span class="sxs-lookup"><span data-stu-id="574d9-140">If hello results of hello query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="574d9-141">Le regole di avviso in una soluzione di gestione sono costituite da hello seguenti tre risorse diverse.</span><span class="sxs-lookup"><span data-stu-id="574d9-141">Alert rules in a management solution are made up of hello following three different resources.</span></span>

- <span data-ttu-id="574d9-142">**Ricerca salvata.**</span><span class="sxs-lookup"><span data-stu-id="574d9-142">**Saved search.**</span></span>  <span data-ttu-id="574d9-143">Definisce una ricerca nei log hello che verrà eseguita.</span><span class="sxs-lookup"><span data-stu-id="574d9-143">Defines hello log search that will be run.</span></span>  <span data-ttu-id="574d9-144">Una singola ricerca salvata può essere condivisa da più regole di avviso.</span><span class="sxs-lookup"><span data-stu-id="574d9-144">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="574d9-145">**Pianificazione.**</span><span class="sxs-lookup"><span data-stu-id="574d9-145">**Schedule.**</span></span>  <span data-ttu-id="574d9-146">Definisce la frequenza con cui hello ricerca nei log verrà eseguito.</span><span class="sxs-lookup"><span data-stu-id="574d9-146">Defines how often hello log search will be run.</span></span>  <span data-ttu-id="574d9-147">Ogni regola di avviso avrà una sola pianificazione.</span><span class="sxs-lookup"><span data-stu-id="574d9-147">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="574d9-148">**Azione di avviso.**</span><span class="sxs-lookup"><span data-stu-id="574d9-148">**Alert action.**</span></span>  <span data-ttu-id="574d9-149">Ogni regola di avviso avrà una risorsa di azione con un tipo di **avviso** che definisce i dettagli di hello di hello avviso, ad esempio criteri hello verrà creato un record di avviso e hello gravità dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="574d9-149">Each alert rule will have one action resource with a type of **Alert** that defines hello details of hello alert such as hello criteria for when an alert record will be created and hello alert's severity.</span></span>  <span data-ttu-id="574d9-150">risorsa dell'azione Hello definirà facoltativamente una risposta di posta elettronica e il runbook.</span><span class="sxs-lookup"><span data-stu-id="574d9-150">hello action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="574d9-151">**Azione webhook (facoltativa).**</span><span class="sxs-lookup"><span data-stu-id="574d9-151">**Webhook action (optional).**</span></span>  <span data-ttu-id="574d9-152">Se la regola di avviso hello chiamerà un webhook, quindi richiede una risorsa di un'ulteriore azione con un tipo di **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="574d9-152">If hello alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="574d9-153">Le risorse ricerca salvata sono illustrate sopra.</span><span class="sxs-lookup"><span data-stu-id="574d9-153">Saved search resources are described above.</span></span>  <span data-ttu-id="574d9-154">Hello altre risorse sono descritti di seguito.</span><span class="sxs-lookup"><span data-stu-id="574d9-154">hello other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="574d9-155">Risorsa pianificazione</span><span class="sxs-lookup"><span data-stu-id="574d9-155">Schedule resource</span></span>

<span data-ttu-id="574d9-156">Una ricerca salvata può avere una o più pianificazioni, ognuna delle quali rappresenta una regola di avviso separata.</span><span class="sxs-lookup"><span data-stu-id="574d9-156">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="574d9-157">Hello pianificazione definisce la frequenza con cui hello ricerca viene eseguita e hello intervallo di tempo su cui hello vengono recuperati i dati.</span><span class="sxs-lookup"><span data-stu-id="574d9-157">hello schedule defines how often hello search is run and hello time interval over which hello data is retrieved.</span></span>  <span data-ttu-id="574d9-158">Risorse di pianificazione dispongono di un tipo di `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` e hello seguente struttura.</span><span class="sxs-lookup"><span data-stu-id="574d9-158">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have hello following structure.</span></span> <span data-ttu-id="574d9-159">Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-159">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


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



<span data-ttu-id="574d9-160">Nella hello nella tabella seguente sono descritte le proprietà di Hello per le risorse di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="574d9-160">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="574d9-161">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="574d9-161">Element name</span></span> | <span data-ttu-id="574d9-162">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="574d9-162">Required</span></span> | <span data-ttu-id="574d9-163">Descrizione</span><span class="sxs-lookup"><span data-stu-id="574d9-163">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="574d9-164">Enabled</span><span class="sxs-lookup"><span data-stu-id="574d9-164">enabled</span></span>       | <span data-ttu-id="574d9-165">Sì</span><span class="sxs-lookup"><span data-stu-id="574d9-165">Yes</span></span> | <span data-ttu-id="574d9-166">Specifica se l'avviso di hello è abilitato quando viene creato.</span><span class="sxs-lookup"><span data-stu-id="574d9-166">Specifies whether hello alert is enabled when it's created.</span></span> |
| <span data-ttu-id="574d9-167">interval</span><span class="sxs-lookup"><span data-stu-id="574d9-167">interval</span></span>      | <span data-ttu-id="574d9-168">Sì</span><span class="sxs-lookup"><span data-stu-id="574d9-168">Yes</span></span> | <span data-ttu-id="574d9-169">La frequenza con cui hello query viene eseguita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="574d9-169">How often hello query runs in minutes.</span></span> |
| <span data-ttu-id="574d9-170">queryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="574d9-170">queryTimeSpan</span></span> | <span data-ttu-id="574d9-171">Sì</span><span class="sxs-lookup"><span data-stu-id="574d9-171">Yes</span></span> | <span data-ttu-id="574d9-172">Periodo di tempo in minuti in base alla quale tooevaluate.</span><span class="sxs-lookup"><span data-stu-id="574d9-172">Length of time in minutes over which tooevaluate results.</span></span> |

<span data-ttu-id="574d9-173">risorse di pianificazione Hello dovrebbero dipendere hello ricerca salvata in modo che viene creato prima pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-173">hello schedule resource should depend on hello saved search so that it's created before hello schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="574d9-174">Azioni</span><span class="sxs-lookup"><span data-stu-id="574d9-174">Actions</span></span>
<span data-ttu-id="574d9-175">Esistono due tipi di risorsa dell'azione specificata da hello **tipo** proprietà.</span><span class="sxs-lookup"><span data-stu-id="574d9-175">There are two types of action resource specified by hello **Type** property.</span></span>  <span data-ttu-id="574d9-176">Una pianificazione richiede una **avviso** azione che definisce i dettagli di hello di regola di avviso hello e le azioni eseguite quando viene creato un avviso.</span><span class="sxs-lookup"><span data-stu-id="574d9-176">A schedule requires one **Alert** action which defines hello details of hello alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="574d9-177">Può inoltre includere un **Webhook** azione se un webhook deve essere chiamato dall'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-177">It may also include a **Webhook** action if a webhook should be called from hello alert.</span></span>  

<span data-ttu-id="574d9-178">Le risorse azione sono di tipo `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span><span class="sxs-lookup"><span data-stu-id="574d9-178">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="574d9-179">Azioni di avviso</span><span class="sxs-lookup"><span data-stu-id="574d9-179">Alert actions</span></span>

<span data-ttu-id="574d9-180">Ogni pianificazione avrà un'azione **Alert**,</span><span class="sxs-lookup"><span data-stu-id="574d9-180">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="574d9-181">Definisce i dettagli di hello di avviso hello e, facoltativamente, le azioni di notifica e monitoraggio e aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="574d9-181">This defines hello details of hello alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="574d9-182">Una notifica invia un messaggio di posta elettronica tooone o più indirizzi.</span><span class="sxs-lookup"><span data-stu-id="574d9-182">A notification sends an email tooone or more addresses.</span></span>  <span data-ttu-id="574d9-183">Una risoluzione avvia un runbook problema rilevato hello tooremediate tooattempt di automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="574d9-183">A remediation starts a runbook in Azure Automation tooattempt tooremediate hello detected issue.</span></span>

<span data-ttu-id="574d9-184">Le azioni avviso hanno hello seguente struttura.</span><span class="sxs-lookup"><span data-stu-id="574d9-184">Alert actions have hello following structure.</span></span>  <span data-ttu-id="574d9-185">Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-185">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 



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

<span data-ttu-id="574d9-186">Nella hello le tabelle seguenti sono descritte le proprietà di Hello per le risorse di azione di allarme.</span><span class="sxs-lookup"><span data-stu-id="574d9-186">hello properties for Alert action resources are described in hello following tables.</span></span>

| <span data-ttu-id="574d9-187">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="574d9-187">Element name</span></span> | <span data-ttu-id="574d9-188">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="574d9-188">Required</span></span> | <span data-ttu-id="574d9-189">Descrizione</span><span class="sxs-lookup"><span data-stu-id="574d9-189">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="574d9-190">Type</span><span class="sxs-lookup"><span data-stu-id="574d9-190">Type</span></span> | <span data-ttu-id="574d9-191">Sì</span><span class="sxs-lookup"><span data-stu-id="574d9-191">Yes</span></span> | <span data-ttu-id="574d9-192">Tipo di azione hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-192">Type of hello action.</span></span>  <span data-ttu-id="574d9-193">Per le azioni di avviso, sarà **Alert**.</span><span class="sxs-lookup"><span data-stu-id="574d9-193">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="574d9-194">Nome</span><span class="sxs-lookup"><span data-stu-id="574d9-194">Name</span></span> | <span data-ttu-id="574d9-195">Sì</span><span class="sxs-lookup"><span data-stu-id="574d9-195">Yes</span></span> | <span data-ttu-id="574d9-196">Nome visualizzato per l'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-196">Display name for hello alert.</span></span>  <span data-ttu-id="574d9-197">Si tratta di nome hello che viene visualizzato nella console di hello per regola di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-197">This is hello name that's displayed in hello console for hello alert rule.</span></span> |
| <span data-ttu-id="574d9-198">Descrizione</span><span class="sxs-lookup"><span data-stu-id="574d9-198">Description</span></span> | <span data-ttu-id="574d9-199">No</span><span class="sxs-lookup"><span data-stu-id="574d9-199">No</span></span> | <span data-ttu-id="574d9-200">Descrizione facoltativa dell'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-200">Optional description of hello alert.</span></span> |
| <span data-ttu-id="574d9-201">Severity</span><span class="sxs-lookup"><span data-stu-id="574d9-201">Severity</span></span> | <span data-ttu-id="574d9-202">Sì</span><span class="sxs-lookup"><span data-stu-id="574d9-202">Yes</span></span> | <span data-ttu-id="574d9-203">Gravità di record di avviso hello da hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="574d9-203">Severity of hello alert record from hello following values:</span></span><br><br> <span data-ttu-id="574d9-204">**Critical**</span><span class="sxs-lookup"><span data-stu-id="574d9-204">**Critical**</span></span><br><span data-ttu-id="574d9-205">**Warning**</span><span class="sxs-lookup"><span data-stu-id="574d9-205">**Warning**</span></span><br><span data-ttu-id="574d9-206">**Informational**</span><span class="sxs-lookup"><span data-stu-id="574d9-206">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="574d9-207">Soglia</span><span class="sxs-lookup"><span data-stu-id="574d9-207">Threshold</span></span>
<span data-ttu-id="574d9-208">Questa sezione è obbligatoria</span><span class="sxs-lookup"><span data-stu-id="574d9-208">This section is required.</span></span>  <span data-ttu-id="574d9-209">Definisce le proprietà di hello di soglia di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-209">It defines hello properties for hello alert threshold.</span></span>

| <span data-ttu-id="574d9-210">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="574d9-210">Element name</span></span> | <span data-ttu-id="574d9-211">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="574d9-211">Required</span></span> | <span data-ttu-id="574d9-212">Descrizione</span><span class="sxs-lookup"><span data-stu-id="574d9-212">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="574d9-213">Operatore</span><span class="sxs-lookup"><span data-stu-id="574d9-213">Operator</span></span> | <span data-ttu-id="574d9-214">Sì</span><span class="sxs-lookup"><span data-stu-id="574d9-214">Yes</span></span> | <span data-ttu-id="574d9-215">Operatore per il confronto di hello da hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="574d9-215">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="574d9-216">**gt = maggiore di<br>lt = minore di**</span><span class="sxs-lookup"><span data-stu-id="574d9-216">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="574d9-217">Valore</span><span class="sxs-lookup"><span data-stu-id="574d9-217">Value</span></span> | <span data-ttu-id="574d9-218">Sì</span><span class="sxs-lookup"><span data-stu-id="574d9-218">Yes</span></span> | <span data-ttu-id="574d9-219">risultati di hello toocompare valore Hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-219">hello value toocompare hello results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="574d9-220">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="574d9-220">MetricsTrigger</span></span>
<span data-ttu-id="574d9-221">Questa sezione è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="574d9-221">This section is optional.</span></span>  <span data-ttu-id="574d9-222">Includere la sezione per un avviso di misurazione delle metriche.</span><span class="sxs-lookup"><span data-stu-id="574d9-222">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="574d9-223">Gli avvisi di misurazione delle metriche sono attualmente disponibili in anteprima pubblica.</span><span class="sxs-lookup"><span data-stu-id="574d9-223">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="574d9-224">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="574d9-224">Element name</span></span> | <span data-ttu-id="574d9-225">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="574d9-225">Required</span></span> | <span data-ttu-id="574d9-226">Descrizione</span><span class="sxs-lookup"><span data-stu-id="574d9-226">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="574d9-227">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="574d9-227">TriggerCondition</span></span> | <span data-ttu-id="574d9-228">Sì</span><span class="sxs-lookup"><span data-stu-id="574d9-228">Yes</span></span> | <span data-ttu-id="574d9-229">Specifica se la soglia hello è per il numero totale di violazioni della sicurezza o violazioni consecutivi da hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="574d9-229">Specifies whether hello threshold is for total number of breaches or consecutive breaches from hello following values:</span></span><br><br><span data-ttu-id="574d9-230">**Total<br>Consecutive**</span><span class="sxs-lookup"><span data-stu-id="574d9-230">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="574d9-231">Operatore</span><span class="sxs-lookup"><span data-stu-id="574d9-231">Operator</span></span> | <span data-ttu-id="574d9-232">Sì</span><span class="sxs-lookup"><span data-stu-id="574d9-232">Yes</span></span> | <span data-ttu-id="574d9-233">Operatore per il confronto di hello da hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="574d9-233">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="574d9-234">**gt = maggiore di<br>lt = minore di**</span><span class="sxs-lookup"><span data-stu-id="574d9-234">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="574d9-235">Valore</span><span class="sxs-lookup"><span data-stu-id="574d9-235">Value</span></span> | <span data-ttu-id="574d9-236">Sì</span><span class="sxs-lookup"><span data-stu-id="574d9-236">Yes</span></span> | <span data-ttu-id="574d9-237">Numero di hello volte hello criteri deve essere avviso hello tootrigger soddisfatto.</span><span class="sxs-lookup"><span data-stu-id="574d9-237">Number of hello times hello criteria must be met tootrigger hello alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="574d9-238">Limitazione</span><span class="sxs-lookup"><span data-stu-id="574d9-238">Throttling</span></span>
<span data-ttu-id="574d9-239">Questa sezione è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="574d9-239">This section is optional.</span></span>  <span data-ttu-id="574d9-240">Includere questa sezione se si desidera ricevere avvisi relativi toosuppress da hello stessa regola per un periodo di tempo dopo la creazione di un avviso.</span><span class="sxs-lookup"><span data-stu-id="574d9-240">Include this section if you want toosuppress alerts from hello same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="574d9-241">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="574d9-241">Element name</span></span> | <span data-ttu-id="574d9-242">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="574d9-242">Required</span></span> | <span data-ttu-id="574d9-243">Descrizione</span><span class="sxs-lookup"><span data-stu-id="574d9-243">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="574d9-244">DurationInMinutes</span><span class="sxs-lookup"><span data-stu-id="574d9-244">DurationInMinutes</span></span> | <span data-ttu-id="574d9-245">Sì, se è incluso l'elemento Throttling</span><span class="sxs-lookup"><span data-stu-id="574d9-245">Yes if Throttling element included</span></span> | <span data-ttu-id="574d9-246">Numero di minuti toosuppress avvisi dopo uno dal hello viene creata la regola di avviso stesso.</span><span class="sxs-lookup"><span data-stu-id="574d9-246">Number of minutes toosuppress alerts after one from hello same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="574d9-247">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="574d9-247">EmailNotification</span></span>
 <span data-ttu-id="574d9-248">In questa sezione è facoltativa Include se si desidera hello avviso toosend tooone di posta elettronica o altri destinatari.</span><span class="sxs-lookup"><span data-stu-id="574d9-248">This section is optional  Include it if you want hello alert toosend mail tooone or more recipients.</span></span>

| <span data-ttu-id="574d9-249">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="574d9-249">Element name</span></span> | <span data-ttu-id="574d9-250">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="574d9-250">Required</span></span> | <span data-ttu-id="574d9-251">Descrizione</span><span class="sxs-lookup"><span data-stu-id="574d9-251">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="574d9-252">Destinatari</span><span class="sxs-lookup"><span data-stu-id="574d9-252">Recipients</span></span> | <span data-ttu-id="574d9-253">Sì</span><span class="sxs-lookup"><span data-stu-id="574d9-253">Yes</span></span> | <span data-ttu-id="574d9-254">Elenco delimitato da virgole di posta elettronica indirizzi toosend notifica quando un avviso viene creato come nel seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-254">Comma delimited list of email addresses toosend notification when an alert is created such as in hello following example.</span></span><br><br><span data-ttu-id="574d9-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="574d9-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="574d9-256">Oggetto</span><span class="sxs-lookup"><span data-stu-id="574d9-256">Subject</span></span> | <span data-ttu-id="574d9-257">Sì</span><span class="sxs-lookup"><span data-stu-id="574d9-257">Yes</span></span> | <span data-ttu-id="574d9-258">Oggetto riga del messaggio di posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-258">Subject line of hello mail.</span></span> |
| <span data-ttu-id="574d9-259">Attachment</span><span class="sxs-lookup"><span data-stu-id="574d9-259">Attachment</span></span> | <span data-ttu-id="574d9-260">No</span><span class="sxs-lookup"><span data-stu-id="574d9-260">No</span></span> | <span data-ttu-id="574d9-261">Gli allegati non sono attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="574d9-261">Attachments are not currently supported.</span></span>  <span data-ttu-id="574d9-262">Se questo elemento è incluso, il valore dovrà essere **None**.</span><span class="sxs-lookup"><span data-stu-id="574d9-262">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="574d9-263">Correzione</span><span class="sxs-lookup"><span data-stu-id="574d9-263">Remediation</span></span>
<span data-ttu-id="574d9-264">Questa sezione è facoltativa se si desidera che un runbook toostart nell'avviso toohello risposta Include.</span><span class="sxs-lookup"><span data-stu-id="574d9-264">This section is optional  Include it if you want a runbook toostart in response toohello alert.</span></span> |

| <span data-ttu-id="574d9-265">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="574d9-265">Element name</span></span> | <span data-ttu-id="574d9-266">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="574d9-266">Required</span></span> | <span data-ttu-id="574d9-267">Descrizione</span><span class="sxs-lookup"><span data-stu-id="574d9-267">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="574d9-268">RunbookName</span><span class="sxs-lookup"><span data-stu-id="574d9-268">RunbookName</span></span> | <span data-ttu-id="574d9-269">Sì</span><span class="sxs-lookup"><span data-stu-id="574d9-269">Yes</span></span> | <span data-ttu-id="574d9-270">Nome di hello runbook toostart.</span><span class="sxs-lookup"><span data-stu-id="574d9-270">Name of hello runbook toostart.</span></span> |
| <span data-ttu-id="574d9-271">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="574d9-271">WebhookUri</span></span> | <span data-ttu-id="574d9-272">Sì</span><span class="sxs-lookup"><span data-stu-id="574d9-272">Yes</span></span> | <span data-ttu-id="574d9-273">URI del webhook hello per hello runbook.</span><span class="sxs-lookup"><span data-stu-id="574d9-273">Uri of hello webhook for hello runbook.</span></span> |
| <span data-ttu-id="574d9-274">Expiry</span><span class="sxs-lookup"><span data-stu-id="574d9-274">Expiry</span></span> | <span data-ttu-id="574d9-275">No</span><span class="sxs-lookup"><span data-stu-id="574d9-275">No</span></span> | <span data-ttu-id="574d9-276">Data e ora in cui monitoraggio e aggiornamento hello scadenza.</span><span class="sxs-lookup"><span data-stu-id="574d9-276">Date and time that hello remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="574d9-277">Azioni webhook</span><span class="sxs-lookup"><span data-stu-id="574d9-277">Webhook actions</span></span>

<span data-ttu-id="574d9-278">Le azioni Webhook avviano un processo chiamando un URL e fornendo facoltativamente toobe un payload inviato.</span><span class="sxs-lookup"><span data-stu-id="574d9-278">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span> <span data-ttu-id="574d9-279">Sono azioni tooRemediation simili, ma sono disponibili solo per webhook che può richiamare processi diversi dai runbook di automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="574d9-279">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="574d9-280">Forniscono anche l'opzione aggiuntiva di hello di fornire un processo di payload recapitati toobe toohello remoto.</span><span class="sxs-lookup"><span data-stu-id="574d9-280">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="574d9-281">Se l'avviso chiamerà un webhook, quindi è necessario una risorsa di azione con un tipo di **Webhook** in aggiunta toohello **avviso** risorsa dell'azione.</span><span class="sxs-lookup"><span data-stu-id="574d9-281">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition toohello **Alert** action resource.</span></span>  

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

<span data-ttu-id="574d9-282">proprietà Hello per le risorse di azione Webhook sono descritte in hello le tabelle seguenti.</span><span class="sxs-lookup"><span data-stu-id="574d9-282">hello properties for Webhook action resources are described in hello following tables.</span></span>

| <span data-ttu-id="574d9-283">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="574d9-283">Element name</span></span> | <span data-ttu-id="574d9-284">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="574d9-284">Required</span></span> | <span data-ttu-id="574d9-285">Descrizione</span><span class="sxs-lookup"><span data-stu-id="574d9-285">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="574d9-286">type</span><span class="sxs-lookup"><span data-stu-id="574d9-286">type</span></span> | <span data-ttu-id="574d9-287">Sì</span><span class="sxs-lookup"><span data-stu-id="574d9-287">Yes</span></span> | <span data-ttu-id="574d9-288">Tipo di azione hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-288">Type of hello action.</span></span>  <span data-ttu-id="574d9-289">Per le azioni webhook, sarà **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="574d9-289">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="574d9-290">name</span><span class="sxs-lookup"><span data-stu-id="574d9-290">name</span></span> | <span data-ttu-id="574d9-291">Sì</span><span class="sxs-lookup"><span data-stu-id="574d9-291">Yes</span></span> | <span data-ttu-id="574d9-292">Nome visualizzato per l'azione di hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-292">Display name for hello action.</span></span>  <span data-ttu-id="574d9-293">Non è visualizzato nella console di hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-293">This is not displayed in hello console.</span></span> |
| <span data-ttu-id="574d9-294">wehookUri</span><span class="sxs-lookup"><span data-stu-id="574d9-294">wehookUri</span></span> | <span data-ttu-id="574d9-295">Sì</span><span class="sxs-lookup"><span data-stu-id="574d9-295">Yes</span></span> | <span data-ttu-id="574d9-296">URI per il webhook hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-296">Uri for hello webhook.</span></span> |
| <span data-ttu-id="574d9-297">customPayload</span><span class="sxs-lookup"><span data-stu-id="574d9-297">customPayload</span></span> | <span data-ttu-id="574d9-298">No</span><span class="sxs-lookup"><span data-stu-id="574d9-298">No</span></span> | <span data-ttu-id="574d9-299">Payload personalizzato toobe inviati toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="574d9-299">Custom payload toobe sent toohello webhook.</span></span> <span data-ttu-id="574d9-300">formato Hello dipenderà quali webhook hello è previsto.</span><span class="sxs-lookup"><span data-stu-id="574d9-300">hello format will depend on what hello webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="574d9-301">Esempio</span><span class="sxs-lookup"><span data-stu-id="574d9-301">Sample</span></span>

<span data-ttu-id="574d9-302">Ecco un esempio di una soluzione che includono che include hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="574d9-302">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="574d9-303">Ricerca salvata</span><span class="sxs-lookup"><span data-stu-id="574d9-303">Saved search</span></span>
- <span data-ttu-id="574d9-304">Pianificazione</span><span class="sxs-lookup"><span data-stu-id="574d9-304">Schedule</span></span>
- <span data-ttu-id="574d9-305">Azione di avviso</span><span class="sxs-lookup"><span data-stu-id="574d9-305">Alert action</span></span>
- <span data-ttu-id="574d9-306">Azione webhook</span><span class="sxs-lookup"><span data-stu-id="574d9-306">Webhook action</span></span>

<span data-ttu-id="574d9-307">esempio utilizza Hello [parametri soluzione standard](operations-management-suite-solutions-solution-file.md#parameters) variabili comunemente utilizzati in una soluzione come anziché valori toohardcoding nelle definizioni di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="574d9-307">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>

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
              "Description": "List of recipients for hello email alert separated by semicolon"
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


<span data-ttu-id="574d9-308">Hello seguenti il file di parametro fornisce i valori di esempi per questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="574d9-308">hello following parameter file provides samples values for this solution.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="574d9-309">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="574d9-309">Next steps</span></span>
* <span data-ttu-id="574d9-310">[Aggiungere visualizzazioni](operations-management-suite-solutions-resources-views.md) tooyour soluzione di gestione.</span><span class="sxs-lookup"><span data-stu-id="574d9-310">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="574d9-311">[Aggiungere i runbook di automazione e altre risorse](operations-management-suite-solutions-resources-automation.md) tooyour soluzione di gestione.</span><span class="sxs-lookup"><span data-stu-id="574d9-311">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>


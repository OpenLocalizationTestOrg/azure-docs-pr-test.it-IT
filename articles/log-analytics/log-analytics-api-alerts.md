---
title: API REST degli avvisi di OMS Log Analitica aaaUsing
description: Hello Log Analitica avviso REST API consente toocreate e gestire gli avvisi in Analitica di Log che fa parte di Operations Management Suite (OMS).  Questo articolo fornisce informazioni dettagliate di hello API e alcuni esempi per l'esecuzione di diverse operazioni.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="7621a-104">Creare e gestire regole di avviso in Log Analytics con l'API REST</span><span class="sxs-lookup"><span data-stu-id="7621a-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="7621a-105">Hello Log Analitica avviso REST API consente toocreate e gestire gli avvisi in Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="7621a-105">hello Log Analytics Alert REST API allows you toocreate and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="7621a-106">Questo articolo fornisce informazioni dettagliate di hello API e alcuni esempi per l'esecuzione di diverse operazioni.</span><span class="sxs-lookup"><span data-stu-id="7621a-106">This article provides details of hello API and several examples for performing different operations.</span></span>

<span data-ttu-id="7621a-107">API REST di ricerca di Log Analitica Hello è RESTful e accessibile tramite hello REST API di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="7621a-107">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager REST API.</span></span> <span data-ttu-id="7621a-108">In questo documento sono disponibili esempi in cui hello API viene usata da una riga di comando di PowerShell usando [ARMClient](https://github.com/projectkudu/ARMClient), uno strumento della riga di comando open source che semplifica la chiamata hello API di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="7621a-108">In this document you will find examples where hello API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="7621a-109">uso di Hello di ARMClient e PowerShell è una delle numerose opzioni tooaccess hello API di ricerca Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="7621a-109">hello use of ARMClient and PowerShell is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="7621a-110">Con questi strumenti è possibile utilizzare le aree di lavoro di hello API di gestione risorse di Azure RESTful toomake chiamate tooOMS ed eseguire i comandi di ricerca al loro interno.</span><span class="sxs-lookup"><span data-stu-id="7621a-110">With these tools you can utilize hello RESTful Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="7621a-111">Hello API restituiscono tooyou risultati di ricerca in formato JSON, che consente i risultati della ricerca toouse hello in molti modi diversi a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="7621a-111">hello API will output search results tooyou in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7621a-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7621a-112">Prerequisites</span></span>
<span data-ttu-id="7621a-113">Attualmente, gli avvisi possono essere creati solo con una ricerca salvata in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="7621a-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="7621a-114">È possibile fare riferimento toohello [API REST di ricerca Log](log-analytics-log-search-api.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="7621a-114">You can refer toohello [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="7621a-115">Pianificazioni</span><span class="sxs-lookup"><span data-stu-id="7621a-115">Schedules</span></span>
<span data-ttu-id="7621a-116">Una ricerca salvata può avere una o più pianificazioni.</span><span class="sxs-lookup"><span data-stu-id="7621a-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="7621a-117">Hello pianificazione definisce la frequenza con cui hello ricerca viene eseguita e viene identificato l'intervallo di tempo hello su quali criteri hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-117">hello schedule defines how often hello search is run and hello time interval over which hello criteria is identified.</span></span>
<span data-ttu-id="7621a-118">Le pianificazioni sono proprietà hello in hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="7621a-118">Schedules have hello properties in hello following table.</span></span>

| <span data-ttu-id="7621a-119">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7621a-119">Property</span></span> | <span data-ttu-id="7621a-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7621a-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7621a-121">Interval</span><span class="sxs-lookup"><span data-stu-id="7621a-121">Interval</span></span> |<span data-ttu-id="7621a-122">La frequenza con cui hello ricerca viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="7621a-122">How often hello search is run.</span></span> <span data-ttu-id="7621a-123">Il valore è espresso in minuti.</span><span class="sxs-lookup"><span data-stu-id="7621a-123">Measured in minutes.</span></span> |
| <span data-ttu-id="7621a-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="7621a-124">QueryTimeSpan</span></span> |<span data-ttu-id="7621a-125">intervallo di tempo Hello su quale hello viene valutata criteri.</span><span class="sxs-lookup"><span data-stu-id="7621a-125">hello time interval over which hello criteria is evaluated.</span></span> <span data-ttu-id="7621a-126">Deve essere maggiore di intervallo tooor uguale.</span><span class="sxs-lookup"><span data-stu-id="7621a-126">Must be equal tooor greater than Interval.</span></span> <span data-ttu-id="7621a-127">Il valore è espresso in minuti.</span><span class="sxs-lookup"><span data-stu-id="7621a-127">Measured in minutes.</span></span> |
| <span data-ttu-id="7621a-128">Versione</span><span class="sxs-lookup"><span data-stu-id="7621a-128">Version</span></span> |<span data-ttu-id="7621a-129">Hello versione API utilizzata.</span><span class="sxs-lookup"><span data-stu-id="7621a-129">hello API version being used.</span></span>  <span data-ttu-id="7621a-130">Attualmente, questo deve sempre essere impostato too1.</span><span class="sxs-lookup"><span data-stu-id="7621a-130">Currently, this should always be set too1.</span></span> |

<span data-ttu-id="7621a-131">Si consideri ad esempio una query eventi con Interval pari a 15 minuti e Timespan pari a 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="7621a-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="7621a-132">In questo caso, query hello verrebbe eseguito ogni 15 minuti e potrebbe essere generato un avviso se i criteri di hello continuassero tooresolve tootrue in un intervallo di 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="7621a-132">In this case, hello query would be run every 15 minutes, and an alert would be triggered if hello criteria continued tooresolve tootrue over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="7621a-133">Recupero delle pianificazioni</span><span class="sxs-lookup"><span data-stu-id="7621a-133">Retrieving schedules</span></span>
<span data-ttu-id="7621a-134">Hello utilizzare ottenere tooretrieve metodo tutte le pianificazioni per una ricerca salvata.</span><span class="sxs-lookup"><span data-stu-id="7621a-134">Use hello Get method tooretrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="7621a-135">Metodo con un tooretrieve ID pianificazione hello utilizzare Get una determinata pianificazione per una ricerca salvata.</span><span class="sxs-lookup"><span data-stu-id="7621a-135">Use hello Get method with a schedule ID tooretrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="7621a-136">Di seguito è riportata una risposta di esempio per una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="7621a-136">Following is a sample response for a schedule.</span></span>

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a><span data-ttu-id="7621a-137">Creazione di una pianificazione</span><span class="sxs-lookup"><span data-stu-id="7621a-137">Creating a schedule</span></span>
<span data-ttu-id="7621a-138">Utilizzare il metodo Put hello con un toocreate ID pianificazione univoca una nuova pianificazione.</span><span class="sxs-lookup"><span data-stu-id="7621a-138">Use hello Put method with a unique schedule ID toocreate a new schedule.</span></span>  <span data-ttu-id="7621a-139">Si noti che due pianificazioni non possono avere hello lo stesso ID, anche se sono associate con diverse ricerche salvate.</span><span class="sxs-lookup"><span data-stu-id="7621a-139">Note that two schedules cannot have hello same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="7621a-140">Quando si crea una pianificazione nella console OMS hello, viene creato un GUID per l'ID di pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-140">When you create a schedule in hello OMS console, a GUID is created for hello schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="7621a-141">nome Hello per le ricerche salvate tutte, pianificazioni e le azioni create con hello Log Analitica API deve essere in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="7621a-141">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="7621a-142">Modifica di una pianificazione</span><span class="sxs-lookup"><span data-stu-id="7621a-142">Editing a schedule</span></span>
<span data-ttu-id="7621a-143">Utilizzare il metodo Put hello con una pianificazione esistente ID per hello stesso salvato ricerca toomodify che pianifica.</span><span class="sxs-lookup"><span data-stu-id="7621a-143">Use hello Put method with an existing schedule ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="7621a-144">il corpo di Hello di hello richiesta deve includere hello etag della pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-144">hello body of hello request must include hello etag of hello schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="7621a-145">Eliminazione delle pianificazioni</span><span class="sxs-lookup"><span data-stu-id="7621a-145">Deleting schedules</span></span>
<span data-ttu-id="7621a-146">Utilizzare il metodo di eliminazione hello con un toodelete ID pianificazione una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="7621a-146">Use hello Delete method with a schedule ID toodelete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="7621a-147">Azioni</span><span class="sxs-lookup"><span data-stu-id="7621a-147">Actions</span></span>
<span data-ttu-id="7621a-148">Una pianificazione può avere più azioni.</span><span class="sxs-lookup"><span data-stu-id="7621a-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="7621a-149">Un'azione può definire uno o più tooperform processi, ad esempio l'invio di un messaggio di posta o l'avvio di un runbook, o è possibile definire una soglia che determina quando risultati hello di una ricerca corrispondono a certi criteri.</span><span class="sxs-lookup"><span data-stu-id="7621a-149">An action may define one or more processes tooperform such as sending a mail or starting a runbook, or it may define a threshold that determines when hello results of a search match some criteria.</span></span>  <span data-ttu-id="7621a-150">Alcune azioni verranno definiti sia in modo che i processi di hello vengono eseguiti quando viene raggiunta la soglia di hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-150">Some actions will define both so that hello processes are performed when hello threshold is met.</span></span>

<span data-ttu-id="7621a-151">Tutte le azioni sono proprietà hello in hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="7621a-151">All actions have hello properties in hello following table.</span></span>  <span data-ttu-id="7621a-152">I vari tipi di avvisi hanno diverse proprietà aggiuntive che sono descritte di seguito.</span><span class="sxs-lookup"><span data-stu-id="7621a-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="7621a-153">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7621a-153">Property</span></span> | <span data-ttu-id="7621a-154">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7621a-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7621a-155">Tipo</span><span class="sxs-lookup"><span data-stu-id="7621a-155">Type</span></span> |<span data-ttu-id="7621a-156">Tipo di azione hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-156">Type of hello action.</span></span>  <span data-ttu-id="7621a-157">I valori possibili hello non sono attualmente gli avvisi e Webhook.</span><span class="sxs-lookup"><span data-stu-id="7621a-157">Currently hello possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="7621a-158">Nome</span><span class="sxs-lookup"><span data-stu-id="7621a-158">Name</span></span> |<span data-ttu-id="7621a-159">Nome visualizzato per l'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-159">Display name for hello alert.</span></span> |
| <span data-ttu-id="7621a-160">Versione</span><span class="sxs-lookup"><span data-stu-id="7621a-160">Version</span></span> |<span data-ttu-id="7621a-161">Hello versione API utilizzata.</span><span class="sxs-lookup"><span data-stu-id="7621a-161">hello API version being used.</span></span>  <span data-ttu-id="7621a-162">Attualmente, questo deve sempre essere impostato too1.</span><span class="sxs-lookup"><span data-stu-id="7621a-162">Currently, this should always be set too1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="7621a-163">Recupero delle azioni</span><span class="sxs-lookup"><span data-stu-id="7621a-163">Retrieving actions</span></span>
<span data-ttu-id="7621a-164">Hello utilizzare ottenere tooretrieve metodo tutte le azioni per una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="7621a-164">Use hello Get method tooretrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="7621a-165">Metodo con hello azione ID tooretrieve hello utilizzare Get una determinata azione per una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="7621a-165">Use hello Get method with hello action ID tooretrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="7621a-166">Creazione o modifica di azioni</span><span class="sxs-lookup"><span data-stu-id="7621a-166">Creating or editing actions</span></span>
<span data-ttu-id="7621a-167">Utilizzare il metodo Put hello con un ID azione toohello univoco pianificazione toocreate una nuova azione.</span><span class="sxs-lookup"><span data-stu-id="7621a-167">Use hello Put method with an action ID that is unique toohello schedule toocreate a new action.</span></span>  <span data-ttu-id="7621a-168">Quando si crea un'azione nella console OMS hello, un GUID è per ID hello azione.</span><span class="sxs-lookup"><span data-stu-id="7621a-168">When you create an action in hello OMS console, a GUID is for hello action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="7621a-169">nome Hello per le ricerche salvate tutte, pianificazioni e le azioni create con hello Log Analitica API deve essere in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="7621a-169">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="7621a-170">Utilizzare il metodo Put hello con una ID per hello stesso salvato ricerca toomodify che pianifica delle azioni esistente.</span><span class="sxs-lookup"><span data-stu-id="7621a-170">Use hello Put method with an existing action ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="7621a-171">il corpo di Hello di hello richiesta deve includere hello etag della pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-171">hello body of hello request must include hello etag of hello schedule.</span></span>

<span data-ttu-id="7621a-172">formato della richiesta per la creazione di una nuova azione Hello varia in base al tipo di azione in modo da questi esempi sono forniti nelle sezioni hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-172">hello request format for creating a new action varies by action type so these examples are provided in hello sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="7621a-173">Eliminazione delle azioni</span><span class="sxs-lookup"><span data-stu-id="7621a-173">Deleting actions</span></span>
<span data-ttu-id="7621a-174">Utilizzare il metodo di eliminazione hello con hello azione ID toodelete un'azione.</span><span class="sxs-lookup"><span data-stu-id="7621a-174">Use hello Delete method with hello action ID toodelete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="7621a-175">Azioni di avviso</span><span class="sxs-lookup"><span data-stu-id="7621a-175">Alert Actions</span></span>
<span data-ttu-id="7621a-176">Una pianificazione deve avere una sola azione di avviso.</span><span class="sxs-lookup"><span data-stu-id="7621a-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="7621a-177">Azioni avviso presentano uno o più delle sezioni hello hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="7621a-177">Alert actions have one or more of hello sections in hello following table.</span></span>  <span data-ttu-id="7621a-178">Ciascuna è descritta in dettaglio di seguito.</span><span class="sxs-lookup"><span data-stu-id="7621a-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="7621a-179">Sezione</span><span class="sxs-lookup"><span data-stu-id="7621a-179">Section</span></span> | <span data-ttu-id="7621a-180">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7621a-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7621a-181">Soglia</span><span class="sxs-lookup"><span data-stu-id="7621a-181">Threshold</span></span> |<span data-ttu-id="7621a-182">Criteri di esecuzione azione hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-182">Criteria for when hello action is run.</span></span> |
| <span data-ttu-id="7621a-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="7621a-183">EmailNotification</span></span> |<span data-ttu-id="7621a-184">Inviare posta elettronica ai destinatari toomultiple.</span><span class="sxs-lookup"><span data-stu-id="7621a-184">Send mail toomultiple recipients.</span></span> |
| <span data-ttu-id="7621a-185">Correzione</span><span class="sxs-lookup"><span data-stu-id="7621a-185">Remediation</span></span> |<span data-ttu-id="7621a-186">Avvia un runbook in automazione di Azure tooattempt toocorrect identificato problema.</span><span class="sxs-lookup"><span data-stu-id="7621a-186">Start a runbook in Azure Automation tooattempt toocorrect identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="7621a-187">Soglie</span><span class="sxs-lookup"><span data-stu-id="7621a-187">Thresholds</span></span>
<span data-ttu-id="7621a-188">Un’azione di avviso deve avere una sola soglia.</span><span class="sxs-lookup"><span data-stu-id="7621a-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="7621a-189">Quando una ricerca salvata hello risultati corrispondano a soglia hello in un'azione associata con la ricerca, vengono eseguiti tutti gli altri processi in tale azione.</span><span class="sxs-lookup"><span data-stu-id="7621a-189">When hello results of a saved search match hello threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="7621a-190">Inoltre, un'azione può contenere solo una soglia, in modo da poter essere utilizzata con azioni di altri tipi che non contengono soglie.</span><span class="sxs-lookup"><span data-stu-id="7621a-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="7621a-191">Le soglie dispongono di proprietà di hello in hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="7621a-191">Thresholds have hello properties in hello following table.</span></span>

| <span data-ttu-id="7621a-192">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7621a-192">Property</span></span> | <span data-ttu-id="7621a-193">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7621a-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7621a-194">operatore</span><span class="sxs-lookup"><span data-stu-id="7621a-194">Operator</span></span> |<span data-ttu-id="7621a-195">Operatore di confronto tra le soglie hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-195">Operator for hello threshold comparison.</span></span> <br> <span data-ttu-id="7621a-196">gt = Maggiore di</span><span class="sxs-lookup"><span data-stu-id="7621a-196">gt = Greater Than</span></span> <br> <span data-ttu-id="7621a-197">lt = minore di</span><span class="sxs-lookup"><span data-stu-id="7621a-197">lt = Less Than</span></span> |
| <span data-ttu-id="7621a-198">Valore</span><span class="sxs-lookup"><span data-stu-id="7621a-198">Value</span></span> |<span data-ttu-id="7621a-199">Valore di soglia hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-199">Value for hello threshold.</span></span> |

<span data-ttu-id="7621a-200">Si consideri ad esempio una query eventi con Interval pari a 15 minuti, Timespan pari a 30 minuti e Threshold maggiore di 10.</span><span class="sxs-lookup"><span data-stu-id="7621a-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="7621a-201">In questo caso, query hello verrebbe eseguito ogni 15 minuti e potrebbe essere generato un avviso se restituito 10 eventi creati in un intervallo di 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="7621a-201">In this case, hello query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="7621a-202">Di seguito è riportata una risposta di esempio per un'azione con una sola soglia.</span><span class="sxs-lookup"><span data-stu-id="7621a-202">Following is a sample response for an action with only a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

<span data-ttu-id="7621a-203">Per una pianificazione, utilizzare il metodo Put hello con un toocreate ID azione univoci una nuova azione di soglia.</span><span class="sxs-lookup"><span data-stu-id="7621a-203">Use hello Put method with a unique action ID toocreate a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="7621a-204">Per una pianificazione, utilizzare il metodo Put hello con un toomodify di ID azione un'azione di soglia esistente.</span><span class="sxs-lookup"><span data-stu-id="7621a-204">Use hello Put method with an existing action ID toomodify a threshold action for a schedule.</span></span>  <span data-ttu-id="7621a-205">il corpo di Hello di hello richiesta deve includere hello etag dell'azione hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-205">hello body of hello request must include hello etag of hello action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="7621a-206">Notifica tramite posta elettronica</span><span class="sxs-lookup"><span data-stu-id="7621a-206">Email Notification</span></span>
<span data-ttu-id="7621a-207">Notifiche di posta elettronica inviano tooone di posta elettronica o altri destinatari.</span><span class="sxs-lookup"><span data-stu-id="7621a-207">Email Notifications send mail tooone or more recipients.</span></span>  <span data-ttu-id="7621a-208">Sono incluse proprietà hello nelle hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="7621a-208">They include hello properties in hello following table.</span></span>

| <span data-ttu-id="7621a-209">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7621a-209">Property</span></span> | <span data-ttu-id="7621a-210">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7621a-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7621a-211">Recipients</span><span class="sxs-lookup"><span data-stu-id="7621a-211">Recipients</span></span> |<span data-ttu-id="7621a-212">Elenco di indirizzi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="7621a-212">List of mail addresses.</span></span> |
| <span data-ttu-id="7621a-213">Oggetto</span><span class="sxs-lookup"><span data-stu-id="7621a-213">Subject</span></span> |<span data-ttu-id="7621a-214">oggetto Hello di posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-214">hello subject of hello mail.</span></span> |
| <span data-ttu-id="7621a-215">Attachment</span><span class="sxs-lookup"><span data-stu-id="7621a-215">Attachment</span></span> |<span data-ttu-id="7621a-216">Gli allegati non sono attualmente supportati, pertanto il valore corrispondente sarà sempre "None".</span><span class="sxs-lookup"><span data-stu-id="7621a-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="7621a-217">Di seguito è riportata una risposta di esempio per un'azione di notifica di posta elettronica con una determinata soglia.</span><span class="sxs-lookup"><span data-stu-id="7621a-217">Following is a sample response for an email notification action with a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="7621a-218">Per una pianificazione, utilizzare il metodo Put hello con un toocreate ID azione univoci una nuova azione di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="7621a-218">Use hello Put method with a unique action ID toocreate a new e-mail action for a schedule.</span></span>  <span data-ttu-id="7621a-219">Hello seguente viene creata una notifica di posta elettronica con una soglia di posta elettronica hello viene inviato quando i risultati di hello della ricerca salvata hello superano la soglia di hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-219">hello following example creates an email notification with a threshold so hello mail is sent when hello results of hello saved search exceed hello threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="7621a-220">Per una pianificazione, utilizzare il metodo Put hello con un toomodify di ID azione un'azione di posta elettronica esistente.</span><span class="sxs-lookup"><span data-stu-id="7621a-220">Use hello Put method with an existing action ID toomodify an e-mail action for a schedule.</span></span>  <span data-ttu-id="7621a-221">il corpo di Hello di hello richiesta deve includere hello etag dell'azione hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-221">hello body of hello request must include hello etag of hello action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="7621a-222">Azioni correttive</span><span class="sxs-lookup"><span data-stu-id="7621a-222">Remediation actions</span></span>
<span data-ttu-id="7621a-223">Correzioni di avviare un runbook in automazione di Azure che tenta di problema hello toocorrect identificato dall'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-223">Remediations start a runbook in Azure Automation that attempts toocorrect hello problem identified by hello alert.</span></span>  <span data-ttu-id="7621a-224">È necessario creare un webhook per runbook hello utilizzato in un'azione correttiva e quindi specificare hello URI nella proprietà WebhookUri hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-224">You must create a webhook for hello runbook used in a remediation action and then specify hello URI in hello WebhookUri property.</span></span>  <span data-ttu-id="7621a-225">Quando si crea questa azione utilizzando la console di OMS hello, viene creato automaticamente un nuovo webhook per hello runbook.</span><span class="sxs-lookup"><span data-stu-id="7621a-225">When you create this action using hello OMS console, a new webhook is automatically created for hello runbook.</span></span>

<span data-ttu-id="7621a-226">Correzioni includono le proprietà di hello in hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="7621a-226">Remediations include hello properties in hello following table.</span></span>

| <span data-ttu-id="7621a-227">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7621a-227">Property</span></span> | <span data-ttu-id="7621a-228">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7621a-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7621a-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="7621a-229">RunbookName</span></span> |<span data-ttu-id="7621a-230">Nome del runbook hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-230">Name of hello runbook.</span></span> <span data-ttu-id="7621a-231">Deve corrispondere un runbook pubblicato nell'account di automazione hello configurato nella soluzione di automazione nell'area di lavoro OMS hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-231">This must match a published runbook in hello automation account configured in hello Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="7621a-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="7621a-232">WebhookUri</span></span> |<span data-ttu-id="7621a-233">URI del webhook hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-233">URI of hello webhook.</span></span> |
| <span data-ttu-id="7621a-234">Expiry</span><span class="sxs-lookup"><span data-stu-id="7621a-234">Expiry</span></span> |<span data-ttu-id="7621a-235">Data di scadenza Hello e l'ora di hello webhook.</span><span class="sxs-lookup"><span data-stu-id="7621a-235">hello expiration date and time of hello webhook.</span></span>  <span data-ttu-id="7621a-236">Se hello webhook non dispone di una scadenza, questo può essere una data futura valida.</span><span class="sxs-lookup"><span data-stu-id="7621a-236">If hello webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="7621a-237">Di seguito è riportata una risposta di esempio per un'azione correttiva con una determinata soglia.</span><span class="sxs-lookup"><span data-stu-id="7621a-237">Following is a sample response for a remediation action with a threshold.</span></span>

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

<span data-ttu-id="7621a-238">Per una pianificazione, utilizzare il metodo Put hello con un toocreate ID azione univoci una nuova azione di correzione.</span><span class="sxs-lookup"><span data-stu-id="7621a-238">Use hello Put method with a unique action ID toocreate a new remediation action for a schedule.</span></span>  <span data-ttu-id="7621a-239">Hello seguente viene creato un monitoraggio e aggiornamento con una soglia in modo hello runbook viene avviato quando risultati hello della ricerca salvata hello superano la soglia di hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-239">hello following example creates a remediation with a threshold so hello runbook is started when hello results of hello saved search exceed hello threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="7621a-240">Per una pianificazione, utilizzare il metodo Put hello con un toomodify di ID azione un'azione correttiva esistente.</span><span class="sxs-lookup"><span data-stu-id="7621a-240">Use hello Put method with an existing action ID toomodify a remediation action for a schedule.</span></span>  <span data-ttu-id="7621a-241">il corpo di Hello di hello richiesta deve includere hello etag dell'azione hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-241">hello body of hello request must include hello etag of hello action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="7621a-242">Esempio</span><span class="sxs-lookup"><span data-stu-id="7621a-242">Example</span></span>
<span data-ttu-id="7621a-243">Di seguito è toocreate un esempio completo in un nuovo avviso di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="7621a-243">Following is a complete example toocreate a new email alert.</span></span>  <span data-ttu-id="7621a-244">Verrà creata una nuova pianificazione con un'azione contenente una soglia e un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="7621a-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a><span data-ttu-id="7621a-245">Azioni webhook</span><span class="sxs-lookup"><span data-stu-id="7621a-245">Webhook actions</span></span>
<span data-ttu-id="7621a-246">Le azioni Webhook avviano un processo chiamando un URL e fornendo facoltativamente toobe un payload inviato.</span><span class="sxs-lookup"><span data-stu-id="7621a-246">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span>  <span data-ttu-id="7621a-247">Sono azioni tooRemediation simili, ma sono disponibili solo per webhook che può richiamare processi diversi dai runbook di automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7621a-247">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="7621a-248">Forniscono anche l'opzione aggiuntiva di hello di fornire un processo di payload recapitati toobe toohello remoto.</span><span class="sxs-lookup"><span data-stu-id="7621a-248">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="7621a-249">Le azioni Webhook non dispone di una soglia, ma invece devono essere aggiunti pianificazione tooa con un'azione con una soglia di avviso.</span><span class="sxs-lookup"><span data-stu-id="7621a-249">Webhook actions do not have a threshold but instead should be added tooa schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="7621a-250">È possibile aggiungere più azioni Webhook che verranno tutti eseguite quando viene raggiunta la soglia di hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-250">You can add multiple Webhook actions that will all be run when hello threshold is met.</span></span>

<span data-ttu-id="7621a-251">Le azioni Webhook includono le proprietà di hello in hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="7621a-251">Webhook actions include hello properties in hello following table.</span></span>

| <span data-ttu-id="7621a-252">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7621a-252">Property</span></span> | <span data-ttu-id="7621a-253">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7621a-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7621a-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="7621a-254">WebhookUri</span></span> |<span data-ttu-id="7621a-255">oggetto Hello di posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-255">hello subject of hello mail.</span></span> |
| <span data-ttu-id="7621a-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="7621a-256">CustomPayload</span></span> |<span data-ttu-id="7621a-257">Payload personalizzato toobe inviati toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="7621a-257">Custom payload toobe sent toohello webhook.</span></span>  <span data-ttu-id="7621a-258">formato Hello dipenderà quali webhook hello è previsto.</span><span class="sxs-lookup"><span data-stu-id="7621a-258">hello format will depend on what hello webhook is expecting.</span></span> |

<span data-ttu-id="7621a-259">Di seguito è riportato un esempio di risposta per un’azione webhook e un'azione di avviso associata con una determinata soglia.</span><span class="sxs-lookup"><span data-stu-id="7621a-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="7621a-260">Creazione o modifica di un’azione webhook</span><span class="sxs-lookup"><span data-stu-id="7621a-260">Create or edit a webhook action</span></span>
<span data-ttu-id="7621a-261">Per una pianificazione, utilizzare il metodo Put hello con un toocreate ID azione univoci una nuova azione webhook.</span><span class="sxs-lookup"><span data-stu-id="7621a-261">Use hello Put method with a unique action ID toocreate a new webhook action for a schedule.</span></span>  <span data-ttu-id="7621a-262">Hello seguente viene creato un Webhook di azione e un avviso con una soglia in modo che webhook hello verrà attivata quando risultati hello della ricerca salvata hello superano la soglia di hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-262">hello following example creates a Webhook action and an Alert action with a threshold so that hello webhook will be triggered when hello results of hello saved search exceed hello threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="7621a-263">Per una pianificazione, utilizzare il metodo Put hello con un toomodify di ID azione un'azione webhook esistente.</span><span class="sxs-lookup"><span data-stu-id="7621a-263">Use hello Put method with an existing action ID toomodify a webhook action for a schedule.</span></span>  <span data-ttu-id="7621a-264">il corpo di Hello di hello richiesta deve includere hello etag dell'azione hello.</span><span class="sxs-lookup"><span data-stu-id="7621a-264">hello body of hello request must include hello etag of hello action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="7621a-265">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7621a-265">Next steps</span></span>
* <span data-ttu-id="7621a-266">Hello utilizzare [ricerche nei log tooperform API REST](log-analytics-log-search-api.md) nel Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="7621a-266">Use hello [REST API tooperform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>


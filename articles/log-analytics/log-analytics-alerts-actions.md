---
title: tooalerts aaaResponses in OMS Log Analitica | Documenti Microsoft
description: Gli avvisi nel registro Analitica identificare importanti informazioni nel repository OMS e in modo proattivo ricevere una notifica di problemi o richiamare azioni tooattempt toocorrect li.  In questo articolo viene descritto come toocreate una regola di avviso e azioni diverse a dettagli hello possono assumere.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d24bb726a96e7143985f111c0599dc4e7898b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-actions-tooalert-rules-in-log-analytics"></a><span data-ttu-id="88b41-104">Aggiungere regole di tooalert azioni nel registro Analitica</span><span class="sxs-lookup"><span data-stu-id="88b41-104">Add actions tooalert rules in Log Analytics</span></span>
<span data-ttu-id="88b41-105">Quando un [viene creato l'avviso nel Log Analitica](log-analytics-alerts.md), è possibile hello [configurazione regola di avviso hello](log-analytics-alerts.md) tooperform una o più azioni.</span><span class="sxs-lookup"><span data-stu-id="88b41-105">When an [alert is created in Log Analytics](log-analytics-alerts.md), you have hello option of [configuring hello alert rule](log-analytics-alerts.md) tooperform one or more actions.</span></span>  <span data-ttu-id="88b41-106">Questo articolo descrive hello diverse azioni che sono disponibili e i dettagli sulla configurazione di ogni tipo.</span><span class="sxs-lookup"><span data-stu-id="88b41-106">This article describes hello different actions that are available and details on configuring each kind.</span></span>

| <span data-ttu-id="88b41-107">Azione</span><span class="sxs-lookup"><span data-stu-id="88b41-107">Action</span></span> | <span data-ttu-id="88b41-108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="88b41-108">Description</span></span> |
|:--|:--|
| [<span data-ttu-id="88b41-109">Indirizzo di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="88b41-109">Email</span></span>](#email-actions) | <span data-ttu-id="88b41-110">Invia un messaggio di posta elettronica con i dettagli di hello di hello avviso tooone o altri destinatari.</span><span class="sxs-lookup"><span data-stu-id="88b41-110">Send an e-mail with hello details of hello alert tooone or more recipients.</span></span> |
| [<span data-ttu-id="88b41-111">Webhook</span><span class="sxs-lookup"><span data-stu-id="88b41-111">Webhook</span></span>](#webhook-actions) | <span data-ttu-id="88b41-112">Richiamare un processo esterno tramite una singola richiesta HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="88b41-112">Invoke an external process through a single HTTP POST request.</span></span> |
| [<span data-ttu-id="88b41-113">Runbook</span><span class="sxs-lookup"><span data-stu-id="88b41-113">Runbook</span></span>](#runbook-actions) | <span data-ttu-id="88b41-114">Avviare un runbook in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="88b41-114">Start a runbook in Azure Automation.</span></span> |


## <a name="email-actions"></a><span data-ttu-id="88b41-115">Azioni di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="88b41-115">Email actions</span></span>
<span data-ttu-id="88b41-116">Azioni di posta elettronica Invia messaggio di posta elettronica con i dettagli di hello di hello avviso tooone o altri destinatari.</span><span class="sxs-lookup"><span data-stu-id="88b41-116">Email actions send an e-mail with hello details of hello alert tooone or more recipients.</span></span>  <span data-ttu-id="88b41-117">È possibile specificare l'oggetto hello del messaggio di posta elettronica hello, ma il contenuto è un formato standard costruito dal Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="88b41-117">You can specify hello subject of hello mail, but it's content is a standard format constructed by Log Analytics.</span></span>  <span data-ttu-id="88b41-118">Include informazioni di riepilogo, ad esempio nome hello di avviso hello toodetails aggiunta di record tooten restituito dalla ricerca log hello.</span><span class="sxs-lookup"><span data-stu-id="88b41-118">It includes summary information such as hello name of hello alert in addition toodetails of up tooten records returned by hello log search.</span></span>  <span data-ttu-id="88b41-119">Include inoltre una ricerca di log tooa collegamento in Analitica di Log che verrà restituito l'intero set di record di hello dalla query.</span><span class="sxs-lookup"><span data-stu-id="88b41-119">It also includes a link tooa log search in Log Analytics that will return hello entire set of records from that query.</span></span>   <span data-ttu-id="88b41-120">Hello mittente del messaggio di posta elettronica hello è *Microsoft Operations Management Suite Team &lt; noreply@oms.microsoft.com &gt;* .</span><span class="sxs-lookup"><span data-stu-id="88b41-120">hello sender of hello mail is *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*.</span></span> 

<span data-ttu-id="88b41-121">Messaggio di posta elettronica azioni richiedono proprietà hello in hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="88b41-121">Email actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="88b41-122">Proprietà</span><span class="sxs-lookup"><span data-stu-id="88b41-122">Property</span></span> | <span data-ttu-id="88b41-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="88b41-123">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="88b41-124">Oggetto</span><span class="sxs-lookup"><span data-stu-id="88b41-124">Subject</span></span> |<span data-ttu-id="88b41-125">Nel messaggio di posta elettronica hello del soggetto.</span><span class="sxs-lookup"><span data-stu-id="88b41-125">Subject in hello email.</span></span>  <span data-ttu-id="88b41-126">È possibile modificare il corpo di hello del messaggio di posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="88b41-126">You cannot modify hello body of hello mail.</span></span> |
| <span data-ttu-id="88b41-127">Destinatari</span><span class="sxs-lookup"><span data-stu-id="88b41-127">Recipients</span></span> |<span data-ttu-id="88b41-128">Indirizzi di tutti i destinatari di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="88b41-128">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="88b41-129">Se si specifica più di un indirizzo, quindi gli indirizzi di hello separato con un punto e virgola (;).</span><span class="sxs-lookup"><span data-stu-id="88b41-129">If you specify more than one address, then separate hello addresses with a semicolon (;).</span></span> |


## <a name="webhook-actions"></a><span data-ttu-id="88b41-130">Azioni webhook</span><span class="sxs-lookup"><span data-stu-id="88b41-130">Webhook actions</span></span>

<span data-ttu-id="88b41-131">Le azioni Webhook consentono tooinvoke un processo esterno tramite una singola richiesta HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="88b41-131">Webhook actions allow you tooinvoke an external process through a single HTTP POST request.</span></span>  <span data-ttu-id="88b41-132">servizio Hello chiamato deve supportare webhook e determinare come verrà utilizzato alcun payload riceve.</span><span class="sxs-lookup"><span data-stu-id="88b41-132">hello service being called should support webhooks and determine how it will use any payload it receives.</span></span>  <span data-ttu-id="88b41-133">È anche possibile chiamare un'API REST che non supportano in modo specifico webhook come richiesta di hello è in un formato che hello che riconosce API.</span><span class="sxs-lookup"><span data-stu-id="88b41-133">You could also call a REST API that doesn't specifically support webhooks as long as hello request is in a format that hello API understands.</span></span>  <span data-ttu-id="88b41-134">Esempi di utilizzo di un webhook nell'avviso tooan risposta invia un messaggio [Slack](http://slack.com) o la creazione di un evento imprevisto in [PagerDuty](http://pagerduty.com/).</span><span class="sxs-lookup"><span data-stu-id="88b41-134">Examples of using a webhook in response tooan alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span></span>  <span data-ttu-id="88b41-135">Una procedura dettagliata completa di creazione di una regola di avviso con un margine di flessibilità di toocall webhook è disponibile all'indirizzo [Webhook negli avvisi di Log Analitica](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="88b41-135">A complete walkthrough of creating an alert rule with a webhook toocall Slack is available at [Webhooks in Log Analytics alerts](log-analytics-alerts-webhooks.md).</span></span>

<span data-ttu-id="88b41-136">Le azioni Webhook richiedono proprietà hello in hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="88b41-136">Webhook actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="88b41-137">Proprietà</span><span class="sxs-lookup"><span data-stu-id="88b41-137">Property</span></span> | <span data-ttu-id="88b41-138">Descrizione</span><span class="sxs-lookup"><span data-stu-id="88b41-138">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="88b41-139">URL webhook</span><span class="sxs-lookup"><span data-stu-id="88b41-139">Webhook URL</span></span> |<span data-ttu-id="88b41-140">Hello l'URL del webhook hello.</span><span class="sxs-lookup"><span data-stu-id="88b41-140">hello URL of hello webhook.</span></span> |
| <span data-ttu-id="88b41-141">Payload JSON personalizzato</span><span class="sxs-lookup"><span data-stu-id="88b41-141">Custom JSON payload</span></span> |<span data-ttu-id="88b41-142">Payload personalizzato toosend con hello webhook.</span><span class="sxs-lookup"><span data-stu-id="88b41-142">Custom payload toosend with hello webhook.</span></span>  <span data-ttu-id="88b41-143">Vedere di seguito per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="88b41-143">See below for details.</span></span> |


<span data-ttu-id="88b41-144">Un payload in formato JSON che dati hello inviato servizio esterno toohello Webhook includono un URL.</span><span class="sxs-lookup"><span data-stu-id="88b41-144">Webhooks include a URL and a payload formatted in JSON that is hello data sent toohello external service.</span></span>  <span data-ttu-id="88b41-145">Per impostazione predefinita, il payload di hello includerà i valori hello hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="88b41-145">By default, hello payload will include hello values in hello following table.</span></span>  <span data-ttu-id="88b41-146">È possibile scegliere tooreplace il payload con uno personalizzato personalizzati.</span><span class="sxs-lookup"><span data-stu-id="88b41-146">You can choose tooreplace this payload with a custom one of your own.</span></span>  <span data-ttu-id="88b41-147">In tal caso è possibile utilizzare le variabili di hello nella tabella hello per ognuna delle hello parametri tooinclude al relativo valore nel payload personalizzato.</span><span class="sxs-lookup"><span data-stu-id="88b41-147">In that case you can use hello variables in hello table for each of hello parameters tooinclude their value in your custom payload.</span></span>

| <span data-ttu-id="88b41-148">.</span><span class="sxs-lookup"><span data-stu-id="88b41-148">Parameter</span></span> | <span data-ttu-id="88b41-149">Variabile</span><span class="sxs-lookup"><span data-stu-id="88b41-149">Variable</span></span> | <span data-ttu-id="88b41-150">Descrizione</span><span class="sxs-lookup"><span data-stu-id="88b41-150">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="88b41-151">AlertRuleName</span><span class="sxs-lookup"><span data-stu-id="88b41-151">AlertRuleName</span></span> |<span data-ttu-id="88b41-152">#alertrulename</span><span class="sxs-lookup"><span data-stu-id="88b41-152">#alertrulename</span></span> |<span data-ttu-id="88b41-153">Nome della regola di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="88b41-153">Name of hello alert rule.</span></span> |
| <span data-ttu-id="88b41-154">AlertThresholdOperator</span><span class="sxs-lookup"><span data-stu-id="88b41-154">AlertThresholdOperator</span></span> |<span data-ttu-id="88b41-155">#thresholdoperator</span><span class="sxs-lookup"><span data-stu-id="88b41-155">#thresholdoperator</span></span> |<span data-ttu-id="88b41-156">Operatore di soglia per la regola di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="88b41-156">Threshold operator for hello alert rule.</span></span>  <span data-ttu-id="88b41-157">*Maggiore di* o *Minore di*.</span><span class="sxs-lookup"><span data-stu-id="88b41-157">*Greater than* or *Less than*.</span></span> |
| <span data-ttu-id="88b41-158">AlertThresholdValue</span><span class="sxs-lookup"><span data-stu-id="88b41-158">AlertThresholdValue</span></span> |<span data-ttu-id="88b41-159">#thresholdvalue</span><span class="sxs-lookup"><span data-stu-id="88b41-159">#thresholdvalue</span></span> |<span data-ttu-id="88b41-160">Valore di soglia per la regola di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="88b41-160">Threshold value for hello alert rule.</span></span> |
| <span data-ttu-id="88b41-161">LinkToSearchResults</span><span class="sxs-lookup"><span data-stu-id="88b41-161">LinkToSearchResults</span></span> |<span data-ttu-id="88b41-162">#linktosearchresults</span><span class="sxs-lookup"><span data-stu-id="88b41-162">#linktosearchresults</span></span> |<span data-ttu-id="88b41-163">Collegamento tooLog Analitica Registro ricerca che restituisce i record di hello dalla query hello hello avviso creato.</span><span class="sxs-lookup"><span data-stu-id="88b41-163">Link tooLog Analytics log search that returns hello records from hello query that created hello alert.</span></span> |
| <span data-ttu-id="88b41-164">ResultCount</span><span class="sxs-lookup"><span data-stu-id="88b41-164">ResultCount</span></span> |<span data-ttu-id="88b41-165">#searchresultcount</span><span class="sxs-lookup"><span data-stu-id="88b41-165">#searchresultcount</span></span> |<span data-ttu-id="88b41-166">Numero di record nei risultati della ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="88b41-166">Number of records in hello search results.</span></span> |
| <span data-ttu-id="88b41-167">SearchIntervalEndtimeUtc</span><span class="sxs-lookup"><span data-stu-id="88b41-167">SearchIntervalEndtimeUtc</span></span> |<span data-ttu-id="88b41-168">#searchintervalendtimeutc</span><span class="sxs-lookup"><span data-stu-id="88b41-168">#searchintervalendtimeutc</span></span> |<span data-ttu-id="88b41-169">Ora di fine per la query hello in formato UTC.</span><span class="sxs-lookup"><span data-stu-id="88b41-169">End time for hello query in UTC format.</span></span> |
| <span data-ttu-id="88b41-170">SearchIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="88b41-170">SearchIntervalInSeconds</span></span> |<span data-ttu-id="88b41-171">#searchinterval</span><span class="sxs-lookup"><span data-stu-id="88b41-171">#searchinterval</span></span> |<span data-ttu-id="88b41-172">Intervallo di tempo per la regola di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="88b41-172">Time window for hello alert rule.</span></span> |
| <span data-ttu-id="88b41-173">SearchIntervalStartTimeUtc</span><span class="sxs-lookup"><span data-stu-id="88b41-173">SearchIntervalStartTimeUtc</span></span> |<span data-ttu-id="88b41-174">#searchintervalstarttimeutc</span><span class="sxs-lookup"><span data-stu-id="88b41-174">#searchintervalstarttimeutc</span></span> |<span data-ttu-id="88b41-175">Ora di inizio per la query hello in formato UTC.</span><span class="sxs-lookup"><span data-stu-id="88b41-175">Start time for hello query in UTC format.</span></span> |
| <span data-ttu-id="88b41-176">SearchQuery</span><span class="sxs-lookup"><span data-stu-id="88b41-176">SearchQuery</span></span> |<span data-ttu-id="88b41-177">#searchquery</span><span class="sxs-lookup"><span data-stu-id="88b41-177">#searchquery</span></span> |<span data-ttu-id="88b41-178">Query di ricerca di log utilizzato dalla regola di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="88b41-178">Log search query used by hello alert rule.</span></span> |
| <span data-ttu-id="88b41-179">SearchResults</span><span class="sxs-lookup"><span data-stu-id="88b41-179">SearchResults</span></span> |<span data-ttu-id="88b41-180">Vedere di seguito</span><span class="sxs-lookup"><span data-stu-id="88b41-180">See below</span></span> |<span data-ttu-id="88b41-181">Record restituiti dalla query hello in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="88b41-181">Records returned by hello query in JSON format.</span></span>  <span data-ttu-id="88b41-182">Limitato toohello innanzitutto 5.000 record.</span><span class="sxs-lookup"><span data-stu-id="88b41-182">Limited toohello first 5,000 records.</span></span> |
| <span data-ttu-id="88b41-183">WorkspaceID</span><span class="sxs-lookup"><span data-stu-id="88b41-183">WorkspaceID</span></span> |<span data-ttu-id="88b41-184">#workspaceid</span><span class="sxs-lookup"><span data-stu-id="88b41-184">#workspaceid</span></span> |<span data-ttu-id="88b41-185">ID dell'aea di lavoro di OMS.</span><span class="sxs-lookup"><span data-stu-id="88b41-185">ID of your OMS workspace.</span></span> |

<span data-ttu-id="88b41-186">Ad esempio, è possibile specificare hello seguente payload personalizzato che include un singolo parametro chiamato *testo*.</span><span class="sxs-lookup"><span data-stu-id="88b41-186">For example, you might specify hello following custom payload that includes a single parameter called *text*.</span></span>  <span data-ttu-id="88b41-187">Questo parametro si aspetta servizio Hello che chiama questo webhook.</span><span class="sxs-lookup"><span data-stu-id="88b41-187">hello service that this webhook calls would be expecting this parameter.</span></span>

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

<span data-ttu-id="88b41-188">Il payload di esempio risolverebbe toosomething come hello seguenti quando inviato toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="88b41-188">This example payload would resolve toosomething like hello following when sent toohello webhook.</span></span>

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

<span data-ttu-id="88b41-189">risultati della ricerca tooinclude in un payload personalizzato, aggiungere hello successiva riga come proprietà di livello superiore in payload json hello.</span><span class="sxs-lookup"><span data-stu-id="88b41-189">tooinclude search results in a custom payload, add hello following line as a top level property in hello json payload.</span></span>  

    "IncludeSearchResults":true

<span data-ttu-id="88b41-190">Ad esempio, un payload personalizzato che include solo nome avviso hello e i risultati della ricerca hello toocreate, è possibile utilizzare hello seguente.</span><span class="sxs-lookup"><span data-stu-id="88b41-190">For example, toocreate a custom payload that includes just hello alert name and hello search results, you could use hello following.</span></span> 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


<span data-ttu-id="88b41-191">È possibile eseguire un esempio completo di creazione di una regola di avviso con toostart un webhook di un servizio esterno in [creare un'azione webhook avviso in OMS Log Analitica toosend messaggio tooSlack](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="88b41-191">You can walk through a complete example of creating an alert rule with a webhook toostart an external service at [Create an alert webhook action in OMS Log Analytics toosend message tooSlack](log-analytics-alerts-webhooks.md).</span></span>

## <a name="runbook-actions"></a><span data-ttu-id="88b41-192">Azioni runbook</span><span class="sxs-lookup"><span data-stu-id="88b41-192">Runbook actions</span></span>
<span data-ttu-id="88b41-193">Le azioni runbook avviano un runbook in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="88b41-193">Runbook actions start a runbook in Azure Automation.</span></span>  <span data-ttu-id="88b41-194">In ordine toouse questo tipo di azione, è necessario disporre di hello [soluzione di automazione](log-analytics-add-solutions.md) installato e configurato nell'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="88b41-194">In order toouse this type of action, you must have hello [Automation solution](log-analytics-add-solutions.md) installed and configured in your OMS workspace.</span></span>  <span data-ttu-id="88b41-195">È possibile selezionare hello runbook nell'account di automazione hello configurato nella soluzione di automazione hello.</span><span class="sxs-lookup"><span data-stu-id="88b41-195">You can select from hello runbooks in hello automation account that you configured in hello Automation solution.</span></span>

<span data-ttu-id="88b41-196">Azioni runbook richiedono proprietà hello in hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="88b41-196">Runbook actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="88b41-197">Proprietà</span><span class="sxs-lookup"><span data-stu-id="88b41-197">Property</span></span> | <span data-ttu-id="88b41-198">Descrizione</span><span class="sxs-lookup"><span data-stu-id="88b41-198">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="88b41-199">Runbook</span><span class="sxs-lookup"><span data-stu-id="88b41-199">Runbook</span></span> | <span data-ttu-id="88b41-200">Runbook che si desidera toostart quando viene creato un avviso.</span><span class="sxs-lookup"><span data-stu-id="88b41-200">Runbook that you want toostart when an alert is created.</span></span> |
| <span data-ttu-id="88b41-201">Esegui in</span><span class="sxs-lookup"><span data-stu-id="88b41-201">Run on</span></span> | <span data-ttu-id="88b41-202">Specificare **Azure** toorun hello runbook nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="88b41-202">Specify **Azure** toorun hello runbook in hello cloud.</span></span>  <span data-ttu-id="88b41-203">Specificare **worker ibrido** toorun hello runbook su un agente con [Runbook Worker ibrido](../automation/automation-hybrid-runbook-worker.md ) installato.</span><span class="sxs-lookup"><span data-stu-id="88b41-203">Specify **Hybrid worker** toorun hello runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |

<span data-ttu-id="88b41-204">Azioni runbook avviano runbook hello con un [webhook](../automation/automation-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="88b41-204">Runbook actions start hello runbook using a [webhook](../automation/automation-webhooks.md).</span></span>  <span data-ttu-id="88b41-205">Quando si crea una regola di avviso hello, verrà creato automaticamente un nuovo webhook per hello runbook con il nome di hello **OMS avviso correzione** seguito da un GUID.</span><span class="sxs-lookup"><span data-stu-id="88b41-205">When you create hello alert rule, it will automatically create a new webhook for hello runbook with hello name **OMS Alert Remediation** followed by a GUID.</span></span>  

<span data-ttu-id="88b41-206">Non è direttamente possibile popolare i parametri di runbook hello ma hello [$WebhookData parametro](../automation/automation-webhooks.md) include hello dettagli dell'avviso hello, inclusi hello risultati della ricerca log hello che li ha creati.</span><span class="sxs-lookup"><span data-stu-id="88b41-206">You cannot directly populate any parameters of hello runbook, but hello [$WebhookData parameter](../automation/automation-webhooks.md) will include hello details of hello alert, including hello results of hello log search that created it.</span></span>  <span data-ttu-id="88b41-207">runbook Hello sarà necessario toodefine **$WebhookData** come parametro per tale tooaccess hello proprietà dell'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="88b41-207">hello runbook will need toodefine **$WebhookData** as a parameter for it tooaccess hello properties of hello alert.</span></span>  <span data-ttu-id="88b41-208">Hello avviso dati sono disponibili in formato json in una singola proprietà denominata **SearchResults** in hello **RequestBody** proprietà di **$WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="88b41-208">hello alert data is available in json format in a single property called **SearchResults** in hello **RequestBody** property of **$WebhookData**.</span></span>  <span data-ttu-id="88b41-209">Questa operazione avrà le proprietà di hello in hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="88b41-209">This will have with hello properties in hello following table.</span></span>

| <span data-ttu-id="88b41-210">Nodo</span><span class="sxs-lookup"><span data-stu-id="88b41-210">Node</span></span> | <span data-ttu-id="88b41-211">Description</span><span class="sxs-lookup"><span data-stu-id="88b41-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="88b41-212">id</span><span class="sxs-lookup"><span data-stu-id="88b41-212">id</span></span> |<span data-ttu-id="88b41-213">Percorso e il GUID della ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="88b41-213">Path and GUID of hello search.</span></span> |
| <span data-ttu-id="88b41-214">__metadata</span><span class="sxs-lookup"><span data-stu-id="88b41-214">__metadata</span></span> |<span data-ttu-id="88b41-215">Informazioni su hello avviso inclusi hello numero di record e lo stato dei risultati della ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="88b41-215">Information about hello alert including hello number of records and status of hello search results.</span></span> |
| <span data-ttu-id="88b41-216">value</span><span class="sxs-lookup"><span data-stu-id="88b41-216">value</span></span> |<span data-ttu-id="88b41-217">Voce separata per ogni record nei risultati della ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="88b41-217">Separate entry for each record in hello search results.</span></span>  <span data-ttu-id="88b41-218">Dettagli Hello della voce hello corrisponderà hello proprietà e i valori del record di hello.</span><span class="sxs-lookup"><span data-stu-id="88b41-218">hello details of hello entry will match hello properties and values of hello record.</span></span> |

<span data-ttu-id="88b41-219">Ad esempio, hello runbook seguente sarebbe estrarre record hello restituiti dalla ricerca nei log hello e assegnare proprietà diverse in base al tipo di hello di ogni record.</span><span class="sxs-lookup"><span data-stu-id="88b41-219">For example, hello following runbook would extract hello records returned by hello log search  and assign different properties based on hello type of each record.</span></span>  <span data-ttu-id="88b41-220">Si noti che runbook hello viene avviato tramite la conversione **RequestBody** da json in modo che non possono essere gestiti come un oggetto in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="88b41-220">Note that hello runbook starts by converting **RequestBody** from json so that it can be worked with as an object in PowerShell.</span></span>

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a><span data-ttu-id="88b41-221">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="88b41-221">Next steps</span></span>
- <span data-ttu-id="88b41-222">Completare una procedura dettagliata per la [configurazione di un webhook](log-analytics-alerts-webhooks.md) con una regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="88b41-222">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
- <span data-ttu-id="88b41-223">Informazioni su come toowrite [i runbook in automazione di Azure](https://azure.microsoft.com/documentation/services/automation) tooremediate problemi identificati tramite gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="88b41-223">Learn how toowrite [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) tooremediate problems identified by alerts.</span></span>

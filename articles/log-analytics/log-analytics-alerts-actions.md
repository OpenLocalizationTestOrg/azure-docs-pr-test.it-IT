---
title: Risposte agli avvisi in Log Analytics di OMS | Documentazione Microsoft
description: Gli avvisi in Log Analytics identificano le informazioni importanti nel repository OMS e possono notificare i problemi all'utente in modo proattivo o richiamare le azioni per tentare di correggerle.  Questo articolo descrive come creare una regola di avviso e include i dettagli relativi alle diverse azioni che possono attivare.
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
ms.openlocfilehash: b8731e1fe48b7d809b113eb5273e3962542b8f34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-actions-to-alert-rules-in-log-analytics"></a><span data-ttu-id="a4cf4-104">Aggiungere azioni alle regole di avviso in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="a4cf4-104">Add actions to alert rules in Log Analytics</span></span>
<span data-ttu-id="a4cf4-105">Quando [viene creato un avviso in Log Analytics](log-analytics-alerts.md), è possibile scegliere di [configurare la regola di avviso](log-analytics-alerts.md) per eseguire una o più azioni.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-105">When an [alert is created in Log Analytics](log-analytics-alerts.md), you have the option of [configuring the alert rule](log-analytics-alerts.md) to perform one or more actions.</span></span>  <span data-ttu-id="a4cf4-106">Questo articolo descrive le diverse azioni disponibili e offre informazioni sulla configurazione di ogni tipologia di azione.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-106">This article describes the different actions that are available and details on configuring each kind.</span></span>

| <span data-ttu-id="a4cf4-107">Azione</span><span class="sxs-lookup"><span data-stu-id="a4cf4-107">Action</span></span> | <span data-ttu-id="a4cf4-108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4cf4-108">Description</span></span> |
|:--|:--|
| [<span data-ttu-id="a4cf4-109">Indirizzo di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="a4cf4-109">Email</span></span>](#email-actions) | <span data-ttu-id="a4cf4-110">Inviare un messaggio di posta elettronica con i dettagli dell'avviso a uno o più destinatari.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-110">Send an e-mail with the details of the alert to one or more recipients.</span></span> |
| [<span data-ttu-id="a4cf4-111">Webhook</span><span class="sxs-lookup"><span data-stu-id="a4cf4-111">Webhook</span></span>](#webhook-actions) | <span data-ttu-id="a4cf4-112">Richiamare un processo esterno tramite una singola richiesta HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-112">Invoke an external process through a single HTTP POST request.</span></span> |
| [<span data-ttu-id="a4cf4-113">Runbook</span><span class="sxs-lookup"><span data-stu-id="a4cf4-113">Runbook</span></span>](#runbook-actions) | <span data-ttu-id="a4cf4-114">Avviare un runbook in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-114">Start a runbook in Azure Automation.</span></span> |


## <a name="email-actions"></a><span data-ttu-id="a4cf4-115">Azioni di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="a4cf4-115">Email actions</span></span>
<span data-ttu-id="a4cf4-116">Le azioni di posta elettronica inviano un messaggio di posta elettronica con i dettagli dell'avviso a uno o più destinatari.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-116">Email actions send an e-mail with the details of the alert to one or more recipients.</span></span>  <span data-ttu-id="a4cf4-117">È possibile specificare l'oggetto del messaggio, ma il contenuto è un formato standard creato da Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-117">You can specify the subject of the mail, but it's content is a standard format constructed by Log Analytics.</span></span>  <span data-ttu-id="a4cf4-118">Include informazioni di riepilogo, come il nome dell'avviso, oltre ai dettagli di un massimo di dieci record restituiti dalla ricerca nei log.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-118">It includes summary information such as the name of the alert in addition to details of up to ten records returned by the log search.</span></span>  <span data-ttu-id="a4cf4-119">Include anche un collegamento a una ricerca nei log in Log Analytics che restituirà l'intero set di record dalla query.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-119">It also includes a link to a log search in Log Analytics that will return the entire set of records from that query.</span></span>   <span data-ttu-id="a4cf4-120">Il mittente del messaggio è *Team di Microsoft Operations Management Suite &lt;noreply@oms.microsoft.com&gt;*.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-120">The sender of the mail is *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*.</span></span> 

<span data-ttu-id="a4cf4-121">Le azioni di posta elettronica includono le proprietà elencate nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-121">Email actions require the properties in the following table.</span></span>

| <span data-ttu-id="a4cf4-122">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a4cf4-122">Property</span></span> | <span data-ttu-id="a4cf4-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4cf4-123">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a4cf4-124">Oggetto</span><span class="sxs-lookup"><span data-stu-id="a4cf4-124">Subject</span></span> |<span data-ttu-id="a4cf4-125">Oggetto nel messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-125">Subject in the email.</span></span>  <span data-ttu-id="a4cf4-126">È possibile modificare il corpo del messaggio.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-126">You cannot modify the body of the mail.</span></span> |
| <span data-ttu-id="a4cf4-127">Destinatari</span><span class="sxs-lookup"><span data-stu-id="a4cf4-127">Recipients</span></span> |<span data-ttu-id="a4cf4-128">Indirizzi di tutti i destinatari di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-128">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="a4cf4-129">Se si specifica più di un indirizzo, separare ognuno con un punto e virgola (;).</span><span class="sxs-lookup"><span data-stu-id="a4cf4-129">If you specify more than one address, then separate the addresses with a semicolon (;).</span></span> |


## <a name="webhook-actions"></a><span data-ttu-id="a4cf4-130">Azioni webhook</span><span class="sxs-lookup"><span data-stu-id="a4cf4-130">Webhook actions</span></span>

<span data-ttu-id="a4cf4-131">Le azioni Webhook consentono di richiamare un processo esterno tramite una singola richiesta HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-131">Webhook actions allow you to invoke an external process through a single HTTP POST request.</span></span>  <span data-ttu-id="a4cf4-132">Il servizio chiamato deve supportare i webhook e determinare come usare gli eventuali payload che riceve.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-132">The service being called should support webhooks and determine how it will use any payload it receives.</span></span>  <span data-ttu-id="a4cf4-133">È anche possibile chiamare un'API REST che non supporta in modo specifico i webhook, purché la richiesta sia in un formato l'API riconosce.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-133">You could also call a REST API that doesn't specifically support webhooks as long as the request is in a format that the API understands.</span></span>  <span data-ttu-id="a4cf4-134">Esempi di utilizzo di un webhook in risposta a un avviso sono l'invio di un messaggio in [Slack](http://slack.com) o la creazione di un evento imprevisto in [PagerDuty](http://pagerduty.com/).</span><span class="sxs-lookup"><span data-stu-id="a4cf4-134">Examples of using a webhook in response to an alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span></span>  <span data-ttu-id="a4cf4-135">Una procedura dettagliata completa della creazione di una regola di avviso con un webhook per chiamare Slack è disponibile nell'articolo relativo ai [webhook negli avvisi di Log Analytics](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="a4cf4-135">A complete walkthrough of creating an alert rule with a webhook to call Slack is available at [Webhooks in Log Analytics alerts](log-analytics-alerts-webhooks.md).</span></span>

<span data-ttu-id="a4cf4-136">Le azioni webhook includono le proprietà elencate nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-136">Webhook actions require the properties in the following table.</span></span>

| <span data-ttu-id="a4cf4-137">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a4cf4-137">Property</span></span> | <span data-ttu-id="a4cf4-138">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4cf4-138">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a4cf4-139">URL webhook</span><span class="sxs-lookup"><span data-stu-id="a4cf4-139">Webhook URL</span></span> |<span data-ttu-id="a4cf4-140">URL del webhook.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-140">The URL of the webhook.</span></span> |
| <span data-ttu-id="a4cf4-141">Payload JSON personalizzato</span><span class="sxs-lookup"><span data-stu-id="a4cf4-141">Custom JSON payload</span></span> |<span data-ttu-id="a4cf4-142">Payload personalizzato da inviare insieme al webhook.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-142">Custom payload to send with the webhook.</span></span>  <span data-ttu-id="a4cf4-143">Vedere di seguito per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-143">See below for details.</span></span> |


<span data-ttu-id="a4cf4-144">I webhook includono un URL e un payload in fermato JSON che corrisponde ai dati inviati al servizio esterno.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-144">Webhooks include a URL and a payload formatted in JSON that is the data sent to the external service.</span></span>  <span data-ttu-id="a4cf4-145">Per impostazione predefinita, il payload include i valori riportati nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-145">By default, the payload will include the values in the following table.</span></span>  <span data-ttu-id="a4cf4-146">È possibile scegliere di sostituire questo payload con un payload personalizzato.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-146">You can choose to replace this payload with a custom one of your own.</span></span>  <span data-ttu-id="a4cf4-147">In questo caso è possibile usare le variabili nella tabella per ognuno dei parametri per includerne il valore nel payload personalizzato.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-147">In that case you can use the variables in the table for each of the parameters to include their value in your custom payload.</span></span>

| <span data-ttu-id="a4cf4-148">Parametro</span><span class="sxs-lookup"><span data-stu-id="a4cf4-148">Parameter</span></span> | <span data-ttu-id="a4cf4-149">Variabile</span><span class="sxs-lookup"><span data-stu-id="a4cf4-149">Variable</span></span> | <span data-ttu-id="a4cf4-150">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4cf4-150">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a4cf4-151">AlertRuleName</span><span class="sxs-lookup"><span data-stu-id="a4cf4-151">AlertRuleName</span></span> |<span data-ttu-id="a4cf4-152">#alertrulename</span><span class="sxs-lookup"><span data-stu-id="a4cf4-152">#alertrulename</span></span> |<span data-ttu-id="a4cf4-153">Nome della regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-153">Name of the alert rule.</span></span> |
| <span data-ttu-id="a4cf4-154">AlertThresholdOperator</span><span class="sxs-lookup"><span data-stu-id="a4cf4-154">AlertThresholdOperator</span></span> |<span data-ttu-id="a4cf4-155">#thresholdoperator</span><span class="sxs-lookup"><span data-stu-id="a4cf4-155">#thresholdoperator</span></span> |<span data-ttu-id="a4cf4-156">Operatore di soglia per la regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-156">Threshold operator for the alert rule.</span></span>  <span data-ttu-id="a4cf4-157">*Maggiore di* o *Minore di*.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-157">*Greater than* or *Less than*.</span></span> |
| <span data-ttu-id="a4cf4-158">AlertThresholdValue</span><span class="sxs-lookup"><span data-stu-id="a4cf4-158">AlertThresholdValue</span></span> |<span data-ttu-id="a4cf4-159">#thresholdvalue</span><span class="sxs-lookup"><span data-stu-id="a4cf4-159">#thresholdvalue</span></span> |<span data-ttu-id="a4cf4-160">Valore di soglia per la regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-160">Threshold value for the alert rule.</span></span> |
| <span data-ttu-id="a4cf4-161">LinkToSearchResults</span><span class="sxs-lookup"><span data-stu-id="a4cf4-161">LinkToSearchResults</span></span> |<span data-ttu-id="a4cf4-162">#linktosearchresults</span><span class="sxs-lookup"><span data-stu-id="a4cf4-162">#linktosearchresults</span></span> |<span data-ttu-id="a4cf4-163">Collegamento alla ricerca nei log di Log Analytics che restituisce i record della query che ha creato l'avviso.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-163">Link to Log Analytics log search that returns the records from the query that created the alert.</span></span> |
| <span data-ttu-id="a4cf4-164">ResultCount</span><span class="sxs-lookup"><span data-stu-id="a4cf4-164">ResultCount</span></span> |<span data-ttu-id="a4cf4-165">#searchresultcount</span><span class="sxs-lookup"><span data-stu-id="a4cf4-165">#searchresultcount</span></span> |<span data-ttu-id="a4cf4-166">Numero di record nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-166">Number of records in the search results.</span></span> |
| <span data-ttu-id="a4cf4-167">SearchIntervalEndtimeUtc</span><span class="sxs-lookup"><span data-stu-id="a4cf4-167">SearchIntervalEndtimeUtc</span></span> |<span data-ttu-id="a4cf4-168">#searchintervalendtimeutc</span><span class="sxs-lookup"><span data-stu-id="a4cf4-168">#searchintervalendtimeutc</span></span> |<span data-ttu-id="a4cf4-169">Ora di fine per la query in formato UTC.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-169">End time for the query in UTC format.</span></span> |
| <span data-ttu-id="a4cf4-170">SearchIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="a4cf4-170">SearchIntervalInSeconds</span></span> |<span data-ttu-id="a4cf4-171">#searchinterval</span><span class="sxs-lookup"><span data-stu-id="a4cf4-171">#searchinterval</span></span> |<span data-ttu-id="a4cf4-172">Intervallo di tempo per la regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-172">Time window for the alert rule.</span></span> |
| <span data-ttu-id="a4cf4-173">SearchIntervalStartTimeUtc</span><span class="sxs-lookup"><span data-stu-id="a4cf4-173">SearchIntervalStartTimeUtc</span></span> |<span data-ttu-id="a4cf4-174">#searchintervalstarttimeutc</span><span class="sxs-lookup"><span data-stu-id="a4cf4-174">#searchintervalstarttimeutc</span></span> |<span data-ttu-id="a4cf4-175">Ora di inizio per la query in formato UTC.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-175">Start time for the query in UTC format.</span></span> |
| <span data-ttu-id="a4cf4-176">SearchQuery</span><span class="sxs-lookup"><span data-stu-id="a4cf4-176">SearchQuery</span></span> |<span data-ttu-id="a4cf4-177">#searchquery</span><span class="sxs-lookup"><span data-stu-id="a4cf4-177">#searchquery</span></span> |<span data-ttu-id="a4cf4-178">Query di ricerca nei log usata dalla regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-178">Log search query used by the alert rule.</span></span> |
| <span data-ttu-id="a4cf4-179">SearchResults</span><span class="sxs-lookup"><span data-stu-id="a4cf4-179">SearchResults</span></span> |<span data-ttu-id="a4cf4-180">Vedere di seguito</span><span class="sxs-lookup"><span data-stu-id="a4cf4-180">See below</span></span> |<span data-ttu-id="a4cf4-181">Record restituiti dalla query in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-181">Records returned by the query in JSON format.</span></span>  <span data-ttu-id="a4cf4-182">Limitati ai primi 5.000 record.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-182">Limited to the first 5,000 records.</span></span> |
| <span data-ttu-id="a4cf4-183">WorkspaceID</span><span class="sxs-lookup"><span data-stu-id="a4cf4-183">WorkspaceID</span></span> |<span data-ttu-id="a4cf4-184">#workspaceid</span><span class="sxs-lookup"><span data-stu-id="a4cf4-184">#workspaceid</span></span> |<span data-ttu-id="a4cf4-185">ID dell'aea di lavoro di OMS.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-185">ID of your OMS workspace.</span></span> |

<span data-ttu-id="a4cf4-186">Ad esempio, è possibile specificare il payload personalizzato seguente che include un singolo parametro denominato *text*.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-186">For example, you might specify the following custom payload that includes a single parameter called *text*.</span></span>  <span data-ttu-id="a4cf4-187">Il servizio chiamato da questo webhook si aspetta questo parametro.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-187">The service that this webhook calls would be expecting this parameter.</span></span>

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

<span data-ttu-id="a4cf4-188">Il payload di esempio viene risolto in una stringa di simile alla seguente quando viene inviato al webhook.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-188">This example payload would resolve to something like the following when sent to the webhook.</span></span>

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

<span data-ttu-id="a4cf4-189">Per includere i risultati della ricerca in un payload personalizzato, aggiungere la riga seguente come proprietà di primo livello nel payload JSON.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-189">To include search results in a custom payload, add the following line as a top level property in the json payload.</span></span>  

    "IncludeSearchResults":true

<span data-ttu-id="a4cf4-190">Ad esempio, per creare un payload personalizzato che include solo il nome dell'avviso e i risultati della ricerca, è possibile usare quanto segue.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-190">For example, to create a custom payload that includes just the alert name and the search results, you could use the following.</span></span> 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


<span data-ttu-id="a4cf4-191">Per un esempio completo di creazione di una regola di avviso con un webhook per avviare un servizio esterno, vedere l'articolo su come [creare un'azione webhook di avviso in Log Analytics di OMS per inviare messaggi a Slack](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="a4cf4-191">You can walk through a complete example of creating an alert rule with a webhook to start an external service at [Create an alert webhook action in OMS Log Analytics to send message to Slack](log-analytics-alerts-webhooks.md).</span></span>

## <a name="runbook-actions"></a><span data-ttu-id="a4cf4-192">Azioni runbook</span><span class="sxs-lookup"><span data-stu-id="a4cf4-192">Runbook actions</span></span>
<span data-ttu-id="a4cf4-193">Le azioni runbook avviano un runbook in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-193">Runbook actions start a runbook in Azure Automation.</span></span>  <span data-ttu-id="a4cf4-194">Per usare questo tipo di azione, è necessario che la [soluzione di automazione](log-analytics-add-solutions.md) sia installata e configurata nell'area di lavoro di OMS.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-194">In order to use this type of action, you must have the [Automation solution](log-analytics-add-solutions.md) installed and configured in your OMS workspace.</span></span>  <span data-ttu-id="a4cf4-195">È possibile selezionare i runbook nell'account di automazione che è stato configurato nella soluzione di automazione.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-195">You can select from the runbooks in the automation account that you configured in the Automation solution.</span></span>

<span data-ttu-id="a4cf4-196">Le azioni runbook includono le proprietà elencate nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-196">Runbook actions require the properties in the following table.</span></span>

| <span data-ttu-id="a4cf4-197">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a4cf4-197">Property</span></span> | <span data-ttu-id="a4cf4-198">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4cf4-198">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="a4cf4-199">Runbook</span><span class="sxs-lookup"><span data-stu-id="a4cf4-199">Runbook</span></span> | <span data-ttu-id="a4cf4-200">Runbook da avviare quando viene creato un avviso.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-200">Runbook that you want to start when an alert is created.</span></span> |
| <span data-ttu-id="a4cf4-201">Esegui in</span><span class="sxs-lookup"><span data-stu-id="a4cf4-201">Run on</span></span> | <span data-ttu-id="a4cf4-202">Specificare **Azure** per eseguire il runbook nel cloud.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-202">Specify **Azure** to run the runbook in the cloud.</span></span>  <span data-ttu-id="a4cf4-203">Specificare **Ruolo di lavoro ibrido** per eseguire il runbook in un agente in cui è installato un [ruolo di lavoro ibrido per runbook](../automation/automation-hybrid-runbook-worker.md ).</span><span class="sxs-lookup"><span data-stu-id="a4cf4-203">Specify **Hybrid worker** to run the runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |

<span data-ttu-id="a4cf4-204">Le azioni runbook avviano il runbook tramite un [webhook](../automation/automation-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="a4cf4-204">Runbook actions start the runbook using a [webhook](../automation/automation-webhooks.md).</span></span>  <span data-ttu-id="a4cf4-205">Quando si crea la regola di avviso, viene creato automaticamente un nuovo webhook per il runbook con il nome **OMS Alert Remediation** seguito da un GUID.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-205">When you create the alert rule, it will automatically create a new webhook for the runbook with the name **OMS Alert Remediation** followed by a GUID.</span></span>  

<span data-ttu-id="a4cf4-206">Non è possibile popolare direttamente alcun parametro del runbook, ma il [parametro $WebhookData](../automation/automation-webhooks.md) includerà i dettagli dell'avviso, inclusi i risultati della ricerca nei log che lo ha creato.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-206">You cannot directly populate any parameters of the runbook, but the [$WebhookData parameter](../automation/automation-webhooks.md) will include the details of the alert, including the results of the log search that created it.</span></span>  <span data-ttu-id="a4cf4-207">Il runbook dovrà definire **$WebhookData** come parametro per consentire l'accesso alle proprietà dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-207">The runbook will need to define **$WebhookData** as a parameter for it to access the properties of the alert.</span></span>  <span data-ttu-id="a4cf4-208">I dati dell'avviso sono disponibili in formato JSON in una singola proprietà denominata **SearchResults** nella proprietà **RequestBody** di **$WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-208">The alert data is available in json format in a single property called **SearchResults** in the **RequestBody** property of **$WebhookData**.</span></span>  <span data-ttu-id="a4cf4-209">Saranno incluse le proprietà riportate nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-209">This will have with the properties in the following table.</span></span>

| <span data-ttu-id="a4cf4-210">Nodo</span><span class="sxs-lookup"><span data-stu-id="a4cf4-210">Node</span></span> | <span data-ttu-id="a4cf4-211">Description</span><span class="sxs-lookup"><span data-stu-id="a4cf4-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a4cf4-212">id</span><span class="sxs-lookup"><span data-stu-id="a4cf4-212">id</span></span> |<span data-ttu-id="a4cf4-213">Percorso e GUID della ricerca.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-213">Path and GUID of the search.</span></span> |
| <span data-ttu-id="a4cf4-214">__metadata</span><span class="sxs-lookup"><span data-stu-id="a4cf4-214">__metadata</span></span> |<span data-ttu-id="a4cf4-215">Informazioni sull'avviso, inclusi il numero di record e lo stato dei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-215">Information about the alert including the number of records and status of the search results.</span></span> |
| <span data-ttu-id="a4cf4-216">value</span><span class="sxs-lookup"><span data-stu-id="a4cf4-216">value</span></span> |<span data-ttu-id="a4cf4-217">Voce separata per ogni record nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-217">Separate entry for each record in the search results.</span></span>  <span data-ttu-id="a4cf4-218">I dettagli della voce corrisponderanno alle proprietà e ai valori del record.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-218">The details of the entry will match the properties and values of the record.</span></span> |

<span data-ttu-id="a4cf4-219">Ad esempio, il runbook seguente estrae i record restituiti dalla ricerca nel log e assegna proprietà diverse in base al tipo di ogni record.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-219">For example, the following runbook would extract the records returned by the log search  and assign different properties based on the type of each record.</span></span>  <span data-ttu-id="a4cf4-220">Si noti che il runbook converte prima di tutto **RequestBody** da JSON, in modo che possa essere usato come oggetto in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-220">Note that the runbook starts by converting **RequestBody** from json so that it can be worked with as an object in PowerShell.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="a4cf4-221">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4cf4-221">Next steps</span></span>
- <span data-ttu-id="a4cf4-222">Completare una procedura dettagliata per la [configurazione di un webhook](log-analytics-alerts-webhooks.md) con una regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-222">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
- <span data-ttu-id="a4cf4-223">Informazioni su come scrivere [runbook in Automazione di Azure](https://azure.microsoft.com/documentation/services/automation) per la risoluzione dei problemi identificati dagli avvisi.</span><span class="sxs-lookup"><span data-stu-id="a4cf4-223">Learn how to write [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) to remediate problems identified by alerts.</span></span>
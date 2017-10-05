---
title: Esempio di azione di allarme webhook in Log Analytics di OMS | Documentazione Microsoft
description: "Una delle azioni che è possibile eseguire in risposta a un avviso di Log Analytics è la creazione di un *webhook*, che consente di richiamare un processo esterno tramite una singola richiesta HTTP. Questo articolo illustra un esempio di creazione di un'azione webhook in un avviso di Log Analytics tramite Slack."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 13c39f0f-fd3c-472d-8324-ddf7538be45e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: bwren
ms.openlocfilehash: 55b66132f7ec5c26c0a7cac1ec0a5c403dbd1082
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-to-send-message-to-slack"></a><span data-ttu-id="7713b-104">Creare un'azione di avviso webhook in Log Analytics di OMS per inviare messaggi a Slack</span><span class="sxs-lookup"><span data-stu-id="7713b-104">Create an alert webhook action in OMS Log Analytics to send message to Slack</span></span>
<span data-ttu-id="7713b-105">Una delle azioni che è possibile eseguire in risposta a un [avviso di Log Analytics](log-analytics-alerts.md) è la creazione di un *webhook*, che consente di richiamare un processo esterno tramite una singola richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="7713b-105">One of the actions you can run in response to a [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you to invoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="7713b-106">Per informazioni dettagliate su avvisi e webhook, vedere [Avvisi in Log Analytics](log-analytics-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="7713b-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="7713b-107">Questo articolo illustra un esempio di creazione di un'azione webhook in un avviso di Log Analytics tramite il servizio di messaggistica Slack.</span><span class="sxs-lookup"><span data-stu-id="7713b-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="7713b-108">Per completare l'esempio è necessario disporre di un account Slack.</span><span class="sxs-lookup"><span data-stu-id="7713b-108">You must have a Slack account to complete this sample.</span></span>  <span data-ttu-id="7713b-109">È possibile iscriversi per ottenere un account gratuito nel sito Web [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="7713b-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="7713b-110">Passaggio 1: Abilitare gli webhook in Slack</span><span class="sxs-lookup"><span data-stu-id="7713b-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="7713b-111">Accedere al sito Web Slack all'indirizzo [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="7713b-111">Sign in to Slack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="7713b-112">Selezionare un canale nella sezione **Channels** (Canali) del riquadro a sinistra,</span><span class="sxs-lookup"><span data-stu-id="7713b-112">Select a channel in the **Channels** section in the left pane.</span></span>  <span data-ttu-id="7713b-113">che costituirà il canale a cui verrà inviato il messaggio.</span><span class="sxs-lookup"><span data-stu-id="7713b-113">This is the channel that the message will be sent to.</span></span>  <span data-ttu-id="7713b-114">È possibile selezionare uno dei canali predefiniti, ad esempio **general** o **random**.</span><span class="sxs-lookup"><span data-stu-id="7713b-114">You can select one of the default channels such as **general** or **random**.</span></span>  <span data-ttu-id="7713b-115">In uno scenario di produzione sarà probabilmente necessario creare un canale speciale, ad esempio **criticalservicealerts**.</span><span class="sxs-lookup"><span data-stu-id="7713b-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Canali Slack](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="7713b-117">Fare clic su **Add an app or custom integration** (Aggiungi un'app o l'integrazione personalizzata) per aprire la directory dell'app.</span><span class="sxs-lookup"><span data-stu-id="7713b-117">Click **Add an app or custom integration** to open the App Directory.</span></span>
4. <span data-ttu-id="7713b-118">Digitare *webhooks* nella casella di ricerca e quindi selezionare **Incoming WebHooks**(Webhook in ingresso).</span><span class="sxs-lookup"><span data-stu-id="7713b-118">Type *webhooks* into the search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Canali Slack](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="7713b-120">Fare clic su **Install** (Installa) vicino al nome del proprio team.</span><span class="sxs-lookup"><span data-stu-id="7713b-120">Click **Install** next to your team name.</span></span>
6. <span data-ttu-id="7713b-121">Fare clic su **Add Configuration**(Aggiungi configurazione).</span><span class="sxs-lookup"><span data-stu-id="7713b-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="7713b-122">Selezionare il canale che si intende usare in questo esempio e quindi fare clic su **Add Incoming WebHooks integration**(Aggiungi integrazione webhook in ingresso).</span><span class="sxs-lookup"><span data-stu-id="7713b-122">Select the the channel that you're going to use for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="7713b-123">Copiare l'indirizzo contenuto in **Webhook URL** (URL webhook),</span><span class="sxs-lookup"><span data-stu-id="7713b-123">Copy the **Webhook URL**.</span></span>  <span data-ttu-id="7713b-124">che dovrà essere incollato nella configurazione dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="7713b-124">You'll be pasting this into the Alert configuration.</span></span> <br>
   
    ![Canali Slack](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="7713b-126">Passaggio 2: Creare una regola di avviso in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="7713b-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="7713b-127">[Creare una regola di avviso](log-analytics-alerts.md) con le impostazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="7713b-127">[Create an alert rule](log-analytics-alerts.md) with the following settings.</span></span>
   * <span data-ttu-id="7713b-128">Query: ```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="7713b-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="7713b-129">Check for this alert every: 5 minutes (Verifica la presenza di questo avviso ogni: 5 minuti)</span><span class="sxs-lookup"><span data-stu-id="7713b-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="7713b-130">The number of results is: greater than 10 (Il numero di risultati è: maggiore di 10)</span><span class="sxs-lookup"><span data-stu-id="7713b-130">The number of results is: greater than 10</span></span>
   * <span data-ttu-id="7713b-131">Over this time window: 60 minutes (Finestra temporale: 60 minuti)</span><span class="sxs-lookup"><span data-stu-id="7713b-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="7713b-132">Selezionare **Yes** (Sì) per **Webhook** e **No** per le altre azioni.</span><span class="sxs-lookup"><span data-stu-id="7713b-132">Select **Yes** for **Webhook** and **No** for the other actions.</span></span>
2. <span data-ttu-id="7713b-133">Incollare l'URL del sito Slack nel campo **Webhook URL** (URL webhook).</span><span class="sxs-lookup"><span data-stu-id="7713b-133">Paste the Slack URL into the **Webhook URL** field.</span></span>
3. <span data-ttu-id="7713b-134">Selezionare l'opzione che consente di **includere un payload JSON personalizzato**.</span><span class="sxs-lookup"><span data-stu-id="7713b-134">Select the option to **include a custom JSON payload**.</span></span>
4. <span data-ttu-id="7713b-135">Slack prevede un payload in formato JSON con un parametro denominato *text*.</span><span class="sxs-lookup"><span data-stu-id="7713b-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="7713b-136">che costituisce il testo visualizzato nel messaggio che verrà creato.</span><span class="sxs-lookup"><span data-stu-id="7713b-136">This is the text that it will display in the message it creates.</span></span>  <span data-ttu-id="7713b-137">Usando il simbolo *#* è possibile includere più di un parametro di avviso.</span><span class="sxs-lookup"><span data-stu-id="7713b-137">You can use one or more of the alert parameters using the *#* symbol such as in the following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds the over threshold of #thresholdvalue ."
    }
    ```
   
    ![payload JSON di esempio](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="7713b-139">Fare clic su **Save** (Salva) per salvare la regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="7713b-139">Click **Save** to save the alert rule.</span></span>
6. <span data-ttu-id="7713b-140">Attendere il tempo necessario alla creazione dell'avviso. In Slack apparirà un messaggio simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="7713b-140">Wait sufficient time for an alert to be created and then check Slack for a message which will be similar to the following.</span></span>
   
   ![webhook di esempio in Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="7713b-142">Payload di un webhook avanzato per Slack</span><span class="sxs-lookup"><span data-stu-id="7713b-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="7713b-143">Con Slack è possibile personalizzare in maniera significativa i messaggi in ingresso.</span><span class="sxs-lookup"><span data-stu-id="7713b-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="7713b-144">Per altre informazioni, vedere la sezione [Incoming Webhooks](https://api.slack.com/incoming-webhooks) (Webhook in ingresso) del sito Web Slack.</span><span class="sxs-lookup"><span data-stu-id="7713b-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on the Slack website.</span></span> <span data-ttu-id="7713b-145">Di seguito è riportato un payload complesso che consente la creazione di un messaggio avanzato con formattazione:</span><span class="sxs-lookup"><span data-stu-id="7713b-145">Following is a more complex payload to create a rich message with formatting:</span></span>

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link To SearchResults",
                        "value": "<#linktosearchresults|OMS Search Results>"},
                    {
                        "title": "Search Interval",
                        "value": "#searchinterval"},
                    {
                        "title": "Threshold Operator",
                        "value": "#thresholdoperator"},
                    {
                        "title": "Threshold Value",
                        "value": "#thresholdvalue"}
                ],
                "color": "#F35A00"
            }
        ]
    }


<span data-ttu-id="7713b-146">In Slack viene visualizzato un messaggio simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="7713b-146">This would generate a message in Slack similar to the following.</span></span>

![messaggio di esempio in Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="7713b-148">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="7713b-148">Summary</span></span>
<span data-ttu-id="7713b-149">Con l'attivazione di questa regola, ogni volta che vengono soddisfatti determinati criteri viene inviato un messaggio a Slack.</span><span class="sxs-lookup"><span data-stu-id="7713b-149">With this alert rule in place, you would have a message sent to Slack every time the criteria is met.</span></span>  

<span data-ttu-id="7713b-150">Questo è solo un esempio delle varie azioni che è possibile creare in risposta a un avviso.</span><span class="sxs-lookup"><span data-stu-id="7713b-150">This is only one example of an action that you can create in response to an alert.</span></span>  <span data-ttu-id="7713b-151">È possibile ad esempio creare un'azione webhook per chiamare un altro servizio esterno, un'azione runbook per avviare un runbook in Automazione di Azure o un'azione di posta elettronica per inviare un messaggio di posta a se stessi o ad altri destinatari.</span><span class="sxs-lookup"><span data-stu-id="7713b-151">You could create a webhook action that calls another external service, a runbook action to start a runbook in Azure Automation, or an email action to send a mail to yourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="7713b-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7713b-152">Next Steps</span></span>
* <span data-ttu-id="7713b-153">Altre informazioni sulle [azioni di avviso in Log Analytics](log-analytics-alerts-actions.md) e su altre azioni.</span><span class="sxs-lookup"><span data-stu-id="7713b-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>



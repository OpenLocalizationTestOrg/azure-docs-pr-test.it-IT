---
title: esempio di azione di allarme aaaWebhook in OMS Log Analitica | Documenti Microsoft
description: "Una delle azioni di hello è possibile eseguire in risposta tooa Log Analitica avviso è un * webhook *, che consente di tooinvoke un processo esterno tramite una singola richiesta HTTP. Questo articolo illustra un esempio di creazione di un'azione webhook in un avviso di Log Analytics tramite Slack."
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
ms.openlocfilehash: e60bdc4922347073d572c2e4719461b13e8e7d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a><span data-ttu-id="42bf5-104">Creare un'azione webhook avviso in OMS Log Analitica toosend messaggio tooSlack</span><span class="sxs-lookup"><span data-stu-id="42bf5-104">Create an alert webhook action in OMS Log Analytics toosend message tooSlack</span></span>
<span data-ttu-id="42bf5-105">Una delle azioni di hello è possibile eseguire in risposta tooa [avviso Analitica Log](log-analytics-alerts.md) è un *webhook*, che consente di tooinvoke un processo esterno tramite una singola richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="42bf5-105">One of hello actions you can run in response tooa [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you tooinvoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="42bf5-106">Per informazioni dettagliate su avvisi e webhook, vedere [Avvisi in Log Analytics](log-analytics-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="42bf5-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="42bf5-107">Questo articolo illustra un esempio di creazione di un'azione webhook in un avviso di Log Analytics tramite il servizio di messaggistica Slack.</span><span class="sxs-lookup"><span data-stu-id="42bf5-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="42bf5-108">È necessario un account Slack di toocomplete in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="42bf5-108">You must have a Slack account toocomplete this sample.</span></span>  <span data-ttu-id="42bf5-109">È possibile iscriversi per ottenere un account gratuito nel sito Web [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="42bf5-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="42bf5-110">Passaggio 1: Abilitare gli webhook in Slack</span><span class="sxs-lookup"><span data-stu-id="42bf5-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="42bf5-111">Accedi tooSlack in [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="42bf5-111">Sign in tooSlack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="42bf5-112">Selezionare un canale in hello **canali** sezione nel riquadro di sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="42bf5-112">Select a channel in hello **Channels** section in hello left pane.</span></span>  <span data-ttu-id="42bf5-113">Questo è il canale hello verrà inviato al messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="42bf5-113">This is hello channel that hello message will be sent to.</span></span>  <span data-ttu-id="42bf5-114">È possibile selezionare uno dei canali di hello predefinito, ad esempio **generale** o **casuale**.</span><span class="sxs-lookup"><span data-stu-id="42bf5-114">You can select one of hello default channels such as **general** or **random**.</span></span>  <span data-ttu-id="42bf5-115">In uno scenario di produzione sarà probabilmente necessario creare un canale speciale, ad esempio **criticalservicealerts**.</span><span class="sxs-lookup"><span data-stu-id="42bf5-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Canali Slack](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="42bf5-117">Fare clic su **aggiungere un'applicazione o integrazione personalizzati** tooopen hello Directory dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="42bf5-117">Click **Add an app or custom integration** tooopen hello App Directory.</span></span>
4. <span data-ttu-id="42bf5-118">Tipo *webhook* nella casella di ricerca hello e quindi selezionare **Webhook in ingresso**.</span><span class="sxs-lookup"><span data-stu-id="42bf5-118">Type *webhooks* into hello search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Canali Slack](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="42bf5-120">Fare clic su **installare** nome del team tooyour successivo.</span><span class="sxs-lookup"><span data-stu-id="42bf5-120">Click **Install** next tooyour team name.</span></span>
6. <span data-ttu-id="42bf5-121">Fare clic su **Add Configuration**(Aggiungi configurazione).</span><span class="sxs-lookup"><span data-stu-id="42bf5-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="42bf5-122">Canale di hello hello selezionare archivieranno toouse per questo esempio e quindi fare clic su **integrazione aggiungere Webhook in ingresso**.</span><span class="sxs-lookup"><span data-stu-id="42bf5-122">Select hello hello channel that you're going toouse for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="42bf5-123">Hello copia **URL del Webhook**.</span><span class="sxs-lookup"><span data-stu-id="42bf5-123">Copy hello **Webhook URL**.</span></span>  <span data-ttu-id="42bf5-124">Si sarà incollare questa in configurazione dell'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="42bf5-124">You'll be pasting this into hello Alert configuration.</span></span> <br>
   
    ![Canali Slack](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="42bf5-126">Passaggio 2: Creare una regola di avviso in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="42bf5-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="42bf5-127">[Creare una regola di avviso](log-analytics-alerts.md) con hello seguenti impostazioni.</span><span class="sxs-lookup"><span data-stu-id="42bf5-127">[Create an alert rule](log-analytics-alerts.md) with hello following settings.</span></span>
   * <span data-ttu-id="42bf5-128">Query: ```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="42bf5-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="42bf5-129">Check for this alert every: 5 minutes (Verifica la presenza di questo avviso ogni: 5 minuti)</span><span class="sxs-lookup"><span data-stu-id="42bf5-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="42bf5-130">numero di risultati di Hello: maggiore di 10</span><span class="sxs-lookup"><span data-stu-id="42bf5-130">hello number of results is: greater than 10</span></span>
   * <span data-ttu-id="42bf5-131">Over this time window: 60 minutes (Finestra temporale: 60 minuti)</span><span class="sxs-lookup"><span data-stu-id="42bf5-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="42bf5-132">Selezionare **Sì** per **Webhook** e **n** per hello altre azioni.</span><span class="sxs-lookup"><span data-stu-id="42bf5-132">Select **Yes** for **Webhook** and **No** for hello other actions.</span></span>
2. <span data-ttu-id="42bf5-133">Hello Incolla Slack URL in hello **URL del Webhook** campo.</span><span class="sxs-lookup"><span data-stu-id="42bf5-133">Paste hello Slack URL into hello **Webhook URL** field.</span></span>
3. <span data-ttu-id="42bf5-134">L'opzione hello troppo**includono un payload JSON personalizzato**.</span><span class="sxs-lookup"><span data-stu-id="42bf5-134">Select hello option too**include a custom JSON payload**.</span></span>
4. <span data-ttu-id="42bf5-135">Slack prevede un payload in formato JSON con un parametro denominato *text*.</span><span class="sxs-lookup"><span data-stu-id="42bf5-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="42bf5-136">Questo è il testo hello che verrà visualizzato il messaggio hello che viene creato.</span><span class="sxs-lookup"><span data-stu-id="42bf5-136">This is hello text that it will display in hello message it creates.</span></span>  <span data-ttu-id="42bf5-137">È possibile utilizzare uno o più parametri di avviso hello utilizzando hello  *#*  tale simbolo come hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="42bf5-137">You can use one or more of hello alert parameters using hello *#* symbol such as in hello following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![payload JSON di esempio](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="42bf5-139">Fare clic su **salvare** toosave regola di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="42bf5-139">Click **Save** toosave hello alert rule.</span></span>
6. <span data-ttu-id="42bf5-140">Attendere un tempo sufficiente per un avviso toobe creato e quindi controllare il margine di flessibilità di un messaggio che sarà simile toohello seguente.</span><span class="sxs-lookup"><span data-stu-id="42bf5-140">Wait sufficient time for an alert toobe created and then check Slack for a message which will be similar toohello following.</span></span>
   
   ![webhook di esempio in Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="42bf5-142">Payload di un webhook avanzato per Slack</span><span class="sxs-lookup"><span data-stu-id="42bf5-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="42bf5-143">Con Slack è possibile personalizzare in maniera significativa i messaggi in ingresso.</span><span class="sxs-lookup"><span data-stu-id="42bf5-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="42bf5-144">Per ulteriori informazioni, vedere [Webhook in ingresso](https://api.slack.com/incoming-webhooks) nel sito Web di Slack hello.</span><span class="sxs-lookup"><span data-stu-id="42bf5-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on hello Slack website.</span></span> <span data-ttu-id="42bf5-145">Di seguito è un toocreate payload più complessa di un messaggio con la formattazione RTF:</span><span class="sxs-lookup"><span data-stu-id="42bf5-145">Following is a more complex payload toocreate a rich message with formatting:</span></span>

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link tooSearchResults",
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


<span data-ttu-id="42bf5-146">Questo genera un messaggio di margine di flessibilità seguenti toohello simile.</span><span class="sxs-lookup"><span data-stu-id="42bf5-146">This would generate a message in Slack similar toohello following.</span></span>

![messaggio di esempio in Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="42bf5-148">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="42bf5-148">Summary</span></span>
<span data-ttu-id="42bf5-149">Con questa regola di avviso, è necessario tooSlack un messaggio inviato ogni volta che viene soddisfatto il criterio di hello.</span><span class="sxs-lookup"><span data-stu-id="42bf5-149">With this alert rule in place, you would have a message sent tooSlack every time hello criteria is met.</span></span>  

<span data-ttu-id="42bf5-150">Questo è solo un esempio di un'azione che è possibile creare nell'avviso tooan di risposta.</span><span class="sxs-lookup"><span data-stu-id="42bf5-150">This is only one example of an action that you can create in response tooan alert.</span></span>  <span data-ttu-id="42bf5-151">È possibile creare un'azione webhook che chiama un runbook in automazione di Azure o un toosend di azione del messaggio di posta elettronica di un altro servizio esterno, un toostart azione runbook un tooyourself di posta elettronica o altri destinatari.</span><span class="sxs-lookup"><span data-stu-id="42bf5-151">You could create a webhook action that calls another external service, a runbook action toostart a runbook in Azure Automation, or an email action toosend a mail tooyourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="42bf5-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="42bf5-152">Next Steps</span></span>
* <span data-ttu-id="42bf5-153">Altre informazioni sulle [azioni di avviso in Log Analytics](log-analytics-alerts-actions.md) e su altre azioni.</span><span class="sxs-lookup"><span data-stu-id="42bf5-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>



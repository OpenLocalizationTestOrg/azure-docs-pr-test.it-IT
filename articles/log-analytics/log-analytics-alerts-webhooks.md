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
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a>Creare un'azione webhook avviso in OMS Log Analitica toosend messaggio tooSlack
Una delle azioni di hello è possibile eseguire in risposta tooa [avviso Analitica Log](log-analytics-alerts.md) è un *webhook*, che consente di tooinvoke un processo esterno tramite una singola richiesta HTTP.  Per informazioni dettagliate su avvisi e webhook, vedere [Avvisi in Log Analytics](log-analytics-alerts.md)

Questo articolo illustra un esempio di creazione di un'azione webhook in un avviso di Log Analytics tramite il servizio di messaggistica Slack.

> [!NOTE]
> È necessario un account Slack di toocomplete in questo esempio.  È possibile iscriversi per ottenere un account gratuito nel sito Web [slack.com](http://slack.com).
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a>Passaggio 1: Abilitare gli webhook in Slack
1. Accedi tooSlack in [slack.com](http://slack.com).
2. Selezionare un canale in hello **canali** sezione nel riquadro di sinistra hello.  Questo è il canale hello verrà inviato al messaggio hello.  È possibile selezionare uno dei canali di hello predefinito, ad esempio **generale** o **casuale**.  In uno scenario di produzione sarà probabilmente necessario creare un canale speciale, ad esempio **criticalservicealerts**. <br>
   
   ![Canali Slack](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. Fare clic su **aggiungere un'applicazione o integrazione personalizzati** tooopen hello Directory dell'applicazione.
4. Tipo *webhook* nella casella di ricerca hello e quindi selezionare **Webhook in ingresso**. <br>
   
   ![Canali Slack](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. Fare clic su **installare** nome del team tooyour successivo.
6. Fare clic su **Add Configuration**(Aggiungi configurazione).
7. Canale di hello hello selezionare archivieranno toouse per questo esempio e quindi fare clic su **integrazione aggiungere Webhook in ingresso**.  
8. Hello copia **URL del Webhook**.  Si sarà incollare questa in configurazione dell'avviso hello. <br>
   
    ![Canali Slack](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a>Passaggio 2: Creare una regola di avviso in Log Analytics
1. [Creare una regola di avviso](log-analytics-alerts.md) con hello seguenti impostazioni.
   * Query: ```    Type=Event EventLevelName=error ```
   * Check for this alert every: 5 minutes (Verifica la presenza di questo avviso ogni: 5 minuti)
   * numero di risultati di Hello: maggiore di 10
   * Over this time window: 60 minutes (Finestra temporale: 60 minuti)
   * Selezionare **Sì** per **Webhook** e **n** per hello altre azioni.
2. Hello Incolla Slack URL in hello **URL del Webhook** campo.
3. L'opzione hello troppo**includono un payload JSON personalizzato**.
4. Slack prevede un payload in formato JSON con un parametro denominato *text*.  Questo è il testo hello che verrà visualizzato il messaggio hello che viene creato.  È possibile utilizzare uno o più parametri di avviso hello utilizzando hello  *#*  tale simbolo come hello di esempio seguente.
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![payload JSON di esempio](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. Fare clic su **salvare** toosave regola di avviso hello.
6. Attendere un tempo sufficiente per un avviso toobe creato e quindi controllare il margine di flessibilità di un messaggio che sarà simile toohello seguente.
   
   ![webhook di esempio in Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a>Payload di un webhook avanzato per Slack
Con Slack è possibile personalizzare in maniera significativa i messaggi in ingresso. Per ulteriori informazioni, vedere [Webhook in ingresso](https://api.slack.com/incoming-webhooks) nel sito Web di Slack hello. Di seguito è un toocreate payload più complessa di un messaggio con la formattazione RTF:

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


Questo genera un messaggio di margine di flessibilità seguenti toohello simile.

![messaggio di esempio in Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a>Riepilogo
Con questa regola di avviso, è necessario tooSlack un messaggio inviato ogni volta che viene soddisfatto il criterio di hello.  

Questo è solo un esempio di un'azione che è possibile creare nell'avviso tooan di risposta.  È possibile creare un'azione webhook che chiama un runbook in automazione di Azure o un toosend di azione del messaggio di posta elettronica di un altro servizio esterno, un toostart azione runbook un tooyourself di posta elettronica o altri destinatari.   

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni sulle [azioni di avviso in Log Analytics](log-analytics-alerts-actions.md) e su altre azioni.



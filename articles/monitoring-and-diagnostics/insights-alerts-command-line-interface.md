---
title: gli avvisi aaaCreate per servizi di Azure - CLI multipiattaforma | Documenti Microsoft
description: Attivare l'automazione, notifiche, gli URL di siti Web di chiamata (webhook) o messaggi di posta elettronica quando vengono soddisfatte le condizioni di hello specificate.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a>Creare avvisi sulle metriche in Monitoraggio di Azure per i servizi di Azure - Interfaccia della riga di comando multipiattaforma
> [!div class="op_single_selector"]
> * [Portale](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Panoramica
Questo articolo illustra come tooset di Azure avvisi metrica utilizzando hello multipiattaforma interfaccia della riga di comando (CLI).

> [!NOTE]
> Monitoraggio di Azure è hello nuovo nome per ciò che è stato chiamato "Azure Insights" fino a 25 settembre 2016. Tuttavia, gli spazi dei nomi hello e pertanto comandi hello seguenti comunque contengono approfondite"hello".
>
>

È possibile ricevere avvisi basati su metriche di monitoraggio o eventi nei servizi Azure.

* **Valori della metrica** : hello trigger un avviso quando il valore di hello di una specifica metrica supera una soglia è assegnare in entrambe le direzioni. Ovvero, entrambi attiva quando hello prima condizione e quindi successivamente non condizione when che è non è più in grado di soddisfare.    
* **Eventi del log attività**: è possibile attivare un avviso per *ogni* evento o solo quando si verifica un determinato evento. ulteriori informazioni sugli avvisi di log attività toolearn [fare clic qui](monitoring-activity-log-alerts.md)

È possibile configurare una metrica toodo avviso hello seguenti attiva:

* inviare coamministratore e amministratore del servizio toohello le notifiche tramite posta elettronica
* Invia messaggio di posta elettronica tooadditional messaggi di posta elettronica specificato.
* chiamare un webhook
* avviare l'esecuzione di un runbook di Azure (solo dal portale di Azure in questo momento hello)

È possibile configurare e ottenere informazioni sulle regole degli avvisi sulle metriche tramite

* [Portale di Azure](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [interfaccia della riga di comando](insights-alerts-command-line-interface.md)
* [API REST di Monitoraggio di Azure](https://msdn.microsoft.com/library/azure/dn931945.aspx)

Si può sempre ricevere Guida per i comandi, digitare un comando e la messa - Guida alla fine di hello. ad esempio:

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a>Creare regole di avviso utilizzando hello CLI
1. Eseguire prerequisiti hello e tooAzure account di accesso. Vedere gli [esempi dell'interfaccia della riga di comando di Monitoraggio di Azure](insights-cli-samples.md). In breve, hello CLI di installare ed eseguire questi comandi. E ottenere l'accesso, mostra quale sottoscrizione utilizza e preparazione toorun i comandi di monitoraggio di Azure.

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. le regole esistenti toolist in un gruppo di risorse, utilizzare hello seguente modulo **azure insights elenco di regole avvisi** *[opzioni] &lt;gruppo di risorse&gt;*

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. toocreate una regola, è necessario toohave importanti di varie informazioni prima di tutto.
  * Hello **ID risorsa** per la risorsa hello desiderato tooset un avviso per
  * Hello **le definizioni delle metriche** disponibili per tale risorsa

     Un modo tooget hello ID risorsa è toouse hello portale di Azure. Supponendo che la risorsa hello è già stata creata, selezionarlo nel portale di hello. Selezionare nel pannello successivo hello *proprietà* in hello *impostazioni* sezione. Hello *ID risorsa* è un campo nel pannello successivo hello. Un altro modo consiste hello toouse [Esplora inventario risorse di Azure](https://resources.azure.com/).

     Un esempio di ID risorsa per un'app Web è

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     tooget un elenco delle metriche disponibili hello e unità per le metriche per hello precedente esempio di risorse, hello di utilizzare il comando CLI seguente:  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     *PT1M* è hello granularità di misura disponibili hello (intervalli di 1 minuto). L'uso di granularità diverse offre opzioni di metrica diverse.
4. toocreate una regola di avviso basata su metrica, utilizzare un comando di hello seguente formato:

    **azure insights alerts rule metric set** *[opzioni] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*

    Hello nel seguente esempio impostare un avviso su una risorsa di sito web. trigger avviso Hello ogni volta che riceve il traffico in modo coerente per 5 minuti e nuovamente quando non riceve alcun traffico per 5 minuti.

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. toocreate webhook o Invia messaggio di posta elettronica quando viene generato un avviso di metrica, creare innanzitutto la posta elettronica hello e/o webhook. Quindi creare immediatamente regola hello in seguito. Non è possibile associare webhook o messaggi di posta elettronica con già creato le regole utilizzando hello CLI.

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. È possibile verificare che gli avvisi siano stati creati correttamente esaminando una singola regola.

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. toodelete regole, utilizzare un comando del modulo hello:

    **insights alerts rule delete** [opzioni] &lt;resourceGroup&gt;&lt;ruleName&gt;

    Questi comandi eliminano regole hello create in precedenza in questo articolo.

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a>Passaggi successivi
* [Panoramica di Azure monitoring](monitoring-overview.md) inclusi i tipi di informazioni è possibile raccogliere e monitorare hello.
* Altre informazioni sulla [configurazione dei webhook negli avvisi](insights-webhooks-alerts.md).
* Altre informazioni sulla [configurazione di avvisi sugli eventi del log attività](monitoring-activity-log-alerts.md).
* Altre informazioni sui [runbook di automazione di Azure](../automation/automation-starting-a-runbook.md).
* Ottenere un [Panoramica di raccogliere i log di diagnostica](monitoring-overview-of-diagnostic-logs.md) toocollect dettagliate ad alta frequenza metriche sul servizio.
* Ottenere un [Panoramica della raccolta di metriche](insights-how-to-customize-monitoring.md) toomake che il servizio sia disponibile e reattiva.

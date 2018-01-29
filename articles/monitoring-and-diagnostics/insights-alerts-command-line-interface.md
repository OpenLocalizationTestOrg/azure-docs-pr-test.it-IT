---
title: Creare avvisi per i servizi di Azure - Interfaccia della riga di comando multipiattaforma | Microsoft Docs
description: Attivare messaggi di posta elettronica o notifiche, chiamare URL di siti Web (webhook) o usare l'automazione quando vengono soddisfatte le condizioni specificate.
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
ms.openlocfilehash: 92246a8da73a244a1c9a924bed55711d71a20fd8
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a>Creare avvisi sulle metriche in Monitoraggio di Azure per i servizi di Azure - Interfaccia della riga di comando multipiattaforma
> [!div class="op_single_selector"]
> * [di Microsoft Azure](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Panoramica
Questo articolo descrive come impostare gli avvisi sulle metriche di Azure tramite l'interfaccia della riga di comando multipiattaforma.

> [!NOTE]
> Dal 25 settembre 2016 Monitoraggio di Azure è il nuovo nome di "Azure Insights". Tuttavia, gli spazi dei nomi e quindi i comandi seguenti contengono ancora il termine "insights".
>
>

È possibile ricevere avvisi basati su metriche di monitoraggio o eventi nei servizi Azure.

* **Valori metrici** : l'avviso si attiva quando il valore di una specifica metrica supera una soglia assegnata per eccesso o difetto. Vale a dire che si attiva sia quando la condizione viene inizialmente soddisfatta e successivamente quando tale condizione non è più soddisfatta.    
* **Eventi del log attività**: è possibile attivare un avviso per *ogni* evento o solo quando si verifica un determinato evento. Per altre informazioni sugli avvisi sui log attività [fare clic qui](monitoring-activity-log-alerts.md)

È possibile configurare un avviso sulle metriche affinché esegua queste operazioni al momento dell'attivazione:

* inviare un messaggio di posta elettronica all'amministratore e ai coamministratori del servizio
* inviare un messaggio di posta elettronica ad altri indirizzi specificati
* chiamare un webhook
* avviare l'esecuzione di un runbook di Azure; attualmente è possibile solo dal portale di Azure

È possibile configurare e ottenere informazioni sulle regole degli avvisi sulle metriche tramite

* [Azure portal](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [interfaccia della riga di comando](insights-alerts-command-line-interface.md)
* [API REST di Monitoraggio di Azure](https://msdn.microsoft.com/library/azure/dn931945.aspx)

È possibile ricevere assistenza per i comandi digitando un comando e inserendo -help al termine. Ad esempio: 

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-the-cli"></a>Creare le regole di avviso tramite l'interfaccia della riga di comando
1. Controllare i prerequisiti e accedere ad Azure. Vedere gli [esempi dell'interfaccia della riga di comando di Monitoraggio di Azure](insights-cli-samples.md). In breve, installare l'interfaccia della riga di comando ed eseguire questi comandi. Questi comandi eseguono l'accesso, indicano la sottoscrizione in uso e preparano l'esecuzione dei comandi di Monitoraggio di Azure.

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. Per elencare le regole esistenti in un gruppo di risorse, usare il seguente formato **azure insights alerts rule list** *[opzioni] &lt;resourceGroup&gt;*

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. Per creare una regola, per prima cosa è necessario disporre di alcune informazioni importanti.
  * L' **ID risorsa** della risorsa per la quale si intende impostare un avviso
  * Le **definizioni delle metriche** disponibili per tale risorsa

     È possibile ottenere l'ID della risorsa tramite il portale di Azure. Se la risorsa è già stata creata, selezionarla nel portale. Nel pannello successivo, nella sezione *Impostazioni*, selezionare *Proprietà*. *ID RISORSA* è un campo nel pannello successivo. È anche possibile usare [Esplora risorse di Azure](https://resources.azure.com/).

     Un esempio di ID risorsa per un'app Web è

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     Per ottenere un elenco delle metriche e delle unità per le metriche disponibili per l'esempio precedente di risorse, usare il comando dell'interfaccia della riga di comando seguente:  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     *PT1M* indica la granularità della misurazione disponibile, con intervalli di 1 minuto. L'uso di granularità diverse offre opzioni di metrica diverse.
4. Per creare una regola di avviso basata sulla metrica, usare un comando nel formato seguente:

    **azure insights alerts rule metric set** *[opzioni] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*

    L'esempio seguente imposta un avviso relativo a una risorsa del sito Web. L'avviso viene attivato ogni volta che si riceve il traffico costantemente per 5 minuti e di nuovo quando non si riceve traffico per 5 minuti.

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. Per creare il webhook o inviare un messaggio di posta elettronica all'attivazione di un avviso di metrica, creare prima il messaggio di posta elettronica e/o i webhook. Creare la regola immediatamente dopo. Non è possibile associare il webhook o messaggi di posta elettronica a regole già create tramite l'interfaccia della riga di comando.

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. È possibile verificare che gli avvisi siano stati creati correttamente esaminando una singola regola.

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. Per eliminare le regole, usare un comando nel formato:

    **insights alerts rule delete** [opzioni] &lt;resourceGroup&gt;&lt;ruleName&gt;

    Questi comandi eliminano le regole create in precedenza in questo articolo.

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a>Passaggi successivi
* [Leggere una panoramica del monitoraggio di Azure](monitoring-overview.md) che include anche i tipi di informazioni che è possibile raccogliere e monitorare.
* Altre informazioni sulla [configurazione dei webhook negli avvisi](insights-webhooks-alerts.md).
* Altre informazioni sulla [configurazione di avvisi sugli eventi del log attività](monitoring-activity-log-alerts.md).
* Altre informazioni sui [runbook di automazione di Azure](../automation/automation-starting-a-runbook.md).
* Leggere una [panoramica della raccolta dei log di diagnostica](monitoring-overview-of-diagnostic-logs.md) per raccogliere metriche dettagliate e ad alta frequenza sul servizio.
* Leggere una [panoramica della raccolta di metriche](insights-how-to-customize-monitoring.md) per verificare che il servizio sia disponibile e reattivo.

---
title: gli avvisi aaaCreate per servizi di Azure - PowerShell | Documenti Microsoft
description: Attivare l'automazione, notifiche, gli URL di siti Web di chiamata (webhook) o messaggi di posta elettronica quando vengono soddisfatte le condizioni di hello specificate.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a>Creare avvisi sulle metriche in Monitoraggio di Azure per i servizi di Azure: PowerShell
> [!div class="op_single_selector"]
> * [Portale](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Panoramica
Questo articolo illustra come tooset backup Azure metrica avvisi tramite PowerShell.  

È possibile ricevere avvisi basati su metriche di monitoraggio o eventi nei servizi Azure.

* **Valori della metrica** : hello trigger un avviso quando il valore di hello di una specifica metrica supera una soglia è assegnare in entrambe le direzioni. Ovvero, entrambi attiva quando hello prima condizione e quindi successivamente non condizione when che è non è più in grado di soddisfare.    
* **Eventi del log attività**: è possibile attivare un avviso per *ogni* evento o solo quando si verifica un determinato evento. ulteriori informazioni sugli avvisi di log attività toolearn [fare clic qui](monitoring-activity-log-alerts.md)

È possibile configurare una metrica toodo avviso hello seguenti attiva:

* inviare coamministratore e amministratore del servizio toohello le notifiche tramite posta elettronica
* Invia messaggio di posta elettronica tooadditional messaggi di posta elettronica specificato.
* chiamare un webhook
* avviare l'esecuzione di un runbook di Azure (solo da hello portale di Azure)

È possibile configurare e ottenere informazioni sulle regole degli avvisi tramite

* [Portale di Azure](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [interfaccia della riga di comando](insights-alerts-command-line-interface.md)
* [API REST di Monitoraggio di Azure](https://msdn.microsoft.com/library/azure/dn931945.aspx)

Per ulteriori informazioni, è possibile digitare sempre ```Get-Help``` e quindi hello si vogliono informazioni sul comando di PowerShell.

## <a name="create-alert-rules-in-powershell"></a>Creare regole di avviso in PowerShell
1. Accedi tooAzure.   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. Ottenere un elenco di sottoscrizioni hello disponibile. Verificare che si lavora con sottoscrizione destra hello. In caso contrario, impostarla toohello destra di un utilizzo di output di hello da `Get-AzureRmSubscription`.

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. le regole esistenti toolist in un gruppo di risorse, utilizzare hello comando seguente:

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. toocreate una regola, è necessario toohave importanti di varie informazioni prima di tutto.

  * Hello **ID risorsa** per la risorsa hello desiderato tooset un avviso per
  * Hello **le definizioni delle metriche** disponibili per tale risorsa

     Un modo tooget hello ID risorsa è toouse hello portale di Azure. Supponendo che la risorsa hello è già stata creata, selezionarlo nel portale di hello. Selezionare nel pannello successivo hello *proprietà* in hello *impostazioni* sezione. **ID di risorsa** è un campo nel pannello successivo hello. Un altro modo consiste hello toouse [Esplora inventario risorse di Azure](https://resources.azure.com/).

     Un esempio di ID risorsa per un'app web è

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     È possibile utilizzare `Get-AzureRmMetricDefinition` elenco hello tooview di tutte le definizioni di metrica per una risorsa specifica.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     Hello esempio seguente genera una tabella con nome metrica di hello e hello unità per tale metrica.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     Un elenco completo delle opzioni disponibili per Get-AzureRmMetricDefinition è visualizzabile eseguendo Get-MetricDefinitions.
5. Hello nel seguente esempio impostare un avviso su una risorsa di sito web. trigger avviso Hello ogni volta che riceve il traffico in modo coerente per 5 minuti e nuovamente quando non riceve alcun traffico per 5 minuti.

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. toocreate webhook o Invia messaggio di posta elettronica quando viene generato un avviso, creare innanzitutto la posta elettronica hello e/o webhook. Quindi creare immediatamente regola hello in seguito con hello - tag azioni e, come illustrato nell'esempio seguente hello. Non è possibile associare webhook o messaggi di posta elettronica a regole già create tramite PowerShell.

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. tooverify che gli avvisi siano stati creati correttamente esaminando le singole regole hello.

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. Eliminare gli avvisi. Questi comandi eliminano regole hello create in precedenza in questo articolo.

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a>Passaggi successivi
* [Panoramica di Azure monitoring](monitoring-overview.md) inclusi i tipi di informazioni è possibile raccogliere e monitorare hello.
* Altre informazioni sulla [configurazione dei webhook negli avvisi](insights-webhooks-alerts.md).
* Altre informazioni sulla [configurazione di avvisi sugli eventi del log attività](monitoring-activity-log-alerts.md).
* Altre informazioni sui [runbook di automazione di Azure](../automation/automation-starting-a-runbook.md).
* Ottenere un [Panoramica di raccogliere i log di diagnostica](monitoring-overview-of-diagnostic-logs.md) toocollect dettagliate ad alta frequenza metriche sul servizio.
* Ottenere un [Panoramica della raccolta di metriche](insights-how-to-customize-monitoring.md) toomake che il servizio sia disponibile e reattiva.

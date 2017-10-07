---
title: "set di scalabilità di macchine virtuali di Azure scala aaaVertically | Documenti Microsoft"
description: Come toovertically ridimensionare una macchina virtuale negli avvisi toomonitoring risposta con automazione di Azure
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: madhana
editor: 
tags: azure-resource-manager
ms.assetid: 16b17421-6b8f-483e-8a84-26327c44e9d3
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: guybo
ms.openlocfilehash: 1cc35a805b6a5742252a89c21588ca451ff547a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a>Ridimensionamento automatico verticale con set di scalabilità di macchine virtuali
In questo articolo vengono descritte le modalità di scalabilità di Azure toovertically [set di scalabilità di macchine virtuali](https://azure.microsoft.com/services/virtual-machine-scale-sets/) con o senza la riconfigurazione. Per la scalabilità verticale delle macchine virtuali che non sono presenti nel set di scalabilità, vedere troppo[scalare verticalmente macchina virtuale di Azure con automazione di Azure](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

La scalabilità verticale, anche noto come *scalabilità verticale* e *scalare verso il basso*indica aumentando o riducendo le dimensioni di macchina virtuale (VM) del carico di lavoro di risposta tooa. Confronto con [scalabilità orizzontale](virtual-machine-scale-sets-autoscale-overview.md), definita anche tooas *scalabilità* e *ridimensionare in*, in cui è stato modificato il numero di hello di macchine virtuali a seconda del carico di lavoro di hello.

Per nuovo provisioning si intende la rimozione di una VM esistente e la relativa sostituzione con una nuova. Quando si aumentare o diminuire le dimensioni di hello di macchine virtuali in un Set di scalabilità della macchina virtuale, in alcuni casi si desidera tooresize le macchine virtuali esistenti e mantenere i dati, mentre in altri casi è necessario toodeploy nuove macchine virtuali della nuova dimensione hello. Questo documento illustra entrambi i casi.

Il ridimensionamento verticale, ovvero l'aumento o la riduzione delle prestazioni, può risultare utile quando:

* Un servizio basato su macchine virtuali è sottoutilizzato, ad esempio nel fine settimana. Riduzione delle dimensioni di VM hello, è possibile ridurre i costi mensili.
* Aumento toocope dimensioni di macchina virtuale con richiesta di dimensioni maggiore senza creare altre macchine virtuali.

È possibile impostare verticale scalabilità toobe attivato basati sugli avvisi di base metrica dal Set di scalabilità della macchina virtuale. Quando viene attivato hello avviso viene generato un webhook che attiva un runbook che è possibile ridimensionare la scala è impostato su o giù. Il ridimensionamento verticale può essere configurato seguendo questa procedura:

1. Creare un account di Automazione di Azure con funzionalità RunAs.
2. Importare i runbook di scalabilità verticale di Automazione di Azure per i set di scalabilità di macchine virtuali nella sottoscrizione.
3. Aggiungere un runbook tooyour webhook.
4. Aggiungere un avviso tooyour Set di scalabilità macchina virtuale utilizza la notifica di un webhook.

> [!NOTE]
> Il ridimensionamento verticale può avvenire solo entro determinati intervalli di dimensioni delle VM. Confronto delle specifiche di hello di ogni dimensione prima di decidere tooscale da uno tooanother (numero più alto non indicare sempre più grande dimensione della macchina virtuale). È possibile scegliere tooscale tra hello coppie di dimensioni seguenti:
> 
> | coppie di ridimensionamento di dimensioni delle macchine virtuali |  |
> | --- | --- |
> | Standard_A0 |Standard_A11 |
> | Standard_D1 |Standard_D14 |
> | Standard_DS1 |Standard_DS14 |
> | Standard_D1v2 |Standard_D15v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a>Creare un account di Automazione di Azure con funzionalità RunAs
Hello occorre innanzitutto toodo è creare un account di automazione di Azure che ospiterà hello runbook utilizzato tooscale hello Set di scalabilità della macchina virtuale istanze. Recentemente [automazione di Azure](https://azure.microsoft.com/services/automation/) introdotte funzionalità "Esegui come account" hello che rende impostazione hello dell'entità servizio per l'esecuzione automatica hello runbook per conto dell'utente molto semplice. È possibile leggere altre informazioni nell'articolo hello riportato di seguito:

* [Autenticare runbook con account RunAs di Azure](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Importare i runbook di ridimensionamento verticale di Automazione di Azure nella sottoscrizione
i runbook Hello necessario scala toovertically che il set di scalabilità di macchine Virtuali sono già pubblicati nella raccolta di Runbook di automazione di Azure hello. nella sottoscrizione seguono hello tooimport passaggi riportati in questo articolo.

* [Raccolte di runbook e moduli per l'automazione di Azure](../automation/automation-runbook-gallery.md)

Scegliere l'opzione Sfoglia raccolta hello dal menu di runbook hello:

![Toobe runbook importati][runbooks]

i runbook Hello necessario toobe importati vengono visualizzati. Selezionare il runbook hello in base che si voglia con o senza la riconfigurazione della scalabilità verticale:

![Raccolta di runbook][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a>Aggiungere un runbook tooyour webhook
Dopo aver importato i runbook hello è necessario un runbook toohello webhook tooadd in modo che può essere attivata da un avviso generato da un Set di scalabilità della macchina virtuale. in questo articolo sono descritti i dettagli di Hello per la creazione di un webhook per il Runbook:

* [Webhook di Automazione di Azure](../automation/automation-webhooks.md)

> [!NOTE]
> Assicurarsi di copiare hello webhook URI prima della chiusura di finestra di dialogo webhook hello perché sarà necessaria nella sezione successiva hello.
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a>Aggiungere un avviso tooyour Set di scalabilità della macchina virtuale
Di seguito è riportato un PowerShell script che mostra come tooadd un avviso tooa Set di scalabilità della macchina virtuale. Fare riferimento toohello dopo il nome di hello articolo tooget di avviso di hello toofire metrica hello: [comuni metriche di monitoraggio di Azure per la scalabilità automatica](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).

```
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail user@contoso.com
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri <uri-of-the-webhook>
$threshold = <value-of-the-threshold>
$rg = <resource-group-name>
$id = <resource-id-to-add-the-alert-to>
$location = <location-of-the-resource>
$alertName = <name-of-the-resource>
$metricName = <metric-to-fire-the-alert-on>
$timeWindow = <time-window-in-hh:mm:ss-format>
$condition = <condition-for-the-threshold> # Other valid values are LessThanOrEqual, GreaterThan, GreaterThanOrEqual
$description = <description-for-the-alert>

Add-AzureRmMetricAlertRule  -Name  $alertName `
                            -Location  $location `
                            -ResourceGroup $rg `
                            -TargetResourceId $id `
                            -MetricName $metricName `
                            -Operator  $condition `
                            -Threshold $threshold `
                            -WindowSize  $timeWindow `
                            -TimeAggregationOperator Average `
                            -Actions $actionEmail, $actionWebhook `
                            -Description $description
```

> [!NOTE]
> È consigliabile tooconfigure un intervallo di tempo ragionevole per avviso hello in ordine tooavoid attivando la scalabilità verticale e qualsiasi associata un'interruzione del servizio, troppo spesso. Considerare un intervallo minimo di 20-30 minuti. È consigliabile se è necessario tooavoid interruzione la scalabilità orizzontale.
> 
> 

Per ulteriori informazioni su come toocreate avvisi fare riferimento toohello seguenti articoli:

* [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md) (Esempi di avvio rapido di PowerShell per Monitoraggio di Azure)
* [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md) (Esempi di avvio rapido dell'interfaccia della riga di comando multipiattaforma per Monitoraggio di Azure)

## <a name="summary"></a>Riepilogo
Questo articolo ha illustrato semplici esempi di ridimensionamento verticale. Con questi blocchi predefiniti, ovvero account di automazione, runbook, webhook e avvisi, è possibile connettere una vasta gamma di eventi con un set di azioni personalizzato.

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png

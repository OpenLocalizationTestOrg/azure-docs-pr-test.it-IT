---
title: esempi di avvio rapido di aaaAzure PowerShell di monitoraggio. | Microsoft Docs
description: "Utilizzare PowerShell tooaccess funzionalità di monitoraggio di Azure quali scalabilità automatica, gli avvisi, webhook e la ricerca di log di attività."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a>Esempi di avvio rapido con PowerShell per Monitoraggio di Azure
In questo articolo viene indicato il campionamento toohelp di comandi di PowerShell accedere alle funzionalità di monitoraggio di Azure. Monitoraggio di Azure consente tooAutoScale servizi Cloud, macchine virtuali e le applicazioni Web e toosend notifiche di avviso o URL web chiamata in base ai valori dei dati di telemetria configurato.

> [!NOTE]
> Monitoraggio di Azure è hello nuovo nome per ciò che è stato chiamato "Azure Insights" fino a 25 settembre 2016. Tuttavia, gli spazi dei nomi hello e pertanto hello ancora i comandi seguenti contengono approfondite"hello".
> 
> 

## <a name="set-up-powershell"></a>Configurare PowerShell
Se hai già fatto, configurare toorun PowerShell nel computer in uso. Per ulteriori informazioni, vedere [come tooInstall e configurare PowerShell](/powershell/azure/overview).

## <a name="examples-in-this-article"></a>Esempi in questo articolo
esempi di Hello di articolo hello illustrato come utilizzare i cmdlet di monitoraggio di Azure. È inoltre possibile rivedere l'elenco completo di hello di cmdlet di PowerShell di monitoraggio di Azure in [i cmdlet di Azure Monitor (Insights)](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).

## <a name="sign-in-and-use-subscriptions"></a>Eseguire l'acccesso e usare le sottoscrizioni
Innanzitutto, effettuare l'accesso tooyour sottoscrizione di Azure.

```PowerShell
Login-AzureRmAccount
```

Questa operazione richiede toosign in. Dopo aver effettuato l'accesso, vengono visualizzati l'account, l'ID tenant e l'ID sottoscrizione predefinito. Tutti hello lavoro cmdlet di Azure nel contesto di hello della sottoscrizione predefinita. elenco di hello tooview delle sottoscrizioni si ha accesso a, utilizzare hello comando seguente.

```PowerShell
Get-AzureRmSubscription
```

toochange lavoro contesto tooa diversa sottoscrizione, utilizzare hello comando seguente.

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a>Recuperare il registro attività per una sottoscrizione
Hello utilizzare `Get-AzureRmLog` cmdlet.  Hello di seguito è riportati alcuni esempi comuni.

Ottenere le voci di log da toopresent questa data e ora:

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

Ottenere le voci di log in un intervallo di date e ore:

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

Ottenere le voci di log da un gruppo di risorse specifico:

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

Ottenere le voci di log da un provider di risorse specifico in un intervallo di date e ore:

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

Ottenere tutte le voci di log con un chiamante specifico:

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

Hello comando Recupera hello ultimi 1.000 eventi dal log attività hello seguente:

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

`Get-AzureRmLog` supporta diversi altri parametri. Vedere hello `Get-AzureRmLog` riferimento per altre informazioni.

> [!NOTE]
> `Get-AzureRmLog` fornisce solo 15 giorni di cronologia. Utilizzo di hello **- MaxEvents** parametro consente tooquery hello ultimi N eventi, oltre a 15 giorni. eventi tooaccess anteriori a 15 giorni, utilizzare hello API REST o SDK (esempio di c# utilizzando hello SDK). Se non si include **StartTime**, il valore predefinito di hello **EndTime** meno di un'ora. Se non si include **EndTime**, il valore predefinito di hello ora corrente. Tutte le ore sono in formato UTC.
> 
> 

## <a name="retrieve-alerts-history"></a>Recupero della cronologia di avvisi
tutti gli eventi di allarme, è possibile eseguire query tooview hello registri di gestione risorse di Azure mediante hello seguono esempi.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

regola di cronologia di hello tooview per un avviso specifico, è possibile utilizzare hello `Get-AzureRmAlertHistory` cmdlet, il passaggio di ID di risorsa hello della regola di avviso hello.

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

Hello `Get-AzureRmAlertHistory` cmdlet supporta vari parametri. Per altre informazioni, vedere [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).

## <a name="retrieve-information-on-alert-rules"></a>Recupero delle informazioni sulle regole di avviso
Tutti i seguenti comandi hello agiscono su un gruppo di risorse denominato "montest".

Visualizzare tutte le proprietà di hello della regola di avviso hello:

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

Recuperare tutti gli avvisi in un gruppo di risorse:

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

Recuperare tutte le regole di avviso impostate per una risorsa di destinazione. Ad esempio, tutte le regole di avviso impostate su una VM.

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

`Get-AzureRmAlertRule` supporta altri parametri. Per altre informazioni, vedere [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) .

## <a name="create-metric-alerts"></a>Creare avvisi delle metriche
È possibile utilizzare hello `Add-AlertRule` toocreate cmdlet, aggiornare o disabilitare una regola di avviso.

È possibile creare proprietà di posta elettronica e webhook usando rispettivamente `New-AzureRmAlertRuleEmail` e `New-AzureRmAlertRuleWebhook`. Nel cmdlet hello regola di avviso per assegnare queste come azioni toohello **azioni** proprietà della regola di avviso hello.

Hello nella tabella seguente vengono descritti i parametri di hello e valori utilizzati toocreate un avviso utilizzando una metrica.

| parametro | value |
| --- | --- |
| Nome |simpletestdiskwrite |
| Posizione di questa regola di avviso |Stati Uniti orientali |
| ResourceGroup |montest |
| TargetResourceId |/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig |
| MetricName di avviso hello creato |\PhysicalDisk ( totale) \Disk scritture al secondo. Vedere hello `Get-MetricDefinitions` come tooretrieve hello esatti nomi di metrica relativi ai cmdlet di |
| operator |GreaterThan |
| Valore soglia (conteggio al secondo per questa metrica) |1 |
| WindowSize (formato hh:mm:ss) |00:05:00 |
| Aggregator (statistica della metrica di hello, che utilizza il numero medio, in questo caso) |Media |
| indirizzi di posta elettronica personalizzati (matrice di stringhe) |'foo@example.com','bar@example.com' |
| Invia messaggio di posta elettronica tooowners, contributors e readers |-SendToServiceOwners |

Creare un'azione Email

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

Creazione di un’azione Webhook

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

Crea regola di avviso hello nella metrica % della CPU di hello in una VM classica

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

Recuperare la regola di avviso hello

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

Hello Aggiungi avviso cmdlet Aggiorna regola hello anche se per hello proprietà specificato esiste già una regola di avviso. toodisable una regola di avviso, includere il parametro hello **- DisableRule**.

## <a name="get-a-list-of-available-metrics-for-alerts"></a>Acquisizione di un elenco delle metriche disponibili per gli avvisi
È possibile utilizzare hello `Get-AzureRmMetricDefinition` cmdlet tooview hello elenco tutte le metriche per una risorsa specifica.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

Hello esempio seguente genera una tabella con nome metrica di hello e hello unità per tale.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

Un elenco completo delle opzioni disponibili per `Get-AzureRmMetricDefinition` si trova in [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).

## <a name="create-and-manage-autoscale-settings"></a>Creazione e gestione delle impostazioni di scalabilità automatica
Una risorsa, ad esempio un'app Web, una macchina virtuale, un servizio cloud o un set di scalabilità di macchine virtuali, può avere una sola impostazione di scalabilità automatica configurata.
Tuttavia, ogni impostazione di scalabilità automatica può includere diversi profili. Ad esempio, un profilo di scalabilità in base alle prestazioni e un altro profilo basato sulla pianificazione. Ogni profilo può avere più regole associate configurate. Per ulteriori informazioni sulla scalabilità automatica, vedere [come un'applicazione tooAutoscale](../cloud-services/cloud-services-how-to-scale.md).

Ecco i passaggi di hello che verrà utilizzato:

1. Creare le regole.
2. Creare profili hello mapping regole creata in precedenza toohello profili.
3. Facoltativo: creare notifiche per la scalabilità automatica configurando le proprietà di webhook e posta elettronica.
4. Creare un'impostazione di scalabilità automatica con un nome sulla risorsa di destinazione hello eseguendo il mapping di profili di hello e notifiche creato nei passaggi precedenti hello.

Hello esempi seguenti si illustra come creare un'impostazione di scalabilità automatica per un Set di scalabilità macchina virtuale per un sistema operativo Windows basato mediante la metrica di utilizzo della CPU hello.

Innanzitutto, creare una regola tooscale in orizzontale, con un aumento del numero di istanza.

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

Successivamente, creare una regola tooscale, con una riduzione del numero di istanza.

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

Quindi, creare un profilo per le regole di hello.

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

Creare una proprietà webhook.

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

Creare la proprietà di notifica di hello per l'impostazione di scalabilità automatica hello, inclusa la posta elettronica e hello webhook creato in precedenza.

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

Creare infine hello scalabilità automatica impostazione tooadd hello profilo creato in precedenza.

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

Per altre informazioni sulla gestione delle impostazioni di scalabilità automatica, vedere [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).

## <a name="autoscale-history"></a>Cronologia di scalabilità automatica
Hello seguente esempio viene illustrato come visualizzare gli eventi di ridimensionamento automatico e avviso recente. Utilizzare hello attività tooview hello scalabilità automatica cronologia di ricerca.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

È possibile utilizzare hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve cronologia scalabilità.

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

Per altre informazioni, vedere [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).

### <a name="view-details-for-an-autoscale-setting"></a>Visualizzazione dei dettagli per un'impostazione di scalabilità automatica
È possibile utilizzare hello `Get-Autoscalesetting` cmdlet tooretrieve ulteriori informazioni sull'impostazione di scalabilità automatica hello.

Hello esempio seguente mostra informazioni dettagliate su tutte le impostazioni di scalabilità automatica nel gruppo di risorse hello 'myrg1'.

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

Hello esempio seguente mostra i dettagli di tutte le impostazioni di scalabilità automatica nel gruppo di risorse hello 'myrg1' e in particolare hello denominato 'MyScaleVMSSSetting' impostazione di scalabilità automatica.

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a>Rimozione di un'impostazione di scalabilità automatica
È possibile utilizzare hello `Remove-Autoscalesetting` cmdlet toodelete un'impostazione di scalabilità automatica.

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a>Gestione dei profili di log per i registri attività
È possibile creare un *log profilo* e l'esportazione dei dati da account di archiviazione tooa log attività ed è possibile configurare conservazione dei dati per tale. Facoltativamente, è inoltre possibile trasmettere hello dati tooyour Hub eventi. Questa funzionalità attualmente è in anteprima ed è possibile creare solo un profilo di log per ogni sottoscrizione. È possibile utilizzare hello seguente cmdlet con il toocreate sottoscrizione corrente e gestire i profili di log. È anche possibile scegliere una sottoscrizione specifica. Anche se la sottoscrizione corrente toohello impostazioni predefinite di PowerShell è sempre possibile modificare tale tramite `Set-AzureRmContext`. È possibile configurare l'account di archiviazione tooany dati tooroute log attività o l'Hub di eventi all'interno di tale sottoscrizione. I dati sono scritti come file di BLOB in formato JSON.

### <a name="get-a-log-profile"></a>Acquisizione di un profilo di log
toofetch i profili di log esistente, utilizzare hello `Get-AzureRmLogProfile` cmdlet.

### <a name="add-a-log-profile-without-data-retention"></a>Aggiunta di un profilo di log senza conservazione dei dati
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>Rimozione di un profilo di log
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a>Aggiunta di un profilo di log con conservazione dei dati
È possibile specificare hello **- RetentionInDays** proprietà con hello numero di giorni, come un numero intero positivo, in cui i dati di hello verranno mantenuti.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a>Aggiunta di un profilo di log con conservazione e hub di eventi
In aggiunta toorouting account toostorage di dati, è possibile anche trasmetterlo tramite flusso tooan Hub eventi. Si noti che in questa versione di anteprima release e hello configurazione di account di archiviazione è obbligatorio ma configurazione Hub eventi è facoltativa.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a>Configurazione dei log di diagnostica
Molti servizi di Azure forniscono i log e dati di telemetria che possono essere dati toosave configurata nell'account di archiviazione di Azure, inviare tooEvent hub e/o inviati tooan dell'area di lavoro OMS Log Analitica. Tale operazione può essere eseguita solo a un livello di risorse e hub di eventi o di account di archiviazione hello devono essere presenti in hello stessa area risorse di destinazione hello in hello diagnostica è configurata.

### <a name="get-diagnostic-setting"></a>Acquisizione dell’impostazione di diagnostica
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

Disabilitazione dell’impostazione di diagnostica

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

Abilitazione dell'impostazione di diagnostica senza conservazione

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

Abilitazione dell'impostazione di diagnostica con conservazione

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

Abilitazione dell’impostazione di diagnostica con conservazione per una categoria di log specifica

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

Abilitazione dell'impostazione di diagnostica per hub eventi

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

Abilitazione dell'impostazione di diagnostica per OMS

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```

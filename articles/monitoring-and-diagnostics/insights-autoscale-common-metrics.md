---
title: "metriche di monitoraggio di scalabilità automatica comuni aaaAzure | Documenti Microsoft"
description: "Informazioni su quali metriche vengono comunemente usate per la scalabilità automatica di servizi cloud, macchine virtuali e app Web."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 189b2a13-01c8-4aca-afd5-90711903ca59
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/6/2016
ms.author: ancav
ms.openlocfilehash: 372a40d72d7a6c22c5ff854b1460ec8a3b7ed1d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-autoscaling-common-metrics"></a>Metriche comuni per la scalabilità automatica di Monitoraggio di Azure
La scalabilità automatica monitoraggio di Azure consente si tooscale hello numero di istanze in esecuzione verso l'alto o verso il basso, in base ai dati di telemetria (metriche). Questo documento descrive metriche di uso comune che è possibile toouse. Nel portale di Azure per Server farm e i servizi Cloud hello, è possibile scegliere la metrica di hello di hello risorsa tooscale da. Tuttavia, è possibile scegliere anche le metriche da tooscale una risorsa diversa da.

Azure scalabilità automatica di monitoraggio si applica solo troppo[set di scalabilità di macchine virtuali](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [servizi Cloud](https://azure.microsoft.com/services/cloud-services/), e [servizio App: app Web](https://azure.microsoft.com/services/app-service/web/). Altri servizi Azure usano metodi di ridimensionamento diversi.

## <a name="compute-metrics-for-resource-manager-based-vms"></a>Metriche di calcolo per le macchine virtuali basate su Resource Manager
Per impostazione predefinita, le macchine virtuali e i set di scalabilità di macchine virtuali basati su Resource Manager generano metriche di base (a livello di host). Inoltre, quando si configura raccolta dati di diagnostica per una macchina virtuale di Azure e VMSS, hello estensione diagnostica di Azure genera anche i contatori delle prestazioni di sistema operativo guest (noti come "Sistema operativo guest metriche").  Tutte queste metriche vengono usate nelle regole di scalabilità automatica.

È possibile utilizzare hello `Get MetricDefinitions` PoSH/API/CLI tooview hello le metriche disponibili per la risorsa VMSS.

Se si usano set di scalabilità di macchine virtuali e una metrica specifica non è riportata nell'elenco, è probabile che sia *disabilitata* nell'estensione della diagnostica.

Se una metrica specifica non è in corso frequenza hello campionate o trasferiti nella desiderata, è possibile aggiornare la configurazione di diagnostica hello.

Se entrambi i casi precedenti sono true, quindi esaminare [tooenable PowerShell utilizzare diagnostica Azure in una macchina virtuale che esegue Windows](../virtual-machines/windows/ps-extensions-diagnostics.md) su PowerShell tooconfigure e aggiornare il tooenable estensione diagnostica di Azure VM hello metrica. Questo articolo include anche un file di configurazione della diagnostica di esempio.

### <a name="host-metrics-for-resource-manager-based-windows-and-linux-vms"></a>Metriche host per le VM Windows e Linux basate su Resource Manager
Hello seguendo le metriche a livello di host generato per impostazione predefinita per la macchina virtuale di Azure e VMSS nelle istanze di Windows e Linux. Queste metriche illustrano la macchina virtuale di Azure, ma vengono raccolti da host della macchina virtuale di Azure hello piuttosto che tramite l'agente installato nella macchina virtuale guest hello. Queste metriche possono essere usate nelle regole di scalabilità automatica.

- [Metriche host per le VM Windows e Linux basate su Resource Manager](monitoring-supported-metrics.md#microsoftcomputevirtualmachines)
- [Metriche host per i set di scalabilità di macchine virtuali Windows e Linux basati su Resource Manager](monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets)

### <a name="guest-os-metrics-resource-manager-based-windows-vms"></a>Metriche del sistema operativo guest per le VM Windows basate su Resource Manager
Quando si crea una macchina virtuale in Azure, diagnostica è abilitata con l'estensione di diagnostica hello. estensione di diagnostica Hello genera un set di metriche prelevati all'interno di hello macchina virtuale. Questo significa che è possibile gestire la scalabilità automatica con metriche non generate per impostazione predefinita.

È possibile generare un elenco delle metriche hello utilizzando hello comando PowerShell seguente.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

È possibile creare un avviso per hello seguenti metriche:

| Nome della metrica | Unità |
| --- | --- |
| \Processor(_Total)\% Processor Time |Percentuale |
| \Processor(_Total)\% Privileged Time |Percentuale |
| \Processor(_Total)\% User Time |Percentuale |
| \Processor Information(_Total)\Processor Frequency |Numero |
| \System\Processes |Numero |
| \Process(_Total)\Thread Count |Numero |
| \Process(_Total)\Handle Count |Numero |
| \Memory\% Committed Bytes In Use |Percentuale |
| \Memory\Available Bytes |Byte |
| \Memory\Committed Bytes |Byte |
| \Memory\Commit Limit |Byte |
| \Memory\Pool Paged Bytes |Byte |
| \Memory\Pool Nonpaged Bytes |Byte |
| \PhysicalDisk(_Total)\% Disk Time |Percentuale |
| \PhysicalDisk(_Total)\% Disk Read Time |Percentuale |
| \PhysicalDisk(_Total)\% Disk Write Time |Percentuale |
| \DiscoFisico(_Totale)\Trasferimenti disco/secondo |Conteggio al secondo |
| \PhysicalDisk(_Total)\Disk Reads/sec |Conteggio al secondo |
| \PhysicalDisk(_Total)\Disk Writes/sec |Conteggio al secondo |
| \PhysicalDisk(_Total)\Disk Bytes/sec |Byte al secondo |
| \PhysicalDisk(_Total)\Disk Read Bytes/sec |Byte al secondo |
| \PhysicalDisk(_Total)\Disk Write Bytes/sec |Byte al secondo |
| \PhysicalDisk(_Total)\Avg. Lunghezza coda disco |Numero |
| \PhysicalDisk(_Total)\Avg. Disk Read Queue Length |Numero |
| \PhysicalDisk(_Total)\Avg. Disk Write Queue Length |Numero |
| \LogicalDisk(_Total)\% Free Space |Percentuale |
| \LogicalDisk(_Total)\Free Megabytes |Numero |

### <a name="guest-os-metrics-linux-vms"></a>Metriche del sistema operativo guest per le VM Linux
Quando si crea una nuova VM in Azure, la diagnostica viene abilitata per impostazione predefinita con l'uso dell'estensione Diagnostica.

È possibile generare un elenco delle metriche hello utilizzando hello comando PowerShell seguente.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

 È possibile creare un avviso per hello seguenti metriche:

| Nome della metrica | Unità |
| --- | --- |
| \Memory\AvailableMemory |Byte |
| \Memory\PercentAvailableMemory |Percentuale |
| \Memory\UsedMemory |Byte |
| \Memory\PercentUsedMemory |Percentuale |
| \Memory\PercentUsedByCache |Percentuale |
| \Memory\PagesPerSec |Conteggio al secondo |
| \Memory\PagesReadPerSec |Conteggio al secondo |
| \Memory\PagesWrittenPerSec |Conteggio al secondo |
| \Memory\AvailableSwap |Byte |
| \Memory\PercentAvailableSwap |Percentuale |
| \Memory\UsedSwap |Byte |
| \Memory\PercentUsedSwap |Percentuale |
| \Processor\PercentIdleTime |Percentuale |
| \Processor\PercentUserTime |Percentuale |
| \Processor\PercentNiceTime |Percentuale |
| \Processor\PercentPrivilegedTime |Percentuale |
| \Processor\PercentInterruptTime |Percentuale |
| \Processor\PercentDPCTime |Percentuale |
| \Processor\PercentProcessorTime |Percentuale |
| \Processor\PercentIOWaitTime |Percentuale |
| \PhysicalDisk\BytesPerSecond |Byte al secondo |
| \PhysicalDisk\ReadBytesPerSecond |Byte al secondo |
| \PhysicalDisk\WriteBytesPerSecond |Byte al secondo |
| \PhysicalDisk\TransfersPerSecond |Conteggio al secondo |
| \PhysicalDisk\ReadsPerSecond |Conteggio al secondo |
| \PhysicalDisk\WritesPerSecond |Conteggio al secondo |
| \PhysicalDisk\AverageReadTime |Secondi |
| \PhysicalDisk\AverageWriteTime |Secondi |
| \PhysicalDisk\AverageTransferTime |Secondi |
| \PhysicalDisk\AverageDiskQueueLength |Numero |
| \NetworkInterface\BytesTransmitted |Byte |
| \NetworkInterface\BytesReceived |Byte |
| \NetworkInterface\PacketsTransmitted |Numero |
| \NetworkInterface\PacketsReceived |Numero |
| \NetworkInterface\BytesTotal |Byte |
| \NetworkInterface\TotalRxErrors |Numero |
| \NetworkInterface\TotalTxErrors |Numero |
| \NetworkInterface\TotalCollisions |Numero |

## <a name="commonly-used-web-server-farm-metrics"></a>Metriche Web (server farm) usate comunemente
È anche possibile eseguire in base alle metriche di server web comuni, ad esempio lunghezza della coda Http hello di scalabilità automatica. Il nome della metrica è **HttpQueueLength**.  Hello seguendo le metriche di sezione elenchi disponibili server farm (app Web).

### <a name="web-apps-metrics"></a>Metriche di app Web
È possibile generare un elenco delle metriche di App Web hello utilizzando hello comando PowerShell seguente.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

È possibile generare avvisi o ridimensionare in base a queste metriche.

| Nome della metrica | Unità |
| --- | --- |
| CpuPercentage |Percentuale |
| MemoryPercentage |Percentuale |
| DiskQueueLength |Numero |
| HttpQueueLength |Numero |
| BytesReceived |Byte |
| BytesSent |Byte |

## <a name="commonly-used-storage-metrics"></a>Metriche di archiviazione usate comunemente
È possibile ridimensionare in base alla lunghezza coda di archiviazione, ovvero hello numero di messaggi nella coda di archiviazione hello. Lunghezza coda di archiviazione è una metrica speciale e soglia hello è il numero di hello dei messaggi per ogni istanza. Ad esempio, se sono presenti due istanze e se è stata impostata too100 hello soglia, la scalabilità quando hello il numero totale di messaggi nella coda di hello è 200. Che può essere 100 messaggi per ogni istanza, 120 e 80 o qualsiasi altra combinazione che vengono aggiunti too200 o più.

Configurare questa impostazione in hello portale di Azure in hello **impostazioni** blade. Per il set di scalabilità di macchine Virtuali, è possibile aggiornare l'impostazione di scalabilità automatica hello in hello Gestione risorse modello toouse *metricName* come *ApproximateMessageCount* e passare l'ID di hello della coda di archiviazione hello come  *metricResourceUri*.

Ad esempio, con hello un Account di archiviazione classico metricTrigger impostazione di scalabilità automatica includerà:

```
"metricName": "ApproximateMessageCount",
 "metricNamespace": "",
 "metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ClassicStorage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
 ```

Per un account di archiviazione (non-versione classica), è necessario includere metricTrigger hello:

```
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.Storage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
```

## <a name="commonly-used-service-bus-metrics"></a>Metriche del bus di servizio usate comunemente 
È possibile scalare lunghezza coda di Service Bus, ovvero hello numero di messaggi nella coda di Service Bus hello. Lunghezza coda del Bus di servizio è una metrica speciale e soglia hello è il numero di hello dei messaggi per ogni istanza. Ad esempio, se sono presenti due istanze e se è stata impostata too100 hello soglia, la scalabilità quando hello il numero totale di messaggi nella coda di hello è 200. Che può essere 100 messaggi per ogni istanza, 120 e 80 o qualsiasi altra combinazione che vengono aggiunti too200 o più.

Per il set di scalabilità di macchine Virtuali, è possibile aggiornare l'impostazione di scalabilità automatica hello in hello Gestione risorse modello toouse *metricName* come *ApproximateMessageCount* e passare l'ID di hello della coda di archiviazione hello come  *metricResourceUri*.

```
"metricName": "MessageCount",
 "metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ServiceBus/namespaces/SB_NAMESPACE/queues/QUEUE_NAME"
```

> [!NOTE]
> Per il Bus di servizio, concetto di gruppo di risorse hello non esiste, ma Azure Resource Manager crea un gruppo di risorse predefinito per ogni area. gruppo di risorse Hello è in genere in formato 'Default - bus di servizio-[region]' hello. Ad esempio, "Default-ServiceBus-EastUS", "Default-ServiceBus-WestUS", "Default-ServiceBus-AustraliaEast" e così via.
>
>

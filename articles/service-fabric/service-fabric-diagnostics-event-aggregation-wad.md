---
title: Aggregazione evento dei servizi dell'infrastruttura con diagnostica di Windows Azure aaaAzure | Documenti Microsoft
description: Informazioni sull'aggregazione e la raccolta di eventi con Diagnostica di Microsoft Azure per il monitoraggio e la diagnostica dei cluster di Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 4827ce66620e61c5b4a8682db55952333113188a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a>Aggregazione e raccolta di eventi con Diagnostica di Microsoft Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Quando si esegue un cluster di Azure Service Fabric, è un log di hello buona toocollect da tutti i nodi di hello in una posizione centrale. La presenza di log hello in una posizione centrale consente di analizzare e risolvere i problemi del cluster, o problemi in applicazioni hello e servizi in esecuzione in tale cluster.

Tooupload un modo e raccogliere i log è toouse estensione di Windows Azure di diagnostica hello, che consente di caricare i log tooAzure archiviazione e dispone inoltre di hello opzione toosend registri tooAzure Application Insights o hub eventi. È inoltre possibile utilizzare gli eventi di hello tooread un processo esterno dall'archivio e inserirle in un prodotto di piattaforma di analisi, ad esempio [OMS Log Analitica](../log-analytics/log-analytics-service-fabric.md) o un'altra soluzione di analisi di log.

## <a name="prerequisites"></a>Prerequisiti
Questi strumenti sono tooperform usate alcune delle operazioni di hello in questo documento:

* [Diagnostica di Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (correlata tooAzure servizi Cloud, ma con informazioni ed esempi)
* [Gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Client di Azure Resource Manager](https://github.com/projectkudu/ARMClient)
* [Modello di Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a>Origini di log ed eventi

### <a name="service-fabric-platform-events"></a>Eventi della piattaforma Service Fabric
Come descritto in [questo articolo](service-fabric-diagnostics-event-generation-infra.md), Service Fabric set di con alcuni canali di registrazione della casella, di cui hello seguenti canali sono facili da configurare con WAD toosend monitoraggio e diagnostica tooa archiviazione tabella dati o in altre posizioni:
  * Gli eventi operativi: le operazioni di alto livello che hello Service Fabric piattaforma esegue. Gli esempi includono la creazione di applicazioni e servizi, le modifiche allo stato dei nodi e informazioni sull'aggiornamento. Questi eventi vengono generati come log di Event Tracing for Windows (ETW)
  * [Eventi del modello di programmazione Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
  * [Eventi relativi al modello di programmazione Reliable Services](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a>Eventi dell'applicazione
 Gli eventi generati dal codice delle applicazioni e dei servizi e scritto utilizzando una classe helper di EventSource hello fornito in hello modelli di Visual Studio. Per ulteriori informazioni sulla modalità di registrazione toowrite EventSource dall'applicazione, vedere [Monitor e diagnosticare i servizi in una configurazione di sviluppo locale](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Distribuire l'estensione diagnostica hello
Hello primo passaggio per la raccolta di log è l'estensione di diagnostica toodeploy hello in ognuna delle macchine virtuali di hello in cluster di Service Fabric hello. Hello estensione di diagnostica raccoglie i log in ogni macchina virtuale e li carica toohello account di archiviazione specificato. passaggi di Hello variano leggermente in base che si utilizzi hello portale di Azure o Gestione risorse di Azure. procedura di Hello anche varia a seconda che la distribuzione di hello fa parte della creazione del cluster o per un cluster che esiste già. Esaminiamo i passaggi di hello per ogni scenario.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a>Distribuire l'estensione di diagnostica hello come parte della creazione del cluster tramite il portale di Azure
toodeploy hello diagnostica estensione toohello macchine virtuali in cluster hello come parte della creazione del cluster, utilizzare pannello impostazioni di diagnostica hello illustrato nell'esempio hello immagine, assicurarsi che la diagnostica è troppo**su** (hello l'impostazione predefinita) . Dopo aver creato il cluster hello, è possibile modificare queste impostazioni mediante il portale di hello.

![Impostazioni di diagnostica di Azure nel portale di hello per la creazione del cluster](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

Quando si crea un cluster tramite il portale di hello, si consiglia di scaricare il modello di hello **prima di scegliere OK** cluster hello toocreate. Per informazioni dettagliate, vedere troppo[configurazione di un cluster di Service Fabric utilizzando un modello di gestione risorse di Azure](service-fabric-cluster-creation-via-arm.md). È necessario toomake modifiche al modello hello in un secondo momento, poiché non è possibile apportare alcune modifiche tramite il portale di hello.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Distribuire l'estensione di diagnostica hello come parte della creazione del cluster usando Gestione risorse di Azure
toocreate un cluster usando Gestione risorse, è necessario tooadd hello diagnostica JSON toohello completo del cluster di gestione delle risorse modello di configurazione prima di creare cluster hello. Offriamo un modello di gestione risorse di esempio 5-VM cluster con configurazione di diagnostica aggiunti tooit come parte di esempi di gestione delle risorse modello. È possibile visualizzarlo in questa posizione nella raccolta di esempi di Azure hello: [cluster cinque nodi con il modello di gestione risorse diagnostica esempio](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).

impostazione di diagnostica hello toosee nel modello di gestione risorse di hello, file azuredeploy.json aprire hello e cercare **IaaSDiagnostics**. un cluster utilizzando questo modello, seleziona hello toocreate **distribuire tooAzure** pulsante disponibile all'indirizzo collegamento precedente hello.

In alternativa, è possibile scaricare Gestione risorse: esempio hello, apportare le modifiche tooit e creare un cluster con modello modificato hello utilizzando hello `New-AzureRmResourceGroupDeployment` comando in una finestra di PowerShell di Azure. Vedere hello seguente codice per i parametri di hello che viene passato nel comando toohello. Per informazioni dettagliate sul modo in cui raggruppare toodeploy una risorsa tramite PowerShell, vedere l'articolo hello [distribuire un gruppo di risorse con il modello di gestione risorse di Azure hello](../azure-resource-manager/resource-group-template-deploy.md).

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a>Distribuire cluster esistente tooan estensione diagnostica hello
Se si dispone di un cluster esistente che non dispone di diagnostica distribuita o se si desidera toomodify una configurazione esistente, è possibile aggiungere o aggiornare. Modificare modello di gestione risorse hello cluster esistente di hello toocreate usato o scaricare il modello di hello dal portale hello come descritto in precedenza. Modificare il file di template.json hello eseguendo hello seguenti attività.

Aggiungere un nuovo modello toohello risorse di archiviazione aggiungendo toohello sezione delle risorse.

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 Successivamente, aggiungere parametri toohello sezione subito dopo le definizioni account di archiviazione hello, tra `supportLogStorageAccountName` e `vmNodeType0Name`. Sostituire il testo segnaposto hello *nome account di archiviazione qui* con nome hello hello dell'account di archiviazione.

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
Quindi, aggiornare hello `VirtualMachineProfile` sezione del file template.json hello aggiungendo hello seguente codice all'interno della matrice estensioni hello. Essere tooadd che una virgola all'inizio di hello o alla fine di hello, a seconda di dove viene inserito.

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

Dopo aver modificato il file template.json hello come descritto, è possibile ripubblicare il modello di gestione risorse di hello. Se è stato esportato il modello di hello, l'esecuzione del file di deploy.ps1 hello Ripubblica modello hello. Dopo la distribuzione, assicurarsi che il valore di **ProvisioningState** sia **Succeeded**.

## <a name="collect-health-and-load-events"></a>Raccogliere gli eventi di integrità e di caricamento

A partire dalla versione di hello 5.4 di Service Fabric, gli eventi di metrica di integrità e carico sono disponibili per la raccolta. Questi eventi riflettono gli eventi generati dal sistema hello o il codice tramite integrità hello o caricare le API di creazione di report, ad esempio [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) o [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx). Ciò consente l'aggregazione e la visualizzazione dell'integrità del sistema nel tempo, nonché la generazione di avvisi in base a eventi di integrità o di caricamento. tooview questi eventi nel Visualizzatore eventi di diagnostica di Visual Studio aggiungere "Microsoft-ServiceFabric:4:0x4000000000000008" toohello elenco dei provider ETW.

eventi di hello toocollect, modificare hello Gestione risorse modello tooinclude

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="collect-reverse-proxy-events"></a>Raccogliere eventi del proxy inverso

A partire dalla versione di hello 5.7 dell'infrastruttura di servizio, [proxy inverso](service-fabric-reverseproxy.md) eventi sono disponibili per la raccolta.
Proxy inverso genera eventi in due canali, un errore che contiene gli eventi che riflettono richiedere gli errori di elaborazione e altro contenente gli eventi dettagliati su tutte le richieste di hello elaborati nel proxy inverso hello hello. 

1. Raccolta eventi di errore: tooview questi eventi nel Visualizzatore eventi di diagnostica di Visual Studio aggiungere "Microsoft-ServiceFabric:4:0x4000000000000010" toohello elenco dei provider ETW.
gli eventi di hello toocollect dal cluster di Azure, modificare hello Gestione risorse modello tooinclude

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387920",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

2. Raccogliere tutti gli eventi di elaborazione della richiesta: Visualizzatore eventi diagnostica In Visual Studio, aggiornamento voce hello Microsoft ServiceFabric hello elenco di provider ETW troppo "Microsoft-ServiceFabric:4:0x4000000000000020".
Per i cluster di Azure Service Fabric, modificare hello resource manager modello tooinclude

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387936",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```
> È consigliabile toojudiciously Abilita raccolta degli eventi da questo canale in quanto consente di raccogliere tutto il traffico tramite proxy inverso hello e può utilizzare rapidamente capacità di archiviazione.

Per i cluster di Azure Service Fabric, gli eventi di hello da tutti i nodi di hello vengono raccolti e aggregati in hello SystemEventTable.
Per risoluzione dei problemi degli eventi di proxy inverso hello dettagliata, fare riferimento hello [Guida di diagnostica proxy inverso](service-fabric-reverse-proxy-diagnostics.md).

## <a name="collect-from-new-eventsource-channels"></a>Eseguire la raccolta dai nuovi canali EventSource

log di toocollect tooupdate diagnostica da nuovi canali EventSource che rappresentano una nuova applicazione che è quasi toodeploy, eseguire hello stessi passaggi come descritto in precedenza per l'installazione di hello di diagnostica per un cluster esistente.

Aggiornare hello `EtwEventSourceProviderConfiguration` sezione nelle voci di hello template.json file tooadd per hello nuovi EventSource canali prima di applicare la configurazione hello aggiornare utilizzando hello `New-AzureRmResourceGroupDeployment` comando di PowerShell. nome di Hello dell'origine evento hello è definito come parte del codice nel file di Visual Studio generati ServiceEventSource.cs hello.

Ad esempio, se l'origine eventi è denominato My Eventsource, aggiungere hello dopo gli eventi di codice tooplace hello da My Eventsource in una tabella denominata MyDestinationTableName.

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

i contatori delle prestazioni toocollect o nei registri eventi, è possibile modificare il modello di gestione risorse di hello usando hello esempi forniti in [creare una macchina virtuale Windows con monitoraggio e diagnostica utilizzando un modello di gestione risorse di Azure](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Quindi, pubblicare di nuovo il modello di gestione risorse di hello.

## <a name="collect-performance-counters"></a>Raccogliere i contatori delle prestazioni

le metriche delle prestazioni toocollect dal cluster, aggiungere tooyour di contatori delle prestazioni di hello "WadCfg > DiagnosticMonitorConfiguration" nel modello di gestione risorse di hello per il cluster. Per informazioni sui contatori delle prestazioni che è consigliabile raccogliere, vedere l'articolo relativo ai [contatori delle prestazioni in Service Fabric](service-fabric-diagnostics-event-generation-perf.md).

Ad esempio, di seguito viene impostato un contatore di prestazioni, campionato ogni 15 secondi (questo comportamento può essere modificato e segue hello formato di "PT\<ora >\<unità >", ad esempio, PT3M sarebbe esempio a intervalli di tre minuti) e trasferiti toohello tabella di archiviazione appropriato ogni minuto.

  ```json
  "PerformanceCounters": {
      "scheduledTransferPeriod": "PT1M",
      "PerformanceCounterConfiguration": [
          {
              "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
              "sampleRate": "PT15S",
              "unit": "Percent",
              "annotation": [
              ],
              "sinks": ""
          }
      ]
  }
  ```
  
Se si utilizza un sink di Application Insights, come descritto nella seguente sezione hello e si desidera tooshow queste metriche in Application Insights, assicurarsi che nome di sink hello tooadd della sezione "sink" hello come illustrato in precedenza. Inoltre, è consigliabile creare toosend una tabella separata i contatori delle prestazioni, in modo che non troppi out hello hello di dati provenienti da altri canali di registrazione è stata abilitata.


## <a name="send-logs-tooapplication-insights"></a>Trasmissione registra informazioni dettagliate tooApplication

L'invio di dati di monitoraggio e diagnostica tooApplication Insights (AI) può essere eseguita come parte della configurazione di WAD hello. Se si decide di toouse per la visualizzazione e analisi degli eventi, leggere [analisi degli eventi e la visualizzazione con Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset un sink AI come parte del "WadCfg".

## <a name="next-steps"></a>Passaggi successivi

Dopo aver configurato correttamente diagnostica Windows Azure, verranno visualizzati dati nelle tabelle di archiviazione da hello ETW e i registri di EventSource. Se si sceglie toouse OMS, Kibana o qualsiasi altra dati analitica e la visualizzazione piattaforma che non viene configurata direttamente nel modello di gestione risorse di hello, apportare tooset che compongono la piattaforma hello di tooread la scelta hello dati da tali tabelle di archiviazione. Questa operazione in OMS è relativamente semplice ed è illustrata nell'articolo relativo all'[analisi di eventi e log tramite OMS](service-fabric-diagnostics-event-analysis-oms.md). Application Insights è un po' di un caso speciale in questo senso, poiché può essere configurato come parte della configurazione dell'estensione diagnostica hello, fare riferimento toohello [appropriato](service-fabric-diagnostics-event-analysis-appinsights.md) se si sceglie toouse AI.

>[!NOTE]
>Non è presente alcun modo toofilter o pulitura hello gli eventi inviati toohello tabella. Se si non implementa un tooremove di elaborare gli eventi dalla tabella hello, tabella hello continuerà toogrow. Attualmente è disponibile un esempio di un servizio di pulitura di dati in esecuzione in hello [esempio Watchdog](https://github.com/Azure-Samples/service-fabric-watchdog-service), è consigliabile scrivere uno per se stessi, a meno che non vi è un buon motivo per l'utente registri toostore oltre a un intervallo di 30 o 90 giorni.

* [Informazioni su come i contatori delle prestazioni toocollect o i registri tramite hello estensione di diagnostica](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) (Analisi e visualizzazione degli eventi con Application Insights)
* [Event Analysis and Visualization with OMS](service-fabric-diagnostics-event-analysis-oms.md) (Analisi e visualizzazione di eventi con OMS)
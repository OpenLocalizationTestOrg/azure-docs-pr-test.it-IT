---
title: aaaCollect log tramite diagnostica Azure | Documenti Microsoft
description: In questo articolo viene descritto come tooset di diagnostica Azure toocollect log da un cluster di Service Fabric in esecuzione in Azure.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 9f7e1fa5-6543-4efd-b53f-39510f18df56
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: afbcfbe972b1847ef33bf0539b4398794b1bd56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Raccogliere log con Diagnostica di Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Quando si esegue un cluster di Azure Service Fabric, è un log di hello buona toocollect da tutti i nodi di hello in una posizione centrale. La presenza di log hello in una posizione centrale consente di analizzare e risolvere i problemi del cluster, o problemi in applicazioni hello e servizi in esecuzione in tale cluster.

Tooupload un modo e raccogliere i log è toouse hello l'estensione diagnostica Azure, quali caricamenti registra tooAzure archiviazione, Azure Application Insights o hub eventi di Azure. i registri di Hello non sono utili direttamente nell'archiviazione o negli hub eventi. Ma è possibile utilizzare gli eventi di hello tooread un processo esterno dall'archivio e inserirli in un prodotto, ad esempio [Log Analitica](../log-analytics/log-analytics-service-fabric.md) o un'altra soluzione di analisi di log. In [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) è integrato un servizio completo di analisi e di ricerca dei log.

## <a name="prerequisites"></a>Prerequisiti
Utilizzare questi strumenti tooperform alcune delle operazioni di hello in questo documento:

* [Diagnostica di Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (correlata tooAzure servizi Cloud, ma con informazioni ed esempi)
* [Gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Client di Azure Resource Manager](https://github.com/projectkudu/ARMClient)
* [Modello di Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a>Origini di log che è possibile toocollect
* **I log di Service Fabric**: generato dai hello piattaforma toostandard traccia eventi per Windows (ETW) ed EventSource canali. I log possono essere di diversi tipi:
  * Gli eventi operativi: log per operazioni che hello Service Fabric piattaforma esegue. Gli esempi includono la creazione di applicazioni e servizi, le modifiche allo stato dei nodi e informazioni sull'aggiornamento.
  * [Eventi del modello di programmazione Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
  * [Eventi relativi al modello di programmazione Reliable Services](service-fabric-reliable-services-diagnostics.md)
* **Gli eventi dell'applicazione**: gli eventi generati dal codice del servizio e scritte usando classe helper di EventSource hello fornito nei modelli di Visual Studio hello. Per ulteriori informazioni sulla modalità di registrazione toowrite dall'applicazione, vedere [Monitor e diagnosticare i servizi in una configurazione di sviluppo locale](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Distribuire l'estensione diagnostica hello
Hello primo passaggio per la raccolta di log è l'estensione di diagnostica toodeploy hello in ognuna delle macchine virtuali di hello in cluster di Service Fabric hello. Hello estensione di diagnostica raccoglie i log in ogni macchina virtuale e li carica toohello account di archiviazione specificato. passaggi di Hello variano leggermente in base che si utilizzi hello portale di Azure o Gestione risorse di Azure. procedura di Hello anche varia a seconda che la distribuzione di hello fa parte della creazione del cluster o per un cluster che esiste già. Esaminiamo i passaggi di hello per ogni scenario.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a>Distribuire l'estensione di diagnostica hello come parte della creazione del cluster tramite il portale di hello
toodeploy hello diagnostica estensione toohello macchine virtuali in cluster hello come parte della creazione del cluster, utilizzare pannello impostazioni di diagnostica hello mostrato nella seguente immagine hello. tooenable Reliable Actors o servizi affidabili raccolta degli eventi, assicurarsi che la diagnostica sia impostata troppo**su** (hello l'impostazione predefinita). Dopo aver creato il cluster hello, è possibile modificare queste impostazioni mediante il portale di hello.

![Impostazioni di diagnostica di Azure nel portale di hello per la creazione del cluster](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

salve team di supporto tecnico di Azure *richiede* supporto registra toohelp risolvere tutte le richieste di supporto che si creano. Questi log vengono raccolti in tempo reale e vengono archiviati in uno degli account di archiviazione hello creato nel gruppo di risorse hello. le impostazioni di diagnostica Hello configurano gli eventi a livello di applicazione. Questi eventi includono [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) eventi, [servizi affidabili](service-fabric-reliable-services-diagnostics.md) eventi e alcuni toobe gli eventi di Service Fabric a livello di sistema archiviati in archiviazione di Azure.

I prodotti, ad esempio [Elasticsearch](https://www.elastic.co/guide/index.html) o un processo personalizzato è possibile ottenere gli eventi di hello dall'account di archiviazione hello. Non è presente alcun modo toofilter o pulitura hello gli eventi inviati toohello tabella. Se si non implementa un tooremove di elaborare gli eventi dalla tabella hello, tabella hello continuerà toogrow.

Quando si crea un cluster tramite il portale di hello, si consiglia di scaricare il modello di hello **prima di scegliere OK** cluster hello toocreate. Per informazioni dettagliate, vedere troppo[configurazione di un cluster di Service Fabric utilizzando un modello di gestione risorse di Azure](service-fabric-cluster-creation-via-arm.md). È necessario toomake modifiche al modello hello in un secondo momento, poiché non è possibile apportare alcune modifiche tramite il portale di hello.

È possibile esportare i modelli dal portale hello utilizzando hello alla procedura seguente. Tuttavia, questi modelli possono essere più difficile toouse perché potrebbe contengono valori null che mancano informazioni necessarie.

1. Aprire il gruppo di risorse.
2. Selezionare **impostazioni** toodisplay hello impostazioni del pannello.
3. Selezionare **distribuzioni** pannello della cronologia di distribuzione hello toodisplay.
4. Selezionare i dettagli hello toodisplay distribuzione su distribuzione hello.
5. Selezionare **Esporta modello** Pannello di toodisplay hello modello.
6. Selezionare **salvare toofile** tooexport un file con estensione zip che contiene il modello di hello, parametro e i file di PowerShell.

Dopo aver esportato il file hello, è necessario toomake una modifica. Modificare il file parameters.json hello e rimuovere hello **adminPassword** elemento. In questo modo la richiesta hello password durante l'esecuzione di script di distribuzione hello. Quando si esegue lo script di distribuzione hello, potrebbe essere toofix valori di parametro null.

hello toouse scaricati tooupdate modello una configurazione:

1. Estrarre la cartella di tooa hello contenuto nel computer locale.
2. Modificare hello contenuto tooreflect hello nuova configurazione.
3. Avviare PowerShell e modificare toohello cartella in cui è stato estratto il contenuto di hello.
4. Eseguire **deploy.ps1** e compilare hello sottoscrizione ID, nome del gruppo di risorse hello (utilizzare hello stessa configurazione del nome tooupdate hello) e un nome univoco di distribuzione.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Distribuire l'estensione di diagnostica hello come parte della creazione del cluster usando Gestione risorse di Azure
toocreate un cluster usando Gestione risorse, è necessario tooadd hello diagnostica JSON toohello completo del cluster di gestione delle risorse modello di configurazione prima di creare cluster hello. Offriamo un modello di gestione risorse di esempio 5-VM cluster con configurazione di diagnostica aggiunti tooit come parte di esempi di gestione delle risorse modello. È possibile visualizzarlo in questa posizione nella raccolta di esempi di Azure hello: [cluster cinque nodi con il modello di gestione risorse diagnostica esempio](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).

impostazione di diagnostica hello toosee nel modello di gestione risorse di hello, file azuredeploy.json aprire hello e cercare **IaaSDiagnostics**. un cluster utilizzando questo modello, seleziona hello toocreate **distribuire tooAzure** pulsante disponibile all'indirizzo collegamento precedente hello.

In alternativa, è possibile scaricare Gestione risorse: esempio hello, apportare le modifiche tooit e creare un cluster con modello modificato hello utilizzando hello `New-AzureRmResourceGroupDeployment` comando in una finestra di PowerShell di Azure. Vedere hello seguente codice per i parametri di hello che viene passato nel comando toohello. Per informazioni dettagliate sul modo in cui raggruppare toodeploy una risorsa tramite PowerShell, vedere l'articolo hello [distribuire un gruppo di risorse con il modello di gestione risorse di Azure hello](../azure-resource-manager/resource-group-template-deploy.md).

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

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

## <a name="update-diagnostics-toocollect-health-and-load-events"></a>Aggiornare gli eventi di integrità e carico toocollect diagnostica

A partire dalla versione di hello 5.4 di Service Fabric, gli eventi di metrica di integrità e carico sono disponibili per la raccolta. Questi eventi riflettono gli eventi generati dal sistema hello o il codice tramite integrità hello o caricare le API di creazione di report, ad esempio [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) o [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx). Ciò consente l'aggregazione e la visualizzazione dell'integrità del sistema nel tempo, nonché la generazione di avvisi in base a eventi di integrità o di caricamento. tooview questi eventi nel Visualizzatore eventi di diagnostica di Visual Studio aggiungere "Microsoft-ServiceFabric:4:0x4000000000000008" toohello elenco dei provider ETW.

eventi di hello toocollect, modificare hello resource manager modello tooinclude

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

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a>Aggiornare toocollect diagnostica e caricare i log dei nuovi canali EventSource
log di toocollect tooupdate diagnostica da nuovi canali EventSource che rappresentano una nuova applicazione che è quasi toodeploy, eseguire hello stessi passaggi come hello [precedente sezione](#deploywadarm) per l'installazione di diagnostica per un oggetto esistente cluster.

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

## <a name="next-steps"></a>Passaggi successivi
toounderstand in dettaglio gli eventi che è necessario cercare la risoluzione dei problemi, vedere gli eventi di diagnostica hello generati per [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) e [servizi affidabili](service-fabric-reliable-services-diagnostics.md).

## <a name="related-articles"></a>Articoli correlati
* [Informazioni su come i contatori delle prestazioni toocollect o i registri tramite hello estensione di diagnostica](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Soluzione Service Fabric in Log Analytics](../log-analytics/log-analytics-service-fabric.md)


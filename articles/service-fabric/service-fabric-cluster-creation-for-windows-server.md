---
title: un cluster di Azure Service Fabric autonomo aaaCreate | Documenti Microsoft
description: Creare un cluster di Azure Service Fabric su qualsiasi macchina (fisica o virtuale) che esegue Windows Server, sia locale che nel cloud.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik;dekapur
ms.openlocfilehash: 444970816290a0448d88a8b2082c75eb7a64cb44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a>Creare un cluster autonomo in esecuzione su Windows Server
È possibile utilizzare cluster di Service Fabric toocreate Azure Service Fabric in macchine virtuali o computer che eseguono Windows Server. In questo modo è possibile distribuire ed eseguire applicazioni di Service Fabric in qualsiasi ambiente che contenga un set di computer Windows Server interconnessi, in locale o con qualsiasi provider di cloud. Service Fabric fornisce un toocreate pacchetto di installazione che cluster di Service Fabric chiamato pacchetto di Windows Server autonomo hello.

In questo articolo vengono illustrati i passaggi hello per la creazione di un cluster di Service Fabric autonomo.

> [!NOTE]
> Questo pacchetto autonomo di Windows Server è disponibile in commercio e può essere usato per distribuzioni di produzione. Il pacchetto può contenere nuove funzionalità di Service Fabric in "Anteprima". Scorrere verso il basso troppo"[funzionalità incluse in questo pacchetto di anteprima](#previewfeatures_anchor)." sezione elenco hello delle funzionalità di anteprima hello. È possibile [scaricare una copia del contratto di licenza hello](http://go.microsoft.com/fwlink/?LinkID=733084) ora.
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a>Ottenere supporto per il pacchetto di Service Fabric per Windows Server hello
* Chiedi community hello pacchetto autonomo di hello Service Fabric per Windows Server in hello [forum di Azure Service Fabric](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).
* Aprire un ticket per ottenere il [supporto professionale per Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).  Altre informazioni sul supporto professionale Microsoft sono disponibili [qui](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).
* È possibile anche ottenere supporto per questo pacchetto come parte del [Supporto tecnico Microsoft Premier](https://support.microsoft.com/en-us/premier).
* Per altre informazioni vedere [Opzioni di supporto di Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).
* i registri toocollect per scopi di supporto, Esegui hello [servizio Fabric autonomo Log collector](service-fabric-cluster-standalone-package-contents.md).

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a>Scaricare il pacchetto di Service Fabric per Windows Server hello
cluster hello toocreate, utilizzare un pacchetto di Service Fabric per Windows Server hello (Windows Server 2012 R2 e versioni successive) disponibili qui: <br>
[Collegamento per il download - Pacchetto autonomo di Service Fabric - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)

Trovare i dettagli sul contenuto del pacchetto di hello [qui](service-fabric-cluster-standalone-package-contents.md).

pacchetto di runtime di Service Fabric Hello viene scaricato automaticamente al momento della creazione del cluster. Se la distribuzione da un computer non connessi toohello internet, scaricare il pacchetto di runtime hello fuori banda da qui: <br>
[Collegamento per il download - Runtime di Service Fabric - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)

Trovare esempi di configurazione di cluster autonomi in: <br>
[Esempi di configurazione di cluster autonomi](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a>Creare il cluster hello
Service Fabric può essere il cluster di sviluppo di una macchina tooa distribuito tramite hello *ClusterConfig.Unsecure.DevCluster.json* i file inclusi in [esempi](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).

Decomprimere macchina tooyour pacchetto di hello autonoma, copia hello esempio config file toohello locale, quindi esecuzione hello *CreateServiceFabricCluster.ps1* uno script tramite una sessione di PowerShell amministratore dal hello autonomo cartella del pacchetto:
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a>Passaggio 1A: creare un cluster di sviluppo locale non protetto
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

Vedere hello sezione di configurazione dell'ambiente alla [pianificare e preparare la distribuzione di cluster](service-fabric-cluster-standalone-deployment-preparation.md) dettagli della risoluzione dei problemi.

Se si sono terminato in esecuzione gli scenari di sviluppo, è possibile rimuovere il cluster di Service Fabric hello dalla macchina di hello riferendosi toosteps nella sezione "[rimuovere un cluster](#removecluster_anchor)". 

### <a name="step-1b-create-a-multi-machine-cluster"></a>Passaggio 1B: creare un cluster con più macchine
Dopo che sono già state completate tramite pianificazione hello e passaggi di preparazione dettagliate in hello di sotto di collegamento, si è pronti a toocreate il cluster di produzione usando il file di configurazione del cluster. <br>
[Pianificare e preparare la distribuzione del cluster](service-fabric-cluster-standalone-deployment-preparation.md)

1. Convalidare il file di configurazione hello è stato scritto eseguendo hello *TestConfiguration.ps1* script dalla cartella del pacchetto autonomo hello:  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    Verrà visualizzato un output simile al seguente: Se il campo inferiore hello "Superato" viene restituito come "True", i controlli di integrità sono stati superati e cluster hello Cerca toobe distribuibile in base alla configurazione di input hello.

    ```
    Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
    Running Best Practices Analyzer...
    Best Practices Analyzer completed successfully.
    
    LocalAdminPrivilege        : True
    IsJsonValid                : True
    IsCabValid                 : True
    RequiredPortsOpen          : True
    RemoteRegistryAvailable    : True
    FirewallAvailable          : True
    RpcCheckPassed             : True
    NoConflictingInstallations : True
    FabricInstallable          : True
    Passed                     : True
    ```

2. Creare il cluster hello: eseguire hello *CreateServiceFabricCluster.ps1* cluster di Service Fabric hello toodeploy script in ogni computer nella configurazione di hello. 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> Tracce di distribuzione vengono scritte toohello macchine Virtuali/computer in cui è stato eseguito uno script di PowerShell CreateServiceFabricCluster.ps1 hello. Questi sono disponibili nella sottocartella hello DeploymentTraces, basato su nella directory hello da quale hello è stato eseguito uno script. toosee se Service Fabric è stato distribuito correttamente tooa computer, trovare i file hello installato nella directory FabricDataRoot hello, come descritto in dettaglio nel file di configurazione del cluster hello sezione FabricSettings (per impostazione predefinita c:\ProgramData\SF). I processi FabricHost.exe e Fabric.exe possono essere visualizzati in esecuzione in Gestione attività.
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a>Passaggio 1C: Creare un cluster offline (non connesso a Internet)
pacchetto di runtime di Service Fabric Hello viene scaricato automaticamente al momento della creazione del cluster. Quando la distribuzione di un cluster di toomachines non connessi toohello internet, è necessario hello toodownload Service Fabric runtime pacchetto separatamente e fornire hello percorso tooit al momento della creazione del cluster.
possono essere scaricati separatamente mediante Hello runtime package, da un altro computer connesso toohello internet, in [collegamento Download - Runtime dell'infrastruttura del servizio - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354). Copiare hello runtime pacchetto toowhere la distribuzione di cluster non in linea di hello da e creare il cluster hello eseguendo `CreateServiceFabricCluster.ps1` con hello `-FabricRuntimePackagePath` parametro incluso, come illustrato di seguito: 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
dove `.\ClusterConfig.json` e `.\MicrosoftAzureServiceFabric.cab` sono rispettivamente di configurazione del cluster toohello percorsi hello e file CAB di runtime hello.


### <a name="step-2-connect-toohello-cluster"></a>Passaggio 2: Connettere il cluster di toohello
cluster sicuro tooa tooconnect, vedere [Service fabric connettersi cluster toosecure](service-fabric-connect-to-secure-cluster.md).

tooconnect tooan non sicuri cluster, eseguire il comando PowerShell seguente hello:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
Esempio:
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a>Passaggio 3: Visualizzare Service Fabric Explorer
Ora è possibile collegare toohello cluster con Service Fabric Explorer direttamente da uno dei computer hello http://localhost:19080/Explorer/index.html o in modalità remota con http://<*IPAddressofaMachine*>: 19080 / Explorer/index.HTML.

## <a name="add-and-remove-nodes"></a>Aggiungere e rimuovere ruoli
È possibile aggiungere o rimuovere i cluster di Service Fabric autonomo tooyour nodi come variare delle esigenze aziendali. Vedere [aggiungere o rimuovere nodi tooa Service Fabric autonomo cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) per i passaggi dettagliati.

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a>Rimuovere un cluster
tooremove un cluster, eseguire hello *RemoveServiceFabricCluster.ps1* dalla cartella del pacchetto hello e passare nel file di configurazione JSON toohello percorso hello uno script di PowerShell. È facoltativamente possibile specificare un percorso per il log di hello di eliminazione hello.

Questo script può essere eseguito su qualsiasi computer che dispone di amministratore accesso tooall hello computer elencati come nodi nel file di configurazione del cluster hello. macchina Hello che questo script viene eseguito in non è una parte del cluster hello toobe.

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a>Dati di telemetria raccolti e come tooopt esplicitamente
Per impostazione predefinita, prodotto hello raccoglie dati di telemetria del prodotto hello Service Fabric utilizzo tooimprove hello. Hello Best Practice Analyzer che viene eseguita come parte dell'installazione di hello verifica la presenza di connettività troppo[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1). Se non è raggiungibile, il programma di installazione di hello ha esito negativo a meno che non è rifiutare esplicitamente i dati di telemetria.

1. pipeline di dati di telemetria Hello tenta hello tooupload segue dati troppo[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) una volta al giorno. È un principio del best effort caricamento e non ha alcun impatto sulla funzionalità di cluster hello. dati di telemetria Hello viene inviato solo dal nodo hello che viene eseguito hello failover manager primario. Nessun altro nodo invia dati di telemetria.
2. telemetria Hello è costituita dai seguenti hello:

* Numero di servizi
* Numero di elementi ServiceTypes
* Numero di elementi Applications
* Numero di elementi ApplicationUpgrades
* Numero di elementi FailoverUnits
* Numero di elementi InBuildFailoverUnits
* Numero di elementi UnhealthyFailoverUnits
* Numero di elementi Replicas
* Numero di elementi InBuildReplicas
* Numero di elementi StandByReplicas
* Numero di elementi OfflineReplicas
* CommonQueueLength
* QueryQueueLength
* FailoverUnitQueueLength
* CommitQueueLength
* Numero di elementi Nodes
* IsContextComplete: True/False
* ClusterId: GUID generato casualmente per ogni cluster
* ServiceFabricVersion
* Indirizzo IP di macchina virtuale hello o computer dal quale hello vengono caricati dati di telemetria

dati di telemetria toodisable, aggiungere il seguente troppo di hello*proprietà* nella configurazione del cluster: *enableTelemetry: false*.

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a>Funzionalità di anteprima incluse in questo pacchetto
Nessuna.


> [!NOTE]
> A partire da hello nuovo [versione GA di cluster autonomi hello per Windows Server (versione 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), è possibile aggiornare le versioni di toofuture cluster, manualmente o automaticamente. Fare riferimento troppo[aggiornare una versione di cluster di Service Fabric autonomo](service-fabric-cluster-upgrade-windows-server.md) per informazioni dettagliate.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* [Distribuire e rimuovere applicazioni con PowerShell](service-fabric-deploy-remove-applications.md)
* [Impostazioni di configurazione per un cluster autonomo in Windows](service-fabric-cluster-manifest.md)
* [Aggiungere o rimuovere nodi tooa autonoma dell'infrastruttura del servizio cluster](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [Aggiornare il cluster autonomo di Service Fabric in Windows Server](service-fabric-cluster-upgrade-windows-server.md)
* [Creare un cluster di Service Fabric autonomo con VM di Azure che eseguono Windows](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [Proteggere un cluster autonomo in Windows tramite la funzionalità di sicurezza di Windows](service-fabric-windows-cluster-windows-security.md)
* [Proteggere un cluster autonomo in Windows con certificati X.509](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png

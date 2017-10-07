---
title: aaaUpgrade autonoma Azure Service Fabric del cluster in Windows Server | Documenti Microsoft
description: "Aggiornare il codice di Azure Service Fabric hello e/o di configurazione che esegue un cluster di Service Fabric autonomo, inclusa l'impostazione di modalità di aggiornamento di cluster hello."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 5132795e544b6f0185accedbf5092dcaafd66df0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a>Aggiornare il cluster autonomo di Azure Service Fabric in Windows Server
> [!div class="op_single_selector"]
> * [Cluster di Azure](service-fabric-cluster-upgrade.md)
> * [Cluster autonomo](service-fabric-cluster-upgrade-windows-server.md)
>
>

Per qualsiasi sistema moderna, hello possibilità tooupgrade è un successo a lungo termine toohello chiave del prodotto. Un cluster di Azure Service Fabric è una risorsa di cui si è proprietari. Questo articolo descrive come è possibile assicurarsi che cluster hello viene sempre eseguito versioni supportate di codice dell'infrastruttura di servizio e configurazioni.

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a>Versione di Service Fabric hello di controllo che esegue il cluster
tooset Aggiorna toodownload il cluster di Service Fabric quando Microsoft rilascia una nuova versione, set hello **fabricClusterAutoupgradeEnabled** tootrue di configurazione del cluster. una versione supportata di Service Fabric che si desidera il toobe cluster sul set hello tooselect **fabricClusterAutoupgradeEnabled** toofalse di configurazione del cluster.

> [!NOTE]
> Verificare che il cluster esegua sempre una versione di Service Fabric supportata. Quando Microsoft annuncia versione hello di una nuova versione di Service Fabric, la versione precedente di hello viene contrassegnata per la fine del supporto dopo un minimo di 60 giorni dalla data di hello annuncio hello. Le nuove versioni vengono annunciate [sul blog del team di Service Fabric hello](https://blogs.msdn.microsoft.com/azureservicefabric/). nuova versione di Hello è toochoose disponibili a questo punto.
>
>

È possibile aggiornare la nuova versione di toohello cluster solo se si utilizza una configurazione di nodi di stile di produzione, in cui ogni nodo di Service Fabric è allocato in una macchina virtuale o fisico separato. Se si dispone di un cluster di sviluppo, più di un nodo di Service Fabric in cui è in un unico computer fisico o macchina virtuale, è necessario creare nuovamente il cluster hello con la nuova versione di hello.

Due flussi di lavoro distinti è possibile aggiornare la versione più recente di toohello cluster o una versione supportata di Service Fabric. Un flusso di lavoro è per i cluster con versione più recente di connettività toodownload hello automaticamente. Hello altro flusso di lavoro è per i cluster che non dispone di connettività toodownload hello Service Fabric più recente.

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a>Aggiornare i cluster con configurazione e il codice più recente di connettività toodownload hello
Utilizzare la versione di tooa supportato cluster tooupgrade questi passaggi se i nodi del cluster dispongono di connettività Internet troppo[http://download.microsoft.com](http://download.microsoft.com).

Per i cluster che dispone della connettività troppo[http://download.microsoft.com](http://download.microsoft.com), Microsoft controlla periodicamente per la disponibilità di nuove versioni di Service Fabric hello.

Quando una nuova versione di Service Fabric è disponibile, il pacchetto di hello venga scaricato localmente toohello cluster e il provisioning per l'aggiornamento. Inoltre, cliente di hello tooinform di questa nuova versione, sistema hello Mostra cluster esplicita integrità di un avviso è simile toohello seguenti:

"supporto della versione [versione #] cluster corrente hello termina [Date]".

Dopo che il cluster hello è in esecuzione la versione più recente di hello, avviso hello è stata risolta.

#### <a name="cluster-upgrade-workflow"></a>Flusso di lavoro per l'aggiornamento del cluster
Dopo aver visualizzato l'avviso di integrità del cluster di hello, hello seguenti:

1. Connettere il cluster di toohello da qualsiasi computer che dispone di amministratore accesso tooall hello computer elencati come nodi cluster hello. macchina Hello che questo script viene eseguito in non è una parte del cluster hello toobe.

    ```powershell

    ###### connect toohello secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. Ottenere l'elenco di hello delle versioni di Service Fabric che è possibile eseguire l'aggiornamento.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    È necessario ottenere un toothis simili di output:

    ![ottenere versioni di Fabric][getfabversions]
3. Avviare una versione di cluster tooan aggiornamento disponibile tramite il [inizio ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) cmd di PowerShell.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   toomonitor hello lo stato di avanzamento dell'aggiornamento di hello, è possibile utilizzare Service Fabric Explorer o hello esecuzione comando di Windows PowerShell seguente.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Se non vengono soddisfatti i criteri di integrità del cluster di hello, viene eseguito il rollback di aggiornamento hello. criteri di integrità personalizzato toospecify per hello **inizio ServiceFabricClusterUpgrade** command, vedere la documentazione per [inizio ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).

Dopo aver risolto i problemi di hello che ha comportato il rollback di hello, avviare nuovamente l'aggiornamento di hello hello seguente procedura come descritto in precedenza.

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a>Aggiornare i cluster che presentano <U>nessuna connettività</u> codice più recente di toodownload hello e la configurazione
Utilizzare la versione di tooa supportato cluster tooupgrade questi passaggi se i nodi del cluster non dispongono di connettività Internet troppo[http://download.microsoft.com](http://download.microsoft.com).

> [!NOTE]
> Se si utilizza un cluster che non è connesso toohello Internet, sarà necessario toolearn toomonitor hello Service Fabric team blog su una nuova versione. sistema di Hello non viene visualizzato un tooalert di avviso di integrità del cluster di una nuova versione.  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a>Confronto tra provisioning automatico e provisioning manuale
tooenable il download automatico e la registrazione per la versione del codice più recente hello, configurare l'aggiornamento dell'infrastruttura del servizio. Fare riferimento toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt all'interno di hello [pacchetto autonomo](service-fabric-cluster-standalone-package-contents.md) per le istruzioni.
Per un processo manuale, istruzioni hello riportato di seguito.

Modificare il hello tooset configurazione di cluster seguendo toofalse proprietà prima di avviare un aggiornamento della configurazione.

        "fabricClusterAutoupgradeEnabled": false,

Fare riferimento troppo[cmd PS inizio ServiceFabricClusterConfigurationUpgrade ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) per informazioni dettagliate sull'utilizzo. Verificare che tooupdate 'clusterConfigurationVersion' nel file JSON prima di iniziare l'aggiornamento della configurazione hello.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a>Flusso di lavoro per l'aggiornamento del cluster

1. Eseguire Get-ServiceFabricClusterUpgrade da uno dei nodi cluster hello hello e prendere nota di hello TargetCodeVersion.
2. Seguente hello esecuzione da un toolist computer connesso internet tutti aggiornare le versioni compatibili con la versione corrente di hello e scaricare hello pacchetto dai collegamenti di download associati hello corrispondente.

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. Connettere il cluster di toohello da qualsiasi computer che dispone di amministratore accesso tooall hello computer elencati come nodi cluster hello. macchina Hello che questo script viene eseguito in non è una parte del cluster di hello toobe

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. Copiare il pacchetto scaricato hello nell'archivio di immagini cluster hello.

5. Registrare il pacchetto copiato hello.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. Avviare una versione di cluster tooan aggiornamento disponibile.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   È possibile monitorare lo stato di avanzamento hello dell'aggiornamento hello in Service Fabric Explorer o è possibile eseguire il comando PowerShell seguente hello.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Se non vengono soddisfatti i criteri di integrità del cluster di hello, viene eseguito il rollback di aggiornamento hello. criteri di integrità personalizzato toospecify per hello **inizio ServiceFabricClusterUpgrade** command, vedere la documentazione di hello per [inizio ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).

Dopo aver risolto i problemi di hello che ha comportato il rollback di hello, avviare nuovamente l'aggiornamento di hello hello seguente procedura come descritto in precedenza.


## <a name="upgrade-hello-cluster-configuration"></a>Aggiorna la configurazione del cluster hello
Prima di iniziare l'aggiornamento della configurazione hello, è possibile testare il nuovo json di configurazione del cluster eseguendo uno script di powershell hello in pacchetto autonomo hello.

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
oppure

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

Alcune configurazioni non possono essere aggiornate, ad esempio gli endpoint, il nome del cluster, l'IP del nodo e così via. Questo test hello nuovo cluster configurazione json rispetto hello precedente e generano errori nella finestra di Powershell hello se è presente alcun problema.

l'aggiornamento della configurazione cluster hello tooupgrade, eseguire **inizio ServiceFabricClusterConfigurationUpgrade**. l'aggiornamento della configurazione Hello è elaborato aggiornamento del dominio dal dominio di aggiornamento.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a>Aggiornamento della configurazione del certificato del cluster  
Il certificato del cluster viene utilizzato per l'autenticazione tra i nodi del cluster, in modo rollover del certificato hello deve essere eseguita con prestare particolare attenzione perché verrà bloccata la comunicazione hello tra i nodi del cluster.  
Tecnicamente, sono supportate tre opzioni:  

1. Aggiornamento singolo certificato: percorso di aggiornamento hello ' certificato (primaria) -> B certificato (primaria) -> C certificato (primaria) ->... '.   
2. Double aggiornamento certificati: percorso di aggiornamento hello ' certificato -> (principale) del certificato (primaria) e B (secondario) -> B certificato (primaria) -> B certificato (primaria) e C (secondario) -> C certificato (primaria) ->... '.
3. Aggiornamento del tipo di certificato: configurazione dei certificati basati su identificazione personale <-> configurazione dei certificati basati su CommonName. Ad esempio, identificazione personale del certificato A (primario) e identificazione personale B (secondario) -> CommonName del certificato C.


## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come toocustomize alcuni [impostazioni cluster di Service Fabric](service-fabric-cluster-fabric-settings.md).
* Informazioni su come troppo[aumentare e ridurre il cluster](service-fabric-cluster-scale-up-down.md).
* Informazioni su come eseguire [aggiornamenti dell'applicazione](service-fabric-application-upgrade.md).

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG

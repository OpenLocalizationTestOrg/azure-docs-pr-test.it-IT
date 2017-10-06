---
title: aaaAdd o rimuovere nodi tooa autonomo cluster di Service Fabric | Documenti Microsoft
description: "Informazioni su come tooadd o rimuovere nodi tooan Azure Service Fabric cluster in un computer fisico o macchina virtuale che esegue Windows Server, che può essere locale o in qualsiasi cloud."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a>Aggiungere o rimuovere nodi tooa autonomo Service Fabric cluster che esegue Windows Server
Dopo aver [creato il cluster di Service Fabric autonomo nei computer Windows Server](service-fabric-cluster-creation-for-windows-server.md), possono modificare le esigenze aziendali e potrebbe essere necessario tooadd o rimuovere nodi tooyour cluster. Questo articolo fornisce i passaggi dettagliati tooachieve questo. Si noti che la funzionalità di aggiunta o rimozione di nodi non è supportata nei cluster di sviluppo locali.

## <a name="add-nodes-tooyour-cluster"></a>Aggiungere nodi tooyour cluster
1. Preparazione hello VM/macchina da tooadd tooyour cluster seguendo i passaggi di hello indicati in hello [hello Prepara computer prerequisiti hello toomeet per la distribuzione di cluster](service-fabric-cluster-creation-for-windows-server.md) sezione
2. Identificare il dominio di errore e dominio di aggiornamento si corso tooadd la macchina virtuale/macchina
3. Desktop remoto (RDP) nella macchina virtuale o computer che si desidera che il cluster di toohello tooadd hello
4. Copia o [download del pacchetto autonomo hello per Service Fabric per Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/macchina e decomprimere il pacchetto di hello
5. Esecuzione di Powershell con privilegi elevati e passare toohello percorso del pacchetto decompresso hello
6. Eseguire hello *AddNode.ps1* script con i parametri di hello che descrivono hello nuovo nodo tooadd. esempio Hello seguente aggiunge un nuovo nodo denominato VM5, con il tipo NodeType0 e un indirizzo IP, 182.17.34.52 in UD1 e fd: / dc1/r0. Hello *ExistingClusterConnectionEndPoint* è già un endpoint della connessione per un nodo nel cluster esistente hello, che può essere l'indirizzo IP hello del *qualsiasi* nodo cluster hello.

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    Al termine dell'esecuzione dello script hello, è possibile verificare se è stato aggiunto il nuovo nodo di hello eseguendo hello [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.

7. tooensure la coerenza tra i diversi nodi cluster hello, è necessario avviare un aggiornamento della configurazione. Eseguire [Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello file di configurazione più recente e aggiungere hello appena aggiunta nodo troppo sezione "Nodi". È inoltre consigliabile tooalways hanno hello configurazione più recente del cluster disponibile in caso di hello che è necessario un cluster con hello tooredploy stessa configurazione.

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. Eseguire [inizio ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) aggiornamento hello toobegin.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    È possibile monitorare lo stato di avanzamento hello dell'aggiornamento hello in Service Fabric Explorer. In alternativa è possibile eseguire [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps).

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a>Aggiunta di nodi tooclusters configurato con la sicurezza di Windows utilizzando l'account
Per i cluster configurati con un account del servizio gestito del gruppo (gMSA, Group Managed Service Account) (https://technet.microsoft.com/library/hh831782.aspx) è possibile aggiungere un nuovo nodo con un aggiornamento della configurazione:
1. Eseguire [Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) in uno dei nodi esistenti hello tooget hello file di configurazione più recente e aggiungere i dettagli sul nuovo nodo hello desiderato tooadd nella sezione dei nodi"hello". Verificare che il nuovo nodo hello fa parte di hello stesso account gestito di gruppo. Questo account deve essere un account Administrator su tutti i computer.

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. Eseguire [inizio ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) aggiornamento hello toobegin.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    È possibile monitorare lo stato di avanzamento hello dell'aggiornamento hello in Service Fabric Explorer. In alternativa è possibile eseguire [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps).

### <a name="add-node-types-tooyour-cluster"></a>Aggiungere cluster tooyour tipi di nodo
In ordine tooadd un nuovo tipo di nodo, modificare il configurazione tooinclude hello nuovo tipo di nodo nella sezione "NodeTypes" in "Proprietà" e iniziare una configurazione di eseguire l'aggiornamento utilizzando [inizio ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps). Una volta completato l'aggiornamento di hello, è possibile aggiungere nuovo cluster di nodi tooyour con questo tipo di nodo.

## <a name="remove-nodes-from-your-cluster"></a>Rimuovere nodi dal cluster
Un nodo può essere rimosso da un cluster con un aggiornamento della configurazione, nel seguente modo hello:

1. Eseguire [Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) file di configurazione più recente di tooget hello e *rimuovere* nodo hello dalla sezione "Nodi".
Aggiungere "NodesToBeRemoved" hello parametro troppo "configurazione" sezione all'interno di sezione "FabricSettings". Hello "value" deve essere un elenco separato da virgole di nomi di nodo di nodi che devono toobe rimosso.

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. Eseguire [inizio ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) aggiornamento hello toobegin.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    È possibile monitorare lo stato di avanzamento hello dell'aggiornamento hello in Service Fabric Explorer. In alternativa è possibile eseguire [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps).

> [!NOTE]
> È possibile che con la rimozione di nodi vengano avviati più aggiornamenti in sequenza. Alcuni nodi sono contrassegnati con `IsSeedNode=”true”` tag e può essere identificato tramite l'esecuzione di query cluster hello manifesto utilizzando `Get-ServiceFabricClusterManifest`. La rimozione di tali nodi può richiedere più tempo rispetto ad altri poiché dispongono di nodi seme hello toobe spostati in tali scenari. cluster Hello devono mantenere un minimo di 3 nodi di tipo di nodo primario.
> 
> 

### <a name="remove-node-types-from-your-cluster"></a>Rimuovere i tipi di nodi dal cluster
Prima di rimuovere un tipo di nodo, verificare se sono presenti nodi che fanno riferimento a tipo di nodo hello. Rimuovere questi nodi prima di rimuovere il tipo di nodo corrispondente hello. Dopo aver rimosso tutti i nodi corrispondenti, è possibile rimuovere hello NodeType dalla configurazione del cluster hello e una configurazione di iniziare l'aggiornamento utilizzando [inizio ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).


### <a name="replace-primary-nodes-of-your-cluster"></a>Sostituire i nodi primari del cluster
sostituzione di Hello dei nodi primari deve essere un nodo eseguito dopo l'altro, invece di rimuovere e quindi aggiungere in batch.


## <a name="next-steps"></a>Passaggi successivi
* [Impostazioni di configurazione per un cluster autonomo in Windows](service-fabric-cluster-manifest.md)
* [Proteggere un cluster autonomo in Windows con certificati X.509](service-fabric-windows-cluster-x509-security.md)
* [Creare un cluster di Service Fabric autonomo con VM di Azure che eseguono Windows](service-fabric-cluster-creation-with-windows-azure-vms.md)


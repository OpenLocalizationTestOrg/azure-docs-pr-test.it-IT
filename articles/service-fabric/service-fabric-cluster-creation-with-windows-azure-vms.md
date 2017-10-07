---
title: un computer autonomo aaaCreate cluster con macchine virtuali di Azure che eseguono Windows | Documenti Microsoft
description: Informazioni su come toocreate e gestire un cluster di Azure Service Fabric in macchine virtuali di Azure che esegue Windows Server.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a>Creare un cluster di Service Fabric autonomo a tre nodi con macchine virtuali di Azure che eseguono Windows Server
In questo articolo viene descritto come toocreate un cluster basato su Windows Azure macchine virtuali (VM), utilizzando hello programma di installazione autonomo Service Fabric per Windows Server. scenario Hello è un caso speciale di [creare e gestire un cluster che esegue Windows Server](service-fabric-cluster-creation-for-windows-server.md) in cui le macchine virtuali hello sono [macchine virtuali di Azure che esegue Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), anche se non si sta creando [un Azure cluster basato su cloud di Service Fabric](service-fabric-cluster-creation-via-portal.md). distinzione di Hello nei seguenti di questo modello è tale cluster di Service Fabric autonomo hello creati hello alla procedura seguente viene gestito interamente dall'utente, mentre hello Azure basato su cloud Service Fabric cluster gestiti e aggiornata da hello Service Fabric provider di risorse.

## <a name="steps-toocreate-hello-standalone-cluster"></a>Cluster di passaggi toocreate hello autonomo
1. Accedi toohello portale di Azure e creare un nuovo Windows Server 2012 R2 Datacenter o macchina virtuale di Windows Server 2016 Data Center in un gruppo di risorse. Leggere l'articolo hello [creare una macchina virtuale di Windows nel portale di Azure hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) per altri dettagli.
2. Aggiungere due ulteriori toohello di macchine virtuali nello stesso gruppo di risorse. Verificare che ciascuna delle macchine virtuali hello è hello stesso nome utente dell'amministratore e una password quando viene creato. Dopo la creazione, si noterà che tutte le tre macchine virtuali in hello stessa rete virtuale.
3. Connettersi tooeach di hello macchine virtuali e disattivare hello Windows Firewall utilizzando hello [Server Manager, il dashboard di Server locale](https://technet.microsoft.com/library/jj134147.aspx). In questo modo si garantisce che il traffico di rete hello può comunicare tra le macchine hello. Durante la macchina tooeach connesso, ottenere l'indirizzo IP hello aprendo un prompt dei comandi e digitando `ipconfig`. In alternativa è possibile visualizzare hello IP indirizzo di ogni computer nel portale di hello, selezionando hello risorsa di rete virtuale per il gruppo di risorse hello e controllando le interfacce di rete hello create per ognuno di questi computer.
4. Connettersi tooone di hello macchine virtuali e i test che è possibile effettuare il ping hello altri due macchine virtuali correttamente.
5. Connettersi tooone di hello macchine virtuali e [download del pacchetto di Service Fabric di hello autonomo per Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) in una nuova cartella hello computer ed estrarre il pacchetto di hello.
6. Aprire hello *ClusterConfig.Unsecure.MultiMachine.json* file nel blocco note e modificare ogni nodo con gli indirizzi IP hello tre macchine hello. Modificare il nome del cluster hello nella parte superiore di hello e salvare file hello.  Un esempio parziale hello del manifesto del cluster è illustrato di seguito.
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. Se si prevede un cluster protetto questo toobe, decidere di misura di sicurezza hello desideri toouse e seguire i passaggi di hello in hello associata collegamento: [certificato X509](service-fabric-windows-cluster-x509-security.md) o [la sicurezza di Windows](service-fabric-windows-cluster-windows-security.md). Se si imposta la sicurezza di Windows del cluster di hello, occorre tooset backup un toomanage di controller di dominio Active Directory. Si noti che l'uso di un computer controller di dominio come nodo di Service Fabric non è supportato.
8. Aprire una [finestra di PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise). Passare toohello cartella in cui si estratti pacchetto di installazione autonomo scaricato hello e salvata i file di configurazione del cluster hello. Eseguire hello cluster hello toodeploy comando di PowerShell seguente:
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

script di Hello configurerà in modalità remota i cluster di Service Fabric hello e devono segnalare lo stato di avanzamento come distribuzione transita in.

9. Dopo circa un minuto, è possibile verificare se il cluster hello è operativo connettendosi toohello Service Fabric Explorer utilizzando uno degli IP della macchina hello indirizzi, ad esempio tramite `http://10.1.0.5:19080/Explorer/index.html`. 

## <a name="next-steps"></a>Passaggi successivi
* [Creare cluster autonomi di Service Fabric in Windows Server o Linux](service-fabric-deploy-anywhere.md)
* [Aggiungere o rimuovere nodi tooa autonoma dell'infrastruttura del servizio cluster](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [Impostazioni di configurazione per un cluster autonomo in Windows](service-fabric-cluster-manifest.md)
* [Proteggere un cluster autonomo in Windows tramite la funzionalità di sicurezza di Windows](service-fabric-windows-cluster-windows-security.md)
* [Proteggere un cluster autonomo in Windows con certificati X.509](service-fabric-windows-cluster-x509-security.md)


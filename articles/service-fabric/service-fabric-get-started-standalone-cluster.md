---
title: aaaSet di un cluster di Azure Service Fabric autonomo | Documenti Microsoft
description: "Creare un cluster di sviluppo autonomo con tre nodi in esecuzione su hello stesso computer. Dopo aver completato il programma di installazione, sarà possibile toocreate un cluster con più computer."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/06/2017
ms.author: dekapur
ms.openlocfilehash: e4d0ea9fc3b8475160bd8ed19fd3716463791cc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a>Creare il primo cluster autonomo di Service Fabric
È possibile creare un cluster di Service Fabric autonomi in macchine virtuali o computer che eseguono Windows Server 2012 R2 o Windows Server 2016, locale o nel cloud hello. Questa Guida rapida consente di un cluster di sviluppo autonomo toocreate solo alcuni minuti.  Al termine si ottiene un cluster di tre nodi in esecuzione in un singolo computer nel quale è possibile distribuire app.

## <a name="before-you-begin"></a>Prima di iniziare
Service Fabric fornisce un programma di installazione di cluster autonomi di pacchetto toocreate Service Fabric.  [Scaricare il pacchetto di installazione di hello](http://go.microsoft.com/fwlink/?LinkId=730690).  Decomprimere hello pacchetto tooa cartella di installazione nel computer di hello o macchina virtuale in cui si configura il cluster di sviluppo hello.  contenuto Hello hello del pacchetto di installazione è descritti in dettaglio [qui](service-fabric-cluster-standalone-package-contents.md).

amministrazione di cluster Hello distribuzione e configurazione dei cluster hello deve disporre dei privilegi di amministratore sul computer di hello. Non è possibile installare Service Fabric in un controller di dominio.

## <a name="validate-hello-environment"></a>Convalidare hello ambiente
Hello *TestConfiguration.ps1* script nel pacchetto autonomo hello viene utilizzato come una migliore toovalidate Analizzatore procedure consigliate, se un cluster può essere distribuito in un determinato ambiente. [Preparazione della distribuzione](service-fabric-cluster-standalone-deployment-preparation.md) elenchi hello i prerequisiti e requisiti dell'ambiente. Eseguire hello script tooverify se è possibile creare cluster di sviluppo hello:

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-hello-cluster"></a>Creare il cluster hello
Diversi file di configurazione del cluster di esempio vengono installati con il pacchetto di installazione di hello. *ClusterConfig.Unsecure.DevCluster.json* è più semplice configurazione del cluster hello: un cluster non sicuro, tre nodi in esecuzione in un singolo computer.  Altri file di configurazione descrivono cluster con una o più macchine virtuali protetti con la sicurezza di Windows o certificati X.509.  Non necessari toomodify le impostazioni di configurazione di hello predefinito per questa esercitazione, ma esaminare il file di configurazione hello e acquisire familiarità con le impostazioni di hello.  Hello **nodi** sezione vengono descritte hello in tre nodi di cluster hello: nome, indirizzo IP, [tipo di nodo, dominio di errore e dominio di aggiornamento](service-fabric-cluster-manifest.md#nodes-on-the-cluster).  Hello **proprietà** sezione definisce hello [sicurezza, livello di affidabilità, raccolta di dati diagnostici e tipi di nodi](service-fabric-cluster-manifest.md#cluster-properties) per cluster hello.

Questo cluster è senza protezione.  Chiunque si può connettere in modo anonimo ed eseguire operazioni di gestione. È quindi necessario proteggere sempre i cluster di produzione usando certificati X.509 o la sicurezza di Windows.  Al momento della creazione del cluster viene configurata solo la sicurezza e non è possibile tooenable sicurezza dopo la creazione di cluster hello.  Lettura [proteggere un cluster](service-fabric-cluster-security.md) toolearn ulteriori informazioni sulla protezione del cluster di Service Fabric.  

toocreate hello sviluppo tre nodi cluster, eseguire hello *CreateServiceFabricCluster.ps1* script da una sessione di PowerShell di amministratore:

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

pacchetto di runtime di Service Fabric Hello viene automaticamente scaricato e installato al momento della creazione del cluster.

## <a name="connect-toohello-cluster"></a>Connettere il cluster toohello
Il cluster di sviluppo di tre nodi è ora in esecuzione. Hello modulo ServiceFabric di PowerShell viene installato con il runtime di hello.  È possibile verificare tale cluster hello è in esecuzione da hello stesso computer o da un computer remoto con il runtime di Service Fabric hello.  Hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet stabilisce un cluster di toohello di connessione.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
Vedere [Connetti tooa sicura cluster](service-fabric-connect-to-secure-cluster.md) per altri esempi di connessione tooa cluster. Dopo la connessione toohello cluster, utilizzare hello [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay cmdlet un elenco di nodi nelle informazioni del cluster e lo stato di hello per ogni nodo. **HealthState** deve essere *OK* per ogni nodo.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>Visualizzare i cluster hello tramite Service Fabric explorer
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) rappresenta un ottimo strumento per la visualizzazione del cluster e la gestione delle applicazioni.  Service Fabric Explorer è un servizio che viene eseguito in un cluster di hello, che si accede tramite un browser passando troppo[http://localhost:19080/Esplora](http://localhost:19080/Explorer). 

dashboard del cluster Hello viene fornita una panoramica del cluster, incluso un riepilogo dell'applicazione e l'integrità del nodo. visualizzazione del nodo Hello Mostra struttura fisica di hello del cluster di hello. Per un determinato nodo, è possibile esaminare le applicazioni con il codice distribuito in quel nodo.

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-hello-cluster"></a>Rimuovere il cluster hello
tooremove un cluster, eseguire hello *RemoveServiceFabricCluster.ps1* dalla cartella del pacchetto hello e passare nel file di configurazione JSON toohello percorso hello uno script di PowerShell. È facoltativamente possibile specificare un percorso per il log di hello di eliminazione hello.

```powershell
# Removes Service Fabric cluster nodes from each computer in hello configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

runtime di Service Fabric tooremove hello dal computer di hello, eseguire lo script di PowerShell seguente dalla cartella del pacchetto hello hello.

```powershell
# Removes Service Fabric from hello current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a>Passaggi successivi
Una volta impostati un cluster di sviluppo autonomo, provare hello seguenti articoli:
* [Configurare un cluster autonomo con più computer](service-fabric-cluster-creation-for-windows-server.md) e abilitare la sicurezza.
* [Distribuire le app tramite PowerShell](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png

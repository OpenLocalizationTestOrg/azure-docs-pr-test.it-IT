---
title: Pacchetto autonomo dell'infrastruttura del servizio per Windows Server aaaAzure | Documenti Microsoft
description: Descrizione e il contenuto del pacchetto di hello Azure Service Fabric autonoma per Windows Server.
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik
ms.openlocfilehash: e4c6cb9128d659144e559fcad06bb78c9969dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="contents-of-service-fabric-standalone-package-for-windows-server"></a>Contenuto del pacchetto autonomo di Service Fabric per Windows Server
In hello [scaricato](http://go.microsoft.com/fwlink/?LinkId=730690) pacchetto autonomo dell'infrastruttura del servizio, si noterà hello i seguenti file:

| **Nome file** | **Descrizione breve** |
| --- | --- |
| CreateServiceFabricCluster.ps1 |Uno script di PowerShell che consente di creare cluster hello utilizzando le impostazioni di hello Clusterconfig. |
| RemoveServiceFabricCluster.ps1 |Uno script di PowerShell che consente di rimuovere un cluster usando le impostazioni di hello nelle Clusterconfig. |
| AddNode.ps1 |Uno script di PowerShell per l'aggiunta di un nodo di tooan esistente distribuito cluster sul computer corrente hello. |
| RemoveNode.ps1 |Uno script di PowerShell per la rimozione di un nodo da un oggetto esistente distribuito cluster dal computer corrente hello. |
| CleanFabric.ps1 |Uno script di PowerShell per la pulizia di un'installazione di Service Fabric macchina corrente hello autonoma. Le installazioni MSI precedenti devono essere rimosse usando i programmi di disinstallazione associati. |
| TestConfiguration.ps1 |Uno script di PowerShell per l'analisi dell'infrastruttura di hello come specificato in hello Cluster.json. |
| DownloadServiceFabricRuntimePackage.ps1 |Uno script di PowerShell utilizzato per il download del pacchetto di runtime più recente di hello fuori banda, per gli scenari in cui hello distribuzione macchina non è connesso toohello internet. |
| DeploymentComponentsAutoextractor.exe |Archivio contenente i componenti di distribuzione autoestraente utilizzato da hello script pacchetto autonomo. |
| EULA_ENU.txt |condizioni di licenza Hello per hello l'utilizzo di pacchetto di Windows Server autonomo di Microsoft Azure Service Fabric. È possibile [scaricare una copia del contratto di licenza hello](http://go.microsoft.com/fwlink/?LinkID=733084) ora. |
| Readme.txt |Un collegamento di toohello note sulla versione e le istruzioni di installazione di base. È un subset di istruzioni hello in questo documento. |
| ThirdPartyNotice.rtf |Avviso del software di terze parti che è nel pacchetto hello. |
| Tools\Microsoft.Azure.ServiceFabric.WindowsServer.SupportPackage.zip |StandaloneLogCollector.exe che viene eseguito su richiesta toocollect e caricamento traccia registra tooMicrosoft a scopo di supporto. |
| Tools\ServiceFabricUpdateService.zip |Un aggiornamento del codice automatica tooenable viene usato per i cluster che non hanno accesso a internet. Altri dettagli sono disponibili [qui](service-fabric-cluster-upgrade-windows-server.md)|

**Modelli** 
| **Nome file** | **Descrizione breve** |
| --- | --- |
| ClusterConfig.Unsecure.DevCluster.json |Un file di esempio configurazione del cluster che contiene le impostazioni di hello per un non protetto, tre nodi (singolo computer o macchina virtuale) sviluppo cluster, incluse le informazioni di hello per ogni nodo nel cluster hello. |
| ClusterConfig.Unsecure.MultiMachine.json |Un file di esempio configurazione del cluster che contiene le impostazioni di hello per un cluster non protetta, con più computer (o una macchina virtuale), incluse le informazioni di hello per ogni computer nel cluster hello. |
| ClusterConfig.Windows.DevCluster.json |Un file di esempio configurazione del cluster che contiene tutti hello le impostazioni per un singolo computer protetto, tre nodi (o macchina virtuale) cluster sviluppo, incluse le informazioni di hello per ogni nodo in cluster hello. cluster Hello è protetta tramite [le identità Windows](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.Windows.MultiMachine.json |Un file di esempio configurazione del cluster che contiene tutte le impostazioni di hello per un cluster con più computer (o una macchina virtuale) sicuro, utilizzando la sicurezza di Windows, incluse le informazioni di hello per ogni computer in cluster protetto hello. cluster Hello è protetta tramite [le identità Windows](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.x509.DevCluster.json |Un file di esempio configurazione del cluster che contiene tutte le impostazioni di hello per un protetta, tre nodi (singolo computer o macchina virtuale) sviluppo cluster, incluse le informazioni di hello per ogni nodo nel cluster hello. Hello cluster sia protetta con x509 certificati. |
| ClusterConfig.x509.MultiMachine.json |Proteggere un file di esempio di configurazione del cluster che contiene tutte le impostazioni di hello per hello, cluster con più computer (o una macchina virtuale), incluse le informazioni di hello per ogni nodo cluster protetto hello. Hello cluster sia protetta con x509 certificati. |
| ClusterConfig.gMSA.Windows.MultiMachine.json |Proteggere un file di esempio di configurazione del cluster che contiene tutte le impostazioni di hello per hello, cluster con più computer (o una macchina virtuale), incluse le informazioni di hello per ogni nodo cluster protetto hello. Hello cluster sia protetta con [Group Managed Service Accounts](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11).aspx). |

## <a name="cluster-configuration-samples"></a>Esempi di configurazione del cluster
Sono disponibili versioni più recenti dei modelli di configurazione del cluster nella pagina di GitHub hello: [esempi di configurazione di Cluster autonomi](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).

## <a name="independent-runtime-package"></a>Pacchetto di Runtime indipendente
il pacchetto di runtime più recente di Hello viene scaricato automaticamente durante la distribuzione di cluster da [collegamento Download - Runtime dell'infrastruttura del servizio - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).

## <a name="related"></a>Risorse correlate
* [Creare un cluster autonomo di Azure Service Fabric](service-fabric-cluster-creation-for-windows-server.md)
* [Scenari di sicurezza di un cluster di Service Fabric](service-fabric-windows-cluster-windows-security.md)

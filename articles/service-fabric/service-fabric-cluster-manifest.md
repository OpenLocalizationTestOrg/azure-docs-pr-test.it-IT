---
title: aaaConfigure il cluster di Azure Service Fabric autonomo | Documenti Microsoft
description: Informazioni su come tooconfigure autonomo o un cluster di Service Fabric privato.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a>Impostazioni di configurazione per un cluster autonomo in Windows
In questo articolo viene descritto come un cluster di Service Fabric autonomo tramite tooconfigure hello ***Clusterconfig*** file. È possibile utilizzare queste informazioni toospecify file, ad esempio nodi di Service Fabric hello e i relativi indirizzi IP, i diversi tipi di nodi nel cluster hello, configurazioni di sicurezza hello, nonché la topologia di rete hello in termini di domini di errore, aggiornamento, l'autonomo cluster.

Quando si [download del pacchetto Service Fabric autonomo hello](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), alcuni esempi di file Clusterconfig hello sono computer di lavoro tooyour scaricato. esempi di Hello con *DevCluster* nei relativi nomi consente di creare un cluster con tutti i tre nodi hello stesso computer, ad esempio nodi logici. Almeno uno di questi nodi deve essere contrassegnato come primario. Questo cluster è utile per un ambiente di sviluppo o test e non è supportato come cluster di produzione. esempi di Hello con *MultiMachine* nei relativi nomi, consente di creare un cluster di qualità di produzione, con ogni nodo in un computer separato.

1. *ClusterConfig.Unsecure.DevCluster.JSON* e *ClusterConfig.Unsecure.MultiMachine.JSON* Mostra come toocreate un test non protetto o produzione cluster rispettivamente. 
2. *ClusterConfig.Windows.DevCluster.JSON* e *ClusterConfig.Windows.MultiMachine.JSON* Mostra come cluster di test o produzione toocreate, protetti tramite [la sicurezza di Windows](service-fabric-windows-cluster-windows-security.md).
3. *ClusterConfig.X509.DevCluster.JSON* e *ClusterConfig.X509.MultiMachine.JSON* Mostra come cluster di test o produzione toocreate, protetti tramite [X509 sicurezza basata sui certificati](service-fabric-windows-cluster-x509-security.md). 

Ora verrà esaminata hello diverse sezioni di un ***Clusterconfig*** file come indicato di seguito.

## <a name="general-cluster-configurations"></a>Configurazioni generali del cluster
Questo articolo descrive hello ampie specifiche configurazioni dei cluster, come illustrato nel frammento di codice JSON hello riportato di seguito.

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

È possibile assegnare i cluster di Service Fabric tooyour qualsiasi nome descrittivo assegnandole toohello **nome** variabile. Hello **clusterConfigurationVersion** è il numero di versione hello del cluster; è necessario aumentare ogni volta che si esegue l'aggiornamento del cluster di Service Fabric. È tuttavia consigliabile lasciare hello **apiVersion** toohello predefinita.

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a>Nodi cluster hello
È possibile configurare i nodi di hello nel cluster di Service Fabric utilizzando hello **nodi** sezione come hello seguente mostra.

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

Un cluster Service Fabric deve contenere almeno 3 nodi. È possibile aggiungere una sezione di toothis più nodi in base all'impostazione. Hello nella tabella seguente vengono illustrate le impostazioni di configurazione hello per ogni nodo.

| **Configurazione nodo** | **Descrizione** |
| --- | --- |
| nodeName |È possibile assegnare qualsiasi nodo toohello nome descrittivo. |
| iPAddress |Trovare l'indirizzo IP di hello del nodo, aprire una finestra di comando e digitare `ipconfig`. Prendere nota di indirizzo IPV4 hello e assegnarlo toohello **iPAddress** variabile. |
| nodeTypeRef |È possibile assegnare un tipo diverso a ogni nodo. Hello [tipi di nodo](#nodetypes) definiti nella sezione hello riportato di seguito. |
| faultDomain |Errore domini Abilita amministratori toodefine hello fisici nodi del cluster che potrebbero non riuscire in hello stesso tempo a causa di dipendenze fisico tooshared. |
| upgradeDomain |Domini di aggiornamento vengono descritti i set di nodi che vengono arrestati per Service Fabric aggiornato su hello stesso tempo. È possibile scegliere quali toowhich tooassign nodi domini di aggiornamento, poiché non sono limitate dalle eventuali requisiti fisici. |

## <a name="cluster-properties"></a>Proprietà del cluster
Hello **proprietà** sezione hello Clusterconfig è cluster hello tooconfigure usati come indicato di seguito.

<a id="reliability"></a>

### <a name="reliability"></a>Affidabilità
il concetto di Hello di **reliabilityLevel** definisce il numero di hello di repliche o istanze di servizi di sistema di Service Fabric hello che è possono eseguire sui nodi primari di hello del cluster di hello. Determina l'affidabilità di hello di questi servizi e pertanto hello cluster. il valore di Hello è calcolata dal sistema hello in fase di creazione e l'aggiornamento del cluster.

### <a name="diagnostics"></a>Diagnostica
Hello **diagnosticsStore** sezione consente di diagnostica di tooenable parametri tooconfigure e nodo di risoluzione dei problemi o errori del cluster, come illustrato nel seguente frammento di codice hello. 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

Hello **metadati** è una descrizione di diagnostica del cluster e può essere impostata in base all'impostazione. Queste variabili consentono di raccogliere log di traccia ETW, dump di arresto anomalo e contatori delle prestazioni. Per altre informazioni sui log di traccia ETW, leggere gli articoli [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) e [Traccia ETW](https://msdn.microsoft.com/library/ms751538.aspx). Tutti i log inclusi [dump di arresto anomalo](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) e [i contatori delle prestazioni](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) può essere indirizzato toohello **connectionString** cartella nel computer. È anche possibile usare *AzureStorage* per l'archiviazione della diagnostica. Per un frammento di esempio, vedere di seguito.

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a>Sicurezza
Hello **sicurezza** sezione è necessaria per un cluster di Service Fabric autonomo sicura. Hello frammento di codice seguente viene illustrata una parte di questa sezione.

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

Hello **metadati** è una descrizione del cluster protetto e può essere impostata in base all'impostazione. Hello **ClusterCredentialType** e **ServerCredentialType** determinare il tipo di hello di sicurezza che consente di implementare cluster hello e nodi hello. Possono essere impostati tooeither *X509* per una sicurezza basata sui certificati o *Windows* per una protezione basata su Azure Active Directory. Hello rest di hello **sicurezza** sezione si baserà sul tipo hello di sicurezza hello. Lettura [sicurezza basata sui certificati in un cluster autonomo](service-fabric-windows-cluster-x509-security.md) o [la sicurezza di Windows in un cluster autonomo](service-fabric-windows-cluster-windows-security.md) per informazioni su come toofill out hello rest di hello **sicurezza**sezione.

<a id="nodetypes"></a>

### <a name="node-types"></a>Tipi di nodi
Hello **nodeTypes** sezione descrive il tipo di hello dei nodi di hello con il cluster. Come illustrato nel seguente frammento di hello, è necessario specificare il tipo di almeno un nodo per un cluster. 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

Hello **nome** hello nome descrittivo per questo tipo di nodo specifico. toocreate un nodo di questo tipo di nodo, assegnare il nome descrittivo di toohello **proprietà nodeTypeRef** variabile per il nodo, come indicato in [sopra](#clusternodes). Per ogni tipo di nodo, definire l'endpoint della connessione hello che verrà utilizzato. È possibile scegliere qualsiasi numero di porta per gli endpoint di connessione, purché non entrino in conflitto con altri endpoint in questo cluster. In un cluster a più nodi, saranno presenti uno o più nodi principali (ad esempio **isPrimary** impostare troppo*true*), a seconda di hello [ **reliabilityLevel** ](#reliability). Lettura [considerazioni sulla pianificazione della capacità di Service Fabric cluster](service-fabric-cluster-capacity.md) per informazioni su **nodeTypes** e **reliabilityLevel**, tooknow le primario e hello e tipi di nodo non primario. 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a>Gli endpoint utilizzati tipi di nodo hello tooconfigure
* *clientConnectionEndpointPort* hello porta utilizzato dal cluster toohello tooconnect di hello client, quando si utilizza l'API client hello. 
* *clusterConnectionEndpointPort* hello porta in cui i nodi di hello comunicano tra loro.
* *leaseDriverEndpointPort* hello porta utilizzata dal hello cluster lease driver toofind out se i nodi di hello sono ancora attivi. 
* *serviceConnectionEndpointPort* è porta hello utilizzata dalle applicazioni hello e i servizi distribuiti in un nodo, toocommunicate con client di Service Fabric hello in quel determinato nodo.
* *httpGatewayEndpointPort* hello porta utilizzato dal cluster toohello tooconnect di hello Service Fabric Explorer.
* *ephemeralPorts* override hello [porte dinamiche utilizzate dal sistema operativo hello](https://support.microsoft.com/kb/929851). Service Fabric utilizzerà una parte di queste porte dell'applicazione e hello rimanenti saranno disponibili per hello del sistema operativo. Presente nel sistema operativo, hello questo intervallo toohello esistente intervallo eseguirà il mapping anche per tutti gli scopi, è possibile utilizzare intervalli hello dati nei file JSON di esempio hello. È necessario che la differenza hello tra inizio hello e porte finali hello sia almeno 255 toomake. Se questa differenza è troppo bassa, poiché questo intervallo è condiviso con sistema operativo hello, che potrebbero verificarsi conflitti. Visualizzare l'intervallo di porte dinamiche hello configurato eseguendo `netsh int ipv4 show dynamicport tcp`.
* *applicationPorts* sono porte hello che verranno utilizzate dalle applicazioni di Service Fabric hello. intervallo di porte applicazione Hello deve essere sufficientemente grande toocover requisito di endpoint hello delle applicazioni. Questo intervallo deve essere esclusivo dall'intervallo di porte dinamiche hello computer hello, vale a dire hello *ephemeralPorts* intervallo come set di configurazione di hello.  Service Fabric utilizzeranno queste ogni volta che nuove porte sono necessari, nonché occuperà di apertura firewall hello per queste porte. 
* *reverseProxyEndpointPort* è un endpoint proxy inverso facoltativo. Per altri dettagli vedere [Proxy inverso di Service Fabric](service-fabric-reverseproxy.md). 

### <a name="log-settings"></a>Impostazioni log
Hello **fabricSettings** sezione consente di directory radice di hello tooset per dati di Service Fabric hello e di log. È possibile personalizzare queste solo durante la creazione iniziale del cluster hello. Per un frammento di esempio di questa sezione, vedere di seguito.

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

È consigliabile usare un'unità non del sistema operativo come hello FabricDataRoot e FabricLogRoot poiché fornisce maggiore affidabilità rispetto degli arresti anomali del sistema operativo. Si noti che se si personalizza solo radice dei dati di hello, quindi radice log hello verrà inserito un livello inferiore radice dei dati hello.

### <a name="stateful-reliable-service-settings"></a>Impostazioni di Reliable Services con stato
Hello **KtlLogger** sezione consente di impostazioni di configurazione globali hello tooset per servizi affidabili. Per altre informazioni su queste impostazioni leggere [Configurazione dei servizi Reliable Services con stato](service-fabric-reliable-services-configuration.md).
esempio Hello riportato di seguito viene illustrata la toochange hello hello condiviso log delle transazioni che ottiene creazione tooback raccolte affidabile per i servizi con stati.

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a>Funzionalità aggiuntive
le funzioni aggiuntive tooconfigure, hello apiVersion deve essere configurato come ' 04-2017' o versione successiva e addonFeatures deve toobe configurato:

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a>Supporto dei contenitori
supporto del contenitore tooenable per contenitore di windows server e il contenitore di hyper-v per i cluster autonomo, funzionalità di componente aggiuntivo 'DnsService' hello deve toobe abilitato.


## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato un file Clusterconfig completo configurato per l'installazione del cluster autonomo, è possibile distribuire il cluster dal seguente hello [creare un cluster di Service Fabric autonomo](service-fabric-cluster-creation-for-windows-server.md) e quindi procedere troppo[visualizzazione cluster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).


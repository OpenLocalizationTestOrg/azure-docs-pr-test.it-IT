---
title: Preparazione della distribuzione di Service Fabric autonomo Cluster aaaAzure | Documenti Microsoft
description: Documentazione correlata ambiente hello toopreparing e la creazione di configurazione del cluster hello toobe considerato toodeploying precedente un cluster previsto per la gestione di un carico di lavoro di produzione.
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
ms.date: 1/17/2017
ms.author: maburlik;chackdan
ms.openlocfilehash: e503c61a64b408af3f22bd75ab02f1c34ac9f380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
<a id="preparemachines"></a>

## <a name="plan-and-prepare-your-service-fabric-standalone-cluster-deployment"></a>Pianificare e preparare la distribuzione del cluster autonomo di Service Fabric
Eseguire hello seguendo i passaggi prima di creare il cluster.

### <a name="step-1-plan-your-cluster-infrastructure"></a>Passaggio 1: pianificazione dell’infrastruttura del cluster
Si sta toocreate un cluster di Service Fabric nel computer che si è proprietari, pertanto è possibile decidere quali tipi di errori che si desidera hello toosurvive cluster. Ad esempio, è necessario linee di alimentazione separate o connessioni Internet fornito macchine toothese? Inoltre, prendere in considerazione sicurezza fisica di hello di tali macchine. Dove si trovano le macchine hello e necessita di accesso toothem? Dopo aver apportato queste decisioni, è possibile logicamente hello macchine toohello diversi domini di errore (vedere il passaggio 4). la pianificazione per i cluster di produzione dell'infrastruttura di Hello è più complessa di quella per i cluster di test.

### <a name="step-2-prepare-hello-machines-toomeet-hello-prerequisites"></a>Passaggio 2: Preparare i prerequisiti di hello hello macchine toomeet
Prerequisiti per ogni computer che si desidera tooadd toohello cluster:

* Consigliati minimo 16 GB di RAM.
* Consigliati minimo 40 GB di spazio disponibile su disco.
* Consigliata una CPU 4 core o superiore.
* Rete sicura tooa di connettività o di rete per tutte le macchine.
* Windows Server 2012 R2 o Windows Server 2016. 
* [.NET Framework 4.5.1 o versione successiva](https://www.microsoft.com/download/details.aspx?id=40773), installazione completa.
* [Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell).
* Hello [RemoteRegistry servizio](https://technet.microsoft.com/library/cc754820) deve essere in esecuzione in tutti i computer hello.

Hello Amministrazione cluster, distribuzione e configurazione dei cluster hello deve avere [privilegi di amministratore](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx) in ciascun computer hello di. Non è possibile installare Service Fabric in un controller di dominio.

### <a name="step-3-determine-hello-initial-cluster-size"></a>Passaggio 3: Determinare le dimensioni di cluster iniziale hello
Ogni nodo in un cluster di Service Fabric autonomo è hello Service Fabric runtime distribuito ed è un membro del cluster di hello. In una distribuzione di produzione tipica è presente un nodo per istanza (fisica o virtuale) del sistema operativo. dimensione del cluster Hello è determinato dalle esigenze aziendali. È tuttavia necessario avere una dimensione minima del cluster di tre nodi (computer o macchine virtuali).
A scopi di sviluppo è possibile configurare più di un nodo in una macchina specifica. In un ambiente di produzione, il Service Fabric supporta solo un nodo per ogni macchina virtuale o fisica.

### <a name="step-4-determine-hello-number-of-fault-domains-and-upgrade-domains"></a>Passaggio 4: Determinare il numero di hello di domini di errore e domini di aggiornamento
Oggetto *dominio di errore* (FD) è un'unità fisica di errore e dell'infrastruttura fisica toohello direttamente correlati nei centri dati hello. È costituito da componenti hardware (computer, commutatori, rete e altro) che condividono un singolo punto di guasto. Sebbene non sia presente una mappatura 1:1 tra domini di errore e rack, ogni rack può essere considerato in senso lato un dominio di errore. Quando si considera i nodi del cluster hello, è consigliabile che i nodi di hello distribuito tra almeno tre domini di errore.

Quando si specificano i domini di errore in Clusterconfig, è possibile scegliere il nome di hello per ogni FD. Il Service Fabric supporta i domini di errore gerarchici, in modo che possano rispecchiare la topologia infrastrutturale.  Ad esempio, hello domini di errore seguenti è valido:

* "faultDomain": "fd:/Room1/Rack1/Machine1"
* "faultDomain": "fd:/FD1"
* "faultDomain": "fd:/Room1/Rack1/PDU1/M1"

Un *dominio di aggiornamento* è un'unità logica di nodi. Durante gli aggiornamenti orchestrati di Service Fabric (un aggiornamento dell'applicazione o un aggiornamento del cluster), tutti i nodi in un UD vengono portati aggiornamento hello tooperform mentre i nodi in altri domini di aggiornamento rimangono disponibili tooserve richieste. Hello gli aggiornamenti del firmware eseguite nei computer che non rispettano UD, pertanto è necessario eseguire in una macchina alla volta.

toothink modo più semplice di Hello su questi concetti è tooconsider Fd come unità hello di errore non pianificato e domini di aggiornamento come unità hello di manutenzione pianificata.

Quando si specifica UD in Clusterconfig, è possibile scegliere il nome di hello per ogni ID. Ad esempio, hello seguente i nomi è valido:

* "upgradeDomain": "UD0"
* "upgradeDomain": "UD1A"
* "upgradeDomain": "DomainRed"
* "upgradeDomain": "Blue"

Per informazioni più dettagliate sui domini di aggiornamento e di errore, vedere [Descrizione di un cluster di Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md).

### <a name="step-5-download-hello-service-fabric-standalone-package-for-windows-server"></a>Passaggio 5: Scaricare pacchetto autonomo di hello Service Fabric per Windows Server
[Scaricare Windows Server di collegamento - pacchetto autonomo di Service Fabric -](http://go.microsoft.com/fwlink/?LinkId=730690) e decomprimere il pacchetto di hello, vale a dire dei entrambi distribuzione tooa computer non fa parte del cluster hello o tooone macchine hello che farà parte del cluster.

### <a name="step-6-modify-cluster-configuration"></a>Passaggio 6: modificare la configurazione del cluster
un cluster autonomo toocreate è toocreate un autonomo cluster Clusterconfig file di configurazione che descrive la specifica di hello del cluster di hello. È possibile basare i file di configurazione hello nei modelli di hello nella hello collegamento sottostante. <br>
[Configurazioni di cluster autonomi](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

Per informazioni dettagliate sulle sezioni hello in questo file, vedere [le impostazioni di configurazione per il cluster di Windows autonoma](service-fabric-cluster-manifest.md).

Aprire uno dei file Clusterconfig hello dal pacchetto hello scaricato e modificare hello seguenti impostazioni:
| **Impostazioni di configurazione** | **Descrizione** |
| --- | --- |
| **NodeTypes** |Tipi di nodo consentono tooseparate i nodi del cluster in gruppi diversi. Un cluster deve avere almeno un NodeType. Tutti i nodi in un gruppo sia hello caratteristiche comuni seguenti: <br> **Nome** -si tratta del tipo di nodo hello. <br>**Porte di endpoint** : endpoint con nomi diversi (porte) associati a questo tipo di nodo. È possibile utilizzare qualsiasi numero di porta che si desidera, purché non siano in conflitto con qualsiasi altro in questo manifesto e non sono già in uso da un'altra applicazione in esecuzione nella macchina hello/macchina virtuale. <br> **Proprietà di posizionamento** -questi descrivono le proprietà per questo tipo di nodo che si utilizza come vincoli di posizionamento per servizi di sistema hello o i servizi. Queste proprietà sono coppie chiave-valore definite dall'utente che forniscono metadati aggiuntivi per un determinato nodo. Esempi di proprietà del nodo sarebbe se il nodo hello dispone di un disco rigido o scheda grafica, il numero di hello di assi nel relativo disco rigido, Core e altre proprietà fisiche. <br> **Capacità** -capacità nodo definire hello nome e la quantità di una risorsa specifica che un determinato nodo è disponibile per l'utilizzo. Ad esempio, un nodo può definire la propria capacità per una metrica denominata "MemoryInMb" con un valore predefinito di 2048 MB di memoria disponibile. Queste capacità vengono usati servizi che richiedono una determinata quantità di risorse vengono inseriti nei nodi hello sono le risorse disponibili in hello necessarie quantità tooensure di runtime.<br>**IsPrimary** : se presente più di un tipo di nodo definito assicurarsi che solo uno è impostato tooprimary con valore hello *true*, che è in esecuzione dei servizi di sistema hello. Tutti gli altri tipi di nodo devono essere impostati come valore toohello *false* |
| **Nodi** |Questi sono i dettagli di hello per ognuno dei nodi di hello che fanno parte del cluster di hello (tipo di nodo, il nome del nodo, IP indirizzo, dominio di errore e dominio di aggiornamento del nodo hello). macchine Hello desiderato hello cluster toobe creato in toobe necessità elencati di seguito con gli indirizzi IP. <br> Se si utilizza hello stesso indirizzo IP di tutti i nodi di hello, viene creato un cluster di una casella, che è possibile utilizzare a scopo di test. Non usare cluster di una casella per la distribuzione dei carichi di lavoro di produzione. |

Dopo la configurazione del cluster hello ha tutte le impostazioni configurate toohello ambiente, può essere testato in ambiente cluster hello (passaggio 7).

<a id="environmentsetup"></a>

### <a name="step-7-environment-setup"></a>Passaggio 7. Configurazione dell'ambiente

Quando un amministratore di cluster consente di configurare un cluster di Service Fabric autonomo, ambiente hello è deve toobe impostato con hello seguenti criteri: <br>
1. utente di Hello creazione hello cluster deve disporre di macchine di tooall privilegi di sicurezza a livello di amministratore elencati come nodi nel file di configurazione del cluster hello.
2. Computer da cui hello cluster è stato creato, nonché a ogni computer del nodo del cluster deve:
* Service Fabric SDK non installato
* Runtime di Service Fabric non installato 
* Avrà hello servizio Windows Firewall (mpssvc) abilitato
* Hello servizio Registro di sistema remoto (remoteregistry) è stato abilitato
* Condivisione file (SMB) abilitata
* Porte aperte necessarie in base alle porte di configurazione del cluster
* Porte aperte necessarie per il servizio Registro di sistema remoto e Windows SMB: 135, 137, 138, 139 e 445
* Tooone di connettività di rete hanno un altro
3. Nessuno dei computer del nodo cluster hello deve essere un Controller di dominio.
4. Se hello cluster toobe distribuita è un cluster protetto, convalidare la sicurezza hello prerequisiti siano posizionare e sono configurati correttamente con configurazione hello.
5. Se i computer del cluster hello non sono accessibili da internet, configurazione dei cluster di set seguente di hello in hello:
* Disabilitare la telemetria: in *properties* impostare *"enableTelemetry": false*
* Disabilitare il download di versione di Fabric & notifiche tale versione del cluster corrente hello è vicina al termine del supporto automatico: in *proprietà* impostare *"fabricClusterAutoupgradeEnabled": false*
* In alternativa se l'accesso alla rete internet è limitati domini elencati toowhite, domini hello riportato di seguito sono necessari per l'aggiornamento automatico: go.microsoft.com download.microsoft.com

6. Impostare le esclusioni antivirus di Service Fabric appropriate:

| **Directory escluse dall'antivirus** |
| --- |
| Program Files\Microsoft Service Fabric |
| FabricDataRoot (dalla configurazione del cluster) |
| FabricLogRoot (dalla configurazione del cluster) |

| **Processi esclusi dall'antivirus** |
| --- |
| Fabric.exe |
| FabricHost.exe |
| FabricInstallerService.exe |
| FabricSetup.exe |
| FabricDeployer.exe |
| ImageBuilder.exe |
| FabricGateway.exe |
| FabricDCA.exe |
| FabricFAS.exe |
| FabricUOS.exe |
| FabricRM.exe |
| FileStoreService.exe |

### <a name="step-8-validate-environment-using-testconfiguration-script"></a>Passaggio 8. Convalidare l'ambiente con lo script TestConfiguration
Hello TestConfiguration.ps1 script può essere trovato nel pacchetto autonomo di hello. È utilizzato come un toovalidate Best Practices Analyzer alcuni criteri hello precedente e deve essere utilizzato come un toovalidate di controllo di integrità, se un cluster può essere distribuito in un determinato ambiente. Se si verifica qualsiasi errore, vedere elenco toohello [impostazione dell'ambiente](service-fabric-cluster-standalone-deployment-preparation.md) per la risoluzione dei problemi. 

Questo script può essere eseguito su qualsiasi computer che dispone di amministratore accesso tooall hello computer elencati come nodi nel file di configurazione del cluster hello. macchina Hello che questo script viene eseguito in non è una parte del cluster hello toobe.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
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

Questo modulo di configurazione di test attualmente non convalida la configurazione di sicurezza hello pertanto ha toobe eseguita in modo indipendente.  

> [!NOTE]
> Vengono continuamente apportati miglioramenti toomake questo modulo più affidabile, pertanto se si verifica un guasto o mancante case che si ritiene che non è attualmente rilevata da TestConfiguration, segnalarlo tramite il nostro [supportano i canali](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).   
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* [Creare un cluster autonomo in esecuzione su Windows Server](service-fabric-cluster-creation-for-windows-server.md)

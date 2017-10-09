---
title: soluzione di monitoraggio in Azure Log Analitica aaaContainer | Documenti Microsoft
description: soluzione di monitoraggio della contenitore nel Log Analitica Hello consente di visualizzare e gestire Docker e Windows host contenitore in un'unica posizione.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a>Soluzione Monitoraggio contenitori in Log Analytics

![Simbolo di Contenitori](./media/log-analytics-containers/containers-symbol.png)

In questo articolo viene descritto come tooset backup e utilizzare hello contenitore monitoraggio soluzione Analitica di Log, che consente di visualizzare e gestire Docker e Windows host contenitore in un'unica posizione. Docker è un sistema di virtualizzazione software utilizzati contenitori toocreate che consentono di automatizzare la distribuzione di software tootheir IT dell'infrastruttura.

soluzione Mostra contenitori in esecuzione, quali immagini contenitore vengono eseguiti, Hello e in cui vengono eseguiti i contenitori. È possibile visualizzare informazioni di controllo dettagliate che indicano i comandi usati con i contenitori. E, è possibile risolvere i contenitori mediante la visualizzazione e la ricerca di log centralizzato senza visualizzazione tooremotely Docker o host di Windows. È possibile trovare contenitori che consumano una quantità eccessiva di risorse in un host. È anche possibile visualizzare informazioni centralizzate su utilizzo di CPU, memoria, archiviazione e rete e sulle prestazioni dei contenitori. Nei computer che eseguono Windows, è possibile centralizzare e confrontare i log dai contenitori Windows Server, Hyper-V e Docker. soluzione Hello supporta hello orchestrators contenitore seguente:

- Docker Swarm
- Controller di dominio/sistema operativo
- kubernetes
- Service Fabric
- Red Hat OpenShift


Hello diagramma seguente mostra le relazioni di hello tra vari host contenitore e di agenti con OMS.

![Diagramma dei contenitori](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a>Requisiti di sistema

Prima di iniziare, esaminare hello seguenti siano soddisfatti i prerequisiti di hello tooverify di dettagli.

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a>Supporto della soluzione di monitoraggio del contenitore per l'orchestrazione di Docker e la piattaforma del sistema operativo
Hello tabella seguente vengono illustrati hello orchestrazione Docker e supporto di inventario di contenitore, prestazioni e i registri con Analitica di Log di controllo del sistema operativo.   

| | ACS | Linux | Windows | Contenitore<br>Inventario | Image<br>Inventario | Nodo<br>Inventario | Contenitore<br>Prestazioni | Contenitore<br>Evento | Evento<br>Log | Contenitore<br>Log |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| kubernetes | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Mesosphere<br>Controller di dominio/sistema operativo | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; |
| Docker<br>Swarm | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| Service<br>Infrastruttura | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Red Hat Open<br>MAIUSC | | &#8226; | | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; | | &#8226; |
| Windows Server<br>(autonomo) | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| Server Linux<br>(autonomo) | | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |


### <a name="docker-versions-supported-on-linux"></a>Versioni di Docker supportate in Linux

- Docker 1.11 too1.13
- Docker CE e EE v17.06

### <a name="x64-linux-distributions-supported-as-container-hosts"></a>Distribuzioni Linux x64 supportate come host del contenitore

- Ubuntu 14.04 LTS e 16.04 LTS
- CoreOS (stable)
- Amazon Linux 2016.09.0
- openSUSE 13.2
- openSUSE LEAP 42.2
- CentOS 7.2 e 7.3
- SLES 12
- RHEL 7.2 e 7.3
- Red Hat OpenShift Container Platform (OCP) 3.4 e 3.5
- ACS Mesosphere DC/OS 1.7.3 too1.8.8
- ACS Kubernetes 1.4.5 too1.6
- ACS Docker Swarm

### <a name="supported-windows-operating-system"></a>Sistema operativo Windows supportato

- Windows Server 2016
- Versione di Windows per il 10° anniversario (professionale o aziendale)

### <a name="docker-versions-supported-on-windows"></a>Versioni di Docker supportate in Windows

- Docker 1.12 e 1.13
- Docker 17.03.0 e successive

## <a name="installing-and-configuring-hello-solution"></a>Installazione e configurazione di soluzione hello
Utilizzare hello tooinstall le informazioni seguenti e configurare la soluzione hello.

1. Aggiungere hello contenitore monitoraggio soluzione tooyour area di lavoro OMS da [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) o tramite il processo di hello descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).

2. Installare e usare Docker con un agente OMS.  In base al sistema operativo, è possibile scegliere tra hello dei seguenti metodi:

  * Nei sistemi operativi Linux supportati, installare e l'esecuzione di Docker e quindi installare e configurare hello [agente OMS per Linux](log-analytics-agent-linux.md).  
  * In CoreOS, è possibile eseguire hello agente OMS per Linux. Eseguire invece una versione nei contenitori di hello agente OMS per Linux. Vedere la sezione [Per tutti gli host del contenitore Linux inclusi CoreOS](#for-all-linux-container-hosts-including-coreos) o [Per tutti gli host del contenitore Linux Azure per enti pubblici incluso CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) se si usano contenitori nel cloud di Azure per enti pubblici.
  * In Windows Server 2016 e Windows 10, è possibile installare hello motore Docker e il client quindi connettersi informazioni toogather agente e inviarlo tooLog Analitica.  

### <a name="container-services"></a>Servizi contenitore

- Se si opera in un ambiente Red Hat OpenShift, vedere [Configurare un agente OMS per Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).
- Se si dispone di un cluster di Kubernetes utilizzando hello servizio contenitore di Azure, consultare [monitorare un cluster il servizio contenitore di Azure con Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).
- Se si ha un cluster DC/OS del servizio contenitore di Azure, vedere [Monitorare un cluster DC/OS del servizio contenitore di Azure con Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).
- Se è presente un ambiente in modalità Docker Swarm, per altre informazioni vedere [Configurare un agente OMS per Docker Swarm](#configure-an-oms-agent-for-docker-swarm).
- Se si usano contenitori con Service Fabric, vedere [Panoramica di Azure Service Fabric](../service-fabric/service-fabric-overview.md).
- Hello revisione [motore Docker in Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) articolo per ulteriori informazioni su come tooinstall e configurare i motori di Docker su computer che eseguono Windows.

> [!IMPORTANT]
> Deve essere in esecuzione di docker **prima** installare hello [agente OMS per Linux](log-analytics-agent-linux.md) negli host contenitore. Se è già stato installato l'agente di hello prima di installare Docker, è necessario tooreinstall hello agente OMS per Linux. Per ulteriori informazioni su Docker, vedere hello [sito Web di Docker](https://www.docker.com).


## <a name="linux-container-hosts"></a>Host del contenitore Linux

Dopo aver installato Docker, usare hello seguenti impostazioni per l'agente di hello tooconfigure host contenitore per l'utilizzo con Docker. È necessario l'ID area di lavoro OMS e la chiave, che è possibile trovare nel portale di Azure hello. Nell'area di lavoro, fare clic su **avvio rapido** > **computer** tooview il **ID area di lavoro** e **chiave primaria**.  Copiare e incollare entrambi i valori nell'editor predefinito.

### <a name="for-all-linux-container-hosts-except-coreos"></a>Per tutti gli host del contenitore Linux, ad eccezione di CoreOS

- Per ulteriori informazioni e procedure su come tooinstall hello agente OMS per Linux, vedere [connettersi il tooOperations computer Linux Management Suite (OMS)](log-analytics-agent-linux.md).

### <a name="for-all-linux-container-hosts-including-coreos"></a>Per tutti gli host del contenitore Linux inclusi CoreOS

Avviare il contenitore OMS hello che si desidera toomonitor. Modificare e usare hello di esempio seguente:

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a>Per tutti gli host del contenitore Linux Azure per enti pubblici incluso CoreOS

Avviare il contenitore OMS hello che si desidera toomonitor. Modificare e usare hello di esempio seguente:

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a>Il passaggio da utilizzando un tooone di agente Linux installato in un contenitore
Se si precedentemente utilizzato agente installato direttamente hello e si desidera utilizzare tooinstead un agente in esecuzione in un contenitore, è necessario innanzitutto rimuovere hello agente OMS per Linux. Vedere [hello il processo di disinstallazione agente OMS per Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand come toosuccessfully disinstallare hello agente.  

### <a name="configure-an-oms-agent-for-docker-swarm"></a>Configurare un agente OMS per Docker Swarm

È possibile eseguire hello agente OMS come servizio globale su Docker Swarm. Utilizzare hello seguente informazioni toocreate un servizio dell'agente OMS. È necessario tooinsert l'ID area di lavoro OMS e la chiave primaria.

- Eseguire l'istruzione seguente hello su nodo principale hello.

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a>Configurare un agente OMS per Red Hat OpenShift
Esistono tre modi tooadd hello agente OMS tooRed Hat OpenShift toostart raccolta contenitore dati di monitoraggio.

* [Installare hello agente OMS per Linux](log-analytics-agent-linux.md) direttamente in ogni nodo OpenShift  
* [Abilitare l'estensione della macchina virtuale di Log Analytics](log-analytics-azure-vm-extension.md) in ogni nodo OpenShift che risiede in Azure  
* Installare l'agente OMS hello come un set di daemon OpenShift  

In questa sezione viene illustrata hello passaggi necessari tooinstall hello agente OMS come un set di daemon OpenShift.  

1. Accesso toohello OpenShift nodo e copia hello yaml file master [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) da GitHub tooyour master nodo e modificare il valore di hello con l'ID dell'area di lavoro OMS e con la chiave primaria.
2. Eseguire un progetto di hello toocreate i comandi seguenti per OMS e impostare l'account utente di hello.

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. hello toodeploy set daemon, eseguire hello:

    `oc create -f ocp-omsagent.yaml`

5. tooverify è configurato e che funzioni correttamente, digitare il seguente di hello:

    `oc describe daemonset omsagent`  

    e l'output di hello dovrebbe essere simile:

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

Se si desidera toouse segreti toosecure l'ID area di lavoro OMS e la chiave primaria quando si utilizza hello agente OMS yaml daemon-set di file, eseguire hello alla procedura seguente.

1. Accesso toohello OpenShift nodo e copia hello yaml file master [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) e il segreto di generazione dello script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) da GitHub.  Lo script genererà hello segreti yaml file toosecure ID area di lavoro OMS e la chiave primaria il secrete informazioni.  
2. Eseguire un progetto di hello toocreate i comandi seguenti per OMS e impostare l'account utente di hello. segreto Hello generazione dello script richiede l'ID dell'area di lavoro OMS <WSID> e la chiave primaria <KEY> e dopo il completamento, crea file ocp-secret.yaml hello.  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. Distribuire file segreto hello eseguendo hello:

    `oc create -f ocp-secret.yaml`

5. Verificare la distribuzione eseguendo hello:

    `oc describe secret omsagent-secret`  

    e l'output di hello dovrebbe essere simile:  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. Distribuire file daemon set yaml di hello agente OMS eseguendo hello:

    `oc create -f ocp-ds-omsagent.yaml`  

7. Verificare la distribuzione eseguendo hello:

    `oc describe ds oms`

    e l'output di hello dovrebbe essere simile:

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a>Proteggere le informazioni segrete per Docker Swarm e Kubernetes

È possibile proteggere l'ID segreto dell'area di lavoro OMS e le chiavi primarie segrete per i servizi contenitore Docker Swarm e Kubernetes.

#### <a name="secure-secrets-for-docker-swarm"></a>Proteggere i segreti per Docker Swarm

Per Docker Swarm, una volta creato il segreto di hello per ID area di lavoro e la chiave primaria, è possibile eseguire hello creare il servizio Docker hello per OMSagent. Utilizzare hello toocreate informazioni seguendo le informazioni segrete.

1. Eseguire l'istruzione seguente hello su nodo principale hello.

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. Verificare che i segreti siano stati creati correttamente.

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. Esecuzione hello successivo comando toomount hello segreti toohello contenitore agente OMS.

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a>Proteggere i segreti per Kubernetes con file yaml

Per Kubernetes, utilizzare un file di script toogenerate hello segreti yaml per l'ID area di lavoro e la chiave primaria. In hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) pagina, sono disponibili i file che è possibile utilizzare con o senza le informazioni segrete.

- Hello predefinito OMS Agent DaemonSet non dispone di informazioni segrete (omsagent.yaml)
- file yaml di Hello DaemonSet agente OMS Usa informazioni segrete (omsagent-ds-secrets.yaml) con file di generazione secret script toogenerate hello segreti yaml (omsagentsecret.yaml).

È possibile scegliere toocreate omsagent DaemonSets con o senza i segreti.

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a>File DaemonSet con estensione yaml predefinito dell'agente OMS senza segreti

- Per file yaml DaemonSet agente OMS di hello predefinito, sostituire hello `<WSID>` e `<KEY>` tooyour WSID e la chiave. Copiare nodo principale di hello file tooyour e seguenti hello esecuzione:

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a>File DaemonSet con estensione yaml predefinito dell'agente OMS con segreti

1. toouse DaemonSet agente OMS utilizzando le informazioni segrete, creare i segreti hello prima.
    1. Copiare script hello e file di modello segreta e verificare che siano presenti hello stessa directory.
        - Script per la generazione di segreti: secret-gen.sh
        - Modello di segreto: secret-template.yaml
    2. Eseguire script hello, ad esempio hello di esempio seguente. script Hello chiede hello ID area di lavoro OMS e la chiave primaria e dopo l'immissione, script hello crea un file di secret yaml in modo da eseguire.   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. Creare pod segreti hello eseguendo hello:
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. tooverify, eseguire hello seguente:

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        L'output deve essere simile a:

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        L'output deve essere simile a:

        ```
        Name:           omsagent-secret
        Namespace:      default
        Labels:         <none>
        Annotations:    <none>

        Type:   Opaque

        Data
        ====
        WSID:   36 bytes
        KEY:    88 bytes
        ```

    5. Creare il DaemonSet dell'agente OMS eseguendo l'istruzione ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```

2. Verificare che hello che daemonset agente OMS è in esecuzione, simile toohello seguenti:

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


Per Kubernetes, utilizzare un file di script toogenerate hello segreti yaml per ID area di lavoro e la chiave primaria. Hello di utilizzare le seguenti informazioni di esempio con hello [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure le informazioni segrete.

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
Name:           omsagent-secret
Namespace:      default
Labels:         <none>
Annotations:    <none>

Type:   Opaque

Data
====
WSID:   36 bytes
KEY:    88 bytes
```

## <a name="windows-container-hosts"></a>Host del contenitore Windows

### <a name="preparation-before-installing-windows-agents"></a>Preparazione prima dell'installazione degli agenti di Windows

Prima di installare gli agenti nei computer che eseguono Windows, è necessario servizio Docker di tooconfigure hello. configurazione di Hello consente hello Windows hello o agente di Log Analitica macchina virtuale estensione toouse hello del socket TCP Docker in modo che gli agenti di hello possono accedere in remoto i daemon Docker hello e toocapture dati per il monitoraggio.

#### <a name="toostart-docker-and-verify-its-configuration"></a>toostart Docker e verificare la configurazione

Esistono passaggi necessari tooset backup TCP, named pipe per Windows Server:

1. In Windows PowerShell, abilitare pipe TCP e named pipe.

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. Configurare Docker con il file di configurazione hello per pipe TCP e named pipe. file di configurazione Hello è disponibile in c:\programdata\docker\config\daemon.JSON..

    Nel file daemon hello, sarà necessario seguente hello:

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

Per ulteriori informazioni sulla configurazione del daemon Docker hello usato con i contenitori di Windows, vedere [motore Docker in Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).


### <a name="install-windows-agents"></a>Installare gli agenti Windows

tooenable Windows e contenitore di Hyper-V di monitoraggio, installare Microsoft Monitoring Agent (MMA) hello nei computer Windows che sono host contenitore. Per i computer che eseguono Windows nell'ambiente locale, vedere [tooLog computer Windows di connettersi Analitica](log-analytics-windows-agents.md). Per le macchine virtuali in esecuzione in Azure, connetterle tooLog Analitica utilizzando hello [estensione della macchina virtuale](log-analytics-azure-vm-extension.md).

È possibile monitorare i contenitori Windows in esecuzione in Service Fabric. Solo le [macchine virtuali in esecuzione in Azure](log-analytics-azure-vm-extension.md) e i [computer che eseguono Windows nell'ambiente locale](log-analytics-windows-agents.md), tuttavia, sono attualmente supportati da Service Fabric.

È possibile verificare che tale soluzione di monitoraggio contenitore hello sia impostato correttamente per Windows. toocheck se hello management pack download non è correttamente, cercare *ContainerManagement.xxx*. file di Hello devono trovarsi nella cartella c:\Programmi\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs hello.


## <a name="solution-components"></a>Componenti della soluzione

Se si usano agenti di Windows, quindi hello seguenti management pack è installato in ogni computer con un agente quando si aggiunge questa soluzione. Non è necessaria per il management pack di hello alcuna configurazione o manutenzione.

- *ContainerManagement.xxx* installato in C:\Programmi\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs

## <a name="container-data-collection-details"></a>Informazioni dettagliate sulla raccolta di dati dei contenitori
soluzione di monitoraggio contenitore Hello raccoglie diversi dati di log e le metriche delle prestazioni dall'host contenitore e i contenitori usano agenti che si attivano.

Dati raccolti ogni tre minuti per hello seguenti tipi di agente.

- [Agente OMS per Linux](log-analytics-linux-agents.md)
- [Agente Windows](log-analytics-windows-agents.md)
- [Estensione macchina virtuale di Log Analytics](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a>Record dei contenitori

Hello nella tabella seguente vengono illustrati esempi di record raccolti dalla soluzione di monitoraggio di contenitore hello e hello i tipi di dati che vengono visualizzati nei risultati della ricerca log.

| Tipo di dati | Tipo di dati in Ricerca log | Fields |
| --- | --- | --- |
| Prestazioni per host e contenitori | `Type=Perf` | Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem |
| Inventario contenitori | `Type=ContainerInventory` | TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID |
| Inventario delle immagini dei contenitori | `Type=ContainerImageInventory` | TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer |
| Log contenitori | `Type=ContainerLog` | TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID |
| Log servizio contenitori | `Type=ContainerServiceLog`  | TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID |
| Inventario di nodi contenitore | `Type=ContainerNodeInventory_CL`| TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem|
| Inventario di Kubernetes | `Type=KubePodInventory_CL` | TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem |
| Processo contenitore | `Type=ContainerProcess_CL` | TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem |
| Eventi di Kubernetes | `Type=KubeEvents_CL` | TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message |

Aggiunta di etichette troppo*PodLabel* etichette personalizzate sono di tipi di dati. Hello aggiunte etichette PodLabel illustrate nella tabella hello sono esempi. `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` saranno quindi diverse nel set di dati dell'ambiente e in genere saranno simili a `PodLabel_yourlabel_s`.


## <a name="monitor-containers"></a>Monitorare i contenitori
Dopo aver creato una soluzione di hello abilitata nel portale OMS hello, hello **contenitori** riquadro mostra le informazioni di riepilogo sull'host contenitore e i contenitori di hello in esecuzione negli host.

![Riquadro Containers (Contenitori)](./media/log-analytics-containers/containers-title.png)

riquadro Hello Mostra una panoramica dei contenitori di quanti sono in ambiente hello e se è impossibile, in esecuzione o arrestato.

### <a name="using-hello-containers-dashboard"></a>Tramite il dashboard di contenitori hello
Fare clic su hello **contenitori** riquadro. Le visualizzazioni sono organizzate in base agli elementi seguenti:

- **Eventi del contenitore**: visualizza lo stato dei contenitori e i computer con contenitori non riusciti.
- **Contenitore registri** -Visualizza un grafico dei file di log contenitore generati nel tempo e un elenco di computer con numero più alto di hello dei file di log.
- **Eventi Kubernetes** -Mostra un grafico di eventi Kubernetes generati nel tempo e un elenco di motivi hello perché POD generati eventi hello. *Questo set di dati viene usato solo negli ambienti Linux.*
- **Inventario Namespace Kubernetes** - Mostra il numero di hello di unità e spazi dei nomi e viene illustrata la gerarchia. *Questo set di dati viene usato solo negli ambienti Linux.*
- **Inventario nodo contenitore** -Mostra il numero di hello dei tipi di orchestrazione utilizzati in nodi/host contenitore. Hello computer nodi/host sono elencati anche dal numero di hello di contenitori. *Questo set di dati viene usato solo negli ambienti Linux.*
- **Inventario delle immagini contenitore** -Mostra numero totale di hello di immagini contenitore utilizzato e numero di tipi di immagine. numero di Hello delle immagini è inoltre elencato dal tag di immagine hello.
- **Lo stato di contenitori** -Mostra il numero totale di hello del contenitore di computer o l'host di nodi che dispongono di contenitori in esecuzione. I computer sono elencati anche dal numero di hello dell'esecuzione di host.
- **Processi del contenitore**: visualizza un grafico a linee dei processi del contenitore in esecuzione nel corso del tempo. I contenitori vengono anche indicati dal comando/processo in esecuzione nei contenitori. *Questo set di dati viene usato solo negli ambienti Linux.*
- **Prestazioni CPU contenitore** -Mostra un grafico a linee dell'utilizzo medio della CPU hello nel corso del tempo per i nodi di computer o gli host. Anche gli elenchi di hello computer nodi/ospita in base medio della CPU.
- **Prestazioni memoria contenitore**: visualizza un grafico a linee dell'utilizzo della memoria nel corso del tempo. Elenca anche l'utilizzo della memoria del computer in base al nome dell'istanza.
- **Prestazioni del computer** -Mostra i grafici a linee pari al % hello di prestazioni della CPU nel tempo, percentuale di utilizzo della memoria nel tempo e megabyte di spazio libero su disco nel tempo. È possibile passare il mouse su qualsiasi riga in un grafico di tooview ulteriori dettagli.


Ogni area del dashboard hello è una rappresentazione visiva di una ricerca eseguita sui dati raccolti.

![Dashboard Containers (Contenitori)](./media/log-analytics-containers/containers-dash01.png)

![Dashboard Containers (Contenitori)](./media/log-analytics-containers/containers-dash02.png)

In hello **stato contenitore** area, fare clic su area superiore hello, come illustrato di seguito.

![Stato dei contenitori](./media/log-analytics-containers/containers-status.png)

Verrà visualizzata la finestra di ricerca nei log, visualizzazione di informazioni sullo stato di hello i contenitori.

![Ricerca log per i contenitori](./media/log-analytics-containers/containers-log-search.png)

Da qui è possibile modificare toomodify query di ricerca hello è informazioni specifiche hello toofind si è interessati. Per altre informazioni sulle ricerche log, vedere [Ricerche nei log in Log Analytics](log-analytics-log-searches.md).

## <a name="troubleshoot-by-finding-a-failed-container"></a>Risolvere i problemi cercando un contenitore con errori

Log Analytics contrassegna un contenitore come **Non riuscito** se il contenitore è stato terminato con un codice di uscita diverso da zero. È possibile visualizzare una panoramica di hello errori e problemi nell'ambiente di hello in hello **Impossibile contenitori** area.

### <a name="toofind-failed-containers"></a>contenitori toofind non riuscita
1. Fare clic su hello **stato contenitore** area.  
   ![Stato dei contenitori](./media/log-analytics-containers/containers-status.png)
2. Ricerca nei log aprirà e visualizzerà stato hello i contenitori, simile toohello seguente.  
   ![stato dei contenitori](./media/log-analytics-containers/containers-log-search.png)
3. Successivamente, fare clic su valore hello aggregato di informazioni aggiuntive di tooview contenitori non riuscita. Espandere **Mostra altre** tooview hello immagine ID  
   ![contenitori non riusciti](./media/log-analytics-containers/containers-state-failed.png)  
4. Digitare quindi seguito hello nella query di ricerca hello. `Type=ContainerInventory <ImageID>`toosee informazioni dettagliate sull'immagine di hello quali dimensioni dell'immagine e il numero di immagini arrestate e non riuscite.  
   ![contenitori non riusciti](./media/log-analytics-containers/containers-failed04.png)

## <a name="search-logs-for-container-data"></a>Ricerca dei dati dei contenitori nei log
Quando si sta cercando di risolvere un errore specifico, può essere utile toosee in cui viene eseguito nell'ambiente in uso. Hello seguenti tipi di log consente di creare query informazioni hello tooreturn desiderate.


- **ContainerImageInventory** : usare questo tipo quando si cerca di informazioni sul toofind organizzate per immagine e tooview informazioni sulle immagini, ad esempio gli ID immagine o dimensioni.
- **ContainerInventory**: usare questo tipo per ottenere informazioni sul percorso dei contenitori, i relativi nomi e le immagini che eseguono.
- **ContainerLog** : usare questo tipo quando si desidera toofind informazioni nel registro errori specifici e le voci.
- **ContainerNodeInventory_CL** usare questo tipo di informazioni di hello/nodo host in cui sono presenti contenitori. Fornisce informazioni su versione di Docker, tipo di orchestrazione, risorsa di archiviazione e rete.
- **ContainerProcess_CL** tooquickly questo tipo di utilizzo visualizzare hello del processo in esecuzione all'interno del contenitore di hello.
- **ContainerServiceLog** : usare questo tipo quando si cerca informazioni toofind audit trail per hello daemon Docker, ad esempio avvio, arresto, eliminare o comandi pull.
- **KubeEvents_CL** utilizzare gli eventi di Kubernetes questo tipo toosee hello.
- **KubePodInventory_CL** utilizzare questo tipo quando si desiderano che le informazioni di gerarchia toounderstand hello cluster.


### <a name="toosearch-logs-for-container-data"></a>toosearch registri per i dati del contenitore
* Scegliere un'immagine che si è certi recentemente si sono verificati e cercare i log degli errori di hello. Iniziare cercando il nome di un contenitore che esegue l'immagine con una ricerca **ContainerInventory**. Cercare ad esempio `Type=ContainerInventory ubuntu Failed`  
    ![Cercare contenitori Ubuntu](./media/log-analytics-containers/search-ubuntu.png)

  Hello nome del contenitore hello accanto troppo**nome**e cercare tali log. In questo esempio si tratta di `Type=ContainerLog cranky_stonebreaker`.

**Visualizzare le informazioni sulle prestazioni**

Quando si sta iniziando tooconstruct query, può essere utile toosee ciò che è possibile innanzitutto. Ad esempio, eseguire una query toosee ricerca di tutti i dati sulle prestazioni, provare una query ampia digitando hello seguente.

```
Type=Perf
```

![prestazioni dei contenitori](./media/log-analytics-containers/containers-perf01.png)

È possibile definire l'ambito di dati sulle prestazioni hello risposta tooa specifico contenitore digitando il nome di hello di esso toohello a destra della query.

```
Type=Perf <containerName>
```

Che mostra l'elenco di hello delle metriche delle prestazioni raccolti per un singolo contenitore.

![prestazioni dei contenitori](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a>Esempio di query di ricerca log
È spesso utile toobuild esegue una query a partire da un esempio o due e quindi modificandoli toofit l'ambiente. Come punto di partenza, è possibile sperimentare hello **query di esempio** toohelp area si compila una query più avanzate.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Query sui contenitori](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a>Salvataggio delle query di ricerca log
Il salvataggio di query è una funzionalità standard di Log Analytics. Le query salvate potranno essere riusate rapidamente in futuro.

Dopo aver creato una query che utile, salvarlo facendo **Preferiti** nella parte superiore di hello della pagina di ricerca nei Log hello. Quindi è possibile accedervi facilmente in un secondo momento da hello **My Dashboard** pagina.

## <a name="next-steps"></a>Passaggi successivi
* [Ricerca dei registri](log-analytics-log-searches.md) tooview dettagliate record dei dati contenitore.

---
title: HDInsight con rete virtuale di Azure - aaaExtend | Documenti Microsoft
description: Informazioni su come toouse rete virtuale di Azure tooconnect HDInsight tooother cloud risorse o le risorse nel Data Center
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a>Estendere Azure HDInsight usando Rete virtuale di Azure

Informazioni su come toouse HDInsight con un [rete virtuale di Azure](../virtual-network/virtual-networks-overview.md). L'utilizzo di una rete virtuale di Azure consente hello seguenti scenari:

* Connessione tooHDInsight direttamente da una rete locale.

* Connessione toodata HDInsight vengono archiviati in una rete virtuale di Azure.

* L'accesso ai servizi di Hadoop che non sono disponibili pubblicamente in salve direttamente a internet. Ad esempio, le API Kafka o hello API Java HBase.

> [!WARNING]
> informazioni di Hello in questo documento richiedono la comprensione delle reti TCP/IP. Se non si ha familiarità con la rete TCP/IP, è necessario collaborare con un utente prima di apportare modifiche tooproduction reti.

## <a name="planning"></a>Pianificazione

di seguito Hello sono domande hello che è necessario rispondere durante la pianificazione tooinstall HDInsight in una rete virtuale:

* È necessario tooinstall HDInsight in una rete virtuale esistente? Oppure si intende creare una rete nuova?

    Se si utilizza una rete virtuale esistente, potrebbe essere la configurazione di rete hello toomodify prima di poter installare HDInsight. Per ulteriori informazioni, vedere hello [aggiungere la rete virtuale esistente di HDInsight tooan](#existingvnet) sezione.

* Si desidera rete virtuale hello tooconnect contenente una rete virtuale di HDInsight tooanother o la rete locale?

    lavoro tooeasily con risorse tra le reti, è possibile necessario toocreate un DNS personalizzato e configurare l'inoltro di DNS. Per ulteriori informazioni, vedere hello [la connessione di più reti](#multinet) sezione.

* Si desidera toorestrict/reindirizzamento del traffico in ingresso o in uscita tooHDInsight?

    HDInsight deve avere la comunicazione con indirizzi IP specifici nel hello data center di Azure senza restrizioni. Sono presenti anche diverse porte che devono essere abilitate attraverso i firewall per la comunicazione client. Per ulteriori informazioni, vedere hello [controllare il traffico di rete](#networktraffic) sezione.

## <a id="existingvnet"></a>Aggiungere la rete virtuale esistente tooan a HDInsight

Utilizzare i passaggi di hello in questa sezione di toodiscover come tooadd un tooan HDInsight nuova rete virtuale di Azure esistente.

> [!NOTE]
> È possibile aggiungere un cluster HDInsight esistente in una rete virtuale.

1. Si sta utilizzando un classico o il modello di distribuzione di gestione risorse per la rete virtuale hello?

    HDInsight 3.4 e versione successiva richiedono l'utilizzo di una rete virtuale di Resource Manager. Le versioni precedenti di HDInsight richiedono una rete virtuale classica.

    Se la rete esistente è una rete virtuale classica, è necessario creare una rete virtuale di gestione delle risorse e quindi connettersi hello due. [Connessione toonew reti virtuali classiche reti virtuali](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

    Una volta inserito, HDInsight installato nella rete di gestione risorse di hello possibile interagire con le risorse di rete classiche hello.

2. Si usa il tunneling forzato? Il tunneling forzato è impostata una subnet che forza una periferica di tooa il traffico Internet in uscita per l'ispezione e la registrazione. HDInsight non supporta il tunneling forzato. Occorre quindi rimuovere questa funzionalità prima di installare HDInsight in una subnet oppure si può creare una nuova subnet per HDInsight.

3. Si usano gruppi di sicurezza di rete, le route definite dall'utente o il traffico toorestrict ai dispositivi di rete virtuale da o verso la rete virtuale hello?

    Come servizio gestito, HDInsight richiede l'accesso illimitato tooseveral degli indirizzi IP in hello data center di Azure. tooallow comunicazione con questi indirizzi IP, aggiornare eventuali gruppi di sicurezza di rete esistente o di una route definita dall'utente.

    HDInsight ospita più servizi, che usano porte diverse. Non bloccare le porte toothese di traffico. Per un elenco di porte tooallow attraverso i firewall appliance virtuale, vedere hello [sicurezza](#security) sezione.

    toofind la configurazione di protezione esistente, utilizzare hello seguenti comandi di Azure PowerShell o l'interfaccia CLI di Azure:

    * Gruppi di sicurezza di rete

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        Per ulteriori informazioni, vedere hello [risolvere i problemi relativi a gruppi di sicurezza di rete](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) documento.

        > [!IMPORTANT]
        > Le regole di gruppo di sicurezza di rete vengono applicate seguendo un ordine basato sulla priorità delle regole. viene applicata Hello prima regola corrispondente a modello di traffico hello e non da altri vengono applicate per il traffico. Ordine delle regole da tooleast più permissivo. Per ulteriori informazioni, vedere hello [filtrare il traffico di rete con gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md) documento.

    * Route definite dall'utente

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        Per ulteriori informazioni, vedere hello [risolvere route](../virtual-network/virtual-network-routes-troubleshoot-portal.md) documento.

4. Creare un cluster HDInsight e selezionare la rete virtuale di Azure hello durante la configurazione. Usare i passaggi di hello in hello successivo processo di creazione di documenti toounderstand hello cluster:

    * [Creare utilizzando hello portale di Azure HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [Creare cluster HDInsight tramite Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [Creare cluster HDInsight tramite l'interfaccia della riga di comando di Azure 1.0](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [Creare cluster HDInsight tramite un modello Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > Aggiunta di HDInsight tooa di rete virtuale è un passaggio di configurazione facoltativa. Essere la rete virtuale che tooselect hello durante la configurazione cluster hello.

## <a id="multinet"></a>Connessione a più reti

sfida Hello con una configurazione di multi-rete è la risoluzione dei nomi tra reti hello.

Azure assicura la risoluzione dei nomi per i servizi di Azure che vengono installati in una rete virtuale. La risoluzione dei nomi predefinito consente di HDInsight tooconnect toohello seguenti risorse utilizzando un nome di dominio completo (FQDN):

* Qualsiasi risorsa che è disponibile in hello internet. ad esempio microsoft.com, google.com.

* Qualsiasi risorsa che è in hello stessa rete virtuale di Azure tramite hello __nomi DNS interni__ della risorsa hello. Ad esempio, quando si utilizza la risoluzione dei nomi predefinito di hello, hello di seguito è esempio interno DNS nomi tooHDInsight assegnati i nodi di lavoro:

    * wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net
    * wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net

    Entrambi questi nodi possono comunicare direttamente tra loro e con altri nodi in HDInsight, usando i nomi DNS interni.

risoluzione dei nomi predefinito Hello __non__ consentire HDInsight tooresolve nomi hello delle risorse nella rete virtuale toohello unita in join le reti. Ad esempio, è comune toojoin toohello di rete virtuale di rete locale. Con solo hello risoluzione dei nomi predefiniti, HDInsight non è possibile accedere alle risorse nella rete locale hello in base al nome. Hello opposto è anche true, le risorse nella rete locale non è possibile accedere alle risorse nella rete virtuale hello in base al nome.

> [!WARNING]
> È necessario creare un server DNS personalizzato hello e configurare hello toouse di rete virtuale, prima di creare hello cluster HDInsight.

risoluzione dei nomi tooenable tra la rete virtuale hello e risorse in reti unita in join, è necessario eseguire hello seguenti azioni:

1. Creare un server DNS personalizzato nella rete virtuale di Azure in cui si prevede di tooinstall HDInsight hello.

2. Configurare hello rete virtuale toouse hello server DNS personalizzato.

3. Trovare hello che Azure viene assegnato il suffisso DNS per la rete virtuale. Questo valore è troppo simile`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`. Per informazioni sulla ricerca suffisso DNS hello, vedere hello [esempio: DNS personalizzato](#example-dns) sezione.

4. Configurare l'inoltro tra i server DNS hello. configurazione di Hello dipende dal tipo di hello della rete remota.

    * Se la rete remota hello è una rete locale, configurare il DNS come indicato di seguito:
        
        * __DNS personalizzato__ (in rete virtuale hello):

            * Inoltrare le richieste per il suffisso DNS hello del sistema di risoluzione ricorsiva Azure di hello rete virtuale toohello (168.63.129.16). Azure gestisce le richieste di risorse nella rete virtuale hello

            * Tutte le altre richieste toohello locale servizio DNS di inoltro. Hello locale DNS gestisce tutte le altre richieste di risoluzione nome, anche le richieste per le risorse internet, ad esempio Microsoft.com.

        * __DNS locale__: inoltrare le richieste per hello rete virtuale DNS suffisso toohello server DNS personalizzato. un server DNS personalizzato Hello inoltra quindi toohello ricorsiva Azure resolver.

        Richieste di route questa configurazione per i nomi di dominio che contengono il suffisso DNS hello del server DNS personalizzato di hello rete virtuale toohello completo. Tutte le altre richieste (anche per gli indirizzi internet pubblici) vengono gestiti dal server DNS locale di hello.

    * Se la rete remota hello è un'altra rete virtuale di Azure, configurare il DNS come indicato di seguito:

        * __DNS personalizzato__ (in ogni rete virtuale):

            * Le richieste per il suffisso DNS hello di reti virtuali hello vengono inoltrate toohello i server DNS personalizzati. Hello DNS in ogni rete virtuale è responsabile per la risoluzione delle risorse all'interno della rete.

            * Inoltrare tutti gli altri resolver ricorsivo Azure toohello di richieste. resolver ricorsivo Hello è responsabile della risoluzione locale e alle risorse internet.

        server DNS Hello per ogni rete inoltra le richieste toohello altri, basata sul suffisso DNS. Le altre richieste vengono risolti mediante resolver ricorsivo Azure hello.

    Per un esempio di ogni configurazione, vedere hello [esempio: DNS personalizzato](#example-dns) sezione.

Per ulteriori informazioni, vedere hello [risoluzione dei nomi per le macchine virtuali e istanze del ruolo](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) documento.

## <a name="directly-connect-toohadoop-services"></a>Connettersi direttamente servizi tooHadoop

La maggior parte delle documentazione su HDInsight si presuppone la presenza di cluster di accesso toohello su hello internet. Ad esempio, che è possibile connettersi cluster toohello https://CLUSTERNAME.azurehdinsight.net. Questo indirizzo Usa gateway hello pubblico, non è disponibile se è stato utilizzato NSGs o UDRs toorestrict accesso da hello internet.

tooconnect tooAmbari e le altre pagine web attraverso la rete virtuale di hello, utilizzare hello alla procedura seguente:

1. toodiscover nomi di dominio completo interno hello (FQDN) dei nodi del cluster HDInsight hello, utilizzare uno dei seguenti metodi hello:

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    Nell'elenco di nodi restituiti hello trovare hello FQDN per hello nodi head e utilizzare hello FQDN tooconnect tooAmbari e altri servizi web. Ad esempio, utilizzare `http://<headnode-fqdn>:8080` tooaccess Ambari.

    > [!IMPORTANT]
    > Alcuni servizi ospitate nei nodi head hello attivi solo in un nodo alla volta. Se si tenta di accedere al servizio in un nodo head e viene restituito un errore 404, passare toohello altro nodo head.

2. nodo hello toodetermine e la porta di un servizio è disponibile, vedere hello [porte utilizzate da servizi di Hadoop in HDInsight](./hdinsight-hadoop-port-settings-for-services.md) documento.

## <a id="networktraffic"></a> Controllo del traffico di rete

Traffico di rete in un reti virtuali di Azure può essere controllato utilizzando hello dei seguenti metodi:

* **Gruppi di sicurezza di rete** (gruppo) consentono di rete di toohello toofilter traffico in entrata e in uscita. Per ulteriori informazioni, vedere hello [filtrare il traffico di rete con gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md) documento.

    > [!WARNING]
    > HDInsight non supporta la limitazione del traffico in uscita.

* **Le route definite dall'utente** (UDR) definiscono il flusso di traffico tra le risorse nella rete hello. Per ulteriori informazioni, vedere hello [le route definite dall'utente e l'inoltro IP](../virtual-network/virtual-networks-udr-overview.md) documento.

* **Dispositivi di rete virtuale** replicare hello le funzionalità dei dispositivi, ad esempio router e firewall. Per ulteriori informazioni, vedere hello [ai dispositivi di rete](https://azure.microsoft.com/solutions/network-appliances) documento.

Come servizio gestito, HDInsight richiede l'accesso illimitato tooAzure integrità e la gestione servizi in cloud di Azure hello. Quando si usano i gruppi di sicurezza di rete e le route definite dall'utente, è necessario assicurarsi che questi servizi possano ancora comunicare con HDInsight.

HDInsight espone i servizi su porte diverse. Quando si utilizza un firewall appliance virtuale, è necessario consentire il traffico su hello porte usate per questi servizi. Per ulteriori informazioni, vedere la sezione hello [porte necessarie].

### <a id="hdinsight-ip"></a>HDInsight con gruppi di sicurezza di rete e route definite dall'utente

Se si intende usare **gruppi di sicurezza di rete** o **le route definite dall'utente** toocontrol il traffico di rete, eseguire hello seguenti azioni prima di installare HDInsight:

1. Identificare hello regione di Azure che si prevede di toouse per HDInsight.

2. Identificare gli indirizzi IP hello necessari da HDInsight. Per ulteriori informazioni, vedere hello [indirizzi IP richiesti da HDInsight](#hdinsight-ip) sezione.

3. Creare o modificare gruppi di sicurezza di rete hello o le route definite dall'utente per la subnet hello pianificare tooinstall HDInsight in.

    * __Gruppi di sicurezza di rete__: Consenti __in ingresso__ il traffico sulla porta __443__ da indirizzi IP hello.
    * __Le route definite dall'utente__: creare un indirizzo IP tooeach di route e impostare hello __tipo dell'hop successivo__ too__Internet__.

Per ulteriori informazioni su gruppi di sicurezza di rete o le route definite dall'utente, vedere hello seguente documentazione:

* [Gruppo di sicurezza di rete](../virtual-network/virtual-networks-nsg.md)

* [Route definite dall'utente](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a>Tunneling forzato

Il tunneling forzato è una configurazione di routing definite dall'utente in cui tutto il traffico da una subnet è forzato tooa specifici di rete o posizione, ad esempio la rete locale. HDInsight __non__ supporta il tunneling forzato.

## <a id="hdinsight-ip"></a> Indirizzi IP richiesti

> [!IMPORTANT]
> Hello Azure integrità e servizi di gestione devono essere in grado di toocommunicate con HDInsight. Se si utilizzano gruppi di sicurezza di rete o le route definite dall'utente, consentire il traffico dal hello gli indirizzi IP per questi tooreach servizi HDInsight.
>
> Se non si utilizza gruppi di sicurezza di rete o il traffico toocontrol le route definite dall'utente, è possibile ignorare questa sezione.

Se si utilizzano gruppi di sicurezza di rete o le route definite dall'utente, è necessario consentire il traffico proveniente da hello Azure health e Gestione servizi tooreach HDInsight. Utilizzare hello seguendo i passaggi toofind hello indirizzi IP devono essere consentiti:

1. È sempre necessario consentire il traffico proveniente da hello seguenti indirizzi IP:

    | Indirizzo IP | Porta consentita | Direzione |
    | ---- | ----- | ----- |
    | 168.61.49.99 | 443 | In ingresso |
    | 23.99.5.239 | 443 | In ingresso |
    | 168.61.48.131 | 443 | In ingresso |
    | 138.91.141.162 | 443 | In ingresso |

2. Se il cluster HDInsight è in uno dei seguenti aree hello, è necessario consentire il traffico proveniente da indirizzi IP di hello elencati per area hello:

    > [!IMPORTANT]
    > Se non è elencato hello regione di Azure in uso, quindi utilizzare solo quattro indirizzi IP hello dal passaggio 1.

    | Paese | Region | Indirizzi IP consentiti | Porta consentita | Direzione |
    | ---- | ---- | ---- | ---- | ----- |
    | Asia | Asia orientale | 23.102.235.122</br>52.175.38.134 | 443 | In ingresso |
    | &nbsp; | Asia sudorientale | 13.76.245.160</br>13.76.136.249 | 443 | In ingresso |
    | Australia | Australia orientale | 104.210.84.115</br>13.75.152.195 | 443 | In ingresso |
    | &nbsp; | Australia sudorientale | 13.77.2.56</br>13.77.2.94 | 443 | In ingresso |
    | Brasile | Brasile meridionale | 191.235.84.104</br>191.235.87.113 | 443 | In ingresso |
    | Canada | Canada orientale | 52.229.127.96</br>52.229.123.172 | 443 | In ingresso |
    | &nbsp; | Canada centrale | 52.228.37.66</br>52.228.45.222 | 443 | In ingresso |
    | Cina | Cina settentrionale | 42.159.96.170</br>139.217.2.219 | 443 | In ingresso |
    | &nbsp; | Cina orientale | 42.159.198.178</br>42.159.234.157 | 443 | In ingresso |
    | Europa | Europa settentrionale | 52.164.210.96</br>13.74.153.132 | 443 | In ingresso |
    | &nbsp; | Europa occidentale| 52.166.243.90</br>52.174.36.244 | 443 | In ingresso |
    | Germania | Germania centrale | 51.4.146.68</br>51.4.146.80 | 443 | In ingresso |
    | &nbsp; | Germania nord-orientale | 51.5.150.132</br>51.5.144.101 | 443 | In ingresso |
    | India | India centrale | 52.172.153.209</br>52.172.152.49 | 443 | In ingresso |
    | Giappone | Giappone orientale | 13.78.125.90</br>13.78.89.60 | 443 | In ingresso |
    | &nbsp; | Giappone occidentale | 40.74.125.69</br>138.91.29.150 | 443 | In ingresso |
    | Corea | Corea centrale | 52.231.39.142</br>52.231.36.209 | 433 | In ingresso |
    | &nbsp; | Corea meridionale | 52.231.203.16</br>52.231.205.214 | 443 | In ingresso
    | Regno Unito | Regno Unito occidentale | 51.141.13.110</br>51.141.7.20 | 443 | In ingresso |
    | &nbsp; | Regno Unito meridionale | 51.140.47.39</br>51.140.52.16 | 443 | In ingresso |
    | Stati Uniti | Stati Uniti centrali | 13.67.223.215</br>40.86.83.253 | 443 | In ingresso |
    | &nbsp; | Stati Uniti centro-settentrionali | 157.56.8.38</br>157.55.213.99 | 443 | In ingresso |
    | &nbsp; | Stati Uniti centro-occidentali | 52.161.23.15</br>52.161.10.167 | 443 | In ingresso |
    | &nbsp; | Stati Uniti occidentali 2 | 52.175.211.210</br>52.175.222.222 | 443 | In ingresso |

    Per informazioni su IP hello indirizzi toouse per Azure per enti pubblici, vedere hello [Azure per enti pubblici Intelligence + Analitica](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) documento.

3. Se si usa un server DNS personalizzato con la rete virtuale, è anche necessario consentire l'accesso da __168.63.129.16__. Questo è l'indirizzo del sistema di risoluzione ricorsiva di Azure. Per ulteriori informazioni, vedere hello [la risoluzione dei nomi per le macchine virtuali e il ruolo istanze](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) documento.

Per ulteriori informazioni, vedere hello [controllare il traffico di rete](#networktraffic) sezione.

## <a id="hdinsight-ports"></a> Porte richieste

Se si intende usare una rete **firewall appliance virtuale** toosecure la rete virtuale hello, è necessario consentire il traffico in uscita hello seguenti porte:

* 53
* 443
* 1433
* 11000-11999
* 14000-14999

Per un elenco di porte per servizi specifici, vedere hello [porte utilizzate da servizi di Hadoop in HDInsight](hdinsight-hadoop-port-settings-for-services.md) documento.

Per ulteriori informazioni sulle regole firewall per i dispositivi virtuali, vedere hello [scenario appliance virtuale](../virtual-network/virtual-network-scenario-udr-gw-nva.md) documento.

## <a id="hdinsight-nsg"></a>Ad esempio: gruppi di sicurezza di rete con HDInsight

esempi di Hello in questa sezione illustrano come gruppo di sicurezza di rete toocreate regole che consentono di HDInsight toocommunicate con hello servizi di gestione di Azure. Prima di usare esempi di hello regolare hello IP indirizzi toomatch hello quelli per hello regione di Azure in uso. È possibile trovare queste informazioni in hello [HDInsight con gruppi di sicurezza di rete e le route definite dall'utente](#hdinsight-ip) sezione.

### <a name="azure-resource-management-template"></a>Modello di Resource Manager di Azure

Hello seguente modello di gestione delle risorse consente di creare una rete virtuale che consente di limitare il traffico in ingresso, ma consente il traffico proveniente da indirizzi IP hello necessario da HDInsight. Questo modello crea anche un cluster HDInsight nella rete virtuale hello.

* [Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/) (Distribuire una rete virtuale di Azure protetta e un cluster Hadoop HDInsight)

> [!IMPORTANT]
> Modificare gli indirizzi IP hello utilizzati in questo hello toomatch esempio regione di Azure in uso. È possibile trovare queste informazioni in hello [HDInsight con gruppi di sicurezza di rete e le route definite dall'utente](#hdinsight-ip) sezione.

### <a name="azure-powershell"></a>Azure PowerShell

Utilizzare hello seguente script di PowerShell toocreate una rete virtuale che consente di limitare il traffico in ingresso e consente il traffico proveniente da hello gli indirizzi IP per l'area Europa settentrionale hello.

> [!IMPORTANT]
> Modificare gli indirizzi IP hello utilizzati in questo hello toomatch esempio regione di Azure in uso. È possibile trovare queste informazioni in hello [HDInsight con gruppi di sicurezza di rete e le route definite dall'utente](#hdinsight-ip) sezione.

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> In questo esempio viene illustrato come tooadd tooallow di regole in entrata traffico sugli indirizzi IP hello necessario. Non contiene una regola toorestrict accesso in entrata da altre origini.
>
> Hello di esempio seguente viene illustrato come accedere tooenable SSH da hello Internet:
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

Utilizzare i seguenti passaggi toocreate una rete virtuale che consente di limitare il traffico in ingresso, ma consente il traffico proveniente da indirizzi IP hello necessario da HDInsight hello.

1. Hello utilizzo successivo comando toocreate un nuovo gruppo di sicurezza di rete denominato `hdisecure`. Sostituire **RESOURCEGROUPNAME** con gruppo di risorse hello contenente hello rete virtuale di Azure. Sostituire **percorso** con percorso hello (area) creato in quel gruppo hello.

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    Dopo aver creato il gruppo di hello, vengono visualizzate informazioni sul nuovo gruppo di hello.

2. Utilizzare hello seguente tooadd regole toohello nuovo gruppo di sicurezza rete che consentono le comunicazioni in ingresso sulla porta 443 da hello servizio integrità e la gestione di Azure HDInsight. Sostituire **RESOURCEGROUPNAME** con nome hello hello del gruppo di risorse contenente hello rete virtuale di Azure.

    > [!IMPORTANT]
    > Modificare gli indirizzi IP hello utilizzati in questo hello toomatch esempio regione di Azure in uso. È possibile trovare queste informazioni in hello [HDInsight con gruppi di sicurezza di rete e le route definite dall'utente](#hdinsight-ip) sezione.

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. tooretrieve hello identificatore univoco per questo gruppo di sicurezza di rete, utilizzare hello comando seguente:

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    Questo comando restituisce un toohello simile valore testo seguente:

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    Utilizzare virgolette doppie id comando hello se non si ottengono risultati hello previsto.

4. Utilizzare hello successivo comando tooapply hello rete sicurezza gruppo tooa subnet. Sostituire hello __GUID__ e __RESOURCEGROUPNAME__ valori con quelli hello restituito dal passaggio precedente hello. Sostituire __VNETNAME__ e __SUBNETNAME__ con il nome di rete virtuale hello e subnet che si desidera toocreate.

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    Dopo il completamento del comando, è possibile installare HDInsight in hello rete virtuale.

> [!IMPORTANT]
> Questi passaggi aprire solo accesso toohello HDInsight integrità e la gestione del servizio nel cloud di Azure hello. Qualsiasi altro accesso toohello cluster HDInsight da hello di fuori rete virtuale è bloccata. accesso tooenable da rete virtuale esterna hello, è necessario aggiungere regole aggiuntive di gruppo di sicurezza di rete.
>
> Hello di esempio seguente viene illustrato come accedere tooenable SSH da hello Internet:
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <a id="example-dns"></a> Esempio: configurazione DNS

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a>Risoluzione dei nomi tra una rete virtuale e una rete locale connessa

In questo esempio viene hello seguenti presupposti:

* Si dispone di una rete virtuale di Azure che è una rete locale tooan connessi tramite un gateway VPN.

* server DNS personalizzato Hello nella rete virtuale hello è in esecuzione Linux o Unix come sistema operativo hello.

* [Associare](https://www.isc.org/downloads/bind/) è installato nel server DNS personalizzato hello.

Nel server DNS personalizzato hello nella rete virtuale hello:

1. Utilizza Azure PowerShell o Azure CLI toofind hello il suffisso DNS della rete virtuale hello:

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. Nel server DNS personalizzato hello per la rete virtuale hello, utilizzare hello segue testo come contenuto di hello di hello `/etc/bind/named.conf.local` file:

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    Sostituire hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` valore con il suffisso DNS hello della rete virtuale.

    Questa configurazione consente di indirizzare tutte le richieste DNS per il suffisso DNS hello del sistema di risoluzione ricorsiva Azure toohello di hello rete virtuale.

2. Nel server DNS personalizzato hello per la rete virtuale hello, utilizzare hello segue testo come contenuto di hello di hello `/etc/bind/named.conf.options` file:

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * Sostituire hello `10.0.0.0/16` valore con l'intervallo di indirizzi IP hello della rete virtuale. Questa voce consente l'indirizzamento delle richieste di risoluzione dei nomi all'interno di questo intervallo.

    * Aggiungi intervallo di indirizzi IP hello di hello locale rete toohello `acl goodclients { ... }` sezione.  voce consente le richieste di risoluzione nome dalle risorse nella rete locale hello.
    
    * Sostituire il valore di hello `192.168.0.1` con indirizzo IP di hello del server DNS locale. Questa voce indirizza tutte le altre richieste toohello locale DNS server DNS.

3. configurazione di hello toouse, riavviare l'operazione di binding. ad esempio `sudo service bind9 restart`.

4. Aggiungere un server DNS di server d'inoltro condizionale toohello locale. Configurare le richieste di hello server d'inoltro condizionale toosend per il suffisso DNS hello dal passaggio 1 toohello un server DNS personalizzato.

    > [!NOTE]
    > Consultare la documentazione hello per il DNS per informazioni dettagliate su come tooadd un server d'inoltro condizionale.

Dopo aver completato questi passaggi, è possibile connettersi tooresources in una rete tramite nomi di dominio completo (FQDN). È ora possibile installare HDInsight in rete virtuale hello.

### <a name="name-resolution-between-two-connected-virtual-networks"></a>Risoluzione dei nomi tra due reti virtuali connesse

In questo esempio viene hello seguenti presupposti:

* Si dispone di due reti virtuali di Azure connesse tramite gateway VPN o peering.

* server DNS personalizzato Hello in entrambe le reti è in esecuzione Linux o Unix come sistema operativo hello.

* [Associare](https://www.isc.org/downloads/bind/) è installato nel server DNS personalizzati hello.

1. Utilizza Azure PowerShell o Azure CLI toofind hello il suffisso DNS di entrambe le reti virtuali:

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. Hello utilizzo successivo di testo come contenuto di hello di hello `/etc/bind/named.config.local` file in un server DNS personalizzato hello. Apportare questa modifica nel server DNS personalizzato hello in entrambe le reti virtuali.

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    Sostituire hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` valore con il suffisso DNS hello hello __altri__ rete virtuale. Questa voce instrada le richieste per il suffisso DNS hello di hello rete remota toohello personalizzato DNS nella rete.

3. Nei server DNS personalizzato hello di entrambe le reti virtuali, utilizzare hello segue testo come contenuto di hello di hello `/etc/bind/named.conf.options` file:

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * Sostituire hello `10.0.0.0/16` e `10.1.0.0/16` valori con IP hello intervalli della rete virtuale di indirizzi. Questa voce consente le risorse in ogni rete toomake le richieste dei server DNS hello.

    Tutte le richieste che non sono per i suffissi DNS hello di reti virtuali hello (ad esempio microsoft.com) viene gestita dal sistema di risoluzione ricorsiva Azure hello.

4. configurazione di hello toouse, riavviare l'operazione di binding. Ad esempio `sudo service bind9 restart` su entrambi i server DNS.

Dopo aver completato questi passaggi, è possibile connettersi tooresources nella rete virtuale di hello utilizzando nomi di dominio completo (FQDN). È ora possibile installare HDInsight in rete virtuale hello.

## <a name="next-steps"></a>Passaggi successivi

* Per un esempio end-to-end di configurazione di rete locale tooan tooconnect di HDInsight, vedere [rete locale di connettersi a HDInsight tooan](./connect-on-premises-network.md).

* Per ulteriori informazioni su reti virtuali di Azure, vedere hello [Cenni preliminari sulla rete virtuale di Azure](../virtual-network/virtual-networks-overview.md).

* Per altre informazioni sui gruppi di sicurezza di rete, vedere [Gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md).

* Per altre informazioni sulle route definite dall'utente, vedere [Route definite dall'utente e inoltro IP](../virtual-network/virtual-networks-udr-overview.md).
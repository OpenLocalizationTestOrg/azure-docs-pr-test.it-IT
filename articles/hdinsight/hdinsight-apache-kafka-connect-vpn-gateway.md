---
title: tooKafka aaaConnect usando le reti virtuali - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toodirectly connettersi tooKafka in HDInsight tramite una rete virtuale di Azure. Informazioni su come della rete tooconnect tooKafka dai client di sviluppo tramite un gateway VPN o dai client in locale tramite un dispositivo gateway VPN.
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.custom: hdinsightactive
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/01/2017
ms.author: larryfr
ms.openlocfilehash: 03542fe14b9a1d010dffa22a8f8d96b098a1576e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a>Connettersi tooKafka in HDInsight (anteprima) tramite una rete virtuale di Azure

Informazioni su come toodirectly connettersi tooKafka in HDInsight con reti virtuali di Azure. Questo documento vengono fornite informazioni sulla connessione tooKafka utilizzando hello seguenti configurazioni:

* Dalle risorse in una rete locale. La connessione viene stabilita tramite un dispositivo VPN, un software o un hardware, nella rete locale.
* Da un ambiente di sviluppo tramite un client software VPN.

## <a name="architecture-and-planning"></a>Architettura e pianificazione

HDInsight non consente la connessione diretta tooKafka su hello rete internet pubblica. Invece necessario utilizzare uno dei seguenti metodi di connessione hello client Kafka (producer e consumer):

* Eseguire il client di hello in hello stessa rete virtuale Kafka in HDInsight. Questa configurazione viene utilizzata in hello [iniziano con Apache Kafka (anteprima) in HDInsight](hdinsight-apache-kafka-get-started.md) documento. i nodi del cluster su hello HDInsight Hello client esegue direttamente o in un'altra macchina virtuale di hello stesso rete.

* Connettere una rete privata, ad esempio la rete locale, la rete virtuale toohello. Questa configurazione consente ai client il lavoro toodirectly di rete locale con Kafka. tooenable questa configurazione, eseguire hello seguenti attività:

    1. Creare una rete virtuale.
    2. Creare un gateway VPN che usi una configurazione da sito a sito. configurazione di Hello utilizzata in questo documento si connette dispositivo gateway VPN di tooa nella rete locale.
    3. Creare un server DNS nella rete virtuale hello.
    4. Configurare l'inoltro tra i server DNS hello in ogni rete.
    5. Installare Kafka in HDInsight in rete virtuale hello.

    Per ulteriori informazioni, vedere hello [connettersi tooKafka da una rete locale](#on-premises) sezione. 

* Connettere la rete virtuale toohello singoli computer tramite un gateway VPN e il client VPN. tooenable questa configurazione, eseguire hello seguenti attività:

    1. Creare una rete virtuale.
    2. Creare un gateway VPN che usi una configurazione da punto a sito. Questa configurazione offre un client VPN che può essere installato nei client Windows.
    3. Installare Kafka in HDInsight in rete virtuale hello.
    4. Configurare Kafka per la pubblicità IP. Questa configurazione consente hello client tooconnect con IP addressing anziché i nomi di dominio.
    5. Scaricare e usare i client VPN hello nel sistema di sviluppo hello.

    Per ulteriori informazioni, vedere hello [tooKafka si connettono con un client VPN](#vpnclient) sezione.

    > [!WARNING]
    > Questa configurazione è consigliata solo per scopi di sviluppo a causa di hello limitazioni seguenti:
    >
    > * Ogni client deve connettersi usando un client software VPN. Azure offre solo un client basato su Windows.
    > * client Hello non passa nome risoluzione richieste toohello rete virtuale, è necessario utilizzare indirizzi toocommunicate con Kafka IP. Comunicazione con gli IP richiede ulteriori configurazioni in cluster Kafka hello.

Per altre informazioni sull'uso di HDInsight in una rete virtuale, vedere [Estendere le funzionalità di HDInsight usando Rete virtuale di Azure](./hdinsight-extend-hadoop-virtual-network.md).

## <a id="on-premises"></a>Connettersi tooKafka da una rete locale

toocreate un cluster Kafka che comunica con la rete locale, seguire i passaggi hello hello [rete locale di connettersi a HDInsight tooyour](./connect-on-premises-network.md) documento.

> [!IMPORTANT]
> Quando si crea il cluster di HDInsight hello, selezionare hello __Kafka__ del cluster di tipo.

Questi passaggi creano hello seguente configurazione:

* Rete virtuale di Azure
* Gateway VPN da sito a sito
* Account di archiviazione di Azure, usato da HDInsight
* Kafka in HDInsight

tooverify che un client di Kafka può connettersi toohello cluster locale, utilizzare i passaggi di hello in hello [esempio: client Python](#python-client) sezione.

## <a id="vpnclient"></a>Connettersi tooKafka con un client VPN

Usare i passaggi di hello in questo hello toocreate sezione seguente configurazione:

* Rete virtuale di Azure
* Gateway VPN da punto a sito
* Account di archiviazione di Azure, usato da HDInsight
* Kafka in HDInsight

1. Seguire i passaggi hello hello [utilizzano certificati autofirmati per le connessioni Point-to-site](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) documento. Questo documento consente di creare certificati hello necessari per il gateway hello.

2. Aprire un prompt dei comandi di PowerShell e usare hello seguente codice toolog in tooyour sottoscrizione di Azure:

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. Utilizzare hello variabili toocreate di codice che contengono informazioni di configurazione seguente:

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is hello resource group name?"
    $baseName = Read-Host "What is hello base name? It is used toocreate names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want toocreate hello resources in?"
    $rootCert = Read-Host "What is hello file path toohello root certificate? It is used toosecure hello VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter hello HTTPS user name and password for hello HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter hello SSH user name and password for hello HDInsight cluster" -UserName "sshuser"

    # Names for Azure resources
    $networkName = "net-$baseName"
    $clusterName = "kafka-$baseName"
    $storageName = "store$baseName" # Can't use dashes in storage names
    $defaultContainerName = $clusterName
    $defaultSubnetName = "default"
    $gatewaySubnetName = "GatewaySubnet"
    $gatewayPublicIpName = "GatewayIp"
    $gatewayIpConfigName = "GatewayConfig"
    $vpnRootCertName = "rootcert"
    $vpnName = "VPNGateway"

    # Network settings
    $networkAddressPrefix = "10.0.0.0/16"
    $defaultSubnetPrefix = "10.0.0.0/24"
    $gatewaySubnetPrefix = "10.0.1.0/24"
    $vpnClientAddressPool = "172.16.201.0/24"

    # HDInsight settings
    $HdiWorkerNodes = 4
    $hdiVersion = "3.5"
    $hdiType = "Kafka"
    ```

4. Gruppo di risorse di Azure toocreate hello e rete virtuale di codice seguente hello di utilizzo:

    ```powershell
    # Create hello resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create hello subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get hello network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for hello gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get hello certificate info
    # Get hello full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create hello VPN gateway
    New-AzureRmVirtualNetworkGateway -Name $vpnName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -IpConfigurations $gatewayIpConfig `
        -GatewayType Vpn `
        -VpnType RouteBased `
        -EnableBgp $false `
        -GatewaySku Standard `
        -VpnClientAddressPool $vpnClientAddressPool `
        -VpnClientRootCertificates $p2sRootCert
    ```

    > [!WARNING]
    > Può richiedere alcuni minuti per toocomplete questo processo.

5. Utilizzare hello codice toocreate hello Account di archiviazione di Azure e blob contenitore seguente:

    ```powershell
    # Create hello storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get hello storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create hello default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. Utilizzare hello cluster HDInsight hello toocreate di codice seguente:

    ```powershell
    # Create hello HDInsight cluster
    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $hdiWorkerNodes `
        -ClusterType $hdiType `
        -OSType Linux `
        -Version $hdiVersion `
        -HttpCredential $adminCreds `
        -SshCredential $sshCreds `
        -DefaultStorageAccountName "$storageName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageKey `
        -DefaultStorageContainer $defaultContainerName `
        -VirtualNetworkId $network.Id `
        -SubnetName $defaultSubnet.Id
    ```

  > [!WARNING]
  > Questo processo richiede circa 20 minuti toocomplete.

8. Utilizzare hello cmdlet tooretrieve hello URL per il client VPN di Windows hello per la rete virtuale hello seguente:

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    toodownload hello VPN di Windows client, utilizzare hello restituito URI nel web browser.

### <a name="configure-kafka-for-ip-advertising"></a>Configurare Kafka per la pubblicità IP

Per impostazione predefinita, Zookeeper restituisce il nome di dominio hello di hello Kafka Broker tooclients. Questa configurazione non funziona con hello client software VPN, non può utilizzare la risoluzione dei nomi per le entità nella rete virtuale hello. Per questa configurazione, utilizzare la seguente hello passaggi tooconfigure Kafka tooadvertise indirizzi anziché i nomi di dominio:

1. In un web browser, passare toohttps://CLUSTERNAME.azurehdinsight.net. Sostituire __CLUSTERNAME__ con nome hello di hello Kafka nel cluster HDInsight.

    Quando richiesto, utilizzare nome utente di hello HTTPS e la password per il cluster hello. Hello dell'interfaccia utente Web Ambari per cluster hello viene visualizzato.

2. Selezionare tooview informazioni Kafka, __Kafka__ elenco hello hello sinistra.

    ![Elenco di servizio con Kafka evidenziato](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. Selezionare la configurazione, Kafka tooview __configurazioni__ dall'alto al centro hello.

    ![Collegamenti Configs (Configurazioni) per Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. hello toofind __kafka env__ configurazione, immettere `kafka-env` in hello __filtro__ campo in alto a destra hello.

    ![Configurazione Kafka per kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. gli indirizzi IP tooadvertise Kafka tooconfigure, aggiungere i seguenti hello fondo toohello testo hello __kafka-env-template__ campo:

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. interfaccia hello tooconfigure Kafka in ascolto su, immettere `listeners` in hello __filtro__ campo in alto a destra hello.

7. tooconfigure toolisten Kafka su tutte le interfacce di rete, Modifica valore hello hello __listener__ campo troppo`PLAINTEXT://0.0.0.0:9092`.

8. modifiche alla configurazione di hello toosave, utilizzare hello __salvare__ pulsante. Immettere un messaggio di testo che descrive le modifiche di hello. Selezionare __OK__ una volta hello modifiche sono state salvate.

    ![Pulsante per salvare la configurazione](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. tooprevent errori quando si riavvia Kafka, utilizzare hello __azioni servizio__ e selezionare __attivare la modalità di manutenzione__. Selezionare OK toocomplete questa operazione.

    ![Azioni di servizio, con il pulsante di attivazione manutenzione evidenziato](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. toorestart Kafka, utilizzare hello __riavviare__ e selezionare __riavviare tutti interessati__. Confermare il riavvio di hello e quindi utilizzare hello __OK__ pulsante una volta completata l'operazione di hello.

    ![Pulsante di riavvio con Restart all affected (Riavviare tutti gli elementi interessati) evidenziato](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. modalità di manutenzione toodisable, utilizzare hello __azioni servizio__ e selezionare __attivare la modalità manutenzione__. Selezionare **OK** toocomplete questa operazione.

### <a name="connect-toohello-vpn-gateway"></a>Toohello VPN gateway di connessione

gateway VPN di toohello tooconnect da un __client Windows__, utilizzare hello __connettersi tooAzure__ sezione di hello [configurare una connessione Point-to-Site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) documento.

## <a id="python-client"></a> Esempio: client Python

toovalidate connettività tooKafka, utilizzare i seguenti passaggi toocreate hello ed eseguire un produttore di Python e dell'utente:

1. Utilizzare uno dei seguenti hello tooretrieve metodi completamente hello qualificato il nome di dominio (FQDN) e gli indirizzi IP dei nodi cluster Kafka hello hello:

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

    Questo script si presuppone che `$resourceGroupName` nome hello hello Azure del gruppo di risorse che contiene la rete virtuale hello.

    Salvare hello ha restituito informazioni per l'utilizzo in passaggi successivi hello.

2. Hello utilizzare seguente hello tooinstall [kafka python](http://kafka-python.readthedocs.io/) client:

        pip install kafka-python

3. toosend dati tooKafka, hello utilizzare codice Python di seguito:

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    Sostituire hello `'kafka_broker'` voci con indirizzi hello restituito dal passaggio 1 in questa sezione:

    * Se si utilizza un __Software VPN client__, sostituire hello `kafka_broker` voci con indirizzo IP hello i nodi del lavoro.

    * Se dispone di __abilitata la risoluzione dei nomi tramite un server DNS personalizzato__, sostituire hello `kafka_broker` voci con hello FQDN hello di nodi di lavoro.

    > [!NOTE]
    > Questo codice invia la stringa hello `test message` toohello argomento `testtopic`. configurazione predefinita di Hello di Kafka in HDInsight è argomento hello toocreate se non esiste.

4. messaggi hello tooretrieve da Kafka, utilizzare hello codice Python di seguito:

   ```python
   from kafka import KafkaConsumer
   # Replace hello `ip_address` entries with hello IP address of your worker nodes
   # Again, you only need one or two, not hello full list.
   # Note: auto_offset_reset='earliest' resets hello starting offset toohello beginning
   #       of hello topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    Sostituire hello `'kafka_broker'` voci con indirizzi hello restituito dal passaggio 1 in questa sezione:

    * Se si utilizza un __Software VPN client__, sostituire hello `kafka_broker` voci con indirizzo IP hello i nodi del lavoro.

    * Se dispone di __abilitata la risoluzione dei nomi tramite un server DNS personalizzato__, sostituire hello `kafka_broker` voci con hello FQDN hello di nodi di lavoro.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sull'uso di HDInsight con una rete virtuale, vedere hello [estendere Azure HDInsight tramite una rete virtuale di Azure](hdinsight-extend-hadoop-virtual-network.md) documento.

Per ulteriori informazioni sulla creazione di una rete virtuale di Azure con gateway VPN Point-to-Site, vedere hello seguenti documenti:

* [Configurare una connessione Point-to-Site utilizzando hello portale di Azure](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [Configurare una connessione da punto a sito a una rete virtuale usando Azure PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

Per ulteriori informazioni sull'utilizzo di Kafka in HDInsight, vedere hello seguenti documenti:

* [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) (Introduzione a Kafka in HDInsight)
* [Usare il mirroring con Kafka in HDInsight](hdinsight-apache-kafka-mirroring.md)

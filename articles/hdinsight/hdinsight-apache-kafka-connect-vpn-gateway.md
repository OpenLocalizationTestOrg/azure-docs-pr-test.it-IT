---
title: Connettersi a Kafka tramite le reti virtuali - Azure HDInsight | Microsoft Docs
description: Informazioni su come connettersi direttamente a Kafka in HDInsight tramite una rete virtuale di Azure. Informazioni su come connettersi a Kafka dai client di sviluppo tramite un gateway VPN o dai client nella rete locale tramite un dispositivo gateway VPN.
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
ms.openlocfilehash: 245bee7c1dbb0236afdc2506e7ab84b5573cbc85
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-kafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="8b735-104">Connettersi a Kafka in HDInsight (anteprima) tramite una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="8b735-104">Connect to Kafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="8b735-105">Informazioni su come connettersi direttamente a Kafka in HDInsight tramite le reti virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b735-105">Learn how to directly connect to Kafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="8b735-106">Questo documento contiene informazioni sulla connessione a Kafka con le configurazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b735-106">This document provides information on connecting to Kafka using the following configurations:</span></span>

* <span data-ttu-id="8b735-107">Dalle risorse in una rete locale.</span><span class="sxs-lookup"><span data-stu-id="8b735-107">From resources in an on-premises network.</span></span> <span data-ttu-id="8b735-108">La connessione viene stabilita tramite un dispositivo VPN, un software o un hardware, nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="8b735-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="8b735-109">Da un ambiente di sviluppo tramite un client software VPN.</span><span class="sxs-lookup"><span data-stu-id="8b735-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="8b735-110">Architettura e pianificazione</span><span class="sxs-lookup"><span data-stu-id="8b735-110">Architecture and planning</span></span>

<span data-ttu-id="8b735-111">HDInsight non consente la connessione diretta a Kafka nella rete Internet pubblica.</span><span class="sxs-lookup"><span data-stu-id="8b735-111">HDInsight does not allow direct connection to Kafka over the public internet.</span></span> <span data-ttu-id="8b735-112">I client di Kafka, produttori e clienti, invece, devono usare uno dei seguenti metodi di connessione:</span><span class="sxs-lookup"><span data-stu-id="8b735-112">Instead, Kafka clients (producers and consumers) must use one of the following connection methods:</span></span>

* <span data-ttu-id="8b735-113">Eseguire il client nella stessa rete virtuale di Kafka in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8b735-113">Run the client in the same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="8b735-114">Questa configurazione viene usata nel documento [Iniziare a usare Apache Kafka (anteprima) in HDInsight](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8b735-114">This configuration is used in the [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="8b735-115">Il client viene eseguito direttamente nei nodi del cluster di HDInsight o in un'altra macchina virtuale nella stessa rete.</span><span class="sxs-lookup"><span data-stu-id="8b735-115">The client runs directly on the HDInsight cluster nodes or on another virtual machine in the same network.</span></span>

* <span data-ttu-id="8b735-116">Collegare una rete privata, ad esempio la rete locale, alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="8b735-116">Connect a private network, such as your on-premises network, to the virtual network.</span></span> <span data-ttu-id="8b735-117">Questa configurazione consente ai client nella rete locale per lavorare direttamente con Kafka.</span><span class="sxs-lookup"><span data-stu-id="8b735-117">This configuration allows clients in your on-premises network to directly work with Kafka.</span></span> <span data-ttu-id="8b735-118">Per abilitare questa configurazione, eseguire le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b735-118">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="8b735-119">Creare una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="8b735-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="8b735-120">Creare un gateway VPN che usi una configurazione da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="8b735-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="8b735-121">La configurazione usata in questo documento si connette a un dispositivo gateway VPN nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="8b735-121">The configuration used in this document connects to a VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="8b735-122">Creare un server DNS nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="8b735-122">Create a DNS server in the virtual network.</span></span>
    4. <span data-ttu-id="8b735-123">Configurare l'inoltro tra il server DNS in ogni rete.</span><span class="sxs-lookup"><span data-stu-id="8b735-123">Configure forwarding between the DNS server in each network.</span></span>
    5. <span data-ttu-id="8b735-124">Installare Kafka in HDInsight nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="8b735-124">Install Kafka on HDInsight into the virtual network.</span></span>

    <span data-ttu-id="8b735-125">Per altre informazioni, vedere la sezione [Connetti a Kafka da una rete locale](#on-premises).</span><span class="sxs-lookup"><span data-stu-id="8b735-125">For more information, see the [Connect to Kafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="8b735-126">Connettere i computer individualmente alla rete virtuale usando un gateway VPN e il client VPN.</span><span class="sxs-lookup"><span data-stu-id="8b735-126">Connect individual machines to the virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="8b735-127">Per abilitare questa configurazione, eseguire le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b735-127">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="8b735-128">Creare una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="8b735-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="8b735-129">Creare un gateway VPN che usi una configurazione da punto a sito.</span><span class="sxs-lookup"><span data-stu-id="8b735-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="8b735-130">Questa configurazione offre un client VPN che può essere installato nei client Windows.</span><span class="sxs-lookup"><span data-stu-id="8b735-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="8b735-131">Installare Kafka in HDInsight nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="8b735-131">Install Kafka on HDInsight into the virtual network.</span></span>
    4. <span data-ttu-id="8b735-132">Configurare Kafka per la pubblicità IP.</span><span class="sxs-lookup"><span data-stu-id="8b735-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="8b735-133">Questa configurazione consente al client di connettersi usando gli indirizzi IP anziché i nomi di dominio.</span><span class="sxs-lookup"><span data-stu-id="8b735-133">This configuration allows the client to connect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="8b735-134">Scaricare e usare il client VPN nel sistema di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="8b735-134">Download and use the VPN client on the development system.</span></span>

    <span data-ttu-id="8b735-135">Per altre informazioni, vedere la sezione [Connettersi a Kafka con un client VPN](#vpnclient).</span><span class="sxs-lookup"><span data-stu-id="8b735-135">For more information, see the [Connect to Kafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="8b735-136">Questa configurazione è consigliata solo per scopi di sviluppo a causa delle limitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b735-136">This configuration is only recommended for development purposes because of the following limitations:</span></span>
    >
    > * <span data-ttu-id="8b735-137">Ogni client deve connettersi usando un client software VPN.</span><span class="sxs-lookup"><span data-stu-id="8b735-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="8b735-138">Azure offre solo un client basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="8b735-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="8b735-139">Il client non passare le richieste di risoluzione dei nomi alla rete virtuale, quindi è necessario usare gli indirizzi IP per comunicare con Kafka.</span><span class="sxs-lookup"><span data-stu-id="8b735-139">The client does not pass name resolution requests to the virtual network, so you must use IP addressing to communicate with Kafka.</span></span> <span data-ttu-id="8b735-140">La comunicazione tramite IP richiede una configurazione aggiuntiva nel cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="8b735-140">IP communication requires additional configuration on the Kafka cluster.</span></span>

<span data-ttu-id="8b735-141">Per altre informazioni sull'uso di HDInsight in una rete virtuale, vedere [Estendere le funzionalità di HDInsight usando Rete virtuale di Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="8b735-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="8b735-142"><a id="on-premises"></a> Connettersi a Kafka da una rete locale</span><span class="sxs-lookup"><span data-stu-id="8b735-142"><a id="on-premises"></a> Connect to Kafka from an on-premises network</span></span>

<span data-ttu-id="8b735-143">Per creare un cluster Kafka che comunichi con la rete locale, seguire i passaggi descritti nel documento [Connect HDInsight to your on-premises network](./connect-on-premises-network.md) (Connettere HDInsight alla rete locale).</span><span class="sxs-lookup"><span data-stu-id="8b735-143">To create a Kafka cluster that communicates with your on-premises network, follow the steps in the [Connect HDInsight to your on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b735-144">Quando si crea il cluster HDInsight, selezionare il tipo di cluster __Kafka__.</span><span class="sxs-lookup"><span data-stu-id="8b735-144">When creating the HDInsight cluster, select the __Kafka__ cluster type.</span></span>

<span data-ttu-id="8b735-145">Questi passaggi creano la configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="8b735-145">These steps create the following configuration:</span></span>

* <span data-ttu-id="8b735-146">Rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="8b735-146">Azure Virtual Network</span></span>
* <span data-ttu-id="8b735-147">Gateway VPN da sito a sito</span><span class="sxs-lookup"><span data-stu-id="8b735-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="8b735-148">Account di archiviazione di Azure, usato da HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b735-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="8b735-149">Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b735-149">Kafka on HDInsight</span></span>

<span data-ttu-id="8b735-150">Per verificare che un client Kafka riesce a connettersi al cluster da locale, usare la procedura descritta nella sezione [Esempio: client Python](#python-client).</span><span class="sxs-lookup"><span data-stu-id="8b735-150">To verify that a Kafka client can connect to the cluster from on-premises, use the steps in the [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="8b735-151"><a id="vpnclient"></a> Connettersi a Kafka con un client VPN</span><span class="sxs-lookup"><span data-stu-id="8b735-151"><a id="vpnclient"></a> Connect to Kafka with a VPN client</span></span>

<span data-ttu-id="8b735-152">Usare la procedura descritta in questa sezione per creare la configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="8b735-152">Use the steps in this section to create the following configuration:</span></span>

* <span data-ttu-id="8b735-153">Rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="8b735-153">Azure Virtual Network</span></span>
* <span data-ttu-id="8b735-154">Gateway VPN da punto a sito</span><span class="sxs-lookup"><span data-stu-id="8b735-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="8b735-155">Account di archiviazione di Azure, usato da HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b735-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="8b735-156">Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b735-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="8b735-157">Seguire la procedura nel documento [Usare i certificati autofirmati per le connessioni da punto a sito](../vpn-gateway/vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="8b735-157">Follow the steps in the [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="8b735-158">Questo documento consente di creare i certificati necessari per il gateway.</span><span class="sxs-lookup"><span data-stu-id="8b735-158">This document creates the certificates needed for the gateway.</span></span>

2. <span data-ttu-id="8b735-159">Aprire un prompt di PowerShell e usare il codice seguente per accedere alla sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="8b735-159">Open a PowerShell prompt and use the following code to log in to your Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment to set the subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="8b735-160">Usare il codice seguente per creare le variabili che contengono le informazioni di configurazione:</span><span class="sxs-lookup"><span data-stu-id="8b735-160">Use the following code to create variables that contain configuration information:</span></span>

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is the resource group name?"
    $baseName = Read-Host "What is the base name? It is used to create names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want to create the resources in?"
    $rootCert = Read-Host "What is the file path to the root certificate? It is used to secure the VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter the HTTPS user name and password for the HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter the SSH user name and password for the HDInsight cluster" -UserName "sshuser"

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

4. <span data-ttu-id="8b735-161">Usare il codice seguente per creare il gruppo di risorse di Azure e la rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="8b735-161">Use the following code to create the Azure resource group and virtual network:</span></span>

    ```powershell
    # Create the resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create the subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create the subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get the network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for the gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get the certificate info
    # Get the full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create the VPN gateway
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
    > <span data-ttu-id="8b735-162">Il completamento del processo richiede qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="8b735-162">It can take several minutes for this process to complete.</span></span>

5. <span data-ttu-id="8b735-163">Per creare un contenitore BLOB e l'account di archiviazione di Azure, usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="8b735-163">Use the following code to create the Azure Storage Account and blob container:</span></span>

    ```powershell
    # Create the storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get the storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create the default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. <span data-ttu-id="8b735-164">Per creare il cluster HDInsight usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="8b735-164">Use the following code to create the HDInsight cluster:</span></span>

    ```powershell
    # Create the HDInsight cluster
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
  > <span data-ttu-id="8b735-165">Il completamento di questa procedura richiede circa 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="8b735-165">This process takes around 20 minutes to complete.</span></span>

8. <span data-ttu-id="8b735-166">Usare il cmdlet seguente per recuperare l'URL per il client VPN di Windows per la rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="8b735-166">Use the following cmdlet to retrieve the URL for the Windows VPN client for the virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="8b735-167">Per scaricare il client VPN di Windows, usare l'URI restituito nel Web browser.</span><span class="sxs-lookup"><span data-stu-id="8b735-167">To download the Windows VPN client, use the returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="8b735-168">Configurare Kafka per la pubblicità IP</span><span class="sxs-lookup"><span data-stu-id="8b735-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="8b735-169">Per impostazione predefinita, Zookeeper restituisce il nome di dominio dei broker di Kafka ai client.</span><span class="sxs-lookup"><span data-stu-id="8b735-169">By default, Zookeeper returns the domain name of the Kafka brokers to clients.</span></span> <span data-ttu-id="8b735-170">Questa configurazione non funziona con il client software VPN, poiché non può usare la risoluzione dei nomi per le entità nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="8b735-170">This configuration does not work with the VPN software client, as it cannot use name resolution for entities in the virtual network.</span></span> <span data-ttu-id="8b735-171">Per questa configurazione usare la procedura seguente per configurare Kafka in HDInsight affinché possa creare pubblicità per gli indirizzi IP anziché per i nomi di dominio:</span><span class="sxs-lookup"><span data-stu-id="8b735-171">For this configuration, use the following steps to configure Kafka to advertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="8b735-172">Tramite il Web browser, aprire https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="8b735-172">Using a web browser, go to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="8b735-173">Sostituire __CLUSTERNAME__ con il nome di Kafka nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8b735-173">Replace __CLUSTERNAME__ with the name of the Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="8b735-174">Quando richiesto, usare il nome utente HTTPS e la password per il cluster.</span><span class="sxs-lookup"><span data-stu-id="8b735-174">When prompted, use the HTTPS user name and password for the cluster.</span></span> <span data-ttu-id="8b735-175">Viene visualizzata l'interfaccia utente di Ambari Web per il cluster.</span><span class="sxs-lookup"><span data-stu-id="8b735-175">The Ambari Web UI for the cluster is displayed.</span></span>

2. <span data-ttu-id="8b735-176">Per visualizzare le informazioni su Kafka, selezionare __Kafka__ dall'elenco a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8b735-176">To view information on Kafka, select __Kafka__ from the list on the left.</span></span>

    ![Elenco di servizio con Kafka evidenziato](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="8b735-178">Per visualizzare la configurazione di Kafka, selezionare __Configs__ (Configurazioni) nella parte centrale in alto.</span><span class="sxs-lookup"><span data-stu-id="8b735-178">To view Kafka configuration, select __Configs__ from the top middle.</span></span>

    ![Collegamenti Configs (Configurazioni) per Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="8b735-180">Per trovare la configurazione __kafka-env__, immettere `kafka-env` nel campo __Filtro__ in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="8b735-180">To find the __kafka-env__ configuration, enter `kafka-env` in the __Filter__ field on the upper right.</span></span>

    ![Configurazione Kafka per kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="8b735-182">Per configurare Kafka affinché generi pubblicità per gli indirizzi IP, aggiungere il testo seguente nella parte inferiore del campo __kafka-env-template__:</span><span class="sxs-lookup"><span data-stu-id="8b735-182">To configure Kafka to advertise IP addresses, add the following text to the bottom of the __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka to advertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="8b735-183">Per configurare l'interfaccia per cui è in ascolto Kafka immettere `listeners` nel campo __Filtro__ in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="8b735-183">To configure the interface that Kafka listens on, enter `listeners` in the __Filter__ field on the upper right.</span></span>

7. <span data-ttu-id="8b735-184">Per configurare tutte le interfacce di rete per cui Kafka è in ascolto, modificare il valore nel campo __Listener__ su `PLAINTEXT://0.0.0.0:9092`.</span><span class="sxs-lookup"><span data-stu-id="8b735-184">To configure Kafka to listen on all network interfaces, change the value in the __listeners__ field to `PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="8b735-185">Per salvare le modifiche alla configurazione usare il pulsante __Salva__.</span><span class="sxs-lookup"><span data-stu-id="8b735-185">To save the configuration changes, use the __Save__ button.</span></span> <span data-ttu-id="8b735-186">Immettere un messaggio di testo che descrive le modifiche.</span><span class="sxs-lookup"><span data-stu-id="8b735-186">Enter a text message describing the changes.</span></span> <span data-ttu-id="8b735-187">Selezionare __OK__ dopo aver salvato le modifiche.</span><span class="sxs-lookup"><span data-stu-id="8b735-187">Select __OK__ once the changes have been saved.</span></span>

    ![Pulsante per salvare la configurazione](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="8b735-189">Per evitare errori al riavvio di Kafka, usare il pulsante __Service Actions__ (Azioni del servizio) e selezionare __Attiva modalità di manutenzione__.</span><span class="sxs-lookup"><span data-stu-id="8b735-189">To prevent errors when restarting Kafka, use the __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="8b735-190">Per completare questa operazione selezionare OK.</span><span class="sxs-lookup"><span data-stu-id="8b735-190">Select OK to complete this operation.</span></span>

    ![Azioni di servizio, con il pulsante di attivazione manutenzione evidenziato](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="8b735-192">Per riavviare Kafka, utilizzare il pulsante __Riavvia__ e selezionare __Restart All Affected__ (Riavviare tutti gli elementi interessati).</span><span class="sxs-lookup"><span data-stu-id="8b735-192">To restart Kafka, use the __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="8b735-193">Confermare il riavvio, quindi usare il pulsante __OK__ dopo aver completato l'operazione.</span><span class="sxs-lookup"><span data-stu-id="8b735-193">Confirm the restart, and then use the __OK__ button after the operation has completed.</span></span>

    ![Pulsante di riavvio con Restart all affected (Riavviare tutti gli elementi interessati) evidenziato](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="8b735-195">Per disabilitare la modalità di manutenzione, usare il pulsante __Service Actions__ (Azioni del servizio) e selezionare __Disattiva modalità di manutenzione__.</span><span class="sxs-lookup"><span data-stu-id="8b735-195">To disable maintenance mode, use the __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="8b735-196">Per completare questa operazione selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="8b735-196">Select **OK** to complete this operation.</span></span>

### <a name="connect-to-the-vpn-gateway"></a><span data-ttu-id="8b735-197">Connettersi al gateway VPN</span><span class="sxs-lookup"><span data-stu-id="8b735-197">Connect to the VPN gateway</span></span>

<span data-ttu-id="8b735-198">Per connettersi al gateway VPN da un __client Windows__, usare la sezione __Connettersi ad Azure__ del documento [Configurare una connessione da punto a sito](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate).</span><span class="sxs-lookup"><span data-stu-id="8b735-198">To connect to the VPN gateway from a __Windows client__, use the __Connect to Azure__ section of the [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="8b735-199"><a id="python-client"></a> Esempio: client Python</span><span class="sxs-lookup"><span data-stu-id="8b735-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="8b735-200">Per convalidare la connettività a Kafka, usare la procedura seguente per creare ed eseguire un produttore e un utente di Python:</span><span class="sxs-lookup"><span data-stu-id="8b735-200">To validate connectivity to Kafka, use the following steps to create and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="8b735-201">Per recuperare il nome di dominio completo e gli indirizzi IP dei nodi nel cluster Kafka, usare uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b735-201">Use one of the following methods to retrieve the fully qualified domain name (FQDN) and IP addresses of the nodes in the Kafka cluster:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

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

    <span data-ttu-id="8b735-202">Questo script presuppone che `$resourceGroupName` sia il nome del gruppo di risorse di Azure che contiene la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="8b735-202">This script assumes that `$resourceGroupName` is the name of the Azure resource group that contains the virtual network.</span></span>

    <span data-ttu-id="8b735-203">Salvare le informazioni restituite da usare nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="8b735-203">Save the returned information for use in the next steps.</span></span>

2. <span data-ttu-id="8b735-204">Per installare il client [kafka-python](http://kafka-python.readthedocs.io/) usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="8b735-204">Use the following to install the [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="8b735-205">Per inviare dati a Kafka, usare il seguente codice Python:</span><span class="sxs-lookup"><span data-stu-id="8b735-205">To send data to Kafka, use the following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace the `ip_address` entries with the IP address of your worker nodes
  # NOTE: you don't need the full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="8b735-206">Sostituire le voci `'kafka_broker'` con gli indirizzi restituiti dal passaggio 1 in questa sezione:</span><span class="sxs-lookup"><span data-stu-id="8b735-206">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="8b735-207">Se si usa un __client VPN del software__, sostituire le voci `kafka_broker` con l'indirizzo IP dei nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8b735-207">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="8b735-208">Se è __abilitata la risoluzione dei nomi tramite un server DNS personalizzato__, sostituire le voci `kafka_broker` con il nome di dominio completo dei nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8b735-208">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8b735-209">Questo codice invia la stringa `test message` all'argomento `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="8b735-209">This code sends the string `test message` to the topic `testtopic`.</span></span> <span data-ttu-id="8b735-210">La configurazione predefinita di Kafka in HDInsight consiste nel creare l'argomento se non esiste.</span><span class="sxs-lookup"><span data-stu-id="8b735-210">The default configuration of Kafka on HDInsight is to create the topic if it does not exist.</span></span>

4. <span data-ttu-id="8b735-211">Per recuperare i messaggi da Kafka, usare il seguente codice Python:</span><span class="sxs-lookup"><span data-stu-id="8b735-211">To retrieve the messages from Kafka, use the following Python code:</span></span>

   ```python
   from kafka import KafkaConsumer
   # Replace the `ip_address` entries with the IP address of your worker nodes
   # Again, you only need one or two, not the full list.
   # Note: auto_offset_reset='earliest' resets the starting offset to the beginning
   #       of the topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    <span data-ttu-id="8b735-212">Sostituire le voci `'kafka_broker'` con gli indirizzi restituiti dal passaggio 1 in questa sezione:</span><span class="sxs-lookup"><span data-stu-id="8b735-212">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="8b735-213">Se si usa un __client VPN del software__, sostituire le voci `kafka_broker` con l'indirizzo IP dei nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8b735-213">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="8b735-214">Se è __abilitata la risoluzione dei nomi tramite un server DNS personalizzato__, sostituire le voci `kafka_broker` con il nome di dominio completo dei nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8b735-214">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b735-215">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8b735-215">Next steps</span></span>

<span data-ttu-id="8b735-216">Per altre informazioni sull'uso di HDInsight con le reti virtuali, vedere il documento [Estendere le funzionalità di HDInsight usando Rete virtuale di Azure](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="8b735-216">For more information on using HDInsight with a virtual network, see the [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="8b735-217">Per altre informazioni sulla creazione di una rete virtuale di Azure con gateway VPN da punto a sito, vedere i seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="8b735-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see the following documents:</span></span>

* [<span data-ttu-id="8b735-218">Configurare una connessione da punto a sito a una rete virtuale usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8b735-218">Configure a Point-to-Site connection using the Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="8b735-219">Configurare una connessione da punto a sito a una rete virtuale usando Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b735-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="8b735-220">Per altre informazioni sull'uso della gestione di Kafka in HDInsight, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b735-220">For more information on working with Kafka on HDInsight, see the following documents:</span></span>

* <span data-ttu-id="8b735-221">[Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) (Introduzione a Kafka in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="8b735-221">[Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md)</span></span>
* [<span data-ttu-id="8b735-222">Usare il mirroring con Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b735-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)

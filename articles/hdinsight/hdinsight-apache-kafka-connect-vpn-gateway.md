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
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="9e68e-104">Connettersi tooKafka in HDInsight (anteprima) tramite una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="9e68e-104">Connect tooKafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="9e68e-105">Informazioni su come toodirectly connettersi tooKafka in HDInsight con reti virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="9e68e-105">Learn how toodirectly connect tooKafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="9e68e-106">Questo documento vengono fornite informazioni sulla connessione tooKafka utilizzando hello seguenti configurazioni:</span><span class="sxs-lookup"><span data-stu-id="9e68e-106">This document provides information on connecting tooKafka using hello following configurations:</span></span>

* <span data-ttu-id="9e68e-107">Dalle risorse in una rete locale.</span><span class="sxs-lookup"><span data-stu-id="9e68e-107">From resources in an on-premises network.</span></span> <span data-ttu-id="9e68e-108">La connessione viene stabilita tramite un dispositivo VPN, un software o un hardware, nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="9e68e-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="9e68e-109">Da un ambiente di sviluppo tramite un client software VPN.</span><span class="sxs-lookup"><span data-stu-id="9e68e-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="9e68e-110">Architettura e pianificazione</span><span class="sxs-lookup"><span data-stu-id="9e68e-110">Architecture and planning</span></span>

<span data-ttu-id="9e68e-111">HDInsight non consente la connessione diretta tooKafka su hello rete internet pubblica.</span><span class="sxs-lookup"><span data-stu-id="9e68e-111">HDInsight does not allow direct connection tooKafka over hello public internet.</span></span> <span data-ttu-id="9e68e-112">Invece necessario utilizzare uno dei seguenti metodi di connessione hello client Kafka (producer e consumer):</span><span class="sxs-lookup"><span data-stu-id="9e68e-112">Instead, Kafka clients (producers and consumers) must use one of hello following connection methods:</span></span>

* <span data-ttu-id="9e68e-113">Eseguire il client di hello in hello stessa rete virtuale Kafka in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9e68e-113">Run hello client in hello same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="9e68e-114">Questa configurazione viene utilizzata in hello [iniziano con Apache Kafka (anteprima) in HDInsight](hdinsight-apache-kafka-get-started.md) documento.</span><span class="sxs-lookup"><span data-stu-id="9e68e-114">This configuration is used in hello [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="9e68e-115">i nodi del cluster su hello HDInsight Hello client esegue direttamente o in un'altra macchina virtuale di hello stesso rete.</span><span class="sxs-lookup"><span data-stu-id="9e68e-115">hello client runs directly on hello HDInsight cluster nodes or on another virtual machine in hello same network.</span></span>

* <span data-ttu-id="9e68e-116">Connettere una rete privata, ad esempio la rete locale, la rete virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="9e68e-116">Connect a private network, such as your on-premises network, toohello virtual network.</span></span> <span data-ttu-id="9e68e-117">Questa configurazione consente ai client il lavoro toodirectly di rete locale con Kafka.</span><span class="sxs-lookup"><span data-stu-id="9e68e-117">This configuration allows clients in your on-premises network toodirectly work with Kafka.</span></span> <span data-ttu-id="9e68e-118">tooenable questa configurazione, eseguire hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="9e68e-118">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="9e68e-119">Creare una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9e68e-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="9e68e-120">Creare un gateway VPN che usi una configurazione da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="9e68e-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="9e68e-121">configurazione di Hello utilizzata in questo documento si connette dispositivo gateway VPN di tooa nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="9e68e-121">hello configuration used in this document connects tooa VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="9e68e-122">Creare un server DNS nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="9e68e-122">Create a DNS server in hello virtual network.</span></span>
    4. <span data-ttu-id="9e68e-123">Configurare l'inoltro tra i server DNS hello in ogni rete.</span><span class="sxs-lookup"><span data-stu-id="9e68e-123">Configure forwarding between hello DNS server in each network.</span></span>
    5. <span data-ttu-id="9e68e-124">Installare Kafka in HDInsight in rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="9e68e-124">Install Kafka on HDInsight into hello virtual network.</span></span>

    <span data-ttu-id="9e68e-125">Per ulteriori informazioni, vedere hello [connettersi tooKafka da una rete locale](#on-premises) sezione.</span><span class="sxs-lookup"><span data-stu-id="9e68e-125">For more information, see hello [Connect tooKafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="9e68e-126">Connettere la rete virtuale toohello singoli computer tramite un gateway VPN e il client VPN.</span><span class="sxs-lookup"><span data-stu-id="9e68e-126">Connect individual machines toohello virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="9e68e-127">tooenable questa configurazione, eseguire hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="9e68e-127">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="9e68e-128">Creare una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9e68e-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="9e68e-129">Creare un gateway VPN che usi una configurazione da punto a sito.</span><span class="sxs-lookup"><span data-stu-id="9e68e-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="9e68e-130">Questa configurazione offre un client VPN che può essere installato nei client Windows.</span><span class="sxs-lookup"><span data-stu-id="9e68e-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="9e68e-131">Installare Kafka in HDInsight in rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="9e68e-131">Install Kafka on HDInsight into hello virtual network.</span></span>
    4. <span data-ttu-id="9e68e-132">Configurare Kafka per la pubblicità IP.</span><span class="sxs-lookup"><span data-stu-id="9e68e-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="9e68e-133">Questa configurazione consente hello client tooconnect con IP addressing anziché i nomi di dominio.</span><span class="sxs-lookup"><span data-stu-id="9e68e-133">This configuration allows hello client tooconnect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="9e68e-134">Scaricare e usare i client VPN hello nel sistema di sviluppo hello.</span><span class="sxs-lookup"><span data-stu-id="9e68e-134">Download and use hello VPN client on hello development system.</span></span>

    <span data-ttu-id="9e68e-135">Per ulteriori informazioni, vedere hello [tooKafka si connettono con un client VPN](#vpnclient) sezione.</span><span class="sxs-lookup"><span data-stu-id="9e68e-135">For more information, see hello [Connect tooKafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="9e68e-136">Questa configurazione è consigliata solo per scopi di sviluppo a causa di hello limitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9e68e-136">This configuration is only recommended for development purposes because of hello following limitations:</span></span>
    >
    > * <span data-ttu-id="9e68e-137">Ogni client deve connettersi usando un client software VPN.</span><span class="sxs-lookup"><span data-stu-id="9e68e-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="9e68e-138">Azure offre solo un client basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="9e68e-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="9e68e-139">client Hello non passa nome risoluzione richieste toohello rete virtuale, è necessario utilizzare indirizzi toocommunicate con Kafka IP.</span><span class="sxs-lookup"><span data-stu-id="9e68e-139">hello client does not pass name resolution requests toohello virtual network, so you must use IP addressing toocommunicate with Kafka.</span></span> <span data-ttu-id="9e68e-140">Comunicazione con gli IP richiede ulteriori configurazioni in cluster Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="9e68e-140">IP communication requires additional configuration on hello Kafka cluster.</span></span>

<span data-ttu-id="9e68e-141">Per altre informazioni sull'uso di HDInsight in una rete virtuale, vedere [Estendere le funzionalità di HDInsight usando Rete virtuale di Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="9e68e-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="9e68e-142"><a id="on-premises"></a>Connettersi tooKafka da una rete locale</span><span class="sxs-lookup"><span data-stu-id="9e68e-142"><a id="on-premises"></a> Connect tooKafka from an on-premises network</span></span>

<span data-ttu-id="9e68e-143">toocreate un cluster Kafka che comunica con la rete locale, seguire i passaggi hello hello [rete locale di connettersi a HDInsight tooyour](./connect-on-premises-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="9e68e-143">toocreate a Kafka cluster that communicates with your on-premises network, follow hello steps in hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9e68e-144">Quando si crea il cluster di HDInsight hello, selezionare hello __Kafka__ del cluster di tipo.</span><span class="sxs-lookup"><span data-stu-id="9e68e-144">When creating hello HDInsight cluster, select hello __Kafka__ cluster type.</span></span>

<span data-ttu-id="9e68e-145">Questi passaggi creano hello seguente configurazione:</span><span class="sxs-lookup"><span data-stu-id="9e68e-145">These steps create hello following configuration:</span></span>

* <span data-ttu-id="9e68e-146">Rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="9e68e-146">Azure Virtual Network</span></span>
* <span data-ttu-id="9e68e-147">Gateway VPN da sito a sito</span><span class="sxs-lookup"><span data-stu-id="9e68e-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="9e68e-148">Account di archiviazione di Azure, usato da HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e68e-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="9e68e-149">Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e68e-149">Kafka on HDInsight</span></span>

<span data-ttu-id="9e68e-150">tooverify che un client di Kafka può connettersi toohello cluster locale, utilizzare i passaggi di hello in hello [esempio: client Python](#python-client) sezione.</span><span class="sxs-lookup"><span data-stu-id="9e68e-150">tooverify that a Kafka client can connect toohello cluster from on-premises, use hello steps in hello [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="9e68e-151"><a id="vpnclient"></a>Connettersi tooKafka con un client VPN</span><span class="sxs-lookup"><span data-stu-id="9e68e-151"><a id="vpnclient"></a> Connect tooKafka with a VPN client</span></span>

<span data-ttu-id="9e68e-152">Usare i passaggi di hello in questo hello toocreate sezione seguente configurazione:</span><span class="sxs-lookup"><span data-stu-id="9e68e-152">Use hello steps in this section toocreate hello following configuration:</span></span>

* <span data-ttu-id="9e68e-153">Rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="9e68e-153">Azure Virtual Network</span></span>
* <span data-ttu-id="9e68e-154">Gateway VPN da punto a sito</span><span class="sxs-lookup"><span data-stu-id="9e68e-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="9e68e-155">Account di archiviazione di Azure, usato da HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e68e-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="9e68e-156">Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e68e-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="9e68e-157">Seguire i passaggi hello hello [utilizzano certificati autofirmati per le connessioni Point-to-site](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) documento.</span><span class="sxs-lookup"><span data-stu-id="9e68e-157">Follow hello steps in hello [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="9e68e-158">Questo documento consente di creare certificati hello necessari per il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="9e68e-158">This document creates hello certificates needed for hello gateway.</span></span>

2. <span data-ttu-id="9e68e-159">Aprire un prompt dei comandi di PowerShell e usare hello seguente codice toolog in tooyour sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="9e68e-159">Open a PowerShell prompt and use hello following code toolog in tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="9e68e-160">Utilizzare hello variabili toocreate di codice che contengono informazioni di configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="9e68e-160">Use hello following code toocreate variables that contain configuration information:</span></span>

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

4. <span data-ttu-id="9e68e-161">Gruppo di risorse di Azure toocreate hello e rete virtuale di codice seguente hello di utilizzo:</span><span class="sxs-lookup"><span data-stu-id="9e68e-161">Use hello following code toocreate hello Azure resource group and virtual network:</span></span>

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
    > <span data-ttu-id="9e68e-162">Può richiedere alcuni minuti per toocomplete questo processo.</span><span class="sxs-lookup"><span data-stu-id="9e68e-162">It can take several minutes for this process toocomplete.</span></span>

5. <span data-ttu-id="9e68e-163">Utilizzare hello codice toocreate hello Account di archiviazione di Azure e blob contenitore seguente:</span><span class="sxs-lookup"><span data-stu-id="9e68e-163">Use hello following code toocreate hello Azure Storage Account and blob container:</span></span>

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

6. <span data-ttu-id="9e68e-164">Utilizzare hello cluster HDInsight hello toocreate di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="9e68e-164">Use hello following code toocreate hello HDInsight cluster:</span></span>

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
  > <span data-ttu-id="9e68e-165">Questo processo richiede circa 20 minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="9e68e-165">This process takes around 20 minutes toocomplete.</span></span>

8. <span data-ttu-id="9e68e-166">Utilizzare hello cmdlet tooretrieve hello URL per il client VPN di Windows hello per la rete virtuale hello seguente:</span><span class="sxs-lookup"><span data-stu-id="9e68e-166">Use hello following cmdlet tooretrieve hello URL for hello Windows VPN client for hello virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="9e68e-167">toodownload hello VPN di Windows client, utilizzare hello restituito URI nel web browser.</span><span class="sxs-lookup"><span data-stu-id="9e68e-167">toodownload hello Windows VPN client, use hello returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="9e68e-168">Configurare Kafka per la pubblicità IP</span><span class="sxs-lookup"><span data-stu-id="9e68e-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="9e68e-169">Per impostazione predefinita, Zookeeper restituisce il nome di dominio hello di hello Kafka Broker tooclients.</span><span class="sxs-lookup"><span data-stu-id="9e68e-169">By default, Zookeeper returns hello domain name of hello Kafka brokers tooclients.</span></span> <span data-ttu-id="9e68e-170">Questa configurazione non funziona con hello client software VPN, non può utilizzare la risoluzione dei nomi per le entità nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="9e68e-170">This configuration does not work with hello VPN software client, as it cannot use name resolution for entities in hello virtual network.</span></span> <span data-ttu-id="9e68e-171">Per questa configurazione, utilizzare la seguente hello passaggi tooconfigure Kafka tooadvertise indirizzi anziché i nomi di dominio:</span><span class="sxs-lookup"><span data-stu-id="9e68e-171">For this configuration, use hello following steps tooconfigure Kafka tooadvertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="9e68e-172">In un web browser, passare toohttps://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="9e68e-172">Using a web browser, go toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="9e68e-173">Sostituire __CLUSTERNAME__ con nome hello di hello Kafka nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9e68e-173">Replace __CLUSTERNAME__ with hello name of hello Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="9e68e-174">Quando richiesto, utilizzare nome utente di hello HTTPS e la password per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9e68e-174">When prompted, use hello HTTPS user name and password for hello cluster.</span></span> <span data-ttu-id="9e68e-175">Hello dell'interfaccia utente Web Ambari per cluster hello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="9e68e-175">hello Ambari Web UI for hello cluster is displayed.</span></span>

2. <span data-ttu-id="9e68e-176">Selezionare tooview informazioni Kafka, __Kafka__ elenco hello hello sinistra.</span><span class="sxs-lookup"><span data-stu-id="9e68e-176">tooview information on Kafka, select __Kafka__ from hello list on hello left.</span></span>

    ![Elenco di servizio con Kafka evidenziato](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="9e68e-178">Selezionare la configurazione, Kafka tooview __configurazioni__ dall'alto al centro hello.</span><span class="sxs-lookup"><span data-stu-id="9e68e-178">tooview Kafka configuration, select __Configs__ from hello top middle.</span></span>

    ![Collegamenti Configs (Configurazioni) per Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="9e68e-180">hello toofind __kafka env__ configurazione, immettere `kafka-env` in hello __filtro__ campo in alto a destra hello.</span><span class="sxs-lookup"><span data-stu-id="9e68e-180">toofind hello __kafka-env__ configuration, enter `kafka-env` in hello __Filter__ field on hello upper right.</span></span>

    ![Configurazione Kafka per kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="9e68e-182">gli indirizzi IP tooadvertise Kafka tooconfigure, aggiungere i seguenti hello fondo toohello testo hello __kafka-env-template__ campo:</span><span class="sxs-lookup"><span data-stu-id="9e68e-182">tooconfigure Kafka tooadvertise IP addresses, add hello following text toohello bottom of hello __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="9e68e-183">interfaccia hello tooconfigure Kafka in ascolto su, immettere `listeners` in hello __filtro__ campo in alto a destra hello.</span><span class="sxs-lookup"><span data-stu-id="9e68e-183">tooconfigure hello interface that Kafka listens on, enter `listeners` in hello __Filter__ field on hello upper right.</span></span>

7. <span data-ttu-id="9e68e-184">tooconfigure toolisten Kafka su tutte le interfacce di rete, Modifica valore hello hello __listener__ campo troppo`PLAINTEXT://0.0.0.0:9092`.</span><span class="sxs-lookup"><span data-stu-id="9e68e-184">tooconfigure Kafka toolisten on all network interfaces, change hello value in hello __listeners__ field too`PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="9e68e-185">modifiche alla configurazione di hello toosave, utilizzare hello __salvare__ pulsante.</span><span class="sxs-lookup"><span data-stu-id="9e68e-185">toosave hello configuration changes, use hello __Save__ button.</span></span> <span data-ttu-id="9e68e-186">Immettere un messaggio di testo che descrive le modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="9e68e-186">Enter a text message describing hello changes.</span></span> <span data-ttu-id="9e68e-187">Selezionare __OK__ una volta hello modifiche sono state salvate.</span><span class="sxs-lookup"><span data-stu-id="9e68e-187">Select __OK__ once hello changes have been saved.</span></span>

    ![Pulsante per salvare la configurazione](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="9e68e-189">tooprevent errori quando si riavvia Kafka, utilizzare hello __azioni servizio__ e selezionare __attivare la modalità di manutenzione__.</span><span class="sxs-lookup"><span data-stu-id="9e68e-189">tooprevent errors when restarting Kafka, use hello __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="9e68e-190">Selezionare OK toocomplete questa operazione.</span><span class="sxs-lookup"><span data-stu-id="9e68e-190">Select OK toocomplete this operation.</span></span>

    ![Azioni di servizio, con il pulsante di attivazione manutenzione evidenziato](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="9e68e-192">toorestart Kafka, utilizzare hello __riavviare__ e selezionare __riavviare tutti interessati__.</span><span class="sxs-lookup"><span data-stu-id="9e68e-192">toorestart Kafka, use hello __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="9e68e-193">Confermare il riavvio di hello e quindi utilizzare hello __OK__ pulsante una volta completata l'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="9e68e-193">Confirm hello restart, and then use hello __OK__ button after hello operation has completed.</span></span>

    ![Pulsante di riavvio con Restart all affected (Riavviare tutti gli elementi interessati) evidenziato](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="9e68e-195">modalità di manutenzione toodisable, utilizzare hello __azioni servizio__ e selezionare __attivare la modalità manutenzione__.</span><span class="sxs-lookup"><span data-stu-id="9e68e-195">toodisable maintenance mode, use hello __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="9e68e-196">Selezionare **OK** toocomplete questa operazione.</span><span class="sxs-lookup"><span data-stu-id="9e68e-196">Select **OK** toocomplete this operation.</span></span>

### <a name="connect-toohello-vpn-gateway"></a><span data-ttu-id="9e68e-197">Toohello VPN gateway di connessione</span><span class="sxs-lookup"><span data-stu-id="9e68e-197">Connect toohello VPN gateway</span></span>

<span data-ttu-id="9e68e-198">gateway VPN di toohello tooconnect da un __client Windows__, utilizzare hello __connettersi tooAzure__ sezione di hello [configurare una connessione Point-to-Site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) documento.</span><span class="sxs-lookup"><span data-stu-id="9e68e-198">tooconnect toohello VPN gateway from a __Windows client__, use hello __Connect tooAzure__ section of hello [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="9e68e-199"><a id="python-client"></a> Esempio: client Python</span><span class="sxs-lookup"><span data-stu-id="9e68e-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="9e68e-200">toovalidate connettività tooKafka, utilizzare i seguenti passaggi toocreate hello ed eseguire un produttore di Python e dell'utente:</span><span class="sxs-lookup"><span data-stu-id="9e68e-200">toovalidate connectivity tooKafka, use hello following steps toocreate and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="9e68e-201">Utilizzare uno dei seguenti hello tooretrieve metodi completamente hello qualificato il nome di dominio (FQDN) e gli indirizzi IP dei nodi cluster Kafka hello hello:</span><span class="sxs-lookup"><span data-stu-id="9e68e-201">Use one of hello following methods tooretrieve hello fully qualified domain name (FQDN) and IP addresses of hello nodes in hello Kafka cluster:</span></span>

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

    <span data-ttu-id="9e68e-202">Questo script si presuppone che `$resourceGroupName` nome hello hello Azure del gruppo di risorse che contiene la rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="9e68e-202">This script assumes that `$resourceGroupName` is hello name of hello Azure resource group that contains hello virtual network.</span></span>

    <span data-ttu-id="9e68e-203">Salvare hello ha restituito informazioni per l'utilizzo in passaggi successivi hello.</span><span class="sxs-lookup"><span data-stu-id="9e68e-203">Save hello returned information for use in hello next steps.</span></span>

2. <span data-ttu-id="9e68e-204">Hello utilizzare seguente hello tooinstall [kafka python](http://kafka-python.readthedocs.io/) client:</span><span class="sxs-lookup"><span data-stu-id="9e68e-204">Use hello following tooinstall hello [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="9e68e-205">toosend dati tooKafka, hello utilizzare codice Python di seguito:</span><span class="sxs-lookup"><span data-stu-id="9e68e-205">toosend data tooKafka, use hello following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="9e68e-206">Sostituire hello `'kafka_broker'` voci con indirizzi hello restituito dal passaggio 1 in questa sezione:</span><span class="sxs-lookup"><span data-stu-id="9e68e-206">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="9e68e-207">Se si utilizza un __Software VPN client__, sostituire hello `kafka_broker` voci con indirizzo IP hello i nodi del lavoro.</span><span class="sxs-lookup"><span data-stu-id="9e68e-207">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="9e68e-208">Se dispone di __abilitata la risoluzione dei nomi tramite un server DNS personalizzato__, sostituire hello `kafka_broker` voci con hello FQDN hello di nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="9e68e-208">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9e68e-209">Questo codice invia la stringa hello `test message` toohello argomento `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="9e68e-209">This code sends hello string `test message` toohello topic `testtopic`.</span></span> <span data-ttu-id="9e68e-210">configurazione predefinita di Hello di Kafka in HDInsight è argomento hello toocreate se non esiste.</span><span class="sxs-lookup"><span data-stu-id="9e68e-210">hello default configuration of Kafka on HDInsight is toocreate hello topic if it does not exist.</span></span>

4. <span data-ttu-id="9e68e-211">messaggi hello tooretrieve da Kafka, utilizzare hello codice Python di seguito:</span><span class="sxs-lookup"><span data-stu-id="9e68e-211">tooretrieve hello messages from Kafka, use hello following Python code:</span></span>

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

    <span data-ttu-id="9e68e-212">Sostituire hello `'kafka_broker'` voci con indirizzi hello restituito dal passaggio 1 in questa sezione:</span><span class="sxs-lookup"><span data-stu-id="9e68e-212">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="9e68e-213">Se si utilizza un __Software VPN client__, sostituire hello `kafka_broker` voci con indirizzo IP hello i nodi del lavoro.</span><span class="sxs-lookup"><span data-stu-id="9e68e-213">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="9e68e-214">Se dispone di __abilitata la risoluzione dei nomi tramite un server DNS personalizzato__, sostituire hello `kafka_broker` voci con hello FQDN hello di nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="9e68e-214">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e68e-215">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9e68e-215">Next steps</span></span>

<span data-ttu-id="9e68e-216">Per ulteriori informazioni sull'uso di HDInsight con una rete virtuale, vedere hello [estendere Azure HDInsight tramite una rete virtuale di Azure](hdinsight-extend-hadoop-virtual-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="9e68e-216">For more information on using HDInsight with a virtual network, see hello [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="9e68e-217">Per ulteriori informazioni sulla creazione di una rete virtuale di Azure con gateway VPN Point-to-Site, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="9e68e-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see hello following documents:</span></span>

* [<span data-ttu-id="9e68e-218">Configurare una connessione Point-to-Site utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9e68e-218">Configure a Point-to-Site connection using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="9e68e-219">Configurare una connessione da punto a sito a una rete virtuale usando Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e68e-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="9e68e-220">Per ulteriori informazioni sull'utilizzo di Kafka in HDInsight, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="9e68e-220">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* <span data-ttu-id="9e68e-221">[Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) (Introduzione a Kafka in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="9e68e-221">[Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md)</span></span>
* [<span data-ttu-id="9e68e-222">Usare il mirroring con Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e68e-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)

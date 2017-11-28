---
title: "Configurare un listener ILB per gruppi di disponibilità AlwaysOn in Azure | Microsoft Docs"
description: "Questa esercitazione usa risorse create con il modello di distribuzione classica e crea un listener del gruppo di disponibilità AlwaysOn in Azure usando un servizio di bilanciamento del carico interno."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: fea70b389b1f1d6af963e3f14fdc48e8d857dd53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a><span data-ttu-id="e7f33-103">Configurare un listener ILB per gruppi di disponibilità AlwaysOn in Azure</span><span class="sxs-lookup"><span data-stu-id="e7f33-103">Configure an ILB listener for Always On availability groups in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e7f33-104">Listener interno</span><span class="sxs-lookup"><span data-stu-id="e7f33-104">Internal listener</span></span>](../classic/ps-sql-int-listener.md)
> * [<span data-ttu-id="e7f33-105">Listener esterno</span><span class="sxs-lookup"><span data-stu-id="e7f33-105">External listener</span></span>](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a><span data-ttu-id="e7f33-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e7f33-106">Overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7f33-107">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager e classico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e7f33-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e7f33-108">In questo articolo viene illustrato l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="e7f33-108">This article covers the use of the classic deployment model.</span></span> <span data-ttu-id="e7f33-109">Per le distribuzioni più recenti si consiglia di usare il modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e7f33-109">We recommend that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="e7f33-110">Per configurare un listener per un gruppo di disponibilità AlwaysOn nel modello di Resource Manager, vedere [Configurare un servizio di bilanciamento del carico per un gruppo di disponibilità AlwaysOn in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="e7f33-110">To configure a listener for an Always On availability group in the Resource Manager model, see [Configure a load balancer for an Always On availability group in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

<span data-ttu-id="e7f33-111">Il gruppo di disponibilità può contenere repliche solo locali, solo di Azure oppure sia locali che di Azure per le configurazioni ibride.</span><span class="sxs-lookup"><span data-stu-id="e7f33-111">Your availability group can contain replicas that are on-premises only or Azure only, or that span both on-premises and Azure for hybrid configurations.</span></span> <span data-ttu-id="e7f33-112">Le repliche di Azure possono trovarsi nella stessa area o in più aree grazie a più reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="e7f33-112">Azure replicas can reside within the same region or across multiple regions that use multiple virtual networks.</span></span> <span data-ttu-id="e7f33-113">Le procedure riportate in questo articolo presuppongono che sia già stato [configurato un gruppo di disponibilità](../classic/portal-sql-alwayson-availability-groups.md) ma che non sia stato configurato un listener.</span><span class="sxs-lookup"><span data-stu-id="e7f33-113">The procedures in this article assume that you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not yet configured a listener.</span></span>

## <a name="guidelines-and-limitations-for-internal-listeners"></a><span data-ttu-id="e7f33-114">Linee guida e limitazioni per listener interni</span><span class="sxs-lookup"><span data-stu-id="e7f33-114">Guidelines and limitations for internal listeners</span></span>
<span data-ttu-id="e7f33-115">L'uso di un servizio di bilanciamento del carico interno con un listener del gruppo di disponibilità in Azure è soggetto alle seguenti linee guida:</span><span class="sxs-lookup"><span data-stu-id="e7f33-115">The use of an internal load balancer (ILB) with an availability group listener in Azure is subject to the following guidelines:</span></span>

* <span data-ttu-id="e7f33-116">Il listener del gruppo di disponibilità è supportato su Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="e7f33-116">The availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span>
* <span data-ttu-id="e7f33-117">Per ogni servizio cloud è supportato un solo listener del gruppo di disponibilità interno, perché il listener è configurato solo per ILB, e c'è un solo ILB per ogni servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="e7f33-117">Only one internal availability group listener is supported for each cloud service, because the listener is configured to the ILB, and there is only one ILB for each cloud service.</span></span> <span data-ttu-id="e7f33-118">Tuttavia, è possibile creare più listener esterni.</span><span class="sxs-lookup"><span data-stu-id="e7f33-118">However, it is possible to create multiple external listeners.</span></span> <span data-ttu-id="e7f33-119">Per altre informazioni, vedere [Configurare un listener esterno per i gruppi di disponibilità AlwaysOn in Azure](../classic/ps-sql-ext-listener.md).</span><span class="sxs-lookup"><span data-stu-id="e7f33-119">For more information, see [Configure an external listener for Always On availability groups in Azure](../classic/ps-sql-ext-listener.md).</span></span>

## <a name="determine-the-accessibility-of-the-listener"></a><span data-ttu-id="e7f33-120">Determinare l'accessibilità del listener</span><span class="sxs-lookup"><span data-stu-id="e7f33-120">Determine the accessibility of the listener</span></span>
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

<span data-ttu-id="e7f33-121">Questo articolo illustra la creazione di un listener che usa un servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="e7f33-121">This article focuses on creating a listener that uses an ILB.</span></span> <span data-ttu-id="e7f33-122">Se è necessario un listener pubblico/esterno, vedere la versione di questo articolo che tratta la procedura per la configurazione di un [listener esterno](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e7f33-122">If you need an public or external listener, see the version of this article that discusses setting up an [external listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a><span data-ttu-id="e7f33-123">Creare endpoint VM con bilanciamento del carico con Direct Server Return</span><span class="sxs-lookup"><span data-stu-id="e7f33-123">Create load-balanced VM endpoints with direct server return</span></span>
<span data-ttu-id="e7f33-124">Creare innanzitutto un servizio di bilanciamento del carico interno eseguendo lo script riportato più avanti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="e7f33-124">You first create an ILB by running the script later in this section.</span></span>

<span data-ttu-id="e7f33-125">Creare un endpoint con carico bilanciato per ogni VM che ospita una replica di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7f33-125">Create a load-balanced endpoint for each VM that hosts an Azure replica.</span></span> <span data-ttu-id="e7f33-126">Se si hanno repliche in più aree, ogni replica per tale area deve essere nello stesso servizio cloud nella stessa rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7f33-126">If you have replicas in multiple regions, each replica for that region must be in the same cloud service in the same Azure virtual network.</span></span> <span data-ttu-id="e7f33-127">La creazione di repliche del gruppo di disponibilità che si estendono su più aree di Azure richiede la configurazione di più reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="e7f33-127">Creating availability group replicas that span multiple Azure regions requires configuring multiple virtual networks.</span></span> <span data-ttu-id="e7f33-128">Per informazioni sulla configurazione della connettività fra reti virtuali, vedere [Configurare una connessione da rete virtuale a rete virtuale](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="e7f33-128">For more information on configuring cross virtual network connectivity, see [Configure virtual network to virtual network connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span>

1. <span data-ttu-id="e7f33-129">Nel portale di Azure passare a ogni VM che ospita una replica per vedere i dettagli.</span><span class="sxs-lookup"><span data-stu-id="e7f33-129">In the Azure portal, go to each VM that hosts a replica to view the details.</span></span>

2. <span data-ttu-id="e7f33-130">Scegliere la scheda **Endpoint** per ogni VM.</span><span class="sxs-lookup"><span data-stu-id="e7f33-130">Click the **Endpoints** tab for each VM.</span></span>

3. <span data-ttu-id="e7f33-131">Verificare che il **nome** e la **porta pubblica** specificati per l'endpoint del listener non siano già in uso.</span><span class="sxs-lookup"><span data-stu-id="e7f33-131">Verify that the **Name** and **Public Port** of the listener endpoint that you want to use are not already in use.</span></span> <span data-ttu-id="e7f33-132">Nell'esempio di questa sezione il nome è *MyEndpoint* e la porta è *1433*.</span><span class="sxs-lookup"><span data-stu-id="e7f33-132">In the example in this section, the name is *MyEndpoint*, and the port is *1433*.</span></span>

4. <span data-ttu-id="e7f33-133">Nel client locale scaricare e installare [l'ultimo modulo PowerShell](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e7f33-133">On your local client, download and install the latest [PowerShell module](https://azure.microsoft.com/downloads/).</span></span>

5. <span data-ttu-id="e7f33-134">Avviare Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7f33-134">Start Azure PowerShell.</span></span>  
    <span data-ttu-id="e7f33-135">Viene aperta una nuova sessione di PowerShell con i moduli amministrativi di Azure caricati.</span><span class="sxs-lookup"><span data-stu-id="e7f33-135">A new PowerShell session opens, with the Azure administrative modules loaded.</span></span>

6. <span data-ttu-id="e7f33-136">Eseguire `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="e7f33-136">Run `Get-AzurePublishSettingsFile`.</span></span> <span data-ttu-id="e7f33-137">Questo cmdlet conduce a un browser per scaricare un file di impostazioni di pubblicazione in una directory locale.</span><span class="sxs-lookup"><span data-stu-id="e7f33-137">This cmdlet directs you to a browser to download a publish settings file to a local directory.</span></span> <span data-ttu-id="e7f33-138">Potrebbero essere richieste le credenziali di accesso per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7f33-138">You might be prompted for your sign-in credentials for your Azure subscription.</span></span>

7. <span data-ttu-id="e7f33-139">Eseguire il comando `Import-AzurePublishSettingsFile` seguente con il percorso del file delle impostazioni di pubblicazione scaricato:</span><span class="sxs-lookup"><span data-stu-id="e7f33-139">Run the following `Import-AzurePublishSettingsFile` command with the path of the publish settings file that you downloaded:</span></span>

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    <span data-ttu-id="e7f33-140">Dopo aver importato il file delle impostazioni di pubblicazione, è possibile gestire la sottoscrizione di Azure nella sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7f33-140">After the publish settings file is imported, you can manage your Azure subscription in the PowerShell session.</span></span>

8. <span data-ttu-id="e7f33-141">Per *ILB* assegnare un indirizzo IP statico.</span><span class="sxs-lookup"><span data-stu-id="e7f33-141">For *ILB*, assign a static IP address.</span></span> <span data-ttu-id="e7f33-142">Esaminare la configurazione attuale della rete virtuale eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e7f33-142">Examine the current virtual network configuration by running the following command:</span></span>

        (Get-AzureVNetConfig).XMLConfiguration
9. <span data-ttu-id="e7f33-143">Annotare il nome *Subnet* per la subnet contenente le VM che ospitano le repliche.</span><span class="sxs-lookup"><span data-stu-id="e7f33-143">Note the *Subnet* name for the subnet that contains the VMs that host the replicas.</span></span> <span data-ttu-id="e7f33-144">Questo nome viene usato nel parametro $SubnetName nello script.</span><span class="sxs-lookup"><span data-stu-id="e7f33-144">This name is used in the $SubnetName parameter in the script.</span></span>

10. <span data-ttu-id="e7f33-145">Annotare il valore *VirtualNetworkSite* e il valore iniziale *AddressPrefix* per la subnet contenente le VM che ospitano le repliche.</span><span class="sxs-lookup"><span data-stu-id="e7f33-145">Note the *VirtualNetworkSite* name and the starting *AddressPrefix* for the subnet that contains the VMs that host the replicas.</span></span> <span data-ttu-id="e7f33-146">Cercare un indirizzo IP disponibile passando entrambi i valori al comando `Test-AzureStaticVNetIP` ed esaminando il valore *AvailableAddresses*.</span><span class="sxs-lookup"><span data-stu-id="e7f33-146">Look for an available IP address by passing both values to the `Test-AzureStaticVNetIP` command and by examining the *AvailableAddresses*.</span></span> <span data-ttu-id="e7f33-147">Se, ad esempio, il nome della rete virtuale è *MyVNet* e l'inizio dell'intervallo di indirizzi della subnet corrisponde a *172.16.0.128*, il comando seguente elencherà gli indirizzi disponibili:</span><span class="sxs-lookup"><span data-stu-id="e7f33-147">For example, if the virtual network is named *MyVNet* and has a subnet address range that starts at *172.16.0.128*, the following command would list available addresses:</span></span>

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. <span data-ttu-id="e7f33-148">Selezionare uno degli indirizzi disponibili e usarlo nel parametro $ILBStaticIP dello script al passaggio seguente.</span><span class="sxs-lookup"><span data-stu-id="e7f33-148">Select one of the available addresses, and use it in the $ILBStaticIP parameter of the script in the next step.</span></span>

12. <span data-ttu-id="e7f33-149">Copiare lo script di PowerShell seguente in un editor di testo e impostare i valori delle variabili in base all'ambiente.</span><span class="sxs-lookup"><span data-stu-id="e7f33-149">Copy the following PowerShell script to a text editor, and set the variable values to suit your environment.</span></span> <span data-ttu-id="e7f33-150">Per alcuni parametri sono stati forniti valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="e7f33-150">Defaults have been provided for some parameters.</span></span>  

    <span data-ttu-id="e7f33-151">Le distribuzioni esistenti che usano i gruppi di affinità non potranno aggiungere un servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="e7f33-151">Existing deployments that use affinity groups cannot add an ILB.</span></span> <span data-ttu-id="e7f33-152">Per altre informazioni sui requisiti per il servizio di bilanciamento del carico interno, vedere la [panoramica del bilanciamento del carico interno](../../../load-balancer/load-balancer-internal-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e7f33-152">For more information about ILB requirements, see [Internal load balancer overview](../../../load-balancer/load-balancer-internal-overview.md).</span></span>

    <span data-ttu-id="e7f33-153">Se il gruppo di disponibilità si estende tra diverse aree di Azure, è necessario eseguire lo script una volta in ogni data center per il servizio cloud e i nodi che risiedono nel data center.</span><span class="sxs-lookup"><span data-stu-id="e7f33-153">Also, if your availability group spans Azure regions, you must run the script once in each datacenter for the cloud service and nodes that reside in that datacenter.</span></span>

        # Define variables
        $ServiceName = "<MyCloudService>" # the name of the cloud service that contains the availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in the same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that the replicas use in the virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for the ILB in the subnet
        $ILBName = "AGListenerLB" # customize the ILB name or use this default value

        # Create the ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. <span data-ttu-id="e7f33-154">Dopo aver impostato le variabili, copiare lo script dall'editor di testo nella sessione di PowerShell per eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="e7f33-154">After you have set the variables, copy the script from the text editor to your PowerShell session to run it.</span></span> <span data-ttu-id="e7f33-155">Se nel prompt viene ancora visualizzato **>>**, digitare di nuovo INVIO per assicurarsi che l'esecuzione dello script sia stata avviata.</span><span class="sxs-lookup"><span data-stu-id="e7f33-155">If the prompt still shows **>>**, press Enter again to make sure the script starts running.</span></span>

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a><span data-ttu-id="e7f33-156">Se necessario, verificare che KB2854082 sia installato.</span><span class="sxs-lookup"><span data-stu-id="e7f33-156">Verify that KB2854082 is installed if necessary</span></span>
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-the-firewall-ports-in-availability-group-nodes"></a><span data-ttu-id="e7f33-157">Aprire le porte firewall nei nodi del gruppo di disponibilità in</span><span class="sxs-lookup"><span data-stu-id="e7f33-157">Open the firewall ports in availability group nodes</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-the-availability-group-listener"></a><span data-ttu-id="e7f33-158">Creare il listener del gruppo di disponibilità</span><span class="sxs-lookup"><span data-stu-id="e7f33-158">Create the availability group listener</span></span>

<span data-ttu-id="e7f33-159">Creare il listener del gruppo di disponibilità in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="e7f33-159">Create the availability group listener in two steps.</span></span> <span data-ttu-id="e7f33-160">Creare prima di tutto la risorsa cluster del punto di accesso client e configurare le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="e7f33-160">First, create the client access point cluster resource and configure  dependencies.</span></span> <span data-ttu-id="e7f33-161">Come seconda cosa, configurare le risorse del cluster in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7f33-161">Second, configure the cluster resources in PowerShell.</span></span>

### <a name="create-the-client-access-point-and-configure-the-cluster-dependencies"></a><span data-ttu-id="e7f33-162">Creare il punto di accesso client e configurare le dipendenze del cluster</span><span class="sxs-lookup"><span data-stu-id="e7f33-162">Create the client access point and configure the cluster dependencies</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-the-cluster-resources-in-powershell"></a><span data-ttu-id="e7f33-163">Configurare le risorse del cluster in PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7f33-163">Configure the cluster resources in PowerShell</span></span>
1. <span data-ttu-id="e7f33-164">Per il servizio di bilanciamento del carico interno è necessario usare l'indirizzo IP del servizio di bilanciamento del carico interno creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e7f33-164">For ILB, you must use the IP address of the ILB that was created earlier.</span></span> <span data-ttu-id="e7f33-165">Usare lo script seguente per ottenere questo indirizzo IP in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e7f33-165">To obtain this IP address in PowerShell, use the following script:</span></span>

        # Define variables
        $ServiceName="<MyServiceName>" # the name of the cloud service that contains the AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. <span data-ttu-id="e7f33-166">Su una delle VM copiare lo script di PowerShell del sistema operativo in un editor di testo quindi impostare le variabili sui valori annotati prima.</span><span class="sxs-lookup"><span data-stu-id="e7f33-166">On one of the VMs, copy the PowerShell script for your operating system to a text editor, and then set the variables to the values you noted earlier.</span></span>

    <span data-ttu-id="e7f33-167">Per Windows Server 2012 o versione successiva usare lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="e7f33-167">For Windows Server 2012 or later, use the following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
        $IPResourceName = "<IPResourceName>" # the IP address resource name
        $ILBIP = “<X.X.X.X>” # the IP address of the ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    <span data-ttu-id="e7f33-168">Per Windows Server 2008 R2 usare lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="e7f33-168">For Windows Server 2008 R2, use the following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
        $IPResourceName = "<IPResourceName>" # the IP address resource name
        $ILBIP = “<X.X.X.X>” # the IP address of the ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. <span data-ttu-id="e7f33-169">Dopo aver impostato le variabili, aprire una finestra con privilegi elevati di Windows PowerShell, incollare lo script dall'editor di testo nella sessione di PowerShell per eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="e7f33-169">After you have set the variables, open an elevated Windows PowerShell window, paste the script from the text editor into your PowerShell session to run it.</span></span> <span data-ttu-id="e7f33-170">Se nel prompt viene ancora visualizzato **>>**, digitare di nuovo INVIO per assicurarsi che l'esecuzione dello script sia stata avviata.</span><span class="sxs-lookup"><span data-stu-id="e7f33-170">If the prompt still shows **>>**, Press Enter again to make sure that the script starts running.</span></span>

4. <span data-ttu-id="e7f33-171">Ripetere i passaggi precedenti per ciascuna VM.</span><span class="sxs-lookup"><span data-stu-id="e7f33-171">Repeat the preceding steps for each VM.</span></span>  
    <span data-ttu-id="e7f33-172">Questo script consente di configurare la risorsa Indirizzo IP con l'indirizzo IP del servizio cloud e di impostare altri parametri come la porta probe.</span><span class="sxs-lookup"><span data-stu-id="e7f33-172">This script configures the IP address resource with the IP address of the cloud service and sets other parameters, such as the probe port.</span></span> <span data-ttu-id="e7f33-173">Quando la risorsa Indirizzo IP viene portata online, può rispondere al polling sulla porta probe dall'endpoint con carico bilanciato, creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e7f33-173">When the IP address resource is brought online, it can respond to the polling on the probe port from the load-balanced endpoint that you created earlier.</span></span>

## <a name="bring-the-listener-online"></a><span data-ttu-id="e7f33-174">Portare online il listener</span><span class="sxs-lookup"><span data-stu-id="e7f33-174">Bring the listener online</span></span>
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a><span data-ttu-id="e7f33-175">Operazioni di completamento della procedura</span><span class="sxs-lookup"><span data-stu-id="e7f33-175">Follow-up items</span></span>
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-the-availability-group-listener-within-the-same-virtual-network"></a><span data-ttu-id="e7f33-176">Testare il listener del gruppo di disponibilità (entro la stessa rete virtuale)</span><span class="sxs-lookup"><span data-stu-id="e7f33-176">Test the availability group listener (within the same virtual network)</span></span>
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a><span data-ttu-id="e7f33-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e7f33-177">Next steps</span></span>
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]

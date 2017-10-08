---
title: ambiente di test basato su cloud ibrido aaaSimulated | Documenti Microsoft
description: Creare un ambiente cloud ibrido simulato per test per professionisti IT o test di sviluppo, usando due reti virtuali di Azure e una connessione da rete virtuale a rete virtuale.
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ca5bf294-8172-44a9-8fed-d6f38d345364
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 6063022e373c2b3564e040c4fbee122e2438974b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a><span data-ttu-id="0b5aa-103">Configurazione di un ambiente cloud ibrido simulato per l'esecuzione di test</span><span class="sxs-lookup"><span data-stu-id="0b5aa-103">Set up a simulated hybrid cloud environment for testing</span></span>
<span data-ttu-id="0b5aa-104">Questo articolo è una guida alla creazione di un ambiente cloud ibrido simulato con Microsoft Azure che usa due reti virtuali di Azure separate.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-104">This article steps you through creating a simulated hybrid cloud environment with Microsoft Azure using two Azure virtual networks.</span></span> <span data-ttu-id="0b5aa-105">Di seguito è riportata la configurazione risultante hello.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="0b5aa-106">Permette di simulare un ambiente di produzione cloud ibrido e include:</span><span class="sxs-lookup"><span data-stu-id="0b5aa-106">This simulates a hybrid cloud production environment and consists of:</span></span>

* <span data-ttu-id="0b5aa-107">Una rete locale simulata e semplificata ospitata in una rete virtuale di Azure (rete virtuale di hello esercitazione).</span><span class="sxs-lookup"><span data-stu-id="0b5aa-107">A simulated and simplified on-premises network hosted in an Azure virtual network (hello TestLab virtual network).</span></span>
* <span data-ttu-id="0b5aa-108">Una rete virtuale cross-premise simulata ospitata in Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="0b5aa-108">A simulated cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="0b5aa-109">Una connessione di rete virtuale a tra reti virtuali hello due.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-109">A VNet-to-VNet connection between hello two virtual networks.</span></span>
* <span data-ttu-id="0b5aa-110">Un controller di dominio secondario nella rete virtuale di hello TestVNET.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-110">A secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="0b5aa-111">Questa configurazione fornisce una base e un punto di partenza comune da cui è possibile:</span><span class="sxs-lookup"><span data-stu-id="0b5aa-111">This provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="0b5aa-112">Sviluppare e testare applicazioni in un ambiente cloud ibrido simulato.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-112">Develop and test applications in a simulated hybrid cloud environment.</span></span>
* <span data-ttu-id="0b5aa-113">Creare configurazioni di test di computer, alcune all'interno di rete virtuale di esercitazione hello e alcuni in rete virtuale hello TestVNET, toosimulate ibrido basato su cloud carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-113">Create test configurations of computers, some within hello TestLab virtual network and some within hello TestVNET virtual network, toosimulate hybrid cloud-based IT workloads.</span></span>

<span data-ttu-id="0b5aa-114">Esistono quattro fasi principali toosetting un ambiente di testing cloud ibrida:</span><span class="sxs-lookup"><span data-stu-id="0b5aa-114">There are four major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="0b5aa-115">Configurare la rete virtuale di hello esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-115">Configure hello TestLab virtual network.</span></span>
2. <span data-ttu-id="0b5aa-116">Creare una rete virtuale cross-premise di hello.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-116">Create hello cross-premises virtual network.</span></span>
3. <span data-ttu-id="0b5aa-117">Creare la connessione VPN per rete virtuale a hello.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-117">Create hello VNet-to-VNet VPN connection.</span></span>
4. <span data-ttu-id="0b5aa-118">Configurare DC2.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-118">Configure DC2.</span></span> 

<span data-ttu-id="0b5aa-119">Questa configurazione richiede una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-119">This configuration requires an Azure subscription.</span></span> <span data-ttu-id="0b5aa-120">Se si ha un abbonamento a MSDN o una sottoscrizione di Visual Studio, vedere [Credito Azure mensile per sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="0b5aa-120">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

> [!NOTE]
> <span data-ttu-id="0b5aa-121">Le macchine virtuali e i gateway di rete virtuale in Azure generano addebiti monetari in caso di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-121">Virtual machines and virtual network gateways in Azure incur an ongoing monetary cost when they are running.</span></span> <span data-ttu-id="0b5aa-122">Il costo viene addebitato sulla base dell'abbonamento a MSDN o della sottoscrizione a pagamento.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-122">This cost is billed against your MSDN or paid subscription.</span></span> <span data-ttu-id="0b5aa-123">Un gateway VPN di Azure viene implementato come set di due macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-123">An Azure VPN gateway is implemented as a set of two Azure virtual machines.</span></span> <span data-ttu-id="0b5aa-124">costi di hello toominimize, creare l'ambiente di test hello ed eseguire il test e dimostrativi necessari al più presto.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-124">toominimize hello costs, create hello test environment and perform your needed testing and demonstration as quickly as possible.</span></span>
> 
> 

## <a name="phase-1-configure-hello-testlab-virtual-network"></a><span data-ttu-id="0b5aa-125">Fase 1: Configurare la rete virtuale di hello esercitazione</span><span class="sxs-lookup"><span data-stu-id="0b5aa-125">Phase 1: Configure hello TestLab virtual network</span></span>
<span data-ttu-id="0b5aa-126">Utilizzare istruzioni hello in hello [ambiente di test configurazione di Base](https://technet.microsoft.com/library/mt771177.aspx) argomento tooconfigure hello DC1, APP1 e CLIENT1 computer nella rete virtuale di Azure denominato esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-126">Use hello instructions in hello [Base Configuration test environment](https://technet.microsoft.com/library/mt771177.aspx) topic tooconfigure hello DC1, APP1, and CLIENT1 computers in hello Azure virtual network named TestLab.</span></span> 

<span data-ttu-id="0b5aa-127">Avviare un prompt di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-127">Next, start an Azure PowerShell prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="0b5aa-128">comando set seguenti Hello Usa Azure PowerShell 1.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-128">hello following command sets use Azure PowerShell 1.0 and later.</span></span>
> 
> 

<span data-ttu-id="0b5aa-129">Eseguire l'accesso tooyour account.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-129">Sign in tooyour account.</span></span>

    Login-AzureRMAccount

<span data-ttu-id="0b5aa-130">Ottenere il nome della sottoscrizione tramite hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-130">Get your subscription name using hello following command.</span></span>

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="0b5aa-131">Impostare la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-131">Set your Azure subscription.</span></span> <span data-ttu-id="0b5aa-132">Utilizzare hello stessa sottoscrizione utilizzata toobuild configurazione di base nella fase 1.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-132">Use hello same subscription that you used toobuild your base configuration in Phase 1.</span></span> <span data-ttu-id="0b5aa-133">Sostituire tutto il contenuto all'interno di virgolette hello, tra cui hello < e > caratteri, con il nome corretto hello.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-133">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

<span data-ttu-id="0b5aa-134">Successivamente, aggiungere una gateway subnet toohello esercitazione rete virtuale della configurazione di base, che sarà utilizzato toohost hello Azure gateway.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-134">Next, add a gateway subnet toohello TestLab virtual network of your base configuration, which will be used toohost hello Azure gateway.</span></span>

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

<span data-ttu-id="0b5aa-135">Successivamente, richiedere un pubblico gateway toohello tooassign di indirizzo IP per rete virtuale di hello esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-135">Next, request a public IP address tooassign toohello gateway for hello TestLab virtual network.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

<span data-ttu-id="0b5aa-136">Creare il gateway.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-136">Next, create your gateway.</span></span>

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="0b5aa-137">Tenere presente che i nuovi gateway può richiedere 20 minuti o più toocreate.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-137">Keep in mind that new gateways can take 20 minutes or more toocreate.</span></span>

<span data-ttu-id="0b5aa-138">Da hello portale di Azure nel computer locale, connettersi tooDC1 con credenziali CORP\User1 hello.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-138">From hello Azure portal on your local computer, connect tooDC1 with hello CORP\User1 credentials.</span></span> <span data-ttu-id="0b5aa-139">dominio CORP di tooconfigure hello in modo che utenti e computer di utilizzano i controller di dominio locale per l'autenticazione, eseguire questi comandi da un prompt dei comandi di Windows PowerShell a livello di amministratore in DC1.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-139">tooconfigure hello CORP domain so that computers and users use their local domain controller for authentication, run these commands from an administrator-level Windows PowerShell command prompt on DC1.</span></span>

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

<span data-ttu-id="0b5aa-140">Questa è la configurazione corrente.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-140">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-hello-testvnet-virtual-network"></a><span data-ttu-id="0b5aa-141">Fase 2: Creare la rete virtuale di hello TestVNET</span><span class="sxs-lookup"><span data-stu-id="0b5aa-141">Phase 2: Create hello TestVNET virtual network</span></span>
<span data-ttu-id="0b5aa-142">Innanzitutto, creare una rete virtuale di hello TestVNET e proteggerli con un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-142">First, create hello TestVNET virtual network and protect it with a network security group.</span></span>

    $rgName="<name of hello resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP tooall VMs on hello subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

<span data-ttu-id="0b5aa-143">Quindi richiesta una toobe di indirizzo IP pubblico allocato toohello gateway per la rete virtuale di hello TestVNET e creare il gateway.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-143">Next, request a public IP address toobe allocated toohello gateway for hello TestVNET virtual network and create your gateway.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="0b5aa-144">Questa è la configurazione corrente.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-144">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-hello-vnet-to-vnet-connection"></a><span data-ttu-id="0b5aa-145">Fase 3: Creare una connessione di rete virtuale a hello</span><span class="sxs-lookup"><span data-stu-id="0b5aa-145">Phase 3: Create hello VNet-to-VNet connection</span></span>
<span data-ttu-id="0b5aa-146">Richiedere all'amministratore di rete o della sicurezza una chiave casuale, crittograficamente complessa, a 32 caratteri, precondivisa.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-146">First, obtain a random, cryptographically strong, 32-character pre-shared key from your network or security administrator.</span></span> <span data-ttu-id="0b5aa-147">In alternativa, utilizzare informazioni hello [creare una stringa casuale per una chiave precondivisa IPsec](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain una chiave già condivisa.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-147">Alternately, use hello information at [Create a random string for an IPsec preshared key](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain a pre-shared key.</span></span>

<span data-ttu-id="0b5aa-148">Successivamente, utilizzare questi comandi toocreate hello da rete connessione VPN, che può richiedere alcuni toocomplete ora.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-148">Next, use these commands toocreate hello VNet-to-VNet VPN connection, which can take some time toocomplete.</span></span>

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

<span data-ttu-id="0b5aa-149">Dopo alcuni minuti, hello devono connettersi.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-149">After a few minutes, hello connection should be established.</span></span>

<span data-ttu-id="0b5aa-150">Questa è la configurazione corrente.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-150">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a><span data-ttu-id="0b5aa-151">Fase 4: Configurare DC2.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-151">Phase 4: Configure DC2</span></span>
<span data-ttu-id="0b5aa-152">Creare prima di tutto una macchina virtuale per DC2.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-152">First, create a virtual machine for DC2.</span></span> <span data-ttu-id="0b5aa-153">Eseguire questi comandi al prompt dei comandi di hello Azure PowerShell nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-153">Run these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<hello storage account name for hello base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="0b5aa-154">Successivamente, connettersi toohello nuova macchina virtuale di DC2 da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-154">Next, connect toohello new DC2 virtual machine from hello Azure portal.</span></span>

<span data-ttu-id="0b5aa-155">Configurare quindi il traffico tooallow una regola Windows Firewall per verificare la connettività di base.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-155">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="0b5aa-156">Da un prompt dei comandi di Windows PowerShell a livello di amministratore in DC2 eseguire questi comandi.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-156">From an administrator-level Windows PowerShell command prompt on DC2, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

<span data-ttu-id="0b5aa-157">comando ping Hello dovrebbe restituire quattro risposte dall'indirizzo IP 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-157">hello ping command should result in four successful replies from IP address 10.0.0.4.</span></span> <span data-ttu-id="0b5aa-158">Si tratta di un test di traffico per hello da rete connessione.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-158">This is a test of traffic across hello VNet-to-VNet connection.</span></span>

<span data-ttu-id="0b5aa-159">Successivamente, aggiungere hello disco dati supplementare in DC2, come un nuovo volume con lettera dell'unità f: hello.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-159">Next, add hello extra data disk on DC2 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="0b5aa-160">Nel riquadro sinistro hello di Server Manager, fare clic su **servizi File e archiviazione**, quindi fare clic su **dischi**.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-160">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="0b5aa-161">Nel riquadro contenuti hello in hello **dischi** gruppo, fare clic su **disco 2** (con hello **partizione** impostare troppo**sconosciuto**).</span><span class="sxs-lookup"><span data-stu-id="0b5aa-161">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="0b5aa-162">Fare clic su **Attività**, quindi su **Nuovo volume**.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-162">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="0b5aa-163">Hello prima pagina della creazione guidata nuovo Volume hello, scegliere **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-163">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="0b5aa-164">Nel server di selezionare hello hello e pagina su disco, fare clic su **disco 2**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-164">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="0b5aa-165">Quando richiesto, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-165">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="0b5aa-166">Specifica dimensioni hello della pagina volume hello hello, scegliere **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-166">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="0b5aa-167">Pagina hello assegnare tooa unità lettera o una cartella, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-167">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="0b5aa-168">Nella pagina Impostazioni di hello selezionare il file system, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-168">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="0b5aa-169">Nella pagina Conferma selezioni per hello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-169">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="0b5aa-170">Al termine, fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-170">When complete, click **Close**.</span></span>

<span data-ttu-id="0b5aa-171">A questo punto, configurare DC2 come controller di dominio di replica per il dominio corp.contoso.com hello.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-171">Next, configure DC2 as a replica domain controller for hello corp.contoso.com domain.</span></span> <span data-ttu-id="0b5aa-172">Eseguire questi comandi dal prompt dei comandi di Windows PowerShell hello in DC2.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-172">Run these commands from hello Windows PowerShell command prompt on DC2.</span></span>

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

<span data-ttu-id="0b5aa-173">Si noti che richiesta toosupply entrambi hello CORP\User1 e password e una password modalità ripristino servizi Directory (DSRM), toorestart DC2.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-173">Note that you are prompted toosupply both hello CORP\User1 password and a Directory Services Restore Mode (DSRM) password, and toorestart DC2.</span></span>

<span data-ttu-id="0b5aa-174">Ora che hello TestVNET di rete virtuale è il proprio server DNS (DC2), è necessario configurare hello TestVNET rete virtuale toouse questo server DNS.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-174">Now that hello TestVNET virtual network has its own DNS server (DC2), you must configure hello TestVNET virtual network toouse this DNS server.</span></span>

1. <span data-ttu-id="0b5aa-175">Nel riquadro sinistro di hello di hello portale di Azure, fare clic sull'icona di reti virtuali hello e quindi fare clic su **TestVNET**.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-175">In hello left pane of hello Azure portal, click hello virtual networks icon, and then click **TestVNET**.</span></span>
2. <span data-ttu-id="0b5aa-176">In hello **impostazioni** scheda, fare clic su **server DNS**.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-176">On hello **Settings** tab, click **DNS servers**.</span></span>
3. <span data-ttu-id="0b5aa-177">In **server DNS primario**, tipo **192.168.0.4** tooreplace 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-177">In **Primary DNS server**, type **192.168.0.4** tooreplace 10.0.0.4.</span></span>
4. <span data-ttu-id="0b5aa-178">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-178">Click **Save**.</span></span>

<span data-ttu-id="0b5aa-179">Questa è la configurazione corrente.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-179">This is your current configuration.</span></span> 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="0b5aa-180">L'ambiente cloud ibrido simulato è ora pronto per il testing.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-180">Your simulated hybrid cloud environment is now ready for testing.</span></span>

## <a name="next-step"></a><span data-ttu-id="0b5aa-181">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="0b5aa-181">Next step</span></span>
* <span data-ttu-id="0b5aa-182">Configurare un'[applicazione line-of-business basata sul Web](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in questo ambiente.</span><span class="sxs-lookup"><span data-stu-id="0b5aa-182">Set up a [web-based, line of business application](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in this environment.</span></span>


---
title: "Creare una VM (classica) con più schede di interfaccia di rete con PowerShell | Documentazione Microsoft"
description: "Informazioni su come creare e configurare VM con più schede di interfaccia di rete usando PowerShell."
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 68ccc1cac22e593b099729fe68c6bee63df44d9b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a><span data-ttu-id="7b3ed-103">Creare una VM (classica) con più schede di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="7b3ed-103">Create a VM (Classic) with multiple NICs</span></span>
<span data-ttu-id="7b3ed-104">È possibile creare macchine virtuali (VM) in Azure e collegare più interfacce di rete (NIC) a ciascuna delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="7b3ed-105">L'uso di più schede di interfaccia di rete è un requisito per molti dispositivi virtuali di rete, ad esempio le soluzioni di ottimizzazione WAN e la distribuzione di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span> <span data-ttu-id="7b3ed-106">Più schede di interfaccia di rete forniscono anche l'isolamento del traffico tra le schede.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-106">Multiple NICs also provide isolation of traffic between NICs.</span></span>

![Più NIC per la macchina virtuale](./media/virtual-networks-multiple-nics/IC757773.png)

<span data-ttu-id="7b3ed-108">La figura illustra una VM con tre schede di interfaccia di rete, ciascuna connessa a una subnet diversa.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-108">The figure shows a VM with three NICs, each connected to a different subnet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b3ed-109">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7b3ed-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7b3ed-110">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-110">This article covers using the classic deployment model.</span></span> <span data-ttu-id="7b3ed-111">Microsoft consiglia di usare Resource Manager per la maggior parte delle distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-111">Microsoft recommends that most new deployments use Resource Manager.</span></span>

* <span data-ttu-id="7b3ed-112">L’indirizzo VIP con connessione Internet (distribuzioni classiche) è supportato solo sulla NIC "predefinita".</span><span class="sxs-lookup"><span data-stu-id="7b3ed-112">Internet-facing VIP (classic deployments) is only supported on the "default" NIC.</span></span> <span data-ttu-id="7b3ed-113">Esiste un solo indirizzo VIP per l'indirizzo IP della NIC predefinita.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-113">There is only one VIP to the IP of the default NIC.</span></span>
* <span data-ttu-id="7b3ed-114">Attualmente, gli indirizzi IP pubblici a livello di istanza (LPIP) (distribuzioni classiche) non sono supportati per le macchine virtuali a più NIC.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span></span>
* <span data-ttu-id="7b3ed-115">L'ordine delle NIC all'interno della macchina virtuale sarà casuale e potrebbe cambiare con gli aggiornamenti dell'infrastruttura di Azure.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-115">The order of the NICs from inside the VM will be random, and could also change across Azure infrastructure updates.</span></span> <span data-ttu-id="7b3ed-116">Tuttavia, gli indirizzi IP e gli indirizzi MAC ethernet corrispondenti resteranno invariati.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-116">However, the IP addresses, and the corresponding ethernet MAC addresses will remain the same.</span></span> <span data-ttu-id="7b3ed-117">Si supponga, ad esempio, che **Eth1** abbia l'indirizzo IP 10.1.0.100 e l'indirizzo MAC 00-0D-3A-B0-39-0D; dopo un aggiornamento dell'infrastruttura di Azure e il riavvio, potrebbe essere modificato in **Eth2**, ma l'abbinamento di indirizzo IP e MAC resterà invariato.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed to **Eth2**, but the IP and MAC pairing will remain the same.</span></span> <span data-ttu-id="7b3ed-118">Quando un riavvio è eseguito dal cliente, l'ordine delle NIC rimane invariato.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-118">When a restart is customer-initiated, the NIC order will remain the same.</span></span>
* <span data-ttu-id="7b3ed-119">L'indirizzo di ciascuna NIC su ciascuna macchina virtuale deve trovarsi in una subnet, a più NIC in una singola macchina virtuale possono essere assegnati indirizzi che si trovano nella stessa subnet.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-119">The address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in the same subnet.</span></span>
* <span data-ttu-id="7b3ed-120">Le dimensioni della macchina virtuale determinano il numero di NIC che è possibile creare per una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-120">The VM size determines the number of NICS that you can create for a VM.</span></span> <span data-ttu-id="7b3ed-121">Fare riferimento agli articoli sulle dimensioni delle VM in [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per determinare il numero di schede di interfacce di rete supportate da ciascuna dimensione di VM.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-121">Reference the [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles to determine how many NICS each VM size supports.</span></span> 

## <a name="network-security-groups-nsgs"></a><span data-ttu-id="7b3ed-122">Gruppi di sicurezza di rete (NGS)</span><span class="sxs-lookup"><span data-stu-id="7b3ed-122">Network Security Groups (NSGs)</span></span>
<span data-ttu-id="7b3ed-123">In una distribuzione di Gestione risorse, qualsiasi NIC in una macchina virtuale può essere associata a un Gruppo di sicurezza di rete, incluse eventuali NIC in una macchina virtuale che presenta la funzionalità Multi-NIC abilitata.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span></span> <span data-ttu-id="7b3ed-124">Se a una NIC viene assegnato un indirizzo all'interno di una subnet dove la subnet è associata a un Gruppo di sicurezza di rete, le regole del Gruppo di sicurezza di rete della subnet si applicano anche a tale NIC.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-124">If a NIC is assigned an address within a subnet where the subnet is associated with an NSG, then the rules in the subnet’s NSG also apply to that NIC.</span></span> <span data-ttu-id="7b3ed-125">Oltre alle subnet, è possibile associare ai Gruppi di sicurezza di rete anche una NIC.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-125">In addition to associating subnets with NSGs, you can also associate a NIC with an NSG.</span></span>

<span data-ttu-id="7b3ed-126">Se una subnet è associata a un Gruppo di sicurezza di rete e una NIC all'interno di tale subnet è associata singolarmente a un Gruppo di sicurezza di rete, le regole del Gruppo di sicurezza di rete associato vengono applicate in **ordine flusso** , in base alla direzione del traffico in entrata e in uscita dalla NIC:</span><span class="sxs-lookup"><span data-stu-id="7b3ed-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, the associated NSG rules are applied in **flow order** according to the direction of the traffic being passed into or out of the NIC:</span></span>

* <span data-ttu-id="7b3ed-127">**Il traffico in entrata** , la cui destinazione è la NIC in questione, passa innanzitutto attraverso la subnet, attivando le regole del Gruppo di sicurezza di rete della subnet, prima di passare nella NIC, attivando quindi le regole del Gruppo di sicurezza di rete della NIC.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-127">**Incoming traffic** whose destination is the NIC in question flows first through the subnet, triggering the subnet’s NSG rules, before passing into the NIC, then triggering the NIC’s NSG rules.</span></span>
* <span data-ttu-id="7b3ed-128">**Il traffico in uscita** , la cui origine è la NIC in questione, fuoriesce innanzitutto dalla subnet, attivando le regole del Gruppo di sicurezza di rete della NIC, prima di passare attraverso la sunet, attivando quindi le regole del Gruppo di sicurezza di rete della subnet.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-128">**Outgoing traffic** whose source is the NIC in question flows first out from the NIC, triggering the NIC’s NSG rules, before passing through the subnet, then triggering the subnet’s NSG rules.</span></span>

<span data-ttu-id="7b3ed-129">Ulteriori informazioni su [Gruppi di sicurezza di rete](virtual-networks-nsg.md) e su come vengono applicati in base alle associazioni con le subnet, con le macchine virtuali e con le schede di rete.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations to subnets, VMs, and NICs..</span></span>

## <a name="how-to-configure-a-multi-nic-vm-in-a-classic-deployment"></a><span data-ttu-id="7b3ed-130">Come configurare una macchina virtuale Multi-NIC in una distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="7b3ed-130">How to Configure a multi NIC VM in a classic deployment</span></span>
<span data-ttu-id="7b3ed-131">Le istruzioni seguenti consentono di creare una macchina virtuale Multi-NIC contenente 3 NIC: una NIC predefinita e due NIC aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-131">The instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span></span> <span data-ttu-id="7b3ed-132">La procedura di configurazione consente di creare una macchina virtuale che verrà configurata in base al frammento del file di configurazione del servizio riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7b3ed-132">The configuration steps will create a VM that will be configured according to the service configuration file fragment below:</span></span>

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over the remainder section …
    </VirtualNetworkSite>


<span data-ttu-id="7b3ed-133">Per tentare di eseguire i comandi PowerShell riportati nell’esempio sono necessari i seguenti prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-133">You need the following prerequisites before trying to run the PowerShell commands in the example.</span></span>

* <span data-ttu-id="7b3ed-134">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-134">An Azure subscription.</span></span>
* <span data-ttu-id="7b3ed-135">Una rete virtuale configurata.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-135">A configured virtual network.</span></span> <span data-ttu-id="7b3ed-136">Per altre informazioni sulle reti virtuali, vedere [Panoramica di Rete virtuale](virtual-networks-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="7b3ed-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span></span>
* <span data-ttu-id="7b3ed-137">La versione più recente di Azure PowerShell scaricata e installata.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-137">The latest version of Azure PowerShell downloaded and installed.</span></span> <span data-ttu-id="7b3ed-138">Vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7b3ed-138">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="7b3ed-139">Per creare una VM con più schede di interfaccia di rete, completare i passaggi seguenti immettendo ogni comando in una singola sessione di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7b3ed-139">To create a VM with multiple NICs, complete the following steps by entering each command within a single PowerShell session:</span></span>

1. <span data-ttu-id="7b3ed-140">Selezionare un'immagine di macchina virtuale dalla raccolta immagini della macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-140">Select a VM image from Azure VM image gallery.</span></span> <span data-ttu-id="7b3ed-141">Le immagini cambiano frequentemente e sono disponibili per area geografica.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-141">Note that images change frequently and are available by region.</span></span> <span data-ttu-id="7b3ed-142">L'immagine specificata nell'esempio riportato di seguito può cambiare o potrebbe non trovarsi nell’area desiderata, assicurarsi pertanto di specificare l'immagine necessaria.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-142">The image specified in the example below may change or might not be in your region, so be sure to specify the image you need.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. <span data-ttu-id="7b3ed-143">Creare una configurazione di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-143">Create a VM configuration.</span></span>

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. <span data-ttu-id="7b3ed-144">Creare l’account di accesso dell’amministratore predefinito.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-144">Create the default administrator login.</span></span>

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. <span data-ttu-id="7b3ed-145">Aggiungere le schede NIC aggiuntive alla configurazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-145">Add additional NICs to the VM configuration.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. <span data-ttu-id="7b3ed-146">Specificare la subnet e l’indirizzo IP per la NIC predefinita.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-146">Specify the subnet and IP address for the default NIC.</span></span>

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. <span data-ttu-id="7b3ed-147">Creare la macchina virtuale nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-147">Create the VM in your virtual network.</span></span>

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > <span data-ttu-id="7b3ed-148">La rete virtuale specificata deve essere già esistente (come indicato nei prerequisiti).</span><span class="sxs-lookup"><span data-stu-id="7b3ed-148">The VNet that you specify here must already exist (as mentioned in the prerequisites).</span></span> <span data-ttu-id="7b3ed-149">Nell'esempio seguente viene specificata una rete virtuale denominata **MultiNIC-VNet**.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-149">The example below specifies a virtual network named **MultiNIC-VNet**.</span></span>
    >

## <a name="limitations"></a><span data-ttu-id="7b3ed-150">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="7b3ed-150">Limitations</span></span>
<span data-ttu-id="7b3ed-151">Quando si usano più schede di interfaccia di rete, sono applicabili le seguenti limitazioni:</span><span class="sxs-lookup"><span data-stu-id="7b3ed-151">The following limitations are applicable when using multiple NICs:</span></span>

* <span data-ttu-id="7b3ed-152">È necessario creare VM con più schede di interfaccia di rete nelle reti virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span></span> <span data-ttu-id="7b3ed-153">Non è possibile configurare VM che non si trovano in reti virtuali con più schede di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-153">Non-VNet VMs cannot be configured with multiple NICs.</span></span>
* <span data-ttu-id="7b3ed-154">Tutte le VM in un set di disponibilità devono usare più schede di interfaccia di rete o una singola scheda.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-154">All VMs in an availability set need to use either multiple NICs or a single NIC.</span></span> <span data-ttu-id="7b3ed-155">Non è possibile combinare VM con più schede di interfaccia di rete e VM con una singola scheda di interfaccia di rete all'interno di un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span></span> <span data-ttu-id="7b3ed-156">Le stesse regole sono valide per le VM in un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-156">Same rules apply for VMs in a cloud service.</span></span> <span data-ttu-id="7b3ed-157">Per le VM con più schede di interfaccia di rete, non è obbligatorio che il numero di schede siano lo stesso, a condizione che ognuna disponga almeno di due schede.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-157">For multiple NIC VMs, they aren't required to have the same number of NICs, as long as they each have at least two.</span></span>
* <span data-ttu-id="7b3ed-158">Non è possibile configurare una VM con una singola scheda di interfaccia di rete con più schede di interfaccia di rete (e viceversa) dopo la distribuzione, senza eliminarla e crearla di nuovo.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span></span>

## <a name="secondary-nics-access-to-other-subnets"></a><span data-ttu-id="7b3ed-159">Accesso NIC secondarie ad altre subnet</span><span class="sxs-lookup"><span data-stu-id="7b3ed-159">Secondary NICs access to other subnets</span></span>
<span data-ttu-id="7b3ed-160">Per impostazione predefinita, le NIC secondarie non verranno configurate con un gateway predefinito, pertanto il flusso del traffico sulle NIC secondarie sarà limitato esclusivamente all’interno della stessa subnet.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-160">By default secondary NICs will not be configured with a default gateway, due to which the traffic flow on the secondary NICs will be limited to be within the same subnet.</span></span> <span data-ttu-id="7b3ed-161">Se si desidera abilitare le NIC secondarie per la comunicazione all'esterno della propria subnet, si dovrà aggiungere una voce nella tabella di routing per configurare il gateway come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-161">If the users want to enable secondary NICs to talk outside their own subnet, they will need to add an entry in the routing table to configure the gateway as described below.</span></span>

> [!NOTE]
> <span data-ttu-id="7b3ed-162">Le VM create prima di luglio 2015 potrebbero avere un gateway predefinito configurato per tutte le NIC.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span></span> <span data-ttu-id="7b3ed-163">Il gateway predefinito per le NIC secondarie non verrà rimosso fino al riavvio delle VM.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-163">The default gateway for secondary NICs will not be removed until these VMs are rebooted.</span></span> <span data-ttu-id="7b3ed-164">Nei sistemi operativi che utilizzano il modello di routing dell'host vulnerabile, ad esempio Linux, la connettività Internet può interrompersi se il traffico in entrata e in uscita utilizza NIC diverse.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-164">In Operating systems that use the weak host routing model, such as Linux, Internet connectivity can break if the ingress and egress traffic use different NICs.</span></span>
> 

### <a name="configure-windows-vms"></a><span data-ttu-id="7b3ed-165">Configurare le macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="7b3ed-165">Configure Windows VMs</span></span>
<span data-ttu-id="7b3ed-166">Supponiamo di utilizzare una macchina virtuale di Windows con due NIC come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7b3ed-166">Suppose that you have a Windows VM with two NICs as follows:</span></span>

* <span data-ttu-id="7b3ed-167">Indirizzo IP primario della NIC: 192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="7b3ed-167">Primary NIC IP address: 192.168.1.4</span></span>
* <span data-ttu-id="7b3ed-168">Indirizzo IP secondario della NIC: 192.168.2.5</span><span class="sxs-lookup"><span data-stu-id="7b3ed-168">Secondary NIC IP address: 192.168.2.5</span></span>

<span data-ttu-id="7b3ed-169">La tabella di route IPv4 per questa macchina virtuale sarà analoga alla seguente:</span><span class="sxs-lookup"><span data-stu-id="7b3ed-169">The IPv4 route table for this VM would look like this:</span></span>

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

<span data-ttu-id="7b3ed-170">Si noti che la route predefinita (0.0.0.0) è disponibile solo per la NIC primaria.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-170">Notice that the default route (0.0.0.0) is only available to the primary NIC.</span></span> <span data-ttu-id="7b3ed-171">Non sarà possibile accedere alle risorse all'esterno della subnet per la NIC secondaria, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7b3ed-171">You will not be able to access resources outside the subnet for the secondary NIC, as seen below:</span></span>

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

<span data-ttu-id="7b3ed-172">Per aggiungere una route predefinita nella NIC secondaria, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7b3ed-172">To add a default route on the secondary NIC, follow the steps below:</span></span>

1. <span data-ttu-id="7b3ed-173">Dal prompt dei comandi, eseguire il seguente comando per identificare il numero di indice per la NIC secondaria:</span><span class="sxs-lookup"><span data-stu-id="7b3ed-173">From a command prompt, run the command below to identify the index number for the secondary NIC:</span></span>
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. <span data-ttu-id="7b3ed-174">Si noti la seconda voce nella tabella, con un indice pari a 27 (in questo esempio).</span><span class="sxs-lookup"><span data-stu-id="7b3ed-174">Notice the second entry in the table, with an index of 27 (in this example).</span></span>
3. <span data-ttu-id="7b3ed-175">Dal prompt dei comandi, eseguire il comando **aggiungere route** come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-175">From the command prompt, run the **route add** command as shown below.</span></span> <span data-ttu-id="7b3ed-176">In questo esempio si specifica 192.168.2.1 come gateway predefinito per la NIC secondaria:</span><span class="sxs-lookup"><span data-stu-id="7b3ed-176">In this example, you are specifying 192.168.2.1 as the default gateway for the secondary NIC:</span></span>
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. <span data-ttu-id="7b3ed-177">Per verificare la connettività, tornare al prompt dei comandi e provare a effettuare il ping a una subnet diversa dalla NIC secondaria come illustrato nell’esempio riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7b3ed-177">To test connectivity, go back to the command prompt and try to ping a different subnet from the secondary NIC as shown int eh example below:</span></span>
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. <span data-ttu-id="7b3ed-178">È inoltre possibile controllare la tabella di route per controllare la route appena aggiunta, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7b3ed-178">You can also check your route table to check the newly added route, as shown below:</span></span>
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a><span data-ttu-id="7b3ed-179">Configurare le macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="7b3ed-179">Configure Linux VMs</span></span>
<span data-ttu-id="7b3ed-180">Per le macchine virtuali Linux, poiché è stato utilizzato il comportamento predefinito dell'host routing vulnerabile, è consigliabile che le schede NIC secondarie siano limitate ai flussi di traffico all'interno della stessa subnet.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-180">For Linux VMs, since the default behavior uses weak host routing, we recommend that the secondary NICs are restricted to traffic flows only within the same subnet.</span></span> <span data-ttu-id="7b3ed-181">Tuttavia se alcune situazioni richiedono la connettività all'esterno della subnet, gli utenti devono attivare la “policy based routing” per fare in modo che il traffico in entrata e in uscita utilizzi la stessa scheda NIC.</span><span class="sxs-lookup"><span data-stu-id="7b3ed-181">However if certain scenarios demand connectivity outside the subnet, users should enable policy based routing to ensure that the ingress and egress traffic uses the same NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b3ed-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7b3ed-182">Next steps</span></span>
* <span data-ttu-id="7b3ed-183">Distribuire [Macchine virtuali MultiNIC in uno scenario di applicazione a 2 livelli in una distribuzione di Gestione risorse](virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="7b3ed-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span></span>
* <span data-ttu-id="7b3ed-184">Distribuire [Macchine virtuali MultiNIC in uno scenario di applicazione a 2 livelli in una distribuzione classica](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="7b3ed-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span></span>


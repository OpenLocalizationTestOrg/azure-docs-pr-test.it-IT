---
title: "una macchina virtuale (versione classica) con più schede di rete con PowerShell aaaCreate | Documenti Microsoft"
description: "Informazioni su come toocreate e configurare macchine virtuali con più schede di rete con PowerShell."
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
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a><span data-ttu-id="4c25a-103">Creare una VM (classica) con più schede di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="4c25a-103">Create a VM (Classic) with multiple NICs</span></span>
<span data-ttu-id="4c25a-104">È possibile creare macchine virtuali (VM) in Azure e collegare più tooeach (NIC) di interfacce di rete delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4c25a-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="4c25a-105">L'uso di più schede di interfaccia di rete è un requisito per molti dispositivi virtuali di rete, ad esempio le soluzioni di ottimizzazione WAN e la distribuzione di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="4c25a-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span> <span data-ttu-id="4c25a-106">Più schede di interfaccia di rete forniscono anche l'isolamento del traffico tra le schede.</span><span class="sxs-lookup"><span data-stu-id="4c25a-106">Multiple NICs also provide isolation of traffic between NICs.</span></span>

![Più NIC per la macchina virtuale](./media/virtual-networks-multiple-nics/IC757773.png)

<span data-ttu-id="4c25a-108">Hello illustrata nella figura una macchina virtuale con tre schede di rete, ciascuno connesso tooa diverse subnet.</span><span class="sxs-lookup"><span data-stu-id="4c25a-108">hello figure shows a VM with three NICs, each connected tooa different subnet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4c25a-109">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4c25a-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4c25a-110">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="4c25a-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="4c25a-111">Microsoft consiglia di usare Resource Manager per la maggior parte delle distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="4c25a-111">Microsoft recommends that most new deployments use Resource Manager.</span></span>

* <span data-ttu-id="4c25a-112">VIP con connessione Internet (distribuzioni classiche) è supportato solo nella scheda di rete. "predefinita" hello</span><span class="sxs-lookup"><span data-stu-id="4c25a-112">Internet-facing VIP (classic deployments) is only supported on hello "default" NIC.</span></span> <span data-ttu-id="4c25a-113">È presente un solo indirizzo VIP toohello IP della scheda di rete predefinito. hello</span><span class="sxs-lookup"><span data-stu-id="4c25a-113">There is only one VIP toohello IP of hello default NIC.</span></span>
* <span data-ttu-id="4c25a-114">Attualmente, gli indirizzi IP pubblici a livello di istanza (LPIP) (distribuzioni classiche) non sono supportati per le macchine virtuali a più NIC.</span><span class="sxs-lookup"><span data-stu-id="4c25a-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span></span>
* <span data-ttu-id="4c25a-115">ordine delle schede NIC hello da Hello all'interno di hello macchina virtuale sarà casuale e potrebbe anche cambiare tra gli aggiornamenti dell'infrastruttura di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c25a-115">hello order of hello NICs from inside hello VM will be random, and could also change across Azure infrastructure updates.</span></span> <span data-ttu-id="4c25a-116">Tuttavia, hello gli indirizzi IP e hello corrispondente ethernet MAC rimarranno indirizzi hello stesso.</span><span class="sxs-lookup"><span data-stu-id="4c25a-116">However, hello IP addresses, and hello corresponding ethernet MAC addresses will remain hello same.</span></span> <span data-ttu-id="4c25a-117">Si supponga ad esempio **scheda Eth1** è l'indirizzo IP 10.1.0.100 e l'indirizzo MAC 00-0D-3A-B0-39-0D; dopo l'aggiornamento dell'infrastruttura di Azure e il riavvio, potrebbe essere diventato troppo**Eth2**, ma hello IP e MAC associazione verrà rimangono hello stesso.</span><span class="sxs-lookup"><span data-stu-id="4c25a-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed too**Eth2**, but hello IP and MAC pairing will remain hello same.</span></span> <span data-ttu-id="4c25a-118">Quando un riavvio è avviato dall'utente, hello ordine NIC rimarrà hello stesso.</span><span class="sxs-lookup"><span data-stu-id="4c25a-118">When a restart is customer-initiated, hello NIC order will remain hello same.</span></span>
* <span data-ttu-id="4c25a-119">Hello indirizzo per ogni scheda di rete in ogni macchina virtuale deve trovarsi in una subnet, più schede di rete in una singola macchina virtuale è ogni possibile assegnare gli indirizzi specificati nella stessa subnet di hello.</span><span class="sxs-lookup"><span data-stu-id="4c25a-119">hello address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in hello same subnet.</span></span>
* <span data-ttu-id="4c25a-120">Hello dimensioni della macchina virtuale determina il numero di hello di schede di rete che è possibile creare per una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4c25a-120">hello VM size determines hello number of NICS that you can create for a VM.</span></span> <span data-ttu-id="4c25a-121">Hello riferimento [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM di dimensioni toodetermine articoli quante NIC supporta ogni dimensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4c25a-121">Reference hello [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles toodetermine how many NICS each VM size supports.</span></span> 

## <a name="network-security-groups-nsgs"></a><span data-ttu-id="4c25a-122">Gruppi di sicurezza di rete (NGS)</span><span class="sxs-lookup"><span data-stu-id="4c25a-122">Network Security Groups (NSGs)</span></span>
<span data-ttu-id="4c25a-123">In una distribuzione di Gestione risorse, qualsiasi NIC in una macchina virtuale può essere associata a un Gruppo di sicurezza di rete, incluse eventuali NIC in una macchina virtuale che presenta la funzionalità Multi-NIC abilitata.</span><span class="sxs-lookup"><span data-stu-id="4c25a-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span></span> <span data-ttu-id="4c25a-124">Se una scheda di rete viene assegnato un indirizzo all'interno di una subnet in cui è associato a un gruppo subnet hello, hello regole nel gruppo della subnet hello anche applicano toothat scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="4c25a-124">If a NIC is assigned an address within a subnet where hello subnet is associated with an NSG, then hello rules in hello subnet’s NSG also apply toothat NIC.</span></span> <span data-ttu-id="4c25a-125">Nella subnet di addizione tooassociating con NSGs, è anche possibile associare una scheda di rete con un gruppo.</span><span class="sxs-lookup"><span data-stu-id="4c25a-125">In addition tooassociating subnets with NSGs, you can also associate a NIC with an NSG.</span></span>

<span data-ttu-id="4c25a-126">Se una subnet è associata a un gruppo e una scheda di rete all'interno di subnet è singolarmente associata a un gruppo, le regole NSG hello associata vengono applicate **flusso ordine** in base toohello direzione del traffico hello passato interna o esterna Hello scheda di rete:</span><span class="sxs-lookup"><span data-stu-id="4c25a-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, hello associated NSG rules are applied in **flow order** according toohello direction of hello traffic being passed into or out of hello NIC:</span></span>

* <span data-ttu-id="4c25a-127">**Il traffico in ingresso** la cui destinazione è hello NIC in questione passano innanzitutto attraverso subnet hello, attivare le regole di NSG della subnet hello, prima di passare in hello NIC, quindi attivare le regole di NSG hello NIC.</span><span class="sxs-lookup"><span data-stu-id="4c25a-127">**Incoming traffic** whose destination is hello NIC in question flows first through hello subnet, triggering hello subnet’s NSG rules, before passing into hello NIC, then triggering hello NIC’s NSG rules.</span></span>
* <span data-ttu-id="4c25a-128">**Il traffico in uscita** la cui origine è hello NIC in questione flussi prima fuori dalla scheda di rete, attivare le regole di NSG hello NIC, prima di attraversamento subnet hello, quindi attivare le regole di NSG della subnet hello hello.</span><span class="sxs-lookup"><span data-stu-id="4c25a-128">**Outgoing traffic** whose source is hello NIC in question flows first out from hello NIC, triggering hello NIC’s NSG rules, before passing through hello subnet, then triggering hello subnet’s NSG rules.</span></span>

<span data-ttu-id="4c25a-129">Altre informazioni, vedere [gruppi di sicurezza di rete](virtual-networks-nsg.md) e come vengono applicate in base alle associazioni toosubnets, le macchine virtuali e schede di rete...</span><span class="sxs-lookup"><span data-stu-id="4c25a-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations toosubnets, VMs, and NICs..</span></span>

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a><span data-ttu-id="4c25a-130">Come tooConfigure un più NIC VM in una distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="4c25a-130">How tooConfigure a multi NIC VM in a classic deployment</span></span>
<span data-ttu-id="4c25a-131">Hello istruzioni seguenti consentono di creare una VM NIC contenente 3 schede di rete multi: una scheda di rete predefinita e due schede aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="4c25a-131">hello instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span></span> <span data-ttu-id="4c25a-132">passaggi di configurazione Hello verranno creata una macchina virtuale che verrà configurata in base toohello servizio configurazione frammento del file seguente:</span><span class="sxs-lookup"><span data-stu-id="4c25a-132">hello configuration steps will create a VM that will be configured according toohello service configuration file fragment below:</span></span>

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
    … Skip over hello remainder section …
    </VirtualNetworkSite>


<span data-ttu-id="4c25a-133">È necessario hello seguenti prerequisiti prima di tentare di comandi di PowerShell hello toorun nell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="4c25a-133">You need hello following prerequisites before trying toorun hello PowerShell commands in hello example.</span></span>

* <span data-ttu-id="4c25a-134">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c25a-134">An Azure subscription.</span></span>
* <span data-ttu-id="4c25a-135">Una rete virtuale configurata.</span><span class="sxs-lookup"><span data-stu-id="4c25a-135">A configured virtual network.</span></span> <span data-ttu-id="4c25a-136">Per altre informazioni sulle reti virtuali, vedere [Panoramica di Rete virtuale](virtual-networks-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="4c25a-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span></span>
* <span data-ttu-id="4c25a-137">versione più recente di Hello di Azure PowerShell scaricato e installato.</span><span class="sxs-lookup"><span data-stu-id="4c25a-137">hello latest version of Azure PowerShell downloaded and installed.</span></span> <span data-ttu-id="4c25a-138">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4c25a-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="4c25a-139">toocreate una macchina virtuale con più schede di rete, hello completa immettendo ogni comando in una singola sessione di PowerShell come segue:</span><span class="sxs-lookup"><span data-stu-id="4c25a-139">toocreate a VM with multiple NICs, complete hello following steps by entering each command within a single PowerShell session:</span></span>

1. <span data-ttu-id="4c25a-140">Selezionare un'immagine di macchina virtuale dalla raccolta immagini della macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c25a-140">Select a VM image from Azure VM image gallery.</span></span> <span data-ttu-id="4c25a-141">Le immagini cambiano frequentemente e sono disponibili per area geografica.</span><span class="sxs-lookup"><span data-stu-id="4c25a-141">Note that images change frequently and are available by region.</span></span> <span data-ttu-id="4c25a-142">Hello immagine specificata nel seguente esempio hello può modificare o potrebbe non essere disponibile nell'area, pertanto è necessario assicurarsi immagine hello toospecify necessaria.</span><span class="sxs-lookup"><span data-stu-id="4c25a-142">hello image specified in hello example below may change or might not be in your region, so be sure toospecify hello image you need.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. <span data-ttu-id="4c25a-143">Creare una configurazione di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4c25a-143">Create a VM configuration.</span></span>

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. <span data-ttu-id="4c25a-144">Creare account di accesso amministratore predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="4c25a-144">Create hello default administrator login.</span></span>

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. <span data-ttu-id="4c25a-145">Aggiungere una configurazione della macchina virtuale toohello schede aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="4c25a-145">Add additional NICs toohello VM configuration.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. <span data-ttu-id="4c25a-146">Specificare l'indirizzo IP e subnet di hello per hello scheda NIC del valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="4c25a-146">Specify hello subnet and IP address for hello default NIC.</span></span>

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. <span data-ttu-id="4c25a-147">Creare hello VM nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4c25a-147">Create hello VM in your virtual network.</span></span>

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > <span data-ttu-id="4c25a-148">rete virtuale che è possibile specificare Hello deve già esistere (come indicato nei prerequisiti hello).</span><span class="sxs-lookup"><span data-stu-id="4c25a-148">hello VNet that you specify here must already exist (as mentioned in hello prerequisites).</span></span> <span data-ttu-id="4c25a-149">esempio Hello seguente specifica una rete virtuale denominata **multi-VNet**.</span><span class="sxs-lookup"><span data-stu-id="4c25a-149">hello example below specifies a virtual network named **MultiNIC-VNet**.</span></span>
    >

## <a name="limitations"></a><span data-ttu-id="4c25a-150">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="4c25a-150">Limitations</span></span>
<span data-ttu-id="4c25a-151">Hello limitazioni seguenti sono applicabile quando si utilizzano più schede di rete:</span><span class="sxs-lookup"><span data-stu-id="4c25a-151">hello following limitations are applicable when using multiple NICs:</span></span>

* <span data-ttu-id="4c25a-152">È necessario creare VM con più schede di interfaccia di rete nelle reti virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c25a-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span></span> <span data-ttu-id="4c25a-153">Non è possibile configurare VM che non si trovano in reti virtuali con più schede di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="4c25a-153">Non-VNet VMs cannot be configured with multiple NICs.</span></span>
* <span data-ttu-id="4c25a-154">Tutte le macchine virtuali in un disponibilità impostare toouse necessità più schede di rete o una singola scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="4c25a-154">All VMs in an availability set need toouse either multiple NICs or a single NIC.</span></span> <span data-ttu-id="4c25a-155">Non è possibile combinare VM con più schede di interfaccia di rete e VM con una singola scheda di interfaccia di rete all'interno di un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="4c25a-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span></span> <span data-ttu-id="4c25a-156">Le stesse regole sono valide per le VM in un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="4c25a-156">Same rules apply for VMs in a cloud service.</span></span> <span data-ttu-id="4c25a-157">Per più macchine virtuali, NIC non sono necessari toohave hello stesso numero di schede di rete, purché ognuna di esse presenta almeno due.</span><span class="sxs-lookup"><span data-stu-id="4c25a-157">For multiple NIC VMs, they aren't required toohave hello same number of NICs, as long as they each have at least two.</span></span>
* <span data-ttu-id="4c25a-158">Non è possibile configurare una VM con una singola scheda di interfaccia di rete con più schede di interfaccia di rete (e viceversa) dopo la distribuzione, senza eliminarla e crearla di nuovo.</span><span class="sxs-lookup"><span data-stu-id="4c25a-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span></span>

## <a name="secondary-nics-access-tooother-subnets"></a><span data-ttu-id="4c25a-159">Schede di rete secondarie accedere tooother subnet</span><span class="sxs-lookup"><span data-stu-id="4c25a-159">Secondary NICs access tooother subnets</span></span>
<span data-ttu-id="4c25a-160">Per impostazione predefinita secondaria NIC non verranno configurate con un gateway predefinito, a causa di flusso del traffico toowhich hello in hello NIC secondaria sarà limitato toobe all'interno di hello stessa subnet.</span><span class="sxs-lookup"><span data-stu-id="4c25a-160">By default secondary NICs will not be configured with a default gateway, due toowhich hello traffic flow on hello secondary NICs will be limited toobe within hello same subnet.</span></span> <span data-ttu-id="4c25a-161">Se gli utenti di hello desiderano tooenable secondario NIC tootalk esterno le proprie subnet, sarà necessario tooadd una voce in hello tabella tooconfigure hello gateway di routing come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="4c25a-161">If hello users want tooenable secondary NICs tootalk outside their own subnet, they will need tooadd an entry in hello routing table tooconfigure hello gateway as described below.</span></span>

> [!NOTE]
> <span data-ttu-id="4c25a-162">Le VM create prima di luglio 2015 potrebbero avere un gateway predefinito configurato per tutte le NIC.</span><span class="sxs-lookup"><span data-stu-id="4c25a-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span></span> <span data-ttu-id="4c25a-163">gateway predefinito Hello per le schede NIC secondario non verrà rimosso fino a quando non vengono riavviate queste macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4c25a-163">hello default gateway for secondary NICs will not be removed until these VMs are rebooted.</span></span> <span data-ttu-id="4c25a-164">In sistemi operativi che utilizzano un modello di host vulnerabile routing hello, ad esempio Linux, è possibile interrompere la connettività a Internet se il traffico in ingresso e uscita hello Usa diverse schede di rete.</span><span class="sxs-lookup"><span data-stu-id="4c25a-164">In Operating systems that use hello weak host routing model, such as Linux, Internet connectivity can break if hello ingress and egress traffic use different NICs.</span></span>
> 

### <a name="configure-windows-vms"></a><span data-ttu-id="4c25a-165">Configurare le macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="4c25a-165">Configure Windows VMs</span></span>
<span data-ttu-id="4c25a-166">Supponiamo di utilizzare una macchina virtuale di Windows con due NIC come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="4c25a-166">Suppose that you have a Windows VM with two NICs as follows:</span></span>

* <span data-ttu-id="4c25a-167">Indirizzo IP primario della NIC: 192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="4c25a-167">Primary NIC IP address: 192.168.1.4</span></span>
* <span data-ttu-id="4c25a-168">Indirizzo IP secondario della NIC: 192.168.2.5</span><span class="sxs-lookup"><span data-stu-id="4c25a-168">Secondary NIC IP address: 192.168.2.5</span></span>

<span data-ttu-id="4c25a-169">tabella di routing IPv4 Hello per questa macchina virtuale sarebbe simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4c25a-169">hello IPv4 route table for this VM would look like this:</span></span>

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

<span data-ttu-id="4c25a-170">Route predefinita (0.0.0.0) hello è solo toohello disponibili primario scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="4c25a-170">Notice that hello default route (0.0.0.0) is only available toohello primary NIC.</span></span> <span data-ttu-id="4c25a-171">Non sarà tooaccess in grado di risorse esterno hello subnet per hello secondario NIC, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="4c25a-171">You will not be able tooaccess resources outside hello subnet for hello secondary NIC, as seen below:</span></span>

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

<span data-ttu-id="4c25a-172">tooadd predefinito instradare sulla hello secondario NIC, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="4c25a-172">tooadd a default route on hello secondary NIC, follow hello steps below:</span></span>

1. <span data-ttu-id="4c25a-173">Da un prompt dei comandi, eseguire il comando di hello sotto tooidentify hello numero di indice hello NIC secondario:</span><span class="sxs-lookup"><span data-stu-id="4c25a-173">From a command prompt, run hello command below tooidentify hello index number for hello secondary NIC:</span></span>
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. <span data-ttu-id="4c25a-174">Si noti hello seconda voce tabella hello, con un indice pari a 27 (in questo esempio).</span><span class="sxs-lookup"><span data-stu-id="4c25a-174">Notice hello second entry in hello table, with an index of 27 (in this example).</span></span>
3. <span data-ttu-id="4c25a-175">Dal prompt dei comandi di hello, eseguire hello **aggiungere route** comando come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="4c25a-175">From hello command prompt, run hello **route add** command as shown below.</span></span> <span data-ttu-id="4c25a-176">In questo esempio si specifica 192.168.2.1 come gateway predefinito hello per hello NIC secondario:</span><span class="sxs-lookup"><span data-stu-id="4c25a-176">In this example, you are specifying 192.168.2.1 as hello default gateway for hello secondary NIC:</span></span>
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. <span data-ttu-id="4c25a-177">connettività tootest, tornare indietro toohello il prompt dei comandi e provare tooping una subnet diversa da hello NIC secondario come int illustrato eh esempio riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="4c25a-177">tootest connectivity, go back toohello command prompt and try tooping a different subnet from hello secondary NIC as shown int eh example below:</span></span>
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. <span data-ttu-id="4c25a-178">È inoltre possibile verificare che il hello toocheck tabella di route appena aggiunti route, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="4c25a-178">You can also check your route table toocheck hello newly added route, as shown below:</span></span>
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a><span data-ttu-id="4c25a-179">Configurare le macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="4c25a-179">Configure Linux VMs</span></span>
<span data-ttu-id="4c25a-180">Per le macchine virtuali Linux, poiché il comportamento predefinito di hello utilizza host vulnerabile routing, è consigliabile che hello secondaria NIC sono flussi tootraffic limitato solo all'interno di hello stessa subnet.</span><span class="sxs-lookup"><span data-stu-id="4c25a-180">For Linux VMs, since hello default behavior uses weak host routing, we recommend that hello secondary NICs are restricted tootraffic flows only within hello same subnet.</span></span> <span data-ttu-id="4c25a-181">Tuttavia, se alcuni scenari richiedono la connettività all'esterno di hello subnet, gli utenti devono attivare tooensure di routing basata su criteri che hello in ingresso e Usa il traffico in uscita hello stessa scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="4c25a-181">However if certain scenarios demand connectivity outside hello subnet, users should enable policy based routing tooensure that hello ingress and egress traffic uses hello same NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c25a-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4c25a-182">Next steps</span></span>
* <span data-ttu-id="4c25a-183">Distribuire [Macchine virtuali MultiNIC in uno scenario di applicazione a 2 livelli in una distribuzione di Gestione risorse](virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="4c25a-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span></span>
* <span data-ttu-id="4c25a-184">Distribuire [Macchine virtuali MultiNIC in uno scenario di applicazione a 2 livelli in una distribuzione classica](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4c25a-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span></span>


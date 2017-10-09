---
title: aaaTroubleshoot gruppi di sicurezza di rete - PowerShell | Documenti Microsoft
description: Informazioni su come gruppi di sicurezza di rete tootroubleshoot nella distribuzione di Azure Resource Manager hello del modello con Azure PowerShell.
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a><span data-ttu-id="d7e38-103">Risolvere i problemi relativi ai gruppi di sicurezza di rete tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7e38-103">Troubleshoot Network Security Groups using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d7e38-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d7e38-104">Azure Portal</span></span>](virtual-network-nsg-troubleshoot-portal.md)
> * [<span data-ttu-id="d7e38-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7e38-105">PowerShell</span></span>](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="d7e38-106">Se si sono verificati problemi di connettività di macchina virtuale configurato rete sicurezza gruppi sulla macchina virtuale (VM), in questo articolo fornisce una panoramica delle funzionalità di diagnostica per NSGs toohelp risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="d7e38-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs toohelp troubleshoot further.</span></span>

<span data-ttu-id="d7e38-107">NSGs consentono tipi hello toocontrol di traffico che il flusso da e verso le macchine virtuali (VM).</span><span class="sxs-lookup"><span data-stu-id="d7e38-107">NSGs enable you toocontrol hello types of traffic that flow in and out of your virtual machines (VMs).</span></span> <span data-ttu-id="d7e38-108">NSGs può essere applicato toosubnets in una rete virtuale di Azure (VNet), le interfacce di rete (NIC) o entrambi.</span><span class="sxs-lookup"><span data-stu-id="d7e38-108">NSGs can be applied toosubnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span></span> <span data-ttu-id="d7e38-109">Hello regole efficaci applicate tooa NIC sono un'aggregazione di regole hello esistenti hello NSGs applicato tooa NIC e hello subnet è connesso a.</span><span class="sxs-lookup"><span data-stu-id="d7e38-109">hello effective rules applied tooa NIC are an aggregation of hello rules that exist in hello NSGs applied tooa NIC and hello subnet it is connected to.</span></span> <span data-ttu-id="d7e38-110">Talvolta le regole nei gruppi di sicurezza di rete possono essere in conflitto tra loro e influire sulla connettività di rete della VM.</span><span class="sxs-lookup"><span data-stu-id="d7e38-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span></span>  

<span data-ttu-id="d7e38-111">È possibile visualizzare tutte le regole di sicurezza efficace hello dal NSGs, così come applicato nelle schede NIC della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d7e38-111">You can view all hello effective security rules from your NSGs, as applied on your VM's NICs.</span></span> <span data-ttu-id="d7e38-112">Questo articolo illustra come problemi di connettività VM tootroubleshoot usando queste regole in hello modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d7e38-112">This article shows how tootroubleshoot VM connectivity issues using these rules in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="d7e38-113">Se non si ha familiarità con i concetti di rete virtuale e di gruppo, leggere hello [rete virtuale](virtual-networks-overview.md) e [gruppi di sicurezza di rete](virtual-networks-nsg.md) articoli Panoramica.</span><span class="sxs-lookup"><span data-stu-id="d7e38-113">If you're not familiar with VNet and NSG concepts, read hello [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span></span>

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="d7e38-114">Utilizzando le regole di sicurezza efficace tootroubleshoot VM il flusso del traffico</span><span class="sxs-lookup"><span data-stu-id="d7e38-114">Using Effective Security Rules tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="d7e38-115">scenario di Hello che segue è un esempio di un problema di connessione comuni:</span><span class="sxs-lookup"><span data-stu-id="d7e38-115">hello scenario that follows is an example of a common connection problem:</span></span>

<span data-ttu-id="d7e38-116">Una macchina virtuale denominata *VM1* fa parte di una subnet denominata *Subnet1* in una rete virtuale denominata *WestUS-VNet1*.</span><span class="sxs-lookup"><span data-stu-id="d7e38-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span></span> <span data-ttu-id="d7e38-117">Un toohello tooconnect tentativo di VM che utilizzano il protocollo RDP sulla porta TCP 3389 ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="d7e38-117">An attempt tooconnect toohello VM using RDP over TCP port 3389 fails.</span></span> <span data-ttu-id="d7e38-118">NSGs vengono applicate a entrambi hello NIC *VM1 NIC1* e hello subnet *Subnet1*.</span><span class="sxs-lookup"><span data-stu-id="d7e38-118">NSGs are applied at both hello NIC *VM1-NIC1* and hello subnet *Subnet1*.</span></span> <span data-ttu-id="d7e38-119">La porta 3389 tooTCP di traffico è consentita in hello NSG associata con l'interfaccia di rete hello *VM1 NIC1*, tuttavia TCP effettuare il ping ha esito 3389 negativo di porta del tooVM1.</span><span class="sxs-lookup"><span data-stu-id="d7e38-119">Traffic tooTCP port 3389 is allowed in hello NSG associated with hello network interface *VM1-NIC1*, however TCP ping tooVM1's port 3389 fails.</span></span>

<span data-ttu-id="d7e38-120">Mentre in questo esempio viene usata la porta TCP 3389, hello i passaggi seguenti può essere utilizzati toodetermine errori di connessione in ingresso e in uscita su qualsiasi porta.</span><span class="sxs-lookup"><span data-stu-id="d7e38-120">While this example uses TCP port 3389, hello following steps can be used toodetermine inbound and outbound connection failures over any port.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="d7e38-121">Procedura di risoluzione dei problemi dettagliata</span><span class="sxs-lookup"><span data-stu-id="d7e38-121">Detailed Troubleshooting Steps</span></span>
<span data-ttu-id="d7e38-122">Completare hello seguendo i passaggi tootroubleshoot NSGs per una macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="d7e38-122">Complete hello following steps tootroubleshoot NSGs for a VM:</span></span>

1. <span data-ttu-id="d7e38-123">Avviare un tooAzure di sessione e l'account di accesso di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7e38-123">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="d7e38-124">Se non si ha familiarità con Azure PowerShell, leggere hello [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) articolo.</span><span class="sxs-lookup"><span data-stu-id="d7e38-124">If you're not familiar with using Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="d7e38-125">Immettere hello comando tooreturn tutte le regole di gruppo applicate tooa NIC denominato seguente *VM1 NIC1* nel gruppo di risorse hello *RG1*:</span><span class="sxs-lookup"><span data-stu-id="d7e38-125">Enter hello following command tooreturn all NSG rules applied tooa NIC named *VM1-NIC1* in hello resource group *RG1*:</span></span>
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="d7e38-126">Se non si conosce il nome di hello di una scheda di rete, immettere hello seguente i nomi di comando tooretrieve hello di tutte le schede di rete in un gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="d7e38-126">If you don't know hello name of a NIC, enter hello following command tooretrieve hello names of all NICs in a resource group:</span></span> 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    <span data-ttu-id="d7e38-127">testo Hello è riportato un esempio dell'output di hello regole valide per hello restituito *VM1 NIC1* NIC:</span><span class="sxs-lookup"><span data-stu-id="d7e38-127">hello following text is a sample of hello effective rules output returned for hello *VM1-NIC1* NIC:</span></span>
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    <span data-ttu-id="d7e38-128">Tenere presente le seguenti informazioni nell'output di hello hello:</span><span class="sxs-lookup"><span data-stu-id="d7e38-128">Note hello following information in hello output:</span></span>
   
   * <span data-ttu-id="d7e38-129">Esistono due sezioni in **NetworkSecurityGroup**: una è associata a una subnet (*Subnet1*), l'altra a un'interfaccia di rete (*VM1-NIC1*).</span><span class="sxs-lookup"><span data-stu-id="d7e38-129">There are two **NetworkSecurityGroup** sections: One is associated with a subnet (*Subnet1*) and one is associated with a NIC (*VM1-NIC1*).</span></span> <span data-ttu-id="d7e38-130">In questo esempio, un gruppo è stato applicato tooeach.</span><span class="sxs-lookup"><span data-stu-id="d7e38-130">In this example, an NSG has been applied tooeach.</span></span>
   * <span data-ttu-id="d7e38-131">**Associazione** Mostra risorse hello (subnet o NIC) è associata a un gruppo specificato.</span><span class="sxs-lookup"><span data-stu-id="d7e38-131">**Association** shows hello resource (subnet or NIC) a given NSG is associated with.</span></span> <span data-ttu-id="d7e38-132">Se hello risorsa gruppo spostato dissociare immediatamente prima di eseguire questo comando, si potrebbe essere necessario toowait alcuni secondi per hello modifica tooreflect nell'output del comando hello.</span><span class="sxs-lookup"><span data-stu-id="d7e38-132">If hello NSG resource is moved/disassociated immediately before running this command, you may need toowait a few seconds for hello change tooreflect in hello command output.</span></span> 
   * <span data-ttu-id="d7e38-133">i nomi delle regole che sono preceduti Hello *defaultSecurityRules*: viene creato quando di un gruppo, vengono create diverse regole di sicurezza predefinito.</span><span class="sxs-lookup"><span data-stu-id="d7e38-133">hello rule names that are prefaced with *defaultSecurityRules*: When an NSG is created, several default security rules are created within it.</span></span> <span data-ttu-id="d7e38-134">Le regole predefinite non possono essere rimosse, tuttavia possono essere sostituite con regole dalla priorità più elevata.</span><span class="sxs-lookup"><span data-stu-id="d7e38-134">Default rules can't be removed, but they can be overridden with higher priority rules.</span></span>
     <span data-ttu-id="d7e38-135">Hello lettura [Panoramica gruppo](virtual-networks-nsg.md#default-rules) toolearn articolo ulteriori informazioni su gruppo predefinito di regole di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d7e38-135">Read hello [NSG overview](virtual-networks-nsg.md#default-rules) article toolearn more about NSG default security rules.</span></span>
   * <span data-ttu-id="d7e38-136">**ExpandedAddressPrefix** espande i prefissi di indirizzo hello per tag di gruppo predefiniti.</span><span class="sxs-lookup"><span data-stu-id="d7e38-136">**ExpandedAddressPrefix** expands hello address prefixes for NSG default tags.</span></span> <span data-ttu-id="d7e38-137">I tag rappresentano più prefissi di indirizzi.</span><span class="sxs-lookup"><span data-stu-id="d7e38-137">Tags represent multiple address prefixes.</span></span> <span data-ttu-id="d7e38-138">Espansione di tag hello può essere utile quando la risoluzione dei problemi di connettività di macchina virtuale da e verso i prefissi di indirizzo specifico.</span><span class="sxs-lookup"><span data-stu-id="d7e38-138">Expansion of hello tags can be useful when troubleshooting VM connectivity to/from specific address prefixes.</span></span> <span data-ttu-id="d7e38-139">Ad esempio, con peering reti VIRTUALI, i tag VIRTUAL_NETWORK espande tooshow peering prefissi di rete virtuale nell'output precedente hello.</span><span class="sxs-lookup"><span data-stu-id="d7e38-139">For example, with VNET peering, VIRTUAL_NETWORK tag expands tooshow peered VNet prefixes in hello previous output.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="d7e38-140">Hello regole efficaci Mostra solo comando se un gruppo è associata a una subnet, una scheda di rete o entrambi.</span><span class="sxs-lookup"><span data-stu-id="d7e38-140">hello command only shows effective rules if an NSG is associated with either a subnet, a NIC, or both.</span></span> <span data-ttu-id="d7e38-141">Una VM può avere diverse interfacce di rete a cui sono applicati vari gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="d7e38-141">A VM may have multiple NICs with different NSGs applied.</span></span> <span data-ttu-id="d7e38-142">Per risolvere il problema, eseguire il comando di hello per ogni scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="d7e38-142">When troubleshooting, run hello command for each NIC.</span></span>
     > 
     > 
3. <span data-ttu-id="d7e38-143">tooease filtro su un numero elevato di regole di gruppo, immettere hello ulteriormente tootroubleshoot i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d7e38-143">tooease filtering over larger number of NSG rules, enter hello following commands tootroubleshoot further:</span></span> 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    <span data-ttu-id="d7e38-144">Un filtro per il traffico RDP (porta TCP 3389), viene applicato toohello visualizzazione griglia, come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="d7e38-144">A filter for RDP traffic (TCP port 3389), is applied toohello grid view, as shown in hello following picture:</span></span>
   
    ![Elenco di regole](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. <span data-ttu-id="d7e38-146">Come può vedere nella visualizzazione griglia hello, sono presenti entrambi consentono e le regole di negazione per RDP.</span><span class="sxs-lookup"><span data-stu-id="d7e38-146">As you can see in hello grid view, there are both allow and deny rules for RDP.</span></span> <span data-ttu-id="d7e38-147">Hello passaggio 2 Mostra output di hello *DenyRDP* regola è nella subnet toohello NSG applicato hello.</span><span class="sxs-lookup"><span data-stu-id="d7e38-147">hello output from step 2 shows that hello *DenyRDP* rule is in hello NSG applied toohello subnet.</span></span> <span data-ttu-id="d7e38-148">Per le regole in entrata, vengono prima elaborate subnet toohello NSGs applicato.</span><span class="sxs-lookup"><span data-stu-id="d7e38-148">For inbound rules, NSGs applied toohello subnet are processed first.</span></span> <span data-ttu-id="d7e38-149">Se viene trovata una corrispondenza, l'interfaccia di rete hello NSG applicato toohello non elaborato.</span><span class="sxs-lookup"><span data-stu-id="d7e38-149">If a match is found, hello NSG applied toohello network interface is not processed.</span></span> <span data-ttu-id="d7e38-150">In questo caso, hello *DenyRDP* regola dalla subnet hello Blocca RDP toohello VM (**VM1**).</span><span class="sxs-lookup"><span data-stu-id="d7e38-150">In this case, hello *DenyRDP* rule from hello subnet blocks RDP toohello VM (**VM1**).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d7e38-151">Una macchina virtuale può avere più tooit collegato a schede di rete.</span><span class="sxs-lookup"><span data-stu-id="d7e38-151">A VM may have multiple NICs attached tooit.</span></span> <span data-ttu-id="d7e38-152">Ognuno può essere connesso tooa diverse subnet.</span><span class="sxs-lookup"><span data-stu-id="d7e38-152">Each may be connected tooa different subnet.</span></span> <span data-ttu-id="d7e38-153">Poiché i comandi di hello nei passaggi precedenti hello vengono eseguiti su una scheda di rete, è importante tooensure specificato hello NIC si verificano errori di connettività hello per.</span><span class="sxs-lookup"><span data-stu-id="d7e38-153">Since hello commands in hello previous steps are run against a NIC, it's important tooensure that you specify hello NIC you're having hello connectivity failure to.</span></span> <span data-ttu-id="d7e38-154">Se non si è certi, è sempre possibile eseguire i comandi di hello in ogni macchina virtuale di toohello NIC associata.</span><span class="sxs-lookup"><span data-stu-id="d7e38-154">If you're not sure, you can always run hello commands against each NIC attached toohello VM.</span></span>
   > 
   > 
5. <span data-ttu-id="d7e38-155">tooRDP in VM1, hello modifica *negare RDP (3389)* regola troppo*consentire RDP(3389)* in hello **Subnet1 NSG** gruppo.</span><span class="sxs-lookup"><span data-stu-id="d7e38-155">tooRDP into VM1, change hello *Deny RDP (3389)* rule too*Allow RDP(3389)* in hello **Subnet1-NSG** NSG.</span></span> <span data-ttu-id="d7e38-156">Verificare che la porta TCP 3389 sia aperta aprendo un toohello connessione RDP macchina virtuale o lo strumento PsPing hello.</span><span class="sxs-lookup"><span data-stu-id="d7e38-156">Confirm that TCP port 3389 is open by opening an RDP connection toohello VM or using hello PsPing tool.</span></span> <span data-ttu-id="d7e38-157">È possibile approfondire PsPing da lettura hello [PsPing pagina di download](https://technet.microsoft.com/sysinternals/psping.aspx)</span><span class="sxs-lookup"><span data-stu-id="d7e38-157">You can learn more about PsPing by reading hello [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx)</span></span>
   
    <span data-ttu-id="d7e38-158">È possibile o rimuovere le regole da un gruppo usando hello informazioni nell'output di hello dalla hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d7e38-158">You can or remove rules from an NSG by using hello information in hello output from hello following command:</span></span>
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a><span data-ttu-id="d7e38-159">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="d7e38-159">Considerations</span></span>
<span data-ttu-id="d7e38-160">Prendere in considerazione hello seguenti punti durante la risoluzione dei problemi di connettività:</span><span class="sxs-lookup"><span data-stu-id="d7e38-160">Consider hello following points when troubleshooting connectivity problems:</span></span>

* <span data-ttu-id="d7e38-161">Regole predefinite di NSG bloccherà l'accesso in ingresso da hello internet e solo Consenti rete virtuale il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="d7e38-161">Default NSG rules will block inbound access from hello internet and only permit VNet inbound traffic.</span></span> <span data-ttu-id="d7e38-162">Le regole devono essere aggiunto esplicitamente tooallow accesso in entrata da Internet, come richiesto.</span><span class="sxs-lookup"><span data-stu-id="d7e38-162">Rules should be explicitly added tooallow inbound access from Internet, as required.</span></span>
* <span data-ttu-id="d7e38-163">Se non sono presenti regole di sicurezza gruppo causando toofail connettività di rete della macchina virtuale, problema di hello può essere dovuto a:</span><span class="sxs-lookup"><span data-stu-id="d7e38-163">If there are no NSG security rules causing a VM’s network connectivity toofail, hello problem may be due to:</span></span>
  * <span data-ttu-id="d7e38-164">Software di firewall in esecuzione all'interno del sistema operativo della macchina virtuale di hello</span><span class="sxs-lookup"><span data-stu-id="d7e38-164">Firewall software running within hello VM's operating system</span></span>
  * <span data-ttu-id="d7e38-165">Route configurate per appliance virtuali o traffico locale.</span><span class="sxs-lookup"><span data-stu-id="d7e38-165">Routes configured for virtual appliances or on-premises traffic.</span></span> <span data-ttu-id="d7e38-166">Il traffico Internet può essere reindirizzati tooon locali tramite il tunneling forzato.</span><span class="sxs-lookup"><span data-stu-id="d7e38-166">Internet traffic can be redirected tooon-premises via forced-tunneling.</span></span> <span data-ttu-id="d7e38-167">Una connessione RDP/SSH da hello Internet tooyour macchina virtuale potrebbe non funzionare con questa impostazione, a seconda di come hardware di rete locale hello gestisce tale traffico.</span><span class="sxs-lookup"><span data-stu-id="d7e38-167">An RDP/SSH connection from hello Internet tooyour VM may not work with this setting, depending on how hello on-premises network hardware handles this traffic.</span></span> <span data-ttu-id="d7e38-168">Hello lettura [risoluzione dei problemi delle route](virtual-network-routes-troubleshoot-powershell.md) toolearn articolo come problemi di route toodiagnose che potrebbero ostacolare hello flusso del traffico in e out di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d7e38-168">Read hello [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article toolearn how toodiagnose route problems that may be impeding hello flow of traffic in and out of hello VM.</span></span> 
* <span data-ttu-id="d7e38-169">Se si dispongano di peering reti virtuali, per impostazione predefinita, hello tag VIRTUAL_NETWORK espanderà automaticamente i prefissi tooinclude per il peering reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="d7e38-169">If you have peered VNets, by default, hello VIRTUAL_NETWORK tag will automatically expand tooinclude prefixes for peered VNets.</span></span> <span data-ttu-id="d7e38-170">È possibile visualizzare tali prefissi nella hello **ExpandedAddressPrefix** elencare, tootroubleshoot qualsiasi tooVNet correlate a problemi peering di connettività.</span><span class="sxs-lookup"><span data-stu-id="d7e38-170">You can view these prefixes in hello **ExpandedAddressPrefix** list, tootroubleshoot any issues related tooVNet peering connectivity.</span></span> 
* <span data-ttu-id="d7e38-171">Le regole di sicurezza efficace vengono visualizzate solo se è che un gruppo associato della macchina virtuale di hello NIC e o una subnet.</span><span class="sxs-lookup"><span data-stu-id="d7e38-171">Effective security rules are only shown if there is an NSG associated with hello VM’s NIC and or subnet.</span></span> 
* <span data-ttu-id="d7e38-172">Se non sono non NSGs associato hello NIC o subnet e si dispone di un indirizzo IP pubblico assegnato tooyour VM, tutte le porte sarà aperte per l'accesso in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="d7e38-172">If there are no NSGs associated with hello NIC or subnet and you have a public IP address assigned tooyour VM, all ports will be open for inbound and outbound access.</span></span> <span data-ttu-id="d7e38-173">Se hello macchina virtuale ha un indirizzo IP pubblico, l'applicazione NSGs toohello NIC o una subnet è consigliabile.</span><span class="sxs-lookup"><span data-stu-id="d7e38-173">If hello VM has a public IP address, applying NSGs toohello NIC or subnet is strongly recommended.</span></span>  


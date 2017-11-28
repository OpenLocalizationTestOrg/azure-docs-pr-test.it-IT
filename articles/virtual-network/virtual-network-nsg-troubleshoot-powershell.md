---
title: Risolvere i problemi relativi ai gruppi di sicurezza di rete - PowerShell | Documentazione Microsoft
description: Informazioni su come risolvere i problemi dei gruppi di sicurezza di rete nel modello di distribuzione Azure Resource Manager con Azure PowerShell.
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
ms.openlocfilehash: 5edaf7197576ac1c0bd1fc6bed21fd65ed135106
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a><span data-ttu-id="a7a9a-103">Risolvere i problemi relativi ai gruppi di sicurezza di rete tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7a9a-103">Troubleshoot Network Security Groups using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a7a9a-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a7a9a-104">Azure Portal</span></span>](virtual-network-nsg-troubleshoot-portal.md)
> * [<span data-ttu-id="a7a9a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7a9a-105">PowerShell</span></span>](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="a7a9a-106">Se sono stati configurati gruppi di sicurezza di rete nella macchina virtuale (VM) e si verificano problemi di connettività alla VM, questo articolo offre una panoramica delle funzionalità di diagnostica per i gruppi di sicurezza di rete per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs to help troubleshoot further.</span></span>

<span data-ttu-id="a7a9a-107">I gruppi di sicurezza di rete consentono di controllare i tipi di traffico che scorrono dentro e fuori le macchine virtuali (VM).</span><span class="sxs-lookup"><span data-stu-id="a7a9a-107">NSGs enable you to control the types of traffic that flow in and out of your virtual machines (VMs).</span></span> <span data-ttu-id="a7a9a-108">I gruppi di sicurezza di rete possono essere applicati alle subnet in una rete virtuale di Azure, nelle interfacce di rete o in entrambe.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-108">NSGs can be applied to subnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span></span> <span data-ttu-id="a7a9a-109">Le regole effettive applicate a un'interfaccia di rete (NIC) sono un'aggregazione delle regole esistenti nei gruppi di sicurezza di rete applicati a un'interfaccia di rete e alla subnet a cui è connessa.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-109">The effective rules applied to a NIC are an aggregation of the rules that exist in the NSGs applied to a NIC and the subnet it is connected to.</span></span> <span data-ttu-id="a7a9a-110">Talvolta le regole nei gruppi di sicurezza di rete possono essere in conflitto tra loro e influire sulla connettività di rete della VM.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span></span>  

<span data-ttu-id="a7a9a-111">È possibile visualizzare tutte le regole di sicurezza effettive dai gruppi di sicurezza di rete, così come vengono applicate nelle interfacce di rete della VM.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-111">You can view all the effective security rules from your NSGs, as applied on your VM's NICs.</span></span> <span data-ttu-id="a7a9a-112">Questo articolo illustra come risolvere i problemi di connettività delle VM usando queste regole nel modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-112">This article shows how to troubleshoot VM connectivity issues using these rules in the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="a7a9a-113">Se si ha scarsa dimestichezza con i concetti di rete virtuale e gruppo di sicurezza di rete, vedere gli articoli generali sulle [reti virtuali](virtual-networks-overview.md) e sui [gruppi di sicurezza di rete](virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="a7a9a-113">If you're not familiar with VNet and NSG concepts, read the [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span></span>

## <a name="using-effective-security-rules-to-troubleshoot-vm-traffic-flow"></a><span data-ttu-id="a7a9a-114">Uso di regole di sicurezza effettive per risolvere i problemi di flusso del traffico delle VM</span><span class="sxs-lookup"><span data-stu-id="a7a9a-114">Using Effective Security Rules to troubleshoot VM traffic flow</span></span>
<span data-ttu-id="a7a9a-115">Lo scenario seguente è un esempio di un problema di connessione comune:</span><span class="sxs-lookup"><span data-stu-id="a7a9a-115">The scenario that follows is an example of a common connection problem:</span></span>

<span data-ttu-id="a7a9a-116">Una macchina virtuale denominata *VM1* fa parte di una subnet denominata *Subnet1* in una rete virtuale denominata *WestUS-VNet1*.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span></span> <span data-ttu-id="a7a9a-117">Un tentativo di connettersi alla VM con RDP su porta TCP 3389 ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-117">An attempt to connect to the VM using RDP over TCP port 3389 fails.</span></span> <span data-ttu-id="a7a9a-118">I gruppi di sicurezza di rete vengono applicati sia all'interfaccia di rete *VM1-NIC1* che alla subnet *Subnet1*.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-118">NSGs are applied at both the NIC *VM1-NIC1* and the subnet *Subnet1*.</span></span> <span data-ttu-id="a7a9a-119">Il traffico verso la porta TCP 3389 è consentito nel gruppo di sicurezza di rete associato all'interfaccia di rete *VM1 NIC1*, tuttavia il comando ping TCP per VM1 della porta 3389 ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-119">Traffic to TCP port 3389 is allowed in the NSG associated with the network interface *VM1-NIC1*, however TCP ping to VM1's port 3389 fails.</span></span>

<span data-ttu-id="a7a9a-120">Sebbene in questo esempio si usi la porta TCP 3389, è possibile attenersi alla procedura seguente per determinare gli errori di connessione in ingresso e in uscita su qualsiasi porta.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-120">While this example uses TCP port 3389, the following steps can be used to determine inbound and outbound connection failures over any port.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="a7a9a-121">Procedura di risoluzione dei problemi dettagliata</span><span class="sxs-lookup"><span data-stu-id="a7a9a-121">Detailed Troubleshooting Steps</span></span>
<span data-ttu-id="a7a9a-122">Completare i passaggi seguenti per risolvere i problemi dei gruppi di sicurezza di rete per una VM:</span><span class="sxs-lookup"><span data-stu-id="a7a9a-122">Complete the following steps to troubleshoot NSGs for a VM:</span></span>

1. <span data-ttu-id="a7a9a-123">Avviare una sessione di Azure PowerShell e accedere ad Azure.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-123">Start an Azure PowerShell session and login to Azure.</span></span> <span data-ttu-id="a7a9a-124">Se non si ha dimestichezza con Azure PowerShell, leggere l'articolo [Come installare e configurare Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="a7a9a-124">If you're not familiar with using Azure PowerShell, read the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="a7a9a-125">Immettere il comando seguente per restituire tutte le regole dei gruppi di sicurezza di rete applicate a un'interfaccia di rete denominata *VM1 NIC1* nel gruppo di risorse *RG1*:</span><span class="sxs-lookup"><span data-stu-id="a7a9a-125">Enter the following command to return all NSG rules applied to a NIC named *VM1-NIC1* in the resource group *RG1*:</span></span>
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="a7a9a-126">Se non si conosce il nome di un'interfaccia di rete, immettere il comando seguente per recuperare i nomi di tutte le interfacce di rete in un gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="a7a9a-126">If you don't know the name of a NIC, enter the following command to retrieve the names of all NICs in a resource group:</span></span> 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    <span data-ttu-id="a7a9a-127">Il testo riportato di seguito è un esempio delle regole valide restituite per l'interfaccia di rete *VM1 NIC1* :</span><span class="sxs-lookup"><span data-stu-id="a7a9a-127">The following text is a sample of the effective rules output returned for the *VM1-NIC1* NIC:</span></span>
   
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
   
    <span data-ttu-id="a7a9a-128">Tenere presenti le seguenti informazioni nell'output:</span><span class="sxs-lookup"><span data-stu-id="a7a9a-128">Note the following information in the output:</span></span>
   
   * <span data-ttu-id="a7a9a-129">Esistono due sezioni in **NetworkSecurityGroup**: una è associata a una subnet (*Subnet1*), l'altra a un'interfaccia di rete (*VM1-NIC1*).</span><span class="sxs-lookup"><span data-stu-id="a7a9a-129">There are two **NetworkSecurityGroup** sections: One is associated with a subnet (*Subnet1*) and one is associated with a NIC (*VM1-NIC1*).</span></span> <span data-ttu-id="a7a9a-130">In questo esempio, è stato applicato un gruppo di sicurezza di rete a ciascuna.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-130">In this example, an NSG has been applied to each.</span></span>
   * <span data-ttu-id="a7a9a-131">**Associazione** mostra la risorsa (subnet o interfaccia di rete) a cui è associato un determinato gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-131">**Association** shows the resource (subnet or NIC) a given NSG is associated with.</span></span> <span data-ttu-id="a7a9a-132">Se la risorsa del gruppo di sicurezza di rete viene spostata oppure se viene eliminata la sua associazione appena prima di eseguire il comando, potrebbe essere necessario attendere qualche secondo prima che la modifica sia effettiva nell'output del comando.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-132">If the NSG resource is moved/disassociated immediately before running this command, you may need to wait a few seconds for the change to reflect in the command output.</span></span> 
   * <span data-ttu-id="a7a9a-133">I nomi delle regole precedute da *defaultSecurityRules*: quando viene creato un gruppo di risorse di rete, vengono create varie regole predefinite al suo interno.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-133">The rule names that are prefaced with *defaultSecurityRules*: When an NSG is created, several default security rules are created within it.</span></span> <span data-ttu-id="a7a9a-134">Le regole predefinite non possono essere rimosse, tuttavia possono essere sostituite con regole dalla priorità più elevata.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-134">Default rules can't be removed, but they can be overridden with higher priority rules.</span></span>
     <span data-ttu-id="a7a9a-135">Per ulteriori informazioni sulle regole di sicurezza predefinite dei gruppi di sicurezza di rete, leggere l'articolo [Panoramica dei gruppi di sicurezza di rete](virtual-networks-nsg.md#default-rules) .</span><span class="sxs-lookup"><span data-stu-id="a7a9a-135">Read the [NSG overview](virtual-networks-nsg.md#default-rules) article to learn more about NSG default security rules.</span></span>
   * <span data-ttu-id="a7a9a-136">**ExpandedAddressPrefix** espande i prefissi degli indirizzi per i tag predefiniti dei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-136">**ExpandedAddressPrefix** expands the address prefixes for NSG default tags.</span></span> <span data-ttu-id="a7a9a-137">I tag rappresentano più prefissi di indirizzi.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-137">Tags represent multiple address prefixes.</span></span> <span data-ttu-id="a7a9a-138">L'espansione dei tag può essere utile per la risoluzione dei problemi di connettività delle VM da e verso prefissi di indirizzi specifici.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-138">Expansion of the tags can be useful when troubleshooting VM connectivity to/from specific address prefixes.</span></span> <span data-ttu-id="a7a9a-139">Ad esempio, con il peering reti virtuali, il tag VIRTUAL_NETWORK viene espanso per visualizzare i prefissi delle reti virtuali con peering nell'output precedente.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-139">For example, with VNET peering, VIRTUAL_NETWORK tag expands to show peered VNet prefixes in the previous output.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="a7a9a-140">Il comando mostra regole efficaci solo se un gruppo di sicurezza di rete è associato a una subnet, a un'interfaccia di rete o a entrambe.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-140">The command only shows effective rules if an NSG is associated with either a subnet, a NIC, or both.</span></span> <span data-ttu-id="a7a9a-141">Una VM può avere diverse interfacce di rete a cui sono applicati vari gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-141">A VM may have multiple NICs with different NSGs applied.</span></span> <span data-ttu-id="a7a9a-142">Per risolvere il problema, eseguire il comando per ogni interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-142">When troubleshooting, run the command for each NIC.</span></span>
     > 
     > 
3. <span data-ttu-id="a7a9a-143">Per semplificare l'applicazione di filtri a grandi quantità di regole per i gruppi di sicurezza di rete, immettere i seguenti comandi per risolvere il problema:</span><span class="sxs-lookup"><span data-stu-id="a7a9a-143">To ease filtering over larger number of NSG rules, enter the following commands to troubleshoot further:</span></span> 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    <span data-ttu-id="a7a9a-144">Viene applicato un filtro per il traffico RDP (porta TCP 3389) alla visualizzazione griglia, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="a7a9a-144">A filter for RDP traffic (TCP port 3389), is applied to the grid view, as shown in the following picture:</span></span>
   
    ![Elenco di regole](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. <span data-ttu-id="a7a9a-146">Come si può vedere, sono presenti regole sia di tipo "allow" che di tipo "deny" per RDP.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-146">As you can see in the grid view, there are both allow and deny rules for RDP.</span></span> <span data-ttu-id="a7a9a-147">L'output del passaggio 2 mostra che la regola *DenyRDP* si trova nel gruppo di sicurezza di rete applicato alla subnet.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-147">The output from step 2 shows that the *DenyRDP* rule is in the NSG applied to the subnet.</span></span> <span data-ttu-id="a7a9a-148">Per le regole in entrata, vengono elaborati per primi i gruppi di sicurezza di rete applicati alla subnet.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-148">For inbound rules, NSGs applied to the subnet are processed first.</span></span> <span data-ttu-id="a7a9a-149">Se viene trovata una corrispondenza, il gruppo di sicurezza di rete applicato all'interfaccia di rete non viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-149">If a match is found, the NSG applied to the network interface is not processed.</span></span> <span data-ttu-id="a7a9a-150">In questo caso, la regola *DenyRDP* della subnet blocca RDP verso la VM (**VM1**).</span><span class="sxs-lookup"><span data-stu-id="a7a9a-150">In this case, the *DenyRDP* rule from the subnet blocks RDP to the VM (**VM1**).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a7a9a-151">A una VM potrebbero essere collegate più interfacce di rete.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-151">A VM may have multiple NICs attached to it.</span></span> <span data-ttu-id="a7a9a-152">Ognuna può essere collegata a una subnet diversa.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-152">Each may be connected to a different subnet.</span></span> <span data-ttu-id="a7a9a-153">Dal momento che i comandi nei passaggi precedenti vengono eseguiti su un'interfaccia di rete, è importante assicurarsi di specificare l'interfaccia di rete su cui si verifica l'errore di connettività.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-153">Since the commands in the previous steps are run against a NIC, it's important to ensure that you specify the NIC you're having the connectivity failure to.</span></span> <span data-ttu-id="a7a9a-154">Se non si è certi, è sempre possibile eseguire i comandi su ogni interfaccia di rete collegata alla VM.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-154">If you're not sure, you can always run the commands against each NIC attached to the VM.</span></span>
   > 
   > 
5. <span data-ttu-id="a7a9a-155">Per effettuare una connessione RDP a VM1, modificare la regola *Deny RDP (3389)* in *Allow RDP(3389)* nel gruppo di sicurezza di rete **Subnet1-NSG**.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-155">To RDP into VM1, change the *Deny RDP (3389)* rule to *Allow RDP(3389)* in the **Subnet1-NSG** NSG.</span></span> <span data-ttu-id="a7a9a-156">Verificare che la porta TCP 3389 sia aperta aprendo una connessione RDP alla VM o usando lo strumento PsPing.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-156">Confirm that TCP port 3389 is open by opening an RDP connection to the VM or using the PsPing tool.</span></span> <span data-ttu-id="a7a9a-157">Per trovare ulteriori informazioni su PsPing, consultare la [pagina di download di PsPing](https://technet.microsoft.com/sysinternals/psping.aspx)</span><span class="sxs-lookup"><span data-stu-id="a7a9a-157">You can learn more about PsPing by reading the [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx)</span></span>
   
    <span data-ttu-id="a7a9a-158">È possibile rimuovere le regole da un gruppo di sicurezza di rete usando le informazioni nell'output dal seguente comando:</span><span class="sxs-lookup"><span data-stu-id="a7a9a-158">You can or remove rules from an NSG by using the information in the output from the following command:</span></span>
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a><span data-ttu-id="a7a9a-159">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="a7a9a-159">Considerations</span></span>
<span data-ttu-id="a7a9a-160">Durante la risoluzione dei problemi di connettività, tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="a7a9a-160">Consider the following points when troubleshooting connectivity problems:</span></span>

* <span data-ttu-id="a7a9a-161">Le regole predefinite dei gruppi di sicurezza di rete bloccano l'accesso in ingresso da Internet e consentono solo il traffico di rete in ingresso nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-161">Default NSG rules will block inbound access from the internet and only permit VNet inbound traffic.</span></span> <span data-ttu-id="a7a9a-162">È necessario aggiungere regole in modo esplicito per consentire l'accesso in ingresso da Internet, come richiesto.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-162">Rules should be explicitly added to allow inbound access from Internet, as required.</span></span>
* <span data-ttu-id="a7a9a-163">Se non sono presenti regole dei gruppi di sicurezza di rete che causano un errore di connettività della VM, il problema potrebbe essere dovuto a:</span><span class="sxs-lookup"><span data-stu-id="a7a9a-163">If there are no NSG security rules causing a VM’s network connectivity to fail, the problem may be due to:</span></span>
  * <span data-ttu-id="a7a9a-164">Software del firewall in esecuzione all'interno del sistema operativo della VM</span><span class="sxs-lookup"><span data-stu-id="a7a9a-164">Firewall software running within the VM's operating system</span></span>
  * <span data-ttu-id="a7a9a-165">Route configurate per appliance virtuali o traffico locale.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-165">Routes configured for virtual appliances or on-premises traffic.</span></span> <span data-ttu-id="a7a9a-166">Il traffico Internet può essere reindirizzato al traffico locale tramite tunneling forzato.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-166">Internet traffic can be redirected to on-premises via forced-tunneling.</span></span> <span data-ttu-id="a7a9a-167">Una connessione RDP o SSH da Internet alla VM potrebbe non funzionare con questa impostazione, a seconda di come l'hardware di rete locale gestisce questo traffico.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-167">An RDP/SSH connection from the Internet to your VM may not work with this setting, depending on how the on-premises network hardware handles this traffic.</span></span> <span data-ttu-id="a7a9a-168">Per informazioni su come diagnosticare problemi di route che potrebbero impedire il flusso del traffico in ingresso e in uscita dalla VM, vedere l'articolo [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) (Risoluzione dei problemi di route).</span><span class="sxs-lookup"><span data-stu-id="a7a9a-168">Read the [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article to learn how to diagnose route problems that may be impeding the flow of traffic in and out of the VM.</span></span> 
* <span data-ttu-id="a7a9a-169">Se si hanno reti virtuali con peering, il tag VIRTUAL_NETWORK si espanderà automaticamente per impostazione predefinita in modo da includere i prefissi delle reti virtuali con peering.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-169">If you have peered VNets, by default, the VIRTUAL_NETWORK tag will automatically expand to include prefixes for peered VNets.</span></span> <span data-ttu-id="a7a9a-170">È possibile vedere questi prefissi nell'elenco **ExpandedAddressPrefix** per risolvere eventuali problemi legati alla connettività di peering della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-170">You can view these prefixes in the **ExpandedAddressPrefix** list, to troubleshoot any issues related to VNet peering connectivity.</span></span> 
* <span data-ttu-id="a7a9a-171">Le regole di sicurezza effettive vengono visualizzate solo se c'è un gruppo di sicurezza di rete associato all'interfaccia di rete o alla subnet della VM.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-171">Effective security rules are only shown if there is an NSG associated with the VM’s NIC and or subnet.</span></span> 
* <span data-ttu-id="a7a9a-172">Se non esistono gruppi di sicurezza di rete associati all'interfaccia di rete o alla subnet e si dispone di un indirizzo IP pubblico assegnato alla VM, tutte le porte saranno aperte per l'accesso in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-172">If there are no NSGs associated with the NIC or subnet and you have a public IP address assigned to your VM, all ports will be open for inbound and outbound access.</span></span> <span data-ttu-id="a7a9a-173">Se la VM ha un indirizzo IP pubblico, è consigliabile applicare gruppi di sicurezza di rete all'interfaccia di rete o alla subnet.</span><span class="sxs-lookup"><span data-stu-id="a7a9a-173">If the VM has a public IP address, applying NSGs to the NIC or subnet is strongly recommended.</span></span>  


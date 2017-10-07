---
title: i comandi di PowerShell aaaCommon per reti virtuali di Azure | Documenti Microsoft
description: I comandi di PowerShell comuni tooget per iniziare a creare una rete virtuale e le risorse associate per le macchine virtuali.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 56e1a73c-8299-4996-bd03-f74585caa1dc
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: b46b78f1b7c5a0c5ba917fb48f568d871e5e8789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-azure-virtual-networks"></a>Comandi di rete di PowerShell comuni per le reti virtuali di Azure

Se si desidera toocreate una macchina virtuale, è necessario toocreate un [rete virtuale](../../virtual-network/virtual-networks-overview.md) o su una rete virtuale esistente in cui hello VM possono essere aggiunti. In genere, quando si crea una macchina virtuale, è anche necessario tooconsider la creazione di risorse hello descritte in questo articolo.

Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per informazioni sull'installazione hello la versione più recente di Azure PowerShell, selezionando la sottoscrizione e la firma nell'account tooyour.

Alcune variabili potrebbero essere utile se più di uno dei comandi di hello in esecuzione in questo articolo:

- $location - percorso hello hello di risorse di rete. È possibile utilizzare [Get AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind un [area geografica](https://azure.microsoft.com/regions/) che funziona automaticamente.
- $myResourceGroup - nome hello hello del gruppo di risorse in cui si trovano le risorse di rete hello.

## <a name="create-network-resources"></a>Creare risorse di rete

| Attività | Comando |
| ---- | ------- |
| Creare configurazioni subnet |$subnet1 = [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) -Name "mySubnet1" -AddressPrefix XX.X.X.X/XX<BR>$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet2" -AddressPrefix XX.X.X.X/XX<BR><BR>Una rete tipica potrebbe disporre di una subnet per un [bilanciamento del carico Internet](../../load-balancer/load-balancer-internet-overview.md) e una subnet separata per un [bilanciamento del carico interno](../../load-balancer/load-balancer-internal-overview.md). |
| Crea rete virtuale |$vnet = [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetwork) -Name "myVNet" -ResourceGroupName $myResourceGroup -Location $location -AddressPrefix XX.X.X.X/XX -Subnet $subnet1, $subnet2 |
| Test per un nome di dominio univoco |[Test-AzureRmDnsAvailability](https://docs.microsoft.com/powershell/module/azurerm.network/test-azurermdnsavailability) -DomainNameLabel "myDNS" -Location $location<BR><BR>È possibile specificare un nome di dominio DNS per un [risorsa IP pubblica](../../virtual-network/virtual-network-ip-addresses-overview-arm.md), che consente di creare un mapping per l'indirizzo IP pubblico di domainname.location.cloudapp.azure.com toohello in hello server DNS gestito di Azure. Hello nome può contenere solo lettere, numeri e trattini. Hello prima e l'ultimo carattere deve essere una lettera o un numero e il nome di dominio hello deve essere univoco nella relativa posizione di Azure. Se viene restituito **True** , il nome proposto è univoco a livello globale. |
| Creare un indirizzo IP pubblico |$pip = [New-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermpublicipaddress) -Name "myPublicIp" -ResourceGroupName $myResourceGroup -DomainNameLabel "myDNS" -Location $location -AllocationMethod Dynamic<BR><BR>indirizzo IP pubblico Hello utilizza hello nome di dominio è precedentemente testato e configurazione di hello front-end di bilanciamento del carico hello. |
| Creare la configurazione di un indirizzo IP front-end |$frontendIP = [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) -Name "myFrontendIP" -PublicIpAddress $pip<BR><BR>configurazione front-end Hello include l'indirizzo IP pubblico hello creato in precedenza per il traffico di rete in ingresso. |
| Creare un pool di indirizzi back-end |$beAddressPool = [New-AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) -Name "myBackendAddressPool"<BR><BR>Fornisce gli indirizzi interni per back-end hello di hello bilanciamento del carico che si accede tramite un'interfaccia di rete. |
| Creare un probe |$healthProbe = [New-AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) -Name "myProbe" -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2<BR><BR>Contiene l'integrità probe usati toocheck disponibilità delle istanze di macchine virtuali nel pool di indirizzi back-end hello. |
| Creare una regola di bilanciamento del carico |$lbRule = [New-AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80<BR><BR>Contiene le regole che assegnare una porta pubblica su servizio di bilanciamento del carico hello porta tooa nel pool di indirizzi back-end hello. |
| Creare una regola NAT in ingresso |$inboundNATRule = [New-AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) -Name "myInboundRule1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389<BR><BR>Contiene le regole di mapping di una porta pubblica nella porta di tooa del bilanciamento del carico hello per una macchina virtuale specifica nel pool di indirizzi back-end hello. |
| Creare un servizio di bilanciamento del carico |$loadBalancer = [New-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancer) -ResourceGroupName $myResourceGroup -Name "myLoadBalancer" -Location $location -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule -LoadBalancingRule $lbRule -BackendAddressPool $beAddressPool -Probe $healthProbe |
| Creare un'interfaccia di rete |$nic1= [New-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermnetworkinterface) -ResourceGroupName $myResourceGroup -Name "myNIC" -Location $location -PrivateIpAddress XX.X.X.X -Subnet $subnet2 -LoadBalancerBackendAddressPool $loadBalancer.BackendAddressPools[0] -LoadBalancerInboundNatRule $loadBalancer.InboundNatRules[0]<BR><BR>Creare un'interfaccia di rete con indirizzo IP pubblico hello e subnet della rete virtuale creata in precedenza. |

## <a name="get-information-about-network-resources"></a>Visualizzare le informazioni sulle risorse di rete

| Attività | Comando |
| ---- | ------- |
| Elencare le reti virtuali |[Get-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetwork) -ResourceGroupName $myResourceGroup<BR><BR>Elenca tutte le reti virtuali hello nel gruppo di risorse hello. |
| Visualizzare le informazioni su una rete virtuale |Get-AzureRmVirtualNetwork -Name "myVNet" -ResourceGroupName $myResourceGroup |
| Elencare le subnet in una rete virtuale |Get-AzureRmVirtualNetwork -Name "myVNet" -ResourceGroupName $myResourceGroup &#124; Select Subnets |
| Visualizzare le informazioni su una subnet |[Get-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) -Name "mySubnet1" -VirtualNetwork $vnet<BR><BR>Ottiene informazioni su hello subnet nella rete virtuale specificata hello. il valore di Hello $vnet rappresenta l'oggetto hello restituito da Get-AzureRmVirtualNetwork. |
| Elencare gli indirizzi IP |[Get-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermpublicipaddress) -ResourceGroupName $myResourceGroup<BR><BR>Elenca hello gli indirizzi IP pubblici nel gruppo di risorse hello. |
| Elencare i servizi di bilanciamento del carico |[Get-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermloadbalancer) -ResourceGroupName $myResourceGroup<BR><BR>Elenca tutti i bilanciamenti del carico hello nel gruppo di risorse hello. |
| Elencare le interfacce di rete |[Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterface) -ResourceGroupName $myResourceGroup<BR><BR>Elenca tutte le interfacce di rete hello nel gruppo di risorse hello. |
| Visualizzare le informazioni su un'interfaccia di rete |Get-AzureRmNetworkInterface -Name "myNIC" -ResourceGroupName $myResourceGroup<BR><BR>Visualizza le informazioni su un'interfaccia di rete specifica. |
| Ottenere la configurazione IP hello un'interfaccia di rete |[Get-AzureRmNetworkInterfaceIPConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterfaceipconfig) -Name "myNICIP" -NetworkInterface $nic<BR><BR>Ottiene informazioni sulla configurazione IP hello hello specificato dell'interfaccia di rete. il valore di Hello $nic rappresenta l'oggetto hello restituito da Get-AzureRmNetworkInterface. |

## <a name="manage-network-resources"></a>Gestire le risorse di rete

| Attività | Comando |
| ---- | ------- |
| Aggiungere una rete virtuale di subnet tooa |[Add-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) -AddressPrefix XX.X.X.X/XX -Name "mySubnet1" -VirtualNetwork $vnet<BR><BR>Aggiunge una rete virtuale esistente subnet tooan. il valore di Hello $vnet rappresenta l'oggetto hello restituito da Get-AzureRmVirtualNetwork. |
| Eliminare una rete virtuale |[Remove-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermvirtualnetwork) -Name "myVNet" -ResourceGroupName $myResourceGroup<BR><BR>Rimuove una rete virtuale specificata hello dal gruppo di risorse hello. |
| Eliminare un'interfaccia di rete |[Remove-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermnetworkinterface) -Name "myNIC" -ResourceGroupName $myResourceGroup<BR><BR>Rimuove l'interfaccia di rete specificata hello dal gruppo di risorse hello. |
| Eliminare un servizio di bilanciamento del carico |[Remove-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermloadbalancer) -Name "myLoadBalancer" -ResourceGroupName $myResourceGroup<BR><BR>Rimuove hello specificato bilanciamento del carico dal gruppo di risorse hello. |
| Eliminare un indirizzo IP pubblico |[Remove-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermpublicipaddress)-Name "myIPAddress" -ResourceGroupName $myResourceGroup<BR><BR>Rimuove hello specificato l'indirizzo IP pubblico del gruppo di risorse hello. |

## <a name="next-steps"></a>Passaggi successivi
* Interfaccia di rete utilizzare hello appena creato quando si [creare una macchina virtuale](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Informazioni su come [creare una VM con più interfacce di rete](../../virtual-network/virtual-networks-multiple-nics.md).


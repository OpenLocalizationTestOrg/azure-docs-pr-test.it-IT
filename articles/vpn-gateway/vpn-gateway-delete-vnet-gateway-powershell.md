---
title: 'Eliminare un gateway di rete virtuale: PowerShell: Azure Resource Manager | Microsoft Docs'
description: Eliminare un gateway di rete virtuale usando PowerShell nel modello di distribuzione Resource Manager.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: cherylmc
ms.openlocfilehash: 4d0f085423d5bd60b24d88649ee1d77bcd1d009f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell"></a><span data-ttu-id="aea0e-103">Eliminare un gateway di rete virtuale usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="aea0e-103">Delete a virtual network gateway using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aea0e-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="aea0e-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="aea0e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aea0e-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="aea0e-106">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="aea0e-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="aea0e-107">Esistono due diversi approcci quando si desidera eliminare un gateway di rete virtuale per una configurazione di gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="aea0e-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="aea0e-108">Se si vuole eliminare tutto e ricominciare da capo, come nel caso di un ambiente di testing, è possibile eliminare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="aea0e-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="aea0e-109">Quando si elimina un gruppo di risorse, vengono eliminate tutte le risorse all'interno del gruppo.</span><span class="sxs-lookup"><span data-stu-id="aea0e-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="aea0e-110">Questo metodo è consigliato solo se non si vuole mantenere alcuna risorsa del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="aea0e-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="aea0e-111">Con questo approccio non è possibile eliminare in modo selettivo solo alcune risorse.</span><span class="sxs-lookup"><span data-stu-id="aea0e-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="aea0e-112">Se si desidera mantenere alcune delle risorse nel gruppo di risorse, eliminare un gateway di rete virtuale diventa leggermente più complicato.</span><span class="sxs-lookup"><span data-stu-id="aea0e-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="aea0e-113">Per poter eliminare il gateway di rete virtuale prima è necessario eliminare tutte le risorse che dipendono dal gateway.</span><span class="sxs-lookup"><span data-stu-id="aea0e-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="aea0e-114">I passaggi variano a seconda del tipo di connessioni che sono state create e delle risorse dipendenti per ogni connessione.</span><span class="sxs-lookup"><span data-stu-id="aea0e-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="aea0e-115">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="aea0e-115">Before beginning</span></span>

### <a name="1-download-the-latest-azure-resource-manager-powershell-cmdlets"></a><span data-ttu-id="aea0e-116">1. Scaricare i più recenti cmdlet PowerShell di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aea0e-116">1. Download the latest Azure Resource Manager PowerShell cmdlets.</span></span>

<span data-ttu-id="aea0e-117">Scaricare e installare la versione più recente dei cmdlet di PowerShell per Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aea0e-117">Download and install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="aea0e-118">Per altre informazioni su come scaricare e installare i cmdlet PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aea0e-118">For more information about downloading and installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="aea0e-119">2. Connettersi all'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="aea0e-119">2. Connect to your Azure account.</span></span>

<span data-ttu-id="aea0e-120">Aprire la console di PowerShell e connettersi al proprio account.</span><span class="sxs-lookup"><span data-stu-id="aea0e-120">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="aea0e-121">Per eseguire la connessione, usare gli esempi che seguono:</span><span class="sxs-lookup"><span data-stu-id="aea0e-121">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="aea0e-122">Controllare le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="aea0e-122">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="aea0e-123">Se sono disponibili più sottoscrizioni, specificare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="aea0e-123">If you have more than one subscription, specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="aea0e-124"><a name="S2S"></a>Eliminare un gateway VPN da sito a sito</span><span class="sxs-lookup"><span data-stu-id="aea0e-124"><a name="S2S"></a>Delete a Site-to-Site VPN gateway</span></span>

<span data-ttu-id="aea0e-125">Per eliminare un gateway di rete virtuale per una configurazione da sito a sito, è necessario innanzitutto eliminare ogni risorsa che riguarda il gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-125">To delete a virtual network gateway for a S2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="aea0e-126">Le risorse devono essere eliminate in un determinato ordine a causa delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="aea0e-126">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="aea0e-127">Quando si usano gli esempi seguenti, alcuni valori devono essere specificati, mentre altri sono un risultato di output.</span><span class="sxs-lookup"><span data-stu-id="aea0e-127">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="aea0e-128">Negli esempi vengono usati i seguenti valori specifici a scopo dimostrativo:</span><span class="sxs-lookup"><span data-stu-id="aea0e-128">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="aea0e-129">Nome VNet: VNet1</span><span class="sxs-lookup"><span data-stu-id="aea0e-129">VNet name: VNet1</span></span><br>
<span data-ttu-id="aea0e-130">Nome del gruppo di risorse: RG1</span><span class="sxs-lookup"><span data-stu-id="aea0e-130">Resource Group name: RG1</span></span><br>
<span data-ttu-id="aea0e-131">Nome del gateway di rete virtuale: GW1</span><span class="sxs-lookup"><span data-stu-id="aea0e-131">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="aea0e-132">La procedura seguente si applica al modello di distribuzione di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aea0e-132">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="aea0e-133">1. Ottenere il gateway di rete virtuale che si vuole eliminare.</span><span class="sxs-lookup"><span data-stu-id="aea0e-133">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="aea0e-134">2. Verificare se il gateway di rete virtuale ha qualche connessione.</span><span class="sxs-lookup"><span data-stu-id="aea0e-134">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
$Conns=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```

### <a name="3-delete-all-connections"></a><span data-ttu-id="aea0e-135">3. Eliminare tutte le connessioni.</span><span class="sxs-lookup"><span data-stu-id="aea0e-135">3. Delete all connections.</span></span>

<span data-ttu-id="aea0e-136">Potrebbe essere richiesto di confermare l'eliminazione di ciascuna delle connessioni.</span><span class="sxs-lookup"><span data-stu-id="aea0e-136">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$Conns | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="4-delete-the-virtual-network-gateway"></a><span data-ttu-id="aea0e-137">4. Eliminare il gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-137">4. Delete the virtual network gateway.</span></span>

<span data-ttu-id="aea0e-138">Potrebbe essere richiesto di confermare l'eliminazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="aea0e-138">You may be prompted to confirm the deletion of the gateway.</span></span> <span data-ttu-id="aea0e-139">Se in aggiunta alla configurazione S2S si dispone di una configurazione P2S per questa rete virtuale, l'eliminazione del gateway di rete virtuale disconnette automaticamente tutti i client P2S senza alcun avviso.</span><span class="sxs-lookup"><span data-stu-id="aea0e-139">If you have a P2S configuration to this VNet in addition to your S2S configuration, deleting the virtual network gateway will automatically disconnect all P2S clients without warning.</span></span>


```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="aea0e-140">A questo punto, il gateway di rete virtuale è stato eliminato.</span><span class="sxs-lookup"><span data-stu-id="aea0e-140">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="aea0e-141">È possibile usare i passaggi successivi per eliminare le risorse che non vengono più usate.</span><span class="sxs-lookup"><span data-stu-id="aea0e-141">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="5-delete-the-local-network-gateways"></a><span data-ttu-id="aea0e-142">5 Eliminare i gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-142">5 Delete the local network gateways.</span></span>

<span data-ttu-id="aea0e-143">Ottenere l'elenco dei gateway di rete locale corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="aea0e-143">Get the list of the corresponding local network gateways.</span></span>

```powershell
$LNG=Get-AzureRmLocalNetworkGateway -ResourceGroupName "RG1" | where-object {$_.Id -In $Conns.LocalNetworkGateway2.Id}
```

<span data-ttu-id="aea0e-144">Eliminare i gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-144">Delete the local network gateways.</span></span> <span data-ttu-id="aea0e-145">Potrebbe essere richiesto di confermare l'eliminazione di ciascuno dei gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-145">You may be prompted to confirm the deletion of each of the local network gateway.</span></span>

```powershell
$LNG | ForEach-Object {Remove-AzureRmLocalNetworkGateway -Name $_.Name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="aea0e-146">6. Eliminare le risorse degli indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="aea0e-146">6. Delete the Public IP address resources.</span></span>

<span data-ttu-id="aea0e-147">Ottenere le configurazioni IP del gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-147">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="aea0e-148">Ottenere l'elenco delle risorse degli indirizzi IP pubblici usate per il gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-148">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="aea0e-149">Se il gateway di rete virtuale è attivo-attivo, compaiono due indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="aea0e-149">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="aea0e-150">Eliminare le risorse IP pubbliche.</span><span class="sxs-lookup"><span data-stu-id="aea0e-150">Delete the Public IP resources.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "RG1"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="aea0e-151">7. Eliminare la subnet del gateway e impostare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="aea0e-151">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="aea0e-152"><a name="v2v"></a>Eliminare un gateway VPN da rete virtuale a rete virtuale</span><span class="sxs-lookup"><span data-stu-id="aea0e-152"><a name="v2v"></a>Delete a VNet-to-VNet VPN gateway</span></span>

<span data-ttu-id="aea0e-153">Per eliminare un gateway di rete virtuale per una configurazione V2V, è necessario innanzitutto eliminare ogni risorsa che riguarda il gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-153">To delete a virtual network gateway for a V2V configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="aea0e-154">Le risorse devono essere eliminate in un determinato ordine a causa delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="aea0e-154">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="aea0e-155">Quando si usano gli esempi seguenti, alcuni valori devono essere specificati, mentre altri sono un risultato di output.</span><span class="sxs-lookup"><span data-stu-id="aea0e-155">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="aea0e-156">Negli esempi vengono usati i seguenti valori specifici a scopo dimostrativo:</span><span class="sxs-lookup"><span data-stu-id="aea0e-156">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="aea0e-157">Nome VNet: VNet1</span><span class="sxs-lookup"><span data-stu-id="aea0e-157">VNet name: VNet1</span></span><br>
<span data-ttu-id="aea0e-158">Nome del gruppo di risorse: RG1</span><span class="sxs-lookup"><span data-stu-id="aea0e-158">Resource Group name: RG1</span></span><br>
<span data-ttu-id="aea0e-159">Nome del gateway di rete virtuale: GW1</span><span class="sxs-lookup"><span data-stu-id="aea0e-159">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="aea0e-160">La procedura seguente si applica al modello di distribuzione di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aea0e-160">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="aea0e-161">1. Ottenere il gateway di rete virtuale che si vuole eliminare.</span><span class="sxs-lookup"><span data-stu-id="aea0e-161">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="aea0e-162">2. Verificare se il gateway di rete virtuale ha qualche connessione.</span><span class="sxs-lookup"><span data-stu-id="aea0e-162">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="aea0e-163">Potrebbero essere presenti altre connessioni a gateway di rete virtuale che fanno parte di un gruppo di risorse diverso.</span><span class="sxs-lookup"><span data-stu-id="aea0e-163">There may be other connections to the virtual network gateway that are part of a different resource group.</span></span> <span data-ttu-id="aea0e-164">Verificare le connessioni aggiuntive in ogni gruppo di risorse aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="aea0e-164">Check for additional connections in each additional resource group.</span></span> <span data-ttu-id="aea0e-165">In questo esempio si controllano le connessioni da RG2.</span><span class="sxs-lookup"><span data-stu-id="aea0e-165">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="aea0e-166">Eseguire questa operazione per ogni gruppo di risorse che potrebbe avere una connessione al gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-166">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG2" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
```

### <a name="3-get-the-list-of-connections-in-both-directions"></a><span data-ttu-id="aea0e-167">3. Ottenere l'elenco di connessioni in entrambe le direzioni.</span><span class="sxs-lookup"><span data-stu-id="aea0e-167">3. Get the list of connections in both directions.</span></span>

<span data-ttu-id="aea0e-168">Poiché si tratta di una configurazione da rete virtuale a rete virtuale, è necessario l'elenco delle connessioni in entrambe le direzioni.</span><span class="sxs-lookup"><span data-stu-id="aea0e-168">Because this is a VNet-to-VNet configuration, you need the list of connections in both directions.</span></span>

```powershell
$ConnsL=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="aea0e-169">In questo esempio si controllano le connessioni da RG2.</span><span class="sxs-lookup"><span data-stu-id="aea0e-169">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="aea0e-170">Eseguire questa operazione per ogni gruppo di risorse che potrebbe avere una connessione al gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-170">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
 $ConnsR=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "<NameOfResourceGroup2>" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
 ```

### <a name="4-delete-all-connections"></a><span data-ttu-id="aea0e-171">4. Eliminare tutte le connessioni.</span><span class="sxs-lookup"><span data-stu-id="aea0e-171">4. Delete all connections.</span></span>

<span data-ttu-id="aea0e-172">Potrebbe essere richiesto di confermare l'eliminazione di ciascuna delle connessioni.</span><span class="sxs-lookup"><span data-stu-id="aea0e-172">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$ConnsL | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
$ConnsR | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="5-delete-the-virtual-network-gateway"></a><span data-ttu-id="aea0e-173">5. Eliminare il gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-173">5. Delete the virtual network gateway.</span></span>

<span data-ttu-id="aea0e-174">Potrebbe essere richiesto di confermare l'eliminazione del gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-174">You may be prompted to confirm the deletion of the virtual network gateway.</span></span> <span data-ttu-id="aea0e-175">Se in aggiunta alla configurazione V2V si dispone di una configurazione PS2 per questa rete virtuale, l'eliminazione dei gateway di rete virtuale disconnette automaticamente tutti i client P2S senza alcun avviso.</span><span class="sxs-lookup"><span data-stu-id="aea0e-175">If you have P2S configurations to your VNets in addition to your V2V configuration, deleting the virtual network gateways will automatically disconnect all P2S clients without warning.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="aea0e-176">A questo punto, il gateway di rete virtuale è stato eliminato.</span><span class="sxs-lookup"><span data-stu-id="aea0e-176">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="aea0e-177">È possibile usare i passaggi successivi per eliminare le risorse che non vengono più usate.</span><span class="sxs-lookup"><span data-stu-id="aea0e-177">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="aea0e-178">6. Eliminare le risorse degli indirizzi IP pubblici</span><span class="sxs-lookup"><span data-stu-id="aea0e-178">6. Delete the Public IP address resources</span></span>

<span data-ttu-id="aea0e-179">Ottenere le configurazioni IP del gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-179">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="aea0e-180">Ottenere l'elenco delle risorse degli indirizzi IP pubblici usate per il gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-180">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="aea0e-181">Se il gateway di rete virtuale è attivo-attivo, compaiono due indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="aea0e-181">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="aea0e-182">Eliminare le risorse IP pubbliche.</span><span class="sxs-lookup"><span data-stu-id="aea0e-182">Delete the Public IP resources.</span></span> <span data-ttu-id="aea0e-183">Potrebbe essere richiesto di confermare l'eliminazione dell'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="aea0e-183">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="aea0e-184">7. Eliminare la subnet del gateway e impostare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="aea0e-184">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="aea0e-185"><a name="deletep2s"></a>Eliminare un gateway VPN da sito a sito</span><span class="sxs-lookup"><span data-stu-id="aea0e-185"><a name="deletep2s"></a>Delete a Point-to-Site VPN gateway</span></span>

<span data-ttu-id="aea0e-186">Per eliminare un gateway di rete virtuale per una configurazione P2S, è necessario innanzitutto eliminare ogni risorsa che riguarda il gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-186">To delete a virtual network gateway for a P2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="aea0e-187">Le risorse devono essere eliminate in un determinato ordine a causa delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="aea0e-187">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="aea0e-188">Quando si usano gli esempi seguenti, alcuni valori devono essere specificati, mentre altri sono un risultato di output.</span><span class="sxs-lookup"><span data-stu-id="aea0e-188">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="aea0e-189">Negli esempi vengono usati i seguenti valori specifici a scopo dimostrativo:</span><span class="sxs-lookup"><span data-stu-id="aea0e-189">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="aea0e-190">Nome VNet: VNet1</span><span class="sxs-lookup"><span data-stu-id="aea0e-190">VNet name: VNet1</span></span><br>
<span data-ttu-id="aea0e-191">Nome del gruppo di risorse: RG1</span><span class="sxs-lookup"><span data-stu-id="aea0e-191">Resource Group name: RG1</span></span><br>
<span data-ttu-id="aea0e-192">Nome del gateway di rete virtuale: GW1</span><span class="sxs-lookup"><span data-stu-id="aea0e-192">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="aea0e-193">La procedura seguente si applica al modello di distribuzione di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aea0e-193">The following steps apply to the Resource Manager deployment model.</span></span>


>[!NOTE]
> <span data-ttu-id="aea0e-194">Quando si elimina il gateway VPN, tutti i client connessi vengono disconnessi dalla rete virtuale senza alcun avviso.</span><span class="sxs-lookup"><span data-stu-id="aea0e-194">When you delete the VPN gateway, all connected clients will be disconnected from the VNet without warning.</span></span>
>
>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="aea0e-195">1. Ottenere il gateway di rete virtuale che si vuole eliminare.</span><span class="sxs-lookup"><span data-stu-id="aea0e-195">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-delete-the-virtual-network-gateway"></a><span data-ttu-id="aea0e-196">2. Eliminare il gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-196">2. Delete the virtual network gateway.</span></span>

<span data-ttu-id="aea0e-197">Potrebbe essere richiesto di confermare l'eliminazione del gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-197">You may be prompted to confirm the deletion of the virtual network gateway.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="aea0e-198">A questo punto, il gateway di rete virtuale è stato eliminato.</span><span class="sxs-lookup"><span data-stu-id="aea0e-198">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="aea0e-199">È possibile usare i passaggi successivi per eliminare le risorse che non vengono più usate.</span><span class="sxs-lookup"><span data-stu-id="aea0e-199">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="3-delete-the-public-ip-address-resources"></a><span data-ttu-id="aea0e-200">3. Eliminare le risorse degli indirizzi IP pubblici</span><span class="sxs-lookup"><span data-stu-id="aea0e-200">3. Delete the Public IP address resources</span></span>

<span data-ttu-id="aea0e-201">Ottenere le configurazioni IP del gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-201">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="aea0e-202">Ottenere l'elenco degli indirizzi IP pubblici utilizzati per il gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="aea0e-202">Get the list of Public IP addresses used for this virtual network gateway.</span></span> <span data-ttu-id="aea0e-203">Se il gateway di rete virtuale è attivo-attivo, compaiono due indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="aea0e-203">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="aea0e-204">Eliminare gli indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="aea0e-204">Delete the Public IPs.</span></span> <span data-ttu-id="aea0e-205">Potrebbe essere richiesto di confermare l'eliminazione dell'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="aea0e-205">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="4-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="aea0e-206">4. Eliminare la subnet del gateway e impostare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="aea0e-206">4. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="aea0e-207"><a name="delete"></a>Eliminare un gateway VPN eliminando il gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="aea0e-207"><a name="delete"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="aea0e-208">Se non si è interessati a mantenere risorse del gruppo di risorse e si vuole solo ricominciare da capo, è possibile eliminare un intero gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="aea0e-208">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="aea0e-209">Questo è un modo rapido per rimuovere tutto.</span><span class="sxs-lookup"><span data-stu-id="aea0e-209">This is a quick way to remove everything.</span></span> <span data-ttu-id="aea0e-210">La procedura seguente si applica solo al modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aea0e-210">The following steps apply only to the Resource Manager deployment model.</span></span>

### <a name="1-get-a-list-of-all-the-resource-groups-in-your-subscription"></a><span data-ttu-id="aea0e-211">1. Ottenere un elenco di tutti i gruppi di risorse nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="aea0e-211">1. Get a list of all the resource groups in your subscription.</span></span>

```powershell
Get-AzureRmResourceGroup
```

### <a name="2-locate-the-resource-group-that-you-want-to-delete"></a><span data-ttu-id="aea0e-212">2. Individuare il gruppo di risorse da eliminare.</span><span class="sxs-lookup"><span data-stu-id="aea0e-212">2. Locate the resource group that you want to delete.</span></span>

<span data-ttu-id="aea0e-213">Individuare il gruppo di risorse che si vuole eliminare e visualizzare l'elenco delle risorse di quel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="aea0e-213">Locate the resource group that you want to delete and view the list of resources in that resource group.</span></span> <span data-ttu-id="aea0e-214">In questo esempio il nome del gruppo di risorse è RG1.</span><span class="sxs-lookup"><span data-stu-id="aea0e-214">In the example, the name of the resource group is RG1.</span></span> <span data-ttu-id="aea0e-215">Modificare l'esempio per recuperare un elenco di tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="aea0e-215">Modify the example to retrieve a list of all the resources.</span></span>

```powershell
Find-AzureRmResource -ResourceGroupNameContains RG1
```

### <a name="3-verify-the-resources-in-the-list"></a><span data-ttu-id="aea0e-216">3. Verificare le risorse dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="aea0e-216">3. Verify the resources in the list.</span></span>

<span data-ttu-id="aea0e-217">Quando viene restituito l'elenco, esaminarlo per verificare che si desidera eliminare tutte le risorse del gruppo di risorse e anche il gruppo di risorse stesso.</span><span class="sxs-lookup"><span data-stu-id="aea0e-217">When the list is returned, review it to verify that you want to delete all the resources in the resource group, as well as the resource group itself.</span></span> <span data-ttu-id="aea0e-218">Se si vogliono mantenere alcune risorse del gruppo, usare la procedura illustrata nelle sezioni precedenti di questo articolo per eliminare il gateway.</span><span class="sxs-lookup"><span data-stu-id="aea0e-218">If you want to keep some of the resources in the resource group, use the steps in the earlier sections of this article to delete your gateway.</span></span>

### <a name="4-delete-the-resource-group-and-resources"></a><span data-ttu-id="aea0e-219">4. Eliminare il gruppo di risorse e le risorse.</span><span class="sxs-lookup"><span data-stu-id="aea0e-219">4. Delete the resource group and resources.</span></span>

<span data-ttu-id="aea0e-220">Per eliminare il gruppo di risorse e tutte le risorse che contiene, modificare l'esempio ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="aea0e-220">To delete the resource group and all the resource contained in the resource group, modify the example and run.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name RG1
```

### <a name="5-check-the-status"></a><span data-ttu-id="aea0e-221">5. Controllare lo stato.</span><span class="sxs-lookup"><span data-stu-id="aea0e-221">5. Check the status.</span></span>

<span data-ttu-id="aea0e-222">Per eliminare tutte le risorse, Azure impiega un po' di tempo.</span><span class="sxs-lookup"><span data-stu-id="aea0e-222">It takes some time for Azure to delete all the resources.</span></span> <span data-ttu-id="aea0e-223">È possibile controllare lo stato del gruppo di risorse usando questo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aea0e-223">You can check the status of your resource group by using this cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName RG1
```

<span data-ttu-id="aea0e-224">Il risultato restituito mostra "Operazione riuscita".</span><span class="sxs-lookup"><span data-stu-id="aea0e-224">The result that is returned shows 'Succeeded'.</span></span>

```
ResourceGroupName : RG1
Location          : eastus
ProvisioningState : Succeeded
```
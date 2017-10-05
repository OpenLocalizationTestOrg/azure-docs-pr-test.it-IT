---
title: Reimpostare un'istanza di gateway VPN di Azure per ristabilire tunnel IPsec | Microsoft Docs
description: Questo articolo descrive la reimpostazione di Gateway VPN di Azure per ristabilire i tunnel IPsec. L'articolo riguarda i gateway VPN nei modelli di distribuzione classica e Resource Manager.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 79d77cb8-d175-4273-93ac-712d7d45b1fe
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: cherylmc
ms.openlocfilehash: 7c5ba9310568571991708ab54a5275df6ea84a39
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="reset-a-vpn-gateway"></a><span data-ttu-id="e911f-104">Reimpostare un gateway VPN</span><span class="sxs-lookup"><span data-stu-id="e911f-104">Reset a VPN Gateway</span></span>

<span data-ttu-id="e911f-105">La reimpostazione del gateway VPN di Azure è utile se si perde la connettività VPN cross-premise in uno o più tunnel VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="e911f-105">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="e911f-106">In questa situazione tutti i dispositivi VPN funzionano correttamente, ma non sono in grado di stabilire tunnel IPsec con i gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="e911f-106">In this situation, your on-premises VPN devices are all working correctly, but are not able to establish IPsec tunnels with the Azure VPN gateways.</span></span> <span data-ttu-id="e911f-107">Questo articolo consente di reimpostare il gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="e911f-107">This article helps you reset your VPN gateway.</span></span>

### <a name="what-happens-during-a-reset"></a><span data-ttu-id="e911f-108">Cosa accade durante un ripristino</span><span class="sxs-lookup"><span data-stu-id="e911f-108">What happens during a reset?</span></span>

<span data-ttu-id="e911f-109">Un gateway VPN di Azure è costituito da due istanze di macchina virtuale in esecuzione in una configurazione di standby attivo.</span><span class="sxs-lookup"><span data-stu-id="e911f-109">A VPN gateway is composed of two VM instances running in an active-standby configuration.</span></span> <span data-ttu-id="e911f-110">Quando si reimposta il gateway, quest'ultimo viene riavviato e gli vengono riapplicate le configurazioni cross-premise.</span><span class="sxs-lookup"><span data-stu-id="e911f-110">When you reset the gateway, it reboots the gateway, and then reapplies the cross-premises configurations to it.</span></span> <span data-ttu-id="e911f-111">Il gateway mantiene l'indirizzo IP pubblico già disponibile.</span><span class="sxs-lookup"><span data-stu-id="e911f-111">The gateway keeps the public IP address it already has.</span></span> <span data-ttu-id="e911f-112">Non sarà quindi necessario aggiornare la configurazione del router VPN con un nuovo indirizzo IP pubblico per il gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="e911f-112">This means you won’t need to update the VPN router configuration with a new public IP address for Azure VPN gateway.</span></span>

<span data-ttu-id="e911f-113">Dopo l'emissione del comando per ripristinare il gateway, l'istanza attualmente attiva del gateway VPN di Azure viene riavviata immediatamente.</span><span class="sxs-lookup"><span data-stu-id="e911f-113">When you issue the command to reset the gateway, the current active instance of the Azure VPN gateway is rebooted immediately.</span></span> <span data-ttu-id="e911f-114">Si verificherà un breve intervallo durante il failover dall'istanza attiva (in fase di riavvio) all'istanza di standby.</span><span class="sxs-lookup"><span data-stu-id="e911f-114">There will be a brief gap during the failover from the active instance (being rebooted), to the standby instance.</span></span> <span data-ttu-id="e911f-115">L'intervallo dovrebbe essere inferiore a un minuto.</span><span class="sxs-lookup"><span data-stu-id="e911f-115">The gap should be less than one minute.</span></span>

<span data-ttu-id="e911f-116">Se la connessione non viene ripristinata dopo il primo riavvio, emettere di nuovo lo stesso comando per riavviare la seconda istanza della VM, ovvero il nuovo gateway attivo.</span><span class="sxs-lookup"><span data-stu-id="e911f-116">If the connection is not restored after the first reboot, issue the same command again to reboot the second VM instance (the new active gateway).</span></span> <span data-ttu-id="e911f-117">Se vengono richiesti due riavvii uno dopo l'altro, il periodo necessario per il riavvio di entrambe le istanze della VM (attiva e di standby) sarà leggermente più lungo.</span><span class="sxs-lookup"><span data-stu-id="e911f-117">If the two reboots are requested back to back, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span></span> <span data-ttu-id="e911f-118">Si verificherà quindi un intervallo più lungo nella connettività VPN, dai 2 ai 4 minuti, in attesa del completamento dei riavvii.</span><span class="sxs-lookup"><span data-stu-id="e911f-118">This will cause a longer gap on the VPN connectivity, up to 2 to 4 minutes for VMs to complete the reboots.</span></span>

<span data-ttu-id="e911f-119">Dopo due riavvii, se si verificano ancora problemi di connettività cross-premise, aprire una richiesta di supporto dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e911f-119">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from the Azure portal.</span></span>

## <span data-ttu-id="e911f-120"><a name="before"></a>Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="e911f-120"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="e911f-121">Prima di reimpostare il gateway, verificare gli elementi chiave elencati di seguito per ogni tunnel VPN da sito a sito (S2S) IPsec.</span><span class="sxs-lookup"><span data-stu-id="e911f-121">Before you reset your gateway, verify the key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span></span> <span data-ttu-id="e911f-122">Eventuali mancate corrispondenze negli elementi provocherà la disconnessione dei tunnel VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="e911f-122">Any mismatch in the items will result in the disconnect of S2S VPN tunnels.</span></span> <span data-ttu-id="e911f-123">La verifica e la correzione delle configurazioni per i gateway locali e VPN di Azure evitano riavvii non necessari e interruzioni per le altre connessioni funzionanti nei gateway.</span><span class="sxs-lookup"><span data-stu-id="e911f-123">Verifying and correcting the configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for the other working connections on the gateways.</span></span>

<span data-ttu-id="e911f-124">Verificare gli elementi seguenti prima di reimpostare il gateway:</span><span class="sxs-lookup"><span data-stu-id="e911f-124">Verify the following items before resetting your gateway:</span></span>

* <span data-ttu-id="e911f-125">Gli indirizzi IP virtuali per il gateway VPN di Azure e il gateway VPN locale devono essere configurati correttamente nei criteri VPN di Azure e locali.</span><span class="sxs-lookup"><span data-stu-id="e911f-125">The Internet IP addresses (VIPs) for both the Azure VPN gateway and the on-premises VPN gateway are configured correctly in both the Azure and the on-premises VPN policies.</span></span>
* <span data-ttu-id="e911f-126">La chiave precondivisa deve essere uguale nei gateway VPN di Azure e locali.</span><span class="sxs-lookup"><span data-stu-id="e911f-126">The pre-shared key must be the same on both Azure and on-premises VPN gateways.</span></span>
* <span data-ttu-id="e911f-127">Se si applica una configurazione IPsec/IKE specifica, ad esempio la crittografia, gli algoritmi hash e PFS (Perfect Forward Secrecy), assicurarsi che i gateway VPN di Azure e locali abbiano le stesse configurazioni.</span><span class="sxs-lookup"><span data-stu-id="e911f-127">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both the Azure and on-premises VPN gateways have the same configurations.</span></span>

## <span data-ttu-id="e911f-128"><a name="portal"></a>Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e911f-128"><a name="portal"></a>Azure portal</span></span>

<span data-ttu-id="e911f-129">È possibile reimpostare un gateway VPN di Resource Manager tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e911f-129">You can reset a Resource Manager VPN gateway using the Azure portal.</span></span> <span data-ttu-id="e911f-130">Se si desidera reimpostare un gateway classico, vedere la procedura di [PowerShell](#resetclassic).</span><span class="sxs-lookup"><span data-stu-id="e911f-130">If you want to reset a classic gateway, see the [PowerShell](#resetclassic) steps.</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="e911f-131">Modello di distribuzione di Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="e911f-131">Resource Manager deployment model</span></span>

1. <span data-ttu-id="e911f-132">Aprire il [portale di Azure](https://portal.azure.com) e passare al gateway di rete virtuale di Resource Manager che si desidera reimpostare.</span><span class="sxs-lookup"><span data-stu-id="e911f-132">Open the [Azure portal](https://portal.azure.com) and navigate to the Resource Manager virtual network gateway that you want to reset.</span></span>
2. <span data-ttu-id="e911f-133">Nel pannello per il gateway di rete virtuale fare clic su "Reimposta".</span><span class="sxs-lookup"><span data-stu-id="e911f-133">On the blade for the virtual network gateway, click 'Reset'.</span></span>

  ![Pannello di reimpostazione gateway VPN](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. <span data-ttu-id="e911f-135">Nel pannello Reimposta, fare clic sul pulsante **Reimposta**.</span><span class="sxs-lookup"><span data-stu-id="e911f-135">On the Reset blade, click the **Reset** button.</span></span>

## <span data-ttu-id="e911f-136"><a name="ps"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="e911f-136"><a name="ps"></a>PowerShell</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="e911f-137">Modello di distribuzione di Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="e911f-137">Resource Manager deployment model</span></span>

<span data-ttu-id="e911f-138">Il cmdlet per la reimpostazione di un gateway è **Reset-AzureRmVirtualNetworkGateway**.</span><span class="sxs-lookup"><span data-stu-id="e911f-138">The cmdlet for resetting a gateway is **Reset-AzureRmVirtualNetworkGateway**.</span></span> <span data-ttu-id="e911f-139">Prima di eseguire un ripristino assicurarsi di avere la versione più recente dei [cmdlet di PowerShell per Azure Resource Manager](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="e911f-139">Before performing a reset, make sure you have the latest version of the [Resource Manager PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span> <span data-ttu-id="e911f-140">Nell'esempio seguente viene ripristinato un gateway di rete virtuale denominato VNet1GW nel gruppo di risorse TestRG1:</span><span class="sxs-lookup"><span data-stu-id="e911f-140">The following example resets a virtual network gateway named VNet1GW in the TestRG1 resource group:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

<span data-ttu-id="e911f-141">Risultato:</span><span class="sxs-lookup"><span data-stu-id="e911f-141">Result:</span></span>

<span data-ttu-id="e911f-142">Quando si riceve un valore restituito, si può presupporre che il ripristino del gateway abbia avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="e911f-142">When you receive a return result, you can assume the gateway reset was successful.</span></span> <span data-ttu-id="e911f-143">Tuttavia, non c'è alcun elemento nel risultato restituito che indica in modo esplicito che il ripristino è riuscito.</span><span class="sxs-lookup"><span data-stu-id="e911f-143">However, there is nothing in the return result that indicates explicitly that the reset was successful.</span></span> <span data-ttu-id="e911f-144">Se si desidera esaminare attentamente la cronologia per trovare il momento preciso in cui si è verificato il ripristino del gateway, è possibile visualizzare l'informazione nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e911f-144">If you want to look closely at the history to see exactly when the gateway reset occurred, you can view that information in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e911f-145">Nel portale, passare a **"GatewayName" -> Integrità risorse**.</span><span class="sxs-lookup"><span data-stu-id="e911f-145">In the portal, navigate to **'GatewayName' -> Resource Health**.</span></span>

### <span data-ttu-id="e911f-146"><a name="resetclassic"></a>Modello di distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="e911f-146"><a name="resetclassic"></a>Classic deployment model</span></span>

<span data-ttu-id="e911f-147">Il cmdlet per la reimpostazione di un gateway è **Reset-AzureVNetGateway**.</span><span class="sxs-lookup"><span data-stu-id="e911f-147">The cmdlet for resetting a gateway is **Reset-AzureVNetGateway**.</span></span> <span data-ttu-id="e911f-148">Prima di eseguire un ripristino assicurarsi di avere la versione più recente dei [cmdlet di PowerShell per Gestione servizi](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="e911f-148">Before performing a reset, make sure you have the latest version of the [Service Management (SM) PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span></span> <span data-ttu-id="e911f-149">L'esempio seguente reimposta il gateway per la rete virtuale denominata "ContosoVNet":</span><span class="sxs-lookup"><span data-stu-id="e911f-149">The following example resets the gateway for a virtual network named "ContosoVNet":</span></span>

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

<span data-ttu-id="e911f-150">Risultato:</span><span class="sxs-lookup"><span data-stu-id="e911f-150">Result:</span></span>

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <span data-ttu-id="e911f-151"><a name="cli"></a></span><span class="sxs-lookup"><span data-stu-id="e911f-151"><a name="cli"></a>Azure CLI</span></span>

<span data-ttu-id="e911f-152">Per reimpostare il gateway, usare il comando [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset).</span><span class="sxs-lookup"><span data-stu-id="e911f-152">To reset the gateway, use the [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) command.</span></span> <span data-ttu-id="e911f-153">Nell'esempio seguente viene ripristinato un gateway di rete virtuale denominato VNet5GW nel gruppo di risorse TestRG5:</span><span class="sxs-lookup"><span data-stu-id="e911f-153">The following example resets a virtual network gateway named VNet5GW in the TestRG5 resource group:</span></span>

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

<span data-ttu-id="e911f-154">Risultato:</span><span class="sxs-lookup"><span data-stu-id="e911f-154">Result:</span></span>

<span data-ttu-id="e911f-155">Quando si riceve un valore restituito, si può presupporre che il ripristino del gateway abbia avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="e911f-155">When you receive a return result, you can assume the gateway reset was successful.</span></span> <span data-ttu-id="e911f-156">Tuttavia, non c'è alcun elemento nel risultato restituito che indica in modo esplicito che il ripristino è riuscito.</span><span class="sxs-lookup"><span data-stu-id="e911f-156">However, there is nothing in the return result that indicates explicitly that the reset was successful.</span></span> <span data-ttu-id="e911f-157">Se si desidera esaminare attentamente la cronologia per trovare il momento preciso in cui si è verificato il ripristino del gateway, è possibile visualizzare l'informazione nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e911f-157">If you want to look closely at the history to see exactly when the gateway reset occurred, you can view that information in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e911f-158">Nel portale, passare a **"GatewayName" -> Integrità risorse**.</span><span class="sxs-lookup"><span data-stu-id="e911f-158">In the portal, navigate to **'GatewayName' -> Resource Health**.</span></span>
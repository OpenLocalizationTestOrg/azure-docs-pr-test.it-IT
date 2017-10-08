---
title: Reimpostare un tooreestablish gateway VPN di Azure tunnel IPsec | Documenti Microsoft
description: In questo articolo illustra la reimpostazione del tunnel IPsec di tooreestablish Gateway VPN di Azure. articolo Hello applica gateway tooVPN hello classic e modelli di distribuzione di gestione risorse di hello.
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
ms.openlocfilehash: 84dd741f0bebd6b18cb235216a68a88da5fe17b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reset-a-vpn-gateway"></a><span data-ttu-id="38936-104">Reimpostare un gateway VPN</span><span class="sxs-lookup"><span data-stu-id="38936-104">Reset a VPN Gateway</span></span>

<span data-ttu-id="38936-105">La reimpostazione del gateway VPN di Azure è utile se si perde la connettività VPN cross-premise in uno o più tunnel VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="38936-105">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="38936-106">In questo caso, i dispositivi VPN locali sono tutte le funzioni correttamente, ma sono tooestablish non è possibile tunnel IPsec con gateway VPN di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="38936-106">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="38936-107">Questo articolo consente di reimpostare il gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="38936-107">This article helps you reset your VPN gateway.</span></span>

### <a name="what-happens-during-a-reset"></a><span data-ttu-id="38936-108">Cosa accade durante un ripristino</span><span class="sxs-lookup"><span data-stu-id="38936-108">What happens during a reset?</span></span>

<span data-ttu-id="38936-109">Un gateway VPN di Azure è costituito da due istanze di macchina virtuale in esecuzione in una configurazione di standby attivo.</span><span class="sxs-lookup"><span data-stu-id="38936-109">A VPN gateway is composed of two VM instances running in an active-standby configuration.</span></span> <span data-ttu-id="38936-110">Quando si reimposta il gateway di hello, riavvio gateway hello e quindi riapplica hello cross-premise tooit configurazioni.</span><span class="sxs-lookup"><span data-stu-id="38936-110">When you reset hello gateway, it reboots hello gateway, and then reapplies hello cross-premises configurations tooit.</span></span> <span data-ttu-id="38936-111">gateway Hello mantiene l'indirizzo IP pubblico hello che è già stato assegnato.</span><span class="sxs-lookup"><span data-stu-id="38936-111">hello gateway keeps hello public IP address it already has.</span></span> <span data-ttu-id="38936-112">Ciò significa che non è necessario configurazione del router VPN hello tooupdate con un nuovo indirizzo IP pubblico per il gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="38936-112">This means you won’t need tooupdate hello VPN router configuration with a new public IP address for Azure VPN gateway.</span></span>

<span data-ttu-id="38936-113">Quando si esegue gateway di hello tooreset comando hello, hello attivo corrente del gateway VPN di Azure hello è stato riavviato immediatamente.</span><span class="sxs-lookup"><span data-stu-id="38936-113">When you issue hello command tooreset hello gateway, hello current active instance of hello Azure VPN gateway is rebooted immediately.</span></span> <span data-ttu-id="38936-114">Vi sarà un gap breve durante il failover hello dal hello active istanza (in corso il riavvio), toohello standby.</span><span class="sxs-lookup"><span data-stu-id="38936-114">There will be a brief gap during hello failover from hello active instance (being rebooted), toohello standby instance.</span></span> <span data-ttu-id="38936-115">gap Hello deve essere inferiore al minuto.</span><span class="sxs-lookup"><span data-stu-id="38936-115">hello gap should be less than one minute.</span></span>

<span data-ttu-id="38936-116">Se la connessione hello non viene ripristinata dopo il riavvio del primo hello, problema hello stesso comando nuovamente tooreboot hello seconda VM istanza (hello nuovo gateway active).</span><span class="sxs-lookup"><span data-stu-id="38936-116">If hello connection is not restored after hello first reboot, issue hello same command again tooreboot hello second VM instance (hello new active gateway).</span></span> <span data-ttu-id="38936-117">Se due riavvii hello richiesto tooback indietro, esisterà un periodo leggermente più lungo in entrambe le istanze di macchina virtuale (attive e standby) sono in corso il riavvio.</span><span class="sxs-lookup"><span data-stu-id="38936-117">If hello two reboots are requested back tooback, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span></span> <span data-ttu-id="38936-118">In questo modo un gap più connettività VPN hello, backup too2 too4 minuti per il riavvio di hello toocomplete macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="38936-118">This will cause a longer gap on hello VPN connectivity, up too2 too4 minutes for VMs toocomplete hello reboots.</span></span>

<span data-ttu-id="38936-119">Dopo due riavvii, se si verificano ancora problemi di connettività tra più sedi locali, aprire una richiesta di supporto da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="38936-119">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from hello Azure portal.</span></span>

## <span data-ttu-id="38936-120"><a name="before"></a>Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="38936-120"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="38936-121">Prima di ripristinare il gateway, verificare gli elementi chiave hello elencati di seguito per ogni tunnel VPN IPsec da sito a sito (S2S).</span><span class="sxs-lookup"><span data-stu-id="38936-121">Before you reset your gateway, verify hello key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span></span> <span data-ttu-id="38936-122">Mancata corrispondenza negli elementi hello comporterà la disconnessione di hello di tunnel VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="38936-122">Any mismatch in hello items will result in hello disconnect of S2S VPN tunnels.</span></span> <span data-ttu-id="38936-123">Verifica e la correzione delle configurazioni di hello per le sedi locali e i gateway VPN di Azure consente di riavvii non necessari e interruzioni per hello altre connessioni di lavoro nei gateway hello.</span><span class="sxs-lookup"><span data-stu-id="38936-123">Verifying and correcting hello configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for hello other working connections on hello gateways.</span></span>

<span data-ttu-id="38936-124">Verificare i seguenti elementi prima di reimpostare il gateway hello:</span><span class="sxs-lookup"><span data-stu-id="38936-124">Verify hello following items before resetting your gateway:</span></span>

* <span data-ttu-id="38936-125">Hello Internet IP (VIP) per entrambi gateway VPN di Azure hello e che hello locale gateway VPN siano configurate correttamente in entrambi hello Azure e hello locale VPN i criteri.</span><span class="sxs-lookup"><span data-stu-id="38936-125">hello Internet IP addresses (VIPs) for both hello Azure VPN gateway and hello on-premises VPN gateway are configured correctly in both hello Azure and hello on-premises VPN policies.</span></span>
* <span data-ttu-id="38936-126">chiave precondivisa Hello devono essere hello stesso nei gateway VPN di Azure sia in locale.</span><span class="sxs-lookup"><span data-stu-id="38936-126">hello pre-shared key must be hello same on both Azure and on-premises VPN gateways.</span></span>
* <span data-ttu-id="38936-127">Se si applica configurazione IPsec/IKE specifico, ad esempio la crittografia, algoritmi di hash e PFS (Perfect Forward Secrecy), assicurarsi che entrambi hello Azure e i gateway VPN locale disponga hello stesse configurazioni.</span><span class="sxs-lookup"><span data-stu-id="38936-127">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both hello Azure and on-premises VPN gateways have hello same configurations.</span></span>

## <span data-ttu-id="38936-128"><a name="portal"></a>Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="38936-128"><a name="portal"></a>Azure portal</span></span>

<span data-ttu-id="38936-129">È possibile reimpostare un gateway di gestione risorse VPN tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="38936-129">You can reset a Resource Manager VPN gateway using hello Azure portal.</span></span> <span data-ttu-id="38936-130">Se si desidera tooreset un gateway classico, vedere hello [PowerShell](#resetclassic) passaggi.</span><span class="sxs-lookup"><span data-stu-id="38936-130">If you want tooreset a classic gateway, see hello [PowerShell](#resetclassic) steps.</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="38936-131">Modello di distribuzione di Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="38936-131">Resource Manager deployment model</span></span>

1. <span data-ttu-id="38936-132">Aprire hello [portale di Azure](https://portal.azure.com) e passare toohello gateway di rete virtuale di gestione risorse che si desidera tooreset.</span><span class="sxs-lookup"><span data-stu-id="38936-132">Open hello [Azure portal](https://portal.azure.com) and navigate toohello Resource Manager virtual network gateway that you want tooreset.</span></span>
2. <span data-ttu-id="38936-133">Nel Pannello di hello per gateway di rete virtuale hello, fare clic su 'Reset'.</span><span class="sxs-lookup"><span data-stu-id="38936-133">On hello blade for hello virtual network gateway, click 'Reset'.</span></span>

  ![Pannello di reimpostazione gateway VPN](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. <span data-ttu-id="38936-135">In hello reimpostare pannello, fare clic su hello **reimpostare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="38936-135">On hello Reset blade, click hello **Reset** button.</span></span>

## <span data-ttu-id="38936-136"><a name="ps"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="38936-136"><a name="ps"></a>PowerShell</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="38936-137">Modello di distribuzione di Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="38936-137">Resource Manager deployment model</span></span>

<span data-ttu-id="38936-138">Hello cmdlet per la reimpostazione di un gateway è **reimpostazione AzureRmVirtualNetworkGateway**.</span><span class="sxs-lookup"><span data-stu-id="38936-138">hello cmdlet for resetting a gateway is **Reset-AzureRmVirtualNetworkGateway**.</span></span> <span data-ttu-id="38936-139">Prima di eseguire una reimpostazione, assicurarsi di disporre hello l'ultima versione di hello [cmdlet PowerShell di gestione risorse](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="38936-139">Before performing a reset, make sure you have hello latest version of hello [Resource Manager PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span> <span data-ttu-id="38936-140">Hello seguente esempio mostra come reimpostare un gateway di rete virtuale denominato VNet1GW nel gruppo di risorse TestRG1 hello:</span><span class="sxs-lookup"><span data-stu-id="38936-140">hello following example resets a virtual network gateway named VNet1GW in hello TestRG1 resource group:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

<span data-ttu-id="38936-141">Risultato:</span><span class="sxs-lookup"><span data-stu-id="38936-141">Result:</span></span>

<span data-ttu-id="38936-142">Quando si riceve un valore restituito, si può presupporre hello gateway reimpostazione è stata eseguita correttamente.</span><span class="sxs-lookup"><span data-stu-id="38936-142">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="38936-143">Tuttavia, non è nothing nel risultato restituito hello che indica in modo esplicito tale reimpostazione hello ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="38936-143">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="38936-144">Se si desidera toolook strettamente in hello cronologia toosee esattamente quando gateway hello reimpostazione si è verificato, è possibile visualizzare tali informazioni in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="38936-144">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="38936-145">Nel portale di hello passare troppo**'GatewayName' -> integrità delle risorse**.</span><span class="sxs-lookup"><span data-stu-id="38936-145">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>

### <span data-ttu-id="38936-146"><a name="resetclassic"></a>Modello di distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="38936-146"><a name="resetclassic"></a>Classic deployment model</span></span>

<span data-ttu-id="38936-147">Hello cmdlet per la reimpostazione di un gateway è **Reset-AzureVNetGateway**.</span><span class="sxs-lookup"><span data-stu-id="38936-147">hello cmdlet for resetting a gateway is **Reset-AzureVNetGateway**.</span></span> <span data-ttu-id="38936-148">Prima di eseguire una reimpostazione, assicurarsi di disporre hello l'ultima versione di hello [i cmdlet PowerShell di gestione del servizio (SM)](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="38936-148">Before performing a reset, make sure you have hello latest version of hello [Service Management (SM) PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span></span> <span data-ttu-id="38936-149">Hello esempio seguente viene reimpostato gateway hello per una rete virtuale denominata "ContosoVNet":</span><span class="sxs-lookup"><span data-stu-id="38936-149">hello following example resets hello gateway for a virtual network named "ContosoVNet":</span></span>

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

<span data-ttu-id="38936-150">Risultato:</span><span class="sxs-lookup"><span data-stu-id="38936-150">Result:</span></span>

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <span data-ttu-id="38936-151"><a name="cli"></a></span><span class="sxs-lookup"><span data-stu-id="38936-151"><a name="cli"></a>Azure CLI</span></span>

<span data-ttu-id="38936-152">gateway hello tooreset, utilizzare hello [az-gateway di rete virtuale rete reimpostare](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) comando.</span><span class="sxs-lookup"><span data-stu-id="38936-152">tooreset hello gateway, use hello [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) command.</span></span> <span data-ttu-id="38936-153">Hello seguente esempio mostra come reimpostare un gateway di rete virtuale denominato VNet5GW nel gruppo di risorse TestRG5 hello:</span><span class="sxs-lookup"><span data-stu-id="38936-153">hello following example resets a virtual network gateway named VNet5GW in hello TestRG5 resource group:</span></span>

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

<span data-ttu-id="38936-154">Risultato:</span><span class="sxs-lookup"><span data-stu-id="38936-154">Result:</span></span>

<span data-ttu-id="38936-155">Quando si riceve un valore restituito, si può presupporre hello gateway reimpostazione è stata eseguita correttamente.</span><span class="sxs-lookup"><span data-stu-id="38936-155">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="38936-156">Tuttavia, non è nothing nel risultato restituito hello che indica in modo esplicito tale reimpostazione hello ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="38936-156">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="38936-157">Se si desidera toolook strettamente in hello cronologia toosee esattamente quando gateway hello reimpostazione si è verificato, è possibile visualizzare tali informazioni in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="38936-157">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="38936-158">Nel portale di hello passare troppo**'GatewayName' -> integrità delle risorse**.</span><span class="sxs-lookup"><span data-stu-id="38936-158">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>

---
title: 'Eliminare un gateway di rete virtuale: Portale di Azure: Resource Manager | Microsoft Docs'
description: Eliminare un gateway di rete virtuale usando il portale di Azure nel modello di distribuzione Resource Manager.
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
ms.openlocfilehash: 1d289c09465cb8d5e4bfa569441dffcbf562b3bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-virtual-network-gateway-using-the-portal"></a><span data-ttu-id="3a563-103">Eliminare un gateway di rete virtuale usando il portale</span><span class="sxs-lookup"><span data-stu-id="3a563-103">Delete a virtual network gateway using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3a563-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3a563-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="3a563-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a563-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="3a563-106">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="3a563-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)

<span data-ttu-id="3a563-107">Esistono due diversi approcci quando si desidera eliminare un gateway di rete virtuale per una configurazione di gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="3a563-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="3a563-108">Se si vuole eliminare tutto e ricominciare da capo, come nel caso di un ambiente di testing, è possibile eliminare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="3a563-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="3a563-109">Quando si elimina un gruppo di risorse, vengono eliminate tutte le risorse all'interno del gruppo.</span><span class="sxs-lookup"><span data-stu-id="3a563-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="3a563-110">Questo metodo è consigliato solo se non si vuole mantenere alcuna risorsa del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="3a563-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="3a563-111">Con questo approccio non è possibile eliminare in modo selettivo solo alcune risorse.</span><span class="sxs-lookup"><span data-stu-id="3a563-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="3a563-112">Se si desidera mantenere alcune delle risorse nel gruppo di risorse, eliminare un gateway di rete virtuale diventa leggermente più complicato.</span><span class="sxs-lookup"><span data-stu-id="3a563-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="3a563-113">Per poter eliminare il gateway di rete virtuale prima è necessario eliminare tutte le risorse che dipendono dal gateway.</span><span class="sxs-lookup"><span data-stu-id="3a563-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="3a563-114">I passaggi variano a seconda del tipo di connessioni che sono state create e delle risorse dipendenti per ogni connessione.</span><span class="sxs-lookup"><span data-stu-id="3a563-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="delete-a-vpn-gateway"></a><span data-ttu-id="3a563-115">Eliminare un gateway VPN</span><span class="sxs-lookup"><span data-stu-id="3a563-115">Delete a VPN gateway</span></span>

<span data-ttu-id="3a563-116">Per eliminare un gateway di rete virtuale, è necessario innanzitutto eliminare ogni risorsa relativa al gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="3a563-116">To delete a virtual network gateway, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="3a563-117">Le risorse devono essere eliminate in un determinato ordine a causa delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="3a563-117">Resources must be deleted in a certain order due to dependencies.</span></span>

[!INCLUDE [delete gateway](../../includes/vpn-gateway-delete-vnet-gateway-portal-include.md)]

<span data-ttu-id="3a563-118">A questo punto, viene eliminato il gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="3a563-118">At this point, the virtual network gateway is deleted.</span></span> <span data-ttu-id="3a563-119">I passaggi successivi consentono di eliminare le risorse che non vengono più usate.</span><span class="sxs-lookup"><span data-stu-id="3a563-119">The next steps help you delete any resources that are no longer being used.</span></span>

### <a name="to-delete-the-local-network-gateway"></a><span data-ttu-id="3a563-120">Per eliminare il gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="3a563-120">To delete the local network gateway</span></span>

1. <span data-ttu-id="3a563-121">In **Tutte le risorse**, individuare i gateway di rete locale associati a ogni connessione.</span><span class="sxs-lookup"><span data-stu-id="3a563-121">In **All resources**, locate the local network gateways that were associated with each connection.</span></span>
2. <span data-ttu-id="3a563-122">Nel pannello **Informazioni generali** del gateway di rete locale, fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="3a563-122">On the **Overview** blade for the local network gateway, click **Delete**.</span></span>

### <a name="to-delete-the-public-ip-address-resource-for-the-gateway"></a><span data-ttu-id="3a563-123">Per eliminare la risorsa dell'indirizzo IP pubblico del gateway</span><span class="sxs-lookup"><span data-stu-id="3a563-123">To delete the Public IP address resource for the gateway</span></span>

1. <span data-ttu-id="3a563-124">In **Tutte le risorse**, individuare la risorsa dell'indirizzo IP pubblico associata al gateway.</span><span class="sxs-lookup"><span data-stu-id="3a563-124">In **All resources**, locate the Public IP address resource that was associated to the gateway.</span></span> <span data-ttu-id="3a563-125">Se il gateway di rete virtuale è attivo-attivo, compaiono due indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="3a563-125">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span> 
2. <span data-ttu-id="3a563-126">Nella pagina **Panoramica** dell'indirizzo IP pubblico fare clic su **Elimina** quindi su **Sì** per confermare.</span><span class="sxs-lookup"><span data-stu-id="3a563-126">On the **Overview** page for the Public IP address, click **Delete**, then **Yes** to confirm.</span></span>

### <a name="to-delete-the-gateway-subnet"></a><span data-ttu-id="3a563-127">Per eliminare la subnet del gateway</span><span class="sxs-lookup"><span data-stu-id="3a563-127">To delete the gateway subnet</span></span>

1. <span data-ttu-id="3a563-128">In **Tutte le risorse**, individuare la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="3a563-128">In **All resources**, locate the virtual network.</span></span> 
2. <span data-ttu-id="3a563-129">Nel pannello **Subnet**, fare clic su **GatewaySubnet** quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="3a563-129">On the **Subnets** blade, click the **GatewaySubnet**, then click **Delete**.</span></span> 
3. <span data-ttu-id="3a563-130">Fare clic su **Sì** per confermare l'eliminazione della subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="3a563-130">Click **Yes** to confirm that you want to delete the gateway subnet.</span></span>

## <span data-ttu-id="3a563-131"><a name="deleterg"></a>Eliminare un gateway VPN eliminando il gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="3a563-131"><a name="deleterg"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="3a563-132">Se non si è interessati a mantenere risorse del gruppo di risorse e si vuole solo ricominciare da capo, è possibile eliminare un intero gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="3a563-132">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="3a563-133">Questo è un modo rapido per rimuovere tutto.</span><span class="sxs-lookup"><span data-stu-id="3a563-133">This is a quick way to remove everything.</span></span> <span data-ttu-id="3a563-134">La procedura seguente si applica solo al modello di distribuzione di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3a563-134">The following steps apply only to the Resource Manager deployment model.</span></span>

1. <span data-ttu-id="3a563-135">In **Tutte le risorse**, individuare il gruppo di risorse e fare clic per aprire il pannello.</span><span class="sxs-lookup"><span data-stu-id="3a563-135">In **All resources**, locate the resource group and click to open the blade.</span></span>
2. <span data-ttu-id="3a563-136">Fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="3a563-136">Click **Delete**.</span></span> <span data-ttu-id="3a563-137">Nel pannello Elimina visualizzare le risorse interessate.</span><span class="sxs-lookup"><span data-stu-id="3a563-137">On the Delete blade, view the affected resources.</span></span> <span data-ttu-id="3a563-138">Assicurarsi che si desidera eliminare tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="3a563-138">Make sure that you want to delete all of these resources.</span></span> <span data-ttu-id="3a563-139">In caso contrario, usare i passaggi in [Eliminare un gateway VPN](#deletegw) all'inizio di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="3a563-139">If not, use the steps in [Delete a VPN gateway](#deletegw) at the top of this article.</span></span>
3. <span data-ttu-id="3a563-140">Per continuare, digitare il nome del gruppo di risorse che si desidera eliminare, quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="3a563-140">To proceed, type the name of the resource group that you want to delete, then click **Delete**.</span></span>
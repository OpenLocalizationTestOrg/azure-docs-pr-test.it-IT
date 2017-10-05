---
title: Impossibile eliminare una rete virtuale in Azure | Microsoft Docs
description: "Informazioni su come risolvere il problema in cui non è possibile eliminare una rete virtuale in Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: 55c42a91bb1c5fad289b975ffae8ce4d6e7343dd
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="troubleshooting-failed-to-delete-a-virtual-network-in-azure"></a><span data-ttu-id="46ef3-103">Risoluzione dei problemi: Impossibile eliminare una rete virtuale in Azure</span><span class="sxs-lookup"><span data-stu-id="46ef3-103">Troubleshooting: Failed to delete a virtual network in Azure</span></span>

<span data-ttu-id="46ef3-104">Quando si tenta di eliminare una rete virtuale in Microsoft Azure, è possibile che si riceva un errore.</span><span class="sxs-lookup"><span data-stu-id="46ef3-104">You might receive errors when you try to delete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="46ef3-105">Questo articolo illustra la procedura per risolvere questo tipo di problema.</span><span class="sxs-lookup"><span data-stu-id="46ef3-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="46ef3-106">Guida alla risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="46ef3-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="46ef3-107">[Verificare se nella rete virtuale è in esecuzione un gateway di rete virtuale](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="46ef3-107">[Check whether a virtual network gateway is running in the virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="46ef3-108">[Verificare se nella rete virtuale è in esecuzione un gateway applicazione](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="46ef3-108">[Check whether an application gateway is running in the virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="46ef3-109">[Verificare se nella rete virtuale è abilitato il servizio Azure Active Directory Domain Service](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="46ef3-109">[Check whether Azure Active Directory Domain Service is enabled in the virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="46ef3-110">[Verificare se la rete virtuale è connessa ad altre risorse](#check-whether-the-virtual-network-is-connected-to-other-resource).</span><span class="sxs-lookup"><span data-stu-id="46ef3-110">[Check whether the virtual network is connected to other resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="46ef3-111">[Verificare se nella rete virtuale è ancora in esecuzione una macchina virtuale](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="46ef3-111">[Check whether a virtual machine is still running in the virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="46ef3-112">[Verificare se la rete virtuale è bloccata in fase di migrazione](#check-whether-the-virtual-network-is-stuck-in-migration).</span><span class="sxs-lookup"><span data-stu-id="46ef3-112">[Check whether the virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="46ef3-113">Passaggi per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="46ef3-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network"></a><span data-ttu-id="46ef3-114">Verificare se nella rete virtuale è in esecuzione un gateway di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="46ef3-114">Check whether a virtual network gateway is running in the virtual network</span></span>

<span data-ttu-id="46ef3-115">Per rimuovere la rete virtuale, è necessario rimuovere prima il gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="46ef3-115">To remove the virtual network, you must first remove the virtual network gateway.</span></span>

<span data-ttu-id="46ef3-116">In caso di reti virtuali classiche, accedere alla pagina **Panoramica** della rete virtuale classica nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="46ef3-116">For classic virtual networks, go to the **Overview** page of the classic virtual network in the Azure portal.</span></span> <span data-ttu-id="46ef3-117">Se il gateway è in esecuzione nella rete virtuale, nella sezione **Connessioni VPN** verrà visualizzato l'indirizzo IP del gateway.</span><span class="sxs-lookup"><span data-stu-id="46ef3-117">In the **VPN connections** section, if the gateway is running in the virtual network, you will see the IP address of the gateway.</span></span> 

![Verificare se il gateway è in esecuzione](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="46ef3-119">In caso di reti virtuali, accedere alla pagina **Panoramica** della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="46ef3-119">For virtual networks, go to the **Overview** page of the virtual network.</span></span> <span data-ttu-id="46ef3-120">Controllare i **dispositivi connessi** associati al gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="46ef3-120">Check **Connected devices** for the virtual network gateway.</span></span>

![Controllare il dispositivo collegato](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="46ef3-122">Prima di poter rimuovere il gateway, è necessario rimuovere eventuali oggetti **Connessione** presenti nel gateway.</span><span class="sxs-lookup"><span data-stu-id="46ef3-122">Before you can remove the gateway, first remove any **Connection** objects in the gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-the-virtual-network"></a><span data-ttu-id="46ef3-123">Verificare se nella rete virtuale è in esecuzione un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="46ef3-123">Check whether an application gateway is running in the virtual network</span></span>

<span data-ttu-id="46ef3-124">Accedere alla pagina **Panoramica** della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="46ef3-124">Go to the **Overview** page of the virtual network.</span></span> <span data-ttu-id="46ef3-125">Controllare i **dispositivi connessi** associati al gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="46ef3-125">Check the **Connected devices** for the application gateway.</span></span>

![Controllare il dispositivo collegato](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="46ef3-127">Se è presente un gateway applicazione, è necessario rimuoverlo prima di poter eliminare la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="46ef3-127">If there is an application gateway, you must remove it before you can delete the virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network"></a><span data-ttu-id="46ef3-128">Verificare se nella rete virtuale è abilitato il servizio Azure Active Directory Domain Service</span><span class="sxs-lookup"><span data-stu-id="46ef3-128">Check whether Azure Active Directory Domain Service is enabled in the virtual network</span></span>

<span data-ttu-id="46ef3-129">Se Active Directory Domain Service è abilitato e connesso alla rete virtuale, non è possibile eliminare la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="46ef3-129">If the Active Directory Domain Service is enabled and connected to the virtual network, you cannot delete this virtual network.</span></span> 

![Controllare il dispositivo collegato](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="46ef3-131">Per disabilitare il servizio, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="46ef3-131">To disable the service, follow these steps:</span></span>

1. <span data-ttu-id="46ef3-132">Passare al [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="46ef3-132">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="46ef3-133">Nel riquadro sinistro selezionare **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46ef3-133">In the left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="46ef3-134">Selezionare la directory di Azure Active Directory (Azure AD) in cui è abilitato Active Directory Domain Service.</span><span class="sxs-lookup"><span data-stu-id="46ef3-134">Select the Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="46ef3-135">Selezionare la scheda **Configura** .</span><span class="sxs-lookup"><span data-stu-id="46ef3-135">Select the **Configure** tab.</span></span>
5. <span data-ttu-id="46ef3-136">In **Servizi di dominio** impostare l'opzione **Abilita Servizi di dominio per la directory** su **No**.</span><span class="sxs-lookup"><span data-stu-id="46ef3-136">Under **domain services**, change the **Enable domain services for this directory** option to **No**.</span></span>  

### <a name="check-whether-the-virtual-network-is-connected-to-other-resource"></a><span data-ttu-id="46ef3-137">Verificare se la rete virtuale è connessa ad altre risorse</span><span class="sxs-lookup"><span data-stu-id="46ef3-137">Check whether the virtual network is connected to other resource</span></span>

<span data-ttu-id="46ef3-138">Controllare i collegamenti del circuito, le connessioni e i peering di rete virtuale,</span><span class="sxs-lookup"><span data-stu-id="46ef3-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="46ef3-139">poiché questi elementi possono impedire l'eliminazione di una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="46ef3-139">Any of these can cause a virtual network deletion to fail.</span></span> 

<span data-ttu-id="46ef3-140">Di seguito è riportato l'ordine di eliminazione consigliato:</span><span class="sxs-lookup"><span data-stu-id="46ef3-140">The recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="46ef3-141">Connessioni del gateway</span><span class="sxs-lookup"><span data-stu-id="46ef3-141">Gateway connections</span></span>
2. <span data-ttu-id="46ef3-142">Gateway</span><span class="sxs-lookup"><span data-stu-id="46ef3-142">Gateways</span></span>
3. <span data-ttu-id="46ef3-143">Indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="46ef3-143">IPs</span></span>
4. <span data-ttu-id="46ef3-144">Peering di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="46ef3-144">Virtual network peerings</span></span>
5. <span data-ttu-id="46ef3-145">Ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="46ef3-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-the-virtual-network"></a><span data-ttu-id="46ef3-146">Verificare se nella rete virtuale è ancora in esecuzione una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="46ef3-146">Check whether a virtual machine is still running in the virtual network</span></span>

<span data-ttu-id="46ef3-147">Assicurarsi che nella rete virtuale non si trovi alcuna macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="46ef3-147">Make sure that no virtual machine is in the virtual network.</span></span>

### <a name="check-whether-the-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="46ef3-148">Verificare se la rete virtuale è bloccata in stato di migrazione</span><span class="sxs-lookup"><span data-stu-id="46ef3-148">Check whether the virtual network is stuck in migration</span></span>

<span data-ttu-id="46ef3-149">Se la rete virtuale è bloccata in uno stato di migrazione, non può essere eliminata.</span><span class="sxs-lookup"><span data-stu-id="46ef3-149">If the virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="46ef3-150">Eseguire il comando seguente per interrompere la migrazione e quindi eliminare la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="46ef3-150">Run the following command to abort the migration, and then delete the virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="46ef3-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="46ef3-151">Next steps</span></span>

- [<span data-ttu-id="46ef3-152">Rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="46ef3-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="46ef3-153">Domande frequenti sulla rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="46ef3-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)
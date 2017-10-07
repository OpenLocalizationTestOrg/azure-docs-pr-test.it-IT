---
title: aaaCannot eliminare una rete virtuale in Azure | Documenti Microsoft
description: "Informazioni su come tootroubleshoot hello problema in cui non è possibile eliminare una rete virtuale in Azure."
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
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a><span data-ttu-id="9d6ee-103">Risoluzione dei problemi: Impossibile toodelete una rete virtuale in Azure</span><span class="sxs-lookup"><span data-stu-id="9d6ee-103">Troubleshooting: Failed toodelete a virtual network in Azure</span></span>

<span data-ttu-id="9d6ee-104">È possibile ricevere errori quando si tenta di toodelete una rete virtuale in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-104">You might receive errors when you try toodelete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="9d6ee-105">Questo articolo fornisce la risoluzione dei problemi toohelp passaggi risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="9d6ee-106">Guida alla risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="9d6ee-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="9d6ee-107">[Verificare se un gateway di rete virtuale è in esecuzione nella rete virtuale hello](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="9d6ee-107">[Check whether a virtual network gateway is running in hello virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="9d6ee-108">[Verificare se un gateway applicazione è in esecuzione nella rete virtuale hello](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="9d6ee-108">[Check whether an application gateway is running in hello virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="9d6ee-109">[Controllare se il servizio di dominio Azure Active Directory è abilitato nella rete virtuale hello](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="9d6ee-109">[Check whether Azure Active Directory Domain Service is enabled in hello virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="9d6ee-110">[Controllare se la rete virtuale hello è connesso tooother risorse](#check-whether-the-virtual-network-is-connected-to-other-resource).</span><span class="sxs-lookup"><span data-stu-id="9d6ee-110">[Check whether hello virtual network is connected tooother resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="9d6ee-111">[Controllare se una macchina virtuale è ancora in esecuzione nella rete virtuale hello](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="9d6ee-111">[Check whether a virtual machine is still running in hello virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="9d6ee-112">[Controllare se la rete virtuale hello è bloccata nella migrazione](#check-whether-the-virtual-network-is-stuck-in-migration).</span><span class="sxs-lookup"><span data-stu-id="9d6ee-112">[Check whether hello virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="9d6ee-113">Passaggi per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="9d6ee-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="9d6ee-114">Verificare se un gateway di rete virtuale è in esecuzione nella rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="9d6ee-114">Check whether a virtual network gateway is running in hello virtual network</span></span>

<span data-ttu-id="9d6ee-115">rete virtuale hello tooremove, è necessario rimuovere prima il gateway di rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-115">tooremove hello virtual network, you must first remove hello virtual network gateway.</span></span>

<span data-ttu-id="9d6ee-116">Per le reti virtuali classiche, visitare toohello **Panoramica** pagina della rete virtuale classica di hello nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-116">For classic virtual networks, go toohello **Overview** page of hello classic virtual network in hello Azure portal.</span></span> <span data-ttu-id="9d6ee-117">In hello **le connessioni VPN** sezione, se il gateway hello è in esecuzione nella rete virtuale hello, verrà visualizzato hello IP indirizzo del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-117">In hello **VPN connections** section, if hello gateway is running in hello virtual network, you will see hello IP address of hello gateway.</span></span> 

![Verificare se il gateway è in esecuzione](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="9d6ee-119">Per le reti virtuali, visitare toohello **Panoramica** pagina della rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-119">For virtual networks, go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="9d6ee-120">Controllare **i dispositivi connessi** per gateway di rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-120">Check **Connected devices** for hello virtual network gateway.</span></span>

![Controllo dispositivo connesso hello](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="9d6ee-122">Prima di poter rimuovere gateway hello, rimuovere innanzitutto qualsiasi **connessione** oggetti nel gateway hello.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-122">Before you can remove hello gateway, first remove any **Connection** objects in hello gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="9d6ee-123">Verificare se un gateway applicazione è in esecuzione nella rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="9d6ee-123">Check whether an application gateway is running in hello virtual network</span></span>

<span data-ttu-id="9d6ee-124">Passare toohello **Panoramica** pagina della rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-124">Go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="9d6ee-125">Controllare hello **i dispositivi connessi** per il gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-125">Check hello **Connected devices** for hello application gateway.</span></span>

![Controllo dispositivo connesso hello](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="9d6ee-127">Se è presente un gateway applicazione, è necessario rimuovere prima di poter eliminare la rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-127">If there is an application gateway, you must remove it before you can delete hello virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a><span data-ttu-id="9d6ee-128">Controllare se il servizio di dominio Azure Active Directory è abilitato nella rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="9d6ee-128">Check whether Azure Active Directory Domain Service is enabled in hello virtual network</span></span>

<span data-ttu-id="9d6ee-129">Se hello servizi di dominio Active Directory è abilitata e connessa toohello rete virtuale, è possibile eliminare questa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-129">If hello Active Directory Domain Service is enabled and connected toohello virtual network, you cannot delete this virtual network.</span></span> 

![Controllo dispositivo connesso hello](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="9d6ee-131">toodisable hello servizio, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="9d6ee-131">toodisable hello service, follow these steps:</span></span>

1. <span data-ttu-id="9d6ee-132">Passare toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9d6ee-132">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="9d6ee-133">Nel riquadro sinistro hello selezionare **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-133">In hello left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="9d6ee-134">Selezionare la directory di Azure Active Directory (Azure AD) hello con Active Directory Domain Services abilitato.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-134">Select hello Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="9d6ee-135">Seleziona hello **configura** scheda.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-135">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="9d6ee-136">In **servizi di dominio**, modificare hello **Abilita servizi di dominio per questa directory** opzione troppo**n**.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-136">Under **domain services**, change hello **Enable domain services for this directory** option too**No**.</span></span>  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a><span data-ttu-id="9d6ee-137">Controllare se la rete virtuale hello è connesso tooother risorse</span><span class="sxs-lookup"><span data-stu-id="9d6ee-137">Check whether hello virtual network is connected tooother resource</span></span>

<span data-ttu-id="9d6ee-138">Controllare i collegamenti del circuito, le connessioni e i peering di rete virtuale,</span><span class="sxs-lookup"><span data-stu-id="9d6ee-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="9d6ee-139">Uno di questi può causare un toofail l'eliminazione di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-139">Any of these can cause a virtual network deletion toofail.</span></span> 

<span data-ttu-id="9d6ee-140">Hello ordine consigliata l'eliminazione è come segue:</span><span class="sxs-lookup"><span data-stu-id="9d6ee-140">hello recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="9d6ee-141">Connessioni del gateway</span><span class="sxs-lookup"><span data-stu-id="9d6ee-141">Gateway connections</span></span>
2. <span data-ttu-id="9d6ee-142">Gateway</span><span class="sxs-lookup"><span data-stu-id="9d6ee-142">Gateways</span></span>
3. <span data-ttu-id="9d6ee-143">Indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="9d6ee-143">IPs</span></span>
4. <span data-ttu-id="9d6ee-144">Peering di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="9d6ee-144">Virtual network peerings</span></span>
5. <span data-ttu-id="9d6ee-145">Ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="9d6ee-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a><span data-ttu-id="9d6ee-146">Controllare se una macchina virtuale è ancora in esecuzione nella rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="9d6ee-146">Check whether a virtual machine is still running in hello virtual network</span></span>

<span data-ttu-id="9d6ee-147">Assicurarsi che nessuna macchina virtuale sia nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-147">Make sure that no virtual machine is in hello virtual network.</span></span>

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="9d6ee-148">Controllare se la rete virtuale hello è bloccata nella migrazione</span><span class="sxs-lookup"><span data-stu-id="9d6ee-148">Check whether hello virtual network is stuck in migration</span></span>

<span data-ttu-id="9d6ee-149">Se la rete virtuale hello è bloccata in uno stato di migrazione, non può essere eliminata.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-149">If hello virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="9d6ee-150">Esecuzione della migrazione hello tooabort comando hello e quindi eliminare la rete virtuale di hello.</span><span class="sxs-lookup"><span data-stu-id="9d6ee-150">Run hello following command tooabort hello migration, and then delete hello virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="9d6ee-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9d6ee-151">Next steps</span></span>

- [<span data-ttu-id="9d6ee-152">Rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="9d6ee-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="9d6ee-153">Domande frequenti sulla rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="9d6ee-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)
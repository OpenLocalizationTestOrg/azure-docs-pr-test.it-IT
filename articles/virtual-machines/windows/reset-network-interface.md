---
title: Come reimpostare l'interfaccia di rete per la VM Windows Azure | Microsoft Docs
description: Illustra come reimpostare l'interfaccia di rete per la VM Windows Azure
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 220e426be20086841854d89831f6c9d67529867f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-network-interface-for-azure-windows-vm"></a><span data-ttu-id="d5952-103">Come reimpostare l'interfaccia di rete per la VM Windows di Azure</span><span class="sxs-lookup"><span data-stu-id="d5952-103">How to reset network interface for Azure Windows VM</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="d5952-104">Non è possibile connettersi alla macchina virtuale (VM) Windows di Microsoft Azure dopo avere disattivato l'interfaccia di rete (NIC) predefinita o si imposta manualmente un indirizzo IP statico per la scheda NIC.</span><span class="sxs-lookup"><span data-stu-id="d5952-104">You cannot connect to Microsoft Azure Windows Virtual Machine (VM) after you disable the default Network Interface (NIC) or manually sets a static IP for the NIC.</span></span> <span data-ttu-id="d5952-105">Questo articolo illustra come reimpostare l'interfaccia di rete per la macchina virtuale Windows di Azure che risolverà il problema della connessione remota.</span><span class="sxs-lookup"><span data-stu-id="d5952-105">This article shows how to reset the network interface for Azure Windows VM, which will resolve the remote connection issue.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a><span data-ttu-id="d5952-106">Reimpostare l'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="d5952-106">Reset network interface</span></span>

### <a name="for-classic-vms"></a><span data-ttu-id="d5952-107">Per VM classiche</span><span class="sxs-lookup"><span data-stu-id="d5952-107">For Classic VMs</span></span>

<span data-ttu-id="d5952-108">Per reimpostare l'interfaccia di rete, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="d5952-108">To reset network interface, follow these steps:</span></span>

1.  <span data-ttu-id="d5952-109">Accedere al [portale di Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d5952-109">Go to the [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="d5952-110">Selezionare **Macchine virtuali (classiche)**.</span><span class="sxs-lookup"><span data-stu-id="d5952-110">Select **Virtual Machines (Classic)**.</span></span>
3.  <span data-ttu-id="d5952-111">Selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d5952-111">Select the affected Virtual Machine.</span></span>
4.  <span data-ttu-id="d5952-112">Selezionare **Indirizzi IP**.</span><span class="sxs-lookup"><span data-stu-id="d5952-112">Select **IP addresses**.</span></span>
5.  <span data-ttu-id="d5952-113">Se l'impostazione **Assegnazione IP privato** non è **Statica**, cambiarla in **Statica**.</span><span class="sxs-lookup"><span data-stu-id="d5952-113">If the **Private IP assignment**  is not  **Static**, change it to **Static**.</span></span>
6.  <span data-ttu-id="d5952-114">Cambiare l'**Indirizzo IP** in un altro indirizzo IP disponibile nella subnet.</span><span class="sxs-lookup"><span data-stu-id="d5952-114">Change the **IP address** to another IP address that is available in the Subnet.</span></span>
7.  <span data-ttu-id="d5952-115">Selezionare Salva.</span><span class="sxs-lookup"><span data-stu-id="d5952-115">Select Save.</span></span>
8.  <span data-ttu-id="d5952-116">La macchina virtuale verrà riavviata per inizializzare la nuova scheda NIC al sistema.</span><span class="sxs-lookup"><span data-stu-id="d5952-116">The virtual machine will restart to initialize the new NIC to the system.</span></span>
9.  <span data-ttu-id="d5952-117">Provare a eseguire RDP al computer in uso.</span><span class="sxs-lookup"><span data-stu-id="d5952-117">Try to RDP to your machine.</span></span> <span data-ttu-id="d5952-118">Se ha esito positivo, è possibile modificare l'indirizzo IP privato originale se si vuole.</span><span class="sxs-lookup"><span data-stu-id="d5952-118">If successful, you can change the Private IP address back to the original if you would like.</span></span> <span data-ttu-id="d5952-119">In caso contrario è possibile mantenerlo.</span><span class="sxs-lookup"><span data-stu-id="d5952-119">Otherwise, you can keep it.</span></span> 

### <a name="for-vms-deployed-in-resource-group-model"></a><span data-ttu-id="d5952-120">Per le VM distribuite nel modello di gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="d5952-120">For VMs deployed in Resource group model</span></span>

1.  <span data-ttu-id="d5952-121">Accedere al [portale di Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d5952-121">Go to the [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="d5952-122">Selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d5952-122">Select the affected Virtual Machine.</span></span>
3.  <span data-ttu-id="d5952-123">Selezionare **Interfacce di rete**.</span><span class="sxs-lookup"><span data-stu-id="d5952-123">Select **Network Interfaces**.</span></span>
4.  <span data-ttu-id="d5952-124">Selezionare l'interfaccia di rete associata al computer</span><span class="sxs-lookup"><span data-stu-id="d5952-124">Select the Network Interface associated with your machine</span></span>
5.  <span data-ttu-id="d5952-125">Selezionare **Configurazioni IP**.</span><span class="sxs-lookup"><span data-stu-id="d5952-125">Select **IP configurations**.</span></span>
6.  <span data-ttu-id="d5952-126">Selezionare l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="d5952-126">Select the IP.</span></span> 
7.  <span data-ttu-id="d5952-127">Se l'impostazione **Assegnazione IP privato** non è **Statica**, cambiarla in **Statica**.</span><span class="sxs-lookup"><span data-stu-id="d5952-127">If the **Private IP assignment**  is not  **Static**, change it to **Static**.</span></span>
8.  <span data-ttu-id="d5952-128">Cambiare l'**Indirizzo IP** in un altro indirizzo IP disponibile nella subnet.</span><span class="sxs-lookup"><span data-stu-id="d5952-128">Change the **IP address** to another IP address that is available in the Subnet.</span></span>
9. <span data-ttu-id="d5952-129">La macchina virtuale verrà riavviata per inizializzare la nuova scheda NIC al sistema.</span><span class="sxs-lookup"><span data-stu-id="d5952-129">The virtual machine will restart to initialize the new NIC to the system.</span></span>
10. <span data-ttu-id="d5952-130">Provare a eseguire RDP al computer in uso.</span><span class="sxs-lookup"><span data-stu-id="d5952-130">Try to RDP to your machine.</span></span> <span data-ttu-id="d5952-131">Se ha esito positivo, è possibile modificare l'indirizzo IP privato originale se si vuole.</span><span class="sxs-lookup"><span data-stu-id="d5952-131">If successful, you can change the Private IP address back to the original if you would like.</span></span> <span data-ttu-id="d5952-132">In caso contrario è possibile mantenerlo.</span><span class="sxs-lookup"><span data-stu-id="d5952-132">Otherwise, you can keep it.</span></span> 

## <a name="delete-the-unavailable-nics"></a><span data-ttu-id="d5952-133">Eliminare le schede di interfaccia non disponibili</span><span class="sxs-lookup"><span data-stu-id="d5952-133">Delete the unavailable NICs</span></span>
<span data-ttu-id="d5952-134">Dopo essere riusciti a eseguire una connessione desktop remoto al computer, è necessario eliminare le schede NIC precedenti per evitare il problema potenziale:</span><span class="sxs-lookup"><span data-stu-id="d5952-134">After you can remote desktop to the machine, you must delete the old NICs to avoid the potential problem:</span></span>

1.  <span data-ttu-id="d5952-135">Aprire Gestione dispositivi.</span><span class="sxs-lookup"><span data-stu-id="d5952-135">Open Device Manager.</span></span>
2.  <span data-ttu-id="d5952-136">Selezionare **Vista** > **Mostra dispositivi nascosti**.</span><span class="sxs-lookup"><span data-stu-id="d5952-136">Select **View** > **Show hidden devices**.</span></span>
3.  <span data-ttu-id="d5952-137">Selezionare **Schede di rete**.</span><span class="sxs-lookup"><span data-stu-id="d5952-137">Select **Network Adapters**.</span></span> 
4.  <span data-ttu-id="d5952-138">Controllare le schede di rete con un nome simile a "Scheda di rete Microsoft Hyper-V".</span><span class="sxs-lookup"><span data-stu-id="d5952-138">Check for the adapters named as "Microsoft Hyper-V Network Adapter".</span></span>
5.  <span data-ttu-id="d5952-139">Si potrebbe vedere una scheda non disponibile che appare in grigio.</span><span class="sxs-lookup"><span data-stu-id="d5952-139">You might see an unavailable adapter that is grayed out.</span></span> <span data-ttu-id="d5952-140">Fare clic con pulsante destro del mouse sulla scheda e selezionare Disinstalla.</span><span class="sxs-lookup"><span data-stu-id="d5952-140">Right-click the adapter and then select Uninstall.</span></span>

    ![immagine della scheda NIC](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > <span data-ttu-id="d5952-142">Disinstallare solo le schede non disponibili con il nome "Scheda di rete Microsoft Hyper-V".</span><span class="sxs-lookup"><span data-stu-id="d5952-142">Only uninstall the unavailable adapters that have the name "Microsoft Hyper-V Network Adapter".</span></span> <span data-ttu-id="d5952-143">Se si disinstalla una delle altre schede nascoste, ciò potrebbe provocare altri problemi.</span><span class="sxs-lookup"><span data-stu-id="d5952-143">If you uninstall any of the other hidden adapters, it could cause additional issues.</span></span>
    >
    >

6.  <span data-ttu-id="d5952-144">Ora tutte le schede disponibili devono essere eliminate dal sistema.</span><span class="sxs-lookup"><span data-stu-id="d5952-144">Now all unavailable adapter should be cleared out from your system.</span></span>
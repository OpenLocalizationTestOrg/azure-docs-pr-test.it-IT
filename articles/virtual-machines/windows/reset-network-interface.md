---
title: aaaHow tooreset di interfaccia di rete per la macchina virtuale Windows Azure | Documenti Microsoft
description: Viene illustrato come tooreset interfaccia di rete per la macchina virtuale Windows Azure
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
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a><span data-ttu-id="8d0dc-103">Come tooreset interfaccia di rete per la macchina virtuale Windows Azure</span><span class="sxs-lookup"><span data-stu-id="8d0dc-103">How tooreset network interface for Azure Windows VM</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="8d0dc-104">È Impossibile connettersi tooMicrosoft macchina virtuale Windows Azure (VM) dopo aver disabilitato predefinito hello interfaccia di rete (NIC) o si imposta manualmente un indirizzo IP statico per una scheda di rete hello.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-104">You cannot connect tooMicrosoft Azure Windows Virtual Machine (VM) after you disable hello default Network Interface (NIC) or manually sets a static IP for hello NIC.</span></span> <span data-ttu-id="8d0dc-105">Questo articolo illustra come tooreset hello interfaccia di rete per la macchina virtuale Windows Azure, che consentirà di risolvere il problema di connessione remota hello.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-105">This article shows how tooreset hello network interface for Azure Windows VM, which will resolve hello remote connection issue.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a><span data-ttu-id="8d0dc-106">Reimpostare l'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="8d0dc-106">Reset network interface</span></span>

### <a name="for-classic-vms"></a><span data-ttu-id="8d0dc-107">Per VM classiche</span><span class="sxs-lookup"><span data-stu-id="8d0dc-107">For Classic VMs</span></span>

<span data-ttu-id="8d0dc-108">rete tooreset interfaccia, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="8d0dc-108">tooreset network interface, follow these steps:</span></span>

1.  <span data-ttu-id="8d0dc-109">Passare toohello [portale di Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8d0dc-109">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="8d0dc-110">Selezionare **Macchine virtuali (classiche)**.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-110">Select **Virtual Machines (Classic)**.</span></span>
3.  <span data-ttu-id="8d0dc-111">Seleziona hello interessate macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-111">Select hello affected Virtual Machine.</span></span>
4.  <span data-ttu-id="8d0dc-112">Selezionare **Indirizzi IP**.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-112">Select **IP addresses**.</span></span>
5.  <span data-ttu-id="8d0dc-113">Se hello **assegnazione IP privato** non **statico**, modificarlo troppo**statico**.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-113">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
6.  <span data-ttu-id="8d0dc-114">Hello modifica **indirizzo IP** indirizzo IP tooanother disponibile in hello Subnet.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-114">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
7.  <span data-ttu-id="8d0dc-115">Selezionare Salva.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-115">Select Save.</span></span>
8.  <span data-ttu-id="8d0dc-116">macchina virtuale Hello riavvierà tooinitialize hello nuovo NIC toohello sistema.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-116">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
9.  <span data-ttu-id="8d0dc-117">Provare a tooRDP tooyour macchina.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-117">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="8d0dc-118">Se ha esito positivo, è possibile modificare hello IP privato indirizzo back toohello originale se si desidera.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-118">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="8d0dc-119">In caso contrario è possibile mantenerlo.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-119">Otherwise, you can keep it.</span></span> 

### <a name="for-vms-deployed-in-resource-group-model"></a><span data-ttu-id="8d0dc-120">Per le VM distribuite nel modello di gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="8d0dc-120">For VMs deployed in Resource group model</span></span>

1.  <span data-ttu-id="8d0dc-121">Passare toohello [portale di Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8d0dc-121">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="8d0dc-122">Seleziona hello interessate macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-122">Select hello affected Virtual Machine.</span></span>
3.  <span data-ttu-id="8d0dc-123">Selezionare **Interfacce di rete**.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-123">Select **Network Interfaces**.</span></span>
4.  <span data-ttu-id="8d0dc-124">Selezionare hello che associato all'interfaccia di rete con il computer</span><span class="sxs-lookup"><span data-stu-id="8d0dc-124">Select hello Network Interface associated with your machine</span></span>
5.  <span data-ttu-id="8d0dc-125">Selezionare **Configurazioni IP**.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-125">Select **IP configurations**.</span></span>
6.  <span data-ttu-id="8d0dc-126">Selezionare IP hello.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-126">Select hello IP.</span></span> 
7.  <span data-ttu-id="8d0dc-127">Se hello **assegnazione IP privato** non **statico**, modificarlo troppo**statico**.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-127">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
8.  <span data-ttu-id="8d0dc-128">Hello modifica **indirizzo IP** indirizzo IP tooanother disponibile in hello Subnet.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-128">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
9. <span data-ttu-id="8d0dc-129">macchina virtuale Hello riavvierà tooinitialize hello nuovo NIC toohello sistema.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-129">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
10. <span data-ttu-id="8d0dc-130">Provare a tooRDP tooyour macchina.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-130">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="8d0dc-131">Se ha esito positivo, è possibile modificare hello IP privato indirizzo back toohello originale se si desidera.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-131">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="8d0dc-132">In caso contrario è possibile mantenerlo.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-132">Otherwise, you can keep it.</span></span> 

## <a name="delete-hello-unavailable-nics"></a><span data-ttu-id="8d0dc-133">Eliminare hello schede di rete non disponibile</span><span class="sxs-lookup"><span data-stu-id="8d0dc-133">Delete hello unavailable NICs</span></span>
<span data-ttu-id="8d0dc-134">Dopo che è possibile macchina toohello desktop remoto, è necessario eliminare hello precedente NIC tooavoid hello potenziale problema:</span><span class="sxs-lookup"><span data-stu-id="8d0dc-134">After you can remote desktop toohello machine, you must delete hello old NICs tooavoid hello potential problem:</span></span>

1.  <span data-ttu-id="8d0dc-135">Aprire Gestione dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-135">Open Device Manager.</span></span>
2.  <span data-ttu-id="8d0dc-136">Selezionare **Vista** > **Mostra dispositivi nascosti**.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-136">Select **View** > **Show hidden devices**.</span></span>
3.  <span data-ttu-id="8d0dc-137">Selezionare **Schede di rete**.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-137">Select **Network Adapters**.</span></span> 
4.  <span data-ttu-id="8d0dc-138">Controllo per le schede di hello denominata come "Scheda di rete Microsoft Hyper-V".</span><span class="sxs-lookup"><span data-stu-id="8d0dc-138">Check for hello adapters named as "Microsoft Hyper-V Network Adapter".</span></span>
5.  <span data-ttu-id="8d0dc-139">Si potrebbe vedere una scheda non disponibile che appare in grigio. Il pulsante destro adapter hello e quindi scegliere Disinstalla.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-139">You might see an unavailable adapter that is grayed out. Right-click hello adapter and then select Uninstall.</span></span>

    ![immagine di Hello di hello NIC](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > <span data-ttu-id="8d0dc-141">Disinstallare solo le schede disponibili hello con nome hello "Scheda di rete Microsoft Hyper-V".</span><span class="sxs-lookup"><span data-stu-id="8d0dc-141">Only uninstall hello unavailable adapters that have hello name "Microsoft Hyper-V Network Adapter".</span></span> <span data-ttu-id="8d0dc-142">Se si disinstalla uno qualsiasi dei hello altre schede nascoste, potrebbe provocare altri problemi.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-142">If you uninstall any of hello other hidden adapters, it could cause additional issues.</span></span>
    >
    >

6.  <span data-ttu-id="8d0dc-143">Ora tutte le schede disponibili devono essere eliminate dal sistema.</span><span class="sxs-lookup"><span data-stu-id="8d0dc-143">Now all unavailable adapter should be cleared out from your system.</span></span>
---
title: 'Azure Active Directory Domain Services: Introduzione | Microsoft Docs'
description: Abilitare Azure Active Directory Domain Services utilizzando hello del portale di Azure (anteprima)
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="74d0a-103">Abilitare Azure Active Directory Domain Services utilizzando hello del portale di Azure (anteprima)</span><span class="sxs-lookup"><span data-stu-id="74d0a-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="74d0a-104">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="74d0a-104">Before you begin</span></span>
<span data-ttu-id="74d0a-105">Fare riferimento troppo[considerazioni sulla rete per Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="74d0a-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="74d0a-106">Attività 2: configurare le impostazioni di rete</span><span class="sxs-lookup"><span data-stu-id="74d0a-106">Task 2: configure network settings</span></span>
<span data-ttu-id="74d0a-107">attività di configurazione successiva Hello è toocreate una rete virtuale di Azure e una subnet dedicata all'interno di esso.</span><span class="sxs-lookup"><span data-stu-id="74d0a-107">hello next configuration task is toocreate an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="74d0a-108">Abilitare Azure Active Directory Domain Services in questa subnet all'interno della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="74d0a-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="74d0a-109">È anche possibile selezionare una rete virtuale esistente e creare subnet hello dedicata all'interno di esso.</span><span class="sxs-lookup"><span data-stu-id="74d0a-109">You may also pick an existing virtual network and create hello dedicated subnet within it.</span></span>

1. <span data-ttu-id="74d0a-110">Fare clic su **rete virtuale** tooselect una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="74d0a-110">Click **Virtual network** tooselect a virtual network.</span></span>
2. <span data-ttu-id="74d0a-111">In hello **rete virtuale scegliere** pannello viene visualizzato di tutte le reti virtuali esistenti.</span><span class="sxs-lookup"><span data-stu-id="74d0a-111">On hello **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="74d0a-112">Viene visualizzato solo hello reti virtuali che appartengono al gruppo di risorse toohello e località di Azure selezionato nell'hello **nozioni di base** pagina della procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="74d0a-112">You see only hello virtual networks that belong toohello resource group and Azure location you have selected on hello **Basics** wizard page.</span></span>

3. <span data-ttu-id="74d0a-113">Scegliere hello di rete virtuale in cui i servizi di dominio Active Directory di Azure devono essere abilitati.</span><span class="sxs-lookup"><span data-stu-id="74d0a-113">Choose hello virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="74d0a-114">Fare clic su **Crea nuovo**, se si preferisce toocreate una nuova rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="74d0a-114">Click **Create new**, if you prefer toocreate a new virtual network.</span></span> <span data-ttu-id="74d0a-115">È consigliabile l'utilizzo di una subnet dedicata per Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="74d0a-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="74d0a-116">Se si seleziona una rete virtuale esistente, [creare una subnet dedicata con estensione reti virtuali hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) , quindi selezionare la subnet.</span><span class="sxs-lookup"><span data-stu-id="74d0a-116">If you pick an existing virtual network, [create a dedicated subnet using hello virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![Selezionare una rete virtuale](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="74d0a-118">Fare clic su **Subnet** toopick hello subnet dedicata in questa rete virtuale, all'interno delle quali tooenable nuova gestiti dominio.</span><span class="sxs-lookup"><span data-stu-id="74d0a-118">Click **Subnet** toopick hello dedicated subnet in this virtual network, within which tooenable your new managed domain.</span></span> <span data-ttu-id="74d0a-119">In hello **creare subnet** pannello, specificare un nome per la subnet hello e fare clic su **OK** al termine.</span><span class="sxs-lookup"><span data-stu-id="74d0a-119">In hello **Create subnet** blade, specify a name for hello subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="74d0a-120">Ad esempio, creare una subnet con nome hello 'DomainServices', consentendo agli altri amministratori toounderstand ciò che viene distribuito all'interno di subnet hello.</span><span class="sxs-lookup"><span data-stu-id="74d0a-120">For example, create a subnet with hello name 'DomainServices', making it easy for other administrators toounderstand what is deployed within hello subnet.</span></span>

    ![Selezionare subnet all'interno di rete virtuale hello](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="74d0a-122">**Linee guida per la selezione di una subnet**</span><span class="sxs-lookup"><span data-stu-id="74d0a-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="74d0a-123">Usare una subnet dedicata per Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="74d0a-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="74d0a-124">Non distribuire qualsiasi altra subnet toothis di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="74d0a-124">Do not deploy any other virtual machines toothis subnet.</span></span> <span data-ttu-id="74d0a-125">Questa configurazione consente tooconfigure rete sicurezza gruppi per le macchine virtuali o i carichi di lavoro senza interromperne il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="74d0a-125">This configuration enables you tooconfigure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="74d0a-126">Per i dettagli vedere [Considerazioni sulla rete per Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="74d0a-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="74d0a-127">Non selezionare subnet del Gateway hello per la distribuzione di servizi di dominio Active Directory di Azure, perché non è una configurazione supportata.</span><span class="sxs-lookup"><span data-stu-id="74d0a-127">Do not select hello Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="74d0a-128">Verificare che tale subnet hello selezionata dispone di sufficiente spazio degli indirizzi disponibile - indirizzi IP disponibili almeno 3-5.</span><span class="sxs-lookup"><span data-stu-id="74d0a-128">Ensure that hello subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="74d0a-129">Al termine, fare clic su **OK** toomove su toohello **gruppo amministratore** pagina della procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="74d0a-129">When you are done, click **OK** toomove on toohello **Administrator group** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="74d0a-130">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="74d0a-130">Next step</span></span>
[<span data-ttu-id="74d0a-131">Attività 3: configurare un gruppo amministrativo e abilitare Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="74d0a-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)

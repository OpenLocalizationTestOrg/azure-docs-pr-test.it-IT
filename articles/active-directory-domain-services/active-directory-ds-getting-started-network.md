---
title: 'Azure Active Directory Domain Services: Introduzione | Microsoft Docs'
description: Abilitare Azure Active Directory Domain Services tramite il portale di Azure (anteprima)
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
ms.openlocfilehash: 7f420d60862adf61e4f21e5abac2932a742bd55d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="5f5d5-103">Abilitare Azure Active Directory Domain Services tramite il portale di Azure (anteprima)</span><span class="sxs-lookup"><span data-stu-id="5f5d5-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="5f5d5-104">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="5f5d5-104">Before you begin</span></span>
<span data-ttu-id="5f5d5-105">Fare riferimento a [Considerazioni sulla rete per Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="5f5d5-105">Refer to [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="5f5d5-106">Attività 2: configurare le impostazioni di rete</span><span class="sxs-lookup"><span data-stu-id="5f5d5-106">Task 2: configure network settings</span></span>
<span data-ttu-id="5f5d5-107">L'attività di configurazione successiva consiste nel creare una rete virtuale di Azure e la relativa subnet dedicata.</span><span class="sxs-lookup"><span data-stu-id="5f5d5-107">The next configuration task is to create an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="5f5d5-108">Abilitare Azure Active Directory Domain Services in questa subnet all'interno della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="5f5d5-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="5f5d5-109">È anche possibile selezionare una rete virtuale esistente e creare la subnet dedicata all'interno di essa.</span><span class="sxs-lookup"><span data-stu-id="5f5d5-109">You may also pick an existing virtual network and create the dedicated subnet within it.</span></span>

1. <span data-ttu-id="5f5d5-110">Fare clic su **Rete virtuale** per selezionare una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="5f5d5-110">Click **Virtual network** to select a virtual network.</span></span>
2. <span data-ttu-id="5f5d5-111">Nel pannello **Scegli rete virtuale** vengono visualizzate tutte le reti virtuali esistenti.</span><span class="sxs-lookup"><span data-stu-id="5f5d5-111">On the **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="5f5d5-112">Vengono visualizzate solamente le reti virtuali che appartengono al gruppo di risorse e la posizione di Azure selezionata nella pagina di procedura guidata **Nozioni di base**.</span><span class="sxs-lookup"><span data-stu-id="5f5d5-112">You see only the virtual networks that belong to the resource group and Azure location you have selected on the **Basics** wizard page.</span></span>

3. <span data-ttu-id="5f5d5-113">Scegliere la rete virtuale in cui abilitare Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="5f5d5-113">Choose the virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="5f5d5-114">Fare clic su **Crea nuovo** se si preferisce creare una nuova rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="5f5d5-114">Click **Create new**, if you prefer to create a new virtual network.</span></span> <span data-ttu-id="5f5d5-115">È consigliabile l'utilizzo di una subnet dedicata per Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="5f5d5-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="5f5d5-116">Se si seleziona una rete virtuale esistente, [creare una subnet dedicata usando l'estensione di reti virtuali](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), quindi selezionare la subnet.</span><span class="sxs-lookup"><span data-stu-id="5f5d5-116">If you pick an existing virtual network, [create a dedicated subnet using the virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![Selezionare una rete virtuale](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="5f5d5-118">Fare clic su **Subnet** per selezionare una subnet dedicata in questa rete virtuale, all'interno della quale è possibile attivare il nuovo dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="5f5d5-118">Click **Subnet** to pick the dedicated subnet in this virtual network, within which to enable your new managed domain.</span></span> <span data-ttu-id="5f5d5-119">Nel pannello **Crea subnet**, specificare un nome per la subnet e per concludere fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5f5d5-119">In the **Create subnet** blade, specify a name for the subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="5f5d5-120">Ad esempio, se si crea una subnet con il nome 'DomainServices', è più semplice per gli altri amministratori comprendere cosa viene implementato all'interno della subnet.</span><span class="sxs-lookup"><span data-stu-id="5f5d5-120">For example, create a subnet with the name 'DomainServices', making it easy for other administrators to understand what is deployed within the subnet.</span></span>

    ![Selezionare una subnet all’interno della rete virtuale](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="5f5d5-122">**Linee guida per la selezione di una subnet**</span><span class="sxs-lookup"><span data-stu-id="5f5d5-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="5f5d5-123">Usare una subnet dedicata per Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="5f5d5-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="5f5d5-124">Non distribuire eventuali altre macchine virtuali per questa subnet.</span><span class="sxs-lookup"><span data-stu-id="5f5d5-124">Do not deploy any other virtual machines to this subnet.</span></span> <span data-ttu-id="5f5d5-125">Questa configurazione consente di configurare gruppi di sicurezza di rete per le macchine virtuali/carichi di lavoro senza interromperne il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="5f5d5-125">This configuration enables you to configure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="5f5d5-126">Per i dettagli vedere [Considerazioni sulla rete per Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="5f5d5-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="5f5d5-127">Non selezionare la subnet del Gateway per l’implementazione di Azure AD Domain Services poiché non si tratta di una configurazione supportata.</span><span class="sxs-lookup"><span data-stu-id="5f5d5-127">Do not select the Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="5f5d5-128">Verificare che la subnet selezionata disponga di sufficiente spazio per gli indirizzi (almeno 3-5 indirizzi IP disponibili).</span><span class="sxs-lookup"><span data-stu-id="5f5d5-128">Ensure that the subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="5f5d5-129">Al termine, fare clic su **OK** per passare alla pagina **Gruppo amministratore** della procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="5f5d5-129">When you are done, click **OK** to move on to the **Administrator group** page of the wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="5f5d5-130">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="5f5d5-130">Next step</span></span>
[<span data-ttu-id="5f5d5-131">Attività 3: configurare un gruppo amministrativo e abilitare Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="5f5d5-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)

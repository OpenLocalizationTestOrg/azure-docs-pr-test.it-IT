---
title: Configurare una rete virtuale per Azure DevTest Labs | Documentazione Microsoft
description: Informazioni su come configurare una rete virtuale esistente e una subnet e utilizzarle in una VM con Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 848752085729df7d98a3a4b7be36d894c12cd033
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="cf626-103">Configurare una rete virtuale per Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="cf626-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="cf626-104">Come illustrato nell'articolo [Aggiungere una VM con elementi a un lab](devtest-lab-add-vm-with-artifacts.md), quando si crea una VM in un lab, è possibile specificare una rete virtuale configurata.</span><span class="sxs-lookup"><span data-stu-id="cf626-104">As explained in the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="cf626-105">Questo potrebbe essere utile, ad esempio, per accedere alle risorse di rete aziendali dalle VM usando la rete virtuale configurata con ExpressRoute o VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="cf626-105">One scenario for doing this is if you need to access your corpnet resources from your VMs using the virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="cf626-106">Le sezioni seguenti illustrano come aggiungere la rete virtuale esistente alle impostazioni della rete virtuale di un lab in modo che sia disponibile al momento della creazione delle VM.</span><span class="sxs-lookup"><span data-stu-id="cf626-106">The following sections illustrate how to add your existing virtual network into a lab's Virtual Network settings so that it is available to choose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-the-azure-portal"></a><span data-ttu-id="cf626-107">Configurare una rete virtuale per un lab con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cf626-107">Configure a virtual network for a lab using the Azure portal</span></span>
<span data-ttu-id="cf626-108">I passaggi seguenti descrivono la procedura per aggiungere una rete virtuale esistente (e una subnet) a un lab in modo che sia disponibile al momento della creazione di una VM nel lab.</span><span class="sxs-lookup"><span data-stu-id="cf626-108">The following steps walk you through adding an existing virtual network (and subnet) to a lab so that it can be used when creating a VM in the same lab.</span></span> 

1. <span data-ttu-id="cf626-109">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="cf626-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="cf626-110">Selezionare **Altri servizi** e quindi **DevTest Labs** dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="cf626-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="cf626-111">Nell'elenco dei lab selezionare il lab desiderato.</span><span class="sxs-lookup"><span data-stu-id="cf626-111">From the list of labs, select the desired lab.</span></span> 
4. <span data-ttu-id="cf626-112">Nel pannello del lab selezionare **Configurazione**.</span><span class="sxs-lookup"><span data-stu-id="cf626-112">On the lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="cf626-113">Nel pannello **Configurazione** del lab selezionare **Reti virtuali**.</span><span class="sxs-lookup"><span data-stu-id="cf626-113">On the lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="cf626-114">Nel pannello **Reti virtuali** viene visualizzato l'elenco delle reti virtuali configurate per il lab corrente, come pure la rete virtuale predefinita creata per il lab.</span><span class="sxs-lookup"><span data-stu-id="cf626-114">On the **Virtual networks** blade, you see a list of virtual networks configured for the current lab as well as the default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="cf626-115">Selezionare **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cf626-115">Select **+ Add**.</span></span>
   
    ![Aggiungere una rete virtuale esistente al lab](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="cf626-117">Nel pannello **Rete virtuale** selezionare **[Select virtual network]** (Seleziona rete virtuale).</span><span class="sxs-lookup"><span data-stu-id="cf626-117">On the **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![Selezionare una rete virtuale esistente](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="cf626-119">Nel pannello **Scegli rete virtuale** selezionare la rete virtuale desiderata.</span><span class="sxs-lookup"><span data-stu-id="cf626-119">On the **Choose virtual network** blade, select the desired virtual network.</span></span> <span data-ttu-id="cf626-120">Il pannello mostra tutte le reti virtuali presenti nella stessa area nella sottoscrizione del lab.</span><span class="sxs-lookup"><span data-stu-id="cf626-120">The blade shows all the virtual networks that are under the same region in the subscription as the lab.</span></span>  
10. <span data-ttu-id="cf626-121">Dopo aver selezionato una rete virtuale, viene visualizzato nuovamente il pannello **Rete virtuale**. Fare clic sulla subnet nell'elenco nella parte inferiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="cf626-121">After selecting a virtual network, you are returned to the **Virtual network** Click the subnet in the list at the bottom of the blade.</span></span>

    ![Elenco di subnet](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="cf626-123">Viene visualizzato il pannello Lab subnet (Subnet lab).</span><span class="sxs-lookup"><span data-stu-id="cf626-123">The Lab Subnet blade is displayed.</span></span>

    ![Pannello Lab Subnet (Subnet lab)](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="cf626-125">Specificare un **nome per la subnet del lab**.</span><span class="sxs-lookup"><span data-stu-id="cf626-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="cf626-126">Per consentire l'uso di una subnet nella creazione della macchina virtuale del lab, selezionare **Use in virtual machine creation** (Usa nella creazione di macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="cf626-126">To allow a subnet to be used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="cf626-127">Per abilitare un [indirizzo IP pubblico condiviso](devtest-lab-shared-ip.md), selezionare **Enable shared public IP** (Abilita indirizzo IP pubblico condiviso).</span><span class="sxs-lookup"><span data-stu-id="cf626-127">To enable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="cf626-128">Per consentire gli indirizzi IP pubblici in una subnet, selezionare **Allow public IP creation** (Consenti la creazione di un indirizzo IP pubblico).</span><span class="sxs-lookup"><span data-stu-id="cf626-128">To allow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="cf626-129">Nel campo **Maximum virtual machines per user** (Numero massimo di macchine virtuali per utente) specificare per ogni utente il numero massimo di macchine virtuali per ogni subnet.</span><span class="sxs-lookup"><span data-stu-id="cf626-129">In the **Maximum virtual machines per user** field, specify the maximum VMs per user for each subnet.</span></span> <span data-ttu-id="cf626-130">Se si desidera un numero illimitato di VM, lasciare vuoto questo campo.</span><span class="sxs-lookup"><span data-stu-id="cf626-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="cf626-131">Selezionare **OK** per chiudere il pannello Lab Subnet (Subnet lab).</span><span class="sxs-lookup"><span data-stu-id="cf626-131">Select **OK** to close the Lab Subnet blade.</span></span>
17. <span data-ttu-id="cf626-132">Selezionare **Salva** per chiudere il pannello Rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="cf626-132">Select **Save** to close the Virtual network blade.</span></span>
18. <span data-ttu-id="cf626-133">Dopo aver configurato la rete virtuale, è possibile selezionarla quando si crea una VM.</span><span class="sxs-lookup"><span data-stu-id="cf626-133">Now that the virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="cf626-134">Per informazioni su come creare una VM e specificare una rete virtuale, vedere l'articolo [Aggiungere una VM con elementi a un lab](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="cf626-134">To see how to create a VM and specify a virtual network, refer to the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="cf626-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cf626-135">Next steps</span></span>
<span data-ttu-id="cf626-136">Dopo avere aggiunto la rete virtuale desiderata al lab, il passaggio successivo consiste nell' [aggiungere una VM a un lab](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="cf626-136">Once you have added the desired virtual network to your lab, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>


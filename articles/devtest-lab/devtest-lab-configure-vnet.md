---
title: una rete virtuale in Azure DevTest Labs aaaConfigure | Documenti Microsoft
description: Informazioni su come tooconfigure una subnet e la rete virtuale esistente e usati in una macchina virtuale con Azure DevTest Labs
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
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="85dab-103">Configurare una rete virtuale per Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="85dab-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="85dab-104">Come illustrato nell'articolo hello [aggiungere una macchina virtuale con lab tooa elementi](devtest-lab-add-vm-with-artifacts.md), quando si crea una macchina virtuale in un lab, è possibile specificare una rete virtuale configurata.</span><span class="sxs-lookup"><span data-stu-id="85dab-104">As explained in hello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="85dab-105">Uno scenario per eseguire questa operazione è se è necessario tooaccess le risorse di rete aziendale dalle macchine virtuali utilizzando hello rete virtuale che è stato configurato con ExpressRoute o VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="85dab-105">One scenario for doing this is if you need tooaccess your corpnet resources from your VMs using hello virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="85dab-106">Hello nelle sezioni seguenti viene illustrato come tooadd la rete virtuale esistente nelle impostazioni di rete virtuale dell'ambiente di test in modo che sia disponibile toochoose durante la creazione di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="85dab-106">hello following sections illustrate how tooadd your existing virtual network into a lab's Virtual Network settings so that it is available toochoose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a><span data-ttu-id="85dab-107">Configurare una rete virtuale per un ambiente lab tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="85dab-107">Configure a virtual network for a lab using hello Azure portal</span></span>
<span data-ttu-id="85dab-108">Hello passaggi seguenti consentono di aggiungere un laboratorio di tooa rete (e la subnet) virtuale esistente in modo che può essere utilizzato durante la creazione di una macchina virtuale in hello lab stesso.</span><span class="sxs-lookup"><span data-stu-id="85dab-108">hello following steps walk you through adding an existing virtual network (and subnet) tooa lab so that it can be used when creating a VM in hello same lab.</span></span> 

1. <span data-ttu-id="85dab-109">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="85dab-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="85dab-110">Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="85dab-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="85dab-111">Elenco dei laboratori hello selezionare lab desiderato hello.</span><span class="sxs-lookup"><span data-stu-id="85dab-111">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="85dab-112">Nel pannello del lab hello, selezionare **configurazione**.</span><span class="sxs-lookup"><span data-stu-id="85dab-112">On hello lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="85dab-113">Nel lab di hello **configurazione** pannello seleziona **le reti virtuali**.</span><span class="sxs-lookup"><span data-stu-id="85dab-113">On hello lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="85dab-114">In hello **le reti virtuali** pannello viene visualizzato un elenco di reti virtuali configurate per lab corrente hello nonché hello predefinito rete virtuale creata per l'ambiente lab.</span><span class="sxs-lookup"><span data-stu-id="85dab-114">On hello **Virtual networks** blade, you see a list of virtual networks configured for hello current lab as well as hello default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="85dab-115">Selezionare **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="85dab-115">Select **+ Add**.</span></span>
   
    ![Aggiungere un laboratorio di tooyour di rete virtuale esistente](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="85dab-117">In hello **rete virtuale** pannello seleziona **[rete virtuale selezionare]**.</span><span class="sxs-lookup"><span data-stu-id="85dab-117">On hello **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![Selezionare una rete virtuale esistente](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="85dab-119">In hello **rete virtuale scegliere** blade, rete virtuale desiderato selezionare hello.</span><span class="sxs-lookup"><span data-stu-id="85dab-119">On hello **Choose virtual network** blade, select hello desired virtual network.</span></span> <span data-ttu-id="85dab-120">Pannello Hello Mostra tutte le reti virtuali hello che sono in hello stessa regione nella sottoscrizione hello lab hello.</span><span class="sxs-lookup"><span data-stu-id="85dab-120">hello blade shows all hello virtual networks that are under hello same region in hello subscription as hello lab.</span></span>  
10. <span data-ttu-id="85dab-121">Dopo aver selezionato una rete virtuale, viene visualizzato toohello **rete virtuale** clic hello subnet nell'elenco di hello nella parte inferiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="85dab-121">After selecting a virtual network, you are returned toohello **Virtual network** Click hello subnet in hello list at hello bottom of hello blade.</span></span>

    ![Elenco di subnet](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="85dab-123">viene visualizzato il pannello di Subnet Lab Hello.</span><span class="sxs-lookup"><span data-stu-id="85dab-123">hello Lab Subnet blade is displayed.</span></span>

    ![Pannello Lab Subnet (Subnet lab)](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="85dab-125">Specificare un **nome per la subnet del lab**.</span><span class="sxs-lookup"><span data-stu-id="85dab-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="85dab-126">tooallow toobe una subnet usati nel lab la creazione di VM, selezionare **utilizzare nella creazione della macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="85dab-126">tooallow a subnet toobe used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="85dab-127">tooenable un [condiviso l'indirizzo IP pubblico](devtest-lab-shared-ip.md)selezionare **Abilita condivisa IP pubblico**.</span><span class="sxs-lookup"><span data-stu-id="85dab-127">tooenable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="85dab-128">tooallow gli indirizzi IP pubblici in una subnet, selezionare **consentire la creazione di IP pubblica**.</span><span class="sxs-lookup"><span data-stu-id="85dab-128">tooallow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="85dab-129">In hello **massimo di macchine virtuali per utente** specificare hello massime macchine virtuali per utente per ogni subnet.</span><span class="sxs-lookup"><span data-stu-id="85dab-129">In hello **Maximum virtual machines per user** field, specify hello maximum VMs per user for each subnet.</span></span> <span data-ttu-id="85dab-130">Se si desidera un numero illimitato di VM, lasciare vuoto questo campo.</span><span class="sxs-lookup"><span data-stu-id="85dab-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="85dab-131">Selezionare **OK** blade di Subnet Lab tooclose hello.</span><span class="sxs-lookup"><span data-stu-id="85dab-131">Select **OK** tooclose hello Lab Subnet blade.</span></span>
17. <span data-ttu-id="85dab-132">Selezionare **salvare** blade di rete virtuale hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="85dab-132">Select **Save** tooclose hello Virtual network blade.</span></span>
18. <span data-ttu-id="85dab-133">Ora che hello rete virtuale è configurata, può essere selezionato quando si crea una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="85dab-133">Now that hello virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="85dab-134">toosee come toocreate una macchina virtuale e specificare una rete virtuale, vedere l'articolo toohello [aggiungere una macchina virtuale con lab tooa elementi](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="85dab-134">toosee how toocreate a VM and specify a virtual network, refer toohello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="85dab-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="85dab-135">Next steps</span></span>
<span data-ttu-id="85dab-136">Dopo aver aggiunto hello desiderato lab tooyour di rete virtuale, hello è troppo[aggiungere un ambiente lab tooyour VM](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="85dab-136">Once you have added hello desired virtual network tooyour lab, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>


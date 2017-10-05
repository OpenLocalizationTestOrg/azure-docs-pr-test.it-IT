---
title: Gestire le formule in Azure DevTest Labs per creare VM | Microsoft Docs
description: Informazioni su come aggiornare e rimuovere le formule di Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfdab5def50158f9b764bbb1e50c2624cc6d5fb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="67f71-103">Gestire le formule di Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="67f71-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="67f71-104">In questo articolo viene illustrato come creare una formula da una base (immagine personalizzata, immagine del Marketplace o un'altra formula) o da una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="67f71-104">This article illustrates how to create a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="67f71-105">Questo articolo illustra inoltre la gestione delle formule esistenti.</span><span class="sxs-lookup"><span data-stu-id="67f71-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="67f71-106">Creare una formula</span><span class="sxs-lookup"><span data-stu-id="67f71-106">Create a formula</span></span>
<span data-ttu-id="67f71-107">Tutti gli utenti con autorizzazione *Utenti* per i lab di sviluppo/test possono creare macchine virtuali usando una formula come base.</span><span class="sxs-lookup"><span data-stu-id="67f71-107">Anyone with DevTest Labs *Users* permissions is able to create VMs using a formula as a base.</span></span> <span data-ttu-id="67f71-108">È possibile creare le formule in due modi:</span><span class="sxs-lookup"><span data-stu-id="67f71-108">There are two ways to create formulas:</span></span> 

* <span data-ttu-id="67f71-109">Da una base: quando si vogliono definire tutte le caratteristiche della formula.</span><span class="sxs-lookup"><span data-stu-id="67f71-109">From a base - Use when you want to define all the characteristics of the formula.</span></span>
* <span data-ttu-id="67f71-110">Da una macchina virtuale di lab già esistente: quando si vuole creare una formula basata sulle impostazioni di una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="67f71-110">From an existing lab VM - Use when you want to create a formula based on the settings of an existing VM.</span></span>

<span data-ttu-id="67f71-111">Per altre informazioni sull'aggiunta di utenti e autorizzazioni, vedere [Aggiungere proprietari e utenti in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="67f71-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="67f71-112">Creare una formula di base</span><span class="sxs-lookup"><span data-stu-id="67f71-112">Create a formula from a base</span></span>
<span data-ttu-id="67f71-113">Nella procedura seguente sono descritti i passaggi per creare una formula da un'immagine personalizzata, un'immagine Marketplace o un'altra formula.</span><span class="sxs-lookup"><span data-stu-id="67f71-113">The following steps guide you through the process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="67f71-114">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="67f71-114">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="67f71-115">Selezionare **Altri servizi** e quindi **DevTest Labs** dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="67f71-115">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>

3. <span data-ttu-id="67f71-116">Nell'elenco dei lab selezionare il lab desiderato.</span><span class="sxs-lookup"><span data-stu-id="67f71-116">From the list of labs, select the desired lab.</span></span>  

4. <span data-ttu-id="67f71-117">Nel pannello del lab selezionare **Formule (basi riutilizzabili)**.</span><span class="sxs-lookup"><span data-stu-id="67f71-117">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menu Formula](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="67f71-119">Nel pannello **Formule** selezionare **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="67f71-119">On the **Formulas** blade, select **+ Add**.</span></span>
   
    ![Aggiungere una formula](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="67f71-121">Nel pannello **Scegli una base** selezionare la base (immagine personalizzata, immagine Marketplace o formula) da cui si desidera creare la formula.</span><span class="sxs-lookup"><span data-stu-id="67f71-121">On the **Choose a base** blade, select the base (custom image, Marketplace image, or formula) from which you want to create the formula.</span></span>
   
    ![Elenco base](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="67f71-123">Specificare i valori seguenti nel pannello **Crea formula** :</span><span class="sxs-lookup"><span data-stu-id="67f71-123">On the **Create formula** blade, specify the following values:</span></span>
   
    * <span data-ttu-id="67f71-124">**Nome formula** : immettere un nome per la formula.</span><span class="sxs-lookup"><span data-stu-id="67f71-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="67f71-125">Questo valore verrà visualizzato nell'elenco delle immagini di base quando si crea una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67f71-125">This value is displayed in the list of base images when you create a VM.</span></span> <span data-ttu-id="67f71-126">Il nome viene convalidato durante la digitazione e, se non è valido, un messaggio indicherà i requisiti per un nome valido.</span><span class="sxs-lookup"><span data-stu-id="67f71-126">The name is validated as you type it, and if not valid, a message indicates the requirements for a valid name.</span></span>
    * <span data-ttu-id="67f71-127">**Descrizione** : immettere una descrizione significativa per la formula.</span><span class="sxs-lookup"><span data-stu-id="67f71-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="67f71-128">Questo valore è disponibile dal menu di scelta rapida della formula quando si crea una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67f71-128">This value is available from the formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="67f71-129">**Nome utente** - Immettere un nome utente a cui siano concessi i privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="67f71-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="67f71-130">**Password** : immettere o scegliere dall'elenco a discesa un valore associato al segreto (password) che si desidera usare per l'utente specificato.</span><span class="sxs-lookup"><span data-stu-id="67f71-130">**Password** - Enter - or select from the dropdown - a value that is associated with the secret (password) that you want to use for the specified user.</span></span> <span data-ttu-id="67f71-131">Per altre informazioni sui segreti, vedere [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/) (Azure DevTest Labs: archivio personale dei segreti).</span><span class="sxs-lookup"><span data-stu-id="67f71-131">For more information about the secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="67f71-132">**Virtual machine disk type** (Tipo di disco della macchina virtuale) - Specificare l'unità disco rigido o l'unità SSD per indicare quale tipo di disco di archiviazione sia consentito per le macchine virtuali il cui provisioning è stato effettuato usando questa immagine di base.</span><span class="sxs-lookup"><span data-stu-id="67f71-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) to indicate which storage disk type is allowed for the virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="67f71-133">**Dimensioni macchina virtuale** - Selezionare uno degli elementi predefiniti che specificano le memorie centrali del processore, le dimensioni della RAM e le dimensioni dell'unità disco rigido della macchina virtuale da creare.</span><span class="sxs-lookup"><span data-stu-id="67f71-133">** Virtual machine size** - Select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span> 
    * <span data-ttu-id="67f71-134">**Elementi** - Selezionare questa opzione per aprire il pannello **Aggiungi elementi** nel quale è possibile selezionare e configurare gli elementi da aggiungere all'immagine di base.</span><span class="sxs-lookup"><span data-stu-id="67f71-134">**Artifacts** - Select to open the **Add artifacts** blade, in which you select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="67f71-135">Per altre informazioni sugli elementi, vedere [Gestire elementi di macchine virtuali in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="67f71-135">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="67f71-136">**Impostazioni avanzate** - Selezionare questa opzione per aprire il pannello **Avanzate** in cui è possibile configurare le impostazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="67f71-136">**Advanced settings** - Select to open the **Advanced** blade where you configure the following settings:</span></span>
        * <span data-ttu-id="67f71-137">**Rete virtuale** : specificare la rete virtuale desiderata.</span><span class="sxs-lookup"><span data-stu-id="67f71-137">**Virtual network** - Specify the desired virtual network.</span></span>
        * <span data-ttu-id="67f71-138">**Subnet** : specificare la subnet desiderata.</span><span class="sxs-lookup"><span data-stu-id="67f71-138">**Subnet** - Specify the desired subnet.</span></span>    
        * <span data-ttu-id="67f71-139">**Configurazione indirizzi IP** - Specificare se si desidera l'indirizzo IP pubblico, privato o condiviso.</span><span class="sxs-lookup"><span data-stu-id="67f71-139">**IP address configuration** - Specify if you want the Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="67f71-140">Per altre informazioni sugli indirizzi IP condivisi, vedere [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md) (Informazioni sugli indirizzi IP condivisi in Azure Devtest Labs).</span><span class="sxs-lookup"><span data-stu-id="67f71-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="67f71-141">**Make this machine claimable** (Rendi attestabile questa macchina) - Rendere "attestabile" una macchina significa che non le sarà assegnata la proprietà al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="67f71-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at the time of creation.</span></span> <span data-ttu-id="67f71-142">Gli utenti del lab saranno invece in grado di assumere la proprietà ("attestazione") della macchina nel pannello del lab.</span><span class="sxs-lookup"><span data-stu-id="67f71-142">Instead lab users will be able to take ownership ("claim") the machine in the lab's blade.</span></span>     
    * <span data-ttu-id="67f71-143">**Immagine** : questo campo visualizza il nome dell'immagine di base selezionata nel pannello precedente.</span><span class="sxs-lookup"><span data-stu-id="67f71-143">**Image** - This field displays name of the base image you selected on the previous blade.</span></span> 
     
       ![Crea formula](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="67f71-145">Selezionare **Crea** per creare la formula.</span><span class="sxs-lookup"><span data-stu-id="67f71-145">Select **Create** to create the formula.</span></span>

9. <span data-ttu-id="67f71-146">Dopo essere stata creata, la formula viene visualizzata nell'elenco del pannello **Formule**.</span><span class="sxs-lookup"><span data-stu-id="67f71-146">When the formula has been created, it displays in the list on the **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="67f71-147">Creare una formula da una VM</span><span class="sxs-lookup"><span data-stu-id="67f71-147">Create a formula from a VM</span></span>
<span data-ttu-id="67f71-148">La procedura seguente consente di creare una formula basata su una macchina virtuale già esistente.</span><span class="sxs-lookup"><span data-stu-id="67f71-148">The following steps guide you through the process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="67f71-149">Per creare una formula da una VM, la VM deve essere stata creata dopo il 30 marzo 2016.</span><span class="sxs-lookup"><span data-stu-id="67f71-149">To create a formula from a VM, the VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="67f71-150">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="67f71-150">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="67f71-151">Selezionare **Altri servizi** e quindi **DevTest Labs** dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="67f71-151">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="67f71-152">Nell'elenco dei lab selezionare il lab desiderato.</span><span class="sxs-lookup"><span data-stu-id="67f71-152">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="67f71-153">Nel pannello **Panoramica** del lab selezionare la VM dalla quale creare la formula.</span><span class="sxs-lookup"><span data-stu-id="67f71-153">On the lab's **Overview** blade, select the VM from which you wish to create the formula.</span></span>
   
    ![Macchine virtuali di lab](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="67f71-155">Nel pannello della VM selezionare **Crea formula (base riutilizzabile)**.</span><span class="sxs-lookup"><span data-stu-id="67f71-155">On the VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![Crea formula](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="67f71-157">Nel pannello **Crea formula** compilare i campi **Name** (Nome) e **Description** (Descrizione) della nuova formula.</span><span class="sxs-lookup"><span data-stu-id="67f71-157">On the **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![Pannello Crea formula](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="67f71-159">Fare clic su **OK** per creare la formula.</span><span class="sxs-lookup"><span data-stu-id="67f71-159">Select **OK** to create the formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="67f71-160">Modificare una formula</span><span class="sxs-lookup"><span data-stu-id="67f71-160">Modify a formula</span></span>
<span data-ttu-id="67f71-161">Per modificare una formula, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="67f71-161">To modify a formula, follow these steps:</span></span>

1. <span data-ttu-id="67f71-162">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="67f71-162">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="67f71-163">Selezionare **Altri servizi** e quindi **DevTest Labs** dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="67f71-163">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="67f71-164">Nell'elenco dei lab selezionare il lab desiderato.</span><span class="sxs-lookup"><span data-stu-id="67f71-164">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="67f71-165">Nel pannello del lab selezionare **Formule (basi riutilizzabili)**.</span><span class="sxs-lookup"><span data-stu-id="67f71-165">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menu Formula](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="67f71-167">Nel pannello **Formule lab** selezionare la formula che si vuole modificare.</span><span class="sxs-lookup"><span data-stu-id="67f71-167">On the **Lab formulas** blade, select the formula you wish to modify.</span></span>
6. <span data-ttu-id="67f71-168">Apportare le modifiche nel pannello **Update formula** (Aggiorna formula) e selezionare **Update** (Aggiorna).</span><span class="sxs-lookup"><span data-stu-id="67f71-168">On the **Update formula** blade, make the desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="67f71-169">Eliminare una formula</span><span class="sxs-lookup"><span data-stu-id="67f71-169">Delete a formula</span></span>
<span data-ttu-id="67f71-170">Per eliminare una formula, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="67f71-170">To delete a formula, follow these steps:</span></span>

1. <span data-ttu-id="67f71-171">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="67f71-171">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="67f71-172">Selezionare **Altri servizi** e quindi **DevTest Labs** dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="67f71-172">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="67f71-173">Nell'elenco dei lab selezionare il lab desiderato.</span><span class="sxs-lookup"><span data-stu-id="67f71-173">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="67f71-174">Nel pannello **Settings** (Impostazioni) del lab selezionare **Formulas** (Formule).</span><span class="sxs-lookup"><span data-stu-id="67f71-174">On the lab **Settings** blade, select **Formulas**.</span></span>
   
    ![Menu Formula](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="67f71-176">Nel pannello **Formule lab** selezionare i puntini di sospensione a destra della formula da eliminare.</span><span class="sxs-lookup"><span data-stu-id="67f71-176">On the **Lab formulas** blade, select the ellipsis to the right of the formula you wish to delete.</span></span>
   
    ![Menu Formula](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="67f71-178">Selezionare **Elimina**dal menu di scelta rapida della formula.</span><span class="sxs-lookup"><span data-stu-id="67f71-178">On the formula's context menu, select **Delete**.</span></span>
   
    ![Menu di scelta rapida Formula](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="67f71-180">Selezionare **Sì** nella finestra di dialogo di conferma dell'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="67f71-180">Select **Yes** to the deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="67f71-181">Post di blog correlati</span><span class="sxs-lookup"><span data-stu-id="67f71-181">Related blog posts</span></span>
* [<span data-ttu-id="67f71-182">Custom images or formulas? (Immagini personalizzate o formule?)</span><span class="sxs-lookup"><span data-stu-id="67f71-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="67f71-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67f71-183">Next steps</span></span>
<span data-ttu-id="67f71-184">Dopo avere creato una formula da usare durante la creazione di una macchina virtuale, il passaggio successivo consiste nell'[aggiungere una macchina virtuale al lab](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="67f71-184">Once you have created a formula for use when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>


---
title: le formule aaaManage in Azure DevTest Labs toocreate macchine virtuali | Documenti Microsoft
description: Informazioni su come tooupdate e rimuovere le formule Azure DevTest Labs
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
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="22792-103">Gestire le formule di Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="22792-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="22792-104">Questo articolo illustra come toocreate una formula da una base (immagine personalizzata, un'immagine del Marketplace o un'altra formula) o una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="22792-104">This article illustrates how toocreate a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="22792-105">Questo articolo illustra inoltre la gestione delle formule esistenti.</span><span class="sxs-lookup"><span data-stu-id="22792-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="22792-106">Creare una formula</span><span class="sxs-lookup"><span data-stu-id="22792-106">Create a formula</span></span>
<span data-ttu-id="22792-107">Chiunque disponga di DevTest Labs *utenti* autorizzazioni è macchine virtuali in grado di toocreate utilizzando una formula come base.</span><span class="sxs-lookup"><span data-stu-id="22792-107">Anyone with DevTest Labs *Users* permissions is able toocreate VMs using a formula as a base.</span></span> <span data-ttu-id="22792-108">Esistono due modi toocreate formule:</span><span class="sxs-lookup"><span data-stu-id="22792-108">There are two ways toocreate formulas:</span></span> 

* <span data-ttu-id="22792-109">Da una base - utilizzare quando si desidera toodefine tutte le caratteristiche di hello della formula hello.</span><span class="sxs-lookup"><span data-stu-id="22792-109">From a base - Use when you want toodefine all hello characteristics of hello formula.</span></span>
* <span data-ttu-id="22792-110">Da un ambiente lab esistente VM - utilizzare questa opzione quando si desidera toocreate una formula in base alle impostazioni di hello di una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="22792-110">From an existing lab VM - Use when you want toocreate a formula based on hello settings of an existing VM.</span></span>

<span data-ttu-id="22792-111">Per altre informazioni sull'aggiunta di utenti e autorizzazioni, vedere [Aggiungere proprietari e utenti in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="22792-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="22792-112">Creare una formula di base</span><span class="sxs-lookup"><span data-stu-id="22792-112">Create a formula from a base</span></span>
<span data-ttu-id="22792-113">Hello alla procedura seguente illustra il processo di hello di creazione di una formula da un'immagine personalizzata, un'immagine del Marketplace o da un'altra formula.</span><span class="sxs-lookup"><span data-stu-id="22792-113">hello following steps guide you through hello process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="22792-114">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="22792-114">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="22792-115">Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="22792-115">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>

3. <span data-ttu-id="22792-116">Elenco dei laboratori hello selezionare lab desiderato hello.</span><span class="sxs-lookup"><span data-stu-id="22792-116">From hello list of labs, select hello desired lab.</span></span>  

4. <span data-ttu-id="22792-117">Nel pannello del lab hello, selezionare **formule (base riutilizzabile)**.</span><span class="sxs-lookup"><span data-stu-id="22792-117">On hello lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menu Formula](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="22792-119">In hello **formule** pannello seleziona **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="22792-119">On hello **Formulas** blade, select **+ Add**.</span></span>
   
    ![Aggiungere una formula](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="22792-121">In hello **scegliere una base** base selezionare hello (immagine personalizzata, un'immagine del Marketplace o formula) da cui si desidera formula hello toocreate pannello.</span><span class="sxs-lookup"><span data-stu-id="22792-121">On hello **Choose a base** blade, select hello base (custom image, Marketplace image, or formula) from which you want toocreate hello formula.</span></span>
   
    ![Elenco base](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="22792-123">In hello **creare formula** pannello specificare hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="22792-123">On hello **Create formula** blade, specify hello following values:</span></span>
   
    * <span data-ttu-id="22792-124">**Nome formula** : immettere un nome per la formula.</span><span class="sxs-lookup"><span data-stu-id="22792-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="22792-125">Questo valore viene visualizzato nell'elenco di hello di immagini di base quando si crea una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="22792-125">This value is displayed in hello list of base images when you create a VM.</span></span> <span data-ttu-id="22792-126">nome Hello viene convalidato durante la digitazione e, se non è valido, un messaggio significa requisiti hello per un nome valido.</span><span class="sxs-lookup"><span data-stu-id="22792-126">hello name is validated as you type it, and if not valid, a message indicates hello requirements for a valid name.</span></span>
    * <span data-ttu-id="22792-127">**Descrizione** : immettere una descrizione significativa per la formula.</span><span class="sxs-lookup"><span data-stu-id="22792-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="22792-128">Questo valore è disponibile dal menu di scelta rapida della formula hello quando si crea una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="22792-128">This value is available from hello formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="22792-129">**Nome utente** - Immettere un nome utente a cui siano concessi i privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="22792-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="22792-130">**Password** - immettere - o selezionare dall'elenco a discesa hello - valore associata al segreto hello (password) che si desidera toouse per utente specificato hello.</span><span class="sxs-lookup"><span data-stu-id="22792-130">**Password** - Enter - or select from hello dropdown - a value that is associated with hello secret (password) that you want toouse for hello specified user.</span></span> <span data-ttu-id="22792-131">Per ulteriori informazioni su segreti hello, vedere [Azure DevTest Labs: archivio segreto personale](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span><span class="sxs-lookup"><span data-stu-id="22792-131">For more information about hello secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="22792-132">**Tipo di disco di macchina virtuale** : specificare l'unità disco rigido (disco rigido) o l'archiviazione su disco di tipo tooindicate di unità SSD (Solid-State) è consentita per le macchine virtuali hello eseguito il provisioning con questa immagine di base.</span><span class="sxs-lookup"><span data-stu-id="22792-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) tooindicate which storage disk type is allowed for hello virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="22792-133">* * Macchina virtuale dimensioni * * - selezionare uno degli elementi di hello predefinito che specificano le dimensioni del disco rigido hello di hello VM toocreate core del processore hello e dimensioni della RAM.</span><span class="sxs-lookup"><span data-stu-id="22792-133">** Virtual machine size** - Select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span> 
    * <span data-ttu-id="22792-134">**Elementi** -tooopen selezionare hello **aggiungere elementi** pannello, in cui selezionare e configurare hello elementi che si desidera tooadd toohello immagine di base.</span><span class="sxs-lookup"><span data-stu-id="22792-134">**Artifacts** - Select tooopen hello **Add artifacts** blade, in which you select and configure hello artifacts that you want tooadd toohello base image.</span></span> <span data-ttu-id="22792-135">Per altre informazioni sugli elementi, vedere [Gestire elementi di macchine virtuali in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="22792-135">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="22792-136">**Impostazioni avanzate** -tooopen selezionare hello **avanzate** pannello in cui configurare hello seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="22792-136">**Advanced settings** - Select tooopen hello **Advanced** blade where you configure hello following settings:</span></span>
        * <span data-ttu-id="22792-137">**Rete virtuale** -è necessario specificare hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="22792-137">**Virtual network** - Specify hello desired virtual network.</span></span>
        * <span data-ttu-id="22792-138">**Subnet** -specificare la subnet hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="22792-138">**Subnet** - Specify hello desired subnet.</span></span>    
        * <span data-ttu-id="22792-139">**Configurazione degli indirizzi IP** -specificare se si desidera che gli indirizzi IP condiviso, privata o pubblica hello.</span><span class="sxs-lookup"><span data-stu-id="22792-139">**IP address configuration** - Specify if you want hello Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="22792-140">Per altre informazioni sugli indirizzi IP condivisi, vedere [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md) (Informazioni sugli indirizzi IP condivisi in Azure Devtest Labs).</span><span class="sxs-lookup"><span data-stu-id="22792-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="22792-141">**Rendere questa macchina claimable** -effettua una macchina "claimable" significa che sarà non assegnato proprietà in fase di creazione di hello.</span><span class="sxs-lookup"><span data-stu-id="22792-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at hello time of creation.</span></span> <span data-ttu-id="22792-142">Gli utenti saranno possibile macchina di hello tootake in grado di proprietà ("attestazioni") nel pannello del lab hello.</span><span class="sxs-lookup"><span data-stu-id="22792-142">Instead lab users will be able tootake ownership ("claim") hello machine in hello lab's blade.</span></span>     
    * <span data-ttu-id="22792-143">**Immagine** -questo campo consente di visualizzare nome dell'immagine di base hello selezionato nel pannello precedente hello.</span><span class="sxs-lookup"><span data-stu-id="22792-143">**Image** - This field displays name of hello base image you selected on hello previous blade.</span></span> 
     
       ![Crea formula](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="22792-145">Selezionare **crea** formula hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="22792-145">Select **Create** toocreate hello formula.</span></span>

9. <span data-ttu-id="22792-146">Quando la formula hello è stata creata, viene visualizzato nell'elenco hello hello **formule** blade.</span><span class="sxs-lookup"><span data-stu-id="22792-146">When hello formula has been created, it displays in hello list on hello **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="22792-147">Creare una formula da una VM</span><span class="sxs-lookup"><span data-stu-id="22792-147">Create a formula from a VM</span></span>
<span data-ttu-id="22792-148">Hello passaggi seguenti consentono di eseguire il processo di hello di creazione di una formula basata su una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="22792-148">hello following steps guide you through hello process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="22792-149">toocreate una formula da una macchina virtuale, hello VM deve essere stato creato dopo il 30 marzo 2016.</span><span class="sxs-lookup"><span data-stu-id="22792-149">toocreate a formula from a VM, hello VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="22792-150">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="22792-150">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="22792-151">Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="22792-151">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="22792-152">Elenco dei laboratori hello selezionare lab desiderato hello.</span><span class="sxs-lookup"><span data-stu-id="22792-152">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="22792-153">Nel lab di hello **Panoramica** pannello selezionare hello VM da cui si desidera formula hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="22792-153">On hello lab's **Overview** blade, select hello VM from which you wish toocreate hello formula.</span></span>
   
    ![Macchine virtuali di lab](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="22792-155">Nel pannello hello della macchina virtuale, selezionare **creare formula (base riutilizzabile)**.</span><span class="sxs-lookup"><span data-stu-id="22792-155">On hello VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![Crea formula](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="22792-157">In hello **creare formula** pannello, immettere un **nome** e **descrizione** per la nuova formula.</span><span class="sxs-lookup"><span data-stu-id="22792-157">On hello **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![Pannello Crea formula](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="22792-159">Selezionare **OK** formula hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="22792-159">Select **OK** toocreate hello formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="22792-160">Modificare una formula</span><span class="sxs-lookup"><span data-stu-id="22792-160">Modify a formula</span></span>
<span data-ttu-id="22792-161">toomodify una formula, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="22792-161">toomodify a formula, follow these steps:</span></span>

1. <span data-ttu-id="22792-162">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="22792-162">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="22792-163">Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="22792-163">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="22792-164">Elenco dei laboratori hello selezionare lab desiderato hello.</span><span class="sxs-lookup"><span data-stu-id="22792-164">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="22792-165">Nel pannello del lab hello, selezionare **formule (base riutilizzabile)**.</span><span class="sxs-lookup"><span data-stu-id="22792-165">On hello lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menu Formula](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="22792-167">In hello **formule Lab** blade, formula hello selezionare desiderato toomodify.</span><span class="sxs-lookup"><span data-stu-id="22792-167">On hello **Lab formulas** blade, select hello formula you wish toomodify.</span></span>
6. <span data-ttu-id="22792-168">In hello **aggiorna formula** pannello hello lo si desidera modificare e selezionare **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="22792-168">On hello **Update formula** blade, make hello desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="22792-169">Eliminare una formula</span><span class="sxs-lookup"><span data-stu-id="22792-169">Delete a formula</span></span>
<span data-ttu-id="22792-170">toodelete una formula, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="22792-170">toodelete a formula, follow these steps:</span></span>

1. <span data-ttu-id="22792-171">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="22792-171">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="22792-172">Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="22792-172">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="22792-173">Elenco dei laboratori hello selezionare lab desiderato hello.</span><span class="sxs-lookup"><span data-stu-id="22792-173">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="22792-174">Lab hello **impostazioni** pannello seleziona **formule**.</span><span class="sxs-lookup"><span data-stu-id="22792-174">On hello lab **Settings** blade, select **Formulas**.</span></span>
   
    ![Menu Formula](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="22792-176">In hello **formule Lab** blade, hello selezionare i puntini di sospensione toohello destra della formula hello desiderato toodelete.</span><span class="sxs-lookup"><span data-stu-id="22792-176">On hello **Lab formulas** blade, select hello ellipsis toohello right of hello formula you wish toodelete.</span></span>
   
    ![Menu Formula](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="22792-178">Selezionare il menu di scelta rapida della formula hello **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="22792-178">On hello formula's context menu, select **Delete**.</span></span>
   
    ![Menu di scelta rapida Formula](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="22792-180">Selezionare **Sì** toohello finestra di dialogo Conferma eliminazione.</span><span class="sxs-lookup"><span data-stu-id="22792-180">Select **Yes** toohello deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="22792-181">Post di blog correlati</span><span class="sxs-lookup"><span data-stu-id="22792-181">Related blog posts</span></span>
* [<span data-ttu-id="22792-182">Custom images or formulas? (Immagini personalizzate o formule?)</span><span class="sxs-lookup"><span data-stu-id="22792-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="22792-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="22792-183">Next steps</span></span>
<span data-ttu-id="22792-184">Dopo aver creato una formula da utilizzare durante la creazione di una macchina virtuale, hello è troppo[aggiungere un ambiente lab tooyour VM](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="22792-184">Once you have created a formula for use when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>


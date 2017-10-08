---
title: immagini di macchina virtuale con Azure PowerShell hello personalizzate aaaCreate | Documenti Microsoft
description: 'Esercitazione: creare un''immagine di macchina virtuale personalizzata utilizzando hello Azure PowerShell.'
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a><span data-ttu-id="3fb8f-103">Creare un'immagine personalizzata di una VM di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="3fb8f-103">Create a custom image of an Azure VM using PowerShell</span></span>

<span data-ttu-id="3fb8f-104">Le immagini personalizzate sono come le immagini di marketplace, ma si possono creare autonomamente.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="3fb8f-105">Immagini personalizzate possono essere utilizzati toobootstrap configurazioni, ad esempio il precaricamento di applicazioni, configurazioni dell'applicazione e altre configurazioni del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="3fb8f-106">In questa esercitazione viene creata un'immagine personalizzata di una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="3fb8f-107">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="3fb8f-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3fb8f-108">Eseguire Sysprep e generalizzare le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="3fb8f-108">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="3fb8f-109">Creare un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="3fb8f-109">Create a custom image</span></span>
> * <span data-ttu-id="3fb8f-110">Creare una VM da un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="3fb8f-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="3fb8f-111">Elenco di tutte le immagini di hello nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="3fb8f-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="3fb8f-112">Eliminare un'immagine</span><span class="sxs-lookup"><span data-stu-id="3fb8f-112">Delete an image</span></span>

<span data-ttu-id="3fb8f-113">Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="3fb8f-114">Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="3fb8f-115">Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="3fb8f-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3fb8f-116">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="3fb8f-116">Before you begin</span></span>

<span data-ttu-id="3fb8f-117">passaggi di Hello riportati di seguito in dettaglio come tootake una macchina virtuale esistente e attivare i dati in un oggetto personalizzato riutilizzabile immagine che si possono usare toocreate nuove istanze di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="3fb8f-118">esempio di hello toocomplete in questa esercitazione, è necessario disporre di una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="3fb8f-119">Se necessario, questo [script di esempio](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) può crearne una appositamente.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-119">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="3fb8f-120">Quando il lavoro esercitazione hello, sostituire il gruppo di risorse di hello e VM nomi dove necessario.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="prepare-vm"></a><span data-ttu-id="3fb8f-121">Preparare la VM</span><span class="sxs-lookup"><span data-stu-id="3fb8f-121">Prepare VM</span></span>

<span data-ttu-id="3fb8f-122">toocreate un'immagine di una macchina virtuale, è necessario tooprepare hello VM da hello generalizzazione macchina virtuale, la deallocazione e quindi contrassegnare origine hello VM come generalizzata in Azure.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-122">toocreate an image of a virtual machine, you need tooprepare hello VM by generalizing hello VM, deallocating, and then marking hello source VM as generalized in Azure.</span></span>

### <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="3fb8f-123">Generalizzare hello macchina virtuale di Windows tramite Sysprep</span><span class="sxs-lookup"><span data-stu-id="3fb8f-123">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="3fb8f-124">Sysprep consente di rimuovere tutte le informazioni sull'account personale, tra le altre cose e lo prepara hello macchina toobe utilizzato come immagine.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-124">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="3fb8f-125">Per ulteriori informazioni su Sysprep, vedere [come tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="3fb8f-125">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>


1. <span data-ttu-id="3fb8f-126">Connessione macchina virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-126">Connect toohello virtual machine.</span></span>
2. <span data-ttu-id="3fb8f-127">Aprire una finestra del prompt dei comandi hello come amministratore.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-127">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="3fb8f-128">Modificare anche le directory hello*%windir%\system32\sysprep*, quindi eseguire *sysprep.exe*.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-128">Change hello directory too*%windir%\system32\sysprep*, and then run *sysprep.exe*.</span></span>
3. <span data-ttu-id="3fb8f-129">In hello **System Preparation Tool** nella finestra di dialogo *immettere sistema Out-of-Box guidata*e assicurarsi che tale hello *Generalize* casella di controllo è selezionata.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-129">In hello **System Preparation Tool** dialog box, select *Enter System Out-of-Box Experience (OOBE)*, and make sure that hello *Generalize* check box is selected.</span></span>
4. <span data-ttu-id="3fb8f-130">In **Opzioni di arresto** selezionare *Arresta il sistema* e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-130">In **Shutdown Options**, select *Shutdown* and then click **OK**.</span></span>
5. <span data-ttu-id="3fb8f-131">Al termine di Sysprep, arresta macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-131">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="3fb8f-132">**Non si riavvia hello VM**.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-132">**Do not restart hello VM**.</span></span>

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="3fb8f-133">Rilasciare e contrassegnare hello VM come generalizzato</span><span class="sxs-lookup"><span data-stu-id="3fb8f-133">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="3fb8f-134">toocreate un'immagine, hello VM deve toobe deallocato e contrassegnati come generalizzata in Azure.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-134">toocreate an image, hello VM needs toobe deallocated and marked as generalized in Azure.</span></span>

<span data-ttu-id="3fb8f-135">Hello deallocata VM utilizzando [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="3fb8f-135">Deallocated hello VM using [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

<span data-ttu-id="3fb8f-136">Impostare lo stato di hello della macchina virtuale hello troppo`-Generalized` utilizzando [Set AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="3fb8f-136">Set hello status of hello virtual machine too`-Generalized` using [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span></span> 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a><span data-ttu-id="3fb8f-137">Creare l'immagine di hello</span><span class="sxs-lookup"><span data-stu-id="3fb8f-137">Create hello image</span></span>

<span data-ttu-id="3fb8f-138">Ora è possibile creare un'immagine di macchina virtuale hello utilizzando [New AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) e [New AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span><span class="sxs-lookup"><span data-stu-id="3fb8f-138">Now you can create an image of hello VM by using [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) and [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span></span> <span data-ttu-id="3fb8f-139">esempio Hello crea un'immagine denominata *myImage* da una macchina virtuale denominata *myVM*.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-139">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>

<span data-ttu-id="3fb8f-140">Ottenere una macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-140">Get hello virtual machine.</span></span> 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

<span data-ttu-id="3fb8f-141">Creare una configurazione immagine hello.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-141">Create hello image configuration.</span></span>

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

<span data-ttu-id="3fb8f-142">Creare l'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-142">Create hello image.</span></span>

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="3fb8f-143">Creare macchine virtuali da immagini hello</span><span class="sxs-lookup"><span data-stu-id="3fb8f-143">Create VMs from hello image</span></span>

<span data-ttu-id="3fb8f-144">Dopo aver creato un'immagine, è possibile creare nuove macchine virtuali dall'immagine hello.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-144">Now that you have an image, you can create one or more new VMs from hello image.</span></span> <span data-ttu-id="3fb8f-145">Creazione di una macchina virtuale da un'immagine personalizzata è molto simile toocreating una macchina virtuale usando un'immagine del Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-145">Creating a VM from a custom image is very similar toocreating a VM using a Marketplace image.</span></span> <span data-ttu-id="3fb8f-146">Quando si utilizza un'immagine del Marketplace, è necessario tooinformation sull'immagine di hello, provider di immagini, offerta, SKU e versione.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-146">When you use a Marketplace image, you have tooinformation about hello image, image provider, offer, SKU and version.</span></span> <span data-ttu-id="3fb8f-147">Con un'immagine personalizzata, è sufficiente tooprovide hello ID della risorsa immagine personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-147">With a custom image, you just need tooprovide hello ID of hello custom image resource.</span></span> 

<span data-ttu-id="3fb8f-148">In hello lo script seguente, si crea una variabile *$image* toostore informazioni sull'utilizzo di immagine personalizzata hello [Get AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) e quindi si utilizza [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)e specificare l'ID di hello utilizzando hello *$image* variabile appena creata.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-148">In hello following script, we create a variable *$image* toostore information about hello custom image using [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) and then we use [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) and specify hello ID using hello *$image* variable we just created.</span></span> 

<span data-ttu-id="3fb8f-149">script di Hello crea una macchina virtuale denominata *myVMfromImage* dal nostro immagine personalizzata in un nuovo gruppo di risorse denominato *myResourceGroupFromImage* in hello *Stati Uniti occidentali* percorso.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-149">hello script creates a VM named *myVMfromImage* from our custom image in a new resource group named *myResourceGroupFromImage* in hello *West US* location.</span></span>


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

  $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a><span data-ttu-id="3fb8f-150">Gestione delle immagini</span><span class="sxs-lookup"><span data-stu-id="3fb8f-150">Image management</span></span> 

<span data-ttu-id="3fb8f-151">Di seguito sono riportati alcuni esempi di attività di immagine di gestione comuni e come toocomplete loro tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-151">Here are some examples of common management image tasks and how toocomplete them using PowerShell.</span></span>

<span data-ttu-id="3fb8f-152">Elencare tutte le immagini per nome.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-152">List all images by name.</span></span>

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

<span data-ttu-id="3fb8f-153">Eliminare un'immagine.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-153">Delete an image.</span></span> <span data-ttu-id="3fb8f-154">In questo esempio elimina hello immagine denominata *myOldImage* da hello *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-154">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="3fb8f-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3fb8f-155">Next steps</span></span>

<span data-ttu-id="3fb8f-156">In questa esercitazione è stata creata un'immagine di macchina virtuale personalizzata.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-156">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="3fb8f-157">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="3fb8f-157">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3fb8f-158">Eseguire Sysprep e generalizzare le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="3fb8f-158">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="3fb8f-159">Creare un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="3fb8f-159">Create a custom image</span></span>
> * <span data-ttu-id="3fb8f-160">Creare una VM da un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="3fb8f-160">Create a VM from a custom image</span></span>
> * <span data-ttu-id="3fb8f-161">Elenco di tutte le immagini di hello nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="3fb8f-161">List all hello images in your subscription</span></span>
> * <span data-ttu-id="3fb8f-162">Eliminare un'immagine</span><span class="sxs-lookup"><span data-stu-id="3fb8f-162">Delete an image</span></span>

<span data-ttu-id="3fb8f-163">Spostare toohello Avanti toolearn esercitazione sulle macchine virtuali a disponibilità elevata come.</span><span class="sxs-lookup"><span data-stu-id="3fb8f-163">Advance toohello next tutorial toolearn about how highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3fb8f-164">Creare VM a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="3fb8f-164">Create highly available VMs</span></span>](tutorial-availability-sets.md)




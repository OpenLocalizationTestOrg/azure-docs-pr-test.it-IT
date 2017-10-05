---
title: Creare immagini di VM personalizzate con Azure PowerShell | Documentazione Microsoft
description: 'Esercitazione: creare un''immagine di VM personalizzata con Azure PowerShell.'
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
ms.openlocfilehash: 96be2872a902a7d7063bf1dff7b4ca209a5b67c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a><span data-ttu-id="2aa67-103">Creare un'immagine personalizzata di una VM di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="2aa67-103">Create a custom image of an Azure VM using PowerShell</span></span>

<span data-ttu-id="2aa67-104">Le immagini personalizzate sono come le immagini di marketplace, ma si possono creare autonomamente.</span><span class="sxs-lookup"><span data-stu-id="2aa67-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="2aa67-105">Le immagini personalizzate possono essere usate per le configurazioni di avvio, ad esempio il precaricamento e le configurazioni di applicazioni e altre configurazioni del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="2aa67-105">Custom images can be used to bootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="2aa67-106">In questa esercitazione viene creata un'immagine personalizzata di una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2aa67-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="2aa67-107">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="2aa67-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2aa67-108">Eseguire Sysprep e generalizzare le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="2aa67-108">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="2aa67-109">Creare un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="2aa67-109">Create a custom image</span></span>
> * <span data-ttu-id="2aa67-110">Creare una VM da un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="2aa67-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="2aa67-111">Elencare tutte le immagini nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="2aa67-111">List all the images in your subscription</span></span>
> * <span data-ttu-id="2aa67-112">Eliminare un'immagine</span><span class="sxs-lookup"><span data-stu-id="2aa67-112">Delete an image</span></span>

<span data-ttu-id="2aa67-113">Questa esercitazione richiede il modulo Azure PowerShell 3.6 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="2aa67-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="2aa67-114">Eseguire ` Get-Module -ListAvailable AzureRM` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="2aa67-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="2aa67-115">Se è necessario eseguire l'aggiornamento, vedere [Installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="2aa67-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2aa67-116">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="2aa67-116">Before you begin</span></span>

<span data-ttu-id="2aa67-117">La procedura riportata di seguito illustra come prendere una VM esistente e convertirla in un'immagine personalizzata riutilizzabile che è possibile usare per creare nuove istanze di VM.</span><span class="sxs-lookup"><span data-stu-id="2aa67-117">The steps below detail how to take an existing VM and turn it into a re-usable custom image that you can use to create new VM instances.</span></span>

<span data-ttu-id="2aa67-118">Per completare l'esempio contenuto in questa esercitazione è necessario disporre di una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="2aa67-118">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="2aa67-119">Se necessario, questo [script di esempio](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) può crearne una appositamente.</span><span class="sxs-lookup"><span data-stu-id="2aa67-119">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="2aa67-120">Quando si esegue l'esercitazione, sostituire i nomi del gruppo di risorse e delle VM dove necessario.</span><span class="sxs-lookup"><span data-stu-id="2aa67-120">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

## <a name="prepare-vm"></a><span data-ttu-id="2aa67-121">Preparare la VM</span><span class="sxs-lookup"><span data-stu-id="2aa67-121">Prepare VM</span></span>

<span data-ttu-id="2aa67-122">Per creare un'immagine di una macchina virtuale, è necessario preparare la VM generalizzandola, eseguendo la deallocazione e contrassegnando la VM di origine come generalizzata in Azure.</span><span class="sxs-lookup"><span data-stu-id="2aa67-122">To create an image of a virtual machine, you need to prepare the VM by generalizing the VM, deallocating, and then marking the source VM as generalized in Azure.</span></span>

### <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="2aa67-123">Generalizzare la macchina virtuale Windows con Sysprep</span><span class="sxs-lookup"><span data-stu-id="2aa67-123">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="2aa67-124">Sysprep rimuove anche tutte le informazioni sull'account personale e prepara la VM da usare come immagine.</span><span class="sxs-lookup"><span data-stu-id="2aa67-124">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="2aa67-125">Per altre informazioni su Sysprep, vedere [Come usare Sysprep: Introduzione](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="2aa67-125">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>


1. <span data-ttu-id="2aa67-126">Connettersi alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2aa67-126">Connect to the virtual machine.</span></span>
2. <span data-ttu-id="2aa67-127">Aprire la finestra del prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="2aa67-127">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="2aa67-128">Cambiare la directory in *%windir%\system32\sysprep* e quindi eseguire *sysprep.exe*.</span><span class="sxs-lookup"><span data-stu-id="2aa67-128">Change the directory to *%windir%\system32\sysprep*, and then run *sysprep.exe*.</span></span>
3. <span data-ttu-id="2aa67-129">Nella finestra di dialogo **Utilità preparazione sistema** selezionare *Passare alla Configurazione guidata* e verificare che la casella di controllo *Generalizza* sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="2aa67-129">In the **System Preparation Tool** dialog box, select *Enter System Out-of-Box Experience (OOBE)*, and make sure that the *Generalize* check box is selected.</span></span>
4. <span data-ttu-id="2aa67-130">In **Opzioni di arresto** selezionare *Arresta il sistema* e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2aa67-130">In **Shutdown Options**, select *Shutdown* and then click **OK**.</span></span>
5. <span data-ttu-id="2aa67-131">Al termine, Sysprep arresta la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2aa67-131">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="2aa67-132">**Non riavviare la VM**.</span><span class="sxs-lookup"><span data-stu-id="2aa67-132">**Do not restart the VM**.</span></span>

### <a name="deallocate-and-mark-the-vm-as-generalized"></a><span data-ttu-id="2aa67-133">Deallocare e contrassegnare la VM come generalizzata</span><span class="sxs-lookup"><span data-stu-id="2aa67-133">Deallocate and mark the VM as generalized</span></span>

<span data-ttu-id="2aa67-134">Per creare un'immagine, la VM deve essere deallocata e contrassegnata come generalizzata in Azure.</span><span class="sxs-lookup"><span data-stu-id="2aa67-134">To create an image, the VM needs to be deallocated and marked as generalized in Azure.</span></span>

<span data-ttu-id="2aa67-135">Deallocare la VM usando [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="2aa67-135">Deallocated the VM using [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

<span data-ttu-id="2aa67-136">Impostare lo stato della macchina virtuale su `-Generalized` usando [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="2aa67-136">Set the status of the virtual machine to `-Generalized` using [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span></span> 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-the-image"></a><span data-ttu-id="2aa67-137">Creare l'immagine</span><span class="sxs-lookup"><span data-stu-id="2aa67-137">Create the image</span></span>

<span data-ttu-id="2aa67-138">A questo punto è possibile creare un'immagine della VM usando [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) e [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span><span class="sxs-lookup"><span data-stu-id="2aa67-138">Now you can create an image of the VM by using [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) and [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span></span> <span data-ttu-id="2aa67-139">Nell'esempio seguente viene creata un'immagine denominata *myImage* dalla VM denominata *myVM*.</span><span class="sxs-lookup"><span data-stu-id="2aa67-139">The following example creates an image named *myImage* from a VM named *myVM*.</span></span>

<span data-ttu-id="2aa67-140">Trovare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2aa67-140">Get the virtual machine.</span></span> 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

<span data-ttu-id="2aa67-141">Creare la configurazione dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="2aa67-141">Create the image configuration.</span></span>

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

<span data-ttu-id="2aa67-142">Creare l'immagine.</span><span class="sxs-lookup"><span data-stu-id="2aa67-142">Create the image.</span></span>

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-the-image"></a><span data-ttu-id="2aa67-143">Creare VM dall'immagine</span><span class="sxs-lookup"><span data-stu-id="2aa67-143">Create VMs from the image</span></span>

<span data-ttu-id="2aa67-144">Ora che si dispone di un'immagine, è possibile creare una o più nuove VM dall'immagine.</span><span class="sxs-lookup"><span data-stu-id="2aa67-144">Now that you have an image, you can create one or more new VMs from the image.</span></span> <span data-ttu-id="2aa67-145">Creare una VM da un'immagine personalizzata è molto simile a creare una VM usando un'immagine del Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2aa67-145">Creating a VM from a custom image is very similar to creating a VM using a Marketplace image.</span></span> <span data-ttu-id="2aa67-146">Quando si usa un'immagine del Marketplace, è necessario fornire informazioni sull'immagine, il provider dell'immagine, l'offerta, lo SKU e la versione.</span><span class="sxs-lookup"><span data-stu-id="2aa67-146">When you use a Marketplace image, you have to information about the image, image provider, offer, SKU and version.</span></span> <span data-ttu-id="2aa67-147">Con un'immagine personalizzata è sufficiente fornire l'ID della risorsa immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2aa67-147">With a custom image, you just need to provide the ID of the custom image resource.</span></span> 

<span data-ttu-id="2aa67-148">Nello script seguente si crea la variabile *$image* per memorizzare le informazioni sull'immagine personalizzata usando [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) e quindi si usa [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) e si specifica l'ID mediante la variabile *$image* appena creata.</span><span class="sxs-lookup"><span data-stu-id="2aa67-148">In the following script, we create a variable *$image* to store information about the custom image using [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) and then we use [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) and specify the ID using the *$image* variable we just created.</span></span> 

<span data-ttu-id="2aa67-149">Lo script crea una VM denominata *myVMfromImage* dall'immagine personalizzata in un nuovo gruppo di risorse denominato *myResourceGroupFromImage* nella posizione *Stati Uniti occidentali*.</span><span class="sxs-lookup"><span data-stu-id="2aa67-149">The script creates a VM named *myVMfromImage* from our custom image in a new resource group named *myResourceGroupFromImage* in the *West US* location.</span></span>


```powershell
$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

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

# Here is where we create a variable to store information about the image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want to create the VM from and image and provide the image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a><span data-ttu-id="2aa67-150">Gestione delle immagini</span><span class="sxs-lookup"><span data-stu-id="2aa67-150">Image management</span></span> 

<span data-ttu-id="2aa67-151">Di seguito sono riportati alcuni esempi di attività comuni di gestione delle immagini e della relativa modalità di completamento tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2aa67-151">Here are some examples of common management image tasks and how to complete them using PowerShell.</span></span>

<span data-ttu-id="2aa67-152">Elencare tutte le immagini per nome.</span><span class="sxs-lookup"><span data-stu-id="2aa67-152">List all images by name.</span></span>

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

<span data-ttu-id="2aa67-153">Eliminare un'immagine.</span><span class="sxs-lookup"><span data-stu-id="2aa67-153">Delete an image.</span></span> <span data-ttu-id="2aa67-154">Questo esempio elimina l'immagine denominata *myOldImage* da *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="2aa67-154">This example deletes the image named *myOldImage* from the *myResourceGroup*.</span></span>

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="2aa67-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2aa67-155">Next steps</span></span>

<span data-ttu-id="2aa67-156">In questa esercitazione è stata creata un'immagine di macchina virtuale personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2aa67-156">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="2aa67-157">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="2aa67-157">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2aa67-158">Eseguire Sysprep e generalizzare le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="2aa67-158">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="2aa67-159">Creare un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="2aa67-159">Create a custom image</span></span>
> * <span data-ttu-id="2aa67-160">Creare una VM da un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="2aa67-160">Create a VM from a custom image</span></span>
> * <span data-ttu-id="2aa67-161">Elencare tutte le immagini nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="2aa67-161">List all the images in your subscription</span></span>
> * <span data-ttu-id="2aa67-162">Eliminare un'immagine</span><span class="sxs-lookup"><span data-stu-id="2aa67-162">Delete an image</span></span>

<span data-ttu-id="2aa67-163">Passare all'esercitazione successiva per la descrizione delle macchine virtuali a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="2aa67-163">Advance to the next tutorial to learn about how highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2aa67-164">Creare VM a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="2aa67-164">Create highly available VMs</span></span>](tutorial-availability-sets.md)




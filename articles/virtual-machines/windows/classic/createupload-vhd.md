---
title: Creare e caricare un'immagine di VM con Powershell | Microsoft Docs
description: Informazioni su come creare e caricare un'immagine Windows Server generalizzata (VHD) utilizzando il modello di distribuzione classica e Azure Powershell.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: bc75c8cdd98b0ea0fbff6483c0e3c9d4468d3941
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-upload-a-windows-server-vhd-to-azure"></a><span data-ttu-id="33cef-103">Creazione e caricamento di un disco rigido virtuale con Windows Server in Azure</span><span class="sxs-lookup"><span data-stu-id="33cef-103">Create and upload a Windows Server VHD to Azure</span></span>
<span data-ttu-id="33cef-104">Questo articolo illustra come caricare la propria immagine VM generalizzata come un disco rigido virtuale (VHD) in modo da usarlo per la creazione di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="33cef-104">This article shows you how to upload your own generalized VM image as a virtual hard disk (VHD) so you can use it to create virtual machines.</span></span> <span data-ttu-id="33cef-105">Per informazioni dettagliate sui dischi e sui dischi rigidi virtuali in Microsoft Azure, vedere [Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="33cef-105">For more details about disks and VHDs in Microsoft Azure, see [About Disks and VHDs for Virtual Machines](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="33cef-106">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="33cef-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="33cef-107">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="33cef-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="33cef-108">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="33cef-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="33cef-109">È anche possibile [caricare](../upload-generalized-managed.md) una macchina virtuale usando il modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="33cef-109">You can also [upload](../upload-generalized-managed.md) a virtual machine using the Resource Manager model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33cef-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="33cef-110">Prerequisites</span></span>
<span data-ttu-id="33cef-111">Questo articolo presuppone che l'utente abbia:</span><span class="sxs-lookup"><span data-stu-id="33cef-111">This article assumes you have:</span></span>

* <span data-ttu-id="33cef-112">**Una sottoscrizione di Azure** : se non si ha tale sottoscrizione, [è possibile aprire un account Azure per ottenerne gratuitamente una](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="33cef-112">**An Azure subscription** - If you don't have one, you can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="33cef-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)**: è necessario che il modulo di Microsoft Azure PowerShell sia installato e configurato per l'uso della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="33cef-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)** - You have the Microsoft Azure PowerShell module installed and configured to use your subscription.</span></span>
* <span data-ttu-id="33cef-114">**Un file .VHD** : una versione supportata del sistema operativo Windows archiviata in un file con .vhd e collegata a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="33cef-114">**A .VHD file** - supported Windows operating system stored in a .vhd file and attached to a virtual machine.</span></span> <span data-ttu-id="33cef-115">Verificare inoltre che i ruoli del server in esecuzione sul disco rigido virtuale siano supportati da Sysprep.</span><span class="sxs-lookup"><span data-stu-id="33cef-115">Check to see if the server roles running on the VHD are supported by Sysprep.</span></span> <span data-ttu-id="33cef-116">Per ulteriori informazioni, vedere [Supporto Sysprep per i ruoli server](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="33cef-116">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="33cef-117">il formato VHDX non è supportato in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="33cef-117">The VHDX format is not supported in Microsoft Azure.</span></span> <span data-ttu-id="33cef-118">È possibile convertire il disco in formato VHD tramite la console di gestione di Hyper-V o il [cmdlet Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="33cef-118">You can convert the disk to VHD format using Hyper-V Manager or the [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="33cef-119">Per informazioni dettagliate, vedere questo [post di blog](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span><span class="sxs-lookup"><span data-stu-id="33cef-119">For details, see this [blogpost](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span></span>

## <a name="step-1-prep-the-vhd"></a><span data-ttu-id="33cef-120">Passaggio 1: Preparare il disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="33cef-120">Step 1: Prep the VHD</span></span>
<span data-ttu-id="33cef-121">Prima di caricare il disco rigido virtuale in Azure, è necessario generalizzarlo usando lo strumento Sysprep,</span><span class="sxs-lookup"><span data-stu-id="33cef-121">Before you upload the VHD to Azure, it needs to be generalized by using the Sysprep tool.</span></span> <span data-ttu-id="33cef-122">che prepara il disco rigido virtuale in modo che possa essere usato come immagine.</span><span class="sxs-lookup"><span data-stu-id="33cef-122">This prepares the VHD to be used as an image.</span></span> <span data-ttu-id="33cef-123">Per altre informazioni su Sysprep, vedere [Come usare Sysprep: Introduzione](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="33cef-123">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> <span data-ttu-id="33cef-124">Eseguire il backup della VM prima di eseguire Sysprep.</span><span class="sxs-lookup"><span data-stu-id="33cef-124">Back up the VM before running Sysprep.</span></span>

<span data-ttu-id="33cef-125">Dalla macchina virtuale su cui è stato installato il sistema operativo, completare la seguente procedura:</span><span class="sxs-lookup"><span data-stu-id="33cef-125">From the virtual machine that the operating system was installed to, complete the following procedure:</span></span>

1. <span data-ttu-id="33cef-126">Accedere al sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="33cef-126">Sign in to the operating system.</span></span>
2. <span data-ttu-id="33cef-127">Aprire una finestra del prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="33cef-127">Open a command prompt window as an administrator.</span></span> <span data-ttu-id="33cef-128">Impostare la directory su **%windir%\system32\sysprep**, quindi eseguire `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="33cef-128">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>

    ![Apertura della finestra del Prompt dei comandi](./media/createupload-vhd/sysprep_commandprompt.png)
3. <span data-ttu-id="33cef-130">Verrà visualizzata la finestra di dialogo **Utilità preparazione sistema** .</span><span class="sxs-lookup"><span data-stu-id="33cef-130">The **System Preparation Tool** dialog box appears.</span></span>

   ![Avvio di Sysprep](./media/createupload-vhd/sysprepgeneral.png)
4. <span data-ttu-id="33cef-132">In **Utilità preparazione sistema** selezionare **Passare alla Configurazione guidata** e assicurarsi che l'opzione **Generalizza** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="33cef-132">In the **System Preparation Tool**, select **Enter System Out of Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span>
5. <span data-ttu-id="33cef-133">In **Opzioni di arresto del sistema** selezionare **Arresta il sistema**.</span><span class="sxs-lookup"><span data-stu-id="33cef-133">In **Shutdown Options**, select **Shutdown**.</span></span>
6. <span data-ttu-id="33cef-134">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="33cef-134">Click **OK**.</span></span>

## <a name="step-2-create-a-storage-account-and-a-container"></a><span data-ttu-id="33cef-135">Passaggio 2: Creare un account di archiviazione e un contenitore</span><span class="sxs-lookup"><span data-stu-id="33cef-135">Step 2: Create a storage account and a container</span></span>
<span data-ttu-id="33cef-136">È necessario un account di archiviazione di Azure in cui caricare il file con estensione vhd.</span><span class="sxs-lookup"><span data-stu-id="33cef-136">You need a storage account in Azure so you have a place to upload the .vhd file.</span></span> <span data-ttu-id="33cef-137">Questo passaggio illustra come creare un account o come ottenere le informazioni necessarie da un account esistente.</span><span class="sxs-lookup"><span data-stu-id="33cef-137">This step shows you how to create an account, or get the info you need from an existing account.</span></span> <span data-ttu-id="33cef-138">Sostituire le variabili tra &lsaquo; parentesi &rsaquo; con le proprie informazioni.</span><span class="sxs-lookup"><span data-stu-id="33cef-138">Replace the variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

1. <span data-ttu-id="33cef-139">Login</span><span class="sxs-lookup"><span data-stu-id="33cef-139">Login</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="33cef-140">Impostare la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="33cef-140">Set your Azure subscription.</span></span>

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. <span data-ttu-id="33cef-141">Creare un nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="33cef-141">Create a new storage account.</span></span> <span data-ttu-id="33cef-142">Il nome dell'account di archiviazione deve essere univoco e composto da minimo 3 e massimo 24 caratteri.</span><span class="sxs-lookup"><span data-stu-id="33cef-142">The name of the storage account should be unique, 3-24 characters.</span></span> <span data-ttu-id="33cef-143">Il nome può essere qualsiasi combinazione di lettere e numeri.</span><span class="sxs-lookup"><span data-stu-id="33cef-143">The name can be any combination of letters and numbers.</span></span> <span data-ttu-id="33cef-144">È inoltre necessario specificare una posizione come "East US"</span><span class="sxs-lookup"><span data-stu-id="33cef-144">You also need to specify a location like "East US"</span></span>

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. <span data-ttu-id="33cef-145">Impostare il nuovo account di archiviazione come predefinito.</span><span class="sxs-lookup"><span data-stu-id="33cef-145">Set the new storage account as the default.</span></span>

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. <span data-ttu-id="33cef-146">Creare un nuovo contenitore.</span><span class="sxs-lookup"><span data-stu-id="33cef-146">Create a new container.</span></span>

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-the-vhd-file"></a><span data-ttu-id="33cef-147">Passaggio 3: Caricare il file .vhd</span><span class="sxs-lookup"><span data-stu-id="33cef-147">Step 3: Upload the .vhd file</span></span>
<span data-ttu-id="33cef-148">Usare [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) per caricare il file VHD.</span><span class="sxs-lookup"><span data-stu-id="33cef-148">Use the [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) to upload the VHD.</span></span>

<span data-ttu-id="33cef-149">Nella finestra di Azure PowerShell usata nel passaggio precedente, digitare il comando seguente e sostituire le variabili tra &lsaquo; parentesi &rsaquo; con le proprie informazioni.</span><span class="sxs-lookup"><span data-stu-id="33cef-149">From the Azure PowerShell window you used in the previous step, type the following command and replace the variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-the-image-to-your-list-of-custom-images"></a><span data-ttu-id="33cef-150">Passaggio 4: Aggiungere l'immagine all'elenco di immagini personalizzate</span><span class="sxs-lookup"><span data-stu-id="33cef-150">Step 4: Add the image to your list of custom images</span></span>
<span data-ttu-id="33cef-151">Usare il cmdlet [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) per aggiungere l'immagine all'elenco di immagini personalizzate.</span><span class="sxs-lookup"><span data-stu-id="33cef-151">Use the [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet to add the image to the list of your custom images.</span></span>

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a><span data-ttu-id="33cef-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="33cef-152">Next steps</span></span>
<span data-ttu-id="33cef-153">È ora possibile [creare una macchina virtuale personalizzata](createportal.md) usando l'immagine caricata.</span><span class="sxs-lookup"><span data-stu-id="33cef-153">You can now [create a custom VM](createportal.md) using the image you uploaded.</span></span>

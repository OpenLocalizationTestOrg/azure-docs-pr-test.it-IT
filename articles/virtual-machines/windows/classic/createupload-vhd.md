---
title: immagini aaaCreate e caricamento di una macchina virtuale mediante Powershell | Documenti Microsoft
description: Informazioni su toocreate e caricare un'immagine di Windows Server generalizzata (VHD) con il modello di distribuzione classica hello e Powershell di Azure.
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
ms.openlocfilehash: 093b57c9157cea5f348c8ba02b5700c917adbcdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a><span data-ttu-id="efe78-103">Creare e caricare tooAzure un disco rigido virtuale di Windows Server</span><span class="sxs-lookup"><span data-stu-id="efe78-103">Create and upload a Windows Server VHD tooAzure</span></span>
<span data-ttu-id="efe78-104">Questo articolo illustra come tooupload la propria macchina virtuale generalizzata immagine come un disco rigido virtuale (VHD) in modo è possibile utilizzare le macchine virtuali toocreate.</span><span class="sxs-lookup"><span data-stu-id="efe78-104">This article shows you how tooupload your own generalized VM image as a virtual hard disk (VHD) so you can use it toocreate virtual machines.</span></span> <span data-ttu-id="efe78-105">Per informazioni dettagliate sui dischi e sui dischi rigidi virtuali in Microsoft Azure, vedere [Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="efe78-105">For more details about disks and VHDs in Microsoft Azure, see [About Disks and VHDs for Virtual Machines](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="efe78-106">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="efe78-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="efe78-107">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="efe78-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="efe78-108">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="efe78-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="efe78-109">È anche possibile [caricare](../upload-generalized-managed.md) una macchina virtuale utilizzando il modello di gestione risorse hello.</span><span class="sxs-lookup"><span data-stu-id="efe78-109">You can also [upload](../upload-generalized-managed.md) a virtual machine using hello Resource Manager model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efe78-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="efe78-110">Prerequisites</span></span>
<span data-ttu-id="efe78-111">Questo articolo presuppone che l'utente abbia:</span><span class="sxs-lookup"><span data-stu-id="efe78-111">This article assumes you have:</span></span>

* <span data-ttu-id="efe78-112">**Una sottoscrizione di Azure** : se non si ha tale sottoscrizione, [è possibile aprire un account Azure per ottenerne gratuitamente una](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="efe78-112">**An Azure subscription** - If you don't have one, you can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="efe78-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)**  -si dispone di Microsoft Azure PowerShell hello modulo installato e configurato toouse la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="efe78-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)** - You have hello Microsoft Azure PowerShell module installed and configured toouse your subscription.</span></span>
* <span data-ttu-id="efe78-114">**A. File VHD** - archiviato in un file con estensione vhd e la macchina virtuale associata tooa sistema operativo di Windows supportati.</span><span class="sxs-lookup"><span data-stu-id="efe78-114">**A .VHD file** - supported Windows operating system stored in a .vhd file and attached tooa virtual machine.</span></span> <span data-ttu-id="efe78-115">Controllare toosee se i ruoli del server hello in esecuzione sul disco rigido virtuale hello sono supportati da Sysprep.</span><span class="sxs-lookup"><span data-stu-id="efe78-115">Check toosee if hello server roles running on hello VHD are supported by Sysprep.</span></span> <span data-ttu-id="efe78-116">Per ulteriori informazioni, vedere [Supporto Sysprep per i ruoli server](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="efe78-116">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="efe78-117">formato VHDX Hello non è supportata in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="efe78-117">hello VHDX format is not supported in Microsoft Azure.</span></span> <span data-ttu-id="efe78-118">È possibile convertire hello disco tooVHD formato Hyper-V Manager oppure hello [cmdlet Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="efe78-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="efe78-119">Per informazioni dettagliate, vedere questo [post di blog](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span><span class="sxs-lookup"><span data-stu-id="efe78-119">For details, see this [blogpost](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span></span>

## <a name="step-1-prep-hello-vhd"></a><span data-ttu-id="efe78-120">Passaggio 1: Preparare hello disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="efe78-120">Step 1: Prep hello VHD</span></span>
<span data-ttu-id="efe78-121">Prima di caricare hello tooAzure di disco rigido virtuale, è necessario che toobe generalizzato usando lo strumento Sysprep hello.</span><span class="sxs-lookup"><span data-stu-id="efe78-121">Before you upload hello VHD tooAzure, it needs toobe generalized by using hello Sysprep tool.</span></span> <span data-ttu-id="efe78-122">Questa funzione Prepara hello toobe di disco rigido virtuale utilizzato come immagine.</span><span class="sxs-lookup"><span data-stu-id="efe78-122">This prepares hello VHD toobe used as an image.</span></span> <span data-ttu-id="efe78-123">Per ulteriori informazioni su Sysprep, vedere [come tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="efe78-123">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> <span data-ttu-id="efe78-124">Eseguire il backup hello VM prima di eseguire Sysprep.</span><span class="sxs-lookup"><span data-stu-id="efe78-124">Back up hello VM before running Sysprep.</span></span>

<span data-ttu-id="efe78-125">È stato installato da macchina virtuale hello hello del sistema operativo per completare hello seguente procedura:</span><span class="sxs-lookup"><span data-stu-id="efe78-125">From hello virtual machine that hello operating system was installed to, complete hello following procedure:</span></span>

1. <span data-ttu-id="efe78-126">Accedi toohello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="efe78-126">Sign in toohello operating system.</span></span>
2. <span data-ttu-id="efe78-127">Aprire una finestra del prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="efe78-127">Open a command prompt window as an administrator.</span></span> <span data-ttu-id="efe78-128">Modificare anche le directory hello**%windir%\system32\sysprep**, quindi eseguire `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="efe78-128">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>

    ![Apertura della finestra del Prompt dei comandi](./media/createupload-vhd/sysprep_commandprompt.png)
3. <span data-ttu-id="efe78-130">Hello **System Preparation Tool** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="efe78-130">hello **System Preparation Tool** dialog box appears.</span></span>

   ![Avvio di Sysprep](./media/createupload-vhd/sysprepgeneral.png)
4. <span data-ttu-id="efe78-132">In hello **System Preparation Tool**selezionare **immettere sistema fuori casella guidata** e verificare che **Generalize** è selezionata.</span><span class="sxs-lookup"><span data-stu-id="efe78-132">In hello **System Preparation Tool**, select **Enter System Out of Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span>
5. <span data-ttu-id="efe78-133">In **Opzioni di arresto del sistema** selezionare **Arresta il sistema**.</span><span class="sxs-lookup"><span data-stu-id="efe78-133">In **Shutdown Options**, select **Shutdown**.</span></span>
6. <span data-ttu-id="efe78-134">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="efe78-134">Click **OK**.</span></span>

## <a name="step-2-create-a-storage-account-and-a-container"></a><span data-ttu-id="efe78-135">Passaggio 2: Creare un account di archiviazione e un contenitore</span><span class="sxs-lookup"><span data-stu-id="efe78-135">Step 2: Create a storage account and a container</span></span>
<span data-ttu-id="efe78-136">È necessario un account di archiviazione di Azure in modo che sia un file con estensione vhd hello tooupload sul posto.</span><span class="sxs-lookup"><span data-stu-id="efe78-136">You need a storage account in Azure so you have a place tooupload hello .vhd file.</span></span> <span data-ttu-id="efe78-137">Questo passaggio illustra come toocreate un account o get hello informazioni è necessario un account esistente.</span><span class="sxs-lookup"><span data-stu-id="efe78-137">This step shows you how toocreate an account, or get hello info you need from an existing account.</span></span> <span data-ttu-id="efe78-138">Sostituire le variabili di hello in &lsaquo; tra parentesi quadre &rsaquo; con informazioni personali.</span><span class="sxs-lookup"><span data-stu-id="efe78-138">Replace hello variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

1. <span data-ttu-id="efe78-139">Login</span><span class="sxs-lookup"><span data-stu-id="efe78-139">Login</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="efe78-140">Impostare la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="efe78-140">Set your Azure subscription.</span></span>

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. <span data-ttu-id="efe78-141">Creare un nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="efe78-141">Create a new storage account.</span></span> <span data-ttu-id="efe78-142">nome Hello hello dell'account di archiviazione deve essere univoco, 3 e 24 caratteri.</span><span class="sxs-lookup"><span data-stu-id="efe78-142">hello name of hello storage account should be unique, 3-24 characters.</span></span> <span data-ttu-id="efe78-143">nome di Hello può essere qualsiasi combinazione di lettere e numeri.</span><span class="sxs-lookup"><span data-stu-id="efe78-143">hello name can be any combination of letters and numbers.</span></span> <span data-ttu-id="efe78-144">È inoltre necessario disporre di una posizione, come "Orientale US" toospecify</span><span class="sxs-lookup"><span data-stu-id="efe78-144">You also need toospecify a location like "East US"</span></span>

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. <span data-ttu-id="efe78-145">Impostare il nuovo account di archiviazione hello come valore predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="efe78-145">Set hello new storage account as hello default.</span></span>

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. <span data-ttu-id="efe78-146">Creare un nuovo contenitore.</span><span class="sxs-lookup"><span data-stu-id="efe78-146">Create a new container.</span></span>

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a><span data-ttu-id="efe78-147">Passaggio 3: Caricare il file con estensione vhd hello</span><span class="sxs-lookup"><span data-stu-id="efe78-147">Step 3: Upload hello .vhd file</span></span>
<span data-ttu-id="efe78-148">Hello utilizzare [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) hello tooupload disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="efe78-148">Use hello [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload hello VHD.</span></span>

<span data-ttu-id="efe78-149">Finestra di Azure PowerShell hello utilizzata nel passaggio precedente hello, digitare quanto segue di hello comando e sostituire le variabili di hello in &lsaquo; tra parentesi quadre &rsaquo; con informazioni personali.</span><span class="sxs-lookup"><span data-stu-id="efe78-149">From hello Azure PowerShell window you used in hello previous step, type hello following command and replace hello variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a><span data-ttu-id="efe78-150">Passaggio 4: Aggiungere hello immagine tooyour elenco immagini personalizzate</span><span class="sxs-lookup"><span data-stu-id="efe78-150">Step 4: Add hello image tooyour list of custom images</span></span>
<span data-ttu-id="efe78-151">Hello utilizzare [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet tooadd hello toohello ImageList di immagini personalizzate.</span><span class="sxs-lookup"><span data-stu-id="efe78-151">Use hello [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet tooadd hello image toohello list of your custom images.</span></span>

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a><span data-ttu-id="efe78-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="efe78-152">Next steps</span></span>
<span data-ttu-id="efe78-153">È ora possibile [creare una macchina virtuale personalizzata](createportal.md) utilizzando hello immagine caricata.</span><span class="sxs-lookup"><span data-stu-id="efe78-153">You can now [create a custom VM](createportal.md) using hello image you uploaded.</span></span>

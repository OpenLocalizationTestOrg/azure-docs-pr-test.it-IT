---
title: aaaAzure vantaggio di utilizzare ibrida per Windows Server e Client Windows | Documenti Microsoft
description: Informazioni su come toomaximize il toobring vantaggi Windows Software Assurance locale tooAzure le licenze
services: virtual-machines-windows
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 332583b6-15a3-4efb-80c3-9082587828b0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 5/26/2017
ms.author: xujing
ms.openlocfilehash: f24487320a60132aaf766a31f3e6f3726d4a3bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a><span data-ttu-id="fda1e-103">Azure Hybrid Use Benefit per Windows Server e Client Windows</span><span class="sxs-lookup"><span data-stu-id="fda1e-103">Azure Hybrid Use Benefit for Windows Server and Windows Client</span></span>
<span data-ttu-id="fda1e-104">Per i clienti con Software Assurance, vantaggio di utilizzare ibrida di Azure consente toouse le licenze di Windows Server e Client di Windows locale e l'esecuzione macchine virtuali di Windows in Azure a un costo ridotto.</span><span class="sxs-lookup"><span data-stu-id="fda1e-104">For customers with Software Assurance, Azure Hybrid Use Benefit allows you toouse your on-premises Windows Server and Windows Client licenses and run Windows virtual machines in Azure at a reduced cost.</span></span> <span data-ttu-id="fda1e-105">Azure Hybrid Use Benefit per Windows Server include Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2 e Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="fda1e-105">Azure Hybrid Use Benefit for Windows Server includes Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2, and Windows Server 2016.</span></span> <span data-ttu-id="fda1e-106">Azure Hybrid Use Benefit per Client Windows include Windows 10.</span><span class="sxs-lookup"><span data-stu-id="fda1e-106">Azure Hybrid Use Benefit for Windows Client includes Windows 10.</span></span> <span data-ttu-id="fda1e-107">Per ulteriori informazioni, vedere hello [pagina di gestione delle licenze vantaggio di utilizzare Azure ibrida](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="fda1e-107">For more information, please see hello [Azure Hybrid Use Benefit licensing page](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

>[!IMPORTANT]
><span data-ttu-id="fda1e-108">Azure ibrida utilizzare vantaggi per Client Windows è attualmente in anteprima utilizzando l'immagine di Windows 10 hello in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="fda1e-108">Azure Hybrid Use Benefits for Windows Client is currently in Preview using hello Windows 10 image in hello Azure Marketplace.</span></span> <span data-ttu-id="fda1e-109">Solo i clienti Enterprise con Windows 10 Enterprise E3/E5 per utente o Windows VDA per utente (licenze di sottoscrizione utente o le licenze di sottoscrizione utente per i componenti aggiuntivi) idonei ("Licenze di qualificazione") sono idonei.</span><span class="sxs-lookup"><span data-stu-id="fda1e-109">Only Enterprise customers with Windows 10 Enterprise E3/E5 per user or Windows VDA per user (User Subscription Licenses or Add-on User Subscription Licenses) (“Qualifying Licenses”) are eligible.</span></span>
>
>

## <a name="ways-toouse-azure-hybrid-use-benefit"></a><span data-ttu-id="fda1e-110">Modi toouse vantaggio di utilizzare ibrida di Azure</span><span class="sxs-lookup"><span data-stu-id="fda1e-110">Ways toouse Azure Hybrid Use Benefit</span></span>
<span data-ttu-id="fda1e-111">Esistono un paio di modi toodeploy macchine virtuali di Windows con hello vantaggio di utilizzare ibrida di Azure:</span><span class="sxs-lookup"><span data-stu-id="fda1e-111">There are a couple of different ways toodeploy Windows VMs with hello Azure Hybrid Use Benefit:</span></span>

1. <span data-ttu-id="fda1e-112">È possibile distribuire le macchine virtuali da [immagini specifiche del Marketplace](#deploy-a-vm-using-the-azure-marketplace) preconfigurate con Azure Hybrid Use Benefit: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008SP1.</span><span class="sxs-lookup"><span data-stu-id="fda1e-112">You can deploy VMs from [specific Marketplace images](#deploy-a-vm-using-the-azure-marketplace) that are pre-configured with Azure Hybrid Use Benefit - Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span>
2. <span data-ttu-id="fda1e-113">È possibile [caricare una macchina virtuale personalizzata](#upload-a-windows-vhd) e [distribuirla usando un modello di Resource Manager](#deploy-a-vm-via-resource-manager) o [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="fda1e-113">You can [upload a custom VM](#upload-a-windows-vhd) and [deploy using a Resource Manager template](#deploy-a-vm-via-resource-manager) or [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span></span>

## <a name="deploy-a-vm-using-hello-azure-marketplace"></a><span data-ttu-id="fda1e-114">Distribuire una macchina virtuale utilizzando hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="fda1e-114">Deploy a VM using hello Azure Marketplace</span></span>
<span data-ttu-id="fda1e-115">Le immagini seguenti sono disponibili in hello preconfigurata con vantaggio di utilizzare ibrida di Azure Marketplace: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008SP1.</span><span class="sxs-lookup"><span data-stu-id="fda1e-115">Following images are available in hello Marketplace pre-configured with Azure Hybrid Use Benefit: Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span> <span data-ttu-id="fda1e-116">Queste immagini possono essere distribuite direttamente dal portale di Azure hello, modelli di gestione risorse o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fda1e-116">These images can be deployed directly from hello Azure portal, Resource Manager templates, or Azure PowerShell.</span></span>

<span data-ttu-id="fda1e-117">È possibile distribuire queste immagini direttamente dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="fda1e-117">You can deploy these images directly from hello Azure portal.</span></span> <span data-ttu-id="fda1e-118">Per l'utilizzo in modelli di gestione risorse e con Azure PowerShell, visualizzare elenco hello delle immagini come segue:</span><span class="sxs-lookup"><span data-stu-id="fda1e-118">For use in Resource Manager templates and with Azure PowerShell, view hello list of images as follows:</span></span>

<span data-ttu-id="fda1e-119">Per Windows Server:</span><span class="sxs-lookup"><span data-stu-id="fda1e-119">For Windows Server:</span></span>
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- <span data-ttu-id="fda1e-120">2016-Datacenter versione 2016.127.20170406 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="fda1e-120">2016-Datacenter version 2016.127.20170406 or above</span></span>

- <span data-ttu-id="fda1e-121">2012-R2-Datacenter versione 4.127.20170406 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="fda1e-121">2012-R2-Datacenter version 4.127.20170406 or above</span></span>

- <span data-ttu-id="fda1e-122">2012-Datacenter versione 3.127.20170406 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="fda1e-122">2012-Datacenter version 3.127.20170406 or above</span></span>

- <span data-ttu-id="fda1e-123">2008 R2-SP1 versione 2.127.20170406 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="fda1e-123">2008-R2-SP1 version 2.127.20170406 or above</span></span>

<span data-ttu-id="fda1e-124">Per Client Windows:</span><span class="sxs-lookup"><span data-stu-id="fda1e-124">For Windows Client:</span></span>
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a><span data-ttu-id="fda1e-125">Caricare un disco rigido virtuale di Windows Server</span><span class="sxs-lookup"><span data-stu-id="fda1e-125">Upload a Windows Server VHD</span></span>
<span data-ttu-id="fda1e-126">toodeploy una VM di Windows Server in Azure, è innanzitutto necessario toocreate un disco rigido virtuale che contiene la build di Windows di base.</span><span class="sxs-lookup"><span data-stu-id="fda1e-126">toodeploy a Windows Server VM in Azure, you first need toocreate a VHD that contains your base Windows build.</span></span> <span data-ttu-id="fda1e-127">Questo disco rigido virtuale è necessario preparare adeguatamente tramite Sysprep prima di caricarla tooAzure.</span><span class="sxs-lookup"><span data-stu-id="fda1e-127">This VHD must be appropriately prepared via Sysprep before you upload it tooAzure.</span></span> <span data-ttu-id="fda1e-128">È possibile [altre informazioni sui requisiti di disco rigido virtuale hello e processo Sysprep](upload-generalized-managed.md) e [supporto Sysprep per i ruoli Server](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="fda1e-128">You can [read more about hello VHD requirements and Sysprep process](upload-generalized-managed.md) and [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span> <span data-ttu-id="fda1e-129">Eseguire il backup hello VM prima di eseguire Sysprep.</span><span class="sxs-lookup"><span data-stu-id="fda1e-129">Back up hello VM before running Sysprep.</span></span> 

<span data-ttu-id="fda1e-130">Assicurarsi di avere [installato e configurato in hello più recente di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fda1e-130">Make sure you have [installed and configured hello latest Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="fda1e-131">Dopo aver preparato il disco rigido virtuale, caricare hello VHD tooyour account di archiviazione Azure tramite hello `Add-AzureRmVhd` cmdlet come segue:</span><span class="sxs-lookup"><span data-stu-id="fda1e-131">Once you have prepared your VHD, upload hello VHD tooyour Azure Storage account using hello `Add-AzureRmVhd` cmdlet as follows:</span></span>

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> <span data-ttu-id="fda1e-132">Microsoft SQL Server, SharePoint Server e Dynamics possono usare anche le licenza di Software Assurance.</span><span class="sxs-lookup"><span data-stu-id="fda1e-132">Microsoft SQL Server, SharePoint Server, and Dynamics can also utilize your Software Assurance licensing.</span></span> <span data-ttu-id="fda1e-133">Immagine di Windows Server tooprepare hello è comunque necessario installare i componenti dell'applicazione e fornendo di conseguenza le chiavi di licenza, quindi caricare tooAzure di immagine disco hello.</span><span class="sxs-lookup"><span data-stu-id="fda1e-133">You still need tooprepare hello Windows Server image by installing your application components and providing license keys accordingly, then uploading hello disk image tooAzure.</span></span> <span data-ttu-id="fda1e-134">Esaminare hello documentazione appropriata per l'esecuzione di Sysprep con l'applicazione, ad esempio [considerazioni per l'installazione di SQL Server tramite Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) o [compilare un'immagine di riferimento di SharePoint Server 2016 (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span><span class="sxs-lookup"><span data-stu-id="fda1e-134">Review hello appropriate documentation for running Sysprep with your application, such as [Considerations for Installing SQL Server using Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) or [Build a SharePoint Server 2016 Reference Image (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span></span>
>
>

<span data-ttu-id="fda1e-135">È inoltre possibile leggere informazioni sui [hello VHD tooAzure processo di caricamento](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span><span class="sxs-lookup"><span data-stu-id="fda1e-135">You can also read more about [uploading hello VHD tooAzure process](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span></span>


## <a name="deploy-a-vm-via-resource-manager-template"></a><span data-ttu-id="fda1e-136">Distribuire una macchina virtuale con il modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fda1e-136">Deploy a VM via Resource Manager Template</span></span>
<span data-ttu-id="fda1e-137">Nei modelli di Resource Manager è possibile specificare un parametro aggiuntivo per `licenseType`.</span><span class="sxs-lookup"><span data-stu-id="fda1e-137">Within your Resource Manager templates, an additional parameter for `licenseType` can be specified.</span></span> <span data-ttu-id="fda1e-138">Altre informazioni sulla [creazione di modelli di Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fda1e-138">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="fda1e-139">Dopo aver creato il disco rigido virtuale caricato di tooAzure, modificare è tipo di licenza di gestione risorse modello tooinclude hello come parte di hello provider di calcolo e distribuire il modello come di consueto:</span><span class="sxs-lookup"><span data-stu-id="fda1e-139">Once you have your VHD uploaded tooAzure, edit you Resource Manager template tooinclude hello license type as part of hello compute provider and deploy your template as normal:</span></span>

<span data-ttu-id="fda1e-140">Per Windows Server:</span><span class="sxs-lookup"><span data-stu-id="fda1e-140">For Windows Server:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

<span data-ttu-id="fda1e-141">Per solo toouse di Client Windows con un'immagine del Marketplace Azure:</span><span class="sxs-lookup"><span data-stu-id="fda1e-141">For Windows Client toouse with Azure Marketplace Image only:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a><span data-ttu-id="fda1e-142">Distribuire una macchina virtuale con l'avvio rapido di PowerShell</span><span class="sxs-lookup"><span data-stu-id="fda1e-142">Deploy a VM via PowerShell quickstart</span></span>
<span data-ttu-id="fda1e-143">Quando si distribuisce la macchina virtuale Windows Server con PowerShell è presente un parametro aggiuntivo per `-LicenseType`.</span><span class="sxs-lookup"><span data-stu-id="fda1e-143">When deploying your Windows Server VM via PowerShell, you have an additional parameter for `-LicenseType`.</span></span> <span data-ttu-id="fda1e-144">Dopo aver creato il disco rigido virtuale caricato di tooAzure, creare una macchina virtuale utilizzando `New-AzureRmVM` e specificare tipo di licenza hello come segue:</span><span class="sxs-lookup"><span data-stu-id="fda1e-144">Once you have your VHD uploaded tooAzure, you create a VM using `New-AzureRmVM` and specify hello licensing type as follows:</span></span>

<span data-ttu-id="fda1e-145">Per Windows Server:</span><span class="sxs-lookup"><span data-stu-id="fda1e-145">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

<span data-ttu-id="fda1e-146">Per solo toouse di Client Windows con un'immagine del Marketplace Azure:</span><span class="sxs-lookup"><span data-stu-id="fda1e-146">For Windows Client toouse with Azure Marketplace Image only:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

<span data-ttu-id="fda1e-147">È possibile [leggere una descrizione più dettagliata sulla distribuzione di una macchina virtuale in Azure tramite PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) seguente o lettura una Guida più descrittiva in hello diversi passaggi troppo[creare una macchina virtuale Windows usando Gestione risorse e PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fda1e-147">You can [read a more detailed walkthrough on deploying a VM in Azure via PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) below, or read a more descriptive guide on hello different steps too[create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="verify-your-vm-is-utilizing-hello-licensing-benefit"></a><span data-ttu-id="fda1e-148">Verificare che la macchina virtuale utilizza vantaggio licenze hello</span><span class="sxs-lookup"><span data-stu-id="fda1e-148">Verify your VM is utilizing hello licensing benefit</span></span>
<span data-ttu-id="fda1e-149">Dopo avere distribuito la macchina virtuale mediante PowerShell hello o il metodo di distribuzione di gestione delle risorse, verificare il tipo di licenza hello con `Get-AzureRmVM` come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="fda1e-149">Once you have deployed your VM through either hello PowerShell or Resource Manager deployment method, verify hello license type with `Get-AzureRmVM` as follows:</span></span>

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="fda1e-150">Hello l'output è simile toohello seguente esempio per Windows Server:</span><span class="sxs-lookup"><span data-stu-id="fda1e-150">hello output is similar toohello following example for Windows Server:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

<span data-ttu-id="fda1e-151">Questo output è in contrasto con hello che seguente macchina virtuale distribuita senza licenze vantaggio di utilizzare ibrida di Azure, ad esempio una macchina virtuale distribuita direttamente dalla raccolta di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="fda1e-151">This output contrasts with hello following VM deployed without Azure Hybrid Use Benefit licensing, such as a VM deployed straight from hello Azure Gallery:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a><span data-ttu-id="fda1e-152">Procedura dettagliata per la distribuzione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="fda1e-152">Detailed PowerShell deployment walkthrough</span></span>
<span data-ttu-id="fda1e-153">esempio Hello dettagliate Mostra i passaggi di PowerShell di una distribuzione completa di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fda1e-153">hello following detailed PowerShell steps show a full deployment of a VM.</span></span> <span data-ttu-id="fda1e-154">È possibile leggere ulteriori informazioni di contesto come toohello effettivo cmdlet e i diversi componenti viene creati [creare una macchina virtuale Windows usando Gestione risorse e PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fda1e-154">You can read more context as toohello actual cmdlets and different components being created in [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="fda1e-155">Verranno creati il gruppo di risorse, l'account di archiviazione e la rete virtuale, quindi verrà definita e creata la VM.</span><span class="sxs-lookup"><span data-stu-id="fda1e-155">You step through creating your resource group, storage account, and virtual networking, then define your VM and finally create your VM.</span></span>

<span data-ttu-id="fda1e-156">Ottenere prima le credenziali in modo sicuro, specificare una località e definire un nome per il gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="fda1e-156">First, securely obtain credentials, set a location, and resource group name:</span></span>

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

<span data-ttu-id="fda1e-157">Creare un IP pubblico:</span><span class="sxs-lookup"><span data-stu-id="fda1e-157">Create a public IP:</span></span>

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

<span data-ttu-id="fda1e-158">Definire la subnet, la scheda di interfaccia di rete e la rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="fda1e-158">Define your subnet, NIC, and VNET:</span></span>

```powershell
$subnetName = "mySubnet"
$nicName = "myNIC"
$vnetName = "myVnet"
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/8
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location `
    -AddressPrefix 10.0.0.0/8 -Subnet $subnetconfig
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroupName -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $publicIP.Id
```

<span data-ttu-id="fda1e-159">Assegnare un nome alla macchina virtuale e creare una configurazione:</span><span class="sxs-lookup"><span data-stu-id="fda1e-159">Name your VM and create a VM config:</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

<span data-ttu-id="fda1e-160">Definire il sistema operativo:</span><span class="sxs-lookup"><span data-stu-id="fda1e-160">Define your OS:</span></span>

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="fda1e-161">Aggiungere il toohello NIC VM:</span><span class="sxs-lookup"><span data-stu-id="fda1e-161">Add your NIC toohello VM:</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="fda1e-162">Definire toouse account di archiviazione hello:</span><span class="sxs-lookup"><span data-stu-id="fda1e-162">Define hello storage account toouse:</span></span>

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

<span data-ttu-id="fda1e-163">Caricare il disco rigido virtuale, adeguatamente preparato e collegare tooyour macchina virtuale per l'utilizzo:</span><span class="sxs-lookup"><span data-stu-id="fda1e-163">Upload your VHD, suitably prepared, and attach tooyour VM for use:</span></span>

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

<span data-ttu-id="fda1e-164">Infine, creare la macchina virtuale e definire hello licenze tipo tooutilize vantaggio di utilizzare ibrida di Azure:</span><span class="sxs-lookup"><span data-stu-id="fda1e-164">Finally, create your VM and define hello licensing type tooutilize Azure Hybrid Use Benefit:</span></span>

<span data-ttu-id="fda1e-165">Per Windows Server:</span><span class="sxs-lookup"><span data-stu-id="fda1e-165">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a><span data-ttu-id="fda1e-166">Distribuire un set di scalabilità di macchine virtuali tramite un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fda1e-166">Deploy a virtual machine scale set via Resource Manager template</span></span>
<span data-ttu-id="fda1e-167">Nei modelli di Resource Manager del set di scalabilità di macchine virtuali è necessario specificare un parametro aggiuntivo per `licenseType`.</span><span class="sxs-lookup"><span data-stu-id="fda1e-167">Within your VMSS Resource Manager templates, an additional parameter for `licenseType` must be specified.</span></span> <span data-ttu-id="fda1e-168">Altre informazioni sulla [creazione di modelli di Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fda1e-168">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="fda1e-169">Modificare la proprietà di gestione risorse modello tooinclude hello licenseType come parte di virtualMachineProfile del set di scalabilità di hello e distribuire il modello come di consueto: vedere l'esempio seguente utilizzando l'immagine di Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="fda1e-169">Edit your Resource Manager template tooinclude hello licenseType property as part of hello scale set’s virtualMachineProfile and deploy your template as normal - see example below using 2016 Windows Server image:</span></span>


```json
"virtualMachineProfile": {
    "storageProfile": {
        "osDisk": {
            "createOption": "FromImage"
        },
        "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2016-Datacenter",
            "version": "latest"
        }
    },
    "licenseType": "Windows_Server",
    "osProfile": {
            "computerNamePrefix": "[parameters('vmssName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
    }
```

> [!NOTE]
> <span data-ttu-id="fda1e-170">Il supporto per la distribuzione di un set di scalabilità di macchine virtuali con vantaggi AHUB tramite PowerShell e altri strumenti SDK sarà presto disponibile.</span><span class="sxs-lookup"><span data-stu-id="fda1e-170">Support for deploying a virtual machine scale set with AHUB benefits through PowerShell and other SDK tools is coming soon.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="fda1e-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fda1e-171">Next steps</span></span>
<span data-ttu-id="fda1e-172">Altre informazioni sul [Vantaggio Microsoft Azure Hybrid Use](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="fda1e-172">Read more about [Azure Hybrid Use Benefit licensing](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

<span data-ttu-id="fda1e-173">Altre informazioni sull' [uso dei modelli di Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fda1e-173">Learn more about [using Resource Manager templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="fda1e-174">Altre informazioni, vedere [vantaggio di utilizzare ibrida di Azure e Azure Site Recovery rendere ancora più economica tooAzure la migrazione di applicazioni](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span><span class="sxs-lookup"><span data-stu-id="fda1e-174">Learn more about [Azure Hybrid Use Benefit and Azure Site Recovery make migrating applications tooAzure even more cost-effective](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span></span>

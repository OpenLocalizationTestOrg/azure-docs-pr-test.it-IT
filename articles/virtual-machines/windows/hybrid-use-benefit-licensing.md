---
title: Azure Hybrid Use Benefit per Windows Server e Client Windows| Microsoft Docs
description: Informazioni su come ottimizzare i vantaggi di Software Assurance per Windows per trasferire le licenze locali in Azure
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
ms.openlocfilehash: 210635624946ddb293427167e9d476c377bcc9b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a><span data-ttu-id="a85d4-103">Azure Hybrid Use Benefit per Windows Server e Client Windows</span><span class="sxs-lookup"><span data-stu-id="a85d4-103">Azure Hybrid Use Benefit for Windows Server and Windows Client</span></span>
<span data-ttu-id="a85d4-104">Per i clienti con Software Assurance, Azure Hybrid Use Benefit consente di usare le licenze di Windows Server e Client di Windows locali e di eseguire le macchine virtuali di Windows in Azure a costi ridotti.</span><span class="sxs-lookup"><span data-stu-id="a85d4-104">For customers with Software Assurance, Azure Hybrid Use Benefit allows you to use your on-premises Windows Server and Windows Client licenses and run Windows virtual machines in Azure at a reduced cost.</span></span> <span data-ttu-id="a85d4-105">Azure Hybrid Use Benefit per Windows Server include Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2 e Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a85d4-105">Azure Hybrid Use Benefit for Windows Server includes Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2, and Windows Server 2016.</span></span> <span data-ttu-id="a85d4-106">Azure Hybrid Use Benefit per Client Windows include Windows 10.</span><span class="sxs-lookup"><span data-stu-id="a85d4-106">Azure Hybrid Use Benefit for Windows Client includes Windows 10.</span></span> <span data-ttu-id="a85d4-107">Per altre informazioni, vedere la [pagina del vantaggio Azure Hybrid Use per la licenza](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="a85d4-107">For more information, please see the [Azure Hybrid Use Benefit licensing page](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

>[!IMPORTANT]
><span data-ttu-id="a85d4-108">Azure Hybrid Use Benefits per Client Windows è attualmente in anteprima con l'immagine di Windows 10 in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a85d4-108">Azure Hybrid Use Benefits for Windows Client is currently in Preview using the Windows 10 image in the Azure Marketplace.</span></span> <span data-ttu-id="a85d4-109">Solo i clienti Enterprise con Windows 10 Enterprise E3/E5 per utente o Windows VDA per utente (licenze di sottoscrizione utente o le licenze di sottoscrizione utente per i componenti aggiuntivi) idonei ("Licenze di qualificazione") sono idonei.</span><span class="sxs-lookup"><span data-stu-id="a85d4-109">Only Enterprise customers with Windows 10 Enterprise E3/E5 per user or Windows VDA per user (User Subscription Licenses or Add-on User Subscription Licenses) (“Qualifying Licenses”) are eligible.</span></span>
>
>

## <a name="ways-to-use-azure-hybrid-use-benefit"></a><span data-ttu-id="a85d4-110">Modalità di utilizzo del vantaggio Azure Hybrid Use</span><span class="sxs-lookup"><span data-stu-id="a85d4-110">Ways to use Azure Hybrid Use Benefit</span></span>
<span data-ttu-id="a85d4-111">Esistono due modi per distribuire le macchine virtuali Windows con il vantaggio Azure Hybrid Use:</span><span class="sxs-lookup"><span data-stu-id="a85d4-111">There are a couple of different ways to deploy Windows VMs with the Azure Hybrid Use Benefit:</span></span>

1. <span data-ttu-id="a85d4-112">È possibile distribuire le macchine virtuali da [immagini specifiche del Marketplace](#deploy-a-vm-using-the-azure-marketplace) preconfigurate con Azure Hybrid Use Benefit: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008SP1.</span><span class="sxs-lookup"><span data-stu-id="a85d4-112">You can deploy VMs from [specific Marketplace images](#deploy-a-vm-using-the-azure-marketplace) that are pre-configured with Azure Hybrid Use Benefit - Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span>
2. <span data-ttu-id="a85d4-113">È possibile [caricare una macchina virtuale personalizzata](#upload-a-windows-vhd) e [distribuirla usando un modello di Resource Manager](#deploy-a-vm-via-resource-manager) o [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="a85d4-113">You can [upload a custom VM](#upload-a-windows-vhd) and [deploy using a Resource Manager template](#deploy-a-vm-via-resource-manager) or [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span></span>

## <a name="deploy-a-vm-using-the-azure-marketplace"></a><span data-ttu-id="a85d4-114">Distribuire una VM usando Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="a85d4-114">Deploy a VM using the Azure Marketplace</span></span>
<span data-ttu-id="a85d4-115">Le immagini seguenti sono disponibili nel Marketplace preconfigurate con Azure Hybrid Use Benefit: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008SP1.</span><span class="sxs-lookup"><span data-stu-id="a85d4-115">Following images are available in the Marketplace pre-configured with Azure Hybrid Use Benefit: Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span> <span data-ttu-id="a85d4-116">Queste immagini possono essere distribuite direttamente dal portale di Azure, da modelli di Resource Manager o da Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a85d4-116">These images can be deployed directly from the Azure portal, Resource Manager templates, or Azure PowerShell.</span></span>

<span data-ttu-id="a85d4-117">È possibile distribuire queste immagini direttamente dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a85d4-117">You can deploy these images directly from the Azure portal.</span></span> <span data-ttu-id="a85d4-118">Per l'utilizzo in modelli di Resource Manager e con Azure PowerShell, visualizzare l'elenco delle immagini come segue:</span><span class="sxs-lookup"><span data-stu-id="a85d4-118">For use in Resource Manager templates and with Azure PowerShell, view the list of images as follows:</span></span>

<span data-ttu-id="a85d4-119">Per Windows Server:</span><span class="sxs-lookup"><span data-stu-id="a85d4-119">For Windows Server:</span></span>
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- <span data-ttu-id="a85d4-120">2016-Datacenter versione 2016.127.20170406 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="a85d4-120">2016-Datacenter version 2016.127.20170406 or above</span></span>

- <span data-ttu-id="a85d4-121">2012-R2-Datacenter versione 4.127.20170406 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="a85d4-121">2012-R2-Datacenter version 4.127.20170406 or above</span></span>

- <span data-ttu-id="a85d4-122">2012-Datacenter versione 3.127.20170406 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="a85d4-122">2012-Datacenter version 3.127.20170406 or above</span></span>

- <span data-ttu-id="a85d4-123">2008 R2-SP1 versione 2.127.20170406 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="a85d4-123">2008-R2-SP1 version 2.127.20170406 or above</span></span>

<span data-ttu-id="a85d4-124">Per Client Windows:</span><span class="sxs-lookup"><span data-stu-id="a85d4-124">For Windows Client:</span></span>
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a><span data-ttu-id="a85d4-125">Caricare un disco rigido virtuale di Windows Server</span><span class="sxs-lookup"><span data-stu-id="a85d4-125">Upload a Windows Server VHD</span></span>
<span data-ttu-id="a85d4-126">Per distribuire una macchina virtuale di Windows Server in Azure è prima necessario creare un disco rigido virtuale contenente la build di base di Windows.</span><span class="sxs-lookup"><span data-stu-id="a85d4-126">To deploy a Windows Server VM in Azure, you first need to create a VHD that contains your base Windows build.</span></span> <span data-ttu-id="a85d4-127">Questo disco rigido virtuale deve essere correttamente preparato con Sysprep prima di caricarlo in Azure.</span><span class="sxs-lookup"><span data-stu-id="a85d4-127">This VHD must be appropriately prepared via Sysprep before you upload it to Azure.</span></span> <span data-ttu-id="a85d4-128">Sono disponibili [altre informazioni sui requisiti dei dischi rigidi virtuali e sul processo Sysprep](upload-generalized-managed.md) e [Supporto Sysprep per i ruoli server](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="a85d4-128">You can [read more about the VHD requirements and Sysprep process](upload-generalized-managed.md) and [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span> <span data-ttu-id="a85d4-129">Eseguire il backup della VM prima di eseguire Sysprep.</span><span class="sxs-lookup"><span data-stu-id="a85d4-129">Back up the VM before running Sysprep.</span></span> 

<span data-ttu-id="a85d4-130">Verificare di aver prima [installato e configurato l'ultima versione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a85d4-130">Make sure you have [installed and configured the latest Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="a85d4-131">Dopo aver preparato il disco rigido virtuale, caricarlo nell'account di archiviazione di Azure usando il cmdlet `Add-AzureRmVhd` come segue:</span><span class="sxs-lookup"><span data-stu-id="a85d4-131">Once you have prepared your VHD, upload the VHD to your Azure Storage account using the `Add-AzureRmVhd` cmdlet as follows:</span></span>

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> <span data-ttu-id="a85d4-132">Microsoft SQL Server, SharePoint Server e Dynamics possono usare anche le licenza di Software Assurance.</span><span class="sxs-lookup"><span data-stu-id="a85d4-132">Microsoft SQL Server, SharePoint Server, and Dynamics can also utilize your Software Assurance licensing.</span></span> <span data-ttu-id="a85d4-133">È comunque necessario preparare l'immagine di Windows Server installando i componenti dell'applicazione e specificando i codici di licenza corrispondenti, quindi caricando l'immagine del disco in Azure.</span><span class="sxs-lookup"><span data-stu-id="a85d4-133">You still need to prepare the Windows Server image by installing your application components and providing license keys accordingly, then uploading the disk image to Azure.</span></span> <span data-ttu-id="a85d4-134">Esaminare la documentazione appropriata per l'esecuzione di SysPrep con l'applicazione, ad esempio [Considerazioni sull'installazione di SQL Server tramite SysPrep](https://msdn.microsoft.com/library/ee210754.aspx) o [Creare un'immagine di riferimento di SharePoint Server 2016 con Sysprep](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span><span class="sxs-lookup"><span data-stu-id="a85d4-134">Review the appropriate documentation for running Sysprep with your application, such as [Considerations for Installing SQL Server using Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) or [Build a SharePoint Server 2016 Reference Image (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span></span>
>
>

<span data-ttu-id="a85d4-135">Altre informazioni sul [caricamento del disco rigido virtuale in Azure](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span><span class="sxs-lookup"><span data-stu-id="a85d4-135">You can also read more about [uploading the VHD to Azure process](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span></span>


## <a name="deploy-a-vm-via-resource-manager-template"></a><span data-ttu-id="a85d4-136">Distribuire una macchina virtuale con il modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a85d4-136">Deploy a VM via Resource Manager Template</span></span>
<span data-ttu-id="a85d4-137">Nei modelli di Resource Manager è possibile specificare un parametro aggiuntivo per `licenseType`.</span><span class="sxs-lookup"><span data-stu-id="a85d4-137">Within your Resource Manager templates, an additional parameter for `licenseType` can be specified.</span></span> <span data-ttu-id="a85d4-138">Altre informazioni sulla [creazione di modelli di Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a85d4-138">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="a85d4-139">Dopo aver caricato il disco rigido virtuale in Azure, modificare il modello di Resource Manager per includere il tipo di licenza come parte del provider di calcolo e distribuire il modello come di consueto:</span><span class="sxs-lookup"><span data-stu-id="a85d4-139">Once you have your VHD uploaded to Azure, edit you Resource Manager template to include the license type as part of the compute provider and deploy your template as normal:</span></span>

<span data-ttu-id="a85d4-140">Per Windows Server:</span><span class="sxs-lookup"><span data-stu-id="a85d4-140">For Windows Server:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

<span data-ttu-id="a85d4-141">Per Client Windows da usare solo con l'immagine di Azure Marketplace:</span><span class="sxs-lookup"><span data-stu-id="a85d4-141">For Windows Client to use with Azure Marketplace Image only:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a><span data-ttu-id="a85d4-142">Distribuire una macchina virtuale con l'avvio rapido di PowerShell</span><span class="sxs-lookup"><span data-stu-id="a85d4-142">Deploy a VM via PowerShell quickstart</span></span>
<span data-ttu-id="a85d4-143">Quando si distribuisce la macchina virtuale Windows Server con PowerShell è presente un parametro aggiuntivo per `-LicenseType`.</span><span class="sxs-lookup"><span data-stu-id="a85d4-143">When deploying your Windows Server VM via PowerShell, you have an additional parameter for `-LicenseType`.</span></span> <span data-ttu-id="a85d4-144">Dopo aver caricato il disco rigido virtuale in Azure, creare una nuova VM usando `New-AzureRmVM` e specificare il tipo di licenza come segue:</span><span class="sxs-lookup"><span data-stu-id="a85d4-144">Once you have your VHD uploaded to Azure, you create a VM using `New-AzureRmVM` and specify the licensing type as follows:</span></span>

<span data-ttu-id="a85d4-145">Per Windows Server:</span><span class="sxs-lookup"><span data-stu-id="a85d4-145">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

<span data-ttu-id="a85d4-146">Per Client Windows da usare solo con l'immagine di Azure Marketplace:</span><span class="sxs-lookup"><span data-stu-id="a85d4-146">For Windows Client to use with Azure Marketplace Image only:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

<span data-ttu-id="a85d4-147">È possibile [leggere una procedura più dettagliata sulla distribuzione di una VM in Azure con PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) più avanti nel documento oppure vedere una guida più descrittiva con i diversi passaggi per [creare una VM Windows usando Resource Manager e PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a85d4-147">You can [read a more detailed walkthrough on deploying a VM in Azure via PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) below, or read a more descriptive guide on the different steps to [create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="verify-your-vm-is-utilizing-the-licensing-benefit"></a><span data-ttu-id="a85d4-148">Verificare che la macchina virtuale usi il vantaggio della licenza</span><span class="sxs-lookup"><span data-stu-id="a85d4-148">Verify your VM is utilizing the licensing benefit</span></span>
<span data-ttu-id="a85d4-149">Dopo avere distribuito la VM con il metodo di distribuzione tramite PowerShell o Resource Manager, verificare il tipo di licenza con `Get-AzureRmVM` come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a85d4-149">Once you have deployed your VM through either the PowerShell or Resource Manager deployment method, verify the license type with `Get-AzureRmVM` as follows:</span></span>

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="a85d4-150">L'output è simile all'esempio seguente per Windows Server:</span><span class="sxs-lookup"><span data-stu-id="a85d4-150">The output is similar to the following example for Windows Server:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

<span data-ttu-id="a85d4-151">L'output differisce da quello della seguente VM distribuita senza vantaggio Azure Hybrid Use, quale ad esempio una VM distribuita direttamente dalla raccolta di Azure:</span><span class="sxs-lookup"><span data-stu-id="a85d4-151">This output contrasts with the following VM deployed without Azure Hybrid Use Benefit licensing, such as a VM deployed straight from the Azure Gallery:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a><span data-ttu-id="a85d4-152">Procedura dettagliata per la distribuzione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="a85d4-152">Detailed PowerShell deployment walkthrough</span></span>
<span data-ttu-id="a85d4-153">La procedura dettagliata per PowerShell seguente illustra la distribuzione completa di una VM.</span><span class="sxs-lookup"><span data-stu-id="a85d4-153">The following detailed PowerShell steps show a full deployment of a VM.</span></span> <span data-ttu-id="a85d4-154">Altre informazioni sui cmdlet effettivi e sui diversi componenti creati sono disponibili in [Creare una VM Windows con Resource Manager e PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a85d4-154">You can read more context as to the actual cmdlets and different components being created in [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="a85d4-155">Verranno creati il gruppo di risorse, l'account di archiviazione e la rete virtuale, quindi verrà definita e creata la VM.</span><span class="sxs-lookup"><span data-stu-id="a85d4-155">You step through creating your resource group, storage account, and virtual networking, then define your VM and finally create your VM.</span></span>

<span data-ttu-id="a85d4-156">Ottenere prima le credenziali in modo sicuro, specificare una località e definire un nome per il gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="a85d4-156">First, securely obtain credentials, set a location, and resource group name:</span></span>

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

<span data-ttu-id="a85d4-157">Creare un IP pubblico:</span><span class="sxs-lookup"><span data-stu-id="a85d4-157">Create a public IP:</span></span>

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

<span data-ttu-id="a85d4-158">Definire la subnet, la scheda di interfaccia di rete e la rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="a85d4-158">Define your subnet, NIC, and VNET:</span></span>

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

<span data-ttu-id="a85d4-159">Assegnare un nome alla macchina virtuale e creare una configurazione:</span><span class="sxs-lookup"><span data-stu-id="a85d4-159">Name your VM and create a VM config:</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

<span data-ttu-id="a85d4-160">Definire il sistema operativo:</span><span class="sxs-lookup"><span data-stu-id="a85d4-160">Define your OS:</span></span>

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="a85d4-161">Aggiungere la scheda di interfaccia di rete alla macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="a85d4-161">Add your NIC to the VM:</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="a85d4-162">Definire l'account di archiviazione da usare:</span><span class="sxs-lookup"><span data-stu-id="a85d4-162">Define the storage account to use:</span></span>

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

<span data-ttu-id="a85d4-163">Caricare il disco rigido virtuale adeguatamente preparato e collegarlo alla macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="a85d4-163">Upload your VHD, suitably prepared, and attach to your VM for use:</span></span>

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

<span data-ttu-id="a85d4-164">Creare infine la macchina virtuale e definire il tipo di licenza per l'uso del vantaggio Azure Hybrid Use:</span><span class="sxs-lookup"><span data-stu-id="a85d4-164">Finally, create your VM and define the licensing type to utilize Azure Hybrid Use Benefit:</span></span>

<span data-ttu-id="a85d4-165">Per Windows Server:</span><span class="sxs-lookup"><span data-stu-id="a85d4-165">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a><span data-ttu-id="a85d4-166">Distribuire un set di scalabilità di macchine virtuali tramite un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a85d4-166">Deploy a virtual machine scale set via Resource Manager template</span></span>
<span data-ttu-id="a85d4-167">Nei modelli di Resource Manager del set di scalabilità di macchine virtuali è necessario specificare un parametro aggiuntivo per `licenseType`.</span><span class="sxs-lookup"><span data-stu-id="a85d4-167">Within your VMSS Resource Manager templates, an additional parameter for `licenseType` must be specified.</span></span> <span data-ttu-id="a85d4-168">Altre informazioni sulla [creazione di modelli di Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a85d4-168">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="a85d4-169">Modificare il modello di Resource Manager per includere la proprietà licenseType come parte dell'elemento virtualMachineProfile del set di scalabilità e distribuire il modello come di consueto. Vedere l'esempio seguente che usa l'immagine di Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="a85d4-169">Edit your Resource Manager template to include the licenseType property as part of the scale set’s virtualMachineProfile and deploy your template as normal - see example below using 2016 Windows Server image:</span></span>


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
> <span data-ttu-id="a85d4-170">Il supporto per la distribuzione di un set di scalabilità di macchine virtuali con vantaggi AHUB tramite PowerShell e altri strumenti SDK sarà presto disponibile.</span><span class="sxs-lookup"><span data-stu-id="a85d4-170">Support for deploying a virtual machine scale set with AHUB benefits through PowerShell and other SDK tools is coming soon.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="a85d4-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a85d4-171">Next steps</span></span>
<span data-ttu-id="a85d4-172">Altre informazioni sul [Vantaggio Microsoft Azure Hybrid Use](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="a85d4-172">Read more about [Azure Hybrid Use Benefit licensing](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

<span data-ttu-id="a85d4-173">Altre informazioni sull' [uso dei modelli di Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a85d4-173">Learn more about [using Resource Manager templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="a85d4-174">Altre informazioni su [Azure Hybrid Use Benefit and Azure Site Recovery make migrating applications to Azure even more cost-effective](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/) (Azure Hybrid Use Benefit e Azure Site Recovery rendono le applicazioni che eseguono la migrazione in Azure ancora più convenienti).</span><span class="sxs-lookup"><span data-stu-id="a85d4-174">Learn more about [Azure Hybrid Use Benefit and Azure Site Recovery make migrating applications to Azure even more cost-effective](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span></span>

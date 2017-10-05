---
title: "Distribuire un'app nei set di scalabilità di macchine virtuali"
description: "Usare le estensioni per distribuire un'app nel set di scalabilità della macchina virtuale di Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: fa7d9d3bef4cb326844ede76171e8c566e87116b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a><span data-ttu-id="c017e-103">Distribuire l'applicazione nei set di scalabilità delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="c017e-103">Deploy your application on virtual machine scale sets</span></span>

<span data-ttu-id="c017e-104">Questo articolo descrive diverse modalità di installazione di software durante il provisioning del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="c017e-104">This article describes different ways of how to install software at the time the scale set is provisioned.</span></span>

<span data-ttu-id="c017e-105">È possibile esaminare l'articolo [Panoramica sulla progettazione del set di scalabilità](virtual-machine-scale-sets-design-overview.md) che descrive alcuni dei limiti imposti dal set di scalabilità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c017e-105">You may want to review the [Scale Set Design Overview](virtual-machine-scale-sets-design-overview.md) article, which describes some of the limits imposed by virtual machine scale sets.</span></span>

## <a name="capture-and-reuse-an-image"></a><span data-ttu-id="c017e-106">Acquisire e riusare un'immagine</span><span class="sxs-lookup"><span data-stu-id="c017e-106">Capture and reuse an image</span></span>

<span data-ttu-id="c017e-107">È possibile usare una macchina virtuale disponibile in Azure per preparare un'immagine di base per il set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="c017e-107">You can use a virtual machine you have in Azure to prepare a base-image for your scale set.</span></span> <span data-ttu-id="c017e-108">Questo processo crea un disco gestito nell'account di archiviazione, a cui è possibile fare riferimento come immagine di base per il set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="c017e-108">This process creates a managed disk in your storage account, which you can reference as the base image for your scale set.</span></span> 

<span data-ttu-id="c017e-109">Seguire anche questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c017e-109">Do the following steps:</span></span>

1. <span data-ttu-id="c017e-110">Creare una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="c017e-110">Create an Azure Virtual Machine</span></span>
   * <span data-ttu-id="c017e-111">[Linux][linux-vm-create]</span><span class="sxs-lookup"><span data-stu-id="c017e-111">[Linux][linux-vm-create]</span></span>
   * <span data-ttu-id="c017e-112">[Windows][windows-vm-create]</span><span class="sxs-lookup"><span data-stu-id="c017e-112">[Windows][windows-vm-create]</span></span>

2. <span data-ttu-id="c017e-113">Connettersi da remoto alla macchina virtuale e personalizzare il sistema in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="c017e-113">Remote into the virtual machine and customize the system to your liking.</span></span>

   <span data-ttu-id="c017e-114">Se lo si desidera, a questo punto è possibile installare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c017e-114">If you want, you can install your application now.</span></span> <span data-ttu-id="c017e-115">Tuttavia, tenere presente che per installare l'applicazione a questo punto potrebbe essere necessario un'operazione di aggiornamento più complessa perché potrebbe essere prima necessario rimuoverla.</span><span class="sxs-lookup"><span data-stu-id="c017e-115">However, know that by installing your application now, you may make upgrading your application more complicated because you may need to remove it first.</span></span> <span data-ttu-id="c017e-116">In alternativa, è possibile usare questo passaggio per installare i prerequisiti necessari all'applicazione, ad esempio una funzionalità specifica di runtime o del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="c017e-116">Instead, you can use this step to install any prerequisites your application may need, like a specific runtime or operating system feature.</span></span>

3. <span data-ttu-id="c017e-117">Seguire l'esercitazione "Acquisire una macchina" per [Linux][linux-vm-capture] o [Windows][windows-vm-capture].</span><span class="sxs-lookup"><span data-stu-id="c017e-117">Follow the "capture a machine" tutorial for either [Linux][linux-vm-capture] or [Windows][windows-vm-capture].</span></span>

4. <span data-ttu-id="c017e-118">Creare un [set di scalabilità della macchina virtuale][vmss-create] con l'URI dell'immagine acquisito nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="c017e-118">Create a [Virtual Machine Scale Set][vmss-create] with the image URI you captured in the previous step.</span></span>

<span data-ttu-id="c017e-119">Per altre informazioni sui dischi, vedere [Panoramica di Managed Disks](../virtual-machines/windows/managed-disks-overview.md) e [Usare dischi dati collegati](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="c017e-119">For more information about disks, see [Managed Disks Overview](../virtual-machines/windows/managed-disks-overview.md) and [Use Attached Data Disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

## <a name="install-when-the-scale-set-is-provisioned"></a><span data-ttu-id="c017e-120">Installare quando viene eseguito il provisioning del set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="c017e-120">Install when the scale set is provisioned</span></span>

<span data-ttu-id="c017e-121">Le estensioni della macchina virtuale possono essere applicate a un set di scalabilità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c017e-121">Virtual machine extensions can be applied to a virtual machine scale set.</span></span> <span data-ttu-id="c017e-122">Con un'estensione della macchina virtuale, è possibile personalizzare le macchine virtuali in un set di scalabilità come gruppo intero.</span><span class="sxs-lookup"><span data-stu-id="c017e-122">With a virtual machine extension, you can customize the virtual machines in a scale set as a whole group.</span></span> <span data-ttu-id="c017e-123">Per altre informazioni sulle estensioni, vedere [Estensioni della macchina virtuale](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c017e-123">For more information about extensions, see [Virtual Machine Extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="c017e-124">È possibile usare tre principali estensioni, a seconda che il sistema operativo si basi su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="c017e-124">There are three main extensions you can use, depending on if your operating system is Linux-based or Windows-based.</span></span>

### <a name="windows"></a><span data-ttu-id="c017e-125">Windows</span><span class="sxs-lookup"><span data-stu-id="c017e-125">Windows</span></span>

<span data-ttu-id="c017e-126">Per un sistema operativo basato su Windows, usare l'estensione **Custom Script v1.8** o l'estensione **PowerShell DSC**.</span><span class="sxs-lookup"><span data-stu-id="c017e-126">For a Windows-based operating system, use either the **Custom Script v1.8** extension, or the **PowerShell DSC** extension.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="c017e-127">Custom Script</span><span class="sxs-lookup"><span data-stu-id="c017e-127">Custom Script</span></span>

<span data-ttu-id="c017e-128">L'estensione Custom Script esegue uno script in ogni istanza della macchina virtuale nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="c017e-128">The Custom Script extension runs a script on each virtual machine instance in the scale set.</span></span> <span data-ttu-id="c017e-129">Un file di configurazione o una variabile indica i file che vengono scaricati nella macchina virtuale, quindi il comando eseguito.</span><span class="sxs-lookup"><span data-stu-id="c017e-129">A config file or variable indicates which files are downloaded to the virtual machine, and then what command runs.</span></span> <span data-ttu-id="c017e-130">Questi vengono usati ad esempio per eseguire un programma di installazione, uno script, un file batch o un file eseguibile.</span><span class="sxs-lookup"><span data-stu-id="c017e-130">You could use this to run an installer, a script, a batch file, any executable for example.</span></span>

<span data-ttu-id="c017e-131">PowerShell usa una tabella hash per le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="c017e-131">PowerShell uses a hashtable for the settings.</span></span> <span data-ttu-id="c017e-132">Questo esempio configura l'estensione dello script personalizzato per eseguire uno script di PowerShell che consente di installare IIS.</span><span class="sxs-lookup"><span data-stu-id="c017e-132">This example configures the custom script extension to run a PowerShell script that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add the extension to the config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send the new config to Azure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="c017e-133">Usare lo switch `-ProtectedSetting` per tutte le impostazioni che potrebbero contenere informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="c017e-133">Use the `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

---------


<span data-ttu-id="c017e-134">L'interfaccia della riga di comando di Azure usa un file JSON per le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="c017e-134">Azure CLI uses a json file for the settings.</span></span> <span data-ttu-id="c017e-135">Questo esempio configura l'estensione dello script personalizzato per eseguire uno script di PowerShell che consente di installare IIS.</span><span class="sxs-lookup"><span data-stu-id="c017e-135">This example configures the custom script extension to run a PowerShell script that installs IIS.</span></span> <span data-ttu-id="c017e-136">Salvare il file JSON seguente come _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="c017e-136">Save the following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

<span data-ttu-id="c017e-137">Quindi, eseguire questo comando dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="c017e-137">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="c017e-138">Usare lo switch `--protected-settings` per tutte le impostazioni che potrebbero contenere informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="c017e-138">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="powershell-dsc"></a><span data-ttu-id="c017e-139">PowerShell DSC</span><span class="sxs-lookup"><span data-stu-id="c017e-139">PowerShell DSC</span></span>

<span data-ttu-id="c017e-140">È possibile usare PowerShell DSC per personalizzare le istanze della macchina virtuale del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="c017e-140">You can use PowerShell DSC to customize the scale set vm instances.</span></span> <span data-ttu-id="c017e-141">L'estensione **DSC** pubblicata da **Microsoft.Powershell** distribuisce ed esegue la configurazione DSC indicata in ogni istanza della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c017e-141">The **DSC** extension published by **Microsoft.Powershell** deploys and runs the provided DSC configuration on each virtual machine instance.</span></span> <span data-ttu-id="c017e-142">Un file di configurazione o una variabile indica l'estensione in cui si trova il pacchetto *.zip* e la combinazione di _funzione e script_ da eseguire.</span><span class="sxs-lookup"><span data-stu-id="c017e-142">A config file or variable tells the extension where *.zip* package is, and which _script-function_ combination to run.</span></span>

<span data-ttu-id="c017e-143">PowerShell usa una tabella hash per le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="c017e-143">PowerShell uses a hashtable for the settings.</span></span> <span data-ttu-id="c017e-144">Questo esempio distribuisce un pacchetto DSC che consente di installare IIS.</span><span class="sxs-lookup"><span data-stu-id="c017e-144">This example deploys a DSC package that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add the extension to the config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send the new config to Azure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="c017e-145">Usare lo switch `-ProtectedSetting` per tutte le impostazioni che potrebbero contenere informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="c017e-145">Use the `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

-----------

<span data-ttu-id="c017e-146">L'interfaccia della riga di comando di Azure usa un file JSON per le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="c017e-146">Azure CLI uses a json for the settings.</span></span> <span data-ttu-id="c017e-147">Questo esempio distribuisce un pacchetto DSC che consente di installare IIS.</span><span class="sxs-lookup"><span data-stu-id="c017e-147">This example deploys a DSC package that installs IIS.</span></span> <span data-ttu-id="c017e-148">Salvare il file JSON seguente come _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="c017e-148">Save the following json file as _settings.json_.</span></span>

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

<span data-ttu-id="c017e-149">Quindi, eseguire questo comando dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="c017e-149">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="c017e-150">Usare lo switch `--protected-settings` per tutte le impostazioni che potrebbero contenere informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="c017e-150">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="linux"></a><span data-ttu-id="c017e-151">Linux</span><span class="sxs-lookup"><span data-stu-id="c017e-151">Linux</span></span>

<span data-ttu-id="c017e-152">Durante la creazione Linux può usare l'estensione **Custom Script v2.0** o **cloud-init**.</span><span class="sxs-lookup"><span data-stu-id="c017e-152">Linux can use either the **Custom Script v2.0** extension or use **cloud-init** during creation.</span></span>

<span data-ttu-id="c017e-153">Custom script è un'estensione semplice che scarica i file per istanze di macchine virtuali ed esegue un comando.</span><span class="sxs-lookup"><span data-stu-id="c017e-153">Custom script is a simple extension that downloads files to the virtual machine instances, and runs a command.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="c017e-154">Custom Script</span><span class="sxs-lookup"><span data-stu-id="c017e-154">Custom Script</span></span>

<span data-ttu-id="c017e-155">Salvare il file JSON seguente come _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="c017e-155">Save the following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

<span data-ttu-id="c017e-156">Usare l'interfaccia della riga di comando di Azure per aggiungere questa estensione a un set di scalabilità della macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="c017e-156">Use the Azure CLI to add this extension to an existing virtual machine scale set.</span></span> <span data-ttu-id="c017e-157">Ogni macchina virtuale nel set di scalabilità esegue automaticamente l'estensione.</span><span class="sxs-lookup"><span data-stu-id="c017e-157">Each virtual machine in the scale set automatically runs the extension.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="c017e-158">Usare lo switch `--protected-settings` per tutte le impostazioni che potrebbero contenere informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="c017e-158">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

#### <a name="cloud-init"></a><span data-ttu-id="c017e-159">cloud-init</span><span class="sxs-lookup"><span data-stu-id="c017e-159">Cloud-Init</span></span>

<span data-ttu-id="c017e-160">Cloud-Init viene usata durante la creazione del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="c017e-160">Cloud-Init is used when the scale set is created.</span></span> <span data-ttu-id="c017e-161">Innanzitutto, creare un file locale denominato _cloud-init.txt_ e aggiungere la configurazione.</span><span class="sxs-lookup"><span data-stu-id="c017e-161">First, create a local file named _cloud-init.txt_ and add your configuration to it.</span></span> <span data-ttu-id="c017e-162">Ad esempio, vedere [questo gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span><span class="sxs-lookup"><span data-stu-id="c017e-162">For example, see [this gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span></span>

<span data-ttu-id="c017e-163">Usare l'interfaccia della riga di comando di Azure per creare un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="c017e-163">Use the Azure CLI to create a scale set.</span></span> <span data-ttu-id="c017e-164">Il campo `--custom-data` accetta il nome del file di uno script cloud-init.</span><span class="sxs-lookup"><span data-stu-id="c017e-164">The `--custom-data` field accepts the file name of a cloud-init script.</span></span>

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a><span data-ttu-id="c017e-165">Gestione degli aggiornamenti dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="c017e-165">How do I manage application updates?</span></span>

<span data-ttu-id="c017e-166">Se l'applicazione è stata distribuita tramite un'estensione, modificare la definizione dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="c017e-166">If you deployed your application through an extension, alter the extension definition in some way.</span></span> <span data-ttu-id="c017e-167">Questa modifica fa sì che l'estensione venga ridistribuita a tutte le istanze della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c017e-167">This change causes the extension to be redeployed to all virtual machine instances.</span></span> <span data-ttu-id="c017e-168">**È necessario** modificare alcuni elementi dell'estensione, ad esempio è possibile rinominare un file di riferimento, altrimenti Azure non vede la modifica apportata all'estensione.</span><span class="sxs-lookup"><span data-stu-id="c017e-168">Something **must** be changed about the extension, such as renaming a referenced file, otherwise, Azure does not see that the extension has changed.</span></span>

<span data-ttu-id="c017e-169">Se è stato eseguito un backup dell'applicazione nell'immagine del sistema operativo, usare una pipeline di distribuzione automatica per gli aggiornamenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c017e-169">If you baked the application into your own operating system image, use an automated deployment pipeline for application updates.</span></span> <span data-ttu-id="c017e-170">Progettare l'architettura per facilitare il passaggio rapido di un set di scalabilità temporaneo in produzione.</span><span class="sxs-lookup"><span data-stu-id="c017e-170">Design your architecture to facilitate rapid swapping of a staged scale set into production.</span></span> <span data-ttu-id="c017e-171">Un buon esempio di questo approccio è rappresentato dall'[uso del driver Spinnaker di Azure](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span><span class="sxs-lookup"><span data-stu-id="c017e-171">A good example of this approach is the [Azure Spinnaker driver work](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span></span>

<span data-ttu-id="c017e-172">[Packer](https://www.packer.io/) e [Terraform](https://www.terraform.io/) supportano Azure Resource Manager; pertanto, è anche possibile definire le immagini "come codice" e compilarle in Azure, quindi usare il disco rigido virtuale nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="c017e-172">[Packer](https://www.packer.io/) and [Terraform](https://www.terraform.io/) support Azure Resource Manager, so you can also define your images "as code" and build them in Azure, then use the VHD in your scale set.</span></span> <span data-ttu-id="c017e-173">Tuttavia, tale approccio diventerebbe problematico per le immagini Marketplace, in cui gli script personalizzati/le estensioni acquistano importanza in quanto i bit non vengono modificati direttamente da Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c017e-173">However, doing so would become problematic for marketplace images, where extensions/custom scripts become more important since you don’t directly manipulate bits from marketplace.</span></span>

## <a name="what-happens-when-a-scale-set-scales-out"></a><span data-ttu-id="c017e-174">Cosa accade in caso di aumento della capacità di un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="c017e-174">What happens when a scale set scales out?</span></span>
<span data-ttu-id="c017e-175">Quando si aggiungono una o più macchine virtuali a un set di scalabilità, l'applicazione viene installata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c017e-175">When you add one or more virtual machines to a scale set, the application is automatically installed.</span></span> <span data-ttu-id="c017e-176">Se ad esempio il set di scalabilità ha estensioni definite, queste vengono eseguite ogni volta che viene creata una nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c017e-176">For example if the scale set has extensions defined, they run on a new virtual machine each time it is created.</span></span> <span data-ttu-id="c017e-177">Se il set di scalabilità è basato su un'immagine personalizzata, qualsiasi nuova macchina virtuale è una copia dell'immagine di origine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c017e-177">If the scale set is based on a custom image, any new virtual machine is a copy of the source custom image.</span></span> <span data-ttu-id="c017e-178">Se le macchine virtuali del set di scalabilità sono host del contenitore, potrebbe essere necessario il codice di avvio per caricare i contenitori in un'estensione Custom Script.</span><span class="sxs-lookup"><span data-stu-id="c017e-178">If the scale set virtual machines are container hosts, then you might have startup code to load the containers in a Custom Script Extension.</span></span> <span data-ttu-id="c017e-179">In alternativa, un'estensione potrebbe installare un agente che esegue la registrazione con un agente di orchestrazione del cluster, ad esempio il servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="c017e-179">Or, an extension might install an agent that registers with a cluster orchestrator, such as Azure Container Service.</span></span>


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a><span data-ttu-id="c017e-180">Come distribuire un aggiornamento del sistema operativo nei domini di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="c017e-180">How do you roll out an OS update across update domains?</span></span>
<span data-ttu-id="c017e-181">Si supponga di voler aggiornare un'immagine del sistema operativo mantenendo in esecuzione il set di scalabilità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c017e-181">Suppose you want to update your OS image while keeping the virtual machine scale set running.</span></span> <span data-ttu-id="c017e-182">PowerShell e l'interfaccia della riga di comando di Azure possono aggiornare le immagini della macchina virtuale, per una macchina virtuale alla volta.</span><span class="sxs-lookup"><span data-stu-id="c017e-182">PowerShell and the Azure CLI can update the virtual machine images, one virtual machine at a time.</span></span> <span data-ttu-id="c017e-183">L'articolo [Aggiornare un set di scalabilità di macchine virtuali](./virtual-machine-scale-sets-upgrade-scale-set.md) include altre informazioni sulle opzioni disponibili per eseguire aggiornamenti del sistema operativo in un set di scalabilità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c017e-183">The [Upgrade a Virtual Machine Scale Set](./virtual-machine-scale-sets-upgrade-scale-set.md) article also provides further information on what options are available to perform an operating system upgrade across a virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c017e-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c017e-184">Next steps</span></span>

* [<span data-ttu-id="c017e-185">Usare PowerShell per gestire il set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="c017e-185">Use PowerShell to manage your scale set.</span></span>](virtual-machine-scale-sets-windows-manage.md)
* [<span data-ttu-id="c017e-186">Creare un modello del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="c017e-186">Create a scale set template.</span></span>](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md


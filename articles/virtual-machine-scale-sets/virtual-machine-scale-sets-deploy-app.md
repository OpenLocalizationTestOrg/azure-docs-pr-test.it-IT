---
title: "Imposta aaaDeploy un'app su scalabilità della macchina virtuale"
description: "Utilizzare le estensioni toodepoy un'app nel set di scalabilità di macchine virtuali di Azure."
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
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a><span data-ttu-id="dbd08-103">Distribuire l'applicazione nei set di scalabilità delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="dbd08-103">Deploy your application on virtual machine scale sets</span></span>

<span data-ttu-id="dbd08-104">In questo articolo descrive diversi modi di impostazione software tooinstall hello hello scala viene eseguito il provisioning.</span><span class="sxs-lookup"><span data-stu-id="dbd08-104">This article describes different ways of how tooinstall software at hello time hello scale set is provisioned.</span></span>

<span data-ttu-id="dbd08-105">È opportuno hello tooreview [Panoramica sulla progettazione di Set di scalabilità](virtual-machine-scale-sets-design-overview.md) articolo vengono descritti alcuni dei limiti di hello imposti dal set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="dbd08-105">You may want tooreview hello [Scale Set Design Overview](virtual-machine-scale-sets-design-overview.md) article, which describes some of hello limits imposed by virtual machine scale sets.</span></span>

## <a name="capture-and-reuse-an-image"></a><span data-ttu-id="dbd08-106">Acquisire e riusare un'immagine</span><span class="sxs-lookup"><span data-stu-id="dbd08-106">Capture and reuse an image</span></span>

<span data-ttu-id="dbd08-107">È possibile utilizzare una macchina virtuale che in Azure tooprepare un'immagine di base per la scala impostate.</span><span class="sxs-lookup"><span data-stu-id="dbd08-107">You can use a virtual machine you have in Azure tooprepare a base-image for your scale set.</span></span> <span data-ttu-id="dbd08-108">Questo processo crea un disco gestito nell'account di archiviazione, è possibile fare riferimento come immagine di base hello per il set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="dbd08-108">This process creates a managed disk in your storage account, which you can reference as hello base image for your scale set.</span></span> 

<span data-ttu-id="dbd08-109">Hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="dbd08-109">Do hello following steps:</span></span>

1. <span data-ttu-id="dbd08-110">Creare una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="dbd08-110">Create an Azure Virtual Machine</span></span>
   * <span data-ttu-id="dbd08-111">[Linux][linux-vm-create]</span><span class="sxs-lookup"><span data-stu-id="dbd08-111">[Linux][linux-vm-create]</span></span>
   * <span data-ttu-id="dbd08-112">[Windows][windows-vm-create]</span><span class="sxs-lookup"><span data-stu-id="dbd08-112">[Windows][windows-vm-create]</span></span>

2. <span data-ttu-id="dbd08-113">Remoto in hello macchina virtuale e personalizzare desiderato di tooyour sistema hello.</span><span class="sxs-lookup"><span data-stu-id="dbd08-113">Remote into hello virtual machine and customize hello system tooyour liking.</span></span>

   <span data-ttu-id="dbd08-114">Se lo si desidera, a questo punto è possibile installare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dbd08-114">If you want, you can install your application now.</span></span> <span data-ttu-id="dbd08-115">Può tuttavia sapere che con l'installazione dell'applicazione a questo punto, è possibile effettuare l'aggiornamento, l'applicazione più complessa poiché potrebbe essere necessario tooremove il primo.</span><span class="sxs-lookup"><span data-stu-id="dbd08-115">However, know that by installing your application now, you may make upgrading your application more complicated because you may need tooremove it first.</span></span> <span data-ttu-id="dbd08-116">In alternativa, è possibile utilizzare tooinstall questo passaggio gli eventuali prerequisiti che dell'applicazione potrebbe essere necessario, ad esempio una funzionalità di runtime o del sistema operativo specifica.</span><span class="sxs-lookup"><span data-stu-id="dbd08-116">Instead, you can use this step tooinstall any prerequisites your application may need, like a specific runtime or operating system feature.</span></span>

3. <span data-ttu-id="dbd08-117">Seguire l'esercitazione "acquisire una macchina" hello per uno [Linux] [ linux-vm-capture] o [Windows][windows-vm-capture].</span><span class="sxs-lookup"><span data-stu-id="dbd08-117">Follow hello "capture a machine" tutorial for either [Linux][linux-vm-capture] or [Windows][windows-vm-capture].</span></span>

4. <span data-ttu-id="dbd08-118">Creare un [Set di scalabilità della macchina virtuale] [ vmss-create] con hello immagine acquisita nel passaggio precedente hello URI.</span><span class="sxs-lookup"><span data-stu-id="dbd08-118">Create a [Virtual Machine Scale Set][vmss-create] with hello image URI you captured in hello previous step.</span></span>

<span data-ttu-id="dbd08-119">Per altre informazioni sui dischi, vedere [Panoramica di Managed Disks](../virtual-machines/windows/managed-disks-overview.md) e [Usare dischi dati collegati](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="dbd08-119">For more information about disks, see [Managed Disks Overview](../virtual-machines/windows/managed-disks-overview.md) and [Use Attached Data Disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

## <a name="install-when-hello-scale-set-is-provisioned"></a><span data-ttu-id="dbd08-120">Installare quando viene eseguito il provisioning di set di scalabilità hello</span><span class="sxs-lookup"><span data-stu-id="dbd08-120">Install when hello scale set is provisioned</span></span>

<span data-ttu-id="dbd08-121">Le estensioni di macchina virtuale possono essere applicato tooa set di scalabilità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dbd08-121">Virtual machine extensions can be applied tooa virtual machine scale set.</span></span> <span data-ttu-id="dbd08-122">Con un'estensione della macchina virtuale, è possibile personalizzare hello le macchine virtuali in un set come un intero gruppo di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="dbd08-122">With a virtual machine extension, you can customize hello virtual machines in a scale set as a whole group.</span></span> <span data-ttu-id="dbd08-123">Per altre informazioni sulle estensioni, vedere [Estensioni della macchina virtuale](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dbd08-123">For more information about extensions, see [Virtual Machine Extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="dbd08-124">È possibile usare tre principali estensioni, a seconda che il sistema operativo si basi su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="dbd08-124">There are three main extensions you can use, depending on if your operating system is Linux-based or Windows-based.</span></span>

### <a name="windows"></a><span data-ttu-id="dbd08-125">Windows</span><span class="sxs-lookup"><span data-stu-id="dbd08-125">Windows</span></span>

<span data-ttu-id="dbd08-126">Per un sistema operativo basato su Windows, utilizzare uno hello **v 1.8 Custom Script** estensione o hello **PowerShell DSC** estensione.</span><span class="sxs-lookup"><span data-stu-id="dbd08-126">For a Windows-based operating system, use either hello **Custom Script v1.8** extension, or hello **PowerShell DSC** extension.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="dbd08-127">Custom Script</span><span class="sxs-lookup"><span data-stu-id="dbd08-127">Custom Script</span></span>

<span data-ttu-id="dbd08-128">estensione Script personalizzata Hello esegue uno script in ogni istanza di macchina virtuale nel set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="dbd08-128">hello Custom Script extension runs a script on each virtual machine instance in hello scale set.</span></span> <span data-ttu-id="dbd08-129">Un file di configurazione o una variabile indica quali file sono macchina virtuale toohello scaricato, quindi viene eseguito il comando.</span><span class="sxs-lookup"><span data-stu-id="dbd08-129">A config file or variable indicates which files are downloaded toohello virtual machine, and then what command runs.</span></span> <span data-ttu-id="dbd08-130">È possibile utilizzare ad esempio un programma di installazione questo toorun, uno script, un file batch, qualsiasi file eseguibile.</span><span class="sxs-lookup"><span data-stu-id="dbd08-130">You could use this toorun an installer, a script, a batch file, any executable for example.</span></span>

<span data-ttu-id="dbd08-131">PowerShell utilizza una tabella hash per le impostazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="dbd08-131">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="dbd08-132">In questo esempio Configura toorun di estensione script personalizzata hello uno script di PowerShell che consente di installare IIS.</span><span class="sxs-lookup"><span data-stu-id="dbd08-132">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="dbd08-133">Hello utilizzare `-ProtectedSetting` passare per tutte le impostazioni che potrebbero contenere informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="dbd08-133">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

---------


<span data-ttu-id="dbd08-134">CLI di Azure Usa un file json per le impostazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="dbd08-134">Azure CLI uses a json file for hello settings.</span></span> <span data-ttu-id="dbd08-135">In questo esempio Configura toorun di estensione script personalizzata hello uno script di PowerShell che consente di installare IIS.</span><span class="sxs-lookup"><span data-stu-id="dbd08-135">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span> <span data-ttu-id="dbd08-136">Salvare i seguenti file json come hello _Settings_.</span><span class="sxs-lookup"><span data-stu-id="dbd08-136">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

<span data-ttu-id="dbd08-137">Quindi, eseguire questo comando dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="dbd08-137">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="dbd08-138">Hello utilizzare `--protected-settings` passare per tutte le impostazioni che potrebbero contenere informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="dbd08-138">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="powershell-dsc"></a><span data-ttu-id="dbd08-139">PowerShell DSC</span><span class="sxs-lookup"><span data-stu-id="dbd08-139">PowerShell DSC</span></span>

<span data-ttu-id="dbd08-140">È possibile utilizzare le istanze di macchina virtuale di PowerShell DSC toocustomize hello scala set.</span><span class="sxs-lookup"><span data-stu-id="dbd08-140">You can use PowerShell DSC toocustomize hello scale set vm instances.</span></span> <span data-ttu-id="dbd08-141">Hello **DSC** estensione pubblicato da **PowerShell** distribuisce ed esegue configurazione DSC hello fornito in ogni istanza di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dbd08-141">hello **DSC** extension published by **Microsoft.Powershell** deploys and runs hello provided DSC configuration on each virtual machine instance.</span></span> <span data-ttu-id="dbd08-142">Estensione hello indica a un file di configurazione o una variabile in cui *zip* pacchetto è e quali _funzione di script_ toorun combinazione.</span><span class="sxs-lookup"><span data-stu-id="dbd08-142">A config file or variable tells hello extension where *.zip* package is, and which _script-function_ combination toorun.</span></span>

<span data-ttu-id="dbd08-143">PowerShell utilizza una tabella hash per le impostazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="dbd08-143">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="dbd08-144">Questo esempio distribuisce un pacchetto DSC che consente di installare IIS.</span><span class="sxs-lookup"><span data-stu-id="dbd08-144">This example deploys a DSC package that installs IIS.</span></span>

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

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="dbd08-145">Hello utilizzare `-ProtectedSetting` passare per tutte le impostazioni che potrebbero contenere informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="dbd08-145">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

-----------

<span data-ttu-id="dbd08-146">CLI di Azure Usa un formato json per le impostazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="dbd08-146">Azure CLI uses a json for hello settings.</span></span> <span data-ttu-id="dbd08-147">Questo esempio distribuisce un pacchetto DSC che consente di installare IIS.</span><span class="sxs-lookup"><span data-stu-id="dbd08-147">This example deploys a DSC package that installs IIS.</span></span> <span data-ttu-id="dbd08-148">Salvare i seguenti file json come hello _Settings_.</span><span class="sxs-lookup"><span data-stu-id="dbd08-148">Save hello following json file as _settings.json_.</span></span>

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

<span data-ttu-id="dbd08-149">Quindi, eseguire questo comando dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="dbd08-149">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="dbd08-150">Hello utilizzare `--protected-settings` passare per tutte le impostazioni che potrebbero contenere informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="dbd08-150">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="linux"></a><span data-ttu-id="dbd08-151">Linux</span><span class="sxs-lookup"><span data-stu-id="dbd08-151">Linux</span></span>

<span data-ttu-id="dbd08-152">Linux è possibile utilizzare entrambi hello **v 2.0 Custom Script** estensione oppure utilizzare **cloud init** durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="dbd08-152">Linux can use either hello **Custom Script v2.0** extension or use **cloud-init** during creation.</span></span>

<span data-ttu-id="dbd08-153">Script personalizzato è un'estensione semplice che scarica istanze di macchine virtuali di file toohello ed esegue un comando.</span><span class="sxs-lookup"><span data-stu-id="dbd08-153">Custom script is a simple extension that downloads files toohello virtual machine instances, and runs a command.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="dbd08-154">Custom Script</span><span class="sxs-lookup"><span data-stu-id="dbd08-154">Custom Script</span></span>

<span data-ttu-id="dbd08-155">Salvare i seguenti file json come hello _Settings_.</span><span class="sxs-lookup"><span data-stu-id="dbd08-155">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

<span data-ttu-id="dbd08-156">Utilizzare hello Azure CLI tooadd tooan questa estensione set di scalabilità della macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="dbd08-156">Use hello Azure CLI tooadd this extension tooan existing virtual machine scale set.</span></span> <span data-ttu-id="dbd08-157">Ogni macchina virtuale in scala di hello impostate automaticamente estensione hello viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="dbd08-157">Each virtual machine in hello scale set automatically runs hello extension.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="dbd08-158">Hello utilizzare `--protected-settings` passare per tutte le impostazioni che potrebbero contenere informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="dbd08-158">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

#### <a name="cloud-init"></a><span data-ttu-id="dbd08-159">cloud-init</span><span class="sxs-lookup"><span data-stu-id="dbd08-159">Cloud-Init</span></span>

<span data-ttu-id="dbd08-160">Cloud-inizializzazione viene utilizzato quando viene creato il set di scalabilità di hello.</span><span class="sxs-lookup"><span data-stu-id="dbd08-160">Cloud-Init is used when hello scale set is created.</span></span> <span data-ttu-id="dbd08-161">Innanzitutto, creare un file locale denominato _cloud init.txt_ e aggiungere il tooit di configurazione.</span><span class="sxs-lookup"><span data-stu-id="dbd08-161">First, create a local file named _cloud-init.txt_ and add your configuration tooit.</span></span> <span data-ttu-id="dbd08-162">Ad esempio, vedere [questo gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span><span class="sxs-lookup"><span data-stu-id="dbd08-162">For example, see [this gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span></span>

<span data-ttu-id="dbd08-163">Imposta hello utilizzare Azure CLI toocreate una scala.</span><span class="sxs-lookup"><span data-stu-id="dbd08-163">Use hello Azure CLI toocreate a scale set.</span></span> <span data-ttu-id="dbd08-164">Hello `--custom-data` campo accetta il nome file hello di uno script di inizializzazione di cloud.</span><span class="sxs-lookup"><span data-stu-id="dbd08-164">hello `--custom-data` field accepts hello file name of a cloud-init script.</span></span>

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

## <a name="how-do-i-manage-application-updates"></a><span data-ttu-id="dbd08-165">Gestione degli aggiornamenti dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="dbd08-165">How do I manage application updates?</span></span>

<span data-ttu-id="dbd08-166">Se è stata distribuita l'applicazione tramite un'estensione, è possibile modificare la definizione di estensione hello in qualche modo.</span><span class="sxs-lookup"><span data-stu-id="dbd08-166">If you deployed your application through an extension, alter hello extension definition in some way.</span></span> <span data-ttu-id="dbd08-167">Questa modifica impedisce a istanze di macchine virtuali tooall hello estensione toobe ridistribuita.</span><span class="sxs-lookup"><span data-stu-id="dbd08-167">This change causes hello extension toobe redeployed tooall virtual machine instances.</span></span> <span data-ttu-id="dbd08-168">Un elemento **deve** modificato sull'estensione hello, ad esempio la ridenominazione di un file di cui viene fatto riferimento, in caso contrario, Azure fa non vedere che hello estensione è stata modificata.</span><span class="sxs-lookup"><span data-stu-id="dbd08-168">Something **must** be changed about hello extension, such as renaming a referenced file, otherwise, Azure does not see that hello extension has changed.</span></span>

<span data-ttu-id="dbd08-169">Se si baked applicazione hello nella propria immagine del sistema operativo, è possibile utilizzare una pipeline di distribuzione automatica degli aggiornamenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dbd08-169">If you baked hello application into your own operating system image, use an automated deployment pipeline for application updates.</span></span> <span data-ttu-id="dbd08-170">Progettare il toofacilitate architettura rapido la sostituzione di una scala di gestione temporanea impostata nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="dbd08-170">Design your architecture toofacilitate rapid swapping of a staged scale set into production.</span></span> <span data-ttu-id="dbd08-171">Un buon esempio di questo approccio è hello [lavoro driver Azure Spinnaker](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span><span class="sxs-lookup"><span data-stu-id="dbd08-171">A good example of this approach is hello [Azure Spinnaker driver work](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span></span>

<span data-ttu-id="dbd08-172">[Chi](https://www.packer.io/) e [Terraform](https://www.terraform.io/) supporto Azure Resource Manager, pertanto è possibile anche definire le immagini "come"codice e compilarle in Azure, quindi utilizzare hello disco rigido virtuale nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="dbd08-172">[Packer](https://www.packer.io/) and [Terraform](https://www.terraform.io/) support Azure Resource Manager, so you can also define your images "as code" and build them in Azure, then use hello VHD in your scale set.</span></span> <span data-ttu-id="dbd08-173">Tuttavia, tale approccio diventerebbe problematico per le immagini Marketplace, in cui gli script personalizzati/le estensioni acquistano importanza in quanto i bit non vengono modificati direttamente da Marketplace.</span><span class="sxs-lookup"><span data-stu-id="dbd08-173">However, doing so would become problematic for marketplace images, where extensions/custom scripts become more important since you don’t directly manipulate bits from marketplace.</span></span>

## <a name="what-happens-when-a-scale-set-scales-out"></a><span data-ttu-id="dbd08-174">Cosa accade in caso di aumento della capacità di un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="dbd08-174">What happens when a scale set scales out?</span></span>
<span data-ttu-id="dbd08-175">Quando si aggiunge uno o più set di scalabilità di tooa macchine virtuali, un'applicazione hello viene installata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="dbd08-175">When you add one or more virtual machines tooa scale set, hello application is automatically installed.</span></span> <span data-ttu-id="dbd08-176">Per esempio se il set di scalabilità hello include le estensioni definite, eseguono in una nuova macchina virtuale ogni volta che viene creato.</span><span class="sxs-lookup"><span data-stu-id="dbd08-176">For example if hello scale set has extensions defined, they run on a new virtual machine each time it is created.</span></span> <span data-ttu-id="dbd08-177">Se il set di scalabilità di hello è basato su un'immagine personalizzata, qualsiasi nuova macchina virtuale è una copia dell'immagine di hello origine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="dbd08-177">If hello scale set is based on a custom image, any new virtual machine is a copy of hello source custom image.</span></span> <span data-ttu-id="dbd08-178">Se le macchine virtuali di set di scalabilità di hello host contenitore, avere contenitori hello tooload codice di avvio in un'estensione Script personalizzata.</span><span class="sxs-lookup"><span data-stu-id="dbd08-178">If hello scale set virtual machines are container hosts, then you might have startup code tooload hello containers in a Custom Script Extension.</span></span> <span data-ttu-id="dbd08-179">In alternativa, un'estensione potrebbe installare un agente che esegue la registrazione con un agente di orchestrazione del cluster, ad esempio il servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="dbd08-179">Or, an extension might install an agent that registers with a cluster orchestrator, such as Azure Container Service.</span></span>


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a><span data-ttu-id="dbd08-180">Come distribuire un aggiornamento del sistema operativo nei domini di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="dbd08-180">How do you roll out an OS update across update domains?</span></span>
<span data-ttu-id="dbd08-181">Si supponga di che voler tooupdate l'immagine del sistema operativo mantenendo scalabilità della macchina virtuale hello impostata in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="dbd08-181">Suppose you want tooupdate your OS image while keeping hello virtual machine scale set running.</span></span> <span data-ttu-id="dbd08-182">PowerShell e hello CLI di Azure è possibile aggiornare le immagini di macchina virtuale hello, una macchina virtuale alla volta.</span><span class="sxs-lookup"><span data-stu-id="dbd08-182">PowerShell and hello Azure CLI can update hello virtual machine images, one virtual machine at a time.</span></span> <span data-ttu-id="dbd08-183">Hello [aggiornare un Set di scalabilità della macchina virtuale](./virtual-machine-scale-sets-upgrade-scale-set.md) articolo inoltre fornisce ulteriori informazioni su quali opzioni sono disponibili tooperform l'aggiornamento di un sistema operativo in un set di scalabilità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dbd08-183">hello [Upgrade a Virtual Machine Scale Set](./virtual-machine-scale-sets-upgrade-scale-set.md) article also provides further information on what options are available tooperform an operating system upgrade across a virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dbd08-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dbd08-184">Next steps</span></span>

* [<span data-ttu-id="dbd08-185">Utilizzare PowerShell toomanage il set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="dbd08-185">Use PowerShell toomanage your scale set.</span></span>](virtual-machine-scale-sets-windows-manage.md)
* [<span data-ttu-id="dbd08-186">Creare un modello del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="dbd08-186">Create a scale set template.</span></span>](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md


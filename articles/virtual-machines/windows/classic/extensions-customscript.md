---
title: estensione dello Script in una macchina virtuale Windows aaaCustom | Documenti Microsoft
description: "Automatizzare le attività di configurazione macchina virtuale di Azure tramite script di PowerShell toorun estensione Custom Script hello in una VM Windows remoto"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: ebb7340a-8f61-4d3c-a290-d7bf8de2d0bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: nepeters
ms.openlocfilehash: cf7bb895dd211f07fd010dc03b68cd77df1127b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows-using-hello-classic-deployment-model"></a><span data-ttu-id="752ce-103">Script di estensione per Windows personalizzata utilizzando il modello di distribuzione classica hello</span><span class="sxs-lookup"><span data-stu-id="752ce-103">Custom Script Extension for Windows using hello classic deployment model</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="752ce-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="752ce-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="752ce-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="752ce-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="752ce-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="752ce-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="752ce-107">Informazioni su come troppo[eseguire questi passaggi tramite il modello di gestione risorse di hello](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="752ce-107">Learn how too[perform these steps using hello Resource Manager model](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="752ce-108">Estensione dello Script personalizzata Hello Scarica ed esegue gli script in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="752ce-108">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="752ce-109">Questa estensione è utile per la configurazione post-distribuzione, l'installazione di software o qualsiasi altra attività di configurazione o gestione.</span><span class="sxs-lookup"><span data-stu-id="752ce-109">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="752ce-110">Gli script possono essere scaricati da GitHub o di archiviazione di Azure o forniti toohello portale di Azure in fase di esecuzione di estensione.</span><span class="sxs-lookup"><span data-stu-id="752ce-110">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="752ce-111">estensione Script personalizzata Hello si integra con i modelli di gestione risorse di Azure e può essere eseguito anche tramite hello Azure CLI, PowerShell, il portale di Azure o hello API REST di macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="752ce-111">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="752ce-112">Questo documento illustra in dettaglio come toouse hello estensione Script personalizzata utilizzando hello modulo Azure PowerShell, i modelli di gestione risorse di Azure e i dettagli di risoluzione dei problemi in sistemi Windows.</span><span class="sxs-lookup"><span data-stu-id="752ce-112">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="752ce-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="752ce-113">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="752ce-114">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="752ce-114">Operating System</span></span>

<span data-ttu-id="752ce-115">Estensione dello Script personalizzata Hello per Windows possono essere eseguite in Windows Server 2008 R2, 2012 e 2012 R2 2016 rilascia.</span><span class="sxs-lookup"><span data-stu-id="752ce-115">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="752ce-116">Percorso dello script</span><span class="sxs-lookup"><span data-stu-id="752ce-116">Script Location</span></span>

<span data-ttu-id="752ce-117">script di Hello deve toobe archiviati in archiviazione di Azure o qualsiasi altro percorso accessibile tramite un URL valido.</span><span class="sxs-lookup"><span data-stu-id="752ce-117">hello script needs toobe stored in Azure storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="752ce-118">Connettività Internet</span><span class="sxs-lookup"><span data-stu-id="752ce-118">Internet Connectivity</span></span>

<span data-ttu-id="752ce-119">Hello Custom Script di estensione per Windows richiede tale macchina virtuale di destinazione hello è connesso toohello internet.</span><span class="sxs-lookup"><span data-stu-id="752ce-119">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="752ce-120">Schema dell'estensione</span><span class="sxs-lookup"><span data-stu-id="752ce-120">Extension schema</span></span>

<span data-ttu-id="752ce-121">Hello JSON seguente viene illustrato lo schema di hello per hello estensione Script personalizzata.</span><span class="sxs-lookup"><span data-stu-id="752ce-121">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="752ce-122">estensione di Hello richiede un percorso di script (archiviazione di Azure o in altre posizioni di URL valido) e tooexecute un comando.</span><span class="sxs-lookup"><span data-stu-id="752ce-122">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="752ce-123">Se si utilizza l'archiviazione di Azure come origine script hello, una chiave account e nome dell'account di archiviazione di Azure è obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="752ce-123">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="752ce-124">Questi elementi devono essere considerati come dati sensibili e specificati nella configurazione di hello estensioni impostazione protetto.</span><span class="sxs-lookup"><span data-stu-id="752ce-124">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="752ce-125">Dati impostazione protette dell'estensione di macchina virtuale di Azure sono crittografati e decrittografati solo nella macchina virtuale di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="752ce-125">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

```json
{
    "name": "config-app",
    "type": "Microsoft.ClassicCompute/virtualMachines/extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-01",
    "properties": {
        "publisher": "Microsoft.Compute",
        "extension": "CustomScriptExtension",
        "version": "1.8",
        "parameters": {
            "public": {
                "fileUris": "[myScriptLocation]"
            },
            "private": {
                "commandToExecute": "[myExecutionString]"
            }
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="752ce-126">Valori delle proprietà</span><span class="sxs-lookup"><span data-stu-id="752ce-126">Property values</span></span>

| <span data-ttu-id="752ce-127">Nome</span><span class="sxs-lookup"><span data-stu-id="752ce-127">Name</span></span> | <span data-ttu-id="752ce-128">Valore/Esempio</span><span class="sxs-lookup"><span data-stu-id="752ce-128">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="752ce-129">apiVersion</span><span class="sxs-lookup"><span data-stu-id="752ce-129">apiVersion</span></span> | <span data-ttu-id="752ce-130">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="752ce-130">2015-06-15</span></span> |
| <span data-ttu-id="752ce-131">publisher</span><span class="sxs-lookup"><span data-stu-id="752ce-131">publisher</span></span> | <span data-ttu-id="752ce-132">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="752ce-132">Microsoft.Compute</span></span> |
| <span data-ttu-id="752ce-133">estensione</span><span class="sxs-lookup"><span data-stu-id="752ce-133">extension</span></span> | <span data-ttu-id="752ce-134">CustomScriptExtension</span><span class="sxs-lookup"><span data-stu-id="752ce-134">CustomScriptExtension</span></span> |
| <span data-ttu-id="752ce-135">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="752ce-135">typeHandlerVersion</span></span> | <span data-ttu-id="752ce-136">1.8</span><span class="sxs-lookup"><span data-stu-id="752ce-136">1.8</span></span> |
| <span data-ttu-id="752ce-137">fileUris (es.)</span><span class="sxs-lookup"><span data-stu-id="752ce-137">fileUris (e.g)</span></span> | <span data-ttu-id="752ce-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="752ce-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="752ce-139">commandToExecute (es.)</span><span class="sxs-lookup"><span data-stu-id="752ce-139">commandToExecute (e.g)</span></span> | <span data-ttu-id="752ce-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="752ce-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="752ce-141">Distribuzione del modello</span><span class="sxs-lookup"><span data-stu-id="752ce-141">Template deployment</span></span>

<span data-ttu-id="752ce-142">Le estensioni macchina virtuale di Azure possono essere distribuite con i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="752ce-142">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="752ce-143">schema JSON Hello descritta in dettaglio nella sezione precedente hello è utilizzabile in un hello toorun modello di gestione risorse di Azure estensione Script personalizzata durante la distribuzione di un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="752ce-143">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="752ce-144">Un modello di esempio che include l'estensione dello Script personalizzata è reperibile qui, hello [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="752ce-144">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="752ce-145">Distribuzione PowerShell</span><span class="sxs-lookup"><span data-stu-id="752ce-145">PowerShell deployment</span></span>

<span data-ttu-id="752ce-146">Hello `Set-AzureVMCustomScriptExtension` comando può essere utilizzato tooadd hello Custom Script estensione tooan macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="752ce-146">hello `Set-AzureVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="752ce-147">Per ulteriori informazioni, vedere [Set-AzureRmVMCustomScriptExtension](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="752ce-147">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="752ce-148">Risoluzione dei problemi e supporto</span><span class="sxs-lookup"><span data-stu-id="752ce-148">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="752ce-149">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="752ce-149">Troubleshoot</span></span>

<span data-ttu-id="752ce-150">Dati sullo stato di hello delle distribuzioni di estensione possono essere recuperati dal portale di Azure hello e, utilizzando il modulo di Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="752ce-150">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="752ce-151">stato di distribuzione toosee hello delle estensioni per una macchina virtuale specificata, eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="752ce-151">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="752ce-152">Esecuzione di estensione output ci toofiles connesso trovato nella seguente directory nella macchina virtuale di destinazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="752ce-152">Extension execution output us logged toofiles found in hello following directory on hello target virtual machine.</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="752ce-153">script Hello stesso viene scaricato nella seguente directory nella macchina virtuale di destinazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="752ce-153">hello script itself is downloaded into hello following directory on hello target virtual machine.</span></span>

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a><span data-ttu-id="752ce-154">Supporto</span><span class="sxs-lookup"><span data-stu-id="752ce-154">Support</span></span>

<span data-ttu-id="752ce-155">Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti hello [forum MSDN di Azure e di Overflow dello Stack](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="752ce-155">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="752ce-156">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="752ce-156">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="752ce-157">Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/en-us/support/options/) e scegliere supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="752ce-157">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="752ce-158">Per informazioni sull'utilizzo di supporto di Azure, leggere hello [supporto tecnico di Microsoft Azure domande frequenti su](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="752ce-158">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>

---
title: Estensione Script personalizzato per una macchina virtuale di Windows | Microsoft Docs
description: "Automatizzare le attività di configurazione della macchina virtuale di Azure utilizzando l'estensione dello Script personalizzato per eseguire gli script di PowerShell in una macchina virtuale di Windows remota"
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
ms.openlocfilehash: 986ab1025dc188cd7fa1cf8b131a9d4b859be8f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="custom-script-extension-for-windows-using-the-classic-deployment-model"></a><span data-ttu-id="3d244-103">Estensione script personalizzata per Windows usando il modello di distribuzione classico</span><span class="sxs-lookup"><span data-stu-id="3d244-103">Custom Script Extension for Windows using the classic deployment model</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="3d244-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3d244-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3d244-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="3d244-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="3d244-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="3d244-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="3d244-107">Informazioni su come [eseguire questa procedura con il modello di Resource Manager](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3d244-107">Learn how to [perform these steps using the Resource Manager model](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="3d244-108">L'estensione script personalizzata scarica ed esegue script sulle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="3d244-108">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="3d244-109">Questa estensione è utile per la configurazione post-distribuzione, l'installazione di software o qualsiasi altra attività di configurazione o gestione.</span><span class="sxs-lookup"><span data-stu-id="3d244-109">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="3d244-110">Gli script possono essere scaricati dall'archiviazione di Azure o da GitHub, oppure possono essere forniti al portale di Azure durante il runtime dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="3d244-110">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span></span> <span data-ttu-id="3d244-111">L'estensione script personalizzata è integrabile nei modelli di Azure Resource Manager e può essere eseguita anche tramite l'interfaccia della riga di comando di Azure, PowerShell, il portale di Azure o l'API REST di Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="3d244-111">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="3d244-112">Questo documento descrive come usare l'estensione di script personalizzata con il modulo Azure PowerShell e i modelli di Azure Resource Manager e inoltre illustra i passaggi per la risoluzione dei problemi nei sistemi Windows.</span><span class="sxs-lookup"><span data-stu-id="3d244-112">This document details how to use the Custom Script Extension using the Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d244-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3d244-113">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="3d244-114">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="3d244-114">Operating System</span></span>

<span data-ttu-id="3d244-115">L'estensione di script personalizzata per Windows può essere eseguita in Windows Server 2008 R2, 2012, 2012 R2 e 2016.</span><span class="sxs-lookup"><span data-stu-id="3d244-115">The Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="3d244-116">Percorso dello script</span><span class="sxs-lookup"><span data-stu-id="3d244-116">Script Location</span></span>

<span data-ttu-id="3d244-117">Lo script deve essere archiviato nell'archiviazione di Azure o in un altro percorso accessibile tramite un URL valido.</span><span class="sxs-lookup"><span data-stu-id="3d244-117">The script needs to be stored in Azure storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="3d244-118">Connettività Internet</span><span class="sxs-lookup"><span data-stu-id="3d244-118">Internet Connectivity</span></span>

<span data-ttu-id="3d244-119">Per distribuire l'estensione di script personalizzata per Windows, è necessario che la macchina virtuale di destinazione sia connessa a Internet.</span><span class="sxs-lookup"><span data-stu-id="3d244-119">The Custom Script Extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="3d244-120">Schema dell'estensione</span><span class="sxs-lookup"><span data-stu-id="3d244-120">Extension schema</span></span>

<span data-ttu-id="3d244-121">Il codice JSON seguente mostra lo schema dell'estensione di script personalizzata.</span><span class="sxs-lookup"><span data-stu-id="3d244-121">The following JSON shows the schema for the Custom Script Extension.</span></span> <span data-ttu-id="3d244-122">L'estensione richiede un percorso dello script (archiviazione di Azure o altro percorso con un URL valido) e un comando da eseguire.</span><span class="sxs-lookup"><span data-stu-id="3d244-122">The extension requires a script location (Azure Storage or other location with valid URL), and a command to execute.</span></span> <span data-ttu-id="3d244-123">Se si usa l'archiviazione di Azure come origine dello script, sono necessari un nome e una chiave di account.</span><span class="sxs-lookup"><span data-stu-id="3d244-123">If using Azure Storage as the script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="3d244-124">Questi elementi devono essere trattati come dati sensibili ed essere specificati nella configurazione protetta dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="3d244-124">These items should be treated as sensitive data and specified in the extensions protected setting configuration.</span></span> <span data-ttu-id="3d244-125">I dati della configurazione protetta dell'estensione macchina virtuale di Azure vengono crittografati, per essere poi decrittografati solo nella macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="3d244-125">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="3d244-126">Valori delle proprietà</span><span class="sxs-lookup"><span data-stu-id="3d244-126">Property values</span></span>

| <span data-ttu-id="3d244-127">Nome</span><span class="sxs-lookup"><span data-stu-id="3d244-127">Name</span></span> | <span data-ttu-id="3d244-128">Valore/Esempio</span><span class="sxs-lookup"><span data-stu-id="3d244-128">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="3d244-129">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3d244-129">apiVersion</span></span> | <span data-ttu-id="3d244-130">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="3d244-130">2015-06-15</span></span> |
| <span data-ttu-id="3d244-131">publisher</span><span class="sxs-lookup"><span data-stu-id="3d244-131">publisher</span></span> | <span data-ttu-id="3d244-132">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="3d244-132">Microsoft.Compute</span></span> |
| <span data-ttu-id="3d244-133">estensione</span><span class="sxs-lookup"><span data-stu-id="3d244-133">extension</span></span> | <span data-ttu-id="3d244-134">CustomScriptExtension</span><span class="sxs-lookup"><span data-stu-id="3d244-134">CustomScriptExtension</span></span> |
| <span data-ttu-id="3d244-135">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="3d244-135">typeHandlerVersion</span></span> | <span data-ttu-id="3d244-136">1.8</span><span class="sxs-lookup"><span data-stu-id="3d244-136">1.8</span></span> |
| <span data-ttu-id="3d244-137">fileUris (es.)</span><span class="sxs-lookup"><span data-stu-id="3d244-137">fileUris (e.g)</span></span> | <span data-ttu-id="3d244-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="3d244-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="3d244-139">commandToExecute (es.)</span><span class="sxs-lookup"><span data-stu-id="3d244-139">commandToExecute (e.g)</span></span> | <span data-ttu-id="3d244-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="3d244-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="3d244-141">Distribuzione del modello</span><span class="sxs-lookup"><span data-stu-id="3d244-141">Template deployment</span></span>

<span data-ttu-id="3d244-142">Le estensioni macchina virtuale di Azure possono essere distribuite con i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3d244-142">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="3d244-143">Lo schema JSON indicato nella sezione precedente può essere usato in un modello di Azure Resource Manager per eseguire l'estensione di script personalizzata durante la distribuzione di un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3d244-143">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="3d244-144">Un modello di esempio che include l'estensione script personalizzata è disponibile su [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="3d244-144">A sample template that includes the Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="3d244-145">Distribuzione PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d244-145">PowerShell deployment</span></span>

<span data-ttu-id="3d244-146">Il comando `Set-AzureVMCustomScriptExtension` consente di aggiungere l'estensione di script personalizzata a una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="3d244-146">The `Set-AzureVMCustomScriptExtension` command can be used to add the Custom Script extension to an existing virtual machine.</span></span> <span data-ttu-id="3d244-147">Per ulteriori informazioni, vedere [Set-AzureRmVMCustomScriptExtension](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="3d244-147">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="3d244-148">Risoluzione dei problemi e supporto</span><span class="sxs-lookup"><span data-stu-id="3d244-148">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="3d244-149">Risolvere problemi</span><span class="sxs-lookup"><span data-stu-id="3d244-149">Troubleshoot</span></span>

<span data-ttu-id="3d244-150">I dati sullo stato delle distribuzioni dell'estensione possono essere recuperati nel portale di Azure e tramite il modulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3d244-150">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="3d244-151">Per visualizzare lo stato di distribuzione delle estensioni per una determinata macchina virtuale, eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="3d244-151">To see the deployment state of extensions for a given VM, run the following command.</span></span>

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="3d244-152">L'output dell'esecuzione dell'estensione viene registrato nei file presenti nella directory seguente nella macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="3d244-152">Extension execution output us logged to files found in the following directory on the target virtual machine.</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="3d244-153">Lo script stesso viene scaricato nella directory seguente nella macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="3d244-153">The script itself is downloaded into the following directory on the target virtual machine.</span></span>

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a><span data-ttu-id="3d244-154">Supporto</span><span class="sxs-lookup"><span data-stu-id="3d244-154">Support</span></span>

<span data-ttu-id="3d244-155">Per ricevere assistenza in relazione a qualsiasi punto di questo articolo, contattare gli esperti di Azure nei [forum MSDN e Stack Overflow relativi ad Azure](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="3d244-155">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="3d244-156">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="3d244-156">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="3d244-157">Accedere al [sito del supporto di Azure](https://azure.microsoft.com/en-us/support/options/) e selezionare l'opzione desiderata per ottenere supporto.</span><span class="sxs-lookup"><span data-stu-id="3d244-157">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="3d244-158">Per informazioni sull'uso del supporto di Azure, leggere le [Domande frequenti sul supporto di Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="3d244-158">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
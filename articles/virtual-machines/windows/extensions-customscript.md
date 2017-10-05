---
title: Estensione script personalizzata di Azure per Windows | Microsoft Docs
description: "Automatizzare le attività di configurazione delle macchine virtuali Windows usando l'estensione script personalizzata"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/16/2017
ms.author: nepeters
ms.openlocfilehash: a6f417ea6575b81258998ae3b31c10e9df59b603
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="custom-script-extension-for-windows"></a><span data-ttu-id="69d23-103">Estensione Script personalizzato per Windows</span><span class="sxs-lookup"><span data-stu-id="69d23-103">Custom Script Extension for Windows</span></span>

<span data-ttu-id="69d23-104">L'estensione script personalizzata scarica ed esegue script sulle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="69d23-104">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="69d23-105">Questa estensione è utile per la configurazione post-distribuzione, l'installazione di software o qualsiasi altra attività di configurazione o gestione.</span><span class="sxs-lookup"><span data-stu-id="69d23-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="69d23-106">Gli script possono essere scaricati dall'archiviazione di Azure o da GitHub, oppure possono essere forniti al portale di Azure durante il runtime dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="69d23-106">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span></span> <span data-ttu-id="69d23-107">L'estensione script personalizzata è integrabile nei modelli di Azure Resource Manager e può essere eseguita anche tramite l'interfaccia della riga di comando di Azure, PowerShell, il portale di Azure o l'API REST di Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="69d23-107">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="69d23-108">Questo documento descrive come usare l'estensione di script personalizzata con il modulo Azure PowerShell e i modelli di Azure Resource Manager e inoltre illustra i passaggi per la risoluzione dei problemi nei sistemi Windows.</span><span class="sxs-lookup"><span data-stu-id="69d23-108">This document details how to use the Custom Script Extension using the Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69d23-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="69d23-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="69d23-110">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="69d23-110">Operating System</span></span>

<span data-ttu-id="69d23-111">L'estensione di script personalizzata per Windows può essere eseguita in Windows Server 2008 R2, 2012, 2012 R2 e 2016.</span><span class="sxs-lookup"><span data-stu-id="69d23-111">The Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="69d23-112">Percorso dello script</span><span class="sxs-lookup"><span data-stu-id="69d23-112">Script Location</span></span>

<span data-ttu-id="69d23-113">Lo script deve essere archiviato nell'archiviazione BLOB di Azure o in un altro percorso accessibile tramite un URL valido.</span><span class="sxs-lookup"><span data-stu-id="69d23-113">The script needs to be stored in Azure Blob storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="69d23-114">Connettività Internet</span><span class="sxs-lookup"><span data-stu-id="69d23-114">Internet Connectivity</span></span>

<span data-ttu-id="69d23-115">Per distribuire l'estensione di script personalizzata per Windows, è necessario che la macchina virtuale di destinazione sia connessa a Internet.</span><span class="sxs-lookup"><span data-stu-id="69d23-115">The Custom Script Extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="69d23-116">Schema dell'estensione</span><span class="sxs-lookup"><span data-stu-id="69d23-116">Extension schema</span></span>

<span data-ttu-id="69d23-117">Il codice JSON seguente mostra lo schema dell'estensione di script personalizzata.</span><span class="sxs-lookup"><span data-stu-id="69d23-117">The following JSON shows the schema for the Custom Script Extension.</span></span> <span data-ttu-id="69d23-118">L'estensione richiede un percorso dello script (archiviazione di Azure o altro percorso con un URL valido) e un comando da eseguire.</span><span class="sxs-lookup"><span data-stu-id="69d23-118">The extension requires a script location (Azure Storage or other location with valid URL), and a command to execute.</span></span> <span data-ttu-id="69d23-119">Se si usa l'archiviazione di Azure come origine dello script, sono necessari un nome e una chiave di account.</span><span class="sxs-lookup"><span data-stu-id="69d23-119">If using Azure Storage as the script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="69d23-120">Questi elementi devono essere trattati come dati sensibili ed essere specificati nella configurazione protetta dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="69d23-120">These items should be treated as sensitive data and specified in the extensions protected setting configuration.</span></span> <span data-ttu-id="69d23-121">I dati della configurazione protetta dell'estensione macchina virtuale di Azure vengono crittografati, per essere poi decrittografati solo nella macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="69d23-121">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
        "[variables('musicstoresqlName')]"
    ],
    "tags": {
        "displayName": "config-app"
    },
    "properties": {
        "publisher": "Microsoft.Compute",
        "type": "CustomScriptExtension",
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="69d23-122">Valori delle proprietà</span><span class="sxs-lookup"><span data-stu-id="69d23-122">Property values</span></span>

| <span data-ttu-id="69d23-123">Nome</span><span class="sxs-lookup"><span data-stu-id="69d23-123">Name</span></span> | <span data-ttu-id="69d23-124">Valore/Esempio</span><span class="sxs-lookup"><span data-stu-id="69d23-124">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="69d23-125">apiVersion</span><span class="sxs-lookup"><span data-stu-id="69d23-125">apiVersion</span></span> | <span data-ttu-id="69d23-126">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="69d23-126">2015-06-15</span></span> |
| <span data-ttu-id="69d23-127">publisher</span><span class="sxs-lookup"><span data-stu-id="69d23-127">publisher</span></span> | <span data-ttu-id="69d23-128">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="69d23-128">Microsoft.Compute</span></span> |
| <span data-ttu-id="69d23-129">type</span><span class="sxs-lookup"><span data-stu-id="69d23-129">type</span></span> | <span data-ttu-id="69d23-130">Estensioni</span><span class="sxs-lookup"><span data-stu-id="69d23-130">extensions</span></span> |
| <span data-ttu-id="69d23-131">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="69d23-131">typeHandlerVersion</span></span> | <span data-ttu-id="69d23-132">1.9</span><span class="sxs-lookup"><span data-stu-id="69d23-132">1.9</span></span> |
| <span data-ttu-id="69d23-133">fileUris (es.)</span><span class="sxs-lookup"><span data-stu-id="69d23-133">fileUris (e.g)</span></span> | <span data-ttu-id="69d23-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="69d23-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="69d23-135">commandToExecute (es.)</span><span class="sxs-lookup"><span data-stu-id="69d23-135">commandToExecute (e.g)</span></span> | <span data-ttu-id="69d23-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="69d23-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |
| <span data-ttu-id="69d23-137">storageAccountName (es.)</span><span class="sxs-lookup"><span data-stu-id="69d23-137">storageAccountName (e.g)</span></span> | <span data-ttu-id="69d23-138">examplestorageacct</span><span class="sxs-lookup"><span data-stu-id="69d23-138">examplestorageacct</span></span> |
| <span data-ttu-id="69d23-139">storageAccountKey (es.)</span><span class="sxs-lookup"><span data-stu-id="69d23-139">storageAccountKey (e.g)</span></span> | <span data-ttu-id="69d23-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span><span class="sxs-lookup"><span data-stu-id="69d23-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span></span> |

<span data-ttu-id="69d23-141">**Nota**: questi nomi di proprietà fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="69d23-141">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="69d23-142">Usare i nomi come sono riportati sopra per evitare problemi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="69d23-142">Use the names as seen above to avoid deployment issues.</span></span>

## <a name="template-deployment"></a><span data-ttu-id="69d23-143">Distribuzione del modello</span><span class="sxs-lookup"><span data-stu-id="69d23-143">Template deployment</span></span>

<span data-ttu-id="69d23-144">Le estensioni macchina virtuale di Azure possono essere distribuite con i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="69d23-144">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="69d23-145">Lo schema JSON indicato nella sezione precedente può essere usato in un modello di Azure Resource Manager per eseguire l'estensione di script personalizzata durante la distribuzione di un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="69d23-145">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="69d23-146">Un modello di esempio che include l'estensione script personalizzata è disponibile su [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="69d23-146">A sample template that includes the Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="69d23-147">Distribuzione PowerShell</span><span class="sxs-lookup"><span data-stu-id="69d23-147">PowerShell deployment</span></span>

<span data-ttu-id="69d23-148">Il comando `Set-AzureRmVMCustomScriptExtension` consente di aggiungere l'estensione di script personalizzata a una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="69d23-148">The `Set-AzureRmVMCustomScriptExtension` command can be used to add the Custom Script extension to an existing virtual machine.</span></span> <span data-ttu-id="69d23-149">Per ulteriori informazioni, vedere [Set-AzureRmVMCustomScriptExtension](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="69d23-149">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="69d23-150">Risoluzione dei problemi e supporto</span><span class="sxs-lookup"><span data-stu-id="69d23-150">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="69d23-151">Risolvere problemi</span><span class="sxs-lookup"><span data-stu-id="69d23-151">Troubleshoot</span></span>

<span data-ttu-id="69d23-152">I dati sullo stato delle distribuzioni dell'estensione possono essere recuperati nel portale di Azure e tramite il modulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="69d23-152">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="69d23-153">Per visualizzare lo stato di distribuzione delle estensioni per una determinata macchina virtuale, eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="69d23-153">To see the deployment state of extensions for a given VM, run the following command.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="69d23-154">L'output dell'esecuzione dell'estensione viene registrato nei file presenti nella directory seguente nella macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="69d23-154">Extension execution output is logged to files found under the following directory on the target virtual machine.</span></span>
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="69d23-155">I file specificati vengono scaricati nella directory seguente nella macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="69d23-155">The specified files are downloaded into the following directory on the target virtual machine.</span></span>
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
<span data-ttu-id="69d23-156">dove `<n>` è un numero intero decimale che può variare nelle diverse esecuzioni dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="69d23-156">where `<n>` is a decimal integer which may change between executions of the extension.</span></span>  <span data-ttu-id="69d23-157">Il valore `1.*` corrisponde al valore effettivo attuale `typeHandlerVersion` dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="69d23-157">The `1.*` value matches the actual, current `typeHandlerVersion` value of the extension.</span></span>  <span data-ttu-id="69d23-158">Ad esempio, la directory effettiva potrebbe essere `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span><span class="sxs-lookup"><span data-stu-id="69d23-158">For example, the actual directory could be `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span></span>  

<span data-ttu-id="69d23-159">Quando si esegue il comando `commandToExecute`, nell'estensione sarà impostata questa directory (ad esempio `...\Downloads\2`) come directory di lavoro attuale.</span><span class="sxs-lookup"><span data-stu-id="69d23-159">When executing the `commandToExecute` command, the extension will have set this directory (e.g., `...\Downloads\2`) as the current working directory.</span></span> <span data-ttu-id="69d23-160">In questo modo viene abilitato l'uso di percorsi relativi per individuare i file scaricati tramite la proprietà `fileURIs`.</span><span class="sxs-lookup"><span data-stu-id="69d23-160">This enables the use of relative paths to locate the files downloaded via the `fileURIs` property.</span></span> <span data-ttu-id="69d23-161">Nella tabella seguente sono riportati alcuni esempi.</span><span class="sxs-lookup"><span data-stu-id="69d23-161">See the table below for examples.</span></span>

<span data-ttu-id="69d23-162">Poiché il percorso di download assoluto può variare nel tempo, quando è possibile è preferibile optare per percorsi relativi di script/file nella stringa `commandToExecute`.</span><span class="sxs-lookup"><span data-stu-id="69d23-162">Since the absolute download path may vary over time, it is better to opt for relative script/file paths in the `commandToExecute` string, whenever possible.</span></span> <span data-ttu-id="69d23-163">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="69d23-163">For example:</span></span>
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

<span data-ttu-id="69d23-164">Le informazioni sul percorso dopo il primo segmento URI vengono mantenute per i file scaricati tramite l'elenco delle proprietà `fileUris`.</span><span class="sxs-lookup"><span data-stu-id="69d23-164">Path information after the first URI segment is retained for files downloaded via the `fileUris` property list.</span></span>  <span data-ttu-id="69d23-165">Come illustrato nella tabella riportata di seguito, per i file scaricati viene eseguito il mapping nelle sottodirectory di download per riflettere la struttura dei valori `fileUris`.</span><span class="sxs-lookup"><span data-stu-id="69d23-165">As shown in the table below, downloaded files are mapped into download subdirectories to reflect the structure of the `fileUris` values.</span></span>  

#### <a name="examples-of-downloaded-files"></a><span data-ttu-id="69d23-166">Esempi di file scaricati</span><span class="sxs-lookup"><span data-stu-id="69d23-166">Examples of Downloaded Files</span></span>

| <span data-ttu-id="69d23-167">URI in fileUris</span><span class="sxs-lookup"><span data-stu-id="69d23-167">URI in fileUris</span></span> | <span data-ttu-id="69d23-168">Percorso relativo scaricato</span><span class="sxs-lookup"><span data-stu-id="69d23-168">Relative downloaded location</span></span> | <span data-ttu-id="69d23-169">Percorso assoluto scaricato *</span><span class="sxs-lookup"><span data-stu-id="69d23-169">Absolute downloaded location *</span></span> |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

<span data-ttu-id="69d23-170">\* Come in precedenza, i percorsi assoluti delle directory cambieranno nella durata della macchina virtuale ma non all'interno di una singola esecuzione dell'estensione CustomScript.</span><span class="sxs-lookup"><span data-stu-id="69d23-170">\* As above, the absolute directory paths will change over the lifetime of the VM, but not within a single execution of the CustomScript extension.</span></span>

### <a name="support"></a><span data-ttu-id="69d23-171">Supporto</span><span class="sxs-lookup"><span data-stu-id="69d23-171">Support</span></span>

<span data-ttu-id="69d23-172">Per ricevere maggiore assistenza in qualsiasi punto di questo articolo, contattare gli esperti di Azure nei [forum di Azure su MSDN e Stack Overflow].(https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="69d23-172">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums] (https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="69d23-173">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="69d23-173">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="69d23-174">Accedere al [sito del supporto di Azure](https://azure.microsoft.com/en-us/support/options/) e selezionare l'opzione desiderata per ottenere supporto.</span><span class="sxs-lookup"><span data-stu-id="69d23-174">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="69d23-175">Per informazioni sull'uso del supporto di Azure, leggere le [Domande frequenti sul supporto di Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="69d23-175">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>

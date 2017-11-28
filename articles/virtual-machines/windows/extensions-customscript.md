---
title: aaaAzure Custom Script di estensione per Windows | Documenti Microsoft
description: "Automatizzare le attività di configurazione macchina virtuale di Windows con l'estensione Custom Script hello"
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
ms.openlocfilehash: 97e065242e9fed116ee20b074f4e302a0cd10585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows"></a><span data-ttu-id="1fb6f-103">Estensione Script personalizzato per Windows</span><span class="sxs-lookup"><span data-stu-id="1fb6f-103">Custom Script Extension for Windows</span></span>

<span data-ttu-id="1fb6f-104">Estensione dello Script personalizzata Hello Scarica ed esegue gli script in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="1fb6f-105">Questa estensione è utile per la configurazione post-distribuzione, l'installazione di software o qualsiasi altra attività di configurazione o gestione.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="1fb6f-106">Gli script possono essere scaricati da GitHub o di archiviazione di Azure o forniti toohello portale di Azure in fase di esecuzione di estensione.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-106">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="1fb6f-107">estensione Script personalizzata Hello si integra con i modelli di gestione risorse di Azure e può essere eseguito anche tramite hello Azure CLI, PowerShell, il portale di Azure o hello API REST di macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="1fb6f-108">Questo documento illustra in dettaglio come toouse hello estensione Script personalizzata utilizzando hello modulo Azure PowerShell, i modelli di gestione risorse di Azure e i dettagli di risoluzione dei problemi in sistemi Windows.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-108">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fb6f-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1fb6f-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="1fb6f-110">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="1fb6f-110">Operating System</span></span>

<span data-ttu-id="1fb6f-111">Estensione dello Script personalizzata Hello per Windows possono essere eseguite in Windows Server 2008 R2, 2012 e 2012 R2 2016 rilascia.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-111">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="1fb6f-112">Percorso dello script</span><span class="sxs-lookup"><span data-stu-id="1fb6f-112">Script Location</span></span>

<span data-ttu-id="1fb6f-113">script di Hello deve toobe archiviati in archiviazione Blob di Azure o qualsiasi altro percorso accessibile tramite un URL valido.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-113">hello script needs toobe stored in Azure Blob storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="1fb6f-114">Connettività Internet</span><span class="sxs-lookup"><span data-stu-id="1fb6f-114">Internet Connectivity</span></span>

<span data-ttu-id="1fb6f-115">Hello Custom Script di estensione per Windows richiede tale macchina virtuale di destinazione hello è connesso toohello internet.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-115">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="1fb6f-116">Schema dell'estensione</span><span class="sxs-lookup"><span data-stu-id="1fb6f-116">Extension schema</span></span>

<span data-ttu-id="1fb6f-117">Hello JSON seguente viene illustrato lo schema di hello per hello estensione Script personalizzata.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-117">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="1fb6f-118">estensione di Hello richiede un percorso di script (archiviazione di Azure o in altre posizioni di URL valido) e tooexecute un comando.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-118">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="1fb6f-119">Se si utilizza l'archiviazione di Azure come origine script hello, una chiave account e nome dell'account di archiviazione di Azure è obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-119">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="1fb6f-120">Questi elementi devono essere considerati come dati sensibili e specificati nella configurazione di hello estensioni impostazione protetto.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-120">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="1fb6f-121">Dati impostazione protette dell'estensione di macchina virtuale di Azure sono crittografati e decrittografati solo nella macchina virtuale di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-121">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="1fb6f-122">Valori delle proprietà</span><span class="sxs-lookup"><span data-stu-id="1fb6f-122">Property values</span></span>

| <span data-ttu-id="1fb6f-123">Nome</span><span class="sxs-lookup"><span data-stu-id="1fb6f-123">Name</span></span> | <span data-ttu-id="1fb6f-124">Valore/Esempio</span><span class="sxs-lookup"><span data-stu-id="1fb6f-124">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="1fb6f-125">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1fb6f-125">apiVersion</span></span> | <span data-ttu-id="1fb6f-126">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="1fb6f-126">2015-06-15</span></span> |
| <span data-ttu-id="1fb6f-127">publisher</span><span class="sxs-lookup"><span data-stu-id="1fb6f-127">publisher</span></span> | <span data-ttu-id="1fb6f-128">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="1fb6f-128">Microsoft.Compute</span></span> |
| <span data-ttu-id="1fb6f-129">type</span><span class="sxs-lookup"><span data-stu-id="1fb6f-129">type</span></span> | <span data-ttu-id="1fb6f-130">Estensioni</span><span class="sxs-lookup"><span data-stu-id="1fb6f-130">extensions</span></span> |
| <span data-ttu-id="1fb6f-131">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="1fb6f-131">typeHandlerVersion</span></span> | <span data-ttu-id="1fb6f-132">1.9</span><span class="sxs-lookup"><span data-stu-id="1fb6f-132">1.9</span></span> |
| <span data-ttu-id="1fb6f-133">fileUris (es.)</span><span class="sxs-lookup"><span data-stu-id="1fb6f-133">fileUris (e.g)</span></span> | <span data-ttu-id="1fb6f-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="1fb6f-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="1fb6f-135">commandToExecute (es.)</span><span class="sxs-lookup"><span data-stu-id="1fb6f-135">commandToExecute (e.g)</span></span> | <span data-ttu-id="1fb6f-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="1fb6f-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |
| <span data-ttu-id="1fb6f-137">storageAccountName (es.)</span><span class="sxs-lookup"><span data-stu-id="1fb6f-137">storageAccountName (e.g)</span></span> | <span data-ttu-id="1fb6f-138">examplestorageacct</span><span class="sxs-lookup"><span data-stu-id="1fb6f-138">examplestorageacct</span></span> |
| <span data-ttu-id="1fb6f-139">storageAccountKey (es.)</span><span class="sxs-lookup"><span data-stu-id="1fb6f-139">storageAccountKey (e.g)</span></span> | <span data-ttu-id="1fb6f-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span><span class="sxs-lookup"><span data-stu-id="1fb6f-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span></span> |

<span data-ttu-id="1fb6f-141">**Nota**: questi nomi di proprietà fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-141">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="1fb6f-142">Nell'esempio precedente tooavoid problemi di distribuzione, utilizzare nomi di hello.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-142">Use hello names as seen above tooavoid deployment issues.</span></span>

## <a name="template-deployment"></a><span data-ttu-id="1fb6f-143">Distribuzione del modello</span><span class="sxs-lookup"><span data-stu-id="1fb6f-143">Template deployment</span></span>

<span data-ttu-id="1fb6f-144">Le estensioni macchina virtuale di Azure possono essere distribuite con i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-144">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="1fb6f-145">schema JSON Hello descritta in dettaglio nella sezione precedente hello è utilizzabile in un hello toorun modello di gestione risorse di Azure estensione Script personalizzata durante la distribuzione di un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-145">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="1fb6f-146">Un modello di esempio che include l'estensione dello Script personalizzata è reperibile qui, hello [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="1fb6f-146">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="1fb6f-147">Distribuzione PowerShell</span><span class="sxs-lookup"><span data-stu-id="1fb6f-147">PowerShell deployment</span></span>

<span data-ttu-id="1fb6f-148">Hello `Set-AzureRmVMCustomScriptExtension` comando può essere utilizzato tooadd hello Custom Script estensione tooan macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-148">hello `Set-AzureRmVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="1fb6f-149">Per ulteriori informazioni, vedere [Set-AzureRmVMCustomScriptExtension](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="1fb6f-149">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="1fb6f-150">Risoluzione dei problemi e supporto</span><span class="sxs-lookup"><span data-stu-id="1fb6f-150">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="1fb6f-151">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="1fb6f-151">Troubleshoot</span></span>

<span data-ttu-id="1fb6f-152">Dati sullo stato di hello delle distribuzioni di estensione possono essere recuperati dal portale di Azure hello e, utilizzando il modulo di Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-152">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="1fb6f-153">stato di distribuzione toosee hello delle estensioni per una macchina virtuale specificata, eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-153">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="1fb6f-154">Esecuzione di estensione di output è toofiles registrati in hello seguenti directory nella macchina virtuale di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-154">Extension execution output is logged toofiles found under hello following directory on hello target virtual machine.</span></span>
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="1fb6f-155">Hello specificato i file vengono scaricati nella seguente directory nella macchina virtuale di destinazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-155">hello specified files are downloaded into hello following directory on hello target virtual machine.</span></span>
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
<span data-ttu-id="1fb6f-156">dove `<n>` è un intero decimale che può cambiare tra le esecuzioni di estensione hello.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-156">where `<n>` is a decimal integer which may change between executions of hello extension.</span></span>  <span data-ttu-id="1fb6f-157">Hello `1.*` valore corrisponde a corrente effettivo, hello `typeHandlerVersion` valore dell'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-157">hello `1.*` value matches hello actual, current `typeHandlerVersion` value of hello extension.</span></span>  <span data-ttu-id="1fb6f-158">Ad esempio, è possibile directory effettiva hello `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-158">For example, hello actual directory could be `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span></span>  

<span data-ttu-id="1fb6f-159">Quando si esegue hello `commandToExecute` comando estensione hello verrà installata questa directory (ad esempio, `...\Downloads\2`) come directory di lavoro corrente hello.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-159">When executing hello `commandToExecute` command, hello extension will have set this directory (e.g., `...\Downloads\2`) as hello current working directory.</span></span> <span data-ttu-id="1fb6f-160">Questo utilizzo hello consente di file di percorsi relativi toolocate hello scaricati tramite hello `fileURIs` proprietà.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-160">This enables hello use of relative paths toolocate hello files downloaded via hello `fileURIs` property.</span></span> <span data-ttu-id="1fb6f-161">Vedere la tabella hello seguente per gli esempi.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-161">See hello table below for examples.</span></span>

<span data-ttu-id="1fb6f-162">Poiché il percorso di download assoluto hello può variare nel tempo, è meglio tooopt per i percorsi relativi script/file hello `commandToExecute` stringa, laddove possibile.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-162">Since hello absolute download path may vary over time, it is better tooopt for relative script/file paths in hello `commandToExecute` string, whenever possible.</span></span> <span data-ttu-id="1fb6f-163">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1fb6f-163">For example:</span></span>
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

<span data-ttu-id="1fb6f-164">Informazioni sul percorso dopo il primo segmento di URI hello viene mantenuto per i file scaricati tramite hello `fileUris` elenco di proprietà.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-164">Path information after hello first URI segment is retained for files downloaded via hello `fileUris` property list.</span></span>  <span data-ttu-id="1fb6f-165">Come illustrato nella tabella hello riportata di seguito, vengono eseguito il mapping di file scaricati in download struttura hello tooreflect di sottodirectory di hello `fileUris` valori.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-165">As shown in hello table below, downloaded files are mapped into download subdirectories tooreflect hello structure of hello `fileUris` values.</span></span>  

#### <a name="examples-of-downloaded-files"></a><span data-ttu-id="1fb6f-166">Esempi di file scaricati</span><span class="sxs-lookup"><span data-stu-id="1fb6f-166">Examples of Downloaded Files</span></span>

| <span data-ttu-id="1fb6f-167">URI in fileUris</span><span class="sxs-lookup"><span data-stu-id="1fb6f-167">URI in fileUris</span></span> | <span data-ttu-id="1fb6f-168">Percorso relativo scaricato</span><span class="sxs-lookup"><span data-stu-id="1fb6f-168">Relative downloaded location</span></span> | <span data-ttu-id="1fb6f-169">Percorso assoluto scaricato *</span><span class="sxs-lookup"><span data-stu-id="1fb6f-169">Absolute downloaded location *</span></span> |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

<span data-ttu-id="1fb6f-170">\*Come in precedenza, i percorsi di directory assoluta hello verranno modificato nel corso della durata hello di hello VM, ma non all'interno di una singola esecuzione dell'estensione CustomScript hello.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-170">\* As above, hello absolute directory paths will change over hello lifetime of hello VM, but not within a single execution of hello CustomScript extension.</span></span>

### <a name="support"></a><span data-ttu-id="1fb6f-171">Supporto</span><span class="sxs-lookup"><span data-stu-id="1fb6f-171">Support</span></span>

<span data-ttu-id="1fb6f-172">Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti hello [forum MSDN di Azure e di Overflow dello Stack] (https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="1fb6f-172">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums] (https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="1fb6f-173">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-173">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="1fb6f-174">Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/en-us/support/options/) e scegliere supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="1fb6f-174">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="1fb6f-175">Per informazioni sull'utilizzo di supporto di Azure, leggere hello [supporto tecnico di Microsoft Azure domande frequenti su](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="1fb6f-175">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>

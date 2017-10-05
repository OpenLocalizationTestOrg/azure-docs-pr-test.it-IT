---
title: Eseguire script personalizzati nelle macchine virtuali Linux | Microsoft Docs
description: "Automatizzare le attività di configurazione delle macchine virtuali Linux usando l'estensione script personalizzata"
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 1dde64aac72c11ccfccf4fdb676279692befaadd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-custom-script-extension-with-linux-virtual-machines"></a><span data-ttu-id="b9caa-103">Uso dell'estensione script personalizzata di Azure con macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="b9caa-103">Using the Azure Custom Script Extension with Linux Virtual Machines</span></span>
<span data-ttu-id="b9caa-104">L'estensione script personalizzata scarica ed esegue script sulle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9caa-104">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="b9caa-105">Questa estensione è utile per la configurazione post-distribuzione, l'installazione di software o qualsiasi altra attività di configurazione o gestione.</span><span class="sxs-lookup"><span data-stu-id="b9caa-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="b9caa-106">Gli script possono essere scaricati dall'archiviazione di Azure, o da un altro percorso Internet accessibile, oppure possono essere forniti al runtime dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="b9caa-106">Scripts can be downloaded from Azure storage or other accessible internet location, or provided to the extension run time.</span></span> <span data-ttu-id="b9caa-107">L'estensione script personalizzata è integrabile nei modelli di Azure Resource Manager e può essere eseguita anche tramite l'interfaccia della riga di comando di Azure, PowerShell, il portale di Azure o l'API REST di Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9caa-107">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="b9caa-108">Questo documento descrive come usare l'estensione script personalizzata dall'interfaccia della riga di comando di Azure, e da un modello di Azure Resource Manager, e inoltre illustra i passaggi per la risoluzione dei problemi nei sistemi Linux.</span><span class="sxs-lookup"><span data-stu-id="b9caa-108">This document details how to use the Custom Script Extension from the Azure CLI, and an Azure Resource Manager template, and also details troubleshooting steps on Linux systems.</span></span>

## <a name="extension-configuration"></a><span data-ttu-id="b9caa-109">Configurazione dell'estensione</span><span class="sxs-lookup"><span data-stu-id="b9caa-109">Extension Configuration</span></span>
<span data-ttu-id="b9caa-110">La configurazione dell'estensione script personalizzata specifica informazioni come il percorso dello script e il comando da eseguire.</span><span class="sxs-lookup"><span data-stu-id="b9caa-110">The Custom Script Extension configuration specifies things like script location and the command to be run.</span></span> <span data-ttu-id="b9caa-111">Questa configurazione può essere archiviata nei file di configurazione, specificata sulla riga di comando o definita in un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b9caa-111">This configuration can be stored in configuration files, specified on the command line, or in an Azure Resource Manager template.</span></span> <span data-ttu-id="b9caa-112">I dati sensibili possono essere archiviati in una configurazione protetta, che verrà crittografata e decrittografata solo all'interno della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b9caa-112">Sensitive data can be stored in a protected configuration, which is encrypted and only decrypted inside the virtual machine.</span></span> <span data-ttu-id="b9caa-113">La configurazione protetta è utile quando il comando di esecuzione include segreti, ad esempio una password.</span><span class="sxs-lookup"><span data-stu-id="b9caa-113">The protected configuration is useful when the execution command includes secrets such as a password.</span></span>

### <a name="public-configuration"></a><span data-ttu-id="b9caa-114">Configurazione pubblica</span><span class="sxs-lookup"><span data-stu-id="b9caa-114">Public Configuration</span></span>
<span data-ttu-id="b9caa-115">Schema:</span><span class="sxs-lookup"><span data-stu-id="b9caa-115">Schema:</span></span>

<span data-ttu-id="b9caa-116">**Nota**: questi nomi di proprietà fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="b9caa-116">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="b9caa-117">Usare i nomi come sono riportati sotto per evitare problemi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b9caa-117">Use the names as seen below to avoid deployment issues.</span></span>

* <span data-ttu-id="b9caa-118">**commandToExecute**: (obbligatorio, stringa) script del punto di ingresso da eseguire.</span><span class="sxs-lookup"><span data-stu-id="b9caa-118">**commandToExecute**: (required, string) the entry point script to execute</span></span>
* <span data-ttu-id="b9caa-119">**fileUris**: (facoltativo, matrice di stringhe) URL relativi ai file da scaricare.</span><span class="sxs-lookup"><span data-stu-id="b9caa-119">**fileUris**: (optional, string array) the URLs for files to be downloaded.</span></span>
* <span data-ttu-id="b9caa-120">**timestamp** : (facoltativo, intero) usare questo campo solo per attivare una nuova esecuzione dello script modificando il valore del campo.</span><span class="sxs-lookup"><span data-stu-id="b9caa-120">**timestamp** (optional, integer) use this field only to trigger a rerun of the script by changing value of this field.</span></span>

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a><span data-ttu-id="b9caa-121">Configurazione protetta</span><span class="sxs-lookup"><span data-stu-id="b9caa-121">Protected Configuration</span></span>
<span data-ttu-id="b9caa-122">Schema:</span><span class="sxs-lookup"><span data-stu-id="b9caa-122">Schema:</span></span>

<span data-ttu-id="b9caa-123">**Nota**: questi nomi di proprietà fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="b9caa-123">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="b9caa-124">Usare i nomi come sono riportati sotto per evitare problemi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b9caa-124">Use the names as seen below to avoid deployment issues.</span></span>

* <span data-ttu-id="b9caa-125">**commandToExecute**: (facoltativo, stringa) script del punto di ingresso da eseguire.</span><span class="sxs-lookup"><span data-stu-id="b9caa-125">**commandToExecute**: (optional, string) the entry point script to execute.</span></span> <span data-ttu-id="b9caa-126">Usare in alternativa questo campo se il comando contiene segreti, ad esempio password.</span><span class="sxs-lookup"><span data-stu-id="b9caa-126">Use this field instead if your command contains secrets such as passwords.</span></span>
* <span data-ttu-id="b9caa-127">**storageAccountName**: (facoltativo, stringa) nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b9caa-127">**storageAccountName**: (optional, string) the name of storage account.</span></span> <span data-ttu-id="b9caa-128">Se si specificano credenziali di archiviazione, tutti i valori di fileUris devono essere URL relativi a BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9caa-128">If you specify storage credentials, all fileUris must be URLs for Azure Blobs.</span></span>
* <span data-ttu-id="b9caa-129">**storageAccountKey**: (facoltativo, stringa) chiave di accesso dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b9caa-129">**storageAccountKey**: (optional, string) the access key of storage account.</span></span>

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a><span data-ttu-id="b9caa-130">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b9caa-130">Azure CLI</span></span>
<span data-ttu-id="b9caa-131">Quando si usa l'interfaccia della riga di comando di Azure per eseguire l'estensione script personalizzata, creare uno o più file di configurazione contenenti almeno il relativo URI e il comando di esecuzione dello script.</span><span class="sxs-lookup"><span data-stu-id="b9caa-131">When using the Azure CLI to run the Custom Script Extension, create a configuration file or files containing at minimum the file uri, and the script execution command.</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="b9caa-132">Le impostazioni possono essere specificate facoltativamente nel comando come una stringa in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="b9caa-132">Optionally the settings can be specified in the command as a JSON formatted string.</span></span> <span data-ttu-id="b9caa-133">Ciò consente di specificare la configurazione durante l'esecuzione e senza un file di configurazione separato.</span><span class="sxs-lookup"><span data-stu-id="b9caa-133">This allows the configuration to be specified during execution and without a separate configuration file.</span></span>

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a><span data-ttu-id="b9caa-134">Esempi di interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b9caa-134">Azure CLI Examples</span></span>

<span data-ttu-id="b9caa-135">**Esempio 1** : configurazione pubblica con file di script.</span><span class="sxs-lookup"><span data-stu-id="b9caa-135">**Example 1** - Public configuration with script file.</span></span>

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

<span data-ttu-id="b9caa-136">Comando dell'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="b9caa-136">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="b9caa-137">**Esempio 2** : configurazione pubblica senza file di script.</span><span class="sxs-lookup"><span data-stu-id="b9caa-137">**Example 2** - Public configuration with no script file.</span></span>

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

<span data-ttu-id="b9caa-138">Comando dell'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="b9caa-138">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="b9caa-139">**Esempio 3** : vengono usati un file di configurazione pubblica per specificare l'URI del file di script e un file di configurazione protetta per specificare il comando da eseguire.</span><span class="sxs-lookup"><span data-stu-id="b9caa-139">**Example 3** - A public configuration file is used to specify the script file URI, and a protected configuration file is used to specify the command to be executed.</span></span>

<span data-ttu-id="b9caa-140">File di configurazione pubblica:</span><span class="sxs-lookup"><span data-stu-id="b9caa-140">Public configuration file:</span></span>

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

<span data-ttu-id="b9caa-141">File di configurazione protetta:</span><span class="sxs-lookup"><span data-stu-id="b9caa-141">Protected configuration file:</span></span>  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

<span data-ttu-id="b9caa-142">Comando dell'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="b9caa-142">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a><span data-ttu-id="b9caa-143">Modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b9caa-143">Resource Manager Template</span></span>
<span data-ttu-id="b9caa-144">L'estensione script personalizzata di Azure può essere eseguita durante la fase di distribuzione della macchina virtuale usando un modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b9caa-144">The Azure Custom Script Extension can be run at Virtual Machine deployment time using a Resource Manager template.</span></span> <span data-ttu-id="b9caa-145">A tale scopo, aggiungere una risorsa JSON formattata correttamente al modello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b9caa-145">To do so, add properly formatted JSON to the deployment template.</span></span>

### <a name="resource-manager-examples"></a><span data-ttu-id="b9caa-146">Esempi di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b9caa-146">Resource Manager Examples</span></span>
<span data-ttu-id="b9caa-147">**Esempio 1** : configurazione pubblica.</span><span class="sxs-lookup"><span data-stu-id="b9caa-147">**Example 1** - public configuration.</span></span>

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

<span data-ttu-id="b9caa-148">**Esempio 2** : comando di esecuzione nella configurazione protetta.</span><span class="sxs-lookup"><span data-stu-id="b9caa-148">**Example 2** - execution command in protected configuration.</span></span>

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

<span data-ttu-id="b9caa-149">Per un esempio completo, vedere la demo di .NET Core Music Store: [Demo di Music Store](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span><span class="sxs-lookup"><span data-stu-id="b9caa-149">See the .Net Core Music Store Demo for a complete example - [Music Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b9caa-150">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="b9caa-150">Troubleshooting</span></span>
<span data-ttu-id="b9caa-151">Quando viene eseguita l'estensione script personalizzata, lo script viene creato o scaricato in una directory simile all'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="b9caa-151">When the Custom Script Extension runs, the script is created or downloaded into a directory similar to the following example.</span></span> <span data-ttu-id="b9caa-152">Anche l'output del comando viene salvato in questa directory, nei file `stdout` e `stderr`.</span><span class="sxs-lookup"><span data-stu-id="b9caa-152">The command output is also saved into this directory in `stdout` and `stderr` file.</span></span>

```bash
/var/lib/waagent/custom-script/download/0/
```

<span data-ttu-id="b9caa-153">L'estensione script di Azure genera un log che è possibile trovare nella directory seguente.</span><span class="sxs-lookup"><span data-stu-id="b9caa-153">The Azure Script Extension produces a log, which can be found here.</span></span>

```bash
/var/log/azure/custom-script/handler.log
```

<span data-ttu-id="b9caa-154">Lo stato dell'esecuzione dell'estensione script personalizzata può essere recuperato anche con l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9caa-154">The execution state of the Custom Script Extension can also be retrieved with the Azure CLI.</span></span>

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

<span data-ttu-id="b9caa-155">L'output ha un aspetto simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="b9caa-155">The output looks like the following text:</span></span>

```azurecli
info:    Executing command vm extension get
+ Looking up the VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a><span data-ttu-id="b9caa-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b9caa-156">Next Steps</span></span>
<span data-ttu-id="b9caa-157">Per informazioni su altre estensioni script delle macchine virtuali, vedere [Panoramica sulle estensioni script di Azure per Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b9caa-157">For information on other VM Script Extensions, see [Azure Script Extension overview for Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


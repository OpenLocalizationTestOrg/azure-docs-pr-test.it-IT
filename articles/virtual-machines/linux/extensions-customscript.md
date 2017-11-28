---
title: gli script personalizzati aaaRun nelle macchine virtuali Linux in Azure | Documenti Microsoft
description: "Automatizzare le attività di configurazione Linux VM utilizzando l'estensione dello Script personalizzata hello"
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
ms.openlocfilehash: f2c273a5fbd4cd1695aea48fa4bd08e691511e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a><span data-ttu-id="a2fdb-103">Utilizzo di hello estensione Script personalizzata di Azure con le macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="a2fdb-103">Using hello Azure Custom Script Extension with Linux Virtual Machines</span></span>
<span data-ttu-id="a2fdb-104">Estensione dello Script personalizzata Hello Scarica ed esegue gli script in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="a2fdb-105">Questa estensione è utile per la configurazione post-distribuzione, l'installazione di software o qualsiasi altra attività di configurazione o gestione.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="a2fdb-106">Gli script possono essere scaricati dall'archiviazione di Azure o un altro percorso internet accessibile o forniti estensione toohello fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-106">Scripts can be downloaded from Azure storage or other accessible internet location, or provided toohello extension run time.</span></span> <span data-ttu-id="a2fdb-107">estensione Script personalizzata Hello si integra con i modelli di gestione risorse di Azure e può essere eseguito anche tramite hello Azure CLI, PowerShell, il portale di Azure o hello API REST di macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="a2fdb-108">Questo documento illustra come toouse hello estensione Script personalizzata da hello CLI di Azure e un modello di gestione risorse di Azure, nonché dettagli risoluzione dei problemi in sistemi Linux.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-108">This document details how toouse hello Custom Script Extension from hello Azure CLI, and an Azure Resource Manager template, and also details troubleshooting steps on Linux systems.</span></span>

## <a name="extension-configuration"></a><span data-ttu-id="a2fdb-109">Configurazione dell'estensione</span><span class="sxs-lookup"><span data-stu-id="a2fdb-109">Extension Configuration</span></span>
<span data-ttu-id="a2fdb-110">configurazione di estensione dello Script personalizzata Hello specifica come percorso dello script e hello toobe di comando eseguire.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-110">hello Custom Script Extension configuration specifies things like script location and hello command toobe run.</span></span> <span data-ttu-id="a2fdb-111">Questa configurazione può essere archiviata nei file di configurazione specificati nella riga di comando hello o in un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-111">This configuration can be stored in configuration files, specified on hello command line, or in an Azure Resource Manager template.</span></span> <span data-ttu-id="a2fdb-112">Dati sensibili possono essere archiviati in una configurazione protetta, che verrà crittografata e decrittografata solo macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-112">Sensitive data can be stored in a protected configuration, which is encrypted and only decrypted inside hello virtual machine.</span></span> <span data-ttu-id="a2fdb-113">la configurazione protetta Hello è utile quando il comando di esecuzione hello include segreti, ad esempio una password.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-113">hello protected configuration is useful when hello execution command includes secrets such as a password.</span></span>

### <a name="public-configuration"></a><span data-ttu-id="a2fdb-114">Configurazione pubblica</span><span class="sxs-lookup"><span data-stu-id="a2fdb-114">Public Configuration</span></span>
<span data-ttu-id="a2fdb-115">Schema:</span><span class="sxs-lookup"><span data-stu-id="a2fdb-115">Schema:</span></span>

<span data-ttu-id="a2fdb-116">**Nota**: questi nomi di proprietà fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-116">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="a2fdb-117">Utilizzare nomi di hello, come illustrato di seguito tooavoid problemi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-117">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="a2fdb-118">**commandToExecute**: (obbligatorio, string) hello tooexecute script punto di ingresso</span><span class="sxs-lookup"><span data-stu-id="a2fdb-118">**commandToExecute**: (required, string) hello entry point script tooexecute</span></span>
* <span data-ttu-id="a2fdb-119">**fileUris**: (facoltativa, matrice di stringhe) hello URL per il file toobe scaricato.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-119">**fileUris**: (optional, string array) hello URLs for files toobe downloaded.</span></span>
* <span data-ttu-id="a2fdb-120">**timestamp** (intero facoltativo) utilizzare questo tootrigger solo una riesecuzione dello script hello di campo tramite la modifica del valore di questo campo.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-120">**timestamp** (optional, integer) use this field only tootrigger a rerun of hello script by changing value of this field.</span></span>

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a><span data-ttu-id="a2fdb-121">Configurazione protetta</span><span class="sxs-lookup"><span data-stu-id="a2fdb-121">Protected Configuration</span></span>
<span data-ttu-id="a2fdb-122">Schema:</span><span class="sxs-lookup"><span data-stu-id="a2fdb-122">Schema:</span></span>

<span data-ttu-id="a2fdb-123">**Nota**: questi nomi di proprietà fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-123">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="a2fdb-124">Utilizzare nomi di hello, come illustrato di seguito tooavoid problemi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-124">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="a2fdb-125">**commandToExecute**: (facoltativa, string) hello tooexecute script punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-125">**commandToExecute**: (optional, string) hello entry point script tooexecute.</span></span> <span data-ttu-id="a2fdb-126">Usare in alternativa questo campo se il comando contiene segreti, ad esempio password.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-126">Use this field instead if your command contains secrets such as passwords.</span></span>
* <span data-ttu-id="a2fdb-127">**storageAccountName**: (facoltativa, string) nome hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-127">**storageAccountName**: (optional, string) hello name of storage account.</span></span> <span data-ttu-id="a2fdb-128">Se si specificano credenziali di archiviazione, tutti i valori di fileUris devono essere URL relativi a BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-128">If you specify storage credentials, all fileUris must be URLs for Azure Blobs.</span></span>
* <span data-ttu-id="a2fdb-129">**storageAccountKey**: (facoltativa, string) la chiave di accesso hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-129">**storageAccountKey**: (optional, string) hello access key of storage account.</span></span>

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a><span data-ttu-id="a2fdb-130">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a2fdb-130">Azure CLI</span></span>
<span data-ttu-id="a2fdb-131">Quando si utilizza hello toorun di hello Azure CLI estensione Script personalizzata, creare un file di configurazione o file contenenti uri di file minimo hello e comando di esecuzione di script hello.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-131">When using hello Azure CLI toorun hello Custom Script Extension, create a configuration file or files containing at minimum hello file uri, and hello script execution command.</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="a2fdb-132">Facoltativamente impostazioni hello possono essere specificate nel comando hello sotto forma di stringa in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-132">Optionally hello settings can be specified in hello command as a JSON formatted string.</span></span> <span data-ttu-id="a2fdb-133">In questo modo toobe configurazione hello specificato durante l'esecuzione e senza un file di configurazione separato.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-133">This allows hello configuration toobe specified during execution and without a separate configuration file.</span></span>

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a><span data-ttu-id="a2fdb-134">Esempi di interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a2fdb-134">Azure CLI Examples</span></span>

<span data-ttu-id="a2fdb-135">**Esempio 1** : configurazione pubblica con file di script.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-135">**Example 1** - Public configuration with script file.</span></span>

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

<span data-ttu-id="a2fdb-136">Comando dell'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="a2fdb-136">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="a2fdb-137">**Esempio 2** : configurazione pubblica senza file di script.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-137">**Example 2** - Public configuration with no script file.</span></span>

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

<span data-ttu-id="a2fdb-138">Comando dell'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="a2fdb-138">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="a2fdb-139">**Esempio 3** : un file di configurazione pubblico è l'URI di file di script hello toospecify utilizzato e un file di configurazione protetto è utilizzato toospecify hello comando toobe eseguita.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-139">**Example 3** - A public configuration file is used toospecify hello script file URI, and a protected configuration file is used toospecify hello command toobe executed.</span></span>

<span data-ttu-id="a2fdb-140">File di configurazione pubblica:</span><span class="sxs-lookup"><span data-stu-id="a2fdb-140">Public configuration file:</span></span>

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

<span data-ttu-id="a2fdb-141">File di configurazione protetta:</span><span class="sxs-lookup"><span data-stu-id="a2fdb-141">Protected configuration file:</span></span>  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

<span data-ttu-id="a2fdb-142">Comando dell'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="a2fdb-142">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a><span data-ttu-id="a2fdb-143">Modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a2fdb-143">Resource Manager Template</span></span>
<span data-ttu-id="a2fdb-144">è possibile eseguire l'estensione dello Script di Azure personalizzata Hello in fase di distribuzione di macchina virtuale utilizzando un modello di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-144">hello Azure Custom Script Extension can be run at Virtual Machine deployment time using a Resource Manager template.</span></span> <span data-ttu-id="a2fdb-145">toodo in tal caso, aggiungere modello di distribuzione toohello JSON formattato correttamente.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-145">toodo so, add properly formatted JSON toohello deployment template.</span></span>

### <a name="resource-manager-examples"></a><span data-ttu-id="a2fdb-146">Esempi di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a2fdb-146">Resource Manager Examples</span></span>
<span data-ttu-id="a2fdb-147">**Esempio 1** : configurazione pubblica.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-147">**Example 1** - public configuration.</span></span>

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

<span data-ttu-id="a2fdb-148">**Esempio 2** : comando di esecuzione nella configurazione protetta.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-148">**Example 2** - execution command in protected configuration.</span></span>

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

<span data-ttu-id="a2fdb-149">Vedere hello .net Core negozio Demo per un esempio completo - [musica Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span><span class="sxs-lookup"><span data-stu-id="a2fdb-149">See hello .Net Core Music Store Demo for a complete example - [Music Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a2fdb-150">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="a2fdb-150">Troubleshooting</span></span>
<span data-ttu-id="a2fdb-151">Quando viene eseguita l'estensione dello Script personalizzata hello, script hello viene creato o scaricati in un toohello simile directory esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-151">When hello Custom Script Extension runs, hello script is created or downloaded into a directory similar toohello following example.</span></span> <span data-ttu-id="a2fdb-152">output del comando Hello viene salvato anche in questa directory `stdout` e `stderr` file.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-152">hello command output is also saved into this directory in `stdout` and `stderr` file.</span></span>

```bash
/var/lib/waagent/custom-script/download/0/
```

<span data-ttu-id="a2fdb-153">Estensione dello Script di Azure Hello produce un log, che è disponibili qui.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-153">hello Azure Script Extension produces a log, which can be found here.</span></span>

```bash
/var/log/azure/custom-script/handler.log
```

<span data-ttu-id="a2fdb-154">Inoltre, è possibile recuperare lo stato di esecuzione di Hello di hello estensione Script personalizzata con hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2fdb-154">hello execution state of hello Custom Script Extension can also be retrieved with hello Azure CLI.</span></span>

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

<span data-ttu-id="a2fdb-155">output di Hello è simile hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="a2fdb-155">hello output looks like hello following text:</span></span>

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a><span data-ttu-id="a2fdb-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a2fdb-156">Next Steps</span></span>
<span data-ttu-id="a2fdb-157">Per informazioni su altre estensioni script delle macchine virtuali, vedere [Panoramica sulle estensioni script di Azure per Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a2fdb-157">For information on other VM Script Extensions, see [Azure Script Extension overview for Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


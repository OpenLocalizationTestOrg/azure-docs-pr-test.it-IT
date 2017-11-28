---
title: Gruppi di risorse di Azure che contiene le estensioni VM aaaExporting | Documenti Microsoft
description: Esportare modelli di Resource Manager che includono estensioni macchina virtuale.
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a><span data-ttu-id="f2dd8-103">Esportazione di gruppi di risorse contenenti estensioni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f2dd8-103">Exporting Resource Groups that contain VM extensions</span></span>

<span data-ttu-id="f2dd8-104">I gruppi di risorse di Azure possono essere esportati in un nuovo modello di Resource Manager ridistribuibile.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-104">Azure Resource Groups can be exported into a new Resource Manager template that can then be redeployed.</span></span> <span data-ttu-id="f2dd8-105">Hello processo di esportazione interpreta le risorse esistenti e crea un modello di gestione risorse che, quando distribuito comporta un gruppo di risorse simili.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-105">hello export process interprets existing resources, and creates a Resource Manager template that when deployed results in a similar Resource Group.</span></span> <span data-ttu-id="f2dd8-106">Quando si utilizza l'opzione di esportazione hello gruppo di risorse rispetto a un gruppo di risorse contenente le estensioni di macchina virtuale, diversi elementi necessità toobe considerato, ad esempio compatibilità dell'estensione e protetti delle impostazioni.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-106">When using hello Resource Group export option against a Resource Group containing Virtual Machine extensions, several items need toobe considered such as extension compatibility and protected settings.</span></span>

<span data-ttu-id="f2dd8-107">Questo documento illustra il funzionamento hello il processo di esportazione di gruppo di risorse relative estensioni di macchine virtuali, incluso un elenco di estensioni supportate e i dettagli sulla gestione di dati protetti.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-107">This document details how hello Resource Group export process works regarding virtual machine extensions, including a list of supported extensions, and details on handling secured data.</span></span>

## <a name="supported-virtual-machine-extensions"></a><span data-ttu-id="f2dd8-108">Estensioni macchina virtuale supportate</span><span class="sxs-lookup"><span data-stu-id="f2dd8-108">Supported Virtual Machine Extensions</span></span>

<span data-ttu-id="f2dd8-109">Sono disponibili molte estensioni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-109">Many Virtual Machine extensions are available.</span></span> <span data-ttu-id="f2dd8-110">Non tutte le estensioni possono essere esportate in un modello di gestione risorse utilizzo funzionalità "Script di automazione" hello.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-110">Not all extensions can be exported into a Resource Manager template using hello “Automation Script” feature.</span></span> <span data-ttu-id="f2dd8-111">Se un'estensione della macchina virtuale non è supportata, è necessario toobe manualmente inserito nel modello esportato hello.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-111">If a virtual machine extension is not supported, it needs toobe manually placed back into hello exported template.</span></span>

<span data-ttu-id="f2dd8-112">Hello estensioni seguenti possono essere esportate con funzionalità di script di automazione hello.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-112">hello following extensions can be exported with hello automation script feature.</span></span>

| <span data-ttu-id="f2dd8-113">Estensione</span><span class="sxs-lookup"><span data-stu-id="f2dd8-113">Extension</span></span> ||||
|---|---|---|---|
| <span data-ttu-id="f2dd8-114">Acronis Backup</span><span class="sxs-lookup"><span data-stu-id="f2dd8-114">Acronis Backup</span></span> | <span data-ttu-id="f2dd8-115">Datadog Windows Agent</span><span class="sxs-lookup"><span data-stu-id="f2dd8-115">Datadog Windows Agent</span></span> | <span data-ttu-id="f2dd8-116">OS Patching For Linux</span><span class="sxs-lookup"><span data-stu-id="f2dd8-116">OS Patching For Linux</span></span> | <span data-ttu-id="f2dd8-117">VM Snapshot Linux</span><span class="sxs-lookup"><span data-stu-id="f2dd8-117">VM Snapshot Linux</span></span>
| <span data-ttu-id="f2dd8-118">Acronis Backup Linux</span><span class="sxs-lookup"><span data-stu-id="f2dd8-118">Acronis Backup Linux</span></span> | <span data-ttu-id="f2dd8-119">Estensione Docker</span><span class="sxs-lookup"><span data-stu-id="f2dd8-119">Docker Extension</span></span> | <span data-ttu-id="f2dd8-120">Puppet Agent</span><span class="sxs-lookup"><span data-stu-id="f2dd8-120">Puppet Agent</span></span> |
| <span data-ttu-id="f2dd8-121">BGInfo</span><span class="sxs-lookup"><span data-stu-id="f2dd8-121">Bg Info</span></span> | <span data-ttu-id="f2dd8-122">DSC Extension</span><span class="sxs-lookup"><span data-stu-id="f2dd8-122">DSC Extension</span></span> | <span data-ttu-id="f2dd8-123">Site 24x7 Apm Insight</span><span class="sxs-lookup"><span data-stu-id="f2dd8-123">Site 24x7 Apm Insight</span></span> |
| <span data-ttu-id="f2dd8-124">BMC CTM Agent Linux</span><span class="sxs-lookup"><span data-stu-id="f2dd8-124">BMC CTM Agent Linux</span></span> | <span data-ttu-id="f2dd8-125">Dynatrace Linux</span><span class="sxs-lookup"><span data-stu-id="f2dd8-125">Dynatrace Linux</span></span> | <span data-ttu-id="f2dd8-126">Site 24x7 Linux Server</span><span class="sxs-lookup"><span data-stu-id="f2dd8-126">Site 24x7 Linux Server</span></span> |
| <span data-ttu-id="f2dd8-127">BMC CTM Agent Windows</span><span class="sxs-lookup"><span data-stu-id="f2dd8-127">BMC CTM Agent Windows</span></span> | <span data-ttu-id="f2dd8-128">Dynatrace Windows</span><span class="sxs-lookup"><span data-stu-id="f2dd8-128">Dynatrace Windows</span></span> | <span data-ttu-id="f2dd8-129">Site 24x7 Windows Server</span><span class="sxs-lookup"><span data-stu-id="f2dd8-129">Site 24x7 Windows Server</span></span> |
| <span data-ttu-id="f2dd8-130">Chef Client</span><span class="sxs-lookup"><span data-stu-id="f2dd8-130">Chef Client</span></span> | <span data-ttu-id="f2dd8-131">HPE Security Application Defender</span><span class="sxs-lookup"><span data-stu-id="f2dd8-131">HPE Security Application Defender</span></span> | <span data-ttu-id="f2dd8-132">Trend Micro DSA</span><span class="sxs-lookup"><span data-stu-id="f2dd8-132">Trend Micro DSA</span></span> |
| <span data-ttu-id="f2dd8-133">Custom Script</span><span class="sxs-lookup"><span data-stu-id="f2dd8-133">Custom Script</span></span> | <span data-ttu-id="f2dd8-134">IaaS Antimalware</span><span class="sxs-lookup"><span data-stu-id="f2dd8-134">IaaS Antimalware</span></span> | <span data-ttu-id="f2dd8-135">Trend Micro DSA Linux</span><span class="sxs-lookup"><span data-stu-id="f2dd8-135">Trend Micro DSA Linux</span></span> |
| <span data-ttu-id="f2dd8-136">Estensione di script personalizzati</span><span class="sxs-lookup"><span data-stu-id="f2dd8-136">Custom Script Extension</span></span> | <span data-ttu-id="f2dd8-137">IaaS Diagnostics</span><span class="sxs-lookup"><span data-stu-id="f2dd8-137">IaaS Diagnostics</span></span> | <span data-ttu-id="f2dd8-138">VM Access For Linux</span><span class="sxs-lookup"><span data-stu-id="f2dd8-138">VM Access For Linux</span></span> |
| <span data-ttu-id="f2dd8-139">Custom Script for Linux</span><span class="sxs-lookup"><span data-stu-id="f2dd8-139">Custom Script for Linux</span></span> | <span data-ttu-id="f2dd8-140">Linux Chef Client</span><span class="sxs-lookup"><span data-stu-id="f2dd8-140">Linux Chef Client</span></span> | <span data-ttu-id="f2dd8-141">VM Access For Linux</span><span class="sxs-lookup"><span data-stu-id="f2dd8-141">VM Access For Linux</span></span> |
| <span data-ttu-id="f2dd8-142">Datadog Linux Agent</span><span class="sxs-lookup"><span data-stu-id="f2dd8-142">Datadog Linux Agent</span></span> | <span data-ttu-id="f2dd8-143">Linux Diagnostic</span><span class="sxs-lookup"><span data-stu-id="f2dd8-143">Linux Diagnostic</span></span> | <span data-ttu-id="f2dd8-144">VM Snapshot</span><span class="sxs-lookup"><span data-stu-id="f2dd8-144">VM Snapshot</span></span> |

## <a name="export-hello-resource-group"></a><span data-ttu-id="f2dd8-145">Esportazione hello gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="f2dd8-145">Export hello Resource Group</span></span>

<span data-ttu-id="f2dd8-146">tooexport un gruppo di risorse in un modello riutilizzabile, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f2dd8-146">tooexport a Resource Group into a reusable template, complete hello following steps:</span></span>

1. <span data-ttu-id="f2dd8-147">Accedi toohello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f2dd8-147">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="f2dd8-148">Nel Menu Hub hello, fare clic su gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="f2dd8-148">On hello Hub Menu, click Resource Groups</span></span>
3. <span data-ttu-id="f2dd8-149">Selezionare il gruppo di risorse di hello destinazione dall'elenco di hello</span><span class="sxs-lookup"><span data-stu-id="f2dd8-149">Select hello target resource group from hello list</span></span>
4. <span data-ttu-id="f2dd8-150">Nel Pannello di hello gruppo di risorse, fare clic su Script di automazione</span><span class="sxs-lookup"><span data-stu-id="f2dd8-150">In hello Resource Group blade, click Automation Script</span></span>

![Esportazione del modello](./media/extensions-export-templates/template-export.png)

<span data-ttu-id="f2dd8-152">Hello script dall'automazione di Azure Resource Manager genera un modello di gestione delle risorse e un file di parametri diversi esempi di script di distribuzione, ad esempio PowerShell e CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-152">hello Azure Resource Manager automations script produces a Resource Manager template, a parameters file, and several sample deployment scripts such as PowerShell and Azure CLI.</span></span> <span data-ttu-id="f2dd8-153">A questo punto, può essere scaricato modello esportato hello mediante il pulsante download hello, aggiunto come una libreria di modelli toohello modello nuovo o ridistribuito utilizzando hello pulsante di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-153">At this point, hello exported template can be downloaded using hello download button, added as a new template toohello template library, or redeployed using hello deploy button.</span></span>

## <a name="configure-protected-settings"></a><span data-ttu-id="f2dd8-154">Configurare le impostazioni protette</span><span class="sxs-lookup"><span data-stu-id="f2dd8-154">Configure protected settings</span></span>

<span data-ttu-id="f2dd8-155">Molte estensioni macchina virtuale di Azure includono una configurazione di impostazioni protette, che crittografa i dati sensibili come credenziali e stringhe di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-155">Many Azure virtual machine extensions include a protected settings configuration, that encrypts sensitive data such as credentials and configuration strings.</span></span> <span data-ttu-id="f2dd8-156">Impostazioni protette non vengono esportate con script di automazione hello.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-156">Protected settings are not exported with hello automation script.</span></span> <span data-ttu-id="f2dd8-157">Se le impostazioni necessarie, protette necessario toobe reinserito hello esportata basati su modelli.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-157">If necessary, protected settings need toobe reinserted into hello exported templated.</span></span>

### <a name="step-1---remove-template-parameter"></a><span data-ttu-id="f2dd8-158">Passaggio 1 - Rimuovere il parametro del modello</span><span class="sxs-lookup"><span data-stu-id="f2dd8-158">Step 1 - Remove template parameter</span></span>

<span data-ttu-id="f2dd8-159">Creazione di hello al che gruppo di risorse viene esportato, un parametro singolo modello tooprovide toohello un valore esportato impostazioni protette.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-159">When hello Resource Group is exported, a single template parameter is created tooprovide a value toohello exported protected settings.</span></span> <span data-ttu-id="f2dd8-160">Questo parametro può essere rimosso.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-160">This parameter can be removed.</span></span> <span data-ttu-id="f2dd8-161">parametro hello tooremove, esaminare l'elenco di parametri hello ed eliminare il parametro hello che controlla l'esempio JSON toothis simile.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-161">tooremove hello parameter, look through hello parameter list and delete hello parameter that looks similar toothis JSON example.</span></span>

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a><span data-ttu-id="f2dd8-162">Passaggio 2 - Proteggere le proprietà delle impostazioni</span><span class="sxs-lookup"><span data-stu-id="f2dd8-162">Step 2 - Get protected settings properties</span></span>

<span data-ttu-id="f2dd8-163">Poiché ciascuna impostazione protetto ha un set di proprietà necessarie, un elenco di queste proprietà necessario toobe raccolte.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-163">Because each protected setting has a set of required properties, a list of these properties need toobe gathered.</span></span> <span data-ttu-id="f2dd8-164">È possibile trovare ogni parametro di configurazione delle impostazioni protette hello in hello [dello schema di gestione risorse di Azure su GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span><span class="sxs-lookup"><span data-stu-id="f2dd8-164">Each parameter of hello protected settings configuration can be found in hello [Azure Resource Manager schema on GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span></span> <span data-ttu-id="f2dd8-165">Questo schema include solo il set di parametri hello per le estensioni di hello elencati nella sezione Panoramica hello di questo documento.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-165">This schema only includes hello parameter sets for hello extensions listed in hello overview section of this document.</span></span> 

<span data-ttu-id="f2dd8-166">All'interno del repository di schema hello, cercare estensione hello desiderato, in questo esempio `IaaSDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-166">From within hello schema repository, search for hello desired extension, for this example `IaaSDiagnostics`.</span></span> <span data-ttu-id="f2dd8-167">Una volta hello estensioni `protectedSettings` oggetto è stato trovato, prendere nota di ogni parametro.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-167">Once hello extensions `protectedSettings` object has been located, take note of each parameter.</span></span> <span data-ttu-id="f2dd8-168">Nell'esempio hello di hello `IaasDiagnostic` estensione, hello richiedono parametri sono `storageAccountName`, `storageAccountKey`, e `storageAccountEndPoint`.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-168">In hello example of hello `IaasDiagnostic` extension, hello require parameters are `storageAccountName`, `storageAccountKey`, and `storageAccountEndPoint`.</span></span>

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-hello-protected-configuration"></a><span data-ttu-id="f2dd8-169">Passaggio 3: creare nuovamente configurazione hello protetto</span><span class="sxs-lookup"><span data-stu-id="f2dd8-169">Step 3 - Re-create hello protected configuration</span></span>

<span data-ttu-id="f2dd8-170">Il modello esportato di hello, cercare `protectedSettings` e sostituire hello esportata protetto l'impostazione dell'oggetto con una nuova istanza che include i parametri di estensione hello necessarie e un valore per ciascuna di esse.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-170">On hello exported template, search for `protectedSettings` and replace hello exported protected setting object with a new one that includes hello required extension parameters and a value for each one.</span></span>

<span data-ttu-id="f2dd8-171">Nell'esempio hello di hello `IaasDiagnostic` estensione, nuova configurazione di impostazione protetto hello avrà un aspetto analogo hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f2dd8-171">In hello example of hello `IaasDiagnostic` extension, hello new protected setting configuration would look like hello following example:</span></span>

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

<span data-ttu-id="f2dd8-172">risorse di estensione finale Hello sono simile toohello esempio JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="f2dd8-172">hello final extension resource looks similar toohello following JSON example:</span></span>

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

<span data-ttu-id="f2dd8-173">Se si utilizza i valori delle proprietà tooprovide modello parametri, questi devono toobe creato.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-173">If using template parameters tooprovide property values, these need toobe created.</span></span> <span data-ttu-id="f2dd8-174">Durante la creazione di parametri di modello per protetto impostazione dei valori, assicurarsi che hello toouse `SecureString` tipo di parametro in modo che i valori sensibili vengono protetti.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-174">When creating template parameters for protected setting values, make sure toouse hello `SecureString` parameter type so that sensitive values are secured.</span></span> <span data-ttu-id="f2dd8-175">Per altre informazioni sull'utilizzo dei parametri, vedere [Creazione di modelli di Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f2dd8-175">For more information on using parameters, see [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="f2dd8-176">Nell'esempio hello di hello `IaasDiagnostic` estensione, verrebbe creato nella sezione parametri hello del modello di gestione risorse di hello hello seguenti parametri.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-176">In hello example of hello `IaasDiagnostic` extension, hello following parameters would be created in hello parameters section of hello Resource Manager template.</span></span>

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

<span data-ttu-id="f2dd8-177">A questo punto, il modello di hello può essere distribuito utilizzando qualsiasi metodo di distribuzione del modello.</span><span class="sxs-lookup"><span data-stu-id="f2dd8-177">At this point, hello template can be deployed using any template deployment method.</span></span>

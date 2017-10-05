---
title: Esportazione di gruppi di risorse di Azure contenenti estensioni macchina virtuale | Microsoft Docs
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
ms.openlocfilehash: cc3c705f1c9123de75ced016a5b39eb1a86b0f73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a><span data-ttu-id="c2271-103">Esportazione di gruppi di risorse contenenti estensioni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c2271-103">Exporting Resource Groups that contain VM extensions</span></span>

<span data-ttu-id="c2271-104">I gruppi di risorse di Azure possono essere esportati in un nuovo modello di Resource Manager ridistribuibile.</span><span class="sxs-lookup"><span data-stu-id="c2271-104">Azure Resource Groups can be exported into a new Resource Manager template that can then be redeployed.</span></span> <span data-ttu-id="c2271-105">Il processo di esportazione interpreta le risorse esistenti e crea un modello di Resource Manager che quando viene distribuito diventa un gruppo di risorse simile.</span><span class="sxs-lookup"><span data-stu-id="c2271-105">The export process interprets existing resources, and creates a Resource Manager template that when deployed results in a similar Resource Group.</span></span> <span data-ttu-id="c2271-106">Quando si utilizza l'opzione di esportazione del gruppo di risorse su un gruppo di risorse contenente le estensioni macchina virtuale, diversi elementi dovranno essere considerati come compatibilità dell'estensione e impostazioni protette.</span><span class="sxs-lookup"><span data-stu-id="c2271-106">When using the Resource Group export option against a Resource Group containing Virtual Machine extensions, several items need to be considered such as extension compatibility and protected settings.</span></span>

<span data-ttu-id="c2271-107">Questo documento illustra il funzionamento del processo di esportazione del gruppo di risorse relativo alle estensioni macchina virtuale, inclusi un elenco di estensioni supportate e i dettagli sulla gestione di dati protetti.</span><span class="sxs-lookup"><span data-stu-id="c2271-107">This document details how the Resource Group export process works regarding virtual machine extensions, including a list of supported extensions, and details on handling secured data.</span></span>

## <a name="supported-virtual-machine-extensions"></a><span data-ttu-id="c2271-108">Estensioni macchina virtuale supportate</span><span class="sxs-lookup"><span data-stu-id="c2271-108">Supported Virtual Machine Extensions</span></span>

<span data-ttu-id="c2271-109">Sono disponibili molte estensioni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c2271-109">Many Virtual Machine extensions are available.</span></span> <span data-ttu-id="c2271-110">Non tutte le estensioni possono essere esportate in un modello di Resource Manager mediante la funzione "Script di automazione".</span><span class="sxs-lookup"><span data-stu-id="c2271-110">Not all extensions can be exported into a Resource Manager template using the “Automation Script” feature.</span></span> <span data-ttu-id="c2271-111">Se un'estensione macchina virtuale non è supportata, deve essere inserita manualmente nel modello esportato.</span><span class="sxs-lookup"><span data-stu-id="c2271-111">If a virtual machine extension is not supported, it needs to be manually placed back into the exported template.</span></span>

<span data-ttu-id="c2271-112">Le estensioni seguenti possono essere esportate con la funzionalità di script di automazione.</span><span class="sxs-lookup"><span data-stu-id="c2271-112">The following extensions can be exported with the automation script feature.</span></span>

| <span data-ttu-id="c2271-113">Estensione</span><span class="sxs-lookup"><span data-stu-id="c2271-113">Extension</span></span> ||||
|---|---|---|---|
| <span data-ttu-id="c2271-114">Acronis Backup</span><span class="sxs-lookup"><span data-stu-id="c2271-114">Acronis Backup</span></span> | <span data-ttu-id="c2271-115">Datadog Windows Agent</span><span class="sxs-lookup"><span data-stu-id="c2271-115">Datadog Windows Agent</span></span> | <span data-ttu-id="c2271-116">OS Patching For Linux</span><span class="sxs-lookup"><span data-stu-id="c2271-116">OS Patching For Linux</span></span> | <span data-ttu-id="c2271-117">VM Snapshot Linux</span><span class="sxs-lookup"><span data-stu-id="c2271-117">VM Snapshot Linux</span></span>
| <span data-ttu-id="c2271-118">Acronis Backup Linux</span><span class="sxs-lookup"><span data-stu-id="c2271-118">Acronis Backup Linux</span></span> | <span data-ttu-id="c2271-119">Estensione Docker</span><span class="sxs-lookup"><span data-stu-id="c2271-119">Docker Extension</span></span> | <span data-ttu-id="c2271-120">Puppet Agent</span><span class="sxs-lookup"><span data-stu-id="c2271-120">Puppet Agent</span></span> |
| <span data-ttu-id="c2271-121">BGInfo</span><span class="sxs-lookup"><span data-stu-id="c2271-121">Bg Info</span></span> | <span data-ttu-id="c2271-122">DSC Extension</span><span class="sxs-lookup"><span data-stu-id="c2271-122">DSC Extension</span></span> | <span data-ttu-id="c2271-123">Site 24x7 Apm Insight</span><span class="sxs-lookup"><span data-stu-id="c2271-123">Site 24x7 Apm Insight</span></span> |
| <span data-ttu-id="c2271-124">BMC CTM Agent Linux</span><span class="sxs-lookup"><span data-stu-id="c2271-124">BMC CTM Agent Linux</span></span> | <span data-ttu-id="c2271-125">Dynatrace Linux</span><span class="sxs-lookup"><span data-stu-id="c2271-125">Dynatrace Linux</span></span> | <span data-ttu-id="c2271-126">Site 24x7 Linux Server</span><span class="sxs-lookup"><span data-stu-id="c2271-126">Site 24x7 Linux Server</span></span> |
| <span data-ttu-id="c2271-127">BMC CTM Agent Windows</span><span class="sxs-lookup"><span data-stu-id="c2271-127">BMC CTM Agent Windows</span></span> | <span data-ttu-id="c2271-128">Dynatrace Windows</span><span class="sxs-lookup"><span data-stu-id="c2271-128">Dynatrace Windows</span></span> | <span data-ttu-id="c2271-129">Site 24x7 Windows Server</span><span class="sxs-lookup"><span data-stu-id="c2271-129">Site 24x7 Windows Server</span></span> |
| <span data-ttu-id="c2271-130">Chef Client</span><span class="sxs-lookup"><span data-stu-id="c2271-130">Chef Client</span></span> | <span data-ttu-id="c2271-131">HPE Security Application Defender</span><span class="sxs-lookup"><span data-stu-id="c2271-131">HPE Security Application Defender</span></span> | <span data-ttu-id="c2271-132">Trend Micro DSA</span><span class="sxs-lookup"><span data-stu-id="c2271-132">Trend Micro DSA</span></span> |
| <span data-ttu-id="c2271-133">Custom Script</span><span class="sxs-lookup"><span data-stu-id="c2271-133">Custom Script</span></span> | <span data-ttu-id="c2271-134">IaaS Antimalware</span><span class="sxs-lookup"><span data-stu-id="c2271-134">IaaS Antimalware</span></span> | <span data-ttu-id="c2271-135">Trend Micro DSA Linux</span><span class="sxs-lookup"><span data-stu-id="c2271-135">Trend Micro DSA Linux</span></span> |
| <span data-ttu-id="c2271-136">Estensione di script personalizzati</span><span class="sxs-lookup"><span data-stu-id="c2271-136">Custom Script Extension</span></span> | <span data-ttu-id="c2271-137">IaaS Diagnostics</span><span class="sxs-lookup"><span data-stu-id="c2271-137">IaaS Diagnostics</span></span> | <span data-ttu-id="c2271-138">VM Access For Linux</span><span class="sxs-lookup"><span data-stu-id="c2271-138">VM Access For Linux</span></span> |
| <span data-ttu-id="c2271-139">Custom Script for Linux</span><span class="sxs-lookup"><span data-stu-id="c2271-139">Custom Script for Linux</span></span> | <span data-ttu-id="c2271-140">Linux Chef Client</span><span class="sxs-lookup"><span data-stu-id="c2271-140">Linux Chef Client</span></span> | <span data-ttu-id="c2271-141">VM Access For Linux</span><span class="sxs-lookup"><span data-stu-id="c2271-141">VM Access For Linux</span></span> |
| <span data-ttu-id="c2271-142">Datadog Linux Agent</span><span class="sxs-lookup"><span data-stu-id="c2271-142">Datadog Linux Agent</span></span> | <span data-ttu-id="c2271-143">Linux Diagnostic</span><span class="sxs-lookup"><span data-stu-id="c2271-143">Linux Diagnostic</span></span> | <span data-ttu-id="c2271-144">VM Snapshot</span><span class="sxs-lookup"><span data-stu-id="c2271-144">VM Snapshot</span></span> |

## <a name="export-the-resource-group"></a><span data-ttu-id="c2271-145">Esportare il gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="c2271-145">Export the Resource Group</span></span>

<span data-ttu-id="c2271-146">Per esportare un gruppo di risorse in un modello riutilizzabile, completare i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c2271-146">To export a Resource Group into a reusable template, complete the following steps:</span></span>

1. <span data-ttu-id="c2271-147">Accedere al portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c2271-147">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="c2271-148">Scegliere Gruppi di risorse dal menu Hub</span><span class="sxs-lookup"><span data-stu-id="c2271-148">On the Hub Menu, click Resource Groups</span></span>
3. <span data-ttu-id="c2271-149">Selezionare il gruppo di risorse di destinazione dall'elenco</span><span class="sxs-lookup"><span data-stu-id="c2271-149">Select the target resource group from the list</span></span>
4. <span data-ttu-id="c2271-150">Nel pannello Gruppo di risorse fare clic su Script di automazione</span><span class="sxs-lookup"><span data-stu-id="c2271-150">In the Resource Group blade, click Automation Script</span></span>

![Esportazione del modello](./media/extensions-export-templates/template-export.png)

<span data-ttu-id="c2271-152">Lo script di automazione di Azure Resource Manager genera un modello di Resource Manager, un file di parametri e diversi esempi di script di distribuzione, ad esempio l'interfaccia della riga di comando di Azure e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2271-152">The Azure Resource Manager automations script produces a Resource Manager template, a parameters file, and several sample deployment scripts such as PowerShell and Azure CLI.</span></span> <span data-ttu-id="c2271-153">A questo punto, il modello esportato può essere scaricato utilizzando il pulsante di download, aggiunto come nuovo modello alla libreria di modelli o ridistribuito utilizzando il pulsante di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c2271-153">At this point, the exported template can be downloaded using the download button, added as a new template to the template library, or redeployed using the deploy button.</span></span>

## <a name="configure-protected-settings"></a><span data-ttu-id="c2271-154">Configurare le impostazioni protette</span><span class="sxs-lookup"><span data-stu-id="c2271-154">Configure protected settings</span></span>

<span data-ttu-id="c2271-155">Molte estensioni macchina virtuale di Azure includono una configurazione di impostazioni protette, che crittografa i dati sensibili come credenziali e stringhe di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c2271-155">Many Azure virtual machine extensions include a protected settings configuration, that encrypts sensitive data such as credentials and configuration strings.</span></span> <span data-ttu-id="c2271-156">Le impostazioni protette non vengono esportate con lo script di automazione.</span><span class="sxs-lookup"><span data-stu-id="c2271-156">Protected settings are not exported with the automation script.</span></span> <span data-ttu-id="c2271-157">Se necessario, le impostazioni protette devono essere reinserite nel modello esportato.</span><span class="sxs-lookup"><span data-stu-id="c2271-157">If necessary, protected settings need to be reinserted into the exported templated.</span></span>

### <a name="step-1---remove-template-parameter"></a><span data-ttu-id="c2271-158">Passaggio 1 - Rimuovere il parametro del modello</span><span class="sxs-lookup"><span data-stu-id="c2271-158">Step 1 - Remove template parameter</span></span>

<span data-ttu-id="c2271-159">Quando viene esportato il gruppo di risorse, viene creato un singolo parametro del modello per fornire un valore alle impostazioni protette esportate.</span><span class="sxs-lookup"><span data-stu-id="c2271-159">When the Resource Group is exported, a single template parameter is created to provide a value to the exported protected settings.</span></span> <span data-ttu-id="c2271-160">Questo parametro può essere rimosso.</span><span class="sxs-lookup"><span data-stu-id="c2271-160">This parameter can be removed.</span></span> <span data-ttu-id="c2271-161">Per rimuovere il parametro, esaminare l'elenco di parametri ed eliminare il parametro che è simile a questo esempio JSON.</span><span class="sxs-lookup"><span data-stu-id="c2271-161">To remove the parameter, look through the parameter list and delete the parameter that looks similar to this JSON example.</span></span>

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a><span data-ttu-id="c2271-162">Passaggio 2 - Proteggere le proprietà delle impostazioni</span><span class="sxs-lookup"><span data-stu-id="c2271-162">Step 2 - Get protected settings properties</span></span>

<span data-ttu-id="c2271-163">Poiché ogni impostazione protetta contiene un set di proprietà obbligatorie, è necessario raccogliere in un elenco tali proprietà.</span><span class="sxs-lookup"><span data-stu-id="c2271-163">Because each protected setting has a set of required properties, a list of these properties need to be gathered.</span></span> <span data-ttu-id="c2271-164">Ogni parametro della configurazione delle impostazioni protette è disponibile nello [schema di Azure Resource Manager su GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span><span class="sxs-lookup"><span data-stu-id="c2271-164">Each parameter of the protected settings configuration can be found in the [Azure Resource Manager schema on GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span></span> <span data-ttu-id="c2271-165">Tale schema include solo il set di parametri per le estensioni elencate nella sezione panoramica di questo documento.</span><span class="sxs-lookup"><span data-stu-id="c2271-165">This schema only includes the parameter sets for the extensions listed in the overview section of this document.</span></span> 

<span data-ttu-id="c2271-166">All'interno del repository dello schema, cercare l'estensione desiderata, per questo esempio `IaaSDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="c2271-166">From within the schema repository, search for the desired extension, for this example `IaaSDiagnostics`.</span></span> <span data-ttu-id="c2271-167">Dopo aver individuato le estensioni dell'oggetto `protectedSettings`, prendere nota di ogni parametro.</span><span class="sxs-lookup"><span data-stu-id="c2271-167">Once the extensions `protectedSettings` object has been located, take note of each parameter.</span></span> <span data-ttu-id="c2271-168">Nell'esempio dell'estensione `IaasDiagnostic`, i parametri richiesti sono `storageAccountName`, `storageAccountKey` e `storageAccountEndPoint`.</span><span class="sxs-lookup"><span data-stu-id="c2271-168">In the example of the `IaasDiagnostic` extension, the require parameters are `storageAccountName`, `storageAccountKey`, and `storageAccountEndPoint`.</span></span>

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

### <a name="step-3---re-create-the-protected-configuration"></a><span data-ttu-id="c2271-169">Passaggio 3 - Ricreare la configurazione protetta</span><span class="sxs-lookup"><span data-stu-id="c2271-169">Step 3 - Re-create the protected configuration</span></span>

<span data-ttu-id="c2271-170">Nel modello esportato, cercare `protectedSettings` e sostituire l'oggetto delle impostazioni protette esportate con uno nuovo che includa i parametri dell'estensione necessari e un valore per ognuno di essi.</span><span class="sxs-lookup"><span data-stu-id="c2271-170">On the exported template, search for `protectedSettings` and replace the exported protected setting object with a new one that includes the required extension parameters and a value for each one.</span></span>

<span data-ttu-id="c2271-171">Nell'esempio dell'estensione `IaasDiagnostic`, la nuova configurazione delle impostazioni protette dovrebbe essere simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c2271-171">In the example of the `IaasDiagnostic` extension, the new protected setting configuration would look like the following example:</span></span>

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

<span data-ttu-id="c2271-172">La risorsa dell'estensione finale è simile all'esempio JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="c2271-172">The final extension resource looks similar to the following JSON example:</span></span>

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

<span data-ttu-id="c2271-173">Se si utilizzano parametri del modello per fornire i valori delle proprietà, questi devono essere creati.</span><span class="sxs-lookup"><span data-stu-id="c2271-173">If using template parameters to provide property values, these need to be created.</span></span> <span data-ttu-id="c2271-174">Durante la creazione di parametri del modello per i valori delle impostazioni protette, assicurarsi di utilizzare il tipo di parametro `SecureString`, in modo che i valori sensibili siano protetti.</span><span class="sxs-lookup"><span data-stu-id="c2271-174">When creating template parameters for protected setting values, make sure to use the `SecureString` parameter type so that sensitive values are secured.</span></span> <span data-ttu-id="c2271-175">Per altre informazioni sull'utilizzo dei parametri, vedere [Creazione di modelli di Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c2271-175">For more information on using parameters, see [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="c2271-176">Nell'esempio dell'estensione `IaasDiagnostic`, i parametri seguenti devono essere creati nella sezione dei parametri del modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c2271-176">In the example of the `IaasDiagnostic` extension, the following parameters would be created in the parameters section of the Resource Manager template.</span></span>

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

<span data-ttu-id="c2271-177">A questo punto, il modello può essere distribuito utilizzando qualsiasi metodo di distribuzione del modello.</span><span class="sxs-lookup"><span data-stu-id="c2271-177">At this point, the template can be deployed using any template deployment method.</span></span>

---
title: estensione di macchina virtuale di Azure per Windows aaaOMS | Documenti Microsoft
description: Distribuire l'agente OMS hello nella macchina virtuale Windows usando un'estensione della macchina virtuale.
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: feae6176-2373-4034-b5d9-a32c6b4e1f10
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: 3000f66c0acdec1d1fad2125b8c6b72a92b1ec92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="47cfb-103">Estensione macchina virtuale OMS per Windows</span><span class="sxs-lookup"><span data-stu-id="47cfb-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="47cfb-104">In Operations Management Suite (OMS) sono disponibili funzionalità di monitoraggio, avviso e correzione tramite avvisi in risorse cloud e locali.</span><span class="sxs-lookup"><span data-stu-id="47cfb-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="47cfb-105">estensione della macchina virtuale agente OMS per Windows Hello è pubblicato e supportato da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="47cfb-105">hello OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="47cfb-106">estensione Hello installa l'agente OMS hello in macchine virtuali di Azure e registra le macchine virtuali in un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="47cfb-106">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="47cfb-107">Opzioni di distribuzione, le configurazioni e piattaforme hello di dettagli in questo documento supportato per l'estensione della macchina virtuale OMS hello per Windows.</span><span class="sxs-lookup"><span data-stu-id="47cfb-107">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47cfb-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="47cfb-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="47cfb-109">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="47cfb-109">Operating system</span></span>
<span data-ttu-id="47cfb-110">Hello estensione OMS Agent per Windows possono essere eseguite in Windows Server 2008 R2, 2012 e 2012 R2 2016 rilascia.</span><span class="sxs-lookup"><span data-stu-id="47cfb-110">hello OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="47cfb-111">Connettività Internet</span><span class="sxs-lookup"><span data-stu-id="47cfb-111">Internet connectivity</span></span>
<span data-ttu-id="47cfb-112">estensione OMS Agent per Windows Hello richiede tale macchina virtuale di destinazione hello è connesso toohello internet.</span><span class="sxs-lookup"><span data-stu-id="47cfb-112">hello OMS Agent extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="47cfb-113">Schema dell'estensione</span><span class="sxs-lookup"><span data-stu-id="47cfb-113">Extension schema</span></span>

<span data-ttu-id="47cfb-114">Hello JSON seguente viene illustrato lo schema di hello per hello estensione OMS Agent.</span><span class="sxs-lookup"><span data-stu-id="47cfb-114">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="47cfb-115">estensione Hello richiede hello dell'area di lavoro area di lavoro e l'Id chiave dall'area di lavoro OMS destinazione hello, questi possono essere disponibili nel portale OMS hello.</span><span class="sxs-lookup"><span data-stu-id="47cfb-115">hello extension requires hello workspace Id and workspace key from hello target OMS workspace, these can be found in hello OMS portal.</span></span> <span data-ttu-id="47cfb-116">Poiché chiave dell'area di lavoro hello deve essere considerate come dati sensibili, devono essere archiviato in una configurazione di impostazione protetto.</span><span class="sxs-lookup"><span data-stu-id="47cfb-116">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="47cfb-117">Dati impostazione protette dell'estensione di macchina virtuale di Azure sono crittografati e decrittografati solo nella macchina virtuale di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="47cfb-117">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="47cfb-118">Tenere presente che **workspaceId** e **workspaceKey** distinguono tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="47cfb-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```
### <a name="property-values"></a><span data-ttu-id="47cfb-119">Valori delle proprietà</span><span class="sxs-lookup"><span data-stu-id="47cfb-119">Property values</span></span>

| <span data-ttu-id="47cfb-120">Nome</span><span class="sxs-lookup"><span data-stu-id="47cfb-120">Name</span></span> | <span data-ttu-id="47cfb-121">Valore/Esempio</span><span class="sxs-lookup"><span data-stu-id="47cfb-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="47cfb-122">apiVersion</span><span class="sxs-lookup"><span data-stu-id="47cfb-122">apiVersion</span></span> | <span data-ttu-id="47cfb-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="47cfb-123">2015-06-15</span></span> |
| <span data-ttu-id="47cfb-124">publisher</span><span class="sxs-lookup"><span data-stu-id="47cfb-124">publisher</span></span> | <span data-ttu-id="47cfb-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="47cfb-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="47cfb-126">type</span><span class="sxs-lookup"><span data-stu-id="47cfb-126">type</span></span> | <span data-ttu-id="47cfb-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="47cfb-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="47cfb-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="47cfb-128">typeHandlerVersion</span></span> | <span data-ttu-id="47cfb-129">1.0</span><span class="sxs-lookup"><span data-stu-id="47cfb-129">1.0</span></span> |
| <span data-ttu-id="47cfb-130">workspaceId (esempio)</span><span class="sxs-lookup"><span data-stu-id="47cfb-130">workspaceId (e.g)</span></span> | <span data-ttu-id="47cfb-131">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="47cfb-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="47cfb-132">workspaceKey (esempio)</span><span class="sxs-lookup"><span data-stu-id="47cfb-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="47cfb-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="47cfb-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="47cfb-134">Distribuzione del modello</span><span class="sxs-lookup"><span data-stu-id="47cfb-134">Template deployment</span></span>

<span data-ttu-id="47cfb-135">Le estensioni macchina virtuale di Azure possono essere distribuite con i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="47cfb-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="47cfb-136">schema JSON Hello descritta in dettaglio nella sezione precedente hello è utilizzabile in un hello toorun modello di gestione risorse di Azure estensione OMS Agent durante la distribuzione di un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="47cfb-136">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="47cfb-137">Un modello di esempio che include l'estensione della macchina virtuale di agente OMS hello è reperibile in hello [raccolta avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="47cfb-137">A sample template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="47cfb-138">Hello JSON per un'estensione della macchina virtuale può essere annidata all'interno di risorsa di macchina virtuale hello o posizionato nella radice di hello o un livello superiore di un modello di gestione risorse di JSON.</span><span class="sxs-lookup"><span data-stu-id="47cfb-138">hello JSON for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="47cfb-139">posizionamento di Hello di hello JSON influisce sul valore di hello del nome della risorsa hello e tipo.</span><span class="sxs-lookup"><span data-stu-id="47cfb-139">hello placement of hello JSON affects hello value of hello resource name and type.</span></span> <span data-ttu-id="47cfb-140">Per altre informazioni, vedere [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md) (Impostare il nome e il tipo per le risorse figlio).</span><span class="sxs-lookup"><span data-stu-id="47cfb-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="47cfb-141">Hello seguente si presuppone hello OMS estensione annidata all'interno di hello risorsa di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="47cfb-141">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="47cfb-142">Quando la nidificazione di risorse di estensione hello, hello JSON viene inserito nel hello `"resources": []` oggetto della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="47cfb-142">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>


```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

<span data-ttu-id="47cfb-143">Quando si inseriscono estensione hello JSON nella radice di hello del modello di hello, il nome di risorsa hello include una macchina virtuale di riferimento toohello padre e il tipo hello riflette configurazione annidati hello.</span><span class="sxs-lookup"><span data-stu-id="47cfb-143">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span> 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

## <a name="powershell-deployment"></a><span data-ttu-id="47cfb-144">Distribuzione PowerShell</span><span class="sxs-lookup"><span data-stu-id="47cfb-144">PowerShell deployment</span></span>

<span data-ttu-id="47cfb-145">Hello `Set-AzureRmVMExtension` comando può essere utilizzato toodeploy hello agente OMS macchina virtuale estensione tooan macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="47cfb-145">hello `Set-AzureRmVMExtension` command can be used toodeploy hello OMS Agent virtual machine extension tooan existing virtual machine.</span></span> <span data-ttu-id="47cfb-146">Prima di eseguire il comando hello, configurazioni di hello pubbliche e private necessario toobe archiviati in una tabella hash di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47cfb-146">Before running hello command, hello public and private configurations need toobe stored in a PowerShell hash table.</span></span> 

```powershell
$PublicSettings = @{"workspaceId" = "myWorkspaceId"}
$ProtectedSettings = @{"workspaceKey" = "myWorkspaceKey"}

Set-AzureRmVMExtension -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
    -ExtensionType "MicrosoftMonitoringAgent" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS ` 
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="47cfb-147">Risoluzione dei problemi e supporto</span><span class="sxs-lookup"><span data-stu-id="47cfb-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="47cfb-148">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="47cfb-148">Troubleshoot</span></span>

<span data-ttu-id="47cfb-149">Dati sullo stato di hello delle distribuzioni di estensione possono essere recuperati dal portale di Azure hello e, utilizzando il modulo di Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="47cfb-149">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="47cfb-150">lo stato di distribuzione hello toosee delle estensioni per una macchina virtuale specificata, hello esecuzione seguente comando utilizzando hello modulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47cfb-150">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="47cfb-151">Esecuzione di estensione di output è toofiles registrati nell'hello seguente directory:</span><span class="sxs-lookup"><span data-stu-id="47cfb-151">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="47cfb-152">Supporto</span><span class="sxs-lookup"><span data-stu-id="47cfb-152">Support</span></span>

<span data-ttu-id="47cfb-153">Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti hello [forum MSDN di Azure e di Overflow dello Stack](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="47cfb-153">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="47cfb-154">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="47cfb-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="47cfb-155">Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/en-us/support/options/) e scegliere supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="47cfb-155">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="47cfb-156">Per informazioni sull'utilizzo di supporto di Azure, leggere hello [supporto tecnico di Microsoft Azure domande frequenti su](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="47cfb-156">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>

---
title: Estensione macchina virtuale di Azure OMS per Windows | Documentazione Microsoft
description: Distribuire l'agente OMS nella macchina virtuale Windows usando un'estensione macchina virtuale.
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
ms.openlocfilehash: d933f488fdda0c1d37892be65f2712cf0eb5694e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="30946-103">Estensione macchina virtuale OMS per Windows</span><span class="sxs-lookup"><span data-stu-id="30946-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="30946-104">In Operations Management Suite (OMS) sono disponibili funzionalità di monitoraggio, avviso e correzione tramite avvisi in risorse cloud e locali.</span><span class="sxs-lookup"><span data-stu-id="30946-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="30946-105">L'estensione macchina virtuale agente OMS per Windows è pubblicata e supportata da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="30946-105">The OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="30946-106">L'estensione installa l'agente OMS in macchine virtuali di Azure e registra le macchine virtuali in un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="30946-106">The extension installs the OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="30946-107">Questo documento descrive in dettaglio le piattaforme, le configurazioni e le opzioni di distribuzione supportate per l'estensione macchina virtuale OMS per Windows.</span><span class="sxs-lookup"><span data-stu-id="30946-107">This document details the supported platforms, configurations, and deployment options for the OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30946-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="30946-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="30946-109">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="30946-109">Operating system</span></span>
<span data-ttu-id="30946-110">L'estensione agente OMS per Windows può essere eseguita in Windows Server 2008 R2, 2012, 2012 R2 e 2016.</span><span class="sxs-lookup"><span data-stu-id="30946-110">The OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="30946-111">Connettività Internet</span><span class="sxs-lookup"><span data-stu-id="30946-111">Internet connectivity</span></span>
<span data-ttu-id="30946-112">Per distribuire l'estensione agente OMS per Windows, è necessario che la macchina virtuale di destinazione sia connessa a Internet.</span><span class="sxs-lookup"><span data-stu-id="30946-112">The OMS Agent extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="30946-113">Schema dell'estensione</span><span class="sxs-lookup"><span data-stu-id="30946-113">Extension schema</span></span>

<span data-ttu-id="30946-114">Il codice JSON riportato di seguito mostra lo schema dell'estensione OMS Agent.</span><span class="sxs-lookup"><span data-stu-id="30946-114">The following JSON shows the schema for the OMS Agent extension.</span></span> <span data-ttu-id="30946-115">L'estensione richiede che siano indicati l'ID e la chiave dell'area di lavoro presenti nell'area di lavoro OMS di destinazione. Questi valori sono disponibili nel portale OMS.</span><span class="sxs-lookup"><span data-stu-id="30946-115">The extension requires the workspace Id and workspace key from the target OMS workspace, these can be found in the OMS portal.</span></span> <span data-ttu-id="30946-116">Poiché la chiave dell'area di lavoro deve essere tratta come i dati sensibili, deve essere memorizzata in una configurazione protetta.</span><span class="sxs-lookup"><span data-stu-id="30946-116">Because the workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="30946-117">I dati della configurazione protetta dell'estensione macchina virtuale di Azure vengono crittografati, per essere poi decrittografati solo nella macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="30946-117">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span> <span data-ttu-id="30946-118">Tenere presente che **workspaceId** e **workspaceKey** distinguono tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="30946-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

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
### <a name="property-values"></a><span data-ttu-id="30946-119">Valori delle proprietà</span><span class="sxs-lookup"><span data-stu-id="30946-119">Property values</span></span>

| <span data-ttu-id="30946-120">Nome</span><span class="sxs-lookup"><span data-stu-id="30946-120">Name</span></span> | <span data-ttu-id="30946-121">Valore/Esempio</span><span class="sxs-lookup"><span data-stu-id="30946-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="30946-122">apiVersion</span><span class="sxs-lookup"><span data-stu-id="30946-122">apiVersion</span></span> | <span data-ttu-id="30946-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="30946-123">2015-06-15</span></span> |
| <span data-ttu-id="30946-124">publisher</span><span class="sxs-lookup"><span data-stu-id="30946-124">publisher</span></span> | <span data-ttu-id="30946-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="30946-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="30946-126">type</span><span class="sxs-lookup"><span data-stu-id="30946-126">type</span></span> | <span data-ttu-id="30946-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="30946-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="30946-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="30946-128">typeHandlerVersion</span></span> | <span data-ttu-id="30946-129">1.0</span><span class="sxs-lookup"><span data-stu-id="30946-129">1.0</span></span> |
| <span data-ttu-id="30946-130">workspaceId (esempio)</span><span class="sxs-lookup"><span data-stu-id="30946-130">workspaceId (e.g)</span></span> | <span data-ttu-id="30946-131">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="30946-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="30946-132">workspaceKey (esempio)</span><span class="sxs-lookup"><span data-stu-id="30946-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="30946-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="30946-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="30946-134">Distribuzione del modello</span><span class="sxs-lookup"><span data-stu-id="30946-134">Template deployment</span></span>

<span data-ttu-id="30946-135">Le estensioni macchina virtuale di Azure possono essere distribuite con i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="30946-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="30946-136">Lo schema JSON indicato nella sezione precedente può essere usato in un modello di Azure Resource Manager per eseguire l'estensione agente OMS durante la distribuzione di un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="30946-136">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="30946-137">Un esempio di modello che include l'estensione macchina virtuale Agente OMS è disponibile nella [raccolta di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="30946-137">A sample template that includes the OMS Agent VM extension can be found on the [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="30946-138">Il codice JSON per un'estensione della macchina virtuale può essere nidificato nella risorsa della macchina virtuale o posizionato nel livello radice o nel livello superiore di un modello JSON di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="30946-138">The JSON for a virtual machine extension can be nested inside the virtual machine resource, or placed at the root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="30946-139">Il posizionamento di JSON influisce sul valore del nome e tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="30946-139">The placement of the JSON affects the value of the resource name and type.</span></span> <span data-ttu-id="30946-140">Per altre informazioni, vedere [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md) (Impostare il nome e il tipo per le risorse figlio).</span><span class="sxs-lookup"><span data-stu-id="30946-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="30946-141">L'esempio seguente presuppone che l'estensione OMS sia annidata all'interno della risorsa della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="30946-141">The following example assumes the OMS extension is nested inside the virtual machine resource.</span></span> <span data-ttu-id="30946-142">Quando la risorsa di estensione viene nidificata, JSON viene inserito nell'oggetto `"resources": []` della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="30946-142">When nesting the extension resource, the JSON is placed in the `"resources": []` object of the virtual machine.</span></span>


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

<span data-ttu-id="30946-143">Quando si posiziona l'estensione JSON nella radice del modello, il nome della risorsa include un riferimento alla macchina virtuale padre e il tipo riflette la configurazione annidata.</span><span class="sxs-lookup"><span data-stu-id="30946-143">When placing the extension JSON at the root of the template, the resource name includes a reference to the parent virtual machine, and the type reflects the nested configuration.</span></span> 

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

## <a name="powershell-deployment"></a><span data-ttu-id="30946-144">Distribuzione PowerShell</span><span class="sxs-lookup"><span data-stu-id="30946-144">PowerShell deployment</span></span>

<span data-ttu-id="30946-145">Il comando `Set-AzureRmVMExtension` consente di distribuire l'estensione macchina virtuale OMS a una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="30946-145">The `Set-AzureRmVMExtension` command can be used to deploy the OMS Agent virtual machine extension to an existing virtual machine.</span></span> <span data-ttu-id="30946-146">Prima di eseguire il comando, le configurazioni pubbliche e private devono essere archiviate in una tabella hash di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="30946-146">Before running the command, the public and private configurations need to be stored in a PowerShell hash table.</span></span> 

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

## <a name="troubleshoot-and-support"></a><span data-ttu-id="30946-147">Risoluzione dei problemi e supporto</span><span class="sxs-lookup"><span data-stu-id="30946-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="30946-148">Risolvere problemi</span><span class="sxs-lookup"><span data-stu-id="30946-148">Troubleshoot</span></span>

<span data-ttu-id="30946-149">I dati sullo stato delle distribuzioni dell'estensione possono essere recuperati nel portale di Azure e tramite il modulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="30946-149">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="30946-150">Per visualizzare lo stato di distribuzione delle estensioni per una determinata VM, eseguire questo comando nel modulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="30946-150">To see the deployment state of extensions for a given VM, run the following command using the Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="30946-151">L'output dell'esecuzione dell'estensione viene registrato nei file presenti nella directory seguente:</span><span class="sxs-lookup"><span data-stu-id="30946-151">Extension execution output is logged to files found in the following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="30946-152">Supporto</span><span class="sxs-lookup"><span data-stu-id="30946-152">Support</span></span>

<span data-ttu-id="30946-153">Per ricevere assistenza in relazione a qualsiasi punto di questo articolo, contattare gli esperti di Azure nei [forum MSDN e Stack Overflow relativi ad Azure](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="30946-153">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="30946-154">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="30946-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="30946-155">Accedere al [sito del supporto di Azure](https://azure.microsoft.com/en-us/support/options/) e selezionare l'opzione desiderata per ottenere supporto.</span><span class="sxs-lookup"><span data-stu-id="30946-155">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="30946-156">Per informazioni sull'uso del supporto di Azure, leggere le [Domande frequenti sul supporto di Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="30946-156">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>

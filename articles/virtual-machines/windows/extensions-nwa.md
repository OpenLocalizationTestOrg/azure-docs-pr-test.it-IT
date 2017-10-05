---
title: Estensione macchina virtuale agente Network Watcher per Windows | Documentazione Microsoft
description: Distribuire l'agente Network Watcher in una macchina virtuale Windows usando un'estensione macchina virtuale.
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: b8d6a998bc86337b286a3434f44f762cca9b7e68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a><span data-ttu-id="5ab4e-103">Estensione macchina virtuale agente Network Watcher per Windows</span><span class="sxs-lookup"><span data-stu-id="5ab4e-103">Network Watcher Agent virtual machine extension for Windows</span></span>

## <a name="overview"></a><span data-ttu-id="5ab4e-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5ab4e-104">Overview</span></span>

<span data-ttu-id="5ab4e-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) è un servizio di monitoraggio delle prestazioni di rete, diagnostica e analisi che consente di monitorare le reti di Azure.</span><span class="sxs-lookup"><span data-stu-id="5ab4e-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="5ab4e-106">L'estensione macchina virtuale Network Watcher Agent è un requisito per alcune funzionalità di Network Watcher nelle macchine virtuali di Azure,</span><span class="sxs-lookup"><span data-stu-id="5ab4e-106">The Network Watcher Agent virtual machine extension is a requirement for some of the Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="5ab4e-107">Include l'acquisizione del traffico di rete su richiesta e altre funzionalità avanzate.</span><span class="sxs-lookup"><span data-stu-id="5ab4e-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="5ab4e-108">Questo documento descrive in dettaglio le piattaforme e le opzioni di distribuzione supportate per l'estensione macchina virtuale agente Network Watcher per Windows.</span><span class="sxs-lookup"><span data-stu-id="5ab4e-108">This document details the supported platforms and deployment options for the Network Watcher Agent virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ab4e-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5ab4e-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="5ab4e-110">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="5ab4e-110">Operating system</span></span>

<span data-ttu-id="5ab4e-111">L'estensione agente Network Watcher per Windows può essere eseguita in Windows Server 2008 R2, 2012, 2012 R2 e 2016.</span><span class="sxs-lookup"><span data-stu-id="5ab4e-111">The Network Watcher Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span> <span data-ttu-id="5ab4e-112">Si noti che il Nano Server non è supportato in questo momento.</span><span class="sxs-lookup"><span data-stu-id="5ab4e-112">Note that the Nano Server is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="5ab4e-113">Connettività Internet</span><span class="sxs-lookup"><span data-stu-id="5ab4e-113">Internet connectivity</span></span>

<span data-ttu-id="5ab4e-114">Alcune delle funzionalità di Network Watcher Agent richiedono che la macchina virtuale di destinazione sia connessa a Internet.</span><span class="sxs-lookup"><span data-stu-id="5ab4e-114">Some of the Network Watcher Agent functionality requires that the target virtual machine be connected to the Internet.</span></span> <span data-ttu-id="5ab4e-115">Se non vi è la possibilità di stabilire connessioni in uscita, alcune funzionalità di Network Watcher Agent potrebbero non funzionare correttamente o non essere disponibili.</span><span class="sxs-lookup"><span data-stu-id="5ab4e-115">Without the ability to establish outgoing connections some of the Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="5ab4e-116">Per maggiori dettagli, vedere la [documentazione di Network Watcher](../../network-watcher/network-watcher-monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ab4e-116">For more details, please see the [Network Watcher documentation](../../network-watcher/network-watcher-monitoring-overview.md).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="5ab4e-117">Schema dell'estensione</span><span class="sxs-lookup"><span data-stu-id="5ab4e-117">Extension schema</span></span>

<span data-ttu-id="5ab4e-118">Lo schema JSON seguente illustra lo schema dell'estensione Network Watcher Agent.</span><span class="sxs-lookup"><span data-stu-id="5ab4e-118">The following JSON shows the schema for the Network Watcher Agent extension.</span></span> <span data-ttu-id="5ab4e-119">Al momento, l'estensione non richiede né supporta impostazioni fornite dall'utente e si basa sulla configurazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5ab4e-119">The extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="5ab4e-120">Valori delle proprietà</span><span class="sxs-lookup"><span data-stu-id="5ab4e-120">Property values</span></span>

| <span data-ttu-id="5ab4e-121">Nome</span><span class="sxs-lookup"><span data-stu-id="5ab4e-121">Name</span></span> | <span data-ttu-id="5ab4e-122">Valore/Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab4e-122">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="5ab4e-123">apiVersion</span><span class="sxs-lookup"><span data-stu-id="5ab4e-123">apiVersion</span></span> | <span data-ttu-id="5ab4e-124">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="5ab4e-124">2015-06-15</span></span> |
| <span data-ttu-id="5ab4e-125">publisher</span><span class="sxs-lookup"><span data-stu-id="5ab4e-125">publisher</span></span> | <span data-ttu-id="5ab4e-126">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="5ab4e-126">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="5ab4e-127">type</span><span class="sxs-lookup"><span data-stu-id="5ab4e-127">type</span></span> | <span data-ttu-id="5ab4e-128">NetworkWatcherAgentWindows</span><span class="sxs-lookup"><span data-stu-id="5ab4e-128">NetworkWatcherAgentWindows</span></span> |
| <span data-ttu-id="5ab4e-129">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="5ab4e-129">typeHandlerVersion</span></span> | <span data-ttu-id="5ab4e-130">1.4</span><span class="sxs-lookup"><span data-stu-id="5ab4e-130">1.4</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="5ab4e-131">Distribuzione del modello</span><span class="sxs-lookup"><span data-stu-id="5ab4e-131">Template deployment</span></span>

<span data-ttu-id="5ab4e-132">Le estensioni macchina virtuale di Azure possono essere distribuite con i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5ab4e-132">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="5ab4e-133">Lo schema JSON indicato nella sezione precedente può essere usato in un modello di Azure Resource Manager per eseguire l'estensione agente Network Watcher durante la distribuzione di un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5ab4e-133">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="5ab4e-134">Distribuzione PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ab4e-134">PowerShell deployment</span></span>

<span data-ttu-id="5ab4e-135">Il comando `Set-AzureRmVMExtension` consente di distribuire l'estensione macchina virtuale agente Network Watcher a una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="5ab4e-135">The `Set-AzureRmVMExtension` command can be used to deploy the Network Watcher Agent virtual machine extension to an existing virtual machine.</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="5ab4e-136">Risoluzione dei problemi e supporto</span><span class="sxs-lookup"><span data-stu-id="5ab4e-136">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="5ab4e-137">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="5ab4e-137">Troubleshooting</span></span>

<span data-ttu-id="5ab4e-138">I dati sullo stato delle distribuzioni dell'estensione possono essere recuperati nel portale di Azure e tramite il modulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5ab4e-138">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="5ab4e-139">Per visualizzare lo stato di distribuzione delle estensioni per una determinata VM, eseguire questo comando nel modulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5ab4e-139">To see the deployment state of extensions for a given VM, run the following command using the Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

<span data-ttu-id="5ab4e-140">L'output dell'esecuzione dell'estensione viene registrato nei file presenti nella directory seguente:</span><span class="sxs-lookup"><span data-stu-id="5ab4e-140">Extension execution output is logged to files found in the following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a><span data-ttu-id="5ab4e-141">Supporto</span><span class="sxs-lookup"><span data-stu-id="5ab4e-141">Support</span></span>

<span data-ttu-id="5ab4e-142">Se in qualsiasi punto dell'articolo sono necessarie altre informazioni, fare riferimento alla documentazione Guida per l'utente di Network Watcher o contattare gli esperti di Azure nei [forum MSDN e Stack Overflow relativi ad Azure](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="5ab4e-142">If you need more help at any point in this article, you can refer to the Network Watcher User Guide documentation or contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="5ab4e-143">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="5ab4e-143">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="5ab4e-144">Accedere al [sito del supporto di Azure](https://azure.microsoft.com/en-us/support/options/) e selezionare l'opzione desiderata per ottenere supporto.</span><span class="sxs-lookup"><span data-stu-id="5ab4e-144">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="5ab4e-145">Per informazioni sull'uso del supporto di Azure, leggere le [Domande frequenti sul supporto di Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="5ab4e-145">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>

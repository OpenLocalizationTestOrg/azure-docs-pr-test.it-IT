---
title: estensione della macchina virtuale dell'agente di controllo di rete per Windows aaaAzure | Documenti Microsoft
description: Distribuire hello agente di controllo di rete nella macchina virtuale Windows usando un'estensione della macchina virtuale.
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
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a><span data-ttu-id="ae8a1-103">Estensione macchina virtuale agente Network Watcher per Windows</span><span class="sxs-lookup"><span data-stu-id="ae8a1-103">Network Watcher Agent virtual machine extension for Windows</span></span>

## <a name="overview"></a><span data-ttu-id="ae8a1-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ae8a1-104">Overview</span></span>

<span data-ttu-id="ae8a1-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) è un servizio di monitoraggio delle prestazioni di rete, diagnostica e analisi che consente di monitorare le reti di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae8a1-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="ae8a1-106">Hello estensione della macchina virtuale dell'agente di controllo di rete è un requisito per alcune delle funzionalità di hello Watcher di rete in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae8a1-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="ae8a1-107">Include l'acquisizione del traffico di rete su richiesta e altre funzionalità avanzate.</span><span class="sxs-lookup"><span data-stu-id="ae8a1-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="ae8a1-108">Questo hello dettagli di documento supportato piattaforme e le opzioni di distribuzione per hello estensione della macchina virtuale dell'agente di controllo di rete per Windows.</span><span class="sxs-lookup"><span data-stu-id="ae8a1-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae8a1-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ae8a1-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="ae8a1-110">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="ae8a1-110">Operating system</span></span>

<span data-ttu-id="ae8a1-111">Hello estensione rete Watcher agente per Windows possono essere eseguite in Windows Server 2008 R2, 2012 e 2012 R2 2016 rilascia.</span><span class="sxs-lookup"><span data-stu-id="ae8a1-111">hello Network Watcher Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span> <span data-ttu-id="ae8a1-112">Si noti che hello Nano Server non sono supportato in questo momento.</span><span class="sxs-lookup"><span data-stu-id="ae8a1-112">Note that hello Nano Server is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="ae8a1-113">Connettività Internet</span><span class="sxs-lookup"><span data-stu-id="ae8a1-113">Internet connectivity</span></span>

<span data-ttu-id="ae8a1-114">Alcune delle funzionalità dell'agente di controllo rete hello richiede tale macchina virtuale di destinazione hello connesso toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="ae8a1-114">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="ae8a1-115">Senza connessioni in uscita di hello possibilità tooestablish alcune delle funzionalità dell'agente di controllo rete hello malfunzionamento o non sono più disponibili.</span><span class="sxs-lookup"><span data-stu-id="ae8a1-115">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="ae8a1-116">Per ulteriori informazioni, vedere hello [documentazione Watcher di rete](../../network-watcher/network-watcher-monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ae8a1-116">For more details, please see hello [Network Watcher documentation](../../network-watcher/network-watcher-monitoring-overview.md).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="ae8a1-117">Schema dell'estensione</span><span class="sxs-lookup"><span data-stu-id="ae8a1-117">Extension schema</span></span>

<span data-ttu-id="ae8a1-118">Hello JSON seguente mostra lo schema di hello per hello estensione Agent Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="ae8a1-118">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="ae8a1-119">estensione di Hello non richiede né supporta le impostazioni fornite dall'utente in questo momento e si basa sulla configurazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ae8a1-119">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="ae8a1-120">Valori delle proprietà</span><span class="sxs-lookup"><span data-stu-id="ae8a1-120">Property values</span></span>

| <span data-ttu-id="ae8a1-121">Nome</span><span class="sxs-lookup"><span data-stu-id="ae8a1-121">Name</span></span> | <span data-ttu-id="ae8a1-122">Valore/Esempio</span><span class="sxs-lookup"><span data-stu-id="ae8a1-122">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="ae8a1-123">apiVersion</span><span class="sxs-lookup"><span data-stu-id="ae8a1-123">apiVersion</span></span> | <span data-ttu-id="ae8a1-124">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="ae8a1-124">2015-06-15</span></span> |
| <span data-ttu-id="ae8a1-125">publisher</span><span class="sxs-lookup"><span data-stu-id="ae8a1-125">publisher</span></span> | <span data-ttu-id="ae8a1-126">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="ae8a1-126">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="ae8a1-127">type</span><span class="sxs-lookup"><span data-stu-id="ae8a1-127">type</span></span> | <span data-ttu-id="ae8a1-128">NetworkWatcherAgentWindows</span><span class="sxs-lookup"><span data-stu-id="ae8a1-128">NetworkWatcherAgentWindows</span></span> |
| <span data-ttu-id="ae8a1-129">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="ae8a1-129">typeHandlerVersion</span></span> | <span data-ttu-id="ae8a1-130">1.4</span><span class="sxs-lookup"><span data-stu-id="ae8a1-130">1.4</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="ae8a1-131">Distribuzione del modello</span><span class="sxs-lookup"><span data-stu-id="ae8a1-131">Template deployment</span></span>

<span data-ttu-id="ae8a1-132">Le estensioni macchina virtuale di Azure possono essere distribuite con i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ae8a1-132">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="ae8a1-133">schema JSON Hello descritta in dettaglio nella sezione precedente hello è utilizzabile in un hello toorun modello di gestione risorse di Azure estensione Agent Watcher di rete durante la distribuzione di un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae8a1-133">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="ae8a1-134">Distribuzione PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae8a1-134">PowerShell deployment</span></span>

<span data-ttu-id="ae8a1-135">Hello `Set-AzureRmVMExtension` comando può essere utilizzato toodeploy hello agente di controllo di rete macchina virtuale estensione tooan macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="ae8a1-135">hello `Set-AzureRmVMExtension` command can be used toodeploy hello Network Watcher Agent virtual machine extension tooan existing virtual machine.</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="ae8a1-136">Risoluzione dei problemi e supporto</span><span class="sxs-lookup"><span data-stu-id="ae8a1-136">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="ae8a1-137">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="ae8a1-137">Troubleshooting</span></span>

<span data-ttu-id="ae8a1-138">Dati sullo stato di hello delle distribuzioni di estensione possono essere recuperati dal portale di Azure hello e, utilizzando il modulo di Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ae8a1-138">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="ae8a1-139">lo stato di distribuzione hello toosee delle estensioni per una macchina virtuale specificata, hello esecuzione seguente comando utilizzando hello modulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ae8a1-139">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

<span data-ttu-id="ae8a1-140">Esecuzione di estensione di output è toofiles registrati nell'hello seguente directory:</span><span class="sxs-lookup"><span data-stu-id="ae8a1-140">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a><span data-ttu-id="ae8a1-141">Supporto</span><span class="sxs-lookup"><span data-stu-id="ae8a1-141">Support</span></span>

<span data-ttu-id="ae8a1-142">Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile consultare la documentazione di toohello Guida utente Watcher di rete o contattare hello Azure esperti hello [forum MSDN di Azure e di Overflow dello Stack](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="ae8a1-142">If you need more help at any point in this article, you can refer toohello Network Watcher User Guide documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="ae8a1-143">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae8a1-143">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="ae8a1-144">Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/en-us/support/options/) e scegliere supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="ae8a1-144">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="ae8a1-145">Per informazioni sull'utilizzo di supporto di Azure, leggere hello [supporto tecnico di Microsoft Azure domande frequenti su](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="ae8a1-145">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>

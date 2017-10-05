---
title: Estensione macchina virtuale Azure Network Watcher Agent per Linux | Microsoft Docs
description: Distribuire Network Watcher Agent in una macchina virtuale Linux usando un'estensione macchina virtuale.
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: eaadd531b9e05a54446e61f98584ae9d75470a5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a><span data-ttu-id="a3130-103">Estensione macchina virtuale Network Watcher Agent per Linux</span><span class="sxs-lookup"><span data-stu-id="a3130-103">Network Watcher Agent virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="a3130-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a3130-104">Overview</span></span>

<span data-ttu-id="a3130-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) è un servizio di monitoraggio delle prestazioni di rete, diagnostica e analisi che consente di monitorare le reti di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3130-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="a3130-106">L'estensione macchina virtuale Network Watcher Agent è un requisito per alcune funzionalità di Network Watcher nelle macchine virtuali di Azure,</span><span class="sxs-lookup"><span data-stu-id="a3130-106">The Network Watcher Agent virtual machine extension is a requirement for some of the Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="a3130-107">tra cui l'acquisizione del traffico di rete su richiesta e altre funzionalità avanzate.</span><span class="sxs-lookup"><span data-stu-id="a3130-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="a3130-108">Questo documento descrive in dettaglio le piattaforme e le opzioni di distribuzione supportate per l'estensione macchina virtuale Network Watcher Agent per Linux.</span><span class="sxs-lookup"><span data-stu-id="a3130-108">This document details the supported platforms and deployment options for the Network Watcher Agent virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3130-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a3130-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="a3130-110">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="a3130-110">Operating system</span></span>

<span data-ttu-id="a3130-111">L'estensione Network Watcher Agent può essere eseguita per le distribuzioni di Linux seguenti:</span><span class="sxs-lookup"><span data-stu-id="a3130-111">The Network Watcher Agent extension can be run against these Linux distributions:</span></span>

| <span data-ttu-id="a3130-112">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="a3130-112">Distribution</span></span> | <span data-ttu-id="a3130-113">Versione</span><span class="sxs-lookup"><span data-stu-id="a3130-113">Version</span></span> |
|---|---|
| <span data-ttu-id="a3130-114">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a3130-114">Ubuntu</span></span> | <span data-ttu-id="a3130-115">16.04 LTS, 14.04 LTS e 12.04 LTS</span><span class="sxs-lookup"><span data-stu-id="a3130-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span></span> |
| <span data-ttu-id="a3130-116">Debian</span><span class="sxs-lookup"><span data-stu-id="a3130-116">Debian</span></span> | <span data-ttu-id="a3130-117">7 e 8</span><span class="sxs-lookup"><span data-stu-id="a3130-117">7 and 8</span></span> |
| <span data-ttu-id="a3130-118">RedHat</span><span class="sxs-lookup"><span data-stu-id="a3130-118">RedHat</span></span> | <span data-ttu-id="a3130-119">6.x e 7.x</span><span class="sxs-lookup"><span data-stu-id="a3130-119">6.x and 7.x</span></span> |
| <span data-ttu-id="a3130-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="a3130-120">Oracle Linux</span></span> | <span data-ttu-id="a3130-121">7x</span><span class="sxs-lookup"><span data-stu-id="a3130-121">7x</span></span> |
| <span data-ttu-id="a3130-122">SUSE</span><span class="sxs-lookup"><span data-stu-id="a3130-122">Suse</span></span> | <span data-ttu-id="a3130-123">11 e 12</span><span class="sxs-lookup"><span data-stu-id="a3130-123">11 and 12</span></span> |
| <span data-ttu-id="a3130-124">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="a3130-124">OpenSuse</span></span> | <span data-ttu-id="a3130-125">7.0</span><span class="sxs-lookup"><span data-stu-id="a3130-125">7.0</span></span> |
| <span data-ttu-id="a3130-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="a3130-126">CentOS</span></span> | <span data-ttu-id="a3130-127">7.0</span><span class="sxs-lookup"><span data-stu-id="a3130-127">7.0</span></span> |

<span data-ttu-id="a3130-128">Si noti che CoreOS non è attualmente supportato.</span><span class="sxs-lookup"><span data-stu-id="a3130-128">Note that CoreOS is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="a3130-129">Connettività Internet</span><span class="sxs-lookup"><span data-stu-id="a3130-129">Internet connectivity</span></span>

<span data-ttu-id="a3130-130">Alcune delle funzionalità di Network Watcher Agent richiedono che la macchina virtuale di destinazione sia connessa a Internet.</span><span class="sxs-lookup"><span data-stu-id="a3130-130">Some of the Network Watcher Agent functionality requires that the target virtual machine be connected to the Internet.</span></span> <span data-ttu-id="a3130-131">Se non vi è la possibilità di stabilire connessioni in uscita, alcune funzionalità di Network Watcher Agent potrebbero non funzionare correttamente o non essere disponibili.</span><span class="sxs-lookup"><span data-stu-id="a3130-131">Without the ability to establish outgoing connections some of the Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="a3130-132">Per maggiori dettagli, vedere la [documentazione di Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span><span class="sxs-lookup"><span data-stu-id="a3130-132">For more details, please see the [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="a3130-133">Schema dell'estensione</span><span class="sxs-lookup"><span data-stu-id="a3130-133">Extension schema</span></span>

<span data-ttu-id="a3130-134">Lo schema JSON seguente illustra lo schema dell'estensione Network Watcher Agent.</span><span class="sxs-lookup"><span data-stu-id="a3130-134">The following JSON shows the schema for the Network Watcher Agent extension.</span></span> <span data-ttu-id="a3130-135">Al momento, l'estensione non richiede né supporta impostazioni fornite dall'utente e si basa sulla configurazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="a3130-135">The extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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
        "type": "NetworkWatcherAgentLinux",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="a3130-136">Valori delle proprietà</span><span class="sxs-lookup"><span data-stu-id="a3130-136">Property values</span></span>

| <span data-ttu-id="a3130-137">Nome</span><span class="sxs-lookup"><span data-stu-id="a3130-137">Name</span></span> | <span data-ttu-id="a3130-138">Valore/Esempio</span><span class="sxs-lookup"><span data-stu-id="a3130-138">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="a3130-139">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a3130-139">apiVersion</span></span> | <span data-ttu-id="a3130-140">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="a3130-140">2015-06-15</span></span> |
| <span data-ttu-id="a3130-141">publisher</span><span class="sxs-lookup"><span data-stu-id="a3130-141">publisher</span></span> | <span data-ttu-id="a3130-142">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="a3130-142">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="a3130-143">type</span><span class="sxs-lookup"><span data-stu-id="a3130-143">type</span></span> | <span data-ttu-id="a3130-144">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="a3130-144">NetworkWatcherAgentLinux</span></span> |
| <span data-ttu-id="a3130-145">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="a3130-145">typeHandlerVersion</span></span> | <span data-ttu-id="a3130-146">1.4</span><span class="sxs-lookup"><span data-stu-id="a3130-146">1.4</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="a3130-147">Distribuzione del modello</span><span class="sxs-lookup"><span data-stu-id="a3130-147">Template deployment</span></span>

<span data-ttu-id="a3130-148">Le estensioni macchina virtuale di Azure possono essere distribuite con i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a3130-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="a3130-149">Lo schema JSON descritto in dettaglio nella sezione precedente può essere usato in un modello di Azure Resource Manager per eseguire l'estensione Network Watcher Agent durante la distribuzione di un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a3130-149">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="azure-cli-deployment"></a><span data-ttu-id="a3130-150">Distribuzione dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a3130-150">Azure CLI deployment</span></span>

<span data-ttu-id="a3130-151">L'interfaccia della riga di comando di Azure può essere usata per distribuire l'estensione macchina virtuale Network Watcher Agent in una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="a3130-151">The Azure CLI can be used to deploy the Network Watcher Agent VM extension to an existing virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="a3130-152">Risoluzione dei problemi e supporto</span><span class="sxs-lookup"><span data-stu-id="a3130-152">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="a3130-153">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="a3130-153">Troubleshooting</span></span>

<span data-ttu-id="a3130-154">I dati sullo stato delle distribuzioni dell'estensione possono essere recuperati nel portale di Azure e tramite l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3130-154">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure CLI.</span></span> <span data-ttu-id="a3130-155">Per visualizzare lo stato di distribuzione delle estensioni per una determinata macchina virtuale, eseguire il comando seguente nell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3130-155">To see the deployment state of extensions for a given VM, run the following command using the Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

<span data-ttu-id="a3130-156">L'output dell'esecuzione dell'estensione viene registrato nei file presenti nella directory seguente:</span><span class="sxs-lookup"><span data-stu-id="a3130-156">Extension execution output is logged to files found in the following directory:</span></span>

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a><span data-ttu-id="a3130-157">Supporto</span><span class="sxs-lookup"><span data-stu-id="a3130-157">Support</span></span>

<span data-ttu-id="a3130-158">Per ricevere assistenza più approfondita su qualsiasi punto dell'articolo, fare riferimento alla documentazione su Network Watcher o contattare gli esperti di Azure nei [forum di Azure su MSDN e Stack Overflow](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="a3130-158">If you need more help at any point in this article, you can refer to the Network Watcher documentation or contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="a3130-159">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3130-159">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="a3130-160">Accedere al [sito del supporto di Azure](https://azure.microsoft.com/en-us/support/options/) e selezionare l'opzione desiderata per ottenere supporto.</span><span class="sxs-lookup"><span data-stu-id="a3130-160">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="a3130-161">Per informazioni sull'uso del supporto di Azure, leggere le [Domande frequenti sul supporto di Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="a3130-161">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>

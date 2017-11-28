---
title: estensione dell'agente di controllo di rete della macchina virtuale per Linux aaaAzure | Documenti Microsoft
description: Distribuire hello agente di controllo di rete nella macchina virtuale di Linux mediante un'estensione di macchina virtuale.
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
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a><span data-ttu-id="7d48d-103">Estensione macchina virtuale Network Watcher Agent per Linux</span><span class="sxs-lookup"><span data-stu-id="7d48d-103">Network Watcher Agent virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="7d48d-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7d48d-104">Overview</span></span>

<span data-ttu-id="7d48d-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) è un servizio di monitoraggio delle prestazioni di rete, diagnostica e analisi che consente di monitorare le reti di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d48d-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="7d48d-106">Hello estensione della macchina virtuale dell'agente di controllo di rete è un requisito per alcune delle funzionalità di hello Watcher di rete in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d48d-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="7d48d-107">Include l'acquisizione del traffico di rete su richiesta e altre funzionalità avanzate.</span><span class="sxs-lookup"><span data-stu-id="7d48d-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="7d48d-108">Per Linux, hello di dettagli in questo documento supporta piattaforme e le opzioni di distribuzione per hello estensione della macchina virtuale dell'agente di controllo di rete.</span><span class="sxs-lookup"><span data-stu-id="7d48d-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d48d-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7d48d-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="7d48d-110">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="7d48d-110">Operating system</span></span>

<span data-ttu-id="7d48d-111">Hello estensione Agent Watcher di rete può essere eseguita su queste distribuzioni Linux:</span><span class="sxs-lookup"><span data-stu-id="7d48d-111">hello Network Watcher Agent extension can be run against these Linux distributions:</span></span>

| <span data-ttu-id="7d48d-112">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="7d48d-112">Distribution</span></span> | <span data-ttu-id="7d48d-113">Versione</span><span class="sxs-lookup"><span data-stu-id="7d48d-113">Version</span></span> |
|---|---|
| <span data-ttu-id="7d48d-114">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="7d48d-114">Ubuntu</span></span> | <span data-ttu-id="7d48d-115">16.04 LTS, 14.04 LTS e 12.04 LTS</span><span class="sxs-lookup"><span data-stu-id="7d48d-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span></span> |
| <span data-ttu-id="7d48d-116">Debian</span><span class="sxs-lookup"><span data-stu-id="7d48d-116">Debian</span></span> | <span data-ttu-id="7d48d-117">7 e 8</span><span class="sxs-lookup"><span data-stu-id="7d48d-117">7 and 8</span></span> |
| <span data-ttu-id="7d48d-118">RedHat</span><span class="sxs-lookup"><span data-stu-id="7d48d-118">RedHat</span></span> | <span data-ttu-id="7d48d-119">6.x e 7.x</span><span class="sxs-lookup"><span data-stu-id="7d48d-119">6.x and 7.x</span></span> |
| <span data-ttu-id="7d48d-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="7d48d-120">Oracle Linux</span></span> | <span data-ttu-id="7d48d-121">7x</span><span class="sxs-lookup"><span data-stu-id="7d48d-121">7x</span></span> |
| <span data-ttu-id="7d48d-122">SUSE</span><span class="sxs-lookup"><span data-stu-id="7d48d-122">Suse</span></span> | <span data-ttu-id="7d48d-123">11 e 12</span><span class="sxs-lookup"><span data-stu-id="7d48d-123">11 and 12</span></span> |
| <span data-ttu-id="7d48d-124">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="7d48d-124">OpenSuse</span></span> | <span data-ttu-id="7d48d-125">7.0</span><span class="sxs-lookup"><span data-stu-id="7d48d-125">7.0</span></span> |
| <span data-ttu-id="7d48d-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="7d48d-126">CentOS</span></span> | <span data-ttu-id="7d48d-127">7.0</span><span class="sxs-lookup"><span data-stu-id="7d48d-127">7.0</span></span> |

<span data-ttu-id="7d48d-128">Si noti che CoreOS non è attualmente supportato.</span><span class="sxs-lookup"><span data-stu-id="7d48d-128">Note that CoreOS is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="7d48d-129">Connettività Internet</span><span class="sxs-lookup"><span data-stu-id="7d48d-129">Internet connectivity</span></span>

<span data-ttu-id="7d48d-130">Alcune delle funzionalità dell'agente di controllo rete hello richiede tale macchina virtuale di destinazione hello connesso toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="7d48d-130">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="7d48d-131">Senza connessioni in uscita di hello possibilità tooestablish alcune delle funzionalità dell'agente di controllo rete hello malfunzionamento o non sono più disponibili.</span><span class="sxs-lookup"><span data-stu-id="7d48d-131">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="7d48d-132">Per ulteriori informazioni, vedere hello [documentazione Watcher di rete](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span><span class="sxs-lookup"><span data-stu-id="7d48d-132">For more details, please see hello [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="7d48d-133">Schema dell'estensione</span><span class="sxs-lookup"><span data-stu-id="7d48d-133">Extension schema</span></span>

<span data-ttu-id="7d48d-134">Hello JSON seguente mostra lo schema di hello per hello estensione Agent Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="7d48d-134">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="7d48d-135">estensione di Hello non richiede né supporta le impostazioni fornite dall'utente in questo momento e si basa sulla configurazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="7d48d-135">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="7d48d-136">Valori delle proprietà</span><span class="sxs-lookup"><span data-stu-id="7d48d-136">Property values</span></span>

| <span data-ttu-id="7d48d-137">Nome</span><span class="sxs-lookup"><span data-stu-id="7d48d-137">Name</span></span> | <span data-ttu-id="7d48d-138">Valore/Esempio</span><span class="sxs-lookup"><span data-stu-id="7d48d-138">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="7d48d-139">apiVersion</span><span class="sxs-lookup"><span data-stu-id="7d48d-139">apiVersion</span></span> | <span data-ttu-id="7d48d-140">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="7d48d-140">2015-06-15</span></span> |
| <span data-ttu-id="7d48d-141">publisher</span><span class="sxs-lookup"><span data-stu-id="7d48d-141">publisher</span></span> | <span data-ttu-id="7d48d-142">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="7d48d-142">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="7d48d-143">type</span><span class="sxs-lookup"><span data-stu-id="7d48d-143">type</span></span> | <span data-ttu-id="7d48d-144">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="7d48d-144">NetworkWatcherAgentLinux</span></span> |
| <span data-ttu-id="7d48d-145">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="7d48d-145">typeHandlerVersion</span></span> | <span data-ttu-id="7d48d-146">1.4</span><span class="sxs-lookup"><span data-stu-id="7d48d-146">1.4</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="7d48d-147">Distribuzione del modello</span><span class="sxs-lookup"><span data-stu-id="7d48d-147">Template deployment</span></span>

<span data-ttu-id="7d48d-148">Le estensioni macchina virtuale di Azure possono essere distribuite con i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7d48d-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="7d48d-149">schema JSON Hello descritta in dettaglio nella sezione precedente hello è utilizzabile in un hello toorun modello di gestione risorse di Azure estensione Agent Watcher di rete durante la distribuzione di un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d48d-149">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="azure-cli-deployment"></a><span data-ttu-id="7d48d-150">Distribuzione dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="7d48d-150">Azure CLI deployment</span></span>

<span data-ttu-id="7d48d-151">Hello CLI di Azure può essere utilizzato toodeploy hello rete Watcher agente VM estensione tooan macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="7d48d-151">hello Azure CLI can be used toodeploy hello Network Watcher Agent VM extension tooan existing virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="7d48d-152">Risoluzione dei problemi e supporto</span><span class="sxs-lookup"><span data-stu-id="7d48d-152">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="7d48d-153">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="7d48d-153">Troubleshooting</span></span>

<span data-ttu-id="7d48d-154">Dati sullo stato di hello delle distribuzioni di estensione possono essere recuperati dal portale di Azure hello e, utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d48d-154">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="7d48d-155">lo stato di distribuzione hello toosee delle estensioni per una macchina virtuale specificata, eseguire hello seguente comando utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d48d-155">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

<span data-ttu-id="7d48d-156">Esecuzione di estensione di output è toofiles registrati nell'hello seguente directory:</span><span class="sxs-lookup"><span data-stu-id="7d48d-156">Extension execution output is logged toofiles found in hello following directory:</span></span>

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a><span data-ttu-id="7d48d-157">Supporto</span><span class="sxs-lookup"><span data-stu-id="7d48d-157">Support</span></span>

<span data-ttu-id="7d48d-158">Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile consultare la documentazione di toohello Watcher di rete o contattare hello Azure esperti hello [forum MSDN di Azure e di Overflow dello Stack](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="7d48d-158">If you need more help at any point in this article, you can refer toohello Network Watcher documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="7d48d-159">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d48d-159">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="7d48d-160">Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/en-us/support/options/) e scegliere supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="7d48d-160">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="7d48d-161">Per informazioni sull'utilizzo di supporto di Azure, leggere hello [supporto tecnico di Microsoft Azure domande frequenti su](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="7d48d-161">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>

---
title: Estensione macchina virtuale di Azure OMS per Linux | Documentazione Microsoft
description: Distribuire l'agente OMS in una macchina virtuale Linux usando un'estensione macchina virtuale.
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 138fc8c98ea6f409b28407b20851c96ecc618b09
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a><span data-ttu-id="41075-103">Estensione macchina virtuale OMS per Linux</span><span class="sxs-lookup"><span data-stu-id="41075-103">OMS virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="41075-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="41075-104">Overview</span></span>

<span data-ttu-id="41075-105">In Operations Management Suite (OMS) sono disponibili funzionalità di monitoraggio, avviso e correzione tramite avvisi in risorse cloud e locali.</span><span class="sxs-lookup"><span data-stu-id="41075-105">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="41075-106">L'estensione macchina virtuale Agente OMS per Linux è pubblicata e supportata da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="41075-106">The OMS Agent virtual machine extension for Linux is published and supported by Microsoft.</span></span> <span data-ttu-id="41075-107">L'estensione installa l'agente OMS in macchine virtuali di Azure e registra le macchine virtuali in un'area di lavoro OMS esistente.</span><span class="sxs-lookup"><span data-stu-id="41075-107">The extension installs the OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="41075-108">Questo documento descrive in dettaglio le piattaforme, le configurazioni e le opzioni di distribuzione supportate per l'estensione macchina virtuale OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="41075-108">This document details the supported platforms, configurations, and deployment options for the OMS virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41075-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="41075-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="41075-110">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="41075-110">Operating system</span></span>

<span data-ttu-id="41075-111">L'estensione agente OMS può essere eseguita in queste distribuzioni di Linux.</span><span class="sxs-lookup"><span data-stu-id="41075-111">The OMS Agent extension can be run against these Linux distributions.</span></span>

| <span data-ttu-id="41075-112">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="41075-112">Distribution</span></span> | <span data-ttu-id="41075-113">Versione</span><span class="sxs-lookup"><span data-stu-id="41075-113">Version</span></span> |
|---|---|
| <span data-ttu-id="41075-114">CentOS Linux</span><span class="sxs-lookup"><span data-stu-id="41075-114">CentOS Linux</span></span> | <span data-ttu-id="41075-115">5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="41075-115">5, 6, and 7</span></span> |
| <span data-ttu-id="41075-116">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="41075-116">Oracle Linux</span></span> | <span data-ttu-id="41075-117">5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="41075-117">5, 6, and 7</span></span> |
| <span data-ttu-id="41075-118">Red Hat Enterprise Linux Server</span><span class="sxs-lookup"><span data-stu-id="41075-118">Red Hat Enterprise Linux Server</span></span> | <span data-ttu-id="41075-119">5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="41075-119">5, 6 and 7</span></span> |
| <span data-ttu-id="41075-120">Debian GNU/Linux</span><span class="sxs-lookup"><span data-stu-id="41075-120">Debian GNU/Linux</span></span> | <span data-ttu-id="41075-121">6, 7 e 8</span><span class="sxs-lookup"><span data-stu-id="41075-121">6, 7, and 8</span></span> |
| <span data-ttu-id="41075-122">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="41075-122">Ubuntu</span></span> | <span data-ttu-id="41075-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="41075-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span></span> |
| <span data-ttu-id="41075-124">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="41075-124">SUSE Linux Enterprise Server</span></span> | <span data-ttu-id="41075-125">11 e 12</span><span class="sxs-lookup"><span data-stu-id="41075-125">11 and 12</span></span> |

### <a name="internet-connectivity"></a><span data-ttu-id="41075-126">Connettività Internet</span><span class="sxs-lookup"><span data-stu-id="41075-126">Internet connectivity</span></span>

<span data-ttu-id="41075-127">Per distribuire l'estensione agente OMS per Linux, è necessario che la macchina virtuale di destinazione sia connessa a Internet.</span><span class="sxs-lookup"><span data-stu-id="41075-127">The OMS Agent extension for Linux requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="41075-128">Schema dell'estensione</span><span class="sxs-lookup"><span data-stu-id="41075-128">Extension schema</span></span>

<span data-ttu-id="41075-129">Il codice JSON riportato di seguito mostra lo schema dell'estensione OMS Agent.</span><span class="sxs-lookup"><span data-stu-id="41075-129">The following JSON shows the schema for the OMS Agent extension.</span></span> <span data-ttu-id="41075-130">L'estensione richiede che siano indicati l'ID e la chiave dell'area di lavoro presenti nell'area di lavoro OMS di destinazione. Questi valori sono disponibili nel portale OMS.</span><span class="sxs-lookup"><span data-stu-id="41075-130">The extension requires the workspace ID and workspace key from the target OMS workspace; these values can be found in the OMS portal.</span></span> <span data-ttu-id="41075-131">Poiché la chiave dell'area di lavoro deve essere tratta come i dati sensibili, deve essere memorizzata in una configurazione protetta.</span><span class="sxs-lookup"><span data-stu-id="41075-131">Because the workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="41075-132">I dati della configurazione protetta dell'estensione macchina virtuale di Azure vengono crittografati, per essere poi decrittografati solo nella macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="41075-132">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span> <span data-ttu-id="41075-133">Tenere presente che **workspaceId** e **workspaceKey** distinguono tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="41075-133">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a><span data-ttu-id="41075-134">Valori delle proprietà</span><span class="sxs-lookup"><span data-stu-id="41075-134">Property values</span></span>

| <span data-ttu-id="41075-135">Nome</span><span class="sxs-lookup"><span data-stu-id="41075-135">Name</span></span> | <span data-ttu-id="41075-136">Valore/Esempio</span><span class="sxs-lookup"><span data-stu-id="41075-136">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="41075-137">apiVersion</span><span class="sxs-lookup"><span data-stu-id="41075-137">apiVersion</span></span> | <span data-ttu-id="41075-138">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="41075-138">2015-06-15</span></span> |
| <span data-ttu-id="41075-139">publisher</span><span class="sxs-lookup"><span data-stu-id="41075-139">publisher</span></span> | <span data-ttu-id="41075-140">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="41075-140">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="41075-141">type</span><span class="sxs-lookup"><span data-stu-id="41075-141">type</span></span> | <span data-ttu-id="41075-142">OmsAgentForLinux</span><span class="sxs-lookup"><span data-stu-id="41075-142">OmsAgentForLinux</span></span> |
| <span data-ttu-id="41075-143">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="41075-143">typeHandlerVersion</span></span> | <span data-ttu-id="41075-144">1.4</span><span class="sxs-lookup"><span data-stu-id="41075-144">1.4</span></span> |
| <span data-ttu-id="41075-145">workspaceId (esempio)</span><span class="sxs-lookup"><span data-stu-id="41075-145">workspaceId (e.g)</span></span> | <span data-ttu-id="41075-146">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="41075-146">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="41075-147">workspaceKey (esempio)</span><span class="sxs-lookup"><span data-stu-id="41075-147">workspaceKey (e.g)</span></span> | <span data-ttu-id="41075-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="41075-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="41075-149">Distribuzione del modello</span><span class="sxs-lookup"><span data-stu-id="41075-149">Template deployment</span></span>

<span data-ttu-id="41075-150">Le estensioni macchina virtuale di Azure possono essere distribuite con i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="41075-150">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="41075-151">I modelli rappresentano la scelta migliore quando si distribuiscono una o più macchine virtuali per cui è necessaria una configurazione post-distribuzione, ad esempio il caricamento in OMS.</span><span class="sxs-lookup"><span data-stu-id="41075-151">Templates are ideal when deploying one or more virtual machines that require post deployment configuration such as onboarding to OMS.</span></span> <span data-ttu-id="41075-152">Un esempio di modello di Resource Manager che include l'estensione macchina virtuale Agente OMS è disponibile nella [raccolta di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span><span class="sxs-lookup"><span data-stu-id="41075-152">A sample Resource Manager template that includes the OMS Agent VM extension can be found on the [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span></span> 

<span data-ttu-id="41075-153">La configurazione JSON per un'estensione macchina virtuale può essere annidata nella risorsa della macchina virtuale o posizionata nel livello radice o nel livello superiore di un modello JSON di Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="41075-153">The JSON configuration for a virtual machine extension can be nested inside the virtual machine resource, or placed at the root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="41075-154">Il posizionamento della configurazione JSON influisce sul valore del nome e del tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="41075-154">The placement of the JSON configuration affects the value of the resource name and type.</span></span> <span data-ttu-id="41075-155">Per altre informazioni, vedere [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md) (Impostare il nome e il tipo per le risorse figlio).</span><span class="sxs-lookup"><span data-stu-id="41075-155">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="41075-156">L'esempio seguente presuppone che l'estensione OMS sia annidata all'interno della risorsa della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="41075-156">The following example assumes the OMS extension is nested inside the virtual machine resource.</span></span> <span data-ttu-id="41075-157">Quando la risorsa di estensione viene nidificata, JSON viene inserito nell'oggetto `"resources": []` della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="41075-157">When nesting the extension resource, the JSON is placed in the `"resources": []` object of the virtual machine.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

<span data-ttu-id="41075-158">Quando si posiziona l'estensione JSON nella radice del modello, il nome della risorsa include un riferimento alla macchina virtuale padre e il tipo riflette la configurazione annidata.</span><span class="sxs-lookup"><span data-stu-id="41075-158">When placing the extension JSON at the root of the template, the resource name includes a reference to the parent virtual machine, and the type reflects the nested configuration.</span></span>  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a><span data-ttu-id="41075-159">Distribuzione dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="41075-159">Azure CLI deployment</span></span>

<span data-ttu-id="41075-160">L'interfaccia della riga di comando di Azure può essere usata per distribuire l'estensione macchina virtuale Agente OMS in una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="41075-160">The Azure CLI can be used to deploy the OMS Agent VM extension to an existing virtual machine.</span></span> <span data-ttu-id="41075-161">Sostituire la chiave OMS e l'ID OMS con i dati presenti nello spazio di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="41075-161">Replace the OMS key and OMS ID with those from your OMS workspace.</span></span> 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="41075-162">Risoluzione dei problemi e supporto</span><span class="sxs-lookup"><span data-stu-id="41075-162">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="41075-163">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="41075-163">Troubleshoot</span></span>

<span data-ttu-id="41075-164">I dati sullo stato delle distribuzioni dell'estensione possono essere recuperati nel portale di Azure e tramite l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="41075-164">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure CLI.</span></span> <span data-ttu-id="41075-165">Per visualizzare lo stato di distribuzione delle estensioni per una determinata VM, eseguire il comando seguente nell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="41075-165">To see the deployment state of extensions for a given VM, run the following command using the Azure CLI.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="41075-166">L'output dell'esecuzione dell'estensione viene registrato nel file seguente:</span><span class="sxs-lookup"><span data-stu-id="41075-166">Extension execution output is logged to the following file:</span></span>

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a><span data-ttu-id="41075-167">Codici di errore e relativi significati</span><span class="sxs-lookup"><span data-stu-id="41075-167">Error codes and their meanings</span></span>

| <span data-ttu-id="41075-168">Codice di errore</span><span class="sxs-lookup"><span data-stu-id="41075-168">Error Code</span></span> | <span data-ttu-id="41075-169">Significato</span><span class="sxs-lookup"><span data-stu-id="41075-169">Meaning</span></span> | <span data-ttu-id="41075-170">Azione possibile</span><span class="sxs-lookup"><span data-stu-id="41075-170">Possible Action</span></span> |
| :---: | --- | --- |
| <span data-ttu-id="41075-171">10</span><span class="sxs-lookup"><span data-stu-id="41075-171">10</span></span> | <span data-ttu-id="41075-172">La macchina virtuale è già connessa a un'area di lavoro OMS</span><span class="sxs-lookup"><span data-stu-id="41075-172">VM is already connected to an OMS workspace</span></span> | <span data-ttu-id="41075-173">Per connettere la macchina virtuale all'area di lavoro specificata nello schema dell'estensione, impostare stopOnMultipleConnections su false nelle impostazioni pubbliche o rimuovere questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="41075-173">To connect the VM to the workspace specified in the extension schema, set stopOnMultipleConnections to false in public settings or remove this property.</span></span> <span data-ttu-id="41075-174">Questa macchina virtuale viene fatturata una volta per ogni area di lavoro a cui è connessa.</span><span class="sxs-lookup"><span data-stu-id="41075-174">This VM gets billed once for each workspace it is connected to.</span></span> |
| <span data-ttu-id="41075-175">11</span><span class="sxs-lookup"><span data-stu-id="41075-175">11</span></span> | <span data-ttu-id="41075-176">Configurazione non valida generata per l'estensione</span><span class="sxs-lookup"><span data-stu-id="41075-176">Invalid config provided to the extension</span></span> | <span data-ttu-id="41075-177">Seguire l'esempio precedente per impostare tutti i valori della proprietà necessari alla distribuzione.</span><span class="sxs-lookup"><span data-stu-id="41075-177">Follow the preceding examples to set all property values necessary for deployment.</span></span> |
| <span data-ttu-id="41075-178">12</span><span class="sxs-lookup"><span data-stu-id="41075-178">12</span></span> | <span data-ttu-id="41075-179">La gestione di pacchetti dpkg è bloccata</span><span class="sxs-lookup"><span data-stu-id="41075-179">The dpkg package manager is locked</span></span> | <span data-ttu-id="41075-180">Assicurarsi che tutte le operazioni di aggiornamento dpkg sul computer siano state completate e riprovare.</span><span class="sxs-lookup"><span data-stu-id="41075-180">Make sure all dpkg update operations on the machine have finished and retry.</span></span> |
| <span data-ttu-id="41075-181">20</span><span class="sxs-lookup"><span data-stu-id="41075-181">20</span></span> | <span data-ttu-id="41075-182">Chiamata Enable anomala</span><span class="sxs-lookup"><span data-stu-id="41075-182">Enable called prematurely</span></span> | <span data-ttu-id="41075-183">[Aggiornare l'agente Linux di Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) all'ultima versione disponibile.</span><span class="sxs-lookup"><span data-stu-id="41075-183">[Update the Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) to the latest available version.</span></span> |
| <span data-ttu-id="41075-184">51</span><span class="sxs-lookup"><span data-stu-id="41075-184">51</span></span> | <span data-ttu-id="41075-185">Questa estensione non è supportata sul sistema operativo della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="41075-185">This extension is not supported on the VM's operation system</span></span> | |
| <span data-ttu-id="41075-186">55</span><span class="sxs-lookup"><span data-stu-id="41075-186">55</span></span> | <span data-ttu-id="41075-187">Non è possibile connettersi al servizio Microsoft Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="41075-187">Cannot connect to the Microsoft Operations Management Suite service</span></span> | <span data-ttu-id="41075-188">Verificare che il sistema disponga dell'accesso a Internet o che sia stato fornito un proxy HTTP valido.</span><span class="sxs-lookup"><span data-stu-id="41075-188">Check that the system either has Internet access, or that a valid HTTP proxy has been provided.</span></span> <span data-ttu-id="41075-189">Verificare anche la correttezza dell'ID dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="41075-189">Additionally, check the correctness of the workspace ID.</span></span> |

<span data-ttu-id="41075-190">Altre informazioni sulla risoluzione dei problemi possono essere consultate nella [Guida alla risoluzione dei problemi per l'agente OMS per Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span><span class="sxs-lookup"><span data-stu-id="41075-190">Additional troubleshooting information can be found on the [OMS-Agent-for-Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span></span>

### <a name="support"></a><span data-ttu-id="41075-191">Supporto</span><span class="sxs-lookup"><span data-stu-id="41075-191">Support</span></span>

<span data-ttu-id="41075-192">Per ricevere assistenza in relazione a qualsiasi punto di questo articolo, contattare gli esperti di Azure nei [forum MSDN e Stack Overflow relativi ad Azure](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="41075-192">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="41075-193">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="41075-193">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="41075-194">Accedere al [sito del supporto di Azure](https://azure.microsoft.com/en-us/support/options/) e selezionare l'opzione desiderata per ottenere supporto.</span><span class="sxs-lookup"><span data-stu-id="41075-194">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="41075-195">Per informazioni sull'uso del supporto di Azure, leggere le [Domande frequenti sul supporto di Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="41075-195">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>

---
title: estensione di macchina virtuale di Azure per Linux aaaOMS | Documenti Microsoft
description: Distribuire l'agente OMS hello nella macchina virtuale di Linux mediante un'estensione di macchina virtuale.
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
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a><span data-ttu-id="73cd4-103">Estensione macchina virtuale OMS per Linux</span><span class="sxs-lookup"><span data-stu-id="73cd4-103">OMS virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="73cd4-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="73cd4-104">Overview</span></span>

<span data-ttu-id="73cd4-105">In Operations Management Suite (OMS) sono disponibili funzionalità di monitoraggio, avviso e correzione tramite avvisi in risorse cloud e locali.</span><span class="sxs-lookup"><span data-stu-id="73cd4-105">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="73cd4-106">Hello estensione della macchina virtuale agente OMS per Linux è pubblicato e supportato da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="73cd4-106">hello OMS Agent virtual machine extension for Linux is published and supported by Microsoft.</span></span> <span data-ttu-id="73cd4-107">estensione Hello installa l'agente OMS hello in macchine virtuali di Azure e registra le macchine virtuali in un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="73cd4-107">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="73cd4-108">Opzioni di distribuzione, le configurazioni e piattaforme hello di dettagli in questo documento supportato per hello estensione della macchina virtuale OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="73cd4-108">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73cd4-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="73cd4-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="73cd4-110">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="73cd4-110">Operating system</span></span>

<span data-ttu-id="73cd4-111">Hello estensione OMS Agent possa essere eseguita su queste distribuzioni di Linux.</span><span class="sxs-lookup"><span data-stu-id="73cd4-111">hello OMS Agent extension can be run against these Linux distributions.</span></span>

| <span data-ttu-id="73cd4-112">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="73cd4-112">Distribution</span></span> | <span data-ttu-id="73cd4-113">Versione</span><span class="sxs-lookup"><span data-stu-id="73cd4-113">Version</span></span> |
|---|---|
| <span data-ttu-id="73cd4-114">CentOS Linux</span><span class="sxs-lookup"><span data-stu-id="73cd4-114">CentOS Linux</span></span> | <span data-ttu-id="73cd4-115">5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="73cd4-115">5, 6, and 7</span></span> |
| <span data-ttu-id="73cd4-116">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="73cd4-116">Oracle Linux</span></span> | <span data-ttu-id="73cd4-117">5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="73cd4-117">5, 6, and 7</span></span> |
| <span data-ttu-id="73cd4-118">Red Hat Enterprise Linux Server</span><span class="sxs-lookup"><span data-stu-id="73cd4-118">Red Hat Enterprise Linux Server</span></span> | <span data-ttu-id="73cd4-119">5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="73cd4-119">5, 6 and 7</span></span> |
| <span data-ttu-id="73cd4-120">Debian GNU/Linux</span><span class="sxs-lookup"><span data-stu-id="73cd4-120">Debian GNU/Linux</span></span> | <span data-ttu-id="73cd4-121">6, 7 e 8</span><span class="sxs-lookup"><span data-stu-id="73cd4-121">6, 7, and 8</span></span> |
| <span data-ttu-id="73cd4-122">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="73cd4-122">Ubuntu</span></span> | <span data-ttu-id="73cd4-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="73cd4-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span></span> |
| <span data-ttu-id="73cd4-124">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="73cd4-124">SUSE Linux Enterprise Server</span></span> | <span data-ttu-id="73cd4-125">11 e 12</span><span class="sxs-lookup"><span data-stu-id="73cd4-125">11 and 12</span></span> |

### <a name="internet-connectivity"></a><span data-ttu-id="73cd4-126">Connettività Internet</span><span class="sxs-lookup"><span data-stu-id="73cd4-126">Internet connectivity</span></span>

<span data-ttu-id="73cd4-127">Hello estensione agente OMS per Linux richiede tale macchina virtuale di destinazione hello è connesso toohello internet.</span><span class="sxs-lookup"><span data-stu-id="73cd4-127">hello OMS Agent extension for Linux requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="73cd4-128">Schema dell'estensione</span><span class="sxs-lookup"><span data-stu-id="73cd4-128">Extension schema</span></span>

<span data-ttu-id="73cd4-129">Hello JSON seguente viene illustrato lo schema di hello per hello estensione OMS Agent.</span><span class="sxs-lookup"><span data-stu-id="73cd4-129">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="73cd4-130">estensione Hello richiede hello dell'area di lavoro area di lavoro e l'ID chiave dall'area di lavoro di hello destinazione OMS; Questi valori sono disponibili nel portale OMS hello.</span><span class="sxs-lookup"><span data-stu-id="73cd4-130">hello extension requires hello workspace ID and workspace key from hello target OMS workspace; these values can be found in hello OMS portal.</span></span> <span data-ttu-id="73cd4-131">Poiché chiave dell'area di lavoro hello deve essere considerate come dati sensibili, devono essere archiviato in una configurazione di impostazione protetto.</span><span class="sxs-lookup"><span data-stu-id="73cd4-131">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="73cd4-132">Dati impostazione protette dell'estensione di macchina virtuale di Azure sono crittografati e decrittografati solo nella macchina virtuale di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="73cd4-132">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="73cd4-133">Tenere presente che **workspaceId** e **workspaceKey** distinguono tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="73cd4-133">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="73cd4-134">Valori delle proprietà</span><span class="sxs-lookup"><span data-stu-id="73cd4-134">Property values</span></span>

| <span data-ttu-id="73cd4-135">Nome</span><span class="sxs-lookup"><span data-stu-id="73cd4-135">Name</span></span> | <span data-ttu-id="73cd4-136">Valore/Esempio</span><span class="sxs-lookup"><span data-stu-id="73cd4-136">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="73cd4-137">apiVersion</span><span class="sxs-lookup"><span data-stu-id="73cd4-137">apiVersion</span></span> | <span data-ttu-id="73cd4-138">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="73cd4-138">2015-06-15</span></span> |
| <span data-ttu-id="73cd4-139">publisher</span><span class="sxs-lookup"><span data-stu-id="73cd4-139">publisher</span></span> | <span data-ttu-id="73cd4-140">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="73cd4-140">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="73cd4-141">type</span><span class="sxs-lookup"><span data-stu-id="73cd4-141">type</span></span> | <span data-ttu-id="73cd4-142">OmsAgentForLinux</span><span class="sxs-lookup"><span data-stu-id="73cd4-142">OmsAgentForLinux</span></span> |
| <span data-ttu-id="73cd4-143">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="73cd4-143">typeHandlerVersion</span></span> | <span data-ttu-id="73cd4-144">1.4</span><span class="sxs-lookup"><span data-stu-id="73cd4-144">1.4</span></span> |
| <span data-ttu-id="73cd4-145">workspaceId (esempio)</span><span class="sxs-lookup"><span data-stu-id="73cd4-145">workspaceId (e.g)</span></span> | <span data-ttu-id="73cd4-146">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="73cd4-146">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="73cd4-147">workspaceKey (esempio)</span><span class="sxs-lookup"><span data-stu-id="73cd4-147">workspaceKey (e.g)</span></span> | <span data-ttu-id="73cd4-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="73cd4-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="73cd4-149">Distribuzione del modello</span><span class="sxs-lookup"><span data-stu-id="73cd4-149">Template deployment</span></span>

<span data-ttu-id="73cd4-150">Le estensioni macchina virtuale di Azure possono essere distribuite con i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="73cd4-150">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="73cd4-151">Modelli sono ideali per la distribuzione di uno o più macchine virtuali che richiedono la configurazione di distribuzione post, ad esempio tooOMS onboarding.</span><span class="sxs-lookup"><span data-stu-id="73cd4-151">Templates are ideal when deploying one or more virtual machines that require post deployment configuration such as onboarding tooOMS.</span></span> <span data-ttu-id="73cd4-152">Un modello di gestione risorse di esempio che include l'estensione della macchina virtuale di agente OMS hello è reperibile in hello [raccolta avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span><span class="sxs-lookup"><span data-stu-id="73cd4-152">A sample Resource Manager template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span></span> 

<span data-ttu-id="73cd4-153">configurazione JSON Hello per un'estensione della macchina virtuale può essere annidata all'interno di risorsa di macchina virtuale hello o posizionati nella radice di hello o un livello superiore di un modello di gestione risorse di JSON.</span><span class="sxs-lookup"><span data-stu-id="73cd4-153">hello JSON configuration for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="73cd4-154">posizionamento di Hello di configurazione JSON hello influisce sul valore di hello del nome della risorsa hello e tipo.</span><span class="sxs-lookup"><span data-stu-id="73cd4-154">hello placement of hello JSON configuration affects hello value of hello resource name and type.</span></span> <span data-ttu-id="73cd4-155">Per altre informazioni, vedere [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md) (Impostare il nome e il tipo per le risorse figlio).</span><span class="sxs-lookup"><span data-stu-id="73cd4-155">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="73cd4-156">Hello seguente si presuppone hello OMS estensione annidata all'interno di hello risorsa di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="73cd4-156">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="73cd4-157">Quando la nidificazione di risorse di estensione hello, hello JSON viene inserito nel hello `"resources": []` oggetto della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="73cd4-157">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>

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

<span data-ttu-id="73cd4-158">Quando si inseriscono estensione hello JSON nella radice di hello del modello di hello, il nome di risorsa hello include una macchina virtuale di riferimento toohello padre e il tipo hello riflette configurazione annidati hello.</span><span class="sxs-lookup"><span data-stu-id="73cd4-158">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span>  

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

## <a name="azure-cli-deployment"></a><span data-ttu-id="73cd4-159">Distribuzione dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="73cd4-159">Azure CLI deployment</span></span>

<span data-ttu-id="73cd4-160">Hello CLI di Azure può essere utilizzato toodeploy hello OMS agente VM estensione tooan macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="73cd4-160">hello Azure CLI can be used toodeploy hello OMS Agent VM extension tooan existing virtual machine.</span></span> <span data-ttu-id="73cd4-161">Sostituire chiave OMS hello e l'ID di OMS con quelle dell'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="73cd4-161">Replace hello OMS key and OMS ID with those from your OMS workspace.</span></span> 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="73cd4-162">Risoluzione dei problemi e supporto</span><span class="sxs-lookup"><span data-stu-id="73cd4-162">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="73cd4-163">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="73cd4-163">Troubleshoot</span></span>

<span data-ttu-id="73cd4-164">Dati sullo stato di hello delle distribuzioni di estensione possono essere recuperati dal portale di Azure hello e, utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="73cd4-164">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="73cd4-165">lo stato di distribuzione hello toosee delle estensioni per una macchina virtuale specificata, eseguire hello seguente comando utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="73cd4-165">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="73cd4-166">Esecuzione di estensione di output è connesso toohello seguenti file:</span><span class="sxs-lookup"><span data-stu-id="73cd4-166">Extension execution output is logged toohello following file:</span></span>

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a><span data-ttu-id="73cd4-167">Codici di errore e relativi significati</span><span class="sxs-lookup"><span data-stu-id="73cd4-167">Error codes and their meanings</span></span>

| <span data-ttu-id="73cd4-168">Codice di errore</span><span class="sxs-lookup"><span data-stu-id="73cd4-168">Error Code</span></span> | <span data-ttu-id="73cd4-169">Significato</span><span class="sxs-lookup"><span data-stu-id="73cd4-169">Meaning</span></span> | <span data-ttu-id="73cd4-170">Azione possibile</span><span class="sxs-lookup"><span data-stu-id="73cd4-170">Possible Action</span></span> |
| :---: | --- | --- |
| <span data-ttu-id="73cd4-171">10</span><span class="sxs-lookup"><span data-stu-id="73cd4-171">10</span></span> | <span data-ttu-id="73cd4-172">Macchina virtuale è già connesso tooan area di lavoro OMS</span><span class="sxs-lookup"><span data-stu-id="73cd4-172">VM is already connected tooan OMS workspace</span></span> | <span data-ttu-id="73cd4-173">tooconnect hello VM toohello dell'area di lavoro specificata nello schema di estensione hello, impostare stopOnMultipleConnections toofalse nelle impostazioni pubbliche o rimuovere la proprietà.</span><span class="sxs-lookup"><span data-stu-id="73cd4-173">tooconnect hello VM toohello workspace specified in hello extension schema, set stopOnMultipleConnections toofalse in public settings or remove this property.</span></span> <span data-ttu-id="73cd4-174">Questa macchina virtuale viene fatturata una volta per ogni area di lavoro a cui è connessa.</span><span class="sxs-lookup"><span data-stu-id="73cd4-174">This VM gets billed once for each workspace it is connected to.</span></span> |
| <span data-ttu-id="73cd4-175">11</span><span class="sxs-lookup"><span data-stu-id="73cd4-175">11</span></span> | <span data-ttu-id="73cd4-176">Configurazione non valido fornito toohello estensione</span><span class="sxs-lookup"><span data-stu-id="73cd4-176">Invalid config provided toohello extension</span></span> | <span data-ttu-id="73cd4-177">Seguire hello precedenti esempi tooset tutti i valori delle proprietà necessari per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="73cd4-177">Follow hello preceding examples tooset all property values necessary for deployment.</span></span> |
| <span data-ttu-id="73cd4-178">12</span><span class="sxs-lookup"><span data-stu-id="73cd4-178">12</span></span> | <span data-ttu-id="73cd4-179">gestione di pacchetti Hello dpkg è bloccato</span><span class="sxs-lookup"><span data-stu-id="73cd4-179">hello dpkg package manager is locked</span></span> | <span data-ttu-id="73cd4-180">Assicurarsi che tutte le operazioni di aggiornamento dpkg computer hello è stata completata e riprovare.</span><span class="sxs-lookup"><span data-stu-id="73cd4-180">Make sure all dpkg update operations on hello machine have finished and retry.</span></span> |
| <span data-ttu-id="73cd4-181">20</span><span class="sxs-lookup"><span data-stu-id="73cd4-181">20</span></span> | <span data-ttu-id="73cd4-182">Chiamata Enable anomala</span><span class="sxs-lookup"><span data-stu-id="73cd4-182">Enable called prematurely</span></span> | <span data-ttu-id="73cd4-183">[Hello aggiornamento agente Linux di Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello versione più recente disponibile.</span><span class="sxs-lookup"><span data-stu-id="73cd4-183">[Update hello Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello latest available version.</span></span> |
| <span data-ttu-id="73cd4-184">51</span><span class="sxs-lookup"><span data-stu-id="73cd4-184">51</span></span> | <span data-ttu-id="73cd4-185">Questa estensione non è supportata nel sistema operativo della macchina virtuale di hello</span><span class="sxs-lookup"><span data-stu-id="73cd4-185">This extension is not supported on hello VM's operation system</span></span> | |
| <span data-ttu-id="73cd4-186">55</span><span class="sxs-lookup"><span data-stu-id="73cd4-186">55</span></span> | <span data-ttu-id="73cd4-187">Non è possibile connettere il servizio di Microsoft Operations Management Suite toohello</span><span class="sxs-lookup"><span data-stu-id="73cd4-187">Cannot connect toohello Microsoft Operations Management Suite service</span></span> | <span data-ttu-id="73cd4-188">Verificare che il sistema hello disponga dell'accesso a Internet o che è stato fornito un proxy HTTP valido.</span><span class="sxs-lookup"><span data-stu-id="73cd4-188">Check that hello system either has Internet access, or that a valid HTTP proxy has been provided.</span></span> <span data-ttu-id="73cd4-189">Inoltre, controllare correttezza hello dell'ID dell'area di lavoro di hello.</span><span class="sxs-lookup"><span data-stu-id="73cd4-189">Additionally, check hello correctness of hello workspace ID.</span></span> |

<span data-ttu-id="73cd4-190">Ulteriori informazioni sulla risoluzione dei problemi possono trovarsi in hello [agente OMS per Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span><span class="sxs-lookup"><span data-stu-id="73cd4-190">Additional troubleshooting information can be found on hello [OMS-Agent-for-Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span></span>

### <a name="support"></a><span data-ttu-id="73cd4-191">Supporto</span><span class="sxs-lookup"><span data-stu-id="73cd4-191">Support</span></span>

<span data-ttu-id="73cd4-192">Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti hello [forum MSDN di Azure e di Overflow dello Stack](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="73cd4-192">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="73cd4-193">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="73cd4-193">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="73cd4-194">Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/en-us/support/options/) e scegliere supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="73cd4-194">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="73cd4-195">Per informazioni sull'utilizzo di supporto di Azure, leggere hello [supporto tecnico di Microsoft Azure domande frequenti su](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="73cd4-195">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>

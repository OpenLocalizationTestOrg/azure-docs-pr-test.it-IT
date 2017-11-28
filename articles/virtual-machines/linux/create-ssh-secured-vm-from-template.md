---
title: aaaCreate una VM Linux di Azure da un modello | Documenti Microsoft
description: Come toouse hello Azure CLI 2.0 toocreate una VM Linux da un modello di gestione risorse
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a><span data-ttu-id="15920-103">Come toocreate una macchina virtuale Linux con modelli di gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="15920-103">How toocreate a Linux virtual machine with Azure Resource Manager templates</span></span>
<span data-ttu-id="15920-104">Questo articolo illustra come tooquickly distribuire una macchina virtuale Linux (VM) con i modelli di gestione risorse di Azure e hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="15920-104">This article shows you how tooquickly deploy a Linux virtual machine (VM) with Azure Resource Manager templates and hello Azure CLI 2.0.</span></span> <span data-ttu-id="15920-105">È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="15920-105">You can also perform these steps with hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span></span>


## <a name="templates-overview"></a><span data-ttu-id="15920-106">Panoramica dei modelli</span><span class="sxs-lookup"><span data-stu-id="15920-106">Templates overview</span></span>
<span data-ttu-id="15920-107">Modelli di gestione risorse di Azure sono i file JSON che definiscono l'infrastruttura di hello e configurazione della soluzione Azure.</span><span class="sxs-lookup"><span data-stu-id="15920-107">Azure Resource Manager templates are JSON files that define hello infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="15920-108">Usando il modello è possibile distribuire ripetutamente la soluzione nel corso del ciclo di vita garantendo al contempo che le risorse vengano distribuite in uno stato coerente.</span><span class="sxs-lookup"><span data-stu-id="15920-108">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="15920-109">toolearn ulteriori informazioni sui formati di hello del modello hello e come creare l'oggetto, vedere [creare il primo modello di gestione risorse di Azure](../../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="15920-109">toolearn more about hello format of hello template and how you construct it, see [Create your first Azure Resource Manager template](../../azure-resource-manager/resource-manager-create-first-template.md).</span></span> <span data-ttu-id="15920-110">hello tooview sintassi JSON per i tipi di risorse, vedere [definire le risorse nei modelli di Azure Resource Manager](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="15920-110">tooview hello JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>


## <a name="create-resource-group"></a><span data-ttu-id="15920-111">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="15920-111">Create resource group</span></span>
<span data-ttu-id="15920-112">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="15920-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="15920-113">Il gruppo di risorse deve essere creato prima della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="15920-113">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="15920-114">esempio Hello crea un gruppo di risorse denominato *myResourceGroupVM* in hello *eastus* area:</span><span class="sxs-lookup"><span data-stu-id="15920-114">hello following example creates a resource group named *myResourceGroupVM* in hello *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="15920-115">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="15920-115">Create virtual machine</span></span>
<span data-ttu-id="15920-116">esempio Hello crea una macchina virtuale da [questo modello di gestione risorse di Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) con [distribuzione gruppo az creare](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="15920-116">hello following example creates a VM from [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="15920-117">Fornire la propria chiave pubblica SSH, ad esempio contenuto hello del valore hello *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="15920-117">Provide hello value of your own SSH public key, such as hello contents of *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="15920-118">Se è necessario toocreate una coppia di chiavi SSH, vedere [come toocreate e utilizzare un SSH coppia di chiavi per le macchine virtuali Linux in Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="15920-118">If you need toocreate an SSH key pair, see [How toocreate and use an SSH key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

<span data-ttu-id="15920-119">In questo esempio è stato specificato un modello archiviato in GitHub.</span><span class="sxs-lookup"><span data-stu-id="15920-119">In this example, you specified a template stored in GitHub.</span></span> <span data-ttu-id="15920-120">È anche possibile scaricare o creare un modello e specificare un percorso locale della hello con hello stesso `--template-file` parametro.</span><span class="sxs-lookup"><span data-stu-id="15920-120">You can also download or create a template and specify hello local path with hello same `--template-file` parameter.</span></span>

<span data-ttu-id="15920-121">tooSSH tooyour macchina virtuale, ottenere l'indirizzo IP pubblico hello con [Mostra public-ip di rete az](/cli/azure/network/public-ip#show):</span><span class="sxs-lookup"><span data-stu-id="15920-121">tooSSH tooyour VM, obtain hello public IP address with [az network public-ip show](/cli/azure/network/public-ip#show):</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="15920-122">È quindi possibile SSH tooyour VM come di consueto:</span><span class="sxs-lookup"><span data-stu-id="15920-122">You can then SSH tooyour VM as normal:</span></span>

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a><span data-ttu-id="15920-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="15920-123">Next steps</span></span>
<span data-ttu-id="15920-124">In questo esempio è stata creata una VM Linux di base.</span><span class="sxs-lookup"><span data-stu-id="15920-124">In this example, you created a basic Linux VM.</span></span> <span data-ttu-id="15920-125">Per ulteriori modelli di gestione risorse per l'inclusione di Framework applicazioni o creare ambienti più complessi, visitare hello [raccolta di modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="15920-125">For more Resource Manager templates that include application frameworks or create more complex environments, browse hello [Azure quickstart templates gallery](https://azure.microsoft.com/documentation/templates/).</span></span>

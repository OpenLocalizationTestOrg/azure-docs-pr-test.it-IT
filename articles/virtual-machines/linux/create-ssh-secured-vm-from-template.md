---
title: Creare una VM Linux in Azure da un modello | Microsoft Docs
description: Procedura per usare l'interfaccia della riga di comando 2.0 di Azure per creare una VM Linux da un modello di Resource Manager
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
ms.openlocfilehash: 908a8a0c82b2d21fb25c9b33dbd714570d1ac272
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-virtual-machine-with-azure-resource-manager-templates"></a><span data-ttu-id="0acb8-103">Procedura per creare una macchina virtuale Linux con i modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0acb8-103">How to create a Linux virtual machine with Azure Resource Manager templates</span></span>
<span data-ttu-id="0acb8-104">Questo articolo illustra come distribuire rapidamente una macchina virtuale (VM) Linux con i modelli di Azure Resource Manager e l'interfaccia della riga di comando 2.0 di Azure.</span><span class="sxs-lookup"><span data-stu-id="0acb8-104">This article shows you how to quickly deploy a Linux virtual machine (VM) with Azure Resource Manager templates and the Azure CLI 2.0.</span></span> <span data-ttu-id="0acb8-105">È possibile anche eseguire questi passaggi tramite l'[interfaccia della riga di comando di Azure 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="0acb8-105">You can also perform these steps with the [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span></span>


## <a name="templates-overview"></a><span data-ttu-id="0acb8-106">Panoramica dei modelli</span><span class="sxs-lookup"><span data-stu-id="0acb8-106">Templates overview</span></span>
<span data-ttu-id="0acb8-107">I modelli di Azure Resource Manager sono file JSON che definiscono l'infrastruttura e la configurazione della soluzione Azure.</span><span class="sxs-lookup"><span data-stu-id="0acb8-107">Azure Resource Manager templates are JSON files that define the infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="0acb8-108">Usando il modello è possibile distribuire ripetutamente la soluzione nel corso del ciclo di vita garantendo al contempo che le risorse vengano distribuite in uno stato coerente.</span><span class="sxs-lookup"><span data-stu-id="0acb8-108">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="0acb8-109">Per altre informazioni sul formato del modello e sulla sua costruzione, vedere [Creare il primo modello di Azure Resource Manager](../../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="0acb8-109">To learn more about the format of the template and how you construct it, see [Create your first Azure Resource Manager template](../../azure-resource-manager/resource-manager-create-first-template.md).</span></span> <span data-ttu-id="0acb8-110">Per visualizzare la sintassi JSON per i tipi di risorse, vedere [Define resources in Azure Resource Manager templates](/azure/templates/) (Definire le risorse nei modelli di Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="0acb8-110">To view the JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>


## <a name="create-resource-group"></a><span data-ttu-id="0acb8-111">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="0acb8-111">Create resource group</span></span>
<span data-ttu-id="0acb8-112">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="0acb8-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="0acb8-113">Il gruppo di risorse deve essere creato prima della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0acb8-113">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="0acb8-114">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroupVM* nell'area *stati uniti orientali*:</span><span class="sxs-lookup"><span data-stu-id="0acb8-114">The following example creates a resource group named *myResourceGroupVM* in the *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="0acb8-115">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0acb8-115">Create virtual machine</span></span>
<span data-ttu-id="0acb8-116">L'esempio seguente crea una VM da [questo modello di Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) con [az group deployment create](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="0acb8-116">The following example creates a VM from [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="0acb8-117">Fornire il valore della chiave pubblica SSH, ad esempio il contenuto di *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="0acb8-117">Provide the value of your own SSH public key, such as the contents of *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="0acb8-118">Se è necessario creare una coppia di chiavi SSH, vedere [Come creare e usare una coppia di chiavi SSH pubblica e privata per le VM Linux in Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="0acb8-118">If you need to create an SSH key pair, see [How to create and use an SSH key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

<span data-ttu-id="0acb8-119">In questo esempio è stato specificato un modello archiviato in GitHub.</span><span class="sxs-lookup"><span data-stu-id="0acb8-119">In this example, you specified a template stored in GitHub.</span></span> <span data-ttu-id="0acb8-120">È possibile anche scaricare o creare un modello e specificare il percorso locale con lo stesso parametro `--template-file`.</span><span class="sxs-lookup"><span data-stu-id="0acb8-120">You can also download or create a template and specify the local path with the same `--template-file` parameter.</span></span>

<span data-ttu-id="0acb8-121">Per la connessione SSH alla VM, ottenere l'indirizzo IP pubblico con [az network public-ip show](/cli/azure/network/public-ip#show):</span><span class="sxs-lookup"><span data-stu-id="0acb8-121">To SSH to your VM, obtain the public IP address with [az network public-ip show](/cli/azure/network/public-ip#show):</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="0acb8-122">È quindi possibile usare la connessione SSH alla VM nel modo usuale:</span><span class="sxs-lookup"><span data-stu-id="0acb8-122">You can then SSH to your VM as normal:</span></span>

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a><span data-ttu-id="0acb8-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0acb8-123">Next steps</span></span>
<span data-ttu-id="0acb8-124">In questo esempio è stata creata una VM Linux di base.</span><span class="sxs-lookup"><span data-stu-id="0acb8-124">In this example, you created a basic Linux VM.</span></span> <span data-ttu-id="0acb8-125">Per altri modelli di Resource Manager che includono i framework di applicazioni o creano ambienti più complessi, visitare la [Raccolta di modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="0acb8-125">For more Resource Manager templates that include application frameworks or create more complex environments, browse the [Azure quickstart templates gallery](https://azure.microsoft.com/documentation/templates/).</span></span>
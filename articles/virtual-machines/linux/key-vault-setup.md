---
title: aaaSet di insieme di credenziali chiave di Azure per le macchine virtuali Linux | Documenti Microsoft
description: Come tooset di insieme di credenziali chiave per l'utilizzo con una macchina virtuale di gestione risorse di Azure con hello CLI 2.0.
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: a5dc1fbe59a71b4456ba5b9bbacdb90440064757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a><span data-ttu-id="d3240-103">Come tooset di insieme di credenziali chiave per le macchine virtuali con hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d3240-103">How tooset up Key Vault for virtual machines with hello Azure CLI 2.0</span></span>

<span data-ttu-id="d3240-104">Nello stack di gestione risorse di Azure hello, segreti/certificati vengono modellati come risorse fornite dall'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="d3240-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span></span> <span data-ttu-id="d3240-105">toolearn ulteriori informazioni sull'insieme di credenziali chiave di Azure, vedere [che cos'è l'insieme di credenziali chiave di Azure?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="d3240-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="d3240-106">Affinché toobe insieme di credenziali chiave utilizzato con le macchine virtuali di Azure Resource Manager, hello *EnabledForDeployment* in insieme di credenziali chiave deve essere impostata tootrue.</span><span class="sxs-lookup"><span data-stu-id="d3240-106">In order for Key Vault toobe used with Azure Resource Manager VMs, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="d3240-107">Questo articolo illustra come tooset di insieme di credenziali chiave per l'utilizzo con macchine virtuali di Azure (VM) utilizzando hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="d3240-107">This article shows you how tooset up Key Vault for use with Azure virtual machines (VMs) using hello Azure CLI 2.0.</span></span> <span data-ttu-id="d3240-108">È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d3240-108">You can also perform these steps with hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d3240-109">tooperform questi passaggi, è necessario hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="d3240-109">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="d3240-110">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="d3240-110">Create a Key Vault</span></span>
<span data-ttu-id="d3240-111">Creare un insieme di credenziali chiave e assegnare criteri di distribuzione hello con [keyvault az creare](/cli/azure/keyvault#create).</span><span class="sxs-lookup"><span data-stu-id="d3240-111">Create a key vault and assign hello deployment policy with [az keyvault create](/cli/azure/keyvault#create).</span></span> <span data-ttu-id="d3240-112">esempio Hello crea un insieme di credenziali chiave denominata `myKeyVault` in hello `myResourceGroup` gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="d3240-112">hello following example creates a key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a><span data-ttu-id="d3240-113">Aggiornare un insieme di credenziali delle chiavi per l'uso con le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="d3240-113">Update a Key Vault for use with VMs</span></span>
<span data-ttu-id="d3240-114">Impostare i criteri di distribuzione hello in un insieme di credenziali chiave esistente con [aggiornamento keyvault az](/cli/azure/keyvault#update).</span><span class="sxs-lookup"><span data-stu-id="d3240-114">Set hello deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#update).</span></span> <span data-ttu-id="d3240-115">gli aggiornamenti seguenti Hello hello chiave dell'insieme di credenziali denominato `myKeyVault` in hello `myResourceGroup` gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="d3240-115">hello following updates hello key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="d3240-116">Utilizzare tooset di modelli di insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="d3240-116">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="d3240-117">Quando si utilizza un modello, è necessario hello tooset `enabledForDeployment` proprietà troppo`true` per la risorsa di hello insieme di credenziali chiave come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d3240-117">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource as follows:</span></span>

```json
{
    "type": "Microsoft.KeyVault/vaults",
    "name": "ContosoKeyVault",
    "apiVersion": "2015-06-01",
    "location": "<location-of-key-vault>",
    "properties": {
    "enabledForDeployment": "true",
    ....
    ....
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="d3240-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d3240-118">Next steps</span></span>
<span data-ttu-id="d3240-119">Per altre opzioni che è possibile configurare quando si crea un insieme di credenziali delle chiavi usando i modelli vedere [Crea un insieme di credenziali delle chiavi](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="d3240-119">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>

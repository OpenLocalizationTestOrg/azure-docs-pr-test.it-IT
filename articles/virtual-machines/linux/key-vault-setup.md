---
title: Configurare Azure Key Vault per le macchine virtuali Linux | Microsoft Docs
description: Come configurare Azure Key Vault da usare con una macchina virtuale di Azure Resource Manager con l'interfaccia della riga di comando 2.0.
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
ms.openlocfilehash: 2cc9b4c978e9a4deb0c8443c4b0f9e301a7cf492
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-key-vault-for-virtual-machines-with-the-azure-cli-20"></a><span data-ttu-id="da3fb-103">Come configurare Key Vault per le macchine virtuali con l'interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="da3fb-103">How to set up Key Vault for virtual machines with the Azure CLI 2.0</span></span>

<span data-ttu-id="da3fb-104">Nello stack di Azure Resource Manager i segreti e i certificati vengono modellati come risorse offerte tramite Key Vault.</span><span class="sxs-lookup"><span data-stu-id="da3fb-104">In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span></span> <span data-ttu-id="da3fb-105">Per altre informazioni sugli insiemi di credenziali delle chiavi di Azure, vedere [Informazioni sull'insieme di credenziali delle chiavi di Azure](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="da3fb-105">To learn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="da3fb-106">Per consentire l'uso di Key Vault con le macchine virtuali di Azure Resource Manager è necessario impostare su true la proprietà *EnabledForDeployment* in Key Vault.</span><span class="sxs-lookup"><span data-stu-id="da3fb-106">In order for Key Vault to be used with Azure Resource Manager VMs, the *EnabledForDeployment* property on Key Vault must be set to true.</span></span> <span data-ttu-id="da3fb-107">In questo articolo viene illustrato come configurare Key Vault delle chiavi per l'uso con macchine virtuali di Azure tramite l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="da3fb-107">This article shows you how to set up Key Vault for use with Azure virtual machines (VMs) using the Azure CLI 2.0.</span></span> <span data-ttu-id="da3fb-108">È possibile anche eseguire questi passaggi tramite l'[interfaccia della riga di comando di Azure 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="da3fb-108">You can also perform these steps with the [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="da3fb-109">Per eseguire questi passaggi è necessario aver installato la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e aver effettuato l'accesso a un account Azure con il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="da3fb-109">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="da3fb-110">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="da3fb-110">Create a Key Vault</span></span>
<span data-ttu-id="da3fb-111">Creare un insieme di credenziali delle chiavi e assegnare i criteri di distribuzione con [az keyvault create](/cli/azure/keyvault#create).</span><span class="sxs-lookup"><span data-stu-id="da3fb-111">Create a key vault and assign the deployment policy with [az keyvault create](/cli/azure/keyvault#create).</span></span> <span data-ttu-id="da3fb-112">Nell'esempio seguente viene creato un insieme di credenziali delle chiavi denominato `myKeyVault` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="da3fb-112">The following example creates a key vault named `myKeyVault` in the `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a><span data-ttu-id="da3fb-113">Aggiornare un insieme di credenziali delle chiavi per l'uso con le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="da3fb-113">Update a Key Vault for use with VMs</span></span>
<span data-ttu-id="da3fb-114">Impostare i criteri di distribuzione per un insieme di credenziali delle chiavi esistente con [az keyvault update](/cli/azure/keyvault#update).</span><span class="sxs-lookup"><span data-stu-id="da3fb-114">Set the deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#update).</span></span> <span data-ttu-id="da3fb-115">Il comando seguente aggiorna l'insieme di credenziali delle chiavi denominato `myKeyVault` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="da3fb-115">The following updates the key vault named `myKeyVault` in the `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="da3fb-116">Utilizzare modelli per configurare l'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="da3fb-116">Use templates to set up Key Vault</span></span>
<span data-ttu-id="da3fb-117">Se si usa un modello è necessario impostare come segue la proprietà `enabledForDeployment` su `true` per la risorsa Key Vault:</span><span class="sxs-lookup"><span data-stu-id="da3fb-117">When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource as follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="da3fb-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="da3fb-118">Next steps</span></span>
<span data-ttu-id="da3fb-119">Per altre opzioni che è possibile configurare quando si crea un insieme di credenziali delle chiavi usando i modelli vedere [Crea un insieme di credenziali delle chiavi](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="da3fb-119">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>

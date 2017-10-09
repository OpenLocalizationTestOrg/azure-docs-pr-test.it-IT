---
title: aaaAzure CLI Script di esempio - crittografare una VM Linux | Documenti Microsoft
description: 'Esempio di script dell''interfaccia della riga di comando di Azure: crittografare una VM Linux'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 1e455da4a8ea6d75b6d0d74b338d2e4d84973413
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="7d638-103">Crittografare una macchina virtuale Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="7d638-103">Encrypt a Linux virtual machine in Azure</span></span>

<span data-ttu-id="7d638-104">Questo script crea un insieme di credenziali delle chiavi di Azure sicuro, le chiavi di crittografia, un'entità servizio di Azure Active Directory e una macchina virtuale (VM) Linux.</span><span class="sxs-lookup"><span data-stu-id="7d638-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Linux virtual machine (VM).</span></span> <span data-ttu-id="7d638-105">Hello macchina virtuale viene quindi crittografata con la chiave di crittografia hello dall'insieme di credenziali chiave e le credenziali dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="7d638-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7d638-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="7d638-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7d638-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="7d638-107">Clean up deployment</span></span> 

<span data-ttu-id="7d638-108">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="7d638-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="7d638-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="7d638-109">Script explanation</span></span>

<span data-ttu-id="7d638-110">Questo script utilizza hello toocreate i comandi seguenti di una risorsa gruppo, insieme di credenziali chiave di Azure, servizio principale, macchina virtuale, e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="7d638-110">This script uses hello following commands toocreate a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="7d638-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="7d638-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7d638-112">Comando</span><span class="sxs-lookup"><span data-stu-id="7d638-112">Command</span></span> | <span data-ttu-id="7d638-113">Note</span><span class="sxs-lookup"><span data-stu-id="7d638-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7d638-114">az group create</span><span class="sxs-lookup"><span data-stu-id="7d638-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7d638-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="7d638-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7d638-116">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="7d638-116">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="7d638-117">Crea un insieme credenziali chiavi Azure toostore sicura di dati, ad esempio le chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="7d638-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="7d638-118">az keyvault key create</span><span class="sxs-lookup"><span data-stu-id="7d638-118">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="7d638-119">Crea una chiave di crittografia in Key Vault.</span><span class="sxs-lookup"><span data-stu-id="7d638-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="7d638-120">az ad sp create-for-rbac</span><span class="sxs-lookup"><span data-stu-id="7d638-120">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="7d638-121">Crea un servizio di Azure Active Directory principale toosecurely autenticare e controllare le chiavi di accesso tooencryption.</span><span class="sxs-lookup"><span data-stu-id="7d638-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="7d638-122">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="7d638-122">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="7d638-123">Imposta le autorizzazioni per hello insieme di credenziali chiave toogrant hello servizio principale tooencryption tasti di scelta.</span><span class="sxs-lookup"><span data-stu-id="7d638-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="7d638-124">az vm create</span><span class="sxs-lookup"><span data-stu-id="7d638-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="7d638-125">Crea macchina virtuale hello e lo connette la scheda di rete toohello, rete virtuale, subnet e gruppo.</span><span class="sxs-lookup"><span data-stu-id="7d638-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="7d638-126">Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="7d638-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="7d638-127">az vm encryption enable</span><span class="sxs-lookup"><span data-stu-id="7d638-127">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="7d638-128">Abilita la crittografia in una macchina virtuale con le credenziali dell'entità servizio di hello e la chiave di crittografia.</span><span class="sxs-lookup"><span data-stu-id="7d638-128">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="7d638-129">az vm encryption show</span><span class="sxs-lookup"><span data-stu-id="7d638-129">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="7d638-130">Mostra stato hello di hello il processo di crittografia di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7d638-130">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="7d638-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="7d638-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="7d638-132">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="7d638-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7d638-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7d638-133">Next steps</span></span>

<span data-ttu-id="7d638-134">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7d638-134">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7d638-135">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7d638-135">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

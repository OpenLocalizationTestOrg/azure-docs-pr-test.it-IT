---
title: aaaAzure CLI Script di esempio - crittografare una macchina virtuale Windows | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Crittografare una macchina virtuale Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 7a9928467f818cd5358d3d19bff5129d8fa21313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="b4072-103">Crittografare una macchina virtuale Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="b4072-103">Encrypt a Windows virtual machine in Azure</span></span>

<span data-ttu-id="b4072-104">Questo script crea un Azure Key Vault sicuro, le chiavi di crittografia, un'entità servizio di Azure Active Directory e una macchina virtuale (VM) Windows.</span><span class="sxs-lookup"><span data-stu-id="b4072-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="b4072-105">Hello macchina virtuale viene quindi crittografata con la chiave di crittografia hello dall'insieme di credenziali chiave e le credenziali dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="b4072-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b4072-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="b4072-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_windows_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b4072-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="b4072-107">Clean up deployment</span></span> 

<span data-ttu-id="b4072-108">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="b4072-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b4072-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="b4072-109">Script explanation</span></span>

<span data-ttu-id="b4072-110">Questo script utilizza hello toocreate i comandi seguenti di una risorsa gruppo, insieme di credenziali chiave di Azure, servizio principale, macchina virtuale, e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="b4072-110">This script uses hello following commands toocreate a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="b4072-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="b4072-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b4072-112">Comando</span><span class="sxs-lookup"><span data-stu-id="b4072-112">Command</span></span> | <span data-ttu-id="b4072-113">Note</span><span class="sxs-lookup"><span data-stu-id="b4072-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b4072-114">az group create</span><span class="sxs-lookup"><span data-stu-id="b4072-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b4072-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="b4072-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b4072-116">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="b4072-116">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="b4072-117">Crea un insieme credenziali chiavi Azure toostore sicura di dati, ad esempio le chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="b4072-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="b4072-118">az keyvault key create</span><span class="sxs-lookup"><span data-stu-id="b4072-118">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="b4072-119">Crea una chiave di crittografia in Key Vault.</span><span class="sxs-lookup"><span data-stu-id="b4072-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="b4072-120">az ad sp create-for-rbac</span><span class="sxs-lookup"><span data-stu-id="b4072-120">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="b4072-121">Crea un servizio di Azure Active Directory principale toosecurely autenticare e controllare le chiavi di accesso tooencryption.</span><span class="sxs-lookup"><span data-stu-id="b4072-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="b4072-122">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="b4072-122">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="b4072-123">Imposta le autorizzazioni per hello insieme di credenziali chiave toogrant hello servizio principale tooencryption tasti di scelta.</span><span class="sxs-lookup"><span data-stu-id="b4072-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="b4072-124">az vm create</span><span class="sxs-lookup"><span data-stu-id="b4072-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="b4072-125">Crea macchina virtuale hello e lo connette la scheda di rete toohello, rete virtuale, subnet e gruppo.</span><span class="sxs-lookup"><span data-stu-id="b4072-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="b4072-126">Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="b4072-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="b4072-127">az vm encryption enable</span><span class="sxs-lookup"><span data-stu-id="b4072-127">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="b4072-128">Abilita la crittografia in una macchina virtuale con le credenziali dell'entità servizio di hello e la chiave di crittografia.</span><span class="sxs-lookup"><span data-stu-id="b4072-128">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="b4072-129">az vm encryption show</span><span class="sxs-lookup"><span data-stu-id="b4072-129">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="b4072-130">Mostra stato hello di hello il processo di crittografia di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b4072-130">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="b4072-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="b4072-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="b4072-132">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="b4072-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b4072-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b4072-133">Next steps</span></span>

<span data-ttu-id="b4072-134">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b4072-134">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b4072-135">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione macchina virtuale Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b4072-135">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).</span></span>

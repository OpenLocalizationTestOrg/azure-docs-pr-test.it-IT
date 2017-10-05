---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Crittografare una macchina virtuale Windows | Microsoft Docs
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
ms.openlocfilehash: 9574d779982c939aa970cd4bdf7df6e66793e3b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="c75c9-103">Crittografare una macchina virtuale Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="c75c9-103">Encrypt a Windows virtual machine in Azure</span></span>

<span data-ttu-id="c75c9-104">Questo script crea un Azure Key Vault sicuro, le chiavi di crittografia, un'entità servizio di Azure Active Directory e una macchina virtuale (VM) Windows.</span><span class="sxs-lookup"><span data-stu-id="c75c9-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="c75c9-105">La VM viene quindi crittografata usando la chiave di crittografia del Key Vault e le credenziali dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="c75c9-105">The VM is then encrypted using the encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c75c9-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="c75c9-106">Sample script</span></span>

<span data-ttu-id="c75c9-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_windows_vm.sh "Crittografare i dischi delle VM")]</span><span class="sxs-lookup"><span data-stu-id="c75c9-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_windows_vm.sh "Encrypt VM disks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c75c9-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="c75c9-108">Clean up deployment</span></span> 

<span data-ttu-id="c75c9-109">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="c75c9-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c75c9-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="c75c9-110">Script explanation</span></span>

<span data-ttu-id="c75c9-111">Questo script usa i comandi seguenti per creare un gruppo di risorse, un insieme di credenziali delle chiavi di Azure, un'entità servizio, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="c75c9-111">This script uses the following commands to create a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="c75c9-112">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="c75c9-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c75c9-113">Comando</span><span class="sxs-lookup"><span data-stu-id="c75c9-113">Command</span></span> | <span data-ttu-id="c75c9-114">Note</span><span class="sxs-lookup"><span data-stu-id="c75c9-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c75c9-115">az group create</span><span class="sxs-lookup"><span data-stu-id="c75c9-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c75c9-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="c75c9-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c75c9-117">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="c75c9-117">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="c75c9-118">Crea un insieme di credenziali delle chiavi di Azure per archiviare i dati protetti, ad esempio le chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="c75c9-118">Creates an Azure Key Vault to store secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="c75c9-119">az keyvault key create</span><span class="sxs-lookup"><span data-stu-id="c75c9-119">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="c75c9-120">Crea una chiave di crittografia in Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c75c9-120">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="c75c9-121">az ad sp create-for-rbac</span><span class="sxs-lookup"><span data-stu-id="c75c9-121">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="c75c9-122">Crea un'entità servizio di Azure Active Directory per autenticare in modo sicuro e controllare l'accesso alle chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="c75c9-122">Creates an Azure Active Directory service principal to securely authenticate and control access to encryption keys.</span></span> |
| [<span data-ttu-id="c75c9-123">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="c75c9-123">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="c75c9-124">Imposta le autorizzazioni in Key Vault per concedere l'accesso dell'entità servizio alle chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="c75c9-124">Sets permissions on the Key Vault to grant the service principal access to encryption keys.</span></span> |
| [<span data-ttu-id="c75c9-125">az vm create</span><span class="sxs-lookup"><span data-stu-id="c75c9-125">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="c75c9-126">Consente di creare la macchina virtuale e la connette alla scheda di rete, alla rete virtuale, alla subnet e al gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="c75c9-126">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="c75c9-127">Questo comando specifica anche l'immagine della macchina virtuale da usare e le credenziali di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="c75c9-127">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="c75c9-128">az vm encryption enable</span><span class="sxs-lookup"><span data-stu-id="c75c9-128">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="c75c9-129">Abilita la crittografia in una VM usando le credenziali dell'entità servizio e la chiave di crittografia.</span><span class="sxs-lookup"><span data-stu-id="c75c9-129">Enables encryption on a VM using the service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="c75c9-130">az vm encryption show</span><span class="sxs-lookup"><span data-stu-id="c75c9-130">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="c75c9-131">Mostra lo stato del processo di crittografia della VM.</span><span class="sxs-lookup"><span data-stu-id="c75c9-131">Shows the status of the VM encryption process.</span></span> |
| [<span data-ttu-id="c75c9-132">az group delete</span><span class="sxs-lookup"><span data-stu-id="c75c9-132">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="c75c9-133">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="c75c9-133">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c75c9-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c75c9-134">Next steps</span></span>

<span data-ttu-id="c75c9-135">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c75c9-135">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c75c9-136">Altri esempi di script dell'interfaccia della riga di comando della macchina virtuale sono reperibili nella [documentazione della macchina virtuale Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c75c9-136">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).</span></span>

---
title: Ridistribuire macchine virtuali Linux in Azure | Documentazione Microsoft
description: Come ridistribuire macchine virtuali Linux in Azure per ridurre i problemi di connessione SSH.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 7a8653a82775e718c38f65f246d997ba61f99d58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="redeploy-linux-virtual-machine-to-new-azure-node"></a><span data-ttu-id="38868-103">Ridistribuire una macchina virtuale Linux in un nuovo nodo di Azure</span><span class="sxs-lookup"><span data-stu-id="38868-103">Redeploy Linux virtual machine to new Azure node</span></span>
<span data-ttu-id="38868-104">Se si riscontrano difficoltà nella risoluzione dei problemi relativi a SSH o all'accesso delle applicazioni a una macchina virtuale Linux in Azure, potrebbe essere utile ridistribuire la VM.</span><span class="sxs-lookup"><span data-stu-id="38868-104">If you face difficulties troubleshooting SSH or application access to a Linux virtual machine (VM) in Azure, redeploying the VM may help.</span></span> <span data-ttu-id="38868-105">Quando si ridistribuisce una VM, quest'ultima viene spostata su un nuovo nodo dell'infrastruttura di Azure, quindi viene riattivata.</span><span class="sxs-lookup"><span data-stu-id="38868-105">When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on.</span></span> <span data-ttu-id="38868-106">Tutte le opzioni di configurazione e le risorse associate vengono mantenute.</span><span class="sxs-lookup"><span data-stu-id="38868-106">All your configuration options and associated resources are retained.</span></span> <span data-ttu-id="38868-107">In questo articolo viene illustrato come ridistribuire una VM con l'interfaccia della riga di comando di Azure o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="38868-107">This article shows you how to redeploy a VM using Azure CLI or the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="38868-108">Dopo la ridistribuzione di una VM, il disco temporaneo viene perso e gli indirizzi IP dinamici associati all'interfaccia di rete virtuale vengono aggiornati.</span><span class="sxs-lookup"><span data-stu-id="38868-108">After you redeploy a VM, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 

<span data-ttu-id="38868-109">È possibile ridistribuire una VM tramite una delle opzioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="38868-109">You can redeploy a VM using one of the following options.</span></span> <span data-ttu-id="38868-110">È sufficiente scegliere un'opzione per la ridistribuzione:</span><span class="sxs-lookup"><span data-stu-id="38868-110">You only need to choose one option to redeploy your VM:</span></span>

- [<span data-ttu-id="38868-111">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="38868-111">Azure CLI 2.0</span></span>](#azure-cli-20)
- [<span data-ttu-id="38868-112">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="38868-112">Azure CLI 1.0</span></span>](#azure-cli-10)
- [<span data-ttu-id="38868-113">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="38868-113">Azure portal</span></span>](#using-azure-portal)

## <a name="use-the-azure-cli-20"></a><span data-ttu-id="38868-114">Usare l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="38868-114">Use the Azure CLI 2.0</span></span>
<span data-ttu-id="38868-115">Installare la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e accedere a un account Azure tramite il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="38868-115">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="38868-116">Ridistribuire la VM con il comando [az vm redeploy](/cli/azure/vm#redeploy).</span><span class="sxs-lookup"><span data-stu-id="38868-116">Redeploy your VM with [az vm redeploy](/cli/azure/vm#redeploy).</span></span> <span data-ttu-id="38868-117">Nell'esempio seguente la VM denominata *myVM* viene ridistribuita nel gruppo di risorse denominato *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="38868-117">The following example redeploys the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-the-azure-cli-10"></a><span data-ttu-id="38868-118">Usare l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="38868-118">Use the Azure CLI 1.0</span></span>
<span data-ttu-id="38868-119">Installare la [versione più recente dell'interfaccia della riga di comando di Azure 1.0](../../cli-install-nodejs.md), accedere a un account Azure e verificare che sia attiva la modalità Resource Manager (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="38868-119">Install the [latest Azure CLI 1.0](../../cli-install-nodejs.md), log in to an Azure account, and make sure that you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="38868-120">Nell'esempio seguente la VM denominata *myVM* viene ridistribuita nel gruppo di risorse denominato *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="38868-120">The following example redeploys the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="38868-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="38868-121">Next steps</span></span>
<span data-ttu-id="38868-122">In caso di problemi di connessione alla VM, è possibile trovare assistenza specifica sulla [risoluzione dei problemi relativi alle connessioni SSH](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o sui [passaggi dettagliati per la risoluzione dei problemi SSH](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="38868-122">If you are having issues connecting to your VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="38868-123">Se non si riesce ad accedere a un'applicazione in esecuzione sulla VM, è possibile leggere l'articolo sulle [difficoltà nella risoluzione dei problemi relativi alle applicazioni](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="38868-123">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


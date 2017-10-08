---
title: Macchine virtuali Linux in Azure aaaRedeploy | Documenti Microsoft
description: Come le macchine virtuali Linux tooredeploy nella connessione SSH toomitigate Azure problemi.
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
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a><span data-ttu-id="45d3f-103">Ridistribuire la macchina virtuale di Linux toonew nodo di Azure</span><span class="sxs-lookup"><span data-stu-id="45d3f-103">Redeploy Linux virtual machine toonew Azure node</span></span>
<span data-ttu-id="45d3f-104">Se si trovano ad affrontare problemi di risoluzione dei problemi SSH o applicazione accedere tooa Linux macchina virtuale (VM) in Azure, ridistribuire hello VM può essere utile.</span><span class="sxs-lookup"><span data-stu-id="45d3f-104">If you face difficulties troubleshooting SSH or application access tooa Linux virtual machine (VM) in Azure, redeploying hello VM may help.</span></span> <span data-ttu-id="45d3f-105">Quando si ridistribuisce una macchina virtuale, sposta hello VM tooa nuovo nodo all'interno dell'infrastruttura di Azure hello e quindi accende viene nuovamente.</span><span class="sxs-lookup"><span data-stu-id="45d3f-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on.</span></span> <span data-ttu-id="45d3f-106">Tutte le opzioni di configurazione e le risorse associate vengono mantenute.</span><span class="sxs-lookup"><span data-stu-id="45d3f-106">All your configuration options and associated resources are retained.</span></span> <span data-ttu-id="45d3f-107">In questo articolo illustra come tooredeploy una macchina virtuale tramite l'interfaccia CLI di Azure o hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="45d3f-107">This article shows you how tooredeploy a VM using Azure CLI or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="45d3f-108">Dopo la ridistribuzione di una macchina virtuale, disco temporaneo hello andrà persa e vengono aggiornati gli indirizzi IP dinamici associati con l'interfaccia di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="45d3f-108">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 

<span data-ttu-id="45d3f-109">È possibile ridistribuire una macchina virtuale usando una delle seguenti opzioni hello.</span><span class="sxs-lookup"><span data-stu-id="45d3f-109">You can redeploy a VM using one of hello following options.</span></span> <span data-ttu-id="45d3f-110">È sufficiente toochoose una opzione tooredeploy la macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="45d3f-110">You only need toochoose one option tooredeploy your VM:</span></span>

- [<span data-ttu-id="45d3f-111">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="45d3f-111">Azure CLI 2.0</span></span>](#azure-cli-20)
- [<span data-ttu-id="45d3f-112">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="45d3f-112">Azure CLI 1.0</span></span>](#azure-cli-10)
- [<span data-ttu-id="45d3f-113">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="45d3f-113">Azure portal</span></span>](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="45d3f-114">Utilizzare hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="45d3f-114">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="45d3f-115">Hello installazione più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) e accedere con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="45d3f-115">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="45d3f-116">Ridistribuire la VM con il comando [az vm redeploy](/cli/azure/vm#redeploy).</span><span class="sxs-lookup"><span data-stu-id="45d3f-116">Redeploy your VM with [az vm redeploy](/cli/azure/vm#redeploy).</span></span> <span data-ttu-id="45d3f-117">Hello seguenti distribuzioni di esempio hello macchina virtuale denominata *myVM* nel gruppo di risorse hello denominato *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="45d3f-117">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="45d3f-118">Utilizzare hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="45d3f-118">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="45d3f-119">Installare hello [più recente di Azure CLI 1.0](../../cli-install-nodejs.md), accedi tooan account Azure e assicurarsi che siano in modalità di gestione risorse (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="45d3f-119">Install hello [latest Azure CLI 1.0](../../cli-install-nodejs.md), log in tooan Azure account, and make sure that you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="45d3f-120">Hello seguenti distribuzioni di esempio hello macchina virtuale denominata *myVM* nel gruppo di risorse hello denominato *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="45d3f-120">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="45d3f-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45d3f-121">Next steps</span></span>
<span data-ttu-id="45d3f-122">Se si sono verificati problemi di connessione tooyour VM, è possibile trovare informazioni specifiche su [risoluzione dei problemi relativi a connessioni SSH](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [dettagliate SSH risoluzione](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="45d3f-122">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="45d3f-123">Se non si riesce ad accedere a un'applicazione in esecuzione sulla VM, è possibile leggere l'articolo sulle [difficoltà nella risoluzione dei problemi relativi alle applicazioni](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="45d3f-123">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


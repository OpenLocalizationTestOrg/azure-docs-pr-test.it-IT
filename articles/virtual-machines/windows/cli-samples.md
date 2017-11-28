---
title: aaaAzure CLI esempi di Windows | Documenti Microsoft
description: Esempi dell'interfaccia della riga di comando di Azure per Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 1eef61a24d14897dd0a88a3f467854cc21b1938d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-windows-virtual-machines"></a><span data-ttu-id="95348-103">Esempi dell'interfaccia della riga di comando di Azure per macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="95348-103">Azure CLI Samples for Windows virtual machines</span></span>

<span data-ttu-id="95348-104">Hello nella tabella seguente sono inclusi collegamenti toobash script compilato utilizzando hello CLI di Azure che distribuire macchine virtuali di Windows.</span><span class="sxs-lookup"><span data-stu-id="95348-104">hello following table includes links toobash scripts built using hello Azure CLI that deploy Windows virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="95348-105">**Creare macchine virtuali**</span><span class="sxs-lookup"><span data-stu-id="95348-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="95348-106">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="95348-106">Create a virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="95348-107">Consente di creare una macchina virtuale Windows con la configurazione minima.</span><span class="sxs-lookup"><span data-stu-id="95348-107">Creates a Windows virtual machine with minimal configuration.</span></span> |
| [<span data-ttu-id="95348-108">Creare una macchina virtuale completamente configurata</span><span class="sxs-lookup"><span data-stu-id="95348-108">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="95348-109">Consente di creare un gruppo di risorse, una macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="95348-109">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="95348-110">Creare macchine virtuali a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="95348-110">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="95348-111">Consente di creare più macchine virtuali in una configurazione a disponibilità elevata e con bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="95348-111">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="95348-112">Creare una macchina virtuale ed eseguire script di configurazione</span><span class="sxs-lookup"><span data-stu-id="95348-112">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-iis.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="95348-113">Crea una macchina virtuale e utilizza hello Azure Custom Script estensione tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="95348-113">Creates a virtual machine and uses hello Azure Custom Script extension tooinstall IIS.</span></span> |
| [<span data-ttu-id="95348-114">Creare una macchina virtuale ed eseguire la configurazione DSC</span><span class="sxs-lookup"><span data-stu-id="95348-114">Create a VM and run DSC configuration</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-iis-using-dsc.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="95348-115">Crea una macchina virtuale e utilizza hello Azure configurazione DSC (Desired State) estensione tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="95348-115">Creates a virtual machine and uses hello Azure Desired State Configuration (DSC) extension tooinstall IIS.</span></span> |
|<span data-ttu-id="95348-116">**Macchine virtuali di rete**</span><span class="sxs-lookup"><span data-stu-id="95348-116">**Network virtual machines**</span></span>||
| [<span data-ttu-id="95348-117">Proteggere il traffico di rete tra le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="95348-117">Secure network traffic between virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="95348-118">Consente di creare due macchine virtuali, tutte le risorse correlate, un gruppo di sicurezza di rete interno e uno esterno.</span><span class="sxs-lookup"><span data-stu-id="95348-118">Creates two virtual machines, all related resources, and an internal and external network security groups (NSG).</span></span> |
|<span data-ttu-id="95348-119">**Proteggere le macchine virtuali**</span><span class="sxs-lookup"><span data-stu-id="95348-119">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="95348-120">Crittografare una macchina virtuale e i dischi dati</span><span class="sxs-lookup"><span data-stu-id="95348-120">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-windows-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="95348-121">Crea un'istanza di Azure Key Vault, una chiave di crittografia e un'entità servizio, quindi crittografa una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="95348-121">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="95348-122">**Monitorare le macchine virtuali**</span><span class="sxs-lookup"><span data-stu-id="95348-122">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="95348-123">Monitorare una macchina virtuale con Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="95348-123">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="95348-124">Crea una macchina virtuale, installa l'agente di Operations Management Suite hello e registra hello macchina virtuale in un'area di lavoro di OMS.</span><span class="sxs-lookup"><span data-stu-id="95348-124">Creates a virtual machine, installs hello Operations Management Suite agent, and enrolls hello VM in an OMS Workspace.</span></span>  |
| | |

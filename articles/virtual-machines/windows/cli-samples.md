---
title: Esempi dell'interfaccia della riga di comando di Azure per Windows | Documentazione Microsoft
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
ms.openlocfilehash: f4b2e8a5583855df7472af3fbef01ac641caf6bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-samples-for-windows-virtual-machines"></a><span data-ttu-id="e63d3-103">Esempi dell'interfaccia della riga di comando di Azure per macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="e63d3-103">Azure CLI Samples for Windows virtual machines</span></span>

<span data-ttu-id="e63d3-104">La tabella seguente fornisce collegamenti a script Bash, compilati tramite l'interfaccia della riga di comando di Azure, che distribuiscono macchine virtuali di Windows.</span><span class="sxs-lookup"><span data-stu-id="e63d3-104">The following table includes links to bash scripts built using the Azure CLI that deploy Windows virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="e63d3-105">**Creare macchine virtuali**</span><span class="sxs-lookup"><span data-stu-id="e63d3-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="e63d3-106">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e63d3-106">Create a virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="e63d3-107">Consente di creare una macchina virtuale Windows con la configurazione minima.</span><span class="sxs-lookup"><span data-stu-id="e63d3-107">Creates a Windows virtual machine with minimal configuration.</span></span> |
| [<span data-ttu-id="e63d3-108">Creare una macchina virtuale completamente configurata</span><span class="sxs-lookup"><span data-stu-id="e63d3-108">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="e63d3-109">Consente di creare un gruppo di risorse, una macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="e63d3-109">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="e63d3-110">Creare macchine virtuali a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="e63d3-110">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="e63d3-111">Consente di creare più macchine virtuali in una configurazione a disponibilità elevata e con bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="e63d3-111">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="e63d3-112">Creare una macchina virtuale ed eseguire script di configurazione</span><span class="sxs-lookup"><span data-stu-id="e63d3-112">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-iis.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="e63d3-113">Consente di creare una macchina virtuale e usa l'estensione dello script personalizzato di Azure per installare IIS.</span><span class="sxs-lookup"><span data-stu-id="e63d3-113">Creates a virtual machine and uses the Azure Custom Script extension to install IIS.</span></span> |
| [<span data-ttu-id="e63d3-114">Creare una macchina virtuale ed eseguire la configurazione DSC</span><span class="sxs-lookup"><span data-stu-id="e63d3-114">Create a VM and run DSC configuration</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-iis-using-dsc.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="e63d3-115">Consente di creare una macchina virtuale e usa l'estensione di configurazione dello stato desiderato di Azure per installare IIS.</span><span class="sxs-lookup"><span data-stu-id="e63d3-115">Creates a virtual machine and uses the Azure Desired State Configuration (DSC) extension to install IIS.</span></span> |
|<span data-ttu-id="e63d3-116">**Macchine virtuali di rete**</span><span class="sxs-lookup"><span data-stu-id="e63d3-116">**Network virtual machines**</span></span>||
| [<span data-ttu-id="e63d3-117">Proteggere il traffico di rete tra le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e63d3-117">Secure network traffic between virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="e63d3-118">Consente di creare due macchine virtuali, tutte le risorse correlate, un gruppo di sicurezza di rete interno e uno esterno.</span><span class="sxs-lookup"><span data-stu-id="e63d3-118">Creates two virtual machines, all related resources, and an internal and external network security groups (NSG).</span></span> |
|<span data-ttu-id="e63d3-119">**Proteggere le macchine virtuali**</span><span class="sxs-lookup"><span data-stu-id="e63d3-119">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="e63d3-120">Crittografare una macchina virtuale e i dischi dati</span><span class="sxs-lookup"><span data-stu-id="e63d3-120">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-windows-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="e63d3-121">Crea un'istanza di Azure Key Vault, una chiave di crittografia e un'entità servizio, quindi crittografa una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e63d3-121">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="e63d3-122">**Monitorare le macchine virtuali**</span><span class="sxs-lookup"><span data-stu-id="e63d3-122">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="e63d3-123">Monitorare una macchina virtuale con Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="e63d3-123">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="e63d3-124">Consente di creare una macchina virtuale, installare l'agente Operations Management Suite e registrare la macchina virtuale in un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="e63d3-124">Creates a virtual machine, installs the Operations Management Suite agent, and enrolls the VM in an OMS Workspace.</span></span>  |
| | |

---
title: aaaDifferent modi toocreate una macchina virtuale Windows in Azure | Documenti Microsoft
description: Elenca i diversi modi di hello toocreate una macchina virtuale di Windows con Gestione risorse.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a><span data-ttu-id="dc005-103">Modi diversi toocreate una macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="dc005-103">Different ways toocreate a Windows virtual machine</span></span>

<span data-ttu-id="dc005-104">Azure offre modi toocreate una macchina virtuale perché le macchine virtuali sono adatti per scopi e utenti diversi.</span><span class="sxs-lookup"><span data-stu-id="dc005-104">Azure offers different ways toocreate a virtual machine because virtual machines are suited for different users and purposes.</span></span> <span data-ttu-id="dc005-105">Ciò significa che è necessario toomake elencate alcune scelte sulla macchina virtuale hello e come toocreate è.</span><span class="sxs-lookup"><span data-stu-id="dc005-105">This means that you need toomake some choices about hello virtual machine and how toocreate it.</span></span> <span data-ttu-id="dc005-106">In questo articolo offre un riepilogo di queste opzioni e i collegamenti tooinstructions.</span><span class="sxs-lookup"><span data-stu-id="dc005-106">This article gives you a summary of these choices and links tooinstructions.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="dc005-107">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="dc005-107">Azure portal</span></span>
<span data-ttu-id="dc005-108">Tramite il portale di Azure hello è tootry un modo semplice out di una macchina virtuale, in particolare se si inizia con Azure.</span><span class="sxs-lookup"><span data-stu-id="dc005-108">Using hello Azure portal is a simple way tootry out a virtual machine, especially if you're just starting out with Azure.</span></span> 

[<span data-ttu-id="dc005-109">Creare una macchina virtuale che esegue Windows usando il portale di hello</span><span class="sxs-lookup"><span data-stu-id="dc005-109">Create a virtual machine running Windows using hello portal</span></span>](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a><span data-ttu-id="dc005-110">Modello</span><span class="sxs-lookup"><span data-stu-id="dc005-110">Template</span></span>
<span data-ttu-id="dc005-111">Le macchine virtuali richiedono una combinazione di risorse (come set di disponibilità e account di archiviazione).</span><span class="sxs-lookup"><span data-stu-id="dc005-111">Virtual machines require a combination of resources (such as a availability sets and storage accounts).</span></span> <span data-ttu-id="dc005-112">Invece di distribuire e gestire separatamente ogni risorsa, è possibile creare un modello di gestione risorse di Azure che distribuisce ed esegue il provisioning di tutte le risorse di hello in un'operazione singola, coordinata.</span><span class="sxs-lookup"><span data-stu-id="dc005-112">Rather than deploying and managing each resource separately, you can create an Azure Resource Manager template that deploys and provisions all of hello resources in a single, coordinated operation.</span></span>

* [<span data-ttu-id="dc005-113">Creare una macchina virtuale Windows con un modello di Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="dc005-113">Create a Windows virtual machine with a Resource Manager template</span></span>](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a><span data-ttu-id="dc005-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc005-114">Azure PowerShell</span></span>
<span data-ttu-id="dc005-115">Se si preferisce lavorare in una shell dei comandi, è possibile utilizzare Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc005-115">If you prefer working in a command shell, you can use Azure PowerShell.</span></span>

* [<span data-ttu-id="dc005-116">Creare una VM Windows tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc005-116">Create a Windows VM using PowerShell</span></span>](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a><span data-ttu-id="dc005-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dc005-117">Visual Studio</span></span>
<span data-ttu-id="dc005-118">Utilizzare Visual Studio toobuild, gestire, distribuire le macchine virtuali con hello Azure Tools per Visual Studio e hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="dc005-118">Use Visual Studio toobuild, manage, and deploy VMs with hello Azure Tools for Visual Studio and hello Azure SDK.</span></span>

[<span data-ttu-id="dc005-119">Strumenti di Azure per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dc005-119">Azure Tools for Visual Studio</span></span>](https://www.visualstudio.com/features/azure-tools-vs)


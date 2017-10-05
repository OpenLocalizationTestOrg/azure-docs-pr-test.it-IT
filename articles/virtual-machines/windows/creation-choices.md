---
title: Diversi modi per creare una macchina virtuale Windows in Azure| Documentazione Microsoft
description: Elenca i diversi modi per creare una macchina virtuale Windows con Gestione risorse.
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
ms.openlocfilehash: 5e51c49aac01a22d86c7c1a12b2f2ca7ddc056bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="different-ways-to-create-a-windows-virtual-machine"></a><span data-ttu-id="8f951-103">Diversi modi per creare una macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="8f951-103">Different ways to create a Windows virtual machine</span></span>

<span data-ttu-id="8f951-104">Azure offre diversi modi per creare una macchina virtuale perché le macchine virtuali sono adatte a scopi e utenti diversi.</span><span class="sxs-lookup"><span data-stu-id="8f951-104">Azure offers different ways to create a virtual machine because virtual machines are suited for different users and purposes.</span></span> <span data-ttu-id="8f951-105">Di conseguenza è necessario effettuare alcune scelte sulla macchina virtuale e su come crearla.</span><span class="sxs-lookup"><span data-stu-id="8f951-105">This means that you need to make some choices about the virtual machine and how to create it.</span></span> <span data-ttu-id="8f951-106">In questo articolo viene fornito un riepilogo di queste opzioni e i collegamenti alle istruzioni.</span><span class="sxs-lookup"><span data-stu-id="8f951-106">This article gives you a summary of these choices and links to instructions.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="8f951-107">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8f951-107">Azure portal</span></span>
<span data-ttu-id="8f951-108">L’utilizzo del portale di Azure è un modo semplice per provare a usare una macchina virtuale, soprattutto se si ha poca esperienza con Azure.</span><span class="sxs-lookup"><span data-stu-id="8f951-108">Using the Azure portal is a simple way to try out a virtual machine, especially if you're just starting out with Azure.</span></span> 

[<span data-ttu-id="8f951-109">Creare una macchina virtuale con Windows tramite il portale</span><span class="sxs-lookup"><span data-stu-id="8f951-109">Create a virtual machine running Windows using the portal</span></span>](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a><span data-ttu-id="8f951-110">Modello</span><span class="sxs-lookup"><span data-stu-id="8f951-110">Template</span></span>
<span data-ttu-id="8f951-111">Le macchine virtuali richiedono una combinazione di risorse (come set di disponibilità e account di archiviazione).</span><span class="sxs-lookup"><span data-stu-id="8f951-111">Virtual machines require a combination of resources (such as a availability sets and storage accounts).</span></span> <span data-ttu-id="8f951-112">Anziché distribuire e gestire separatamente ogni risorsa, è possibile creare un modello Azure Resource Manager che distribuisce e fornisce tutte le risorse in un'unica operazione coordinata.</span><span class="sxs-lookup"><span data-stu-id="8f951-112">Rather than deploying and managing each resource separately, you can create an Azure Resource Manager template that deploys and provisions all of the resources in a single, coordinated operation.</span></span>

* [<span data-ttu-id="8f951-113">Creare una macchina virtuale Windows con un modello di Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="8f951-113">Create a Windows virtual machine with a Resource Manager template</span></span>](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a><span data-ttu-id="8f951-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f951-114">Azure PowerShell</span></span>
<span data-ttu-id="8f951-115">Se si preferisce lavorare in una shell dei comandi, è possibile utilizzare Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f951-115">If you prefer working in a command shell, you can use Azure PowerShell.</span></span>

* [<span data-ttu-id="8f951-116">Creare una VM Windows tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f951-116">Create a Windows VM using PowerShell</span></span>](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a><span data-ttu-id="8f951-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8f951-117">Visual Studio</span></span>
<span data-ttu-id="8f951-118">Usare Visual Studio per creare, gestire e distribuire VM con gli strumenti di Azure per Visual Studio e Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="8f951-118">Use Visual Studio to build, manage, and deploy VMs with the Azure Tools for Visual Studio and the Azure SDK.</span></span>

[<span data-ttu-id="8f951-119">Strumenti di Azure per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8f951-119">Azure Tools for Visual Studio</span></span>](https://www.visualstudio.com/features/azure-tools-vs)


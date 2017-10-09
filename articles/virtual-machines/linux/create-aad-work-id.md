---
title: "aaaCreate un'identità aziendale o dell'istituto di istruzione in AAD per Linux | Documenti Microsoft"
description: "Informazioni su come toocreate un'identità aziendale o dell'istituto di istruzione in Azure Active Directory toouse con le macchine virtuali Linux."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: b0f86d77-c669-4aa1-a095-c2aa4d9105fe
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 54c3d0b0e89fe1b2d6a9b58a46776fe446ed72b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-linux-vms"></a><span data-ttu-id="a9ff1-103">Creazione di un'identità aziendale o dell'istituto di istruzione in Azure Active Directory toouse con le macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="a9ff1-103">Creating a Work or School identity in Azure Active Directory toouse with Linux VMs</span></span>
<span data-ttu-id="a9ff1-104">Se è stato creato un account di Azure personale o disporre di una sottoscrizione MSDN personale e creato hello account Azure tootake sfruttare crediti di Azure di MSDN hello - è stato utilizzato un *account Microsoft* toocreate identità è.</span><span class="sxs-lookup"><span data-stu-id="a9ff1-104">If you created a personal Azure account or have a personal MSDN subscription and created hello Azure account tootake advantage of hello MSDN Azure credits -- you used a *Microsoft account* identity toocreate it.</span></span> <span data-ttu-id="a9ff1-105">Molte caratteristiche di Azure - [modelli di gruppo di risorse](../../azure-resource-manager/resource-group-overview.md) è un esempio, richiedono un account aziendale o dell'istituto di istruzione (un'identità gestita da Azure Active Directory) toowork.</span><span class="sxs-lookup"><span data-stu-id="a9ff1-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) toowork.</span></span> <span data-ttu-id="a9ff1-106">È possibile seguire le istruzioni di hello sotto toocreate che un nuovo lavoro o scuola account perché, per fortuna, uno degli aspetti migliori hello l'account di Azure personale che è dotato di un dominio di Azure Active Directory predefinito che è possibile utilizzare toocreate un nuovo lavoro o dell'istituto di istruzione account che è possibile utilizzare con le funzionalità di Azure che lo richiedono.</span><span class="sxs-lookup"><span data-stu-id="a9ff1-106">You can follow hello instructions below toocreate a new work or school account because fortunately, one of hello best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use toocreate a new work or school account that you can use with Azure features that require it.</span></span>

<span data-ttu-id="a9ff1-107">Tuttavia, le modifiche recenti rendono possibili toomanage la sottoscrizione con qualsiasi tipo di account Azure tramite hello `azure login` il metodo di accesso interattivo descritto [qui](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="a9ff1-107">However, recent changes make it possible toomanage your subscription with any type of Azure account using hello `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span></span> <span data-ttu-id="a9ff1-108">È possibile utilizzare tale meccanismo oppure è possibile seguire le istruzioni hello che seguono.</span><span class="sxs-lookup"><span data-stu-id="a9ff1-108">You can either use that mechanism, or you can follow hello instructions that follow.</span></span> <span data-ttu-id="a9ff1-109">È anche possibile [creare un'identità aziendale o dell'istituto di istruzione in Azure Active Directory toouse con macchine virtuali Windows](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a9ff1-109">You can also [create a work or school identity in Azure Active Directory toouse with Windows VMs](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]


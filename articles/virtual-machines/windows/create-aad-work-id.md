---
title: "Creare un'identità aziendale o dell'istituto di istruzione in AAD per Windows | Documentazione Microsoft"
description: "Informazioni su come creare un'identità di lavoro o scuola in Azure Active Directory da usare con macchine virtuali Windows."
services: virtual-machines-windows
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d07dca34-618a-48aa-9971-03d9c1210f4a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 7694b959a384aaed213adc31e02debca31b7c131
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-to-use-with-windows-vms"></a><span data-ttu-id="4e4d9-103">Creazione di un'identità di lavoro o scuola in Azure Active Directory da usare con macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="4e4d9-103">Creating a Work or School identity in Azure Active Directory to use with Windows VMs</span></span>
<span data-ttu-id="4e4d9-104">Se si è creato un account Azure personale, oppure si dispone di una sottoscrizione MSDN personale e si è creato l'account Azure per sfruttare i vantaggi dei crediti MSDN in Azure, si è usata un'identità *account Microsoft* .</span><span class="sxs-lookup"><span data-stu-id="4e4d9-104">If you created a personal Azure account or have a personal MSDN subscription and created the Azure account to take advantage of the MSDN Azure credits -- you used a *Microsoft account* identity to create it.</span></span> <span data-ttu-id="4e4d9-105">Numerose funzionalità di Azure, ad esempio i [modelli dei gruppi di risorse](../../azure-resource-manager/resource-group-overview.md), per funzionare richiedono un account aziendale o dell'istituto di istruzione (un'identità gestita da Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4e4d9-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) to work.</span></span> <span data-ttu-id="4e4d9-106">Per creare un nuovo account aziendale o dell’istituto d’istruzione è possibile seguire le seguenti istruzioni poichè fortunatamente, uno degli aspetti migliori dell'account Azure personale sta nel fatto che è dotato di un dominio predefinito di Azure Active Directory, che è possibile usare per creare un nuovo account aziendale o dell’istituto d’istruzione da usare con le funzionalità di Azure che lo richiedono.</span><span class="sxs-lookup"><span data-stu-id="4e4d9-106">You can follow the instructions below to create a new work or school account because fortunately, one of the best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use to create a new work or school account that you can use with Azure features that require it.</span></span>

<span data-ttu-id="4e4d9-107">Tuttavia, le modifiche più recenti consentono di gestire la sottoscrizione con qualsiasi tipo di account Azure tramite il metodo di accesso interattivo `azure login` descritto [qui](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="4e4d9-107">However, recent changes make it possible to manage your subscription with any type of Azure account using the `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span></span> <span data-ttu-id="4e4d9-108">È possibile utilizzare tale meccanismo oppure seguire le istruzioni che seguono.</span><span class="sxs-lookup"><span data-stu-id="4e4d9-108">You can either use that mechanism, or you can follow the instructions that follow.</span></span> <span data-ttu-id="4e4d9-109">È anche possibile [creare un'identità di lavoro o scuola in Azure Active Directory da usare con macchine virtuali Linux](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4e4d9-109">You can also [create a work or school identity in Azure Active Directory to use with Linux VMs](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]


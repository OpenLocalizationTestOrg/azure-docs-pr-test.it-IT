---
title: aaaAvailability imposta per le macchine virtuali Linux classico | Documenti Microsoft
description: "Configurare un gruppo di disponibilità per una macchina virtuale Linux nuova o esistente nel modello di distribuzione classica hello utilizzando hello portale di Azure e Azure PowerShell."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b8624315-beca-4ec7-8441-2e98b166b548
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2016
ms.author: cynthn
ms.openlocfilehash: 8d8d041e3540e42a1921f5665469a2fdcaa30a29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-availability-set-for-linux-virtual-machines-in-hello-classic-deployment-model"></a><span data-ttu-id="4053d-103">Come tooconfigure un gruppo di disponibilità per le macchine virtuali Linux nel modello di distribuzione classica hello</span><span class="sxs-lookup"><span data-stu-id="4053d-103">How tooconfigure an availability set for Linux virtual machines in hello classic deployment model</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="4053d-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4053d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4053d-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="4053d-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="4053d-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="4053d-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="4053d-107">È anche possibile [configurare i set di disponibilità](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) nelle distribuzioni Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4053d-107">You can also [configure availability sets](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) in Resource Manager deployments.</span></span>

[!INCLUDE [virtual-machines-common-classic-configure-availability](../../../../includes/virtual-machines-common-classic-configure-availability.md)]
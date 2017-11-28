---
title: "Set di disponibilità per macchine virtuali Linux classiche | Microsoft Docs"
description: "Configurare un set di disponibilità per una macchina virtuale Linux nuova o esistente nel modello di distribuzione classica usando il portale di Azure e Azure PowerShell."
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
ms.openlocfilehash: 41d427862150d17e1ad726afc51114d6f62f5a8e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-an-availability-set-for-linux-virtual-machines-in-the-classic-deployment-model"></a><span data-ttu-id="79ee2-103">Come configurare un set di disponibilità per le macchine virtuali Linux nel modello di distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="79ee2-103">How to configure an availability set for Linux virtual machines in the classic deployment model</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="79ee2-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="79ee2-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="79ee2-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="79ee2-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="79ee2-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="79ee2-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="79ee2-107">È anche possibile [configurare i set di disponibilità](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) nelle distribuzioni Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="79ee2-107">You can also [configure availability sets](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) in Resource Manager deployments.</span></span>

[!INCLUDE [virtual-machines-common-classic-configure-availability](../../../../includes/virtual-machines-common-classic-configure-availability.md)]
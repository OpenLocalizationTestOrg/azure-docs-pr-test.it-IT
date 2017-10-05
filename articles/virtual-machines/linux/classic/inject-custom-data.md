---
title: Inserire dati in macchine virtuali Linux in Azure | Documentazione Microsoft
description: In questo argomento viene descritto come inserire dati personalizzati in una macchina virtuale di Azure durante la creazione dell'istanza e come individuare i dati personalizzati in Windows o Linux.
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: d376093c-e01d-4ee3-a826-2b5a35caaa7e
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 8dd04c26f10950b13fe0689a96b3e12250715019
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="injecting-custom-data-into-an-azure-virtual-machine"></a><span data-ttu-id="13034-103">Inserimento di dati personalizzati in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="13034-103">Injecting custom data into an Azure virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="13034-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="13034-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="13034-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="13034-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="13034-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="13034-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="13034-107">Per informazioni sull'uso dell'estensione script personalizzata con il modello di Resource Manager, vedere [qui](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="13034-107">For information about using the Custom Script Extension with the Resource Manager model, see [here](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-inject-custom-data](../../../../includes/virtual-machines-common-classic-inject-custom-data.md)]


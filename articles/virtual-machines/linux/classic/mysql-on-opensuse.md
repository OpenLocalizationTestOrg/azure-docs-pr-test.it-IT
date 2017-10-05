---
title: Installare MySQL in una macchina virtuale OpenSUSE | Microsoft Docs
description: Informazioni su come installare MySQL in una macchina virtuale OpenSUSE Linux in Azure.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1594e10e-c314-455a-9efb-a89441de364b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/19/2016
ms.author: cynthn
ms.openlocfilehash: 01b798a25575b66f89057315ce80d6cc0cde53b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a><span data-ttu-id="a6b51-103">Installazione di MySQL in una macchina virtuale che esegue OpenSUSE Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="a6b51-103">Install MySQL on a virtual machine running OpenSUSE Linux in Azure</span></span>
<span data-ttu-id="a6b51-104">[MySQL][MySQL] è un database SQL open source molto diffuso.</span><span class="sxs-lookup"><span data-stu-id="a6b51-104">[MySQL][MySQL] is a popular, open-source SQL database.</span></span> <span data-ttu-id="a6b51-105">Questa esercitazione illustra come creare una macchina virtuale che esegue OpenSUSE Linux, poi installa MySQL.</span><span class="sxs-lookup"><span data-stu-id="a6b51-105">This tutorial shows you how to create a virtual machine running OpenSUSE Linux, then install MySQL.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="a6b51-106">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a6b51-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a6b51-107">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="a6b51-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="a6b51-108">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="a6b51-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a><span data-ttu-id="a6b51-109">Creare una macchina virtuale che esegue OpenSUSE Linux</span><span class="sxs-lookup"><span data-stu-id="a6b51-109">Create a virtual machine running OpenSUSE Linux</span></span>
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-the-virtual-machine"></a><span data-ttu-id="a6b51-110">Installare ed eseguire MySQL nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a6b51-110">Install and run MySQL on the virtual machine</span></span>
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="a6b51-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6b51-111">Next steps</span></span>
<span data-ttu-id="a6b51-112">Per informazioni su MySQL, vedere la [documentazione di MySQL][MySQLDocs].</span><span class="sxs-lookup"><span data-stu-id="a6b51-112">For details about MySQL, see the [MySQL Documentation][MySQLDocs].</span></span>

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com


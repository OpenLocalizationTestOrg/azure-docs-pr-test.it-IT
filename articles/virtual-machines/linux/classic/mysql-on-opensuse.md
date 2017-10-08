---
title: aaaInstall MySQL in una VM OpenSUSE | Documenti Microsoft
description: Informazioni su tooinstall MySQL in un computer OpenSUSE VMirtual di Linux in Azure.
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
ms.openlocfilehash: 8f96d29f29cb9c466dd7fdaf92b378783fdaacd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a><span data-ttu-id="84f33-103">Installazione di MySQL in una macchina virtuale che esegue OpenSUSE Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="84f33-103">Install MySQL on a virtual machine running OpenSUSE Linux in Azure</span></span>
<span data-ttu-id="84f33-104">[MySQL][MySQL] è un database SQL open source molto diffuso.</span><span class="sxs-lookup"><span data-stu-id="84f33-104">[MySQL][MySQL] is a popular, open-source SQL database.</span></span> <span data-ttu-id="84f33-105">Questa esercitazione viene illustrato come toocreate una macchina virtuale che esegue OpenSUSE Linux, quindi installare MySQL.</span><span class="sxs-lookup"><span data-stu-id="84f33-105">This tutorial shows you how toocreate a virtual machine running OpenSUSE Linux, then install MySQL.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="84f33-106">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="84f33-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="84f33-107">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="84f33-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="84f33-108">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="84f33-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a><span data-ttu-id="84f33-109">Creare una macchina virtuale che esegue OpenSUSE Linux</span><span class="sxs-lookup"><span data-stu-id="84f33-109">Create a virtual machine running OpenSUSE Linux</span></span>
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-hello-virtual-machine"></a><span data-ttu-id="84f33-110">Installare ed eseguire MySQL nella macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="84f33-110">Install and run MySQL on hello virtual machine</span></span>
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="84f33-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="84f33-111">Next steps</span></span>
<span data-ttu-id="84f33-112">Per informazioni dettagliate su MySQL, vedere hello [documentazione di MySQL][MySQLDocs].</span><span class="sxs-lookup"><span data-stu-id="84f33-112">For details about MySQL, see hello [MySQL Documentation][MySQLDocs].</span></span>

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com


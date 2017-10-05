---
title: Accedere a una VM di Azure classico | Microsoft Docs
description: Usare il portale di Azure per accedere a una macchina virtuale Windows creata con il modello di distribuzione classica.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 3c1239ed-07dc-48b8-8b3d-dc8c5f0ab20e
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 43d54de7e875de9212c23c49ad0539bf2272a312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="log-on-to-a-windows-virtual-machine-using-the-azure-portal"></a><span data-ttu-id="22847-103">Accedere a una macchina virtuale di Windows tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="22847-103">Log on to a Windows virtual machine using the Azure portal</span></span>
<span data-ttu-id="22847-104">Nel portale di Azure, si utilizza il pulsante **Connetti** per avviare una sessione di Desktop remoto e accedere a una macchina virtuale Windows.</span><span class="sxs-lookup"><span data-stu-id="22847-104">In the Azure portal, you use the **Connect** button to start a Remote Desktop session and log on to a Windows VM.</span></span>

<span data-ttu-id="22847-105">Si desidera effettuare la connessione a una macchina virtuale Linux?</span><span class="sxs-lookup"><span data-stu-id="22847-105">Do you want to connect to a Linux VM?</span></span> <span data-ttu-id="22847-106">Vedere [Come accedere a una macchina virtuale che esegue Linux](../../linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="22847-106">See [How to log on to a virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span></span>

<!--
Deleting, but not 100% sure
Learn how to [perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> <span data-ttu-id="22847-107">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="22847-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="22847-108">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="22847-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="22847-109">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="22847-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="22847-110">Per informazioni sull'accesso a una macchina virtuale usando il modello di Resource Manager, vedere [qui](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="22847-110">For information about how to log on to a VM using the Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="22847-111">Connettersi alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="22847-111">Connect to the virtual machine</span></span>
1. <span data-ttu-id="22847-112">Accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="22847-112">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="22847-113">Fare clic sulla macchina virtuale a cui si desidera accedere.</span><span class="sxs-lookup"><span data-stu-id="22847-113">Click on the virtual machine that you want to access.</span></span> <span data-ttu-id="22847-114">Il nome è indicato nel riquadro **Tutte le risorse**.</span><span class="sxs-lookup"><span data-stu-id="22847-114">The name is listed in the **All resources** pane.</span></span>

    ![Virtual-machine-locations](./media/connect-logon/azureportaldashboard.png)

3. <span data-ttu-id="22847-116">Fare clic su **Connetti** sulla barra dei comandi sopra il dashboard della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="22847-116">Click **Connect** on the command bar atop the virtual machine dashboard.</span></span>

    ![Icona di connessione per la macchina virtuale](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If the **Connect** button isn't available, see the troubleshooting tips at the end of this article.
>
>
-->

## <a name="log-on-to-the-virtual-machine"></a><span data-ttu-id="22847-118">Accesso alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="22847-118">Log on to the virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="22847-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="22847-119">Next steps</span></span>
* <span data-ttu-id="22847-120">Se il pulsante **Connetti** non è attivo o si verificano altri problemi di connessione per il Desktop remoto, provare a reimpostare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="22847-120">If the **Connect** button is inactive or you are having other problems with the Remote Desktop connection, try resetting the configuration.</span></span> <span data-ttu-id="22847-121">Fare clic su **Ripristina accesso remoto** dal dashboard della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="22847-121">click **Reset remote access** from the virtual machine dashboard.</span></span>

    ![Reset-remote-access](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* <span data-ttu-id="22847-123">Per problemi con la password, provare a reimpostarla.</span><span class="sxs-lookup"><span data-stu-id="22847-123">For problems with your password, try resetting it.</span></span> <span data-ttu-id="22847-124">Fare clic su **Ripristina password** sul lato sinistro del dashboard della macchina virtuale in **Supporto e risoluzione dei problemi**.</span><span class="sxs-lookup"><span data-stu-id="22847-124">Click **Reset password** along the left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span></span>

    ![Reset-password](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

<span data-ttu-id="22847-126">Se le precedenti istruzioni non sono sufficienti o non sono quelle necessarie, vedere [Risolvere i problemi di connessioni Desktop remoto a una macchina virtuale di Azure basata su Windows](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="22847-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="22847-127">In questo articolo viene illustrato come diagnosticare e risolvere i problemi più comuni.</span><span class="sxs-lookup"><span data-stu-id="22847-127">This article walks you through diagnosing and resolving common problems.</span></span>

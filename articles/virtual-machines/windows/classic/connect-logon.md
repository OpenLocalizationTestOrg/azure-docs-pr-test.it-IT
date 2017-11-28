---
title: aaaLog su tooa macchina virtuale di Azure classico | Documenti Microsoft
description: Utilizzare hello toolog portale Azure nella macchina virtuale di Windows tooa creato con il modello di distribuzione classica hello.
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
ms.openlocfilehash: 2e32b7036c2538e73b46580e0f5f8f4979e8a685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="003e7-103">Accedere tooa macchina virtuale Windows usando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="003e7-103">Log on tooa Windows virtual machine using hello Azure portal</span></span>
<span data-ttu-id="003e7-104">Nel portale di Azure hello, utilizzare hello **Connetti** pulsante toostart una sessione Desktop remoto e accedere tooa macchina virtuale di Windows.</span><span class="sxs-lookup"><span data-stu-id="003e7-104">In hello Azure portal, you use hello **Connect** button toostart a Remote Desktop session and log on tooa Windows VM.</span></span>

<span data-ttu-id="003e7-105">Si desidera tooconnect tooa VM Linux?</span><span class="sxs-lookup"><span data-stu-id="003e7-105">Do you want tooconnect tooa Linux VM?</span></span> <span data-ttu-id="003e7-106">Vedere [come toolog nella macchina virtuale tooa che eseguono Linux](../../linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="003e7-106">See [How toolog on tooa virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span></span>

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> <span data-ttu-id="003e7-107">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="003e7-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="003e7-108">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="003e7-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="003e7-109">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="003e7-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="003e7-110">Per informazioni su come toolog sull'utilizzo delle VM tooa hello Gestione risorse del modello, vedere [qui](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="003e7-110">For information about how toolog on tooa VM using hello Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="003e7-111">Connettere la macchina virtuale di toohello</span><span class="sxs-lookup"><span data-stu-id="003e7-111">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="003e7-112">Accedi toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="003e7-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="003e7-113">Fare clic sulla macchina virtuale hello che si desidera tooaccess.</span><span class="sxs-lookup"><span data-stu-id="003e7-113">Click on hello virtual machine that you want tooaccess.</span></span> <span data-ttu-id="003e7-114">nome Hello è elencato in hello **tutte le risorse** riquadro.</span><span class="sxs-lookup"><span data-stu-id="003e7-114">hello name is listed in hello **All resources** pane.</span></span>

    ![Virtual-machine-locations](./media/connect-logon/azureportaldashboard.png)

3. <span data-ttu-id="003e7-116">Fare clic su **Connetti** hello barra dei comandi nella parte superiore del dashboard di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="003e7-116">Click **Connect** on hello command bar atop hello virtual machine dashboard.</span></span>

    ![Icona per la macchina virtuale hello della connessione](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="003e7-118">Accedere alla macchina virtuale toohello</span><span class="sxs-lookup"><span data-stu-id="003e7-118">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="003e7-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="003e7-119">Next steps</span></span>
* <span data-ttu-id="003e7-120">Se hello **Connetti** pulsante è attivo o di altri problemi con connessione Desktop remoto hello, provare a reimpostare la configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="003e7-120">If hello **Connect** button is inactive or you are having other problems with hello Remote Desktop connection, try resetting hello configuration.</span></span> <span data-ttu-id="003e7-121">Fare clic su **reimpostare l'accesso remoto** dal dashboard macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="003e7-121">click **Reset remote access** from hello virtual machine dashboard.</span></span>

    ![Reset-remote-access](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* <span data-ttu-id="003e7-123">Per problemi con la password, provare a reimpostarla.</span><span class="sxs-lookup"><span data-stu-id="003e7-123">For problems with your password, try resetting it.</span></span> <span data-ttu-id="003e7-124">Fare clic su **reimpostazione password** lungo hello bordo sinistro del dashboard macchina virtuale, in **supporto + Troubleshooting**.</span><span class="sxs-lookup"><span data-stu-id="003e7-124">Click **Reset password** along hello left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span></span>

    ![Reset-password](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

<span data-ttu-id="003e7-126">Se tali suggerimenti non funzionano o non sono quelli desiderati, vedere [tooa connessioni Desktop remoto di risoluzione dei problemi basato su Windows Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="003e7-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="003e7-127">In questo articolo viene illustrato come diagnosticare e risolvere i problemi più comuni.</span><span class="sxs-lookup"><span data-stu-id="003e7-127">This article walks you through diagnosing and resolving common problems.</span></span>

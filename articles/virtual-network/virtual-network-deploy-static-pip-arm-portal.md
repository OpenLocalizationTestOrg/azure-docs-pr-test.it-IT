---
title: aaaCreate una macchina virtuale con un indirizzo IP pubblico statico - portale di Azure | Documenti Microsoft
description: Informazioni su come una macchina virtuale con un indirizzo pubblico IP statico usando toocreate hello portale di Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74d2132785f06148757409ee0a44b98d1e4b98e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a><span data-ttu-id="b316d-103">Creare una macchina virtuale con un indirizzo IP pubblico statico utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b316d-103">Create a VM with a static public IP address using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b316d-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b316d-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="b316d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b316d-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="b316d-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b316d-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="b316d-107">Modello</span><span class="sxs-lookup"><span data-stu-id="b316d-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * <span data-ttu-id="b316d-108">[PowerShell (Classic)](virtual-networks-reserved-public-ip.md) (PowerShell (classico))</span><span class="sxs-lookup"><span data-stu-id="b316d-108">[PowerShell (Classic)](virtual-networks-reserved-public-ip.md)</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="b316d-109">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b316d-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b316d-110">In questo articolo viene illustrato l'utilizzo di modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="b316d-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a><span data-ttu-id="b316d-111">Creare una VM con un IP pubblico statico</span><span class="sxs-lookup"><span data-stu-id="b316d-111">Create a VM with a static public IP</span></span>

<span data-ttu-id="b316d-112">toocreate una macchina virtuale con un indirizzo IP pubblico statico di indirizzi in hello portale di Azure completo hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b316d-112">toocreate a VM with a static public IP address in hello Azure portal, complete hello following steps:</span></span>

1. <span data-ttu-id="b316d-113">Da un browser, passare toohello [portale di Azure](https://portal.azure.com) e, se necessario, accedere con l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="b316d-113">From a browser, navigate toohello [Azure portal](https://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="b316d-114">Nell'angolo superiore sinistro di hello del portale hello, fare clic su **New**>>**calcolo**>**Windows Server 2012 R2 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="b316d-114">On hello top left hand corner of hello portal, click **New**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span></span>
3. <span data-ttu-id="b316d-115">In hello **selezionare un modello di distribuzione** selezionare **Gestione risorse** e fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="b316d-115">In hello **Select a deployment model** list, select **Resource Manager** and click **Create**.</span></span>
4. <span data-ttu-id="b316d-116">In hello **nozioni di base** pannello, immettere le informazioni di VM hello, come illustrato di seguito e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b316d-116">In hello **Basics** blade, enter hello VM information as shown below, and then click **OK**.</span></span>
   
    ![Portale di Azure: Nozioni di base](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. <span data-ttu-id="b316d-118">In hello **scegliere una dimensione** pannello, fare clic su **A1 Standard** come illustrato di seguito, quindi fare clic su **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="b316d-118">In hello **Choose a size** blade, click **A1 Standard** as shown below, and then click **Select**.</span></span>
   
    ![Portale di Azure: Scegliere una dimensione](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. <span data-ttu-id="b316d-120">In hello **impostazioni** pannello, fare clic su **indirizzo IP pubblico**, quindi nella hello **creare l'indirizzo IP pubblico** pannello, in **assegnazione**, fare clic su **Statico** come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b316d-120">In hello **Settings** blade, click **Public IP address**, then in hello **Create public IP address** blade, under **Assignment**, click **Static** as shown below.</span></span> <span data-ttu-id="b316d-121">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b316d-121">And then click **OK**.</span></span>
   
    ![Portale di Azure: Creare l'indirizzo IP pubblico](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. <span data-ttu-id="b316d-123">In hello **impostazioni** pannello, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b316d-123">In hello **Settings** blade, click **OK**.</span></span>
8. <span data-ttu-id="b316d-124">Hello revisione **riepilogo** pannello, come illustrato di seguito e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b316d-124">Review hello **Summary** blade, as shown below, and then click **OK**.</span></span>
   
    ![Portale di Azure: Creare l'indirizzo IP pubblico](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. <span data-ttu-id="b316d-126">Si noti nuovo riquadro di hello nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="b316d-126">Notice hello new tile in your dashboard.</span></span>
   
    ![Portale di Azure: Creare l'indirizzo IP pubblico](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. <span data-ttu-id="b316d-128">Una volta creato, hello VM hello **impostazioni** pannello verrà visualizzato come illustrato di seguito</span><span class="sxs-lookup"><span data-stu-id="b316d-128">Once hello VM is created, hello **Settings** blade will be displayed as shown below</span></span>
    
    ![Portale di Azure: Creare l'indirizzo IP pubblico](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)


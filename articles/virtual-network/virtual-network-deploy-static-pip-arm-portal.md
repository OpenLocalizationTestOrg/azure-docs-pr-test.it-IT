---
title: Creare una VM con un indirizzo IP pubblico statico - Portale di Azure | Documentazione Microsoft
description: Informazioni su come creare una VM con un indirizzo IP pubblico statico mediante il portale di Azure.
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
ms.openlocfilehash: 233e4eea8439320c1c7446e2c2b2e9d379351a3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-the-azure-portal"></a><span data-ttu-id="99d37-103">Creare una VM con un indirizzo IP pubblico statico mediante il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="99d37-103">Create a VM with a static public IP address using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="99d37-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="99d37-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="99d37-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="99d37-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="99d37-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="99d37-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="99d37-107">Modello</span><span class="sxs-lookup"><span data-stu-id="99d37-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * <span data-ttu-id="99d37-108">[PowerShell (Classic)](virtual-networks-reserved-public-ip.md) (PowerShell (classico))</span><span class="sxs-lookup"><span data-stu-id="99d37-108">[PowerShell (Classic)](virtual-networks-reserved-public-ip.md)</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="99d37-109">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="99d37-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="99d37-110">Questo articolo illustra l'uso del modello di distribuzione Resource Manager che Microsoft consiglia di usare invece del modello di distribuzione classica per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="99d37-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a><span data-ttu-id="99d37-111">Creare una VM con un IP pubblico statico</span><span class="sxs-lookup"><span data-stu-id="99d37-111">Create a VM with a static public IP</span></span>

<span data-ttu-id="99d37-112">Per creare una VM con un IP pubblico statico nel portale di Azure, completare i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="99d37-112">To create a VM with a static public IP address in the Azure portal, complete the following steps:</span></span>

1. <span data-ttu-id="99d37-113">In un browser passare al [portale di Azure](https://portal.azure.com) e, se necessario, accedere con l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="99d37-113">From a browser, navigate to the [Azure portal](https://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="99d37-114">Nell'angolo superiore sinistro del portale fare clic su **Nuovo**>>**Calcolo**>**Windows Server 2012 R2 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="99d37-114">On the top left hand corner of the portal, click **New**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span></span>
3. <span data-ttu-id="99d37-115">Nell'elenco **Selezionare un modello di distribuzione** selezionare **Resource Manager** e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="99d37-115">In the **Select a deployment model** list, select **Resource Manager** and click **Create**.</span></span>
4. <span data-ttu-id="99d37-116">Nel pannello **Informazioni di base** immettere le informazioni della VM come illustrato di seguito, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="99d37-116">In the **Basics** blade, enter the VM information as shown below, and then click **OK**.</span></span>
   
    ![Portale di Azure: Nozioni di base](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. <span data-ttu-id="99d37-118">Nel pannello **Scegli una dimensione** fare clic su **Standard A1** come illustrato di seguito, quindi sul pulsante di **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="99d37-118">In the **Choose a size** blade, click **A1 Standard** as shown below, and then click **Select**.</span></span>
   
    ![Portale di Azure: Scegliere una dimensione](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. <span data-ttu-id="99d37-120">Nel pannello **Impostazioni** fare clic su **Indirizzo IP pubblico**, quindi nel pannello **Crea indirizzo IP pubblico**, in **Assegnazione**, fare clic su **Statico** come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="99d37-120">In the **Settings** blade, click **Public IP address**, then in the **Create public IP address** blade, under **Assignment**, click **Static** as shown below.</span></span> <span data-ttu-id="99d37-121">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="99d37-121">And then click **OK**.</span></span>
   
    ![Portale di Azure: Creare l'indirizzo IP pubblico](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. <span data-ttu-id="99d37-123">Nel pannello **Impostazioni** fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="99d37-123">In the **Settings** blade, click **OK**.</span></span>
8. <span data-ttu-id="99d37-124">Esaminare il pannello **Riepilogo**, come illustrato di seguito, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="99d37-124">Review the **Summary** blade, as shown below, and then click **OK**.</span></span>
   
    ![Portale di Azure: Creare l'indirizzo IP pubblico](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. <span data-ttu-id="99d37-126">Notare il nuovo riquadro nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="99d37-126">Notice the new tile in your dashboard.</span></span>
   
    ![Portale di Azure: Creare l'indirizzo IP pubblico](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. <span data-ttu-id="99d37-128">Dopo aver creato la VM, il pannello **Impostazioni** viene visualizzato il pannello come illustrato di seguito</span><span class="sxs-lookup"><span data-stu-id="99d37-128">Once the VM is created, the **Settings** blade will be displayed as shown below</span></span>
    
    ![Portale di Azure: Creare l'indirizzo IP pubblico](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)


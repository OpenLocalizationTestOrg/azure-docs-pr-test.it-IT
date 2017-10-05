---
title: Configurare indirizzi IP privati per le VM (classiche) - Portale di Azure | Documentazione Microsoft
description: Informazioni su come configurare indirizzi IP privati per macchine virtuali (classiche) mediante il portale di Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bde6de3495c2909b63b1f85e420a4ff5e7ac2c1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-the-azure-portal"></a><span data-ttu-id="998b8-103">Configurare indirizzi IP privati per una macchina virtuale (classica) mediante il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="998b8-103">Configure private IP addresses for a virtual machine (Classic) using the Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="998b8-104">In questo articolo viene illustrato il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="998b8-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="998b8-105">È inoltre possibile [gestire un indirizzo IP statico privato nel modello di distribuzione di gestione delle risorse](virtual-networks-static-private-ip-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="998b8-105">You can also [manage a static private IP address in the Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="998b8-106">La procedura di esempio seguente prevede che un ambiente semplice sia già creato.</span><span class="sxs-lookup"><span data-stu-id="998b8-106">The sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="998b8-107">Se si desidera eseguire la procedura illustrata in questo documento, creare innanzitutto l'ambiente di prova descritto in [creare una rete virtuale](virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="998b8-107">If you want to run the steps as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-to-specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="998b8-108">Come specificare un indirizzo IP statico privato durante la creazione di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="998b8-108">How to specify a static private IP address when creating a VM</span></span>
<span data-ttu-id="998b8-109">Per creare una VM denominata *DNS01* nella subnet *FrontEnd* di una rete virtuale denominata *TestVNet* con un indirizzo IP statico privato di *192.168.1.101*, seguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="998b8-109">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="998b8-110">In un browser passare a http://portal.azure.com e, se necessario, accedere con l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="998b8-110">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="998b8-111">Fare clic su **NUOVO** > **Calcolo** > **Windows Server 2012 R2 Datacenter**; si noti che l'elenco **Selezionare un modello di distribuzione** mostra già **Classico**, quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="998b8-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that the **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="998b8-113">Nel pannello **Creare VM** , immettere il nome della macchina virtuale da creare (*DNS01* nello scenario), l'account amministratore locale e la password.</span><span class="sxs-lookup"><span data-stu-id="998b8-113">In the **Create VM** blade, enter the name of the VM to be created (*DNS01* in our scenario), the local administrator account, and password.</span></span>
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="998b8-115">Fare clic su **Configurazione facoltativa** > **Rete** > **Rete virtuale**, poi fare clic su **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="998b8-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="998b8-116">Se **TestVNet** non è disponibile, verificare che si utilizzi la posizione *Stati Uniti centrali* e di aver creato l'ambiente di prova descritto all'inizio di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="998b8-116">If **TestVNet** is not available, make sure you are using the *Central US* location and have created the test environment described at the beginning of this article.</span></span>
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="998b8-118">Nel pannello **Rete** assicurarsi che la subnet attualmente selezionata sia *FrontEnd*, poi fare clic su **Indirizzi IP**, in **Assegnazione indirizzi IP** fare clic su **Statico** e immettere *192.168.1.101* per **Indirizzo IP** come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="998b8-118">In the **Network** blade, make sure the subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="998b8-120">Fare clic su **OK** nel pannello **Indirizzi IP**, poi fare clic su **OK** nel pannello **Rete**, e fare clic su **OK** nel pannello **Configurazione facoltativa**.</span><span class="sxs-lookup"><span data-stu-id="998b8-120">Click **OK** in the **IP addresses** blade, then click **OK** in the **Network** blade, and click **OK** in the **Optional config** blade.</span></span>
7. <span data-ttu-id="998b8-121">Nel pannello **Creare VM** fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="998b8-121">In the **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="998b8-122">Si noti il riquadro visualizzato di seguito nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="998b8-122">Notice the tile below displayed in your dashboard.</span></span>
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="998b8-124">Come recuperare le informazioni relative all'indirizzo IP privato statico per una VM</span><span class="sxs-lookup"><span data-stu-id="998b8-124">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="998b8-125">Per visualizzare le informazioni dell’indirizzo IP privato statico per la macchina virtuale creata con la procedura descritta sopra, eseguire la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="998b8-125">To view the static private IP address information for the VM created with the steps above, execute the steps below.</span></span>

1. <span data-ttu-id="998b8-126">Nel portale di Azure fare clic su **ESPLORA TUTTO** > **Macchine virtuali (classico)** > **DNS01** > **Tutte le impostazioni** > **Indirizzi IP** e notare l'assegnazione di indirizzi IP e l'indirizzo IP come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="998b8-126">From the Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice the IP address assignment and IP address as seen below.</span></span>
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="998b8-128">Come rimuovere un indirizzo IP statico privato da una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="998b8-128">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="998b8-129">Per rimuovere l'indirizzo IP statico privato dalla macchina virtuale creata in precedenza, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="998b8-129">To remove the static private IP address from the VM created above, follow the steps below.</span></span>

1. <span data-ttu-id="998b8-130">Dal pannello **Indirizzi IP** mostrato in precedenza fare clic su **Dinamica** a destra di **Assegnazione indirizzi IP**, poi fare clic su **Salva** e su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="998b8-130">From the **IP addresses** blade shown above, click **Dynamic** to the right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a><span data-ttu-id="998b8-132">Come aggiungere un indirizzo IP statico privato a una macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="998b8-132">How to add a static private IP address to an existing VM</span></span>
<span data-ttu-id="998b8-133">Per aggiungere un indirizzo IP statico privato per la macchina virtuale creata in precedenza, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="998b8-133">To add a static private IP address to the VM created using the steps above, follow the steps below:</span></span>

1. <span data-ttu-id="998b8-134">Dal pannello **Indirizzi IP** mostrato in precedenza, fare clic su **Statica** a destra di **Assegnazione indirizzi IP**.</span><span class="sxs-lookup"><span data-stu-id="998b8-134">From the **IP addresses** blade shown above, click **Static** to the right of **IP address assignment**.</span></span>
2. <span data-ttu-id="998b8-135">Digitare *192.168.1.101* per **indirizzo IP**, fare clic su **Salva**, quindi fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="998b8-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="998b8-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="998b8-136">Next steps</span></span>
* <span data-ttu-id="998b8-137">Informazioni su [indirizzi IP pubblici riservati](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="998b8-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="998b8-138">Informazioni su [indirizzi IP pubblici a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="998b8-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="998b8-139">Consultare le [API REST dell'indirizzo IP riservato](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="998b8-139">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>


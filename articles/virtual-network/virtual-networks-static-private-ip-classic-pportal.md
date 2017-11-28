---
title: indirizzi IP privati aaaConfigure per le macchine virtuali (classico) - portale di Azure | Documenti Microsoft
description: Informazioni su come indirizzi IP privati tooconfigure per le macchine virtuali (classico) utilizzando hello portale di Azure.
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
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a><span data-ttu-id="79333-103">Configurare gli indirizzi IP privati per una macchina virtuale (classico) utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="79333-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="79333-104">Questo articolo descrive il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="79333-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="79333-105">È anche possibile [gestire un indirizzo IP privato statico nel modello di distribuzione di gestione risorse di hello](virtual-networks-static-private-ip-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="79333-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="79333-106">procedura di esempio Hello seguente prevede un ambiente semplice già creato.</span><span class="sxs-lookup"><span data-stu-id="79333-106">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="79333-107">Se si desidera passaggi hello toorun così come sono visualizzati in questo documento, innanzitutto compilare descritto nell'ambiente di test di hello [creare una rete virtuale](virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="79333-107">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="79333-108">Come toospecify un indirizzo IP privato statico di indirizzi durante la creazione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="79333-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="79333-109">una macchina virtuale denominata toocreate *DNS01* in hello *front-end* subnet di una rete virtuale denominata *TestVNet* con un indirizzo IP privato statico di *192.168.1.101*, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="79333-109">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="79333-110">Da un browser, passare toohttp://portal.azure.com e, se necessario, per accedere all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="79333-110">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="79333-111">Fare clic su **NEW** > **calcolo** > **Windows Server 2012 R2 Datacenter**, si noti che hello **selezionare un modello di distribuzione** elenco già illustrato **classico**, quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="79333-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="79333-113">In hello **creare VM** pannello, immettere il nome di hello di hello VM toobe creato (*DNS01* nello scenario di esempio), hello account amministratore locale e la password.</span><span class="sxs-lookup"><span data-stu-id="79333-113">In hello **Create VM** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password.</span></span>
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="79333-115">Fare clic su **Configurazione facoltativa** > **Rete** > **Rete virtuale**, poi fare clic su **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="79333-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="79333-116">Se **TestVNet** non è disponibile, assicurarsi che si sta eseguendo hello *centrale Usa* posizione e aver creato l'ambiente di testing hello descritto all'inizio di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="79333-116">If **TestVNet** is not available, make sure you are using hello *Central US* location and have created hello test environment described at hello beginning of this article.</span></span>
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="79333-118">In hello **rete** pannello, verificare che hello la subnet attualmente selezionata è *front-end*, quindi fare clic su **gli indirizzi IP**in **assegnazionedegliindirizziIP** fare clic su **statico**, quindi immettere *192.168.1.101* per **indirizzo IP** come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="79333-118">In hello **Network** blade, make sure hello subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="79333-120">Fare clic su **OK** in hello **gli indirizzi IP** pannello, quindi fare clic su **OK** in hello **rete** pannello e fare clic su **OK**in hello **configurazione facoltativa** blade.</span><span class="sxs-lookup"><span data-stu-id="79333-120">Click **OK** in hello **IP addresses** blade, then click **OK** in hello **Network** blade, and click **OK** in hello **Optional config** blade.</span></span>
7. <span data-ttu-id="79333-121">In hello **creare VM** pannello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="79333-121">In hello **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="79333-122">Si noti hello sezione riportata di seguito visualizzati nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="79333-122">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="79333-124">Come indirizzo IP privato statico tooretrieve informazioni sull'indirizzo di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="79333-124">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="79333-125">tooview hello private informazioni indirizzi IP statici per hello macchina virtuale creata con i passaggi di hello precedenti, eseguire i passaggi di hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="79333-125">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="79333-126">Dal portale di Azure di Azure hello, fare clic su **Esplora tutto** > **macchine virtuali (classico)** > **DNS01**  >   **Tutte le impostazioni** > **gli indirizzi IP** e notare hello assegnazione di indirizzi IP e l'indirizzo IP, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="79333-126">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice hello IP address assignment and IP address as seen below.</span></span>
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="79333-128">Come tooremove un indirizzo IP privato statico di indirizzi da una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="79333-128">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="79333-129">tooremove hello indirizzo IP privato statico dalla macchina virtuale creata in precedenza, hello procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="79333-129">tooremove hello static private IP address from hello VM created above, follow hello steps below.</span></span>

1. <span data-ttu-id="79333-130">Da hello **gli indirizzi IP** pannello illustrato in precedenza, fare clic su **dinamica** toohello destra **assegnazione di indirizzi IP**, quindi fare clic su **salvare**e quindi Fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="79333-130">From hello **IP addresses** blade shown above, click **Dynamic** toohello right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="79333-132">Come un indirizzo IP privato statico tooadd indirizzo tooan macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="79333-132">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="79333-133">tooadd un statico privato IP indirizzo toohello macchina virtuale creata seguendo i passaggi di hello sopra riportati, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="79333-133">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="79333-134">Da hello **gli indirizzi IP** pannello illustrato in precedenza, fare clic su **statico** toohello destra **assegnazione di indirizzi IP**.</span><span class="sxs-lookup"><span data-stu-id="79333-134">From hello **IP addresses** blade shown above, click **Static** toohello right of **IP address assignment**.</span></span>
2. <span data-ttu-id="79333-135">Digitare *192.168.1.101* per **indirizzo IP**, fare clic su **Salva**, quindi fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="79333-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79333-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="79333-136">Next steps</span></span>
* <span data-ttu-id="79333-137">Informazioni su [indirizzi IP pubblici riservati](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="79333-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="79333-138">Informazioni su [indirizzi IP pubblici a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="79333-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="79333-139">Consultare hello [API REST per IP riservato](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="79333-139">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>


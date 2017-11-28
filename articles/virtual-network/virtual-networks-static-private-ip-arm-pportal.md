---
title: indirizzi IP privati aaaConfigure per le macchine virtuali - portale di Azure | Documenti Microsoft
description: Informazioni su come indirizzi IP privati tooconfigure per macchine virtuali tramite hello portale di Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="3ef5d-103">Configurare gli indirizzi IP privati per una macchina virtuale utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3ef5d-103">Configure private IP addresses for a virtual machine using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ef5d-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3ef5d-104">Azure portal</span></span>](virtual-networks-static-private-ip-arm-pportal.md)
> * [<span data-ttu-id="3ef5d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ef5d-105">PowerShell</span></span>](virtual-networks-static-private-ip-arm-ps.md)
> * [<span data-ttu-id="3ef5d-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="3ef5d-106">Azure CLI</span></span>](virtual-networks-static-private-ip-arm-cli.md)
> * [<span data-ttu-id="3ef5d-107">Portale di Azure (classico)</span><span class="sxs-lookup"><span data-stu-id="3ef5d-107">Azure portal (Classic)</span></span>](virtual-networks-static-private-ip-classic-pportal.md)
> * <span data-ttu-id="3ef5d-108">[PowerShell (Classic)](virtual-networks-static-private-ip-classic-ps.md) (PowerShell (classico))</span><span class="sxs-lookup"><span data-stu-id="3ef5d-108">[PowerShell (Classic)](virtual-networks-static-private-ip-classic-ps.md)</span></span>
> * [<span data-ttu-id="3ef5d-109">Interfaccia della riga di comando di Azure (versione classica)</span><span class="sxs-lookup"><span data-stu-id="3ef5d-109">Azure CLI (Classic)</span></span>](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="3ef5d-110">Questo articolo descrive il modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-110">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="3ef5d-111">È anche possibile [gestire l'indirizzo IP privato statico in modello di distribuzione classica hello](virtual-networks-static-private-ip-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="3ef5d-111">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="3ef5d-112">procedura di esempio Hello seguente prevede un ambiente semplice già creato.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-112">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="3ef5d-113">Se si desidera passaggi hello toorun così come sono visualizzati in questo documento, innanzitutto compilare descritto nell'ambiente di test di hello [creare una rete virtuale](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="3ef5d-113">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-pportal.md).</span></span>

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a><span data-ttu-id="3ef5d-114">Come gli indirizzi toocreate una macchina virtuale per il testing di indirizzo IP privato statico</span><span class="sxs-lookup"><span data-stu-id="3ef5d-114">How toocreate a VM for testing static private IP addresses</span></span>
<span data-ttu-id="3ef5d-115">È possibile impostare un indirizzo IP privato statico durante la creazione di una macchina virtuale in modalità di distribuzione di gestione risorse di hello hello utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-115">You cannot set a static private IP address during hello creation of a VM in hello Resource Manager deployment mode by using hello Azure portal.</span></span> <span data-ttu-id="3ef5d-116">È necessario creare innanzitutto hello macchina virtuale, quindi impostare il relativo toobe IP privato statico.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-116">You must create hello VM first, tehn set its private IP toobe static.</span></span>

<span data-ttu-id="3ef5d-117">una macchina virtuale denominata toocreate *DNS01* in hello *front-end* subnet di una rete virtuale denominata *TestVNet*, attenersi alla procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-117">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet*, follow hello steps below.</span></span>

1. <span data-ttu-id="3ef5d-118">Da un browser, passare toohttp://portal.azure.com e, se necessario, per accedere all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-118">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="3ef5d-119">Fare clic su **NEW** > **calcolo** > **Windows Server 2012 R2 Datacenter**, si noti che hello **selezionare un modello di distribuzione** elenco già illustrato **Gestione risorse**, quindi fare clic su **crea**, come illustrato nella figura che segue hello.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-119">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Resource Manager**, and then click **Create**, as seen in hello figure below.</span></span>
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. <span data-ttu-id="3ef5d-121">In hello **nozioni di base** pannello, immettere il nome di hello di hello VM toobe creato (*DNS01* nello scenario di esempio), hello account amministratore locale e la password, come illustrato nella figura che segue hello.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-121">In hello **Basics** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password, as seen in hello figure below.</span></span>
   
    ![Pannello Nozioni di base](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. <span data-ttu-id="3ef5d-123">Verificare che hello **percorso** selezionato è *Stati Uniti centro*, quindi fare clic su **selezionare esistente** in **gruppo di risorse**, quindi fare clic su **Gruppo di risorse** nuovamente, quindi fare clic su *TestRG*, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-123">Make sure hello **Location** selected is *Central US*, then click **Select existing** under **Resource group**, then click **Resource group** again, then click *TestRG*, and then click **OK**.</span></span>
   
    ![Pannello Nozioni di base](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. <span data-ttu-id="3ef5d-125">In hello **scegliere una dimensione** pannello seleziona **A1 Standard**, quindi fare clic su **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-125">In hello **Choose a size** blade, select **A1 Standard**, and then click **Select**.</span></span>
   
    ![Pannello Scegliere una dimensione](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. <span data-ttu-id="3ef5d-127">Nel **impostazioni** pannello, vengono impostate hello assicurarsi di verificare le proprietà seguenti vengono impostate con i valori hello seguenti e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-127">In teh **Settings** blade, make sure hello following properties are set are set with hello values below, and then click **OK**.</span></span>
   
    <span data-ttu-id="3ef5d-128">-**Account di archiviazione**: *vnetstorage*</span><span class="sxs-lookup"><span data-stu-id="3ef5d-128">-**Storage account**: *vnetstorage*</span></span>
   
   * <span data-ttu-id="3ef5d-129">**Rete**: *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="3ef5d-129">**Network**: *TestVNet*</span></span>
   * <span data-ttu-id="3ef5d-130">**Subnet**: *FrontEnd*</span><span class="sxs-lookup"><span data-stu-id="3ef5d-130">**Subnet**: *FrontEnd*</span></span>
     
     ![Pannello Scegliere una dimensione](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. <span data-ttu-id="3ef5d-132">In hello **riepilogo** pannello, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-132">In hello **Summary** blade, click **OK**.</span></span> <span data-ttu-id="3ef5d-133">Si noti hello sezione riportata di seguito visualizzati nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-133">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="3ef5d-135">Come indirizzo IP privato statico tooretrieve informazioni sull'indirizzo di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3ef5d-135">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="3ef5d-136">tooview hello private informazioni indirizzi IP statici per hello macchina virtuale creata con i passaggi di hello precedenti, eseguire i passaggi di hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-136">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="3ef5d-137">Dal portale di Azure di Azure hello, fare clic su **Esplora tutto** > **macchine virtuali** > **DNS01** > **tutti impostazioni** > **interfacce di rete** e quindi fare clic su hello solo l'interfaccia di rete elencata.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-137">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines** > **DNS01** > **All settings** > **Network interfaces** and then click on hello only network interface listed.</span></span>
   
    ![Distribuzione di un riquadro VM](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. <span data-ttu-id="3ef5d-139">In hello **interfaccia di rete** pannello, fare clic su **tutte le impostazioni** > **gli indirizzi IP** e notifica hello **assegnazione** e **Indirizzo IP** valori.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-139">In hello **Network interface** blade, click **All settings** > **IP addresses** and notice hello **Assignment** and **IP address** values.</span></span>
   
    ![Distribuzione di un riquadro VM](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="3ef5d-141">Come un indirizzo IP privato statico tooadd indirizzo tooan macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="3ef5d-141">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="3ef5d-142">tooadd un statico privato IP indirizzo toohello macchina virtuale creata seguendo i passaggi di hello sopra riportati, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="3ef5d-142">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="3ef5d-143">Da hello **gli indirizzi IP** pannello illustrato in precedenza, fare clic su **statico** in **assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-143">From hello **IP addresses** blade shown above, click **Static** under **Assignment**.</span></span>
2. <span data-ttu-id="3ef5d-144">Digitare *192.168.1.101* per **Indirizzo IP** e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-144">Type *192.168.1.101* for **IP address**, and then click **Save**.</span></span>
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> <span data-ttu-id="3ef5d-146">Se dopo aver fatto clic **salvare** l'assegnazione di hello è ancora impostato troppo**dinamica**, significa che l'indirizzo IP hello digitato è già in uso.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-146">If after clicking **Save** you notice that hello assignment is still set too**Dynamic**, it means that hello IP address you typed is already in use.</span></span> <span data-ttu-id="3ef5d-147">Provare un indirizzo IP diverso.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-147">Try a different IP address.</span></span>
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="3ef5d-148">Come tooremove un indirizzo IP privato statico di indirizzi da una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3ef5d-148">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="3ef5d-149">tooremove hello indirizzo IP privato statico dalla macchina virtuale creata in precedenza, hello completare hello seguente passaggio:</span><span class="sxs-lookup"><span data-stu-id="3ef5d-149">tooremove hello static private IP address from hello VM created above, complete hello following step:</span></span>

<span data-ttu-id="3ef5d-150">Da hello **gli indirizzi IP** pannello illustrato in precedenza, fare clic su **dinamica** in **assegnazione**, quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="3ef5d-150">From hello **IP addresses** blade shown above, click **Dynamic** under **Assignment**, and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ef5d-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3ef5d-151">Next steps</span></span>
* <span data-ttu-id="3ef5d-152">Informazioni su [indirizzi IP pubblici riservati](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="3ef5d-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="3ef5d-153">Informazioni su [indirizzi IP pubblici a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="3ef5d-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="3ef5d-154">Consultare hello [API REST per IP riservato](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ef5d-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>


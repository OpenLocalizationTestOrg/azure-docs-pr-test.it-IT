---
title: Avvio rapido - aaaAzure Crea portale VM di Windows | Documenti Microsoft
description: Avvio rapido in Azure - Creare un portale di VM Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5646ad51244db6d214c0121d1f7cc45c59f9a78b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="d8bd9-103">Creare una macchina virtuale Windows con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d8bd9-103">Create a Windows virtual machine with hello Azure portal</span></span>

<span data-ttu-id="d8bd9-104">Macchine virtuali di Azure può essere create tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-104">Azure virtual machines can be created through hello Azure portal.</span></span> <span data-ttu-id="d8bd9-105">Questo metodo fornisce un'interfaccia utente basata sul browser per la creazione e la configurazione delle macchine virtuali e di tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="d8bd9-106">Questa procedura di avvio rapido tramite la creazione di una macchina virtuale e l'installazione di un server Web in hello VM.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-106">This Quickstart steps through creating a virtual machine and installing a webserver on hello VM.</span></span>

<span data-ttu-id="d8bd9-107">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="d8bd9-108">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="d8bd9-108">Log in tooAzure</span></span>

<span data-ttu-id="d8bd9-109">Accedi toohello portale di Azure all'indirizzo http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-109">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="d8bd9-110">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="d8bd9-110">Create virtual machine</span></span>

1. <span data-ttu-id="d8bd9-111">Fare clic su hello **New** pulsante disponibile nella hello angolo superiore sinistro del portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-111">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="d8bd9-112">Selezionare **Calcolo** e quindi **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-112">Select **Compute**, and then select **Windows Server 2016 Datacenter**.</span></span> 

3. <span data-ttu-id="d8bd9-113">Immettere le informazioni di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-113">Enter hello virtual machine information.</span></span> <span data-ttu-id="d8bd9-114">nome utente Hello e la password immessa in questo caso è toolog utilizzati nella macchina virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="d8bd9-115">Al termine fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-115">When complete, click **OK**.</span></span>

    ![Immettere le informazioni di base di una macchina virtuale nel pannello portale hello](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. <span data-ttu-id="d8bd9-117">Selezionare una dimensione per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-117">Select a size for hello VM.</span></span> <span data-ttu-id="d8bd9-118">Selezionare altre dimensioni, toosee **visualizzare tutti** o modificare hello **il tipo di disco supportati** filtro.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-118">toosee more sizes, select **View all** or change hello **Supported disk type** filter.</span></span> 

    ![Screenshot che mostra le dimensioni delle VM](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. <span data-ttu-id="d8bd9-120">Nel pannello impostazioni hello, mantenere i valori predefiniti di hello e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-120">On hello settings blade, keep hello defaults and click **OK**.</span></span>

6. <span data-ttu-id="d8bd9-121">Nella pagina Riepilogo hello, fare clic su **Ok** distribuzione della macchina virtuale toostart hello.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-121">On hello summary page, click **Ok** toostart hello virtual machine deployment.</span></span>

7. <span data-ttu-id="d8bd9-122">Hello VM sarà bloccato toohello dashboard del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-122">hello VM will be pinned toohello Azure portal dashboard.</span></span> <span data-ttu-id="d8bd9-123">Una volta completata la distribuzione di hello, verrà aperta automaticamente pannello riepilogo di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-123">Once hello deployment has completed, hello VM summary blade automatically opens.</span></span>


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="d8bd9-124">Connettere la macchina toovirtual</span><span class="sxs-lookup"><span data-stu-id="d8bd9-124">Connect toovirtual machine</span></span>

<span data-ttu-id="d8bd9-125">Creare una macchina virtuale di toohello connessione desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-125">Create a remote desktop connection toohello virtual machine.</span></span>

1. <span data-ttu-id="d8bd9-126">Fare clic su hello **Connetti** pulsante sulla proprietà della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-126">Click hello **Connect** button on hello virtual machine properties.</span></span> <span data-ttu-id="d8bd9-127">Verrà creato e scaricato un file Remote Desktop Protocol, con estensione rdp.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-127">A Remote Desktop Protocol file (.rdp file) is created and downloaded.</span></span>

    ![Portale 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="d8bd9-129">tooconnect tooyour macchina virtuale, aprire hello scaricato il file RDP.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-129">tooconnect tooyour VM, open hello downloaded RDP file.</span></span> <span data-ttu-id="d8bd9-130">Se richiesto, fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-130">If prompted, click **Connect**.</span></span> <span data-ttu-id="d8bd9-131">In un Mac, è necessario un client RDP come questo [Client Desktop remoto](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) da hello Mac App Store.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-131">On a Mac, you need an RDP client such as this [Remote Desktop Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) from hello Mac App Store.</span></span>

3. <span data-ttu-id="d8bd9-132">Immettere nome utente hello e la password specificata durante la creazione della macchina virtuale hello, quindi fare clic su **Ok**.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-132">Enter hello user name and password you specified when creating hello virtual machine, then click **Ok**.</span></span>

4. <span data-ttu-id="d8bd9-133">Si potrebbe ricevere un avviso del certificato durante il processo di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-133">You may receive a certificate warning during hello sign-in process.</span></span> <span data-ttu-id="d8bd9-134">Fare clic su **Sì** o **continua** tooproceed con connessione hello.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-134">Click **Yes** or **Continue** tooproceed with hello connection.</span></span>


## <a name="install-iis-using-powershell"></a><span data-ttu-id="d8bd9-135">Installare IIS tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8bd9-135">Install IIS using PowerShell</span></span>

<span data-ttu-id="d8bd9-136">Nella macchina virtuale hello, avviare una sessione di PowerShell ed eseguire hello successivo comando tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-136">On hello virtual machine, start a PowerShell session and run hello following command tooinstall IIS.</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="d8bd9-137">Al termine, uscire dalla sessione RDP hello e restituire le proprietà della VM hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-137">When done, exit hello RDP session and return hello VM properties in hello Azure portal.</span></span>

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="d8bd9-138">Aprire la porta 80 per il traffico Web</span><span class="sxs-lookup"><span data-stu-id="d8bd9-138">Open port 80 for web traffic</span></span> 

<span data-ttu-id="d8bd9-139">Un gruppo di sicurezza di rete (NSG) consente il traffico in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-139">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="d8bd9-140">Quando una macchina virtuale viene creata dal portale di Azure hello, viene creata una regola in entrata sulla porta 3389 per le connessioni RDP.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-140">When a VM is created from hello Azure portal, an inbound rule is created on port 3389 for RDP connections.</span></span> <span data-ttu-id="d8bd9-141">Poiché questa macchina virtuale ospita un server Web, una regola di gruppo deve toobe creato per la porta 80.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-141">Because this VM hosts a webserver, an NSG rule needs toobe created for port 80.</span></span>

1. <span data-ttu-id="d8bd9-142">Nella macchina virtuale hello, fare clic sul nome hello di hello **gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-142">On hello virtual machine, click hello name of hello **Resource group**.</span></span>
2. <span data-ttu-id="d8bd9-143">Seleziona hello **il gruppo di sicurezza di rete**.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-143">Select hello **network security group**.</span></span> <span data-ttu-id="d8bd9-144">Hello gruppo può essere identificato utilizzando hello **tipo** colonna.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-144">hello NSG can be identified using hello **Type** column.</span></span> 
3. <span data-ttu-id="d8bd9-145">Nel menu a sinistra di hello, in impostazioni, fare clic su **sicurezza regole connessioni in entrata**.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-145">On hello left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="d8bd9-146">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-146">Click on **Add**.</span></span>
5. <span data-ttu-id="d8bd9-147">In **Nome** digitare **http**.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-147">In **Name**, type **http**.</span></span> <span data-ttu-id="d8bd9-148">Assicurarsi che **intervallo di porte** è impostato too80 e **azione** è troppo**Consenti**.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-148">Make sure **Port range** is set too80 and **Action** is set too**Allow**.</span></span> 
6. <span data-ttu-id="d8bd9-149">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-149">Click **OK**.</span></span>


## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="d8bd9-150">Hello Visualizza la pagina iniziale di IIS</span><span class="sxs-lookup"><span data-stu-id="d8bd9-150">View hello IIS welcome page</span></span>

<span data-ttu-id="d8bd9-151">Con IIS installato e la porta 80 aprire tooyour VM, server Web hello è ora possibile accedere da hello internet.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-151">With IIS installed, and port 80 open tooyour VM, hello webserver can now be accessed from hello internet.</span></span> <span data-ttu-id="d8bd9-152">Aprire un web browser e immettere l'indirizzo IP pubblico hello di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-152">Open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="d8bd9-153">indirizzo IP pubblico Hello è reperibile nel pannello VM hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-153">hello public IP address can be found on hello VM blade in hello Azure portal.</span></span>

![Sito IIS predefinito](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="d8bd9-155">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="d8bd9-155">Clean up resources</span></span>

<span data-ttu-id="d8bd9-156">Quando non è più necessario, eliminare il gruppo di risorse hello, macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-156">When no longer needed, delete hello resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="d8bd9-157">toodo in tal caso, selezionare il gruppo di risorse di hello dal pannello della macchina virtuale hello e fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-157">toodo so, select hello resource group from hello virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8bd9-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d8bd9-158">Next steps</span></span>

<span data-ttu-id="d8bd9-159">In questa guida introduttiva è stata distribuita una macchina virtuale semplice, è stata creata una regola del gruppo di sicurezza di rete ed è stato installato un server Web.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-159">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="d8bd9-160">toolearn informazioni sulle macchine virtuali di Azure, continuare l'esercitazione toohello per le macchine virtuali di Windows.</span><span class="sxs-lookup"><span data-stu-id="d8bd9-160">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d8bd9-161">Esercitazioni per le macchine virtuali di Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="d8bd9-161">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)

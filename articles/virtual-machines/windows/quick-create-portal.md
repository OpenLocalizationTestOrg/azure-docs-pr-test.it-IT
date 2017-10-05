---
title: Avvio rapido in Azure - Creare un portale di VM Windows | Microsoft Docs
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
ms.openlocfilehash: 31ac18add9c3fd956e0d37b1e0c1a510265c22e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-windows-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="6c07c-103">Creare una macchina virtuale Windows con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6c07c-103">Create a Windows virtual machine with the Azure portal</span></span>

<span data-ttu-id="6c07c-104">È possibile creare macchine virtuali di Azure tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c07c-104">Azure virtual machines can be created through the Azure portal.</span></span> <span data-ttu-id="6c07c-105">Questo metodo fornisce un'interfaccia utente basata sul browser per la creazione e la configurazione delle macchine virtuali e di tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="6c07c-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="6c07c-106">Questa guida introduttiva illustra la creazione di una macchina virtuale e l'installazione di un server Web nella VM.</span><span class="sxs-lookup"><span data-stu-id="6c07c-106">This Quickstart steps through creating a virtual machine and installing a webserver on the VM.</span></span>

<span data-ttu-id="6c07c-107">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="6c07c-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="6c07c-108">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="6c07c-108">Log in to Azure</span></span>

<span data-ttu-id="6c07c-109">Accedere al portale di Azure all'indirizzo http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="6c07c-109">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="6c07c-110">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="6c07c-110">Create virtual machine</span></span>

1. <span data-ttu-id="6c07c-111">Fare clic sul pulsante **Nuovo** nell'angolo superiore sinistro del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c07c-111">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="6c07c-112">Selezionare **Calcolo** e quindi **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="6c07c-112">Select **Compute**, and then select **Windows Server 2016 Datacenter**.</span></span> 

3. <span data-ttu-id="6c07c-113">Immettere le informazioni relative alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6c07c-113">Enter the virtual machine information.</span></span> <span data-ttu-id="6c07c-114">Il nome utente e la password immessi in questo modulo verranno usati per accedere alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6c07c-114">The user name and password entered here is used to log in to the virtual machine.</span></span> <span data-ttu-id="6c07c-115">Al termine fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c07c-115">When complete, click **OK**.</span></span>

    ![Immettere le informazioni di base sulla VM nel pannello del portale](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. <span data-ttu-id="6c07c-117">Selezionare una dimensione per la VM.</span><span class="sxs-lookup"><span data-stu-id="6c07c-117">Select a size for the VM.</span></span> <span data-ttu-id="6c07c-118">Per visualizzare altre dimensioni, selezionare **Visualizza tutto** o modificare il filtro **Supported disk type** (Tipo di disco supportato).</span><span class="sxs-lookup"><span data-stu-id="6c07c-118">To see more sizes, select **View all** or change the **Supported disk type** filter.</span></span> 

    ![Screenshot che mostra le dimensioni delle VM](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. <span data-ttu-id="6c07c-120">Nel pannello delle impostazioni mantenere le impostazioni predefinite e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c07c-120">On the settings blade, keep the defaults and click **OK**.</span></span>

6. <span data-ttu-id="6c07c-121">Nella pagina del riepilogo fare clic su **OK** per avviare la distribuzione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6c07c-121">On the summary page, click **Ok** to start the virtual machine deployment.</span></span>

7. <span data-ttu-id="6c07c-122">La macchina virtuale verrà aggiunta al dashboard del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c07c-122">The VM will be pinned to the Azure portal dashboard.</span></span> <span data-ttu-id="6c07c-123">Una volta completata la distribuzione verrà automaticamente aperto il pannello di riepilogo della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6c07c-123">Once the deployment has completed, the VM summary blade automatically opens.</span></span>


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="6c07c-124">Connettersi alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="6c07c-124">Connect to virtual machine</span></span>

<span data-ttu-id="6c07c-125">Creare una connessione Desktop remoto alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6c07c-125">Create a remote desktop connection to the virtual machine.</span></span>

1. <span data-ttu-id="6c07c-126">Fare clic sul pulsante **Connetti** nelle proprietà della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6c07c-126">Click the **Connect** button on the virtual machine properties.</span></span> <span data-ttu-id="6c07c-127">Verrà creato e scaricato un file Remote Desktop Protocol, con estensione rdp.</span><span class="sxs-lookup"><span data-stu-id="6c07c-127">A Remote Desktop Protocol file (.rdp file) is created and downloaded.</span></span>

    ![Portale 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="6c07c-129">Per connettersi alla VM, aprire il file RDP scaricato.</span><span class="sxs-lookup"><span data-stu-id="6c07c-129">To connect to your VM, open the downloaded RDP file.</span></span> <span data-ttu-id="6c07c-130">Se richiesto, fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="6c07c-130">If prompted, click **Connect**.</span></span> <span data-ttu-id="6c07c-131">In Mac, è necessario un client RDP come questo [client Desktop remoto](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) disponibile nel Mac App Store.</span><span class="sxs-lookup"><span data-stu-id="6c07c-131">On a Mac, you need an RDP client such as this [Remote Desktop Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) from the Mac App Store.</span></span>

3. <span data-ttu-id="6c07c-132">Immettere il nome utente e la password specificati al momento della creazione della macchina virtuale e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c07c-132">Enter the user name and password you specified when creating the virtual machine, then click **Ok**.</span></span>

4. <span data-ttu-id="6c07c-133">Durante il processo di accesso potrebbe essere visualizzato un avviso relativo al certificato.</span><span class="sxs-lookup"><span data-stu-id="6c07c-133">You may receive a certificate warning during the sign-in process.</span></span> <span data-ttu-id="6c07c-134">Fare clic su **Sì** o **Continua** per procedere con la connessione.</span><span class="sxs-lookup"><span data-stu-id="6c07c-134">Click **Yes** or **Continue** to proceed with the connection.</span></span>


## <a name="install-iis-using-powershell"></a><span data-ttu-id="6c07c-135">Installare IIS tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c07c-135">Install IIS using PowerShell</span></span>

<span data-ttu-id="6c07c-136">Nella macchina virtuale avviare una sessione di PowerShell ed eseguire questo comando per installare IIS.</span><span class="sxs-lookup"><span data-stu-id="6c07c-136">On the virtual machine, start a PowerShell session and run the following command to install IIS.</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="6c07c-137">Al termine chiudere la sessione RDP e tornare alle proprietà della macchina virtuale nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c07c-137">When done, exit the RDP session and return the VM properties in the Azure portal.</span></span>

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="6c07c-138">Aprire la porta 80 per il traffico Web</span><span class="sxs-lookup"><span data-stu-id="6c07c-138">Open port 80 for web traffic</span></span> 

<span data-ttu-id="6c07c-139">Un gruppo di sicurezza di rete (NSG) consente il traffico in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="6c07c-139">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="6c07c-140">Quando si crea una VM nel portale di Azure, viene creata una regola in ingresso sulla porta 3389 per le connessioni RDP.</span><span class="sxs-lookup"><span data-stu-id="6c07c-140">When a VM is created from the Azure portal, an inbound rule is created on port 3389 for RDP connections.</span></span> <span data-ttu-id="6c07c-141">Questa VM ospita un server Web, quindi è necessario creare una regola del gruppo di sicurezza di rete per la porta 80.</span><span class="sxs-lookup"><span data-stu-id="6c07c-141">Because this VM hosts a webserver, an NSG rule needs to be created for port 80.</span></span>

1. <span data-ttu-id="6c07c-142">Nella macchina virtuale fare clic sul nome del **gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="6c07c-142">On the virtual machine, click the name of the **Resource group**.</span></span>
2. <span data-ttu-id="6c07c-143">Selezionare il **gruppo di sicurezza di rete**.</span><span class="sxs-lookup"><span data-stu-id="6c07c-143">Select the **network security group**.</span></span> <span data-ttu-id="6c07c-144">Il gruppo di sicurezza di rete può essere identificato tramite la colonna **Tipo**.</span><span class="sxs-lookup"><span data-stu-id="6c07c-144">The NSG can be identified using the **Type** column.</span></span> 
3. <span data-ttu-id="6c07c-145">Nel menu a sinistra fare clic su **Regole di sicurezza in ingresso** in Impostazioni.</span><span class="sxs-lookup"><span data-stu-id="6c07c-145">On the left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="6c07c-146">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6c07c-146">Click on **Add**.</span></span>
5. <span data-ttu-id="6c07c-147">In **Nome** digitare **http**.</span><span class="sxs-lookup"><span data-stu-id="6c07c-147">In **Name**, type **http**.</span></span> <span data-ttu-id="6c07c-148">Assicurarsi che l'opzione **Intervallo di porte** sia impostata su 80 e l'opzione **Azione** sia impostata su **Consenti**.</span><span class="sxs-lookup"><span data-stu-id="6c07c-148">Make sure **Port range** is set to 80 and **Action** is set to **Allow**.</span></span> 
6. <span data-ttu-id="6c07c-149">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c07c-149">Click **OK**.</span></span>


## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="6c07c-150">Visualizzare la pagina iniziale di IIS</span><span class="sxs-lookup"><span data-stu-id="6c07c-150">View the IIS welcome page</span></span>

<span data-ttu-id="6c07c-151">Con IIS installato e la porta 80 aperta per la macchina virtuale, è ora possibile accedere al server Web da Internet.</span><span class="sxs-lookup"><span data-stu-id="6c07c-151">With IIS installed, and port 80 open to your VM, the webserver can now be accessed from the internet.</span></span> <span data-ttu-id="6c07c-152">Aprire un Web browser e immettere l'indirizzo IP pubblico della VM.</span><span class="sxs-lookup"><span data-stu-id="6c07c-152">Open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="6c07c-153">L'indirizzo IP pubblico è indicato nel pannello della macchina virtuale nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c07c-153">the public IP address can be found on the VM blade in the Azure portal.</span></span>

![Sito IIS predefinito](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="6c07c-155">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="6c07c-155">Clean up resources</span></span>

<span data-ttu-id="6c07c-156">Quando non serve più, eliminare il gruppo di risorse e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="6c07c-156">When no longer needed, delete the resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="6c07c-157">A tale scopo selezionare il gruppo di risorse nel pannello della macchina virtuale e fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="6c07c-157">To do so, select the resource group from the virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c07c-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6c07c-158">Next steps</span></span>

<span data-ttu-id="6c07c-159">In questa guida introduttiva è stata distribuita una macchina virtuale semplice, è stata creata una regola del gruppo di sicurezza di rete ed è stato installato un server Web.</span><span class="sxs-lookup"><span data-stu-id="6c07c-159">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="6c07c-160">Per altre informazioni sulle macchine virtuali di Azure, passare all'esercitazione per le VM di Windows.</span><span class="sxs-lookup"><span data-stu-id="6c07c-160">To learn more about Azure virtual machines, continue to the tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6c07c-161">Esercitazioni per le macchine virtuali di Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="6c07c-161">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)

---
title: Installare IIS nella prima VM Windows | Microsoft Docs
description: Sperimentare l'uso della prima macchina virtuale Windows tramite l'installazione di IIS e l'apertura della porta 80 con il portale di Azure.
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: b11ce1eab0c26a802c31bc418cdf725cbc4fba30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="67f59-103">Sperimentare l'installazione di un ruolo in una VM Windows</span><span class="sxs-lookup"><span data-stu-id="67f59-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="67f59-104">Dopo aver creato e reso operativa la prima macchina virtuale (VM), è possibile dedicarsi all'installazione di software e servizi.</span><span class="sxs-lookup"><span data-stu-id="67f59-104">Once you have your first virtual machine (VM) up and running, you can move on to installing software and services.</span></span> <span data-ttu-id="67f59-105">Per questa esercitazione, verrà usato Server Manager nella VM Windows Server per installare IIS.</span><span class="sxs-lookup"><span data-stu-id="67f59-105">For this tutorial, we are going to use Server Manager on the Windows Server VM to install IIS.</span></span> <span data-ttu-id="67f59-106">Si creerà quindi un gruppo di sicurezza di rete tramite il portale di Azure per aprire la porta 80 al traffico IIS.</span><span class="sxs-lookup"><span data-stu-id="67f59-106">Then, we will create a Network Security Group (NSG) using the Azure portal to open port 80 to IIS traffic.</span></span> 

<span data-ttu-id="67f59-107">Se non è ancora stata creata la prima macchina virtuale, tornare all'esercitazione [Creare la prima macchina virtuale Windows nel portale di Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) prima di continuare con questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="67f59-107">If you haven't already created your first VM, you should go back to [Create your first Windows virtual machine in the Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-the-vm-is-running"></a><span data-ttu-id="67f59-108">Assicurarsi che la VM sia in esecuzione</span><span class="sxs-lookup"><span data-stu-id="67f59-108">Make sure the VM is running</span></span>
1. <span data-ttu-id="67f59-109">Aprire il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="67f59-109">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="67f59-110">Scegliere **Macchine virtuali**dal menu Hub.</span><span class="sxs-lookup"><span data-stu-id="67f59-110">On the hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="67f59-111">Selezionare la macchina virtuale dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="67f59-111">Select the virtual machine from the list.</span></span>
3. <span data-ttu-id="67f59-112">Se lo stato è **Arrestato (deallocato)**, fare clic sul pulsante **Avvia** nel pannello **Informazioni di base** della VM.</span><span class="sxs-lookup"><span data-stu-id="67f59-112">If the status is **Stopped (Deallocated)**, click the **Start** button on the **Essentials** blade of the VM.</span></span> <span data-ttu-id="67f59-113">Quando lo stato indica che la macchina virtuale è **In esecuzione**, è possibile passare al passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="67f59-113">If the status is **Running**, you can move on to the next step.</span></span>

## <a name="connect-to-the-virtual-machine-and-sign-in"></a><span data-ttu-id="67f59-114">Connettersi alla macchina virtuale ed eseguire l'accesso</span><span class="sxs-lookup"><span data-stu-id="67f59-114">Connect to the virtual machine and sign in</span></span>
1. <span data-ttu-id="67f59-115">Scegliere **Macchine virtuali**dal menu Hub.</span><span class="sxs-lookup"><span data-stu-id="67f59-115">On the hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="67f59-116">Selezionare la macchina virtuale dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="67f59-116">Select the virtual machine from the list.</span></span>
2. <span data-ttu-id="67f59-117">Nel pannello della macchina virtuale fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="67f59-117">On the blade for the virtual machine, click **Connect**.</span></span> <span data-ttu-id="67f59-118">Verrà creato e scaricato un file Remote Desktop Protocol (file con estensione rdp), che è analogo a un collegamento per la connessione alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67f59-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut to connect to your machine.</span></span> <span data-ttu-id="67f59-119">È consigliabile salvare il file sul desktop per semplificare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="67f59-119">You might want to save the file to your desktop for easy access.</span></span> <span data-ttu-id="67f59-120">**Aprire** questo file per connettersi alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67f59-120">**Open** this file to connect to your VM.</span></span>
   
    ![Screenshot del portale di Azure che illustra come connettersi alla VM](./media/hero-role/connect.png)
3. <span data-ttu-id="67f59-122">Verrà visualizzato un avviso che indica che l'autore del file RDP è sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="67f59-122">You get a warning that the .rdp is from an unknown publisher.</span></span> <span data-ttu-id="67f59-123">Si tratta di una situazione normale.</span><span class="sxs-lookup"><span data-stu-id="67f59-123">This is normal.</span></span> <span data-ttu-id="67f59-124">Nella finestra di Desktop remoto, fare clic su **Connetti** per continuare.</span><span class="sxs-lookup"><span data-stu-id="67f59-124">In the Remote Desktop window, click **Connect** to continue.</span></span>
   
    ![Screenshot di un avviso relativo a un autore sconosciuto](./media/hero-role/rdp-warn.png)
4. <span data-ttu-id="67f59-126">Nella finestra Sicurezza di Windows immettere il nome utente e la password per l'account locale creato quando è stata creata la VM.</span><span class="sxs-lookup"><span data-stu-id="67f59-126">In the Windows Security window, type the username and password for the local account that you created when you created the VM.</span></span> <span data-ttu-id="67f59-127">Il nome utente viene immesso come *nomevm*&#92;*nomeutente*. Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="67f59-127">The username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![Screenshot relativo all'immissione del nome della VM, del nome utente e della password](./media/hero-role/credentials.png)
5. <span data-ttu-id="67f59-129">Verrà visualizzato un avviso che indica che non è possibile verificare il certificato.</span><span class="sxs-lookup"><span data-stu-id="67f59-129">You get a warning that the certificate cannot be verified.</span></span> <span data-ttu-id="67f59-130">Si tratta di una situazione normale.</span><span class="sxs-lookup"><span data-stu-id="67f59-130">This is normal.</span></span> <span data-ttu-id="67f59-131">Fare clic su **Sì** per verificare l'identità della macchina virtuale e terminare la procedura di accesso.</span><span class="sxs-lookup"><span data-stu-id="67f59-131">Click **Yes** to verify the identity of the virtual machine and finish logging on.</span></span>
   
   ![Screenshot che mostra un messaggio sulla verifica dell'identità della VM](./media/hero-role/cert-warning.png)

<span data-ttu-id="67f59-133">In caso di problemi quando si cerca di eseguire la connessione, vedere [Risolvere i problemi di connessioni Desktop remoto a una macchina virtuale di Azure che esegue Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67f59-133">If you run in to trouble when you try to connect, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="67f59-134">Installare IIS nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="67f59-134">Install IIS on your VM</span></span>
<span data-ttu-id="67f59-135">Dopo aver eseguito l'accesso alla macchina virtuale, verrà installato un ruolo del server che permette di fare ulteriori prove.</span><span class="sxs-lookup"><span data-stu-id="67f59-135">Now that you are logged in to the VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="67f59-136">Aprire **Server Manager** se non è già aperto.</span><span class="sxs-lookup"><span data-stu-id="67f59-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="67f59-137">Fare clic sul menu **Start** e su **Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="67f59-137">Click the **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="67f59-138">In **Server Manager** selezionare **Server locale** nel riquadro a sinistra.</span><span class="sxs-lookup"><span data-stu-id="67f59-138">In **Server Manager**, select **Local Server** from the left pane.</span></span> 
3. <span data-ttu-id="67f59-139">Nel menu selezionare **Gestione** > **Aggiungi ruoli e funzionalità**.</span><span class="sxs-lookup"><span data-stu-id="67f59-139">In the menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="67f59-140">Nella pagina **Tipo di installazione** dell'Aggiunta guidata ruoli e funzionalità scegliere **Installazione basata su ruoli o basata su funzionalità** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="67f59-140">In the Add Roles and Features Wizard, on the **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![Screenshot che illustra la scheda Tipo di installazione dell'Aggiunta guidata ruoli e funzionalità](./media/hero-role/role-wizard.png)
5. <span data-ttu-id="67f59-142">Selezionare la macchina virtuale dal pool di server e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="67f59-142">Select the VM from the server pool and click **Next**.</span></span>
6. <span data-ttu-id="67f59-143">Nella pagina **Ruoli server** selezionare **Server Web (IIS)**.</span><span class="sxs-lookup"><span data-stu-id="67f59-143">On the **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![Screenshot che illustra la scheda Ruoli server dell'Aggiunta guidata ruoli e funzionalità](./media/hero-role/add-iis.png)
7. <span data-ttu-id="67f59-145">Nella finestra popup sull'aggiunta di funzionalità necessarie per IIS accertarsi che sia selezionata l'opzione **Includi strumenti di gestione**, quindi fare clic su **Aggiungi funzionalità**.</span><span class="sxs-lookup"><span data-stu-id="67f59-145">In the pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="67f59-146">Quando si chiude la finestra popup, fare clic su **Avanti** nella procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="67f59-146">When the pop-up closes, click **Next** in the wizard.</span></span>
   
    ![Screenshot che illustra la finestra popup per la conferma dell'aggiunta del ruolo IIS](./media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="67f59-148">Nella pagina delle funzionalità fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="67f59-148">On the features page, click **Next**.</span></span>
9. <span data-ttu-id="67f59-149">Nella pagina **Ruolo Server Web (IIS)** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="67f59-149">On the **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="67f59-150">Nella pagina **Servizi ruolo** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="67f59-150">On the **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="67f59-151">Nella pagina **Conferma** fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="67f59-151">On the **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="67f59-152">Al termine dell'installazione fare clic su **Chiudi** nella procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="67f59-152">When the installation is complete, click **Close** on the wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="67f59-153">Aprire la porta 80</span><span class="sxs-lookup"><span data-stu-id="67f59-153">Open port 80</span></span>
<span data-ttu-id="67f59-154">Perché la macchina virtuale possa accettare il traffico in ingresso attraverso porta 80, è necessario aggiungere una regola in ingresso al gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="67f59-154">In order for your VM to accept inbound traffic over port 80, you need to add an inbound rule to the network security group.</span></span> 

1. <span data-ttu-id="67f59-155">Aprire il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="67f59-155">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="67f59-156">In **Macchine virtuali** selezionare la VM creata.</span><span class="sxs-lookup"><span data-stu-id="67f59-156">In **Virtual machines** select the VM that you created.</span></span>
3. <span data-ttu-id="67f59-157">Nelle impostazioni della macchina virtuale scegliere **Interfacce di rete** e quindi selezionare l'interfaccia di rete esistente.</span><span class="sxs-lookup"><span data-stu-id="67f59-157">In the virtual machines settings, select **Network interfaces** and then select the existing network interface.</span></span>
   
    ![Screenshot che illustra l'impostazione della macchina virtuale per le interfacce di rete](./media/hero-role/network-interface.png)
4. <span data-ttu-id="67f59-159">Nel pannello **Informazioni di base** per l'interfaccia di rete fare clic sul **Gruppo di sicurezza di rete**.</span><span class="sxs-lookup"><span data-stu-id="67f59-159">In **Essentials** for the network interface, click the **Network security group**.</span></span>
   
    ![Screenshot che illustra la sezione Informazioni di base per l'interfaccia di rete](./media/hero-role/select-nsg.png)
5. <span data-ttu-id="67f59-161">Nel pannello **Informazioni di base** per il gruppo di sicurezza di rete dovrebbe essere già presente una regola in ingresso predefinita per **default-allow-rdp**, che consente di accedere alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67f59-161">In the **Essentials** blade for the NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you to log in to the VM.</span></span> <span data-ttu-id="67f59-162">Aggiungere un'altra regola in ingresso per consentire il traffico IIS.</span><span class="sxs-lookup"><span data-stu-id="67f59-162">You will add another inbound rule to allow IIS traffic.</span></span> <span data-ttu-id="67f59-163">Fare clic su **Regole di sicurezza in ingresso**.</span><span class="sxs-lookup"><span data-stu-id="67f59-163">Click **Inbound security rule**.</span></span>
   
    ![Screenshot che illustra la sezione Informazioni di base per il gruppo di sicurezza di rete](./media/hero-role/inbound.png)
6. <span data-ttu-id="67f59-165">In **Regole di sicurezza in ingresso** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="67f59-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![Screenshot che mostra il pulsante per l'aggiunta di una regola di sicurezza](./media/hero-role/add-rule.png)
7. <span data-ttu-id="67f59-167">In **Regole di sicurezza in ingresso** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="67f59-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="67f59-168">Digitare **80** nell'intervallo di porte e assicurarsi che sia selezionata l'opzione **Consenti**.</span><span class="sxs-lookup"><span data-stu-id="67f59-168">Type **80** in the port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="67f59-169">Al termine, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="67f59-169">When you are done, click **OK**.</span></span>
   
    ![Screenshot che mostra il pulsante per l'aggiunta di una regola di sicurezza](./media/hero-role/port-80.png)

<span data-ttu-id="67f59-171">Per altre informazioni sui gruppi di sicurezza di rete e le regole in ingresso e in uscita, vedere [Consentire l'accesso esterno alla VM con il portale di Azure](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="67f59-171">For more information about NSGs, inbound and outbound rules, see [Allow external access to your VM using the Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-to-the-default-iis-website"></a><span data-ttu-id="67f59-172">Connettersi al sito Web IIS predefinito</span><span class="sxs-lookup"><span data-stu-id="67f59-172">Connect to the default IIS website</span></span>
1. <span data-ttu-id="67f59-173">Nel portale di Azure fare clic su **Macchine virtuali** e quindi selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67f59-173">In the Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="67f59-174">Copiare l'**indirizzo IP pubblico** nel pannello **Informazioni di base**.</span><span class="sxs-lookup"><span data-stu-id="67f59-174">In the **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![Screenshot che illustra dove trovare l'indirizzo IP pubblico della VM](./media/hero-role/ipaddress.png)
3. <span data-ttu-id="67f59-176">Aprire un browser e digitare l'indirizzo IP pubblico nella barra degli indirizzi come segue: http://<publicIPaddress> e premere **INVIO** per passare a tale indirizzo.</span><span class="sxs-lookup"><span data-stu-id="67f59-176">Open a browser and in the address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** to go to that address.</span></span>
4. <span data-ttu-id="67f59-177">Il browser deve aprire la pagina Web IIS predefinita.</span><span class="sxs-lookup"><span data-stu-id="67f59-177">Your browser should open the default IIS web page.</span></span> <span data-ttu-id="67f59-178">Verrà visualizzata una schermata simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="67f59-178">It looks something like this:</span></span>
   
    ![Screenshot che mostra l'aspetto della pagina IIS predefinita in un browser](./media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="67f59-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67f59-180">Next steps</span></span>
* <span data-ttu-id="67f59-181">È anche possibile provare a [collegare un disco dati](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67f59-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to your virtual machine.</span></span> <span data-ttu-id="67f59-182">I dischi dati forniscono più risorse di archiviazione per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67f59-182">Data disks provide more storage for your virtual machine.</span></span>


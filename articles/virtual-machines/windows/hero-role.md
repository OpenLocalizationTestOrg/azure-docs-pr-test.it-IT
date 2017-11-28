---
title: IIS nella VM Windows prima di aaaInstall | Documenti Microsoft
description: Provare la prima macchina virtuale di Windows, l'installazione di IIS e aprire la porta 80 tramite hello portale di Azure.
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
ms.openlocfilehash: 7cfed6197df058c4569d111ee88961da7c6fe0b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="31e34-103">Sperimentare l'installazione di un ruolo in una VM Windows</span><span class="sxs-lookup"><span data-stu-id="31e34-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="31e34-104">Dopo aver creato il primo e la macchina virtuale (VM) di esecuzione, è possibile spostare in tooinstalling software e servizi.</span><span class="sxs-lookup"><span data-stu-id="31e34-104">Once you have your first virtual machine (VM) up and running, you can move on tooinstalling software and services.</span></span> <span data-ttu-id="31e34-105">Per questa esercitazione, verrà toouse Server Manager su hello tooinstall di macchina virtuale Windows Server IIS.</span><span class="sxs-lookup"><span data-stu-id="31e34-105">For this tutorial, we are going toouse Server Manager on hello Windows Server VM tooinstall IIS.</span></span> <span data-ttu-id="31e34-106">Quindi, si creerà un sicurezza gruppo (rete) utilizzando il traffico di hello tooopen portale Azure porta 80 tooIIS.</span><span class="sxs-lookup"><span data-stu-id="31e34-106">Then, we will create a Network Security Group (NSG) using hello Azure portal tooopen port 80 tooIIS traffic.</span></span> 

<span data-ttu-id="31e34-107">Se è stata ancora creata la prima macchina virtuale, è necessario tornare troppo[creare la prima macchina virtuale di Windows nel portale di Azure hello](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) prima di continuare con questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="31e34-107">If you haven't already created your first VM, you should go back too[Create your first Windows virtual machine in hello Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-hello-vm-is-running"></a><span data-ttu-id="31e34-108">Verificare che hello che macchina virtuale è in esecuzione</span><span class="sxs-lookup"><span data-stu-id="31e34-108">Make sure hello VM is running</span></span>
1. <span data-ttu-id="31e34-109">Aprire hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="31e34-109">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="31e34-110">Nel menu hub hello, fare clic su **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="31e34-110">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="31e34-111">Selezionare macchina virtuale hello hello elenco.</span><span class="sxs-lookup"><span data-stu-id="31e34-111">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="31e34-112">Se è stato hello **arrestato (deallocato)**, fare clic su hello **avviare** pulsante hello **Essentials** blade di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="31e34-112">If hello status is **Stopped (Deallocated)**, click hello **Start** button on hello **Essentials** blade of hello VM.</span></span> <span data-ttu-id="31e34-113">Se è stato hello **esecuzione**, è possibile spostare nel passaggio successivo toohello.</span><span class="sxs-lookup"><span data-stu-id="31e34-113">If hello status is **Running**, you can move on toohello next step.</span></span>

## <a name="connect-toohello-virtual-machine-and-sign-in"></a><span data-ttu-id="31e34-114">Connettere la macchina virtuale di toohello ed eseguire l'accesso</span><span class="sxs-lookup"><span data-stu-id="31e34-114">Connect toohello virtual machine and sign in</span></span>
1. <span data-ttu-id="31e34-115">Nel menu hub hello, fare clic su **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="31e34-115">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="31e34-116">Selezionare macchina virtuale hello hello elenco.</span><span class="sxs-lookup"><span data-stu-id="31e34-116">Select hello virtual machine from hello list.</span></span>
2. <span data-ttu-id="31e34-117">Nel Pannello di hello per la macchina virtuale hello, fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="31e34-117">On hello blade for hello virtual machine, click **Connect**.</span></span> <span data-ttu-id="31e34-118">Viene creato e si scarica un file Remote Desktop Protocol (file con estensione rdp) che è simile a una macchina tooyour tooconnect di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="31e34-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut tooconnect tooyour machine.</span></span> <span data-ttu-id="31e34-119">È possibile desktop tooyour di toosave hello file per semplificare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="31e34-119">You might want toosave hello file tooyour desktop for easy access.</span></span> <span data-ttu-id="31e34-120">**Aprire** questo tooyour tooconnect file macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="31e34-120">**Open** this file tooconnect tooyour VM.</span></span>
   
    ![Schermata di hello che Mostra portale Azure come tooconnect tooyour VM](./media/hero-role/connect.png)
3. <span data-ttu-id="31e34-122">Viene visualizzato un avviso che RDP hello è da un editore sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="31e34-122">You get a warning that hello .rdp is from an unknown publisher.</span></span> <span data-ttu-id="31e34-123">Si tratta di una situazione normale.</span><span class="sxs-lookup"><span data-stu-id="31e34-123">This is normal.</span></span> <span data-ttu-id="31e34-124">Nella finestra di hello Desktop remoto, fare clic su **Connetti** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="31e34-124">In hello Remote Desktop window, click **Connect** toocontinue.</span></span>
   
    ![Screenshot di un avviso relativo a un autore sconosciuto](./media/hero-role/rdp-warn.png)
4. <span data-ttu-id="31e34-126">Nella finestra sicurezza di Windows hello tipo hello username e password per l'account locale hello creato al momento della creazione hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="31e34-126">In hello Windows Security window, type hello username and password for hello local account that you created when you created hello VM.</span></span> <span data-ttu-id="31e34-127">nome utente Hello viene immesso come *vmname*&#92; *nome utente*, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="31e34-127">hello username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![Schermata di immissione di nome della macchina virtuale hello, nome utente e password](./media/hero-role/credentials.png)
5. <span data-ttu-id="31e34-129">Viene visualizzato un avviso non è possibile verificare che il certificato hello.</span><span class="sxs-lookup"><span data-stu-id="31e34-129">You get a warning that hello certificate cannot be verified.</span></span> <span data-ttu-id="31e34-130">Si tratta di una situazione normale.</span><span class="sxs-lookup"><span data-stu-id="31e34-130">This is normal.</span></span> <span data-ttu-id="31e34-131">Fare clic su **Sì** tooverify hello identità della macchina virtuale hello e completare la registrazione.</span><span class="sxs-lookup"><span data-stu-id="31e34-131">Click **Yes** tooverify hello identity of hello virtual machine and finish logging on.</span></span>
   
   ![Screenshot che illustra un messaggio sul verifica identità hello di hello VM](./media/hero-role/cert-warning.png)

<span data-ttu-id="31e34-133">Se si esegue tootrouble quando si tenta di tooconnect, vedere [tooa connessioni Desktop remoto di risoluzione dei problemi basato su Windows Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="31e34-133">If you run in tootrouble when you try tooconnect, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="31e34-134">Installare IIS nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="31e34-134">Install IIS on your VM</span></span>
<span data-ttu-id="31e34-135">Ora che si è connessi toohello macchina virtuale, verrà installato un ruolo del server in modo che è possibile provare più.</span><span class="sxs-lookup"><span data-stu-id="31e34-135">Now that you are logged in toohello VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="31e34-136">Aprire **Server Manager** se non è già aperto.</span><span class="sxs-lookup"><span data-stu-id="31e34-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="31e34-137">Fare clic su hello **avviare** menu e quindi fare clic su **Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="31e34-137">Click hello **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="31e34-138">In **Server Manager**selezionare **Server locale** hello nel riquadro di sinistra.</span><span class="sxs-lookup"><span data-stu-id="31e34-138">In **Server Manager**, select **Local Server** from hello left pane.</span></span> 
3. <span data-ttu-id="31e34-139">Selezionare menu hello **Gestisci** > **Aggiungi ruoli e funzionalità**.</span><span class="sxs-lookup"><span data-stu-id="31e34-139">In hello menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="31e34-140">In hello Aggiunta guidata ruoli e funzionalità, su hello **tipo di installazione** pagina, scegliere **installazione basata su ruoli o basata su funzionalità**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="31e34-140">In hello Add Roles and Features Wizard, on hello **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![Schermata che mostra hello Aggiunta guidata ruoli e funzionalità della scheda per tipo di installazione](./media/hero-role/role-wizard.png)
5. <span data-ttu-id="31e34-142">Selezionare hello VM dal pool di server hello e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="31e34-142">Select hello VM from hello server pool and click **Next**.</span></span>
6. <span data-ttu-id="31e34-143">In hello **i ruoli del Server** selezionare **Server Web (IIS)**.</span><span class="sxs-lookup"><span data-stu-id="31e34-143">On hello **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![Schermata che mostra hello Aggiunta guidata ruoli e funzionalità della scheda per i ruoli del Server](./media/hero-role/add-iis.png)
7. <span data-ttu-id="31e34-145">In hello popup sull'aggiunta di funzionalità necessarie per IIS, verificare che **includono gli strumenti di gestione** è selezionata e quindi fare clic su **Aggiungi funzionalità**.</span><span class="sxs-lookup"><span data-stu-id="31e34-145">In hello pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="31e34-146">Quando si chiude hello popup, fare clic su **Avanti** nella procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="31e34-146">When hello pop-up closes, click **Next** in hello wizard.</span></span>
   
    ![Screenshot che illustra tooconfirm popup Aggiunta ruolo IIS hello](./media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="31e34-148">Nella pagina di funzionalità hello, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="31e34-148">On hello features page, click **Next**.</span></span>
9. <span data-ttu-id="31e34-149">In hello **ruolo Server Web (IIS)** pagina, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="31e34-149">On hello **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="31e34-150">In hello **servizi ruolo** pagina, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="31e34-150">On hello **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="31e34-151">In hello **conferma** pagina, fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="31e34-151">On hello **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="31e34-152">Installazione di hello termine, fare clic su **Chiudi** nella procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="31e34-152">When hello installation is complete, click **Close** on hello wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="31e34-153">Aprire la porta 80</span><span class="sxs-lookup"><span data-stu-id="31e34-153">Open port 80</span></span>
<span data-ttu-id="31e34-154">Affinché la macchina virtuale di tooaccept il traffico in ingresso sulla porta 80, è necessario tooadd un gruppo di sicurezza di rete toohello regola in ingresso.</span><span class="sxs-lookup"><span data-stu-id="31e34-154">In order for your VM tooaccept inbound traffic over port 80, you need tooadd an inbound rule toohello network security group.</span></span> 

1. <span data-ttu-id="31e34-155">Aprire hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="31e34-155">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="31e34-156">In **macchine virtuali** selezionare hello macchina virtuale creata.</span><span class="sxs-lookup"><span data-stu-id="31e34-156">In **Virtual machines** select hello VM that you created.</span></span>
3. <span data-ttu-id="31e34-157">Nelle impostazioni di hello macchine virtuali, selezionare **interfacce di rete** e quindi selezionare hello interfaccia di rete esistente.</span><span class="sxs-lookup"><span data-stu-id="31e34-157">In hello virtual machines settings, select **Network interfaces** and then select hello existing network interface.</span></span>
   
    ![Screenshot che illustra l'impostazione hello macchina virtuale per hello interfacce di rete](./media/hero-role/network-interface.png)
4. <span data-ttu-id="31e34-159">In **Essentials** per interfaccia di rete hello, fare clic su hello **il gruppo di sicurezza di rete**.</span><span class="sxs-lookup"><span data-stu-id="31e34-159">In **Essentials** for hello network interface, click hello **Network security group**.</span></span>
   
    ![Screenshot della sezione di Essentials hello per interfaccia di rete hello](./media/hero-role/select-nsg.png)
5. <span data-ttu-id="31e34-161">In hello **Essentials** pannello hello gruppo, è necessario disporre di un valore predefinito esistente regola in entrata per **predefinita-Consenti-rdp** che consentono di toolog in toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="31e34-161">In hello **Essentials** blade for hello NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you toolog in toohello VM.</span></span> <span data-ttu-id="31e34-162">Si aggiungerà un altro traffico IIS tooallow regola in ingresso.</span><span class="sxs-lookup"><span data-stu-id="31e34-162">You will add another inbound rule tooallow IIS traffic.</span></span> <span data-ttu-id="31e34-163">Fare clic su **Regole di sicurezza in ingresso**.</span><span class="sxs-lookup"><span data-stu-id="31e34-163">Click **Inbound security rule**.</span></span>
   
    ![Screenshot della sezione di Essentials hello per hello NSG](./media/hero-role/inbound.png)
6. <span data-ttu-id="31e34-165">In **Regole di sicurezza in ingresso** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="31e34-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![Screenshot che illustra hello pulsante tooadd una regola di sicurezza](./media/hero-role/add-rule.png)
7. <span data-ttu-id="31e34-167">In **Regole di sicurezza in ingresso** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="31e34-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="31e34-168">Tipo **80** in hello intervallo di porte e assicurarsi che **Consenti** è selezionata.</span><span class="sxs-lookup"><span data-stu-id="31e34-168">Type **80** in hello port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="31e34-169">Al termine, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="31e34-169">When you are done, click **OK**.</span></span>
   
    ![Screenshot che illustra hello pulsante tooadd una regola di sicurezza](./media/hero-role/port-80.png)

<span data-ttu-id="31e34-171">Per ulteriori informazioni su NSGs, le regole in entrata e in uscita, vedere [Consenti accesso esterno tooyour VM utilizzando hello portale di Azure](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="31e34-171">For more information about NSGs, inbound and outbound rules, see [Allow external access tooyour VM using hello Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-toohello-default-iis-website"></a><span data-ttu-id="31e34-172">Connettere il sito Web IIS predefinito toohello</span><span class="sxs-lookup"><span data-stu-id="31e34-172">Connect toohello default IIS website</span></span>
1. <span data-ttu-id="31e34-173">Nel portale di Azure hello, fare clic su **macchine virtuali** e quindi selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="31e34-173">In hello Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="31e34-174">In hello **Essentials** blade, copia il **indirizzo IP pubblico**.</span><span class="sxs-lookup"><span data-stu-id="31e34-174">In hello **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![Screenshot che illustra in toofind hello indirizzo IP pubblico della macchina virtuale](./media/hero-role/ipaddress.png)
3. <span data-ttu-id="31e34-176">Aprire un browser e nella barra degli indirizzi hello, digitare l'indirizzo IP pubblico simile al seguente: http://<publicIPaddress> e fare clic su **invio** toogo toothat indirizzo.</span><span class="sxs-lookup"><span data-stu-id="31e34-176">Open a browser and in hello address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** toogo toothat address.</span></span>
4. <span data-ttu-id="31e34-177">Il browser deve aprire una pagina web IIS predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="31e34-177">Your browser should open hello default IIS web page.</span></span> <span data-ttu-id="31e34-178">Verrà visualizzata una schermata simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="31e34-178">It looks something like this:</span></span>
   
    ![Screenshot che illustra la pagina IIS predefinita hello è simile in un browser](./media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="31e34-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="31e34-180">Next steps</span></span>
* <span data-ttu-id="31e34-181">È inoltre possibile sperimentare [collegando un disco dati](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) macchina virtuale tooyour.</span><span class="sxs-lookup"><span data-stu-id="31e34-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour virtual machine.</span></span> <span data-ttu-id="31e34-182">I dischi dati forniscono più risorse di archiviazione per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="31e34-182">Data disks provide more storage for your virtual machine.</span></span>


---
title: 'Azure Active Directory Domain Services: Aggiunta a un dominio gestito tooa di VM RHEL | Documenti Microsoft'
description: Aggiungere una macchina virtuale Red Hat Enterprise Linux servizi di dominio Active Directory tooAzure
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 41ca2aaf2eefbf9c403d2b834d61a1aa0943d950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a><span data-ttu-id="56fa0-103">Aggiunta a un dominio gestito di macchina virtuale tooa Red Hat Enterprise Linux 7</span><span class="sxs-lookup"><span data-stu-id="56fa0-103">Join a Red Hat Enterprise Linux 7 virtual machine tooa managed domain</span></span>
<span data-ttu-id="56fa0-104">Questo articolo illustra la modalità di gestione dominio toojoin un tooan di macchina virtuale Red Hat Enterprise Linux (RHEL) 7 servizi di dominio Active Directory di Azure.</span><span class="sxs-lookup"><span data-stu-id="56fa0-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="56fa0-105">Eseguire il provisioning di una macchina virtuale di Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="56fa0-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="56fa0-106">Eseguire hello seguente macchina virtuale di tooprovision un RHEL 7 passaggi utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="56fa0-106">Perform hello following steps tooprovision a RHEL 7 virtual machine using hello Azure portal.</span></span>

1. <span data-ttu-id="56fa0-107">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="56fa0-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

    ![Dashboard del portale di Azure](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="56fa0-109">Fare clic su **New** su hello sinistro riquadro e tipo **Red Hat** nella barra di ricerca hello come illustrato nella seguente schermata hello.</span><span class="sxs-lookup"><span data-stu-id="56fa0-109">Click **New** on hello left pane and type **Red Hat** into hello search bar as shown in hello following screenshot.</span></span> <span data-ttu-id="56fa0-110">Le voci per Red Hat Enterprise Linux vengono visualizzati nei risultati della ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="56fa0-110">Entries for Red Hat Enterprise Linux appear in hello search results.</span></span> <span data-ttu-id="56fa0-111">Fare clic su **Red Hat Enterprise Linux 7.2**.</span><span class="sxs-lookup"><span data-stu-id="56fa0-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![Selezionare RHEL nei risultati](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="56fa0-113">risultati della ricerca Hello in hello **tutto** riquadro dovrebbe elencare immagine hello Red Hat Enterprise Linux 7.2.</span><span class="sxs-lookup"><span data-stu-id="56fa0-113">hello search results in hello **Everything** pane should list hello Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="56fa0-114">Fare clic su **Red Hat Enterprise Linux 7.2** tooview ulteriori informazioni sull'immagine di macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="56fa0-114">Click **Red Hat Enterprise Linux 7.2** tooview more information about hello virtual machine image.</span></span>

    ![Selezionare RHEL nei risultati](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="56fa0-116">In hello **Red Hat Enterprise Linux 7.2** riquadro, è necessario visualizzare ulteriori informazioni sull'immagine di macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="56fa0-116">In hello **Red Hat Enterprise Linux 7.2** pane, you should see more information about hello virtual machine image.</span></span> <span data-ttu-id="56fa0-117">In hello **selezionare un modello di distribuzione** elenco a discesa, selezionare **classico**.</span><span class="sxs-lookup"><span data-stu-id="56fa0-117">In hello **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="56fa0-118">Quindi fare clic su hello **crea** pulsante.</span><span class="sxs-lookup"><span data-stu-id="56fa0-118">Then click hello **Create** button.</span></span>

    ![Visualizzare i dettagli dell'immagine](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="56fa0-120">In hello **nozioni di base** pagina di hello **crea macchina virtuale** procedura guidata immettere hello **nome Host** per hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="56fa0-120">In hello **Basics** page of hello **Create virtual machine** wizard, enter hello **Host Name** for hello new virtual machine.</span></span> <span data-ttu-id="56fa0-121">Inoltre, specificare un nome utente dell'amministratore locale in hello **nome utente** campo e un **Password**.</span><span class="sxs-lookup"><span data-stu-id="56fa0-121">Also specify a local administrator user name in hello **User name** field and a **Password**.</span></span> <span data-ttu-id="56fa0-122">È anche possibile scegliere toouse un utente di amministratore locale hello tooauthenticate chiave SSH.</span><span class="sxs-lookup"><span data-stu-id="56fa0-122">You may also choose toouse an SSH key tooauthenticate hello local administrator user.</span></span> <span data-ttu-id="56fa0-123">Selezionare anche un **tariffario** per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="56fa0-123">Also select a **Pricing Tier** for hello virtual machine.</span></span>

    ![Creare una macchina virtuale: dettagli di base](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="56fa0-125">In hello **dimensioni** pagina di hello **crea macchina virtuale** dimensioni hello procedura guidata, selezionare per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="56fa0-125">In hello **Size** page of hello **Create virtual machine** wizard, select hello size for hello virtual machine.</span></span>

    ![Creare una macchina virtuale: selezionare la dimensione](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="56fa0-127">In hello **impostazioni** pagina di hello **crea macchina virtuale** account di archiviazione hello procedura guidata, selezionare per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="56fa0-127">In hello **Settings** page of hello **Create virtual machine** wizard, select hello storage account for hello virtual machine.</span></span> <span data-ttu-id="56fa0-128">Fare clic su **rete virtuale** hello toowhich di tooselect hello rete virtuale devono essere distribuiti VM Linux.</span><span class="sxs-lookup"><span data-stu-id="56fa0-128">Click **Virtual Network** tooselect hello virtual network toowhich hello Linux VM should be deployed.</span></span> <span data-ttu-id="56fa0-129">In hello **rete virtuale** pannello, in cui servizi di dominio Active Directory di Azure è disponibili la rete virtuale selezionare hello.</span><span class="sxs-lookup"><span data-stu-id="56fa0-129">In hello **Virtual Network** blade, select hello virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="56fa0-130">In questo esempio è selezionare una rete virtuale di hello 'MyPreviewVNet'.</span><span class="sxs-lookup"><span data-stu-id="56fa0-130">In this example, we pick hello 'MyPreviewVNet' virtual network.</span></span>

    ![Creare una macchina virtuale: selezionare una rete virtuale](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="56fa0-132">In hello **riepilogo** pagina di hello **crea macchina virtuale** procedura guidata, rivedere e fare clic su hello **OK** pulsante.</span><span class="sxs-lookup"><span data-stu-id="56fa0-132">On hello **Summary** page of hello **Create virtual machine** wizard, review and click hello **OK** button.</span></span>

    ![Creare una macchina virtuale: rete virtuale selezionata](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="56fa0-134">Distribuzione di hello nuova macchina virtuale basata su immagine hello RHEL 7.2 deve iniziare.</span><span class="sxs-lookup"><span data-stu-id="56fa0-134">Deployment of hello new virtual machine based on hello RHEL 7.2 image should start.</span></span>

    ![Creare una macchina virtuale: distribuzione avviata](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="56fa0-136">Dopo alcuni minuti, macchina virtuale hello deve essere distribuito correttamente e pronto all'uso.</span><span class="sxs-lookup"><span data-stu-id="56fa0-136">After a few minutes, hello virtual machine should be deployed successfully and ready for use.</span></span>

    ![Creare una macchina virtuale: distribuzione completata](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="56fa0-138">Connettersi in remoto macchina virtuale di Linux toohello appena effettuato il provisioning</span><span class="sxs-lookup"><span data-stu-id="56fa0-138">Connect remotely toohello newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="56fa0-139">macchina virtuale Hello RHEL 7.2 è stato eseguito il provisioning in Azure.</span><span class="sxs-lookup"><span data-stu-id="56fa0-139">hello RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="56fa0-140">attività successiva Hello è tooconnect in remoto macchina virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="56fa0-140">hello next task is tooconnect remotely toohello virtual machine.</span></span>

<span data-ttu-id="56fa0-141">**Connettere la macchina virtuale di toohello RHEL 7.2** hello di istruzioni nell'articolo hello [come toolog nella macchina virtuale tooa che eseguono Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="56fa0-141">**Connect toohello RHEL 7.2 virtual machine** Follow hello instructions in hello article [How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="56fa0-142">Hello passaggi restanti di hello presuppongono è usare hello SSH PuTTY client tooconnect toohello RHEL macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="56fa0-142">hello rest of hello steps assume you use hello PuTTY SSH client tooconnect toohello RHEL virtual machine.</span></span> <span data-ttu-id="56fa0-143">Per ulteriori informazioni, vedere hello [pagina di Download di PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="56fa0-143">For more information, see hello [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="56fa0-144">Hello aprire PuTTY programma.</span><span class="sxs-lookup"><span data-stu-id="56fa0-144">Open hello PuTTY program.</span></span>
2. <span data-ttu-id="56fa0-145">Immettere hello **nome Host** per hello creata la macchina virtuale RHEL.</span><span class="sxs-lookup"><span data-stu-id="56fa0-145">Enter hello **Host Name** for hello newly created RHEL virtual machine.</span></span> <span data-ttu-id="56fa0-146">In questo esempio, la macchina virtuale con il nome di host hello 'contoso-rhel.cloudapp .net'.</span><span class="sxs-lookup"><span data-stu-id="56fa0-146">In this example, our virtual machine has hello host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="56fa0-147">Se non si certi del nome host hello della macchina virtuale, fare riferimento toohello dashboard della macchina virtuale nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="56fa0-147">If you are not sure of hello host name of your VM, refer toohello VM dashboard on hello Azure portal.</span></span>

    ![Connessione PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="56fa0-149">Accedere a macchina virtuale toohello utilizzando le credenziali di amministratore locale hello specificata durante la creazione della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="56fa0-149">Log on toohello virtual machine using hello local administrator credentials you specified when hello virtual machine was created.</span></span> <span data-ttu-id="56fa0-150">In questo esempio, abbiamo utilizzato l'account amministratore locale hello "mahesh".</span><span class="sxs-lookup"><span data-stu-id="56fa0-150">In this example, we used hello local administrator account "mahesh".</span></span>

    ![Accesso PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a><span data-ttu-id="56fa0-152">Installare i pacchetti richiesti nella macchina virtuale di Linux hello</span><span class="sxs-lookup"><span data-stu-id="56fa0-152">Install required packages on hello Linux virtual machine</span></span>
<span data-ttu-id="56fa0-153">Dopo aver connessione macchina virtuale toohello hello è pacchetti tooinstall necessari per l'aggiunta a un dominio nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="56fa0-153">After connecting toohello virtual machine, hello next task is tooinstall packages required for domain join on hello virtual machine.</span></span> <span data-ttu-id="56fa0-154">Eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="56fa0-154">Perform hello following steps:</span></span>

1. <span data-ttu-id="56fa0-155">**Installare realmd:** pacchetto realmd hello viene utilizzato per l'aggiunta al dominio.</span><span class="sxs-lookup"><span data-stu-id="56fa0-155">**Install realmd:** hello realmd package is used for domain join.</span></span> <span data-ttu-id="56fa0-156">Nel terminale PuTTY, digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="56fa0-156">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="56fa0-157">sudo yum install realmd</span><span class="sxs-lookup"><span data-stu-id="56fa0-157">sudo yum install realmd</span></span>

    ![Installare realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="56fa0-159">Dopo alcuni minuti, hello realmd deve ottenere installato nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="56fa0-159">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![realmd installato](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="56fa0-161">**Installare sssd:** pacchetto realmd hello dipende da operazioni di join sssd tooperform dominio.</span><span class="sxs-lookup"><span data-stu-id="56fa0-161">**Install sssd:** hello realmd package depends on sssd tooperform domain join operations.</span></span> <span data-ttu-id="56fa0-162">Nel terminale PuTTY, digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="56fa0-162">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="56fa0-163">sudo yum install sssd</span><span class="sxs-lookup"><span data-stu-id="56fa0-163">sudo yum install sssd</span></span>

    ![Installare sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="56fa0-165">Dopo alcuni minuti, hello sssd deve ottenere installato nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="56fa0-165">After a few minutes, hello sssd package should get installed on hello virtual machine.</span></span>

    ![realmd installato](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="56fa0-167">**Installare kerberos:** nel terminale PuTTY, digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="56fa0-167">**Install kerberos:** In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="56fa0-168">sudo yum install krb5-workstation krb5-libs</span><span class="sxs-lookup"><span data-stu-id="56fa0-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![Installare kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="56fa0-170">Dopo alcuni minuti, hello realmd deve ottenere installato nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="56fa0-170">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![Kerberos installato](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a><span data-ttu-id="56fa0-172">Aggiunta a dominio gestito toohello hello Linux macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="56fa0-172">Join hello Linux virtual machine toohello managed domain</span></span>
<span data-ttu-id="56fa0-173">Ora che i pacchetti hello necessario sono installati sulla macchina virtuale di Linux hello, hello è dominio gestito toohello toojoin hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="56fa0-173">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

1. <span data-ttu-id="56fa0-174">Individuare hello dominio gestito di servizi di dominio di AAD.</span><span class="sxs-lookup"><span data-stu-id="56fa0-174">Discover hello AAD Domain Services managed domain.</span></span> <span data-ttu-id="56fa0-175">Nel terminale PuTTY, digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="56fa0-175">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="56fa0-176">sudo realm discover CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="56fa0-176">sudo realm discover CONTOSO100.COM</span></span>

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="56fa0-178">Se **individuazione dell'area di autenticazione** è Impossibile toofind dominio gestito, verificare che tale dominio hello sia raggiungibile dalla macchina virtuale hello (ping try).</span><span class="sxs-lookup"><span data-stu-id="56fa0-178">If **realm discover** is unable toofind your managed domain, ensure that hello domain is reachable from hello virtual machine (try ping).</span></span> <span data-ttu-id="56fa0-179">Verificare inoltre che la macchina virtuale hello è stata effettivamente distribuita toohello stessa rete virtuale in cui hello dominio gestito è disponibile.</span><span class="sxs-lookup"><span data-stu-id="56fa0-179">Also ensure that hello virtual machine has indeed been deployed toohello same virtual network in which hello managed domain is available.</span></span>
2. <span data-ttu-id="56fa0-180">Inizializzare kerberos.</span><span class="sxs-lookup"><span data-stu-id="56fa0-180">Initialize kerberos.</span></span> <span data-ttu-id="56fa0-181">Nella finestra terminale PuTTY, digitare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="56fa0-181">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="56fa0-182">Assicurarsi di specificare un utente appartenente al gruppo toohello 'AAD Administrators controller di dominio'.</span><span class="sxs-lookup"><span data-stu-id="56fa0-182">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="56fa0-183">Solo questi utenti è possono aggiungere domini gestiti toohello di computer.</span><span class="sxs-lookup"><span data-stu-id="56fa0-183">Only these users can join computers toohello managed domain.</span></span>

    <span data-ttu-id="56fa0-184">kinit bob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="56fa0-184">kinit bob@CONTOSO100.COM</span></span>

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="56fa0-186">Assicurarsi che si specifica il nome di dominio hello in lettere maiuscole, else kinit ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="56fa0-186">Ensure that you specify hello domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="56fa0-187">Dominio toohello hello macchina.</span><span class="sxs-lookup"><span data-stu-id="56fa0-187">Join hello machine toohello domain.</span></span> <span data-ttu-id="56fa0-188">Nella finestra terminale PuTTY, digitare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="56fa0-188">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="56fa0-189">Specificare hello stesso utente specificato nel precedente passaggio ('kinit') hello.</span><span class="sxs-lookup"><span data-stu-id="56fa0-189">Specify hello same user you specified in hello preceding step ('kinit').</span></span>

    <span data-ttu-id="56fa0-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span><span class="sxs-lookup"><span data-stu-id="56fa0-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![Aggiunta dell'area di autenticazione](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="56fa0-192">È necessario ottenere un messaggio ("correttamente registrato macchina nell'area di autenticazione") quando la macchina hello è dominio gestito toohello correttamente unita in join.</span><span class="sxs-lookup"><span data-stu-id="56fa0-192">You should get a message ("Successfully enrolled machine in realm") when hello machine is successfully joined toohello managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="56fa0-193">Verificare l'aggiunta a un dominio</span><span class="sxs-lookup"><span data-stu-id="56fa0-193">Verify domain join</span></span>
<span data-ttu-id="56fa0-194">È possibile verificare rapidamente se macchina hello è stato dominio gestito toohello correttamente unita in join.</span><span class="sxs-lookup"><span data-stu-id="56fa0-194">You can quickly verify whether hello machine has been successfully joined toohello managed domain.</span></span> <span data-ttu-id="56fa0-195">Connettersi toohello appena dominio RHEL VM utilizzando SSH e un account utente di dominio e quindi toosee di controllo se l'account utente di hello viene risolto correttamente.</span><span class="sxs-lookup"><span data-stu-id="56fa0-195">Connect toohello newly domain joined RHEL VM using SSH and a domain user account and then check toosee if hello user account is resolved correctly.</span></span>

1. <span data-ttu-id="56fa0-196">Nel PuTTY terminal, hello tipo successivo comando tooconnect toohello appena aggiunti al dominio RHEL virtual machine tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="56fa0-196">In your PuTTY terminal, type hello following command tooconnect toohello newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="56fa0-197">Utilizzare un account di dominio appartenente al dominio gestito toohello (ad esempio, 'bob@CONTOSO100.COM' in questo caso.)</span><span class="sxs-lookup"><span data-stu-id="56fa0-197">Use a domain account that belongs toohello managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="56fa0-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="56fa0-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="56fa0-199">Nella finestra terminale PuTTY, digitare hello successivo comando toosee se home directory di hello è stato inizializzato correttamente.</span><span class="sxs-lookup"><span data-stu-id="56fa0-199">In your PuTTY terminal, type hello following command toosee if hello home directory was initialized correctly.</span></span>

    <span data-ttu-id="56fa0-200">pwd</span><span class="sxs-lookup"><span data-stu-id="56fa0-200">pwd</span></span>
3. <span data-ttu-id="56fa0-201">Nella finestra terminale PuTTY, digitare hello successivo comando toosee se appartenenze hello sono stati risolti correttamente.</span><span class="sxs-lookup"><span data-stu-id="56fa0-201">In your PuTTY terminal, type hello following command toosee if hello group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="56fa0-202">id</span><span class="sxs-lookup"><span data-stu-id="56fa0-202">id</span></span>

<span data-ttu-id="56fa0-203">Di seguito è riportato un esempio dell'output di questi comandi:</span><span class="sxs-lookup"><span data-stu-id="56fa0-203">A sample output of these commands follows:</span></span>

![Verificare l'aggiunta a un dominio](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="56fa0-205">Risoluzione dei problemi di aggiunta al dominio</span><span class="sxs-lookup"><span data-stu-id="56fa0-205">Troubleshooting domain join</span></span>
<span data-ttu-id="56fa0-206">Fare riferimento toohello [aggiunta al dominio Troubleshooting](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) articolo.</span><span class="sxs-lookup"><span data-stu-id="56fa0-206">Refer toohello [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="56fa0-207">Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="56fa0-207">Related Content</span></span>
* [<span data-ttu-id="56fa0-208">Guida introduttiva di Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="56fa0-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="56fa0-209">Aggiunta a un dominio gestito con servizi di dominio Active Directory di Azure tooan Windows Server macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="56fa0-209">Join a Windows Server virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="56fa0-210">[Come toolog nella macchina virtuale tooa che eseguono Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="56fa0-210">[How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="56fa0-211">Installazione di Kerberos</span><span class="sxs-lookup"><span data-stu-id="56fa0-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="56fa0-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span><span class="sxs-lookup"><span data-stu-id="56fa0-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)

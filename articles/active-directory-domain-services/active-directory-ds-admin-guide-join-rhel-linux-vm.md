---
title: 'Azure Active Directory Domain Services: aggiungere una macchina virtuale RHEL a un dominio gestito | Documentazione Microsoft'
description: Aggiungere una macchina virtuale Red Hat Enterprise Linux a Servizi di dominio Azure AD
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
ms.openlocfilehash: 69f1850bfed90392e9a4695e2443ffaa6bfc746d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-to-a-managed-domain"></a><span data-ttu-id="6ea69-103">Aggiungere una macchina virtuale di Red Hat Enterprise Linux 7 a un dominio gestito</span><span class="sxs-lookup"><span data-stu-id="6ea69-103">Join a Red Hat Enterprise Linux 7 virtual machine to a managed domain</span></span>
<span data-ttu-id="6ea69-104">Questo articolo illustra come aggiungere una macchina virtuale di Red Hat Enterprise Linux (RHEL) 7 a un dominio gestito di Servizi di dominio Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ea69-104">This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="6ea69-105">Eseguire il provisioning di una macchina virtuale di Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="6ea69-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="6ea69-106">Eseguire questa procedura per effettuare il provisioning di una macchina virtuale RHEL 7 con il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6ea69-106">Perform the following steps to provision a RHEL 7 virtual machine using the Azure portal.</span></span>

1. <span data-ttu-id="6ea69-107">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6ea69-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

    ![Dashboard del portale di Azure](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="6ea69-109">Fare clic su **Nuovo** nel riquadro a sinistra e digitare **Red Hat** nella barra di ricerca, come illustrato nello screenshot seguente.</span><span class="sxs-lookup"><span data-stu-id="6ea69-109">Click **New** on the left pane and type **Red Hat** into the search bar as shown in the following screenshot.</span></span> <span data-ttu-id="6ea69-110">Nei risultati della ricerca vengono visualizzate le voci per Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="6ea69-110">Entries for Red Hat Enterprise Linux appear in the search results.</span></span> <span data-ttu-id="6ea69-111">Fare clic su **Red Hat Enterprise Linux 7.2**.</span><span class="sxs-lookup"><span data-stu-id="6ea69-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![Selezionare RHEL nei risultati](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="6ea69-113">I risultati della ricerca nel riquadro **Tutto** dovrebbero elencare l'immagine di Red Hat Enterprise Linux 7.2.</span><span class="sxs-lookup"><span data-stu-id="6ea69-113">The search results in the **Everything** pane should list the Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="6ea69-114">Fare clic su **Red Hat Enterprise Linux 7.2** per visualizzare altre informazioni sull'immagine della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6ea69-114">Click **Red Hat Enterprise Linux 7.2** to view more information about the virtual machine image.</span></span>

    ![Selezionare RHEL nei risultati](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="6ea69-116">Nel riquadro **Red Hat Enterprise Linux 7.2** dovrebbero essere visualizzate altre informazioni sull'immagine della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6ea69-116">In the **Red Hat Enterprise Linux 7.2** pane, you should see more information about the virtual machine image.</span></span> <span data-ttu-id="6ea69-117">Nell'elenco a discesa **Selezionare un modello di distribuzione** selezionare **Classica**.</span><span class="sxs-lookup"><span data-stu-id="6ea69-117">In the **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="6ea69-118">Quindi, fare clic sul pulsante **Crea** .</span><span class="sxs-lookup"><span data-stu-id="6ea69-118">Then click the **Create** button.</span></span>

    ![Visualizzare i dettagli dell'immagine](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="6ea69-120">Nella pagina **di base** della procedura guidata **Crea macchina virtuale** immettere il **Nome host** per la nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6ea69-120">In the **Basics** page of the **Create virtual machine** wizard, enter the **Host Name** for the new virtual machine.</span></span> <span data-ttu-id="6ea69-121">Specificare anche il nome utente di un amministratore locale nel campo **Nome utente** e la relativa **Password**.</span><span class="sxs-lookup"><span data-stu-id="6ea69-121">Also specify a local administrator user name in the **User name** field and a **Password**.</span></span> <span data-ttu-id="6ea69-122">Si può anche scegliere di usare una chiave SSH per l'autenticazione dell'utente amministratore locale.</span><span class="sxs-lookup"><span data-stu-id="6ea69-122">You may also choose to use an SSH key to authenticate the local administrator user.</span></span> <span data-ttu-id="6ea69-123">Selezionare anche un **Piano tariffario** per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6ea69-123">Also select a **Pricing Tier** for the virtual machine.</span></span>

    ![Creare una macchina virtuale: dettagli di base](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="6ea69-125">Nella pagina delle **dimensioni** della procedura guidata **Crea macchina virtuale** selezionare la dimensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6ea69-125">In the **Size** page of the **Create virtual machine** wizard, select the size for the virtual machine.</span></span>

    ![Creare una macchina virtuale: selezionare la dimensione](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="6ea69-127">Nella pagina delle **impostazioni** della procedura guidata **Crea macchina virtuale** selezionare l'account di archiviazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6ea69-127">In the **Settings** page of the **Create virtual machine** wizard, select the storage account for the virtual machine.</span></span> <span data-ttu-id="6ea69-128">Fare clic su **Rete virtuale** per selezionare la rete virtuale in cui deve essere distribuita la VM Linux.</span><span class="sxs-lookup"><span data-stu-id="6ea69-128">Click **Virtual Network** to select the virtual network to which the Linux VM should be deployed.</span></span> <span data-ttu-id="6ea69-129">Nel pannello **Rete virtuale** selezionare la rete virtuale in cui è disponibile Servizi di dominio Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ea69-129">In the **Virtual Network** blade, select the virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="6ea69-130">In questo esempio viene selezionata la rete virtuale 'MyPreviewVNet'.</span><span class="sxs-lookup"><span data-stu-id="6ea69-130">In this example, we pick the 'MyPreviewVNet' virtual network.</span></span>

    ![Creare una macchina virtuale: selezionare una rete virtuale](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="6ea69-132">Nella pagina di **riepilogo** della procedura guidata **Crea macchina virtuale**, rivedere le impostazioni e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6ea69-132">On the **Summary** page of the **Create virtual machine** wizard, review and click the **OK** button.</span></span>

    ![Creare una macchina virtuale: rete virtuale selezionata](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="6ea69-134">Dovrebbe iniziare la distribuzione della nuova macchina virtuale basata sull'immagine di RHEL 7.2.</span><span class="sxs-lookup"><span data-stu-id="6ea69-134">Deployment of the new virtual machine based on the RHEL 7.2 image should start.</span></span>

    ![Creare una macchina virtuale: distribuzione avviata](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="6ea69-136">Dopo alcuni minuti, la macchina virtuale dovrebbe essere distribuita correttamente e pronta per l'uso.</span><span class="sxs-lookup"><span data-stu-id="6ea69-136">After a few minutes, the virtual machine should be deployed successfully and ready for use.</span></span>

    ![Creare una macchina virtuale: distribuzione completata](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-to-the-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="6ea69-138">Connettersi in remoto alla macchina virtuale Linux di cui è stato appena effettuato il provisioning</span><span class="sxs-lookup"><span data-stu-id="6ea69-138">Connect remotely to the newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="6ea69-139">Il provisioning della macchina virtuale RHEL 7.2 è stato eseguito in Azure.</span><span class="sxs-lookup"><span data-stu-id="6ea69-139">The RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="6ea69-140">L'attività successiva prevede la connessione remota alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6ea69-140">The next task is to connect remotely to the virtual machine.</span></span>

<span data-ttu-id="6ea69-141">**Connettersi alla macchina virtuale RHEL 7.2** Seguire le istruzioni contenute nell'articolo che illustra [come accedere a una macchina virtuale che esegue Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6ea69-141">**Connect to the RHEL 7.2 virtual machine** Follow the instructions in the article [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="6ea69-142">I passaggi rimanenti presuppongono l'uso di PuTTY come client SSH per connettersi alla macchina virtuale RHEL.</span><span class="sxs-lookup"><span data-stu-id="6ea69-142">The rest of the steps assume you use the PuTTY SSH client to connect to the RHEL virtual machine.</span></span> <span data-ttu-id="6ea69-143">Per altre informazioni, vedere la [pagina di download di PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="6ea69-143">For more information, see the [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="6ea69-144">Aprire il programma PuTTY.</span><span class="sxs-lookup"><span data-stu-id="6ea69-144">Open the PuTTY program.</span></span>
2. <span data-ttu-id="6ea69-145">Immettere il **Nome host** per la macchina virtuale RHEL appena creata.</span><span class="sxs-lookup"><span data-stu-id="6ea69-145">Enter the **Host Name** for the newly created RHEL virtual machine.</span></span> <span data-ttu-id="6ea69-146">In questo esempio il nome della macchina virtuale è 'contoso-rhel.cloudapp.net'.</span><span class="sxs-lookup"><span data-stu-id="6ea69-146">In this example, our virtual machine has the host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="6ea69-147">Se non si è certi del nome host della macchina virtuale, vedere il dashboard della macchina virtuale nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6ea69-147">If you are not sure of the host name of your VM, refer to the VM dashboard on the Azure portal.</span></span>

    ![Connessione PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="6ea69-149">Accedere alla macchina virtuale usando le credenziali di amministratore locale specificate durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6ea69-149">Log on to the virtual machine using the local administrator credentials you specified when the virtual machine was created.</span></span> <span data-ttu-id="6ea69-150">In questo esempio viene usato l'account di amministratore locale "mahesh".</span><span class="sxs-lookup"><span data-stu-id="6ea69-150">In this example, we used the local administrator account "mahesh".</span></span>

    ![Accesso PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-the-linux-virtual-machine"></a><span data-ttu-id="6ea69-152">Installare i pacchetti necessari nella macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="6ea69-152">Install required packages on the Linux virtual machine</span></span>
<span data-ttu-id="6ea69-153">Dopo la connessione alla macchina virtuale, l'attività successiva consiste nell'installare nella macchina virtuale i pacchetti necessari per l'aggiunta a un dominio.</span><span class="sxs-lookup"><span data-stu-id="6ea69-153">After connecting to the virtual machine, the next task is to install packages required for domain join on the virtual machine.</span></span> <span data-ttu-id="6ea69-154">Eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6ea69-154">Perform the following steps:</span></span>

1. <span data-ttu-id="6ea69-155">**Installare realmd:** il pacchetto realmd viene usato per l'aggiunta a un dominio.</span><span class="sxs-lookup"><span data-stu-id="6ea69-155">**Install realmd:** The realmd package is used for domain join.</span></span> <span data-ttu-id="6ea69-156">Nel terminale PuTTY digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6ea69-156">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="6ea69-157">sudo yum install realmd</span><span class="sxs-lookup"><span data-stu-id="6ea69-157">sudo yum install realmd</span></span>

    ![Installare realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="6ea69-159">Dopo alcuni minuti, il pacchetto realmd dovrebbe essere installato nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6ea69-159">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![realmd installato](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="6ea69-161">**Installare sssd:** il pacchetto realmd dipende da sssd per l'esecuzione di operazioni di aggiunta a un dominio.</span><span class="sxs-lookup"><span data-stu-id="6ea69-161">**Install sssd:** The realmd package depends on sssd to perform domain join operations.</span></span> <span data-ttu-id="6ea69-162">Nel terminale PuTTY digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6ea69-162">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="6ea69-163">sudo yum install sssd</span><span class="sxs-lookup"><span data-stu-id="6ea69-163">sudo yum install sssd</span></span>

    ![Installare sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="6ea69-165">Dopo alcuni minuti, il pacchetto sssd dovrebbe essere installato nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6ea69-165">After a few minutes, the sssd package should get installed on the virtual machine.</span></span>

    ![realmd installato](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="6ea69-167">**Installare kerberos**. A tale scopo, nel terminale PuTTY digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6ea69-167">**Install kerberos:** In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="6ea69-168">sudo yum install krb5-workstation krb5-libs</span><span class="sxs-lookup"><span data-stu-id="6ea69-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![Installare kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="6ea69-170">Dopo alcuni minuti, il pacchetto realmd dovrebbe essere installato nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6ea69-170">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![Kerberos installato](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-the-linux-virtual-machine-to-the-managed-domain"></a><span data-ttu-id="6ea69-172">Aggiungere la macchina virtuale Linux al dominio gestito</span><span class="sxs-lookup"><span data-stu-id="6ea69-172">Join the Linux virtual machine to the managed domain</span></span>
<span data-ttu-id="6ea69-173">Ora che i pacchetti sono installati nella macchina virtuale Linux, l'attività successiva consiste nell'aggiungere la macchina virtuale al dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="6ea69-173">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

1. <span data-ttu-id="6ea69-174">Individuare il dominio gestito di Servizi di dominio AAD.</span><span class="sxs-lookup"><span data-stu-id="6ea69-174">Discover the AAD Domain Services managed domain.</span></span> <span data-ttu-id="6ea69-175">Nel terminale PuTTY digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6ea69-175">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="6ea69-176">sudo realm discover CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="6ea69-176">sudo realm discover CONTOSO100.COM</span></span>

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="6ea69-178">Se **realm discover** non riesce a trovare il dominio gestito, verificare che il dominio sia raggiungibile dalla macchina virtuale (provare a eseguire il ping).</span><span class="sxs-lookup"><span data-stu-id="6ea69-178">If **realm discover** is unable to find your managed domain, ensure that the domain is reachable from the virtual machine (try ping).</span></span> <span data-ttu-id="6ea69-179">Verificare anche che la macchina virtuale sia stata effettivamente distribuita nella stessa rete virtuale in cui è disponibile il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="6ea69-179">Also ensure that the virtual machine has indeed been deployed to the same virtual network in which the managed domain is available.</span></span>
2. <span data-ttu-id="6ea69-180">Inizializzare kerberos.</span><span class="sxs-lookup"><span data-stu-id="6ea69-180">Initialize kerberos.</span></span> <span data-ttu-id="6ea69-181">Nel terminale PuTTY digitare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="6ea69-181">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="6ea69-182">Verificare che l'utente specificato appartenga al gruppo AAD DC Administrators.</span><span class="sxs-lookup"><span data-stu-id="6ea69-182">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="6ea69-183">Solo questi utenti possono aggiungere computer al dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="6ea69-183">Only these users can join computers to the managed domain.</span></span>

    <span data-ttu-id="6ea69-184">kinit bob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="6ea69-184">kinit bob@CONTOSO100.COM</span></span>

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="6ea69-186">Verificare che il nome di dominio sia scritto in lettere maiuscole; in caso contrario kinit avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="6ea69-186">Ensure that you specify the domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="6ea69-187">Aggiungere il computer al dominio.</span><span class="sxs-lookup"><span data-stu-id="6ea69-187">Join the machine to the domain.</span></span> <span data-ttu-id="6ea69-188">Nel terminale PuTTY digitare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="6ea69-188">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="6ea69-189">Specificare lo stesso utente "kinit" specificato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="6ea69-189">Specify the same user you specified in the preceding step ('kinit').</span></span>

    <span data-ttu-id="6ea69-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span><span class="sxs-lookup"><span data-stu-id="6ea69-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![Aggiunta dell'area di autenticazione](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="6ea69-192">Quando il computer viene aggiunto correttamente al dominio gestito, dovrebbe essere visualizzato un messaggio che indica che il computer è stato registrato correttamente nell'area di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6ea69-192">You should get a message ("Successfully enrolled machine in realm") when the machine is successfully joined to the managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="6ea69-193">Verificare l'aggiunta a un dominio</span><span class="sxs-lookup"><span data-stu-id="6ea69-193">Verify domain join</span></span>
<span data-ttu-id="6ea69-194">È possibile verificare rapidamente se il computer è stato aggiunto correttamente al dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="6ea69-194">You can quickly verify whether the machine has been successfully joined to the managed domain.</span></span> <span data-ttu-id="6ea69-195">Connettersi alla macchina virtuale RHEL appena aggiunta a un dominio usando SSH e un account utente di dominio e quindi verificando se l'account utente viene risolto correttamente.</span><span class="sxs-lookup"><span data-stu-id="6ea69-195">Connect to the newly domain joined RHEL VM using SSH and a domain user account and then check to see if the user account is resolved correctly.</span></span>

1. <span data-ttu-id="6ea69-196">Nel terminale PuTTY digitare il comando seguente per connettere la macchina virtuale RHEL appena aggiunta a un dominio con SSH.</span><span class="sxs-lookup"><span data-stu-id="6ea69-196">In your PuTTY terminal, type the following command to connect to the newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="6ea69-197">Usare un account di dominio appartenente al dominio gestito, in questo caso bob@CONTOSO100.COM.</span><span class="sxs-lookup"><span data-stu-id="6ea69-197">Use a domain account that belongs to the managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="6ea69-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="6ea69-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="6ea69-199">Nel terminale PuTTY digitare il comando seguente per vedere se la home directory dell'utente è stata inizializzata correttamente.</span><span class="sxs-lookup"><span data-stu-id="6ea69-199">In your PuTTY terminal, type the following command to see if the home directory was initialized correctly.</span></span>

    <span data-ttu-id="6ea69-200">pwd</span><span class="sxs-lookup"><span data-stu-id="6ea69-200">pwd</span></span>
3. <span data-ttu-id="6ea69-201">Nel terminale PuTTY digitare il comando seguente per vedere se i membri del gruppo sono stati risolti correttamente.</span><span class="sxs-lookup"><span data-stu-id="6ea69-201">In your PuTTY terminal, type the following command to see if the group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="6ea69-202">id</span><span class="sxs-lookup"><span data-stu-id="6ea69-202">id</span></span>

<span data-ttu-id="6ea69-203">Di seguito è riportato un esempio dell'output di questi comandi:</span><span class="sxs-lookup"><span data-stu-id="6ea69-203">A sample output of these commands follows:</span></span>

![Verificare l'aggiunta a un dominio](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="6ea69-205">Risoluzione dei problemi di aggiunta al dominio</span><span class="sxs-lookup"><span data-stu-id="6ea69-205">Troubleshooting domain join</span></span>
<span data-ttu-id="6ea69-206">Vedere l'articolo [Risoluzione dei problemi dell'aggiunta a un dominio](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) .</span><span class="sxs-lookup"><span data-stu-id="6ea69-206">Refer to the [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="6ea69-207">Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="6ea69-207">Related Content</span></span>
* [<span data-ttu-id="6ea69-208">Guida introduttiva di Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="6ea69-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="6ea69-209">Aggiungere una macchina virtuale Windows Server a un dominio gestito di Servizi di dominio Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ea69-209">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="6ea69-210">[Come accedere a una macchina virtuale che esegue Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="6ea69-210">[How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="6ea69-211">Installazione di Kerberos</span><span class="sxs-lookup"><span data-stu-id="6ea69-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="6ea69-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span><span class="sxs-lookup"><span data-stu-id="6ea69-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)

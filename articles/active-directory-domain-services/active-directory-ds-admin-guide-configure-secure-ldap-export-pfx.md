---
title: Configurare l'accesso LDAP sicuro (LDAPS) in Azure Active Directory Domain Services | Microsoft Docs
description: Configurare l'accesso LDAP sicuro (LDAPS) per un dominio gestito di Servizi di dominio Azure AD
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 5d46f376d46b8bbf3f93de57a7d4e31abdbcdb2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="10e1e-103">Configurare l'accesso LDAP sicuro (LDAPS) per un dominio gestito di Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="10e1e-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="10e1e-104">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="10e1e-104">Before you begin</span></span>
<span data-ttu-id="10e1e-105">Assicurarsi di aver completato l'[Attività 1: Ottenere un certificato per l'accesso LDAP sicuro](active-directory-ds-admin-guide-configure-secure-ldap.md).</span><span class="sxs-lookup"><span data-stu-id="10e1e-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-the-secure-ldap-certificate-to-a-pfx-file"></a><span data-ttu-id="10e1e-106">Attività 2: Esportare il certificato LDAP sicuro in un file PFX</span><span class="sxs-lookup"><span data-stu-id="10e1e-106">Task 2 - export the secure LDAP certificate to a .PFX file</span></span>
<span data-ttu-id="10e1e-107">Prima di iniziare questa attività, assicurarsi di aver ottenuto il certificato LDAP sicuro da un'autorità di certificazione pubblica oppure di aver creato un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="10e1e-107">Before you start this task, ensure that you have obtained the secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="10e1e-108">Per esportare il certificato LDAPS in un file PFX, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="10e1e-108">Perform the following steps, to export the LDAPS certificate to a .PFX file.</span></span>

1. <span data-ttu-id="10e1e-109">Fare clic sul pulsante **Start** e digitare **R**. Nella finestra di dialogo **Esegui** digitare **mmc** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="10e1e-109">Press the **Start** button and type **R**. In the **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![Avviare la console MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="10e1e-111">Nel prompt di **Controllo dell'account utente** fare clic su **Sì** per avviare Microsoft Management Console (MMC) come amministratore.</span><span class="sxs-lookup"><span data-stu-id="10e1e-111">On the **User Account Control** prompt, click **YES** to launch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="10e1e-112">Nel menu **File** fare clic su **Aggiungi/Rimuovi snap-in...**.</span><span class="sxs-lookup"><span data-stu-id="10e1e-112">From the **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![Aggiungere lo snap-in alla console MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="10e1e-114">Nella finestra di dialogo **Aggiungi o rimuovi snap-in** selezionare lo snap-in **Certificati** e fare clic sul pulsante **Aggiungi >**.</span><span class="sxs-lookup"><span data-stu-id="10e1e-114">In the **Add or Remove Snap-ins** dialog, select the **Certificates** snap-in, and click the **Add >** button.</span></span>

    ![Aggiungere lo snap-in certificati alla console MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="10e1e-116">Nella procedura guidata **Snap-in certificati** selezionare **Account del computer** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="10e1e-116">In the **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![Aggiungere lo snap-in certificati per l'account del computer](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="10e1e-118">Nella pagina **Seleziona computer** selezionare **Computer locale (il computer su cui è in esecuzione questa console)** e fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="10e1e-118">On the **Select Computer** page, select **Local computer: (the computer this console is running on)** and click **Finish**.</span></span>

    ![Aggiungere lo snap-in certificati, Seleziona computer](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="10e1e-120">Nella finestra di dialogo **Aggiungi o rimuovi snap-in** fare clic su **OK** per aggiungere lo snap-in Certificati a MMC.</span><span class="sxs-lookup"><span data-stu-id="10e1e-120">In the **Add or Remove Snap-ins** dialog, click **OK** to add the certificates snap-in to MMC.</span></span>

    ![Aggiungere lo snap-in certificati a MMC, Fatto](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="10e1e-122">Nella finestra di MMC selezionare **Radice console**.</span><span class="sxs-lookup"><span data-stu-id="10e1e-122">In the MMC window, click to expand **Console Root**.</span></span> <span data-ttu-id="10e1e-123">Verrà visualizzato lo snap-in certificati caricato.</span><span class="sxs-lookup"><span data-stu-id="10e1e-123">You should see the Certificates snap-in loaded.</span></span> <span data-ttu-id="10e1e-124">Selezionare **Certificati (computer locale)** per espandere la voce.</span><span class="sxs-lookup"><span data-stu-id="10e1e-124">Click **Certificates (Local Computer)** to expand.</span></span> <span data-ttu-id="10e1e-125">Selezionare il nodo **Personale** per espanderlo, poi selezionare il nodo **Certificati**.</span><span class="sxs-lookup"><span data-stu-id="10e1e-125">Click to expand the **Personal** node, followed by the **Certificates** node.</span></span>

    ![Aprire l'archivio certificati personali](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="10e1e-127">Verrà visualizzato il certificato autofirmato che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="10e1e-127">You should see the self-signed certificate we created.</span></span> <span data-ttu-id="10e1e-128">È possibile esaminare le proprietà del certificato per assicurarsi che l'identificazione personale corrisponda a quella indicata nelle finestre di PowerShell al momento della creazione del certificato.</span><span class="sxs-lookup"><span data-stu-id="10e1e-128">You can examine the properties of the certificate to ensure the thumbprint matches that reported on the PowerShell windows when you created the certificate.</span></span>
10. <span data-ttu-id="10e1e-129">Selezionare il certificato autofirmato e **fare clic con il pulsante destro del mouse**.</span><span class="sxs-lookup"><span data-stu-id="10e1e-129">Select the self-signed certificate and **right click**.</span></span> <span data-ttu-id="10e1e-130">Selezionare **Tutte le attività** dal menu di scelta rapida e quindi **Esporta...**.</span><span class="sxs-lookup"><span data-stu-id="10e1e-130">From the right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![Esportare il certificato](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="10e1e-132">Nell'**esportazione guidata dei certificati** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="10e1e-132">In the **Certificate Export Wizard**, click **Next**.</span></span>

    ![Esportare il certificato, procedura guidata](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="10e1e-134">Nella pagina **Esportazione della chiave privata con il certificato** selezionare **Sì, esporta la chiave privata** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="10e1e-134">On the **Export Private Key** page, select **Yes, export the private key**, and click **Next**.</span></span>

    ![Esportare il certificato, chiave privata](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="10e1e-136">È NECESSARIO esportare la chiave privata insieme al certificato.</span><span class="sxs-lookup"><span data-stu-id="10e1e-136">You MUST export the private key along with the certificate.</span></span> <span data-ttu-id="10e1e-137">Se si abilita l'accesso LDAP sicuro per il dominio gestito specificando un file PFX che non contiene la chiave privata per il certificato, l'operazione avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="10e1e-137">If you provide a PFX that does not contain the private key for the certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="10e1e-138">Nella pagina **Formato file di esportazione** selezionare **Scambio di informazioni personali - PKCS #12 (.PFX)** come formato di file per il certificato esportato.</span><span class="sxs-lookup"><span data-stu-id="10e1e-138">On the **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as the file format for the exported certificate.</span></span>

    ![Esportare il certificato, formato di file](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="10e1e-140">È supportato solo il formato di file PFX.</span><span class="sxs-lookup"><span data-stu-id="10e1e-140">Only the .PFX file format is supported.</span></span> <span data-ttu-id="10e1e-141">Non esportare il certificato nel formato di file CER.</span><span class="sxs-lookup"><span data-stu-id="10e1e-141">Do not export the certificate to the .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="10e1e-142">Nella pagina **Sicurezza** selezionare l'opzione **Password** e digitare una password per proteggere il file con estensione pfx.</span><span class="sxs-lookup"><span data-stu-id="10e1e-142">On the **Security** page, select the **Password** option and type in a password to protect the .PFX file.</span></span> <span data-ttu-id="10e1e-143">Prendere nota della password perché sarà necessaria nell'attività successiva.</span><span class="sxs-lookup"><span data-stu-id="10e1e-143">Remember this password since it will be needed in the next task.</span></span> <span data-ttu-id="10e1e-144">Fare clic su **Avanti** per continuare.</span><span class="sxs-lookup"><span data-stu-id="10e1e-144">Click **Next** to proceed.</span></span>

    ![<span data-ttu-id="10e1e-145">Password per l'esportazione del certificato</span><span class="sxs-lookup"><span data-stu-id="10e1e-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="10e1e-146">Prendere nota della password.</span><span class="sxs-lookup"><span data-stu-id="10e1e-146">Make a note of this password.</span></span> <span data-ttu-id="10e1e-147">Sarà necessaria per i passaggi descritti nell'[Attività 3: Abilitare l'accesso LDAP sicuro per il dominio gestito](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="10e1e-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for the managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="10e1e-148">Nella pagina **File da esportare** specificare il nome del file e il percorso in cui esportare il certificato.</span><span class="sxs-lookup"><span data-stu-id="10e1e-148">On the **File to Export** page, specify the file name and location where you'd like to export the certificate.</span></span>

    ![Percorso per l'esportazione del certificato](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="10e1e-150">Nella pagina successiva fare clic su **Fine** per esportare il certificato in un file con estensione pfx.</span><span class="sxs-lookup"><span data-stu-id="10e1e-150">On the following page, click **Finish** to export the certificate to a PFX file.</span></span> <span data-ttu-id="10e1e-151">Al termine dell'esportazione del certificato verrà visualizzata una finestra di dialogo di conferma.</span><span class="sxs-lookup"><span data-stu-id="10e1e-151">You should see confirmation dialog when the certificate has been exported.</span></span>

    ![Esportare il certificato, Fatto](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="10e1e-153">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="10e1e-153">Next step</span></span>
[<span data-ttu-id="10e1e-154">Attività 3: Abilitare l'accesso LDAP sicuro per il dominio gestito</span><span class="sxs-lookup"><span data-stu-id="10e1e-154">Task 3 - enable secure LDAP for the managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)

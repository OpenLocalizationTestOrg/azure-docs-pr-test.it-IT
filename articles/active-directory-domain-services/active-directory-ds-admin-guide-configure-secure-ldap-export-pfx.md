---
title: aaaConfigure Secure LDAP (LDAPS) in servizi di dominio Active Directory di Azure | Documenti Microsoft
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
ms.openlocfilehash: 356b28f8392b0e203df9c81177ec842d52866c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="d4299-103">Configurare l'accesso LDAP sicuro (LDAPS) per un dominio gestito di Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="d4299-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d4299-104">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="d4299-104">Before you begin</span></span>
<span data-ttu-id="d4299-105">Assicurarsi di aver completato l'[Attività 1: Ottenere un certificato per l'accesso LDAP sicuro](active-directory-ds-admin-guide-configure-secure-ldap.md).</span><span class="sxs-lookup"><span data-stu-id="d4299-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a><span data-ttu-id="d4299-106">Attività 2: esportare hello sicura LDAP certificato tooa. File PFX</span><span class="sxs-lookup"><span data-stu-id="d4299-106">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>
<span data-ttu-id="d4299-107">Prima di iniziare questa attività, assicurarsi di aver ottenuto un certificato LDAP sicuro hello da un'autorità di certificazione pubblica o aver creato un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="d4299-107">Before you start this task, ensure that you have obtained hello secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="d4299-108">Eseguire hello alla procedura seguente, hello tooexport LDAPS tooa del certificato. File PFX.</span><span class="sxs-lookup"><span data-stu-id="d4299-108">Perform hello following steps, tooexport hello LDAPS certificate tooa .PFX file.</span></span>

1. <span data-ttu-id="d4299-109">Hello premere **avviare** pulsante e digitare **R**. In hello **eseguire** finestra di dialogo, tipo **mmc** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4299-109">Press hello **Start** button and type **R**. In hello **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![Avviare la console di MMC hello](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="d4299-111">In hello **controllo dell'Account utente** richiesto, fare clic su **Sì** toolaunch MMC (Microsoft Management Console) come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d4299-111">On hello **User Account Control** prompt, click **YES** toolaunch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="d4299-112">Da hello **File** menu, fare clic su **Aggiungi/Rimuovi Snap-in...** .</span><span class="sxs-lookup"><span data-stu-id="d4299-112">From hello **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![Aggiungere lo snap-in tooMMC console](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="d4299-114">In hello **Aggiungi o Rimuovi Snap-in** finestra di dialogo, seleziona hello **certificati** snap-in, fare clic su hello **Aggiungi >** pulsante.</span><span class="sxs-lookup"><span data-stu-id="d4299-114">In hello **Add or Remove Snap-ins** dialog, select hello **Certificates** snap-in, and click hello **Add >** button.</span></span>

    ![Aggiungere console tooMMC snap-in certificati](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="d4299-116">In hello **snap-in certificati** procedura guidata, selezionare **account Computer** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d4299-116">In hello **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![Aggiungere lo snap-in certificati per l'account del computer](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="d4299-118">In hello **seleziona Computer** selezionare **computer locale: (hello computer su cui è in esecuzione questa console)** e fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="d4299-118">On hello **Select Computer** page, select **Local computer: (hello computer this console is running on)** and click **Finish**.</span></span>

    ![Aggiungere lo snap-in certificati, Seleziona computer](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="d4299-120">In hello **Aggiungi o Rimuovi Snap-in** finestra di dialogo, fare clic su **OK** tooadd hello certificati snap-in tooMMC.</span><span class="sxs-lookup"><span data-stu-id="d4299-120">In hello **Add or Remove Snap-ins** dialog, click **OK** tooadd hello certificates snap-in tooMMC.</span></span>

    ![Aggiungere certificati snap-in tooMMC - eseguita](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="d4299-122">Nella finestra MMC hello, fare clic su tooexpand **radice Console**.</span><span class="sxs-lookup"><span data-stu-id="d4299-122">In hello MMC window, click tooexpand **Console Root**.</span></span> <span data-ttu-id="d4299-123">Dovrebbe essere caricati hello snap-in certificati.</span><span class="sxs-lookup"><span data-stu-id="d4299-123">You should see hello Certificates snap-in loaded.</span></span> <span data-ttu-id="d4299-124">Fare clic su **certificati (Computer locale)** tooexpand.</span><span class="sxs-lookup"><span data-stu-id="d4299-124">Click **Certificates (Local Computer)** tooexpand.</span></span> <span data-ttu-id="d4299-125">Fare clic su hello tooexpand **personale** nodo, seguito da hello **certificati** nodo.</span><span class="sxs-lookup"><span data-stu-id="d4299-125">Click tooexpand hello **Personal** node, followed by hello **Certificates** node.</span></span>

    ![Aprire l'archivio certificati personali](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="d4299-127">Dovrebbe essere hello autofirmato che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="d4299-127">You should see hello self-signed certificate we created.</span></span> <span data-ttu-id="d4299-128">È possibile esaminare le proprietà di hello di hello certificato tooensure hello identificazione personale corrisponde a quello riportato in windows PowerShell hello al momento della creazione certificato hello.</span><span class="sxs-lookup"><span data-stu-id="d4299-128">You can examine hello properties of hello certificate tooensure hello thumbprint matches that reported on hello PowerShell windows when you created hello certificate.</span></span>
10. <span data-ttu-id="d4299-129">Selezionare hello certificato autofirmato e **destro del mouse su**.</span><span class="sxs-lookup"><span data-stu-id="d4299-129">Select hello self-signed certificate and **right click**.</span></span> <span data-ttu-id="d4299-130">Selezionare il menu di scelta rapida hello **tutte le attività** e selezionare **Esporta...** .</span><span class="sxs-lookup"><span data-stu-id="d4299-130">From hello right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![Esportare il certificato](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="d4299-132">In hello **esportazione guidata certificati**, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d4299-132">In hello **Certificate Export Wizard**, click **Next**.</span></span>

    ![Esportare il certificato, procedura guidata](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="d4299-134">In hello **Esporta chiave privata** selezionare **Sì, Esporta la chiave privata di hello**, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d4299-134">On hello **Export Private Key** page, select **Yes, export hello private key**, and click **Next**.</span></span>

    ![Esportare il certificato, chiave privata](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="d4299-136">È necessario esportare la chiave privata insieme certificato hello hello.</span><span class="sxs-lookup"><span data-stu-id="d4299-136">You MUST export hello private key along with hello certificate.</span></span> <span data-ttu-id="d4299-137">Se si specifica un file PFX che contiene la chiave privata per il certificato di hello hello, abilitare l'accesso LDAP sicuro per il dominio gestito ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="d4299-137">If you provide a PFX that does not contain hello private key for hello certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="d4299-138">In hello **formato File di esportazione** selezionare **scambio informazioni personali - PKCS #12 (. PFX)** come formato di file hello per hello certificato esportato.</span><span class="sxs-lookup"><span data-stu-id="d4299-138">On hello **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as hello file format for hello exported certificate.</span></span>

    ![Esportare il certificato, formato di file](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="d4299-140">Solo hello. Formato di file PFX è supportato.</span><span class="sxs-lookup"><span data-stu-id="d4299-140">Only hello .PFX file format is supported.</span></span> <span data-ttu-id="d4299-141">Non esportare toohello certificato hello. Formato file CER.</span><span class="sxs-lookup"><span data-stu-id="d4299-141">Do not export hello certificate toohello .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="d4299-142">In hello **sicurezza** pagina, seleziona hello **Password** opzione e digitare un hello tooprotect password. File PFX.</span><span class="sxs-lookup"><span data-stu-id="d4299-142">On hello **Security** page, select hello **Password** option and type in a password tooprotect hello .PFX file.</span></span> <span data-ttu-id="d4299-143">Prendere nota della password perché sarà necessaria nell'attività successiva hello.</span><span class="sxs-lookup"><span data-stu-id="d4299-143">Remember this password since it will be needed in hello next task.</span></span> <span data-ttu-id="d4299-144">Fare clic su **Avanti** tooproceed.</span><span class="sxs-lookup"><span data-stu-id="d4299-144">Click **Next** tooproceed.</span></span>

    ![<span data-ttu-id="d4299-145">Password per l'esportazione del certificato</span><span class="sxs-lookup"><span data-stu-id="d4299-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="d4299-146">Prendere nota della password.</span><span class="sxs-lookup"><span data-stu-id="d4299-146">Make a note of this password.</span></span> <span data-ttu-id="d4299-147">È necessario durante l'abilitazione di LDAP sicuro per questo dominio gestito in [attività 3: abilitare l'accesso LDAP sicuro per il dominio gestito hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="d4299-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for hello managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="d4299-148">In hello **tooExport File** , specificare il nome di file hello e la posizione in cui si desidera certificato hello tooexport.</span><span class="sxs-lookup"><span data-stu-id="d4299-148">On hello **File tooExport** page, specify hello file name and location where you'd like tooexport hello certificate.</span></span>

    ![Percorso per l'esportazione del certificato](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="d4299-150">Hello seguente pagina, scegliere **fine** file PFX del certificato tooa tooexport hello.</span><span class="sxs-lookup"><span data-stu-id="d4299-150">On hello following page, click **Finish** tooexport hello certificate tooa PFX file.</span></span> <span data-ttu-id="d4299-151">Verrà visualizzata nella finestra di conferma quando è stato esportato il certificato di hello.</span><span class="sxs-lookup"><span data-stu-id="d4299-151">You should see confirmation dialog when hello certificate has been exported.</span></span>

    ![Esportare il certificato, Fatto](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="d4299-153">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="d4299-153">Next step</span></span>
[<span data-ttu-id="d4299-154">Attività 3: abilitare l'accesso LDAP sicuro per il dominio gestito hello</span><span class="sxs-lookup"><span data-stu-id="d4299-154">Task 3 - enable secure LDAP for hello managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)

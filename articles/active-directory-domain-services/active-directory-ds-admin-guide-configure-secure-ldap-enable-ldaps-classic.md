---
title: aaaConfigure Secure LDAP (LDAPS) in servizi di dominio Active Directory di Azure | Documenti Microsoft
description: Configurare l'accesso LDAP sicuro (LDAPS) per un dominio gestito di Servizi di dominio Azure AD
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="2aedb-103">Configurare l'accesso LDAP sicuro (LDAPS) per un dominio gestito di Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="2aedb-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2aedb-104">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="2aedb-104">Before you begin</span></span>
<span data-ttu-id="2aedb-105">Assicurarsi di aver completato [attività 2 - esportazione hello sicura LDAP certificato tooa. Il file PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="2aedb-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="2aedb-106">Scegliere se toouse hello anteprima esperienza del portale Azure oppure hello Azure toocomplete portale classico di questa attività.</span><span class="sxs-lookup"><span data-stu-id="2aedb-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="2aedb-107">**Il portale di Azure (anteprima)**: [Enable secure LDAP utilizzando hello portale di Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="2aedb-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="2aedb-108">**Portale di Azure classico**: [Enable secure LDAP utilizzando il portale di Azure classico di hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="2aedb-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a><span data-ttu-id="2aedb-109">Attività 3: abilitare l'accesso LDAP sicuro per hello dominio gestito tramite il portale di Azure classico di hello</span><span class="sxs-lookup"><span data-stu-id="2aedb-109">Task 3 - enable secure LDAP for hello managed domain using hello classic Azure portal</span></span>
<span data-ttu-id="2aedb-110">tooenable secure LDAP, eseguire hello seguendo i passaggi di configurazione:</span><span class="sxs-lookup"><span data-stu-id="2aedb-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="2aedb-111">Passare toohello  **[portale di Azure classico](https://manage.windowsazure.com)**.</span><span class="sxs-lookup"><span data-stu-id="2aedb-111">Navigate toohello **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="2aedb-112">Seleziona hello **Active Directory** nodo nel riquadro di sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="2aedb-112">Select hello **Active Directory** node on hello left pane.</span></span>
3. <span data-ttu-id="2aedb-113">Selezionare hello Azure Active directory (anche noto tooas 'tenant'), per cui sono stati abilitati i servizi di dominio Active Directory di Azure.</span><span class="sxs-lookup"><span data-stu-id="2aedb-113">Select hello Azure AD directory (also referred tooas 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![Selezionare una directory di Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="2aedb-115">Fare clic su hello **configura** scheda.</span><span class="sxs-lookup"><span data-stu-id="2aedb-115">Click hello **Configure** tab.</span></span>

    ![Scheda Configura della directory](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="2aedb-117">Scorrere verso il basso toohello sezione **servizi di dominio**.</span><span class="sxs-lookup"><span data-stu-id="2aedb-117">Scroll down toohello section titled **domain services**.</span></span> <span data-ttu-id="2aedb-118">Dovrebbe essere un'opzione denominata **LDAP sicuro (LDAPS)** come illustrato nella seguente schermata hello:</span><span class="sxs-lookup"><span data-stu-id="2aedb-118">You should see an option titled **Secure LDAP (LDAPS)** as shown in hello following screenshot:</span></span>

    ![Sezione per la configurazione di Servizi di dominio](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="2aedb-120">Fare clic su hello **Configura certificato...**  toobring pulsante backup hello **Configura certificato per l'accesso LDAP sicuro** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="2aedb-120">Click hello **Configure certificate ...** button toobring up hello **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![Configura certificato per accesso LDAP sicuro](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="2aedb-122">Fare clic su seguenti sull'icona di cartella hello **FILE PFX con certificato** file PFX hello toospecify, che contiene il certificato di hello da toouse per toohello di accesso LDAP sicuro gestito dominio.</span><span class="sxs-lookup"><span data-stu-id="2aedb-122">Click hello folder icon following **PFX FILE WITH CERTIFICATE** toospecify hello PFX file, which contains hello certificate you wish toouse for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="2aedb-123">Anche immettere password hello specificata durante l'esportazione di file PFX del certificato toohello hello.</span><span class="sxs-lookup"><span data-stu-id="2aedb-123">Also enter hello password you specified when exporting hello certificate toohello PFX file.</span></span> <span data-ttu-id="2aedb-124">Quindi, fare clic su Fatto pulsante nella parte inferiore di hello hello.</span><span class="sxs-lookup"><span data-stu-id="2aedb-124">Then, click hello done button on hello bottom.</span></span>

    ![Specificare un file PFX di accesso LDAP sicuro e la password](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="2aedb-126">Hello **servizi di dominio** sezione di hello **configura** scheda deve ottenere visualizzato in grigio ed è in hello **in sospeso...**  dello stato per alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="2aedb-126">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="2aedb-127">Durante questo periodo, certificato LDAPS hello viene verificata per verificarne l'accuratezza e la protezione di LDAP è configurato per il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="2aedb-127">During this period, hello LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![LDAP sicuro - In sospeso](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="2aedb-129">Sono necessari circa 10 minuti too15 tooenable LDAP sicuro per il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="2aedb-129">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="2aedb-130">Se hello fornito certificato LDAP sicuro non corrisponde a hello richiesto criteri, accesso LDAP sicuro non è abilitato per la directory e viene visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="2aedb-130">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="2aedb-131">Ad esempio, il nome di dominio hello non è corretto, certificato hello è già scaduto o scadrà a breve.</span><span class="sxs-lookup"><span data-stu-id="2aedb-131">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="2aedb-132">Quando l'accesso LDAP sicuro è abilitata per il dominio gestito, hello **in sospeso...**  messaggio dovrebbe essere eliminato.</span><span class="sxs-lookup"><span data-stu-id="2aedb-132">When secure LDAP is successfully enabled for your managed domain, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="2aedb-133">Verrà visualizzata l'identificazione personale hello del certificato hello visualizzato.</span><span class="sxs-lookup"><span data-stu-id="2aedb-133">You should see hello thumbprint of hello certificate displayed.</span></span>

    ![LDAP sicuro abilitato](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a><span data-ttu-id="2aedb-135">Attività 4: abilitare l'accesso LDAP sicuro tramite hello internet</span><span class="sxs-lookup"><span data-stu-id="2aedb-135">Task 4 - enable secure LDAP access over hello internet</span></span>
<span data-ttu-id="2aedb-136">**Attività facoltative** : se non si prevede tooaccess hello dominio gestito utilizza LDAPS oltre hello internet, ignorare questa attività di configurazione.</span><span class="sxs-lookup"><span data-stu-id="2aedb-136">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="2aedb-137">Prima di iniziare questa attività, assicurarsi di aver completato i passaggi di hello descritti in [attività 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="2aedb-137">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span></span>

1. <span data-ttu-id="2aedb-138">Si noterà un'opzione troppo**hello abilitare SECURE LDAP accesso tramite INTERNET** in hello **servizi di dominio** sezione di hello **configura** pagina.</span><span class="sxs-lookup"><span data-stu-id="2aedb-138">You should see an option too**ENABLE SECURE LDAP ACCESS OVER hello INTERNET** in hello **domain services** section of hello **Configure** page.</span></span> <span data-ttu-id="2aedb-139">Questa opzione è impostata troppo**n** per impostazione predefinita poiché toohello accesso internet gestito dominio tramite LDAP sicuro è disabilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="2aedb-139">This option is set too**NO** by default since internet access toohello managed domain over secure LDAP is disabled by default.</span></span>

    ![LDAP sicuro abilitato](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="2aedb-141">Attiva/disattiva **hello abilitare SECURE LDAP accesso tramite INTERNET** troppo**Sì**.</span><span class="sxs-lookup"><span data-stu-id="2aedb-141">Toggle **ENABLE SECURE LDAP ACCESS OVER hello INTERNET** too**YES**.</span></span> <span data-ttu-id="2aedb-142">Fare clic su hello **salvare** pulsante sul pannello inferiore hello.</span><span class="sxs-lookup"><span data-stu-id="2aedb-142">Click hello **SAVE** button on hello bottom panel.</span></span>
    <span data-ttu-id="2aedb-143">![LDAP sicuro abilitato](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="2aedb-143">![Secure LDAP enabled](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="2aedb-144">Hello **servizi di dominio** sezione di hello **configura** scheda deve ottenere visualizzato in grigio ed è in hello **in sospeso...**  dello stato per alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="2aedb-144">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="2aedb-145">Dopo un po' di tempo è abilitato internet dominio gestito tooyour accesso LDAP sicuro.</span><span class="sxs-lookup"><span data-stu-id="2aedb-145">After some time, internet access tooyour managed domain over secure LDAP is enabled.</span></span>

    ![LDAP sicuro - In sospeso](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="2aedb-147">Sono necessari circa 10 minuti tooenable accesso a internet tramite LDAP sicuro per il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="2aedb-147">It takes about 10 minutes tooenable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="2aedb-148">Quando si tooyour di accesso LDAP sicuro dominio su hello internet è abilitata, hello **in sospeso...**  messaggio dovrebbe essere eliminato.</span><span class="sxs-lookup"><span data-stu-id="2aedb-148">When secure LDAP access tooyour managed domain over hello internet is successfully enabled, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="2aedb-149">Si dovrebbe essere indirizzo IP esterno hello possono essere utilizzati tooaccess directory over LDAPS nel campo hello **IP indirizzo per LDAPS accesso esterno**.</span><span class="sxs-lookup"><span data-stu-id="2aedb-149">You should see hello external IP address that can be used tooaccess your directory over LDAPS in hello field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![LDAP sicuro abilitato](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="2aedb-151">Attività 5: configurare DNS tooaccess hello dominio gestito da hello internet</span><span class="sxs-lookup"><span data-stu-id="2aedb-151">Task 5 - configure DNS tooaccess hello managed domain from hello internet</span></span>
<span data-ttu-id="2aedb-152">**Attività facoltative** : se non si prevede tooaccess hello dominio gestito utilizza LDAPS oltre hello internet, ignorare questa attività di configurazione.</span><span class="sxs-lookup"><span data-stu-id="2aedb-152">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="2aedb-153">Prima di iniziare questa attività, assicurarsi di aver completato i passaggi di hello descritti in [attività 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="2aedb-153">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="2aedb-154">Dopo aver abilitato l'accesso LDAP sicuro tramite hello internet per il dominio gestito, è necessario tooupdate DNS in modo che i computer client possano trovare il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="2aedb-154">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="2aedb-155">Alla fine di hello di attività 4, viene visualizzato un indirizzo IP esterno in hello **configura** scheda **IP indirizzo per LDAPS accesso esterno**.</span><span class="sxs-lookup"><span data-stu-id="2aedb-155">At hello end of task 4, an external IP address is displayed on hello **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="2aedb-156">Configurare il provider DNS esterno in modo che il nome DNS di hello del hello gestiti dominio (ad esempio, ' ldaps.contoso100.com') toothis punti l'indirizzo IP esterno.</span><span class="sxs-lookup"><span data-stu-id="2aedb-156">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="2aedb-157">In questo esempio, è necessario hello toocreate voce DNS seguenti:</span><span class="sxs-lookup"><span data-stu-id="2aedb-157">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="2aedb-158">La procedura è: si è ora pronto tooconnect toohello gestito hello di dominio utilizzando LDAP sicuro tramite internet.</span><span class="sxs-lookup"><span data-stu-id="2aedb-158">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="2aedb-159">Tenere presente che i computer client devono considerare attendibile correttamente autorità emittente hello di hello LDAPS certificato toobe in grado di tooconnect toohello gestiti dominio utilizzando LDAP.</span><span class="sxs-lookup"><span data-stu-id="2aedb-159">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="2aedb-160">Se si utilizza un'autorità di certificazione o di un'autorità di certificazione attendibile pubblicamente, non è necessario toodo alcuna operazione poiché i computer client attendibile queste autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="2aedb-160">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="2aedb-161">Se si utilizza un certificato autofirmato, è necessario tooinstall parte pubblica di hello del certificato autofirmato hello nell'archivio certificati attendibili hello in computer client hello.</span><span class="sxs-lookup"><span data-stu-id="2aedb-161">If you are using a self-signed certificate, you need tooinstall hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="2aedb-162">Blocco LDAPS accedere dominio gestito tooyour su hello internet</span><span class="sxs-lookup"><span data-stu-id="2aedb-162">Lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="2aedb-163">**Attività facoltative** : se non è stato abilitato LDAPS accesso toohello gestito dominio oltre hello internet, ignorare questa attività di configurazione.</span><span class="sxs-lookup"><span data-stu-id="2aedb-163">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="2aedb-164">Prima di iniziare questa attività, assicurarsi di aver completato i passaggi di hello descritti in [attività 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="2aedb-164">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="2aedb-165">Esporre il dominio gestito per l'accesso LDAPS su hello internet rappresenta una minaccia alla sicurezza.</span><span class="sxs-lookup"><span data-stu-id="2aedb-165">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="2aedb-166">Hello dominio gestito è raggiungibile da hello internet hello porta utilizzata per l'accesso LDAP sicuro (ovvero, la porta 636).</span><span class="sxs-lookup"><span data-stu-id="2aedb-166">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="2aedb-167">Pertanto, è possibile scegliere toorestrict accesso toohello gestito dominio toospecific noti gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="2aedb-167">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="2aedb-168">Per migliorare la sicurezza, creare un gruppo di sicurezza di rete (gruppo) e associarlo a subnet hello in cui sono abilitati i servizi di dominio Active Directory di Azure.</span><span class="sxs-lookup"><span data-stu-id="2aedb-168">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="2aedb-169">Hello tabella seguente viene illustrato un esempio di gruppo è possibile configurare, toolock verso il basso l'accesso LDAP sicuro tramite hello internet.</span><span class="sxs-lookup"><span data-stu-id="2aedb-169">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="2aedb-170">Hello gruppo contiene un set di regole che consentono l'accesso LDAPS in ingresso sulla porta TCP 636 solo da un set specificato di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="2aedb-170">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="2aedb-171">Hello predefinito 'DenyAll' regola verrà applicata tooall il traffico in ingresso di hello internet.</span><span class="sxs-lookup"><span data-stu-id="2aedb-171">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="2aedb-172">Hello NSG regola tooallow LDAPS tramite hello internet da indirizzi IP specificati ha una priorità maggiore hello regola DenyAll NSG.</span><span class="sxs-lookup"><span data-stu-id="2aedb-172">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![Esempio NSG toosecure LDAPS tramite hello internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="2aedb-174">**Altre informazioni** - [Gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="2aedb-174">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="2aedb-175">Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="2aedb-175">Related content</span></span>
* [<span data-ttu-id="2aedb-176">Guida introduttiva di Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="2aedb-176">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="2aedb-177">Amministrare un dominio gestito di Servizi di dominio Azure AD</span><span class="sxs-lookup"><span data-stu-id="2aedb-177">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* <span data-ttu-id="2aedb-178">[Administer Group Policy on an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-group-policy.md) (Amministrare i Criteri di gruppo in un dominio gestito da Azure AD Domain Services)</span><span class="sxs-lookup"><span data-stu-id="2aedb-178">[Administer Group Policy on an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-group-policy.md)</span></span>
* [<span data-ttu-id="2aedb-179">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="2aedb-179">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="2aedb-180">Creare un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="2aedb-180">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

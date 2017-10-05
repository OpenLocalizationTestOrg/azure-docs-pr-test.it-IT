---
title: Configurare l'accesso LDAP sicuro (LDAPS) in Azure Active Directory Domain Services | Microsoft Docs
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
ms.openlocfilehash: 3aafe209aad7383cd0610d147b5fdba673023c93
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="c9417-103">Configurare l'accesso LDAP sicuro (LDAPS) per un dominio gestito di Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="c9417-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c9417-104">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="c9417-104">Before you begin</span></span>
<span data-ttu-id="c9417-105">Assicurarsi di aver completato l'[Attività 2: Esportare il certificato LDAP sicuro in un file PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="c9417-105">Ensure you've completed [Task 2 - export the secure LDAP certificate to a .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="c9417-106">Scegliere se usare l'esperienza di anteprima del portale di Azure o il portale di Azure classico per completare questa attività.</span><span class="sxs-lookup"><span data-stu-id="c9417-106">Choose whether to use the preview Azure portal experience or the Azure classic portal to complete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="c9417-107">**Portale di Azure (anteprima)**: [Abilitare l'accesso LDAP sicuro tramite il portale di Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="c9417-107">**Azure portal (Preview)**: [Enable secure LDAP using the Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="c9417-108">**Portale di Azure classico**: [Abilitare l'accesso LDAP sicuro tramite il portale di Azure classico](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="c9417-108">**Azure classic portal**: [Enable secure LDAP using the classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal"></a><span data-ttu-id="c9417-109">Attività 3: Abilitare l'accesso LDAP sicuro per il dominio gestito tramite il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="c9417-109">Task 3 - enable secure LDAP for the managed domain using the classic Azure portal</span></span>
<span data-ttu-id="c9417-110">Per abilitare l'accesso LDAP sicuro, seguire questa procedura di configurazione:</span><span class="sxs-lookup"><span data-stu-id="c9417-110">To enable secure LDAP, perform the following configuration steps:</span></span>

1. <span data-ttu-id="c9417-111">Passare al **[portale di Azure classico](https://manage.windowsazure.com)**.</span><span class="sxs-lookup"><span data-stu-id="c9417-111">Navigate to the **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="c9417-112">Selezionare il nodo **Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="c9417-112">Select the **Active Directory** node on the left pane.</span></span>
3. <span data-ttu-id="c9417-113">Selezionare la directory di Azure AD, detta anche "tenant", per cui sono stati abilitati i Servizi di dominio Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9417-113">Select the Azure AD directory (also referred to as 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![Selezionare una directory di Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="c9417-115">Fare clic sulla scheda **Configure** .</span><span class="sxs-lookup"><span data-stu-id="c9417-115">Click the **Configure** tab.</span></span>

    ![Scheda Configura della directory](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="c9417-117">Scorrere fino alla sezione **Servizi di dominio**.</span><span class="sxs-lookup"><span data-stu-id="c9417-117">Scroll down to the section titled **domain services**.</span></span> <span data-ttu-id="c9417-118">Viene visualizzata l'opzione **Accesso LDAP sicuro (LDAPS)** , come illustrato nella schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="c9417-118">You should see an option titled **Secure LDAP (LDAPS)** as shown in the following screenshot:</span></span>

    ![Sezione per la configurazione di Servizi di dominio](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="c9417-120">Fare clic sul pulsante **Configura certificato...** per visualizzare la finestra di dialogo **Configura certificato per accesso LDAP sicuro**.</span><span class="sxs-lookup"><span data-stu-id="c9417-120">Click the **Configure certificate ...** button to bring up the **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![Configura certificato per accesso LDAP sicuro](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="c9417-122">Fare clic sull'icona cartella che segue il **File PFX con certificato** per specificare il file PFX contenente il certificato da usare per l'accesso LDAP sicuro al dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="c9417-122">Click the folder icon following **PFX FILE WITH CERTIFICATE** to specify the PFX file, which contains the certificate you wish to use for secure LDAP access to the managed domain.</span></span> <span data-ttu-id="c9417-123">Immettere anche la password specificata durante l'esportazione del certificato nel file PFX.</span><span class="sxs-lookup"><span data-stu-id="c9417-123">Also enter the password you specified when exporting the certificate to the PFX file.</span></span> <span data-ttu-id="c9417-124">Quindi fare clic sul pulsante Fine nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="c9417-124">Then, click the done button on the bottom.</span></span>

    ![Specificare un file PFX di accesso LDAP sicuro e la password](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="c9417-126">La sezione **Servizi di dominio** della scheda **Configura** verrà disattivata e rimarrà nello stato **In sospeso...** per alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="c9417-126">The **domain services** section of the **Configure** tab should get grayed out and is in the **Pending...** state for a few minutes.</span></span> <span data-ttu-id="c9417-127">Durante questo periodo, viene verificata l'accuratezza del certificato LDAPS e viene configurato l'accesso LDAP sicuro per il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="c9417-127">During this period, the LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![LDAP sicuro - In sospeso](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="c9417-129">Per abilitare l'accesso LDAP sicuro per il dominio gestito saranno necessari circa 10-15 minuti.</span><span class="sxs-lookup"><span data-stu-id="c9417-129">It takes about 10 to 15 minutes to enable secure LDAP for your managed domain.</span></span> <span data-ttu-id="c9417-130">Se il certificato LDAP sicuro fornito non soddisfa i criteri necessari, l'accesso LDAP sicuro non viene abilitato per la directory e viene visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="c9417-130">If the provided secure LDAP certificate does not match the required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="c9417-131">Ad esempio, il nome di dominio non è corretto, il certificato è già scaduto o scadrà presto.</span><span class="sxs-lookup"><span data-stu-id="c9417-131">For example, the domain name is incorrect, the certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="c9417-132">Il messaggio **In sospeso...** scomparirà non appena l'accesso LDAP sicuro per il dominio gestito sarà abilitato.</span><span class="sxs-lookup"><span data-stu-id="c9417-132">When secure LDAP is successfully enabled for your managed domain, the **Pending...** message should disappear.</span></span> <span data-ttu-id="c9417-133">Verrà visualizzata l'identificazione personale del certificato visualizzato.</span><span class="sxs-lookup"><span data-stu-id="c9417-133">You should see the thumbprint of the certificate displayed.</span></span>

    ![LDAP sicuro abilitato](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-the-internet"></a><span data-ttu-id="c9417-135">Attività 4: Abilitare l'accesso LDAP sicuro su Internet</span><span class="sxs-lookup"><span data-stu-id="c9417-135">Task 4 - enable secure LDAP access over the internet</span></span>
<span data-ttu-id="c9417-136">**Attività facoltativa** : ignorare questa attività di configurazione se non si intende accedere al dominio gestito usando l'accesso LDAP sicuro tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="c9417-136">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>

<span data-ttu-id="c9417-137">Prima di iniziare questa attività, assicurarsi di aver completato la procedura descritta nell' [attività 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="c9417-137">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span></span>

1. <span data-ttu-id="c9417-138">Nella sezione **Servizi di dominio** della pagina **Configura** viene visualizzata l'opzione **Abilita accesso LDAP sicuro tramite Internet**.</span><span class="sxs-lookup"><span data-stu-id="c9417-138">You should see an option to **ENABLE SECURE LDAP ACCESS OVER THE INTERNET** in the **domain services** section of the **Configure** page.</span></span> <span data-ttu-id="c9417-139">Il valore predefinito di questa impostazione è **No** , perché l'accesso LDAP sicuro al dominio gestito tramite Internet è disabilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="c9417-139">This option is set to **NO** by default since internet access to the managed domain over secure LDAP is disabled by default.</span></span>

    ![LDAP sicuro abilitato](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="c9417-141">Impostare **Abilita accesso LDAP sicuro tramite Internet** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="c9417-141">Toggle **ENABLE SECURE LDAP ACCESS OVER THE INTERNET** to **YES**.</span></span> <span data-ttu-id="c9417-142">Fare clic sul pulsante **Salva** nel riquadro inferiore.</span><span class="sxs-lookup"><span data-stu-id="c9417-142">Click the **SAVE** button on the bottom panel.</span></span>
    <span data-ttu-id="c9417-143">![LDAP sicuro abilitato](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="c9417-143">![Secure LDAP enabled](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="c9417-144">La sezione **Servizi di dominio** della scheda **Configura** verrà disattivata e rimarrà nello stato **In sospeso...** per alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="c9417-144">The **domain services** section of the **Configure** tab should get grayed out and is in the **Pending...** state for a few minutes.</span></span> <span data-ttu-id="c9417-145">Dopo un po' di tempo verrà abilitato l'accesso LDAP sicuro tramite Internet al dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="c9417-145">After some time, internet access to your managed domain over secure LDAP is enabled.</span></span>

    ![LDAP sicuro - In sospeso](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="c9417-147">Per abilitare l'accesso LDAP sicuro tramite Internet al dominio gestito sono necessari circa 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="c9417-147">It takes about 10 minutes to enable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="c9417-148">Il messaggio **In sospeso...** scomparirà non appena l'accesso LDAP sicuro al dominio gestito tramite Internet sarà abilitato.</span><span class="sxs-lookup"><span data-stu-id="c9417-148">When secure LDAP access to your managed domain over the internet is successfully enabled, the **Pending...** message should disappear.</span></span> <span data-ttu-id="c9417-149">Nel campo **Indirizzo IP esterno per l'accesso LDAPS**viene visualizzato l'indirizzo IP esterno che può essere usato per accedere alla directory tramite accesso LDAP sicuro.</span><span class="sxs-lookup"><span data-stu-id="c9417-149">You should see the external IP address that can be used to access your directory over LDAPS in the field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![LDAP sicuro abilitato](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-to-access-the-managed-domain-from-the-internet"></a><span data-ttu-id="c9417-151">Attività 5: Configurare il server DNS per l'accesso al dominio gestito da Internet</span><span class="sxs-lookup"><span data-stu-id="c9417-151">Task 5 - configure DNS to access the managed domain from the internet</span></span>
<span data-ttu-id="c9417-152">**Attività facoltativa** : ignorare questa attività di configurazione se non si intende accedere al dominio gestito usando l'accesso LDAP sicuro tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="c9417-152">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>

<span data-ttu-id="c9417-153">Prima di iniziare questa attività, assicurarsi di aver completato la procedura descritta nell' [attività 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="c9417-153">Before you begin this task, ensure you have completed the steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="c9417-154">Dopo aver attivato l'accesso LDAP sicuro tramite Internet al dominio gestito, è necessario aggiornare il server DNS in modo che i computer client possano trovare il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="c9417-154">Once you have enabled secure LDAP access over the internet for your managed domain, you need to update DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="c9417-155">Al termine dell'attività 4 nel campo **INDIRIZZO IP ESTERNO PER L'ACCESSO LDAPS** della scheda **Configura** viene visualizzato un indirizzo IP esterno.</span><span class="sxs-lookup"><span data-stu-id="c9417-155">At the end of task 4, an external IP address is displayed on the **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="c9417-156">Configurare il provider DNS esterno in modo che il nome DNS del dominio gestito, ad esempio "ldaps.contoso100.com", punti a questo indirizzo IP esterno.</span><span class="sxs-lookup"><span data-stu-id="c9417-156">Configure your external DNS provider so that the DNS name of the managed domain (for example, 'ldaps.contoso100.com') points to this external IP address.</span></span> <span data-ttu-id="c9417-157">Nell'esempio è necessario creare la voce DNS seguente:</span><span class="sxs-lookup"><span data-stu-id="c9417-157">In our example, we need to create the following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="c9417-158">La procedura è terminata ed è possibile connettersi al dominio gestito usando l'accesso LDAP sicuro tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="c9417-158">That's it - you are now ready to connect to the managed domain using secure LDAP over the internet.</span></span>

> [!WARNING]
> <span data-ttu-id="c9417-159">Tenere presente che i computer client devono considerare attendibile l'autorità emittente del certificato LDAPS per potersi connettere al dominio gestito tramite LDAPS.</span><span class="sxs-lookup"><span data-stu-id="c9417-159">Remember that client computers must trust the issuer of the LDAPS certificate to be able to connect successfully to the managed domain using LDAPS.</span></span> <span data-ttu-id="c9417-160">Un'autorità di certificazione aziendale o un'autorità di certificazione pubblicamente attendibile sono considerate attendibili dai computer client.</span><span class="sxs-lookup"><span data-stu-id="c9417-160">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need to do anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="c9417-161">Se si usa un certificato autofirmato è necessario installare la parte pubblica del certificato autofirmato nell'archivio certificati attendibili del computer client.</span><span class="sxs-lookup"><span data-stu-id="c9417-161">If you are using a self-signed certificate, you need to install the public part of the self-signed certificate into the trusted certificate store on the client computer.</span></span>
>
>


## <a name="lock-down-ldaps-access-to-your-managed-domain-over-the-internet"></a><span data-ttu-id="c9417-162">Blocco dell'accesso LDAPS al dominio gestito su Internet</span><span class="sxs-lookup"><span data-stu-id="c9417-162">Lock-down LDAPS access to your managed domain over the internet</span></span>
> [!NOTE]
> <span data-ttu-id="c9417-163">**Attività facoltativa**: ignorare questa attività di configurazione se non si ha l'accesso LDAPS abilitato al dominio gestito su Internet.</span><span class="sxs-lookup"><span data-stu-id="c9417-163">**Optional task** - If you have not enabled LDAPS access to the managed domain over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="c9417-164">Prima di iniziare questa attività, assicurarsi di aver completato la procedura descritta nell' [attività 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="c9417-164">Before you begin this task, ensure you have completed the steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="c9417-165">L'esposizione del dominio gestito per l'accesso LDAPS su Internet rappresenta una minaccia alla sicurezza.</span><span class="sxs-lookup"><span data-stu-id="c9417-165">Exposing your managed domain for LDAPS access over the internet represents a security threat.</span></span> <span data-ttu-id="c9417-166">Il dominio gestito è raggiungibile da Internet presso la porta usata per l'accesso LDAP sicuro, ovvero la porta 636.</span><span class="sxs-lookup"><span data-stu-id="c9417-166">The managed domain is reachable from the internet at the port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="c9417-167">Di conseguenza, è possibile scegliere di limitare l'accesso al dominio gestito a determinati indirizzi IP noti.</span><span class="sxs-lookup"><span data-stu-id="c9417-167">Therefore, you can choose to restrict access to the managed domain to specific known IP addresses.</span></span> <span data-ttu-id="c9417-168">Per migliorare la sicurezza, creare un gruppo di sicurezza di rete (NSG) e associarlo alla subnet in cui è stato abilitato Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="c9417-168">For improved security, create a network security group (NSG) and associate it with the subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="c9417-169">La tabella seguente illustra un esempio di gruppo di sicurezza di rete che è possibile configurare per bloccare l'accesso LDAP sicuro su Internet.</span><span class="sxs-lookup"><span data-stu-id="c9417-169">The following table illustrates a sample NSG you can configure, to lock down secure LDAP access over the internet.</span></span> <span data-ttu-id="c9417-170">Il gruppo di sicurezza di rete contiene alcune regole che consentono l'accesso LDAPS in ingresso sulla porta TCP 636 solo da un set specificato di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="c9417-170">The NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="c9417-171">La regola predefinita "DenyAll" si applica a tutto il traffico in ingresso da Internet.</span><span class="sxs-lookup"><span data-stu-id="c9417-171">The default 'DenyAll' rule applies to all other inbound traffic from the internet.</span></span> <span data-ttu-id="c9417-172">La regola del gruppo di sicurezza di rete per consentire l'accesso LDAPS su Internet da indirizzi IP specificati ha una priorità superiore rispetto alla regola DenyAll del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="c9417-172">The NSG rule to allow LDAPS access over the internet from specified IP addresses has a higher priority than the DenyAll NSG rule.</span></span>

![Gruppo di sicurezza di rete di esempio per proteggere l'accesso LDAPS su Internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="c9417-174">**Altre informazioni** - [Gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="c9417-174">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="c9417-175">Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="c9417-175">Related content</span></span>
* [<span data-ttu-id="c9417-176">Guida introduttiva di Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="c9417-176">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="c9417-177">Amministrare un dominio gestito di Servizi di dominio Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9417-177">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* <span data-ttu-id="c9417-178">[Administer Group Policy on an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-group-policy.md) (Amministrare i Criteri di gruppo in un dominio gestito da Azure AD Domain Services)</span><span class="sxs-lookup"><span data-stu-id="c9417-178">[Administer Group Policy on an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-group-policy.md)</span></span>
* [<span data-ttu-id="c9417-179">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="c9417-179">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="c9417-180">Creare un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="c9417-180">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

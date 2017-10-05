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
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 3b19f078b0d6dc3e02d951014056406fd1b099a8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="65517-103">Configurare l'accesso LDAP sicuro (LDAPS) per un dominio gestito di Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="65517-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="65517-104">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="65517-104">Before you begin</span></span>
<span data-ttu-id="65517-105">Assicurarsi di aver completato l'[Attività 2: Esportare il certificato LDAP sicuro in un file PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="65517-105">Ensure you've completed [Task 2 - export the secure LDAP certificate to a .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="65517-106">Scegliere se usare l'esperienza di anteprima del portale di Azure o il portale di Azure classico per completare questa attività.</span><span class="sxs-lookup"><span data-stu-id="65517-106">Choose whether to use the preview Azure portal experience or the Azure classic portal to complete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="65517-107">**Portale di Azure (anteprima)**: [Abilitare l'accesso LDAP sicuro tramite il portale di Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="65517-107">**Azure portal (Preview)**: [Enable secure LDAP using the Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="65517-108">**Portale di Azure classico**: [Abilitare l'accesso LDAP sicuro usando il portale di Azure classico](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="65517-108">**Azure classic portal**: [Enable secure LDAP using the classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview"></a><span data-ttu-id="65517-109">Attività 3: Abilitare l'accesso LDAP sicuro per il dominio gestito usando il portale di Azure (anteprima)</span><span class="sxs-lookup"><span data-stu-id="65517-109">Task 3 - enable secure LDAP for the managed domain using the Azure portal (Preview)</span></span>
<span data-ttu-id="65517-110">Per abilitare l'accesso LDAP sicuro, seguire questa procedura di configurazione:</span><span class="sxs-lookup"><span data-stu-id="65517-110">To enable secure LDAP, perform the following configuration steps:</span></span>

1. <span data-ttu-id="65517-111">Passare al **[portale di Azure](https://portal.azure.com)**.</span><span class="sxs-lookup"><span data-stu-id="65517-111">Navigate to the **[Azure portal](https://portal.azure.com)**.</span></span>

2. <span data-ttu-id="65517-112">Cercare "servizi di dominio" nella casella di ricerca **Cerca risorse**.</span><span class="sxs-lookup"><span data-stu-id="65517-112">Search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="65517-113">Selezionare **Azure AD Domain Services** dai risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="65517-113">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="65517-114">Nel pannello **Azure AD Domain Services** è indicato il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="65517-114">The **Azure AD Domain Services** blade lists your managed domain.</span></span>

    ![Trovare il dominio gestito di cui viene effettuato il provisioning](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="65517-116">Fare clic sul nome del dominio gestito (ad esempio, "contoso100.com") per visualizzare altre informazioni sul dominio.</span><span class="sxs-lookup"><span data-stu-id="65517-116">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span></span>

    ![Domain Services - Stato del provisioning](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="65517-118">Fare clic su **LDAP sicuro** nel riquadro di spostamento.</span><span class="sxs-lookup"><span data-stu-id="65517-118">Click **Secure LDAP** on the navigation pane.</span></span>

    ![Domain Services - Pannello LDAP sicuro](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. <span data-ttu-id="65517-120">Per impostazione predefinita, l'accesso LDAP sicuro al dominio gestito è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="65517-120">By default, secure LDAP access to your managed domain is disabled.</span></span> <span data-ttu-id="65517-121">Impostare **LDAP sicuro** su **Abilita**.</span><span class="sxs-lookup"><span data-stu-id="65517-121">Toggle **Secure LDAP** to **Enable**.</span></span>

    ![Abilitare LDAP sicuro](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. <span data-ttu-id="65517-123">Per impostazione predefinita, l'accesso LDAP sicuro al dominio gestito su Internet è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="65517-123">By default, secure LDAP access to your managed domain over the internet is disabled.</span></span> <span data-ttu-id="65517-124">Impostare **Abilita accesso LDAP sicuro tramite Internet** su **Abilita**, se necessario.</span><span class="sxs-lookup"><span data-stu-id="65517-124">Toggle **Allow secure LDAP access over the internet** to **Enable**, if desired.</span></span> 

6. <span data-ttu-id="65517-125">Fare clic sull'icona della cartella accanto a **File PFX con certificato LDAP sicuro**.</span><span class="sxs-lookup"><span data-stu-id="65517-125">Click the folder icon following **.PFX file with secure LDAP certificate**.</span></span> <span data-ttu-id="65517-126">Specificare il percorso del file PFX con il certificato per l'accesso LDAP sicuro al dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="65517-126">Specify the path to the PFX file with the certificate for secure LDAP access to the managed domain.</span></span>

7. <span data-ttu-id="65517-127">Specificare la **password per decrittografare il file PFX**.</span><span class="sxs-lookup"><span data-stu-id="65517-127">Specify the **Password to decrypt .PFX file**.</span></span> <span data-ttu-id="65517-128">Indicare la stessa password usata per l'esportazione del certificato nel file PFX.</span><span class="sxs-lookup"><span data-stu-id="65517-128">Provide the same password you used when exporting the certificate to the PFX file.</span></span>

8. <span data-ttu-id="65517-129">Al termine, fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="65517-129">When you are done, click the **Save** button.</span></span>

9. <span data-ttu-id="65517-130">Viene visualizzata una notifica che informa che è in corso la configurazione dell'accesso LDAP sicuro per il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="65517-130">You see a notification that informs you secure LDAP is being configured for the managed domain.</span></span> <span data-ttu-id="65517-131">Finché questa operazione non viene completata, non è possibile modificare altre impostazioni per il dominio.</span><span class="sxs-lookup"><span data-stu-id="65517-131">Until this operation is complete, you cannot modify other settings for the domain.</span></span>

    ![Configurazione dell'accesso LDAP sicuro per il dominio gestito](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> <span data-ttu-id="65517-133">Per abilitare l'accesso LDAP sicuro per il dominio gestito saranno necessari circa 10-15 minuti.</span><span class="sxs-lookup"><span data-stu-id="65517-133">It takes about 10 to 15 minutes to enable secure LDAP for your managed domain.</span></span> <span data-ttu-id="65517-134">Se il certificato LDAP sicuro fornito non soddisfa i criteri necessari, l'accesso LDAP sicuro non viene abilitato per la directory e viene visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="65517-134">If the provided secure LDAP certificate does not match the required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="65517-135">Ad esempio, il nome di dominio non è corretto, il certificato è già scaduto o scadrà presto.</span><span class="sxs-lookup"><span data-stu-id="65517-135">For example, the domain name is incorrect, the certificate has already expired or expires soon.</span></span> <span data-ttu-id="65517-136">In questo caso, riprovare con un certificato valido.</span><span class="sxs-lookup"><span data-stu-id="65517-136">In this case, retry with a valid certificate.</span></span>
>
>

<br>

## <a name="task-4---configure-dns-to-access-the-managed-domain-from-the-internet"></a><span data-ttu-id="65517-137">Attività 4: Configurare DNS per l'accesso al dominio gestito da Internet</span><span class="sxs-lookup"><span data-stu-id="65517-137">Task 4 - configure DNS to access the managed domain from the internet</span></span>
> [!NOTE]
> <span data-ttu-id="65517-138">**Attività facoltativa** : ignorare questa attività di configurazione se non si intende accedere al dominio gestito usando l'accesso LDAP sicuro tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="65517-138">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="65517-139">Prima di iniziare questa attività, assicurarsi di aver completato la procedura descritta nell' [attività 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="65517-139">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="65517-140">Dopo aver attivato l'accesso LDAP sicuro tramite Internet al dominio gestito, è necessario aggiornare il server DNS in modo che i computer client possano trovare il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="65517-140">Once you have enabled secure LDAP access over the internet for your managed domain, you need to update DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="65517-141">Al termine dell'attività 3, nel campo **INDIRIZZO IP ESTERNO PER L'ACCESSO LDAPS** del pannello **Proprietà** viene visualizzato un indirizzo IP esterno.</span><span class="sxs-lookup"><span data-stu-id="65517-141">At the end of task 3, an external IP address is displayed on the **Properties** blade in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="65517-142">Configurare il provider DNS esterno in modo che il nome DNS del dominio gestito, ad esempio "ldaps.contoso100.com", punti a questo indirizzo IP esterno.</span><span class="sxs-lookup"><span data-stu-id="65517-142">Configure your external DNS provider so that the DNS name of the managed domain (for example, 'ldaps.contoso100.com') points to this external IP address.</span></span> <span data-ttu-id="65517-143">Nell'esempio è necessario creare la voce DNS seguente:</span><span class="sxs-lookup"><span data-stu-id="65517-143">In our example, we need to create the following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="65517-144">La procedura è terminata ed è possibile connettersi al dominio gestito usando l'accesso LDAP sicuro tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="65517-144">That's it - you are now ready to connect to the managed domain using secure LDAP over the internet.</span></span>

> [!WARNING]
> <span data-ttu-id="65517-145">Tenere presente che i computer client devono considerare attendibile l'autorità emittente del certificato LDAPS per potersi connettere al dominio gestito tramite LDAPS.</span><span class="sxs-lookup"><span data-stu-id="65517-145">Remember that client computers must trust the issuer of the LDAPS certificate to be able to connect successfully to the managed domain using LDAPS.</span></span> <span data-ttu-id="65517-146">Se si usa un'autorità di certificazione pubblicamente attendibile, non sarà necessario eseguire alcuna operazione perché queste autorità sono considerate attendibili dai computer client.</span><span class="sxs-lookup"><span data-stu-id="65517-146">If you are using a publicly trusted certification authority, you do not need to do anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="65517-147">Se si usa un certificato autofirmato, installare la parte pubblica del certificato autofirmato nell'archivio certificati attendibili del computer client.</span><span class="sxs-lookup"><span data-stu-id="65517-147">If you are using a self-signed certificate, install the public part of the self-signed certificate into the trusted certificate store on the client computer.</span></span>
>
>


## <a name="task-5---lock-down-ldaps-access-to-your-managed-domain-over-the-internet"></a><span data-ttu-id="65517-148">Attività 5: Bloccare l'accesso LDAPS al dominio gestito su Internet</span><span class="sxs-lookup"><span data-stu-id="65517-148">Task 5 - lock-down LDAPS access to your managed domain over the internet</span></span>
> [!NOTE]
> <span data-ttu-id="65517-149">**Attività facoltativa**: ignorare questa attività di configurazione se non è stato abilitato l'accesso LDAPS al dominio gestito su Internet.</span><span class="sxs-lookup"><span data-stu-id="65517-149">**Optional task** - If you have not enabled LDAPS access to the managed domain over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="65517-150">Prima di iniziare questa attività, assicurarsi di aver completato la procedura descritta nell' [attività 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="65517-150">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="65517-151">L'esposizione del dominio gestito per l'accesso LDAPS su Internet rappresenta una minaccia alla sicurezza.</span><span class="sxs-lookup"><span data-stu-id="65517-151">Exposing your managed domain for LDAPS access over the internet represents a security threat.</span></span> <span data-ttu-id="65517-152">Il dominio gestito è raggiungibile da Internet presso la porta usata per l'accesso LDAP sicuro, ovvero la porta 636.</span><span class="sxs-lookup"><span data-stu-id="65517-152">The managed domain is reachable from the internet at the port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="65517-153">Di conseguenza, è possibile scegliere di limitare l'accesso al dominio gestito a determinati indirizzi IP noti.</span><span class="sxs-lookup"><span data-stu-id="65517-153">Therefore, you can choose to restrict access to the managed domain to specific known IP addresses.</span></span> <span data-ttu-id="65517-154">Per migliorare la sicurezza, creare un gruppo di sicurezza di rete (NSG) e associarlo alla subnet in cui è stato abilitato Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="65517-154">For improved security, create a network security group (NSG) and associate it with the subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="65517-155">La tabella seguente illustra un esempio di gruppo di sicurezza di rete che è possibile configurare per bloccare l'accesso LDAP sicuro su Internet.</span><span class="sxs-lookup"><span data-stu-id="65517-155">The following table illustrates a sample NSG you can configure, to lock down secure LDAP access over the internet.</span></span> <span data-ttu-id="65517-156">Il gruppo di sicurezza di rete contiene alcune regole che consentono l'accesso LDAPS in ingresso sulla porta TCP 636 solo da un set specificato di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="65517-156">The NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="65517-157">La regola predefinita "DenyAll" si applica a tutto il traffico in ingresso da Internet.</span><span class="sxs-lookup"><span data-stu-id="65517-157">The default 'DenyAll' rule applies to all other inbound traffic from the internet.</span></span> <span data-ttu-id="65517-158">La regola del gruppo di sicurezza di rete per consentire l'accesso LDAPS su Internet da indirizzi IP specificati ha una priorità superiore rispetto alla regola DenyAll del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="65517-158">The NSG rule to allow LDAPS access over the internet from specified IP addresses has a higher priority than the DenyAll NSG rule.</span></span>

![Gruppo di sicurezza di rete di esempio per proteggere l'accesso LDAPS su Internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="65517-160">**Altre informazioni** - [Gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="65517-160">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="65517-161">Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="65517-161">Related content</span></span>
* [<span data-ttu-id="65517-162">Guida introduttiva di Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="65517-162">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="65517-163">Amministrare un dominio gestito di Servizi di dominio Azure AD</span><span class="sxs-lookup"><span data-stu-id="65517-163">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* <span data-ttu-id="65517-164">[Administer Group Policy on an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-group-policy.md) (Amministrare i Criteri di gruppo in un dominio gestito da Azure AD Domain Services)</span><span class="sxs-lookup"><span data-stu-id="65517-164">[Administer Group Policy on an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-group-policy.md)</span></span>
* [<span data-ttu-id="65517-165">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="65517-165">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="65517-166">Creare un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="65517-166">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

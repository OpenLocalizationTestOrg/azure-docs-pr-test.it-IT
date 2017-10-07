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
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="c018e-103">Configurare l'accesso LDAP sicuro (LDAPS) per un dominio gestito di Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="c018e-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c018e-104">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="c018e-104">Before you begin</span></span>
<span data-ttu-id="c018e-105">Assicurarsi di aver completato [attività 2 - esportazione hello sicura LDAP certificato tooa. Il file PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="c018e-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="c018e-106">Scegliere se toouse hello anteprima esperienza del portale Azure oppure hello Azure toocomplete portale classico di questa attività.</span><span class="sxs-lookup"><span data-stu-id="c018e-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="c018e-107">**Il portale di Azure (anteprima)**: [Enable secure LDAP utilizzando hello portale di Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="c018e-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="c018e-108">**Portale di Azure classico**: [Enable secure LDAP utilizzando il portale di Azure classico di hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="c018e-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a><span data-ttu-id="c018e-109">Attività 3: abilitare l'accesso LDAP sicuro per hello dominio gestito utilizzando hello del portale di Azure (anteprima)</span><span class="sxs-lookup"><span data-stu-id="c018e-109">Task 3 - enable secure LDAP for hello managed domain using hello Azure portal (Preview)</span></span>
<span data-ttu-id="c018e-110">tooenable secure LDAP, eseguire hello seguendo i passaggi di configurazione:</span><span class="sxs-lookup"><span data-stu-id="c018e-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="c018e-111">Passare toohello  **[portale di Azure](https://portal.azure.com)**.</span><span class="sxs-lookup"><span data-stu-id="c018e-111">Navigate toohello **[Azure portal](https://portal.azure.com)**.</span></span>

2. <span data-ttu-id="c018e-112">Ricerca di "servizi di dominio' in hello **individuare risorse** casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="c018e-112">Search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="c018e-113">Selezionare **servizi di dominio Active Directory di Azure** dai risultati di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="c018e-113">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="c018e-114">Hello **servizi di dominio Active Directory di Azure** pannello elenca il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="c018e-114">hello **Azure AD Domain Services** blade lists your managed domain.</span></span>

    ![Trovare il dominio gestito di cui viene effettuato il provisioning](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="c018e-116">Fare clic su nome hello di hello gestito dominio (ad esempio, ' contoso100.com') toosee ulteriori dettagli su dominio hello.</span><span class="sxs-lookup"><span data-stu-id="c018e-116">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Domain Services - Stato del provisioning](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="c018e-118">Fare clic su **Secure LDAP** nel riquadro di spostamento hello.</span><span class="sxs-lookup"><span data-stu-id="c018e-118">Click **Secure LDAP** on hello navigation pane.</span></span>

    ![Domain Services - Pannello LDAP sicuro](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. <span data-ttu-id="c018e-120">Per impostazione predefinita, l'accesso LDAP sicuro tooyour una dominio gestito è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="c018e-120">By default, secure LDAP access tooyour managed domain is disabled.</span></span> <span data-ttu-id="c018e-121">Attiva/disattiva **Secure LDAP** troppo**abilitare**.</span><span class="sxs-lookup"><span data-stu-id="c018e-121">Toggle **Secure LDAP** too**Enable**.</span></span>

    ![Abilitare LDAP sicuro](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. <span data-ttu-id="c018e-123">Per impostazione predefinita, tooyour di accesso LDAP sicuro gestiti dominio tramite hello che Internet è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="c018e-123">By default, secure LDAP access tooyour managed domain over hello internet is disabled.</span></span> <span data-ttu-id="c018e-124">Attiva/disattiva **Consenti l'accesso LDAP sicuro su internet di hello** troppo**abilitare**, se necessario.</span><span class="sxs-lookup"><span data-stu-id="c018e-124">Toggle **Allow secure LDAP access over hello internet** too**Enable**, if desired.</span></span> 

6. <span data-ttu-id="c018e-125">Fare clic su seguenti sull'icona di cartella hello **. Il file PFX con certificato LDAP sicuro**.</span><span class="sxs-lookup"><span data-stu-id="c018e-125">Click hello folder icon following **.PFX file with secure LDAP certificate**.</span></span> <span data-ttu-id="c018e-126">Specificare file PFX di hello percorso toohello con certificato hello per accesso LDAP sicuro toohello una dominio gestita.</span><span class="sxs-lookup"><span data-stu-id="c018e-126">Specify hello path toohello PFX file with hello certificate for secure LDAP access toohello managed domain.</span></span>

7. <span data-ttu-id="c018e-127">Specificare hello **toodecrypt Password. Il file PFX**.</span><span class="sxs-lookup"><span data-stu-id="c018e-127">Specify hello **Password toodecrypt .PFX file**.</span></span> <span data-ttu-id="c018e-128">Fornire hello stessa password usata per l'esportazione di file PFX del certificato toohello hello.</span><span class="sxs-lookup"><span data-stu-id="c018e-128">Provide hello same password you used when exporting hello certificate toohello PFX file.</span></span>

8. <span data-ttu-id="c018e-129">Al termine, fare clic su hello **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="c018e-129">When you are done, click hello **Save** button.</span></span>

9. <span data-ttu-id="c018e-130">Viene visualizzata una notifica che informa l'utente che viene configurato per il dominio gestito hello LDAP sicuro.</span><span class="sxs-lookup"><span data-stu-id="c018e-130">You see a notification that informs you secure LDAP is being configured for hello managed domain.</span></span> <span data-ttu-id="c018e-131">Fino a quando questa operazione è stata completata, è possibile modificare altre impostazioni per il dominio hello.</span><span class="sxs-lookup"><span data-stu-id="c018e-131">Until this operation is complete, you cannot modify other settings for hello domain.</span></span>

    ![Configurare il protocollo LDAP sicuro per il dominio gestito hello](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> <span data-ttu-id="c018e-133">Sono necessari circa 10 minuti too15 tooenable LDAP sicuro per il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="c018e-133">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="c018e-134">Se hello fornito certificato LDAP sicuro non corrisponde a hello richiesto criteri, accesso LDAP sicuro non è abilitato per la directory e viene visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="c018e-134">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="c018e-135">Ad esempio, il nome di dominio hello non è corretto, certificato hello è già scaduto o scadrà a breve.</span><span class="sxs-lookup"><span data-stu-id="c018e-135">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span> <span data-ttu-id="c018e-136">In questo caso, riprovare con un certificato valido.</span><span class="sxs-lookup"><span data-stu-id="c018e-136">In this case, retry with a valid certificate.</span></span>
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="c018e-137">Attività 4: configurare DNS tooaccess hello dominio gestito da hello internet</span><span class="sxs-lookup"><span data-stu-id="c018e-137">Task 4 - configure DNS tooaccess hello managed domain from hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="c018e-138">**Attività facoltative** : se non si prevede tooaccess hello dominio gestito utilizza LDAPS oltre hello internet, ignorare questa attività di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c018e-138">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="c018e-139">Prima di iniziare questa attività, assicurarsi di aver completato i passaggi di hello descritti in [attività 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="c018e-139">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="c018e-140">Dopo aver abilitato l'accesso LDAP sicuro tramite hello internet per il dominio gestito, è necessario tooupdate DNS in modo che i computer client possano trovare il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="c018e-140">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="c018e-141">Alla fine di hello di attività 3, viene visualizzato un indirizzo IP esterno in hello **proprietà** pannello in **IP indirizzo per LDAPS accesso esterno**.</span><span class="sxs-lookup"><span data-stu-id="c018e-141">At hello end of task 3, an external IP address is displayed on hello **Properties** blade in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="c018e-142">Configurare il provider DNS esterno in modo che il nome DNS di hello del hello gestiti dominio (ad esempio, ' ldaps.contoso100.com') toothis punti l'indirizzo IP esterno.</span><span class="sxs-lookup"><span data-stu-id="c018e-142">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="c018e-143">In questo esempio, è necessario hello toocreate voce DNS seguenti:</span><span class="sxs-lookup"><span data-stu-id="c018e-143">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="c018e-144">La procedura è: si è ora pronto tooconnect toohello gestito hello di dominio utilizzando LDAP sicuro tramite internet.</span><span class="sxs-lookup"><span data-stu-id="c018e-144">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="c018e-145">Tenere presente che i computer client devono considerare attendibile correttamente autorità emittente hello di hello LDAPS certificato toobe in grado di tooconnect toohello gestiti dominio utilizzando LDAP.</span><span class="sxs-lookup"><span data-stu-id="c018e-145">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="c018e-146">Se si utilizza un'autorità di certificazione attendibile pubblicamente, non è necessario toodo alcuna operazione poiché i computer client attendibile queste autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="c018e-146">If you are using a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="c018e-147">Se si utilizza un certificato autofirmato, è possibile installare parte pubblica di hello del certificato autofirmato hello nell'archivio certificati attendibili hello in computer client hello.</span><span class="sxs-lookup"><span data-stu-id="c018e-147">If you are using a self-signed certificate, install hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="c018e-148">Attività 5 - blocco LDAPS accesso tooyour gestiti hello di dominio tramite internet</span><span class="sxs-lookup"><span data-stu-id="c018e-148">Task 5 - lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="c018e-149">**Attività facoltative** : se non è stato abilitato LDAPS accesso toohello gestito dominio oltre hello internet, ignorare questa attività di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c018e-149">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="c018e-150">Prima di iniziare questa attività, assicurarsi di aver completato i passaggi di hello descritti in [attività 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="c018e-150">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="c018e-151">Esporre il dominio gestito per l'accesso LDAPS su hello internet rappresenta una minaccia alla sicurezza.</span><span class="sxs-lookup"><span data-stu-id="c018e-151">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="c018e-152">Hello dominio gestito è raggiungibile da hello internet hello porta utilizzata per l'accesso LDAP sicuro (ovvero, la porta 636).</span><span class="sxs-lookup"><span data-stu-id="c018e-152">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="c018e-153">Pertanto, è possibile scegliere toorestrict accesso toohello gestito dominio toospecific noti gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="c018e-153">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="c018e-154">Per migliorare la sicurezza, creare un gruppo di sicurezza di rete (gruppo) e associarlo a subnet hello in cui sono abilitati i servizi di dominio Active Directory di Azure.</span><span class="sxs-lookup"><span data-stu-id="c018e-154">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="c018e-155">Hello tabella seguente viene illustrato un esempio di gruppo è possibile configurare, toolock verso il basso l'accesso LDAP sicuro tramite hello internet.</span><span class="sxs-lookup"><span data-stu-id="c018e-155">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="c018e-156">Hello gruppo contiene un set di regole che consentono l'accesso LDAPS in ingresso sulla porta TCP 636 solo da un set specificato di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="c018e-156">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="c018e-157">Hello predefinito 'DenyAll' regola verrà applicata tooall il traffico in ingresso di hello internet.</span><span class="sxs-lookup"><span data-stu-id="c018e-157">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="c018e-158">Hello NSG regola tooallow LDAPS tramite hello internet da indirizzi IP specificati ha una priorità maggiore hello regola DenyAll NSG.</span><span class="sxs-lookup"><span data-stu-id="c018e-158">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![Esempio NSG toosecure LDAPS tramite hello internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="c018e-160">**Altre informazioni** - [Gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="c018e-160">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="c018e-161">Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="c018e-161">Related content</span></span>
* [<span data-ttu-id="c018e-162">Guida introduttiva di Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="c018e-162">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="c018e-163">Amministrare un dominio gestito di Servizi di dominio Azure AD</span><span class="sxs-lookup"><span data-stu-id="c018e-163">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* <span data-ttu-id="c018e-164">[Administer Group Policy on an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-group-policy.md) (Amministrare i Criteri di gruppo in un dominio gestito da Azure AD Domain Services)</span><span class="sxs-lookup"><span data-stu-id="c018e-164">[Administer Group Policy on an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-group-policy.md)</span></span>
* [<span data-ttu-id="c018e-165">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="c018e-165">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="c018e-166">Creare un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="c018e-166">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

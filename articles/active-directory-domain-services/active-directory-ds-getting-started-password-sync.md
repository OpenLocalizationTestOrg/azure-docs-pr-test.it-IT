---
title: 'Azure Active Directory Domain Services: abilitare la sincronizzazione password | Microsoft Docs'
description: Introduzione a Servizi di dominio Azure Active Directory
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 5a32a0df-a3ca-4ebe-b980-91f58f8030fc
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 4b6da997f44860dccb2aa2571ce099ab2d0231f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-password-synchronization-to-azure-active-directory-domain-services"></a><span data-ttu-id="d2f63-103">Abilitare la sincronizzazione password con Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="d2f63-103">Enable password synchronization to Azure Active Directory Domain Services</span></span>
<span data-ttu-id="d2f63-104">Nelle attività precedenti è stato abilitato Azure Active Directory Domain Services per il tenant di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d2f63-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="d2f63-105">L'attività successiva prevede l'abilitazione della sincronizzazione degli hash delle credenziali necessari per l'autenticazione NTLM (NT LAN Manager) e Kerberos con Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d2f63-105">The next task is to enable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication to Azure AD Domain Services.</span></span> <span data-ttu-id="d2f63-106">Al termine della configurazione della sincronizzazione delle credenziali, gli utenti potranno accedere al dominio gestito con le credenziali aziendali.</span><span class="sxs-lookup"><span data-stu-id="d2f63-106">After you've set up credential synchronization, users can sign in to the managed domain with their corporate credentials.</span></span>

<span data-ttu-id="d2f63-107">La procedura da eseguire è diversa per gli account utente solo cloud rispetto agli account utente sincronizzati dalla directory locale tramite Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d2f63-107">The steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span>  <span data-ttu-id="d2f63-108">Se il tenant di Azure AD include una combinazione di utenti solo cloud e utenti dell'istanza locale di AD, è necessario eseguire entrambe le procedure.</span><span class="sxs-lookup"><span data-stu-id="d2f63-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need to perform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="d2f63-109">**Account utente solo cloud**: [Sincronizzare le password per gli account utente solo cloud con il dominio gestito](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="d2f63-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts to your managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="d2f63-110">**Account utente locali**: [Sincronizzare le password per gli account utente sincronizzati dall'istanza locale di AD con il dominio gestito](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="d2f63-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD to your managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-to-your-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="d2f63-111">Attività 5: Abilitare la sincronizzazione password nel dominio gestito per gli account utente solo cloud</span><span class="sxs-lookup"><span data-stu-id="d2f63-111">Task 5: enable password synchronization to your managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="d2f63-112">Per autenticare gli utenti nel dominio gestito, Azure Active Directory Domain Services necessita di hash delle credenziali in un formato idoneo per l'autenticazione NTLM e Kerberos.</span><span class="sxs-lookup"><span data-stu-id="d2f63-112">To authenticate users on the managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="d2f63-113">Azure AD genera e archivia gli hash delle credenziali nel formato necessario per l'autenticazione NTLM o Kerberos solo dopo l'abilitazione di Azure Active Directory Domain Services per il tenant.</span><span class="sxs-lookup"><span data-stu-id="d2f63-113">Azure AD does not generate or store credential hashes in the format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="d2f63-114">Per ovvi motivi di sicurezza, Azure AD non archivia nemmeno le credenziali di tipo password in un formato non crittografato.</span><span class="sxs-lookup"><span data-stu-id="d2f63-114">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="d2f63-115">Azure AD quindi non può generare automaticamente questi hash delle credenziali NTLM o Kerberos in base alle credenziali esistenti degli utenti.</span><span class="sxs-lookup"><span data-stu-id="d2f63-115">Therefore, Azure AD does not have a way to automatically generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="d2f63-116">Se l'organizzazione include account utente solo cloud, gli utenti che devono usare Azure Active Directory Domain Services devono cambiare le proprie password.</span><span class="sxs-lookup"><span data-stu-id="d2f63-116">If your organization has cloud-only user accounts, users who need to use Azure Active Directory Domain Services must change their passwords.</span></span> <span data-ttu-id="d2f63-117">Un account utente solo cloud è un account creato nella directory di Azure AD tramite il portale di Azure o i cmdlet di Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2f63-117">A cloud-only user account is an account that was created in your Azure AD directory using either the Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="d2f63-118">Questi account utente non vengono sincronizzati da una directory locale.</span><span class="sxs-lookup"><span data-stu-id="d2f63-118">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="d2f63-119">Questo processo di modifica delle password determina la generazione in Azure AD degli hash delle credenziali richiesti da Azure Active Directory Domain Services per l'autenticazione Kerberos e NTLM.</span><span class="sxs-lookup"><span data-stu-id="d2f63-119">This password change process causes the credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication to be generated in Azure AD.</span></span> <span data-ttu-id="d2f63-120">È possibile impostare come scadute le password per tutti gli utenti del tenant che devono usare Azure Active Directory Domain Services oppure richiedere a tali utenti di cambiare le proprie password.</span><span class="sxs-lookup"><span data-stu-id="d2f63-120">You can either expire the passwords for all users in the tenant who need to use Azure Active Directory Domain Services or instruct them to change their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="d2f63-121">Abilitare la generazione di hash di credenziali NTLM e Kerberos per account utente solo cloud</span><span class="sxs-lookup"><span data-stu-id="d2f63-121">Enable NTLM and Kerberos credential hash generation for a cloud-only user account</span></span>
<span data-ttu-id="d2f63-122">Di seguito sono riportate le istruzioni che è necessario fornire agli utenti finali affinché possano cambiare le proprie password:</span><span class="sxs-lookup"><span data-stu-id="d2f63-122">Here are the instructions you need to provide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="d2f63-123">Andare alla pagina del [pannello di accesso di Azure AD](http://myapps.microsoft.com) per l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="d2f63-123">Go to the [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![Avviare il pannello di accesso di Azure AD](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="d2f63-125">Nell'angolo superiore destro fare clic sul nome e scegliere **Profilo** dal menu.</span><span class="sxs-lookup"><span data-stu-id="d2f63-125">In the top right corner, click on your name and select **Profile** from the menu.</span></span>

    ![Selezionare un profilo](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="d2f63-127">Nella pagina **Profilo** fare clic su **Cambia password**.</span><span class="sxs-lookup"><span data-stu-id="d2f63-127">On the **Profile** page, click on **Change password**.</span></span>

    ![Fare clic su "Cambia password"](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > <span data-ttu-id="d2f63-129">Se l'opzione **Cambia password** non è visualizzata nella finestra del pannello di accesso, verificare che l'organizzazione abbia configurato la [gestione delle password in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="d2f63-129">If the **Change password** option is not displayed in the Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span></span>
   >
   >
4. <span data-ttu-id="d2f63-130">Nella pagina **Cambia password** digitare la password esistente (precedente) e quindi digitare e confermare una nuova password.</span><span class="sxs-lookup"><span data-stu-id="d2f63-130">On the **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![Creare una rete virtuale per Servizi di dominio Azure AD.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="d2f63-132">Fare clic su **invia**.</span><span class="sxs-lookup"><span data-stu-id="d2f63-132">Click **submit**.</span></span>

<span data-ttu-id="d2f63-133">Dopo alcuni minuti dalla modifica, la nuova password è utilizzabile in Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d2f63-133">A few minutes after you have changed your password, the new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="d2f63-134">Dopo alcuni minuti aggiuntivi (in genere circa 20), è possibile accedere ai computer aggiunti al dominio gestito usando la password appena cambiata.</span><span class="sxs-lookup"><span data-stu-id="d2f63-134">After a few more minutes (typically, about 20 minutes), you can sign in to computers that are joined to the managed domain by using the newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="d2f63-135">Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="d2f63-135">Related Content</span></span>
* [<span data-ttu-id="d2f63-136">Come aggiornare la password</span><span class="sxs-lookup"><span data-stu-id="d2f63-136">How to update your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="d2f63-137">Introduzione alla gestione delle password in Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2f63-137">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="d2f63-138">Abilitare la sincronizzazione password in Azure Active Directory Domain Services per un tenant di Azure AD sincronizzato</span><span class="sxs-lookup"><span data-stu-id="d2f63-138">Enable password synchronization to Azure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="d2f63-139">Amministrare un dominio gestito di Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="d2f63-139">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="d2f63-140">Aggiungere una macchina virtuale Windows a un dominio gestito di Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="d2f63-140">Join a Windows virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="d2f63-141">Aggiungere una macchina virtuale Red Hat Enterprise Linux a un dominio gestito di Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="d2f63-141">Join a Red Hat Enterprise Linux virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)

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
ms.openlocfilehash: 8e073df9de2996f5ad159dda746881c014ea3d66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="52a30-103">Abilitare la sincronizzazione di password tooAzure servizi di dominio Active Directory</span><span class="sxs-lookup"><span data-stu-id="52a30-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="52a30-104">Nelle attività precedenti è stato abilitato Azure Active Directory Domain Services per il tenant di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52a30-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="52a30-105">attività successiva Hello è tooenable sincronizzazione degli hash delle credenziali necessarie per tooAzure autenticazione NT LAN Manager (NTLM) e Kerberos servizi di dominio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="52a30-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="52a30-106">Dopo aver configurato la sincronizzazione delle credenziali, gli utenti possono accedere toohello dominio gestiti con le proprie credenziali aziendali.</span><span class="sxs-lookup"><span data-stu-id="52a30-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="52a30-107">Hello fasi sono diverse per gli account utente e di account utente solo cloud sincronizzate dalla directory locale con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="52a30-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span>  <span data-ttu-id="52a30-108">Se il tenant di Azure AD ha una combinazione di cloud solo gli utenti e gli utenti da locale AD, è necessario tooperform entrambi i passaggi.</span><span class="sxs-lookup"><span data-stu-id="52a30-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="52a30-109">**Gli account utente solo cloud**: [sincronizzare le password per utenti basata esclusivamente sul cloud gli account di dominio gestiti tooyour](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="52a30-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="52a30-110">**Account utente locali**: [sincronizzare le password per gli account utente sincronizzati da locale AD tooyour gestiti dominio](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="52a30-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="52a30-111">Attività 5: abilitare dominio gestiti con tooyour di sincronizzazione password per gli account utente solo cloud</span><span class="sxs-lookup"><span data-stu-id="52a30-111">Task 5: enable password synchronization tooyour managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="52a30-112">gli utenti tooauthenticate hello gestite dominio, Azure Active Directory Domain Services richiede credenziali hash in un formato adatto per l'autenticazione NTLM e Kerberos.</span><span class="sxs-lookup"><span data-stu-id="52a30-112">tooauthenticate users on hello managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="52a30-113">Azure Active Directory non generare o archiviare gli hash delle credenziali nel formato hello necessaria per l'autenticazione NTLM o Kerberos, finché non si abilita Azure Active Directory Domain Services per il tenant.</span><span class="sxs-lookup"><span data-stu-id="52a30-113">Azure AD does not generate or store credential hashes in hello format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="52a30-114">Per ovvi motivi di sicurezza, Azure AD non archivia nemmeno le credenziali di tipo password in un formato non crittografato.</span><span class="sxs-lookup"><span data-stu-id="52a30-114">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="52a30-115">Pertanto, Azure AD è tooautomatically un modo generare degli hash delle credenziali NTLM o Kerberos in base alle credenziali esistenti degli utenti.</span><span class="sxs-lookup"><span data-stu-id="52a30-115">Therefore, Azure AD does not have a way tooautomatically generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="52a30-116">Se l'organizzazione dispone di account utente solo cloud, gli utenti che richiedono servizi di dominio Active Directory di toouse Azure devono modificare le password.</span><span class="sxs-lookup"><span data-stu-id="52a30-116">If your organization has cloud-only user accounts, users who need toouse Azure Active Directory Domain Services must change their passwords.</span></span> <span data-ttu-id="52a30-117">Un account utente solo cloud è un account che è stato creato nella directory di Azure AD utilizzando hello portale di Azure o i cmdlet di Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52a30-117">A cloud-only user account is an account that was created in your Azure AD directory using either hello Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="52a30-118">Questi account utente non vengono sincronizzati da una directory locale.</span><span class="sxs-lookup"><span data-stu-id="52a30-118">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="52a30-119">Questo processo di modifica password comporta credenziali hello gli hash richiesti da Azure Active Directory Domain Services per toobe di autenticazione Kerberos e NTLM generato in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52a30-119">This password change process causes hello credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication toobe generated in Azure AD.</span></span> <span data-ttu-id="52a30-120">Si può scadere password hello è per tutti gli utenti di hello tenant che necessitano di toouse Azure Active Directory Domain Services oppure indicano loro toochange le proprie password.</span><span class="sxs-lookup"><span data-stu-id="52a30-120">You can either expire hello passwords for all users in hello tenant who need toouse Azure Active Directory Domain Services or instruct them toochange their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="52a30-121">Abilitare la generazione di hash di credenziali NTLM e Kerberos per account utente solo cloud</span><span class="sxs-lookup"><span data-stu-id="52a30-121">Enable NTLM and Kerberos credential hash generation for a cloud-only user account</span></span>
<span data-ttu-id="52a30-122">Di seguito sono istruzioni hello che occorre tooprovide utenti, essi possono modificare la password:</span><span class="sxs-lookup"><span data-stu-id="52a30-122">Here are hello instructions you need tooprovide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="52a30-123">Passare toohello [Pannello di accesso AD Azure](http://myapps.microsoft.com) pagina per l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="52a30-123">Go toohello [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![Avviare il pannello di accesso di hello AD Azure](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="52a30-125">In hello angolo superiore destro, fare clic sul proprio nome e selezionare **profilo** dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="52a30-125">In hello top right corner, click on your name and select **Profile** from hello menu.</span></span>

    ![Selezionare un profilo](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="52a30-127">In hello **profilo** pagina, fare clic su **Cambia password**.</span><span class="sxs-lookup"><span data-stu-id="52a30-127">On hello **Profile** page, click on **Change password**.</span></span>

    ![Fare clic su "Cambia password"](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > <span data-ttu-id="52a30-129">Se hello **Cambia password** opzione non viene visualizzata nella finestra Pannello di accesso hello, assicurarsi che l'organizzazione ha configurato [gestione delle password in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="52a30-129">If hello **Change password** option is not displayed in hello Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span></span>
   >
   >
4. <span data-ttu-id="52a30-130">In hello **modifica password** pagina, digitare la password esistente (precedente), digitare una nuova password e quindi confermarla.</span><span class="sxs-lookup"><span data-stu-id="52a30-130">On hello **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![Creare una rete virtuale per Servizi di dominio Azure AD.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="52a30-132">Fare clic su **invia**.</span><span class="sxs-lookup"><span data-stu-id="52a30-132">Click **submit**.</span></span>

<span data-ttu-id="52a30-133">Alcuni minuti dopo aver modificato la password, hello nuova password non può essere usata in Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="52a30-133">A few minutes after you have changed your password, hello new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="52a30-134">Dopo alcuni minuti (in genere, circa 20 minuti), è possibile accedere toocomputers di dominio gestiti toohello unita in join tramite password hello appena modificata.</span><span class="sxs-lookup"><span data-stu-id="52a30-134">After a few more minutes (typically, about 20 minutes), you can sign in toocomputers that are joined toohello managed domain by using hello newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="52a30-135">Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="52a30-135">Related Content</span></span>
* [<span data-ttu-id="52a30-136">Come tooupdate la propria password</span><span class="sxs-lookup"><span data-stu-id="52a30-136">How tooupdate your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="52a30-137">Introduzione alla gestione delle password in Azure AD</span><span class="sxs-lookup"><span data-stu-id="52a30-137">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="52a30-138">Abilitare la sincronizzazione delle password del tenant tooAzure dominio servizi di Active Directory per una sincronizzazione Azure AD</span><span class="sxs-lookup"><span data-stu-id="52a30-138">Enable password synchronization tooAzure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="52a30-139">Amministrare un dominio gestito di Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="52a30-139">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="52a30-140">Aggiunta a un dominio di Azure Active Directory Domain Services gestiti tooan Windows macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="52a30-140">Join a Windows virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="52a30-141">Aggiunta a un dominio di Azure Active Directory Domain Services gestiti tooan Red Hat Enterprise Linux macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="52a30-141">Join a Red Hat Enterprise Linux virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)

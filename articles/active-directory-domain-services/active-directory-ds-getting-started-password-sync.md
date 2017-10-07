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
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>Abilitare la sincronizzazione di password tooAzure servizi di dominio Active Directory
Nelle attività precedenti è stato abilitato Azure Active Directory Domain Services per il tenant di Azure Active Directory (Azure AD). attività successiva Hello è tooenable sincronizzazione degli hash delle credenziali necessarie per tooAzure autenticazione NT LAN Manager (NTLM) e Kerberos servizi di dominio Active Directory. Dopo aver configurato la sincronizzazione delle credenziali, gli utenti possono accedere toohello dominio gestiti con le proprie credenziali aziendali.

Hello fasi sono diverse per gli account utente e di account utente solo cloud sincronizzate dalla directory locale con Azure AD Connect.  Se il tenant di Azure AD ha una combinazione di cloud solo gli utenti e gli utenti da locale AD, è necessario tooperform entrambi i passaggi.

<br>

> [!div class="op_single_selector"]
> * **Gli account utente solo cloud**: [sincronizzare le password per utenti basata esclusivamente sul cloud gli account di dominio gestiti tooyour](active-directory-ds-getting-started-password-sync.md)
> * **Account utente locali**: [sincronizzare le password per gli account utente sincronizzati da locale AD tooyour gestiti dominio](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a>Attività 5: abilitare dominio gestiti con tooyour di sincronizzazione password per gli account utente solo cloud
gli utenti tooauthenticate hello gestite dominio, Azure Active Directory Domain Services richiede credenziali hash in un formato adatto per l'autenticazione NTLM e Kerberos. Azure Active Directory non generare o archiviare gli hash delle credenziali nel formato hello necessaria per l'autenticazione NTLM o Kerberos, finché non si abilita Azure Active Directory Domain Services per il tenant. Per ovvi motivi di sicurezza, Azure AD non archivia nemmeno le credenziali di tipo password in un formato non crittografato. Pertanto, Azure AD è tooautomatically un modo generare degli hash delle credenziali NTLM o Kerberos in base alle credenziali esistenti degli utenti.

> [!NOTE]
> Se l'organizzazione dispone di account utente solo cloud, gli utenti che richiedono servizi di dominio Active Directory di toouse Azure devono modificare le password. Un account utente solo cloud è un account che è stato creato nella directory di Azure AD utilizzando hello portale di Azure o i cmdlet di Azure AD PowerShell. Questi account utente non vengono sincronizzati da una directory locale.
>
>

Questo processo di modifica password comporta credenziali hello gli hash richiesti da Azure Active Directory Domain Services per toobe di autenticazione Kerberos e NTLM generato in Azure AD. Si può scadere password hello è per tutti gli utenti di hello tenant che necessitano di toouse Azure Active Directory Domain Services oppure indicano loro toochange le proprie password.

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a>Abilitare la generazione di hash di credenziali NTLM e Kerberos per account utente solo cloud
Di seguito sono istruzioni hello che occorre tooprovide utenti, essi possono modificare la password:

1. Passare toohello [Pannello di accesso AD Azure](http://myapps.microsoft.com) pagina per l'organizzazione.

    ![Avviare il pannello di accesso di hello AD Azure](./media/active-directory-domain-services-getting-started/access-panel.png)

2. In hello angolo superiore destro, fare clic sul proprio nome e selezionare **profilo** dal menu di hello.

    ![Selezionare un profilo](./media/active-directory-domain-services-getting-started/select-profile.png)

3. In hello **profilo** pagina, fare clic su **Cambia password**.

    ![Fare clic su "Cambia password"](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > Se hello **Cambia password** opzione non viene visualizzata nella finestra Pannello di accesso hello, assicurarsi che l'organizzazione ha configurato [gestione delle password in Azure AD](../active-directory/active-directory-passwords-getting-started.md).
   >
   >
4. In hello **modifica password** pagina, digitare la password esistente (precedente), digitare una nuova password e quindi confermarla.

    ![Creare una rete virtuale per Servizi di dominio Azure AD.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. Fare clic su **invia**.

Alcuni minuti dopo aver modificato la password, hello nuova password non può essere usata in Azure Active Directory Domain Services. Dopo alcuni minuti (in genere, circa 20 minuti), è possibile accedere toocomputers di dominio gestiti toohello unita in join tramite password hello appena modificata.

## <a name="related-content"></a>Contenuti correlati
* [Come tooupdate la propria password](../active-directory/active-directory-passwords-update-your-own-password.md)
* [Introduzione alla gestione delle password in Azure AD](../active-directory/active-directory-passwords-getting-started.md)
* [Abilitare la sincronizzazione delle password del tenant tooAzure dominio servizi di Active Directory per una sincronizzazione Azure AD](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [Amministrare un dominio gestito di Azure Active Directory Domain Services](active-directory-ds-admin-guide-administer-domain.md)
* [Aggiunta a un dominio di Azure Active Directory Domain Services gestiti tooan Windows macchina virtuale](active-directory-ds-admin-guide-join-windows-vm.md)
* [Aggiunta a un dominio di Azure Active Directory Domain Services gestiti tooan Red Hat Enterprise Linux macchina virtuale](active-directory-ds-admin-guide-join-rhel-linux-vm.md)

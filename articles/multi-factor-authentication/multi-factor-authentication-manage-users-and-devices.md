---
title: "aaaAdmins gestire utenti e dispositivi - autenticazione a più fattori di Azure | Documenti Microsoft"
description: Descrive come le impostazioni utente toochange, ad esempio forzare hello utenti toodo hello processo prova nuovamente.
documentationcenter: 
services: multi-factor-authentication
author: kgremban
manager: femila
ms.assetid: aac3b922-7cc1-428c-9044-273579aa7b5a
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8c35435e4f6504014d9a4f6f1b837639c3b53481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-user-settings-with-azure-multi-factor-authentication-in-hello-cloud"></a>Gestire le impostazioni utente con Azure multi-Factor Authentication nel cloud hello
Come amministratore, è possibile gestire hello seguendo le impostazioni utente e dispositivo:

* Richiedere nuovamente i metodi di contatto tooprovide utenti
* Eliminare password per le app
* Richiedere l'autenticazione a più fattori su tutti i dispositivi attendibili 

## <a name="require-users-tooprovide-contact-methods-again"></a>Richiedere nuovamente i metodi di contatto tooprovide utenti
Questa impostazione forza nuovo processo di registrazione hello toocomplete hello utente. App non basate su browser continuano toowork se hello utente dispone di password di app per loro.  È possibile eliminare le password di app agli utenti di hello selezionando anche **eliminare tutte le password di app generate dagli utenti selezionato hello**.

### <a name="how-toorequire-users-tooprovide-contact-methods-again"></a>Come toorequire utenti tooprovide metodi di contatto nuovamente
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. A sinistra di hello, selezionare **Azure Active Directory** > **utenti e gruppi** > **tutti gli utenti**.
3. Selezionare **Multi-Factor Authentication**. verrà visualizzata la pagina di multi-factor authentication di Hello. 
4. Controllare hello casella Avanti toohello o più utenti che si desidera toomanage. In hello destro è visualizzato un elenco di opzioni del passaggio rapido. 
5. Selezionare **Gestisci le impostazioni dell'utente**.
6. Casella hello per **richiedere agli utenti selezionati tooprovide metodi di contatto nuovamente**.
   ![Fornire metodi di contatto](./media/multi-factor-authentication-manage-users-and-devices/reproofup.png)
7. Fare clic su **save**.
8. Fare clic su **chiudi**.

## <a name="delete-users-existing-app-passwords"></a>Eliminare le password per le app esistenti degli utenti
Questa impostazione Elimina tutte le password di app hello che un utente ha creato. Le app non basate su browser associate a tali password dell'app non funzioneranno più fino a quando non verrà creata una nuova password dell'app.

### <a name="how-toodelete-users-existing-app-passwords"></a>Come gli utenti toodelete le password dell'app esistente
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. A sinistra di hello, selezionare **Azure Active Directory** > **utenti e gruppi** > **tutti gli utenti**.
3. Selezionare **Multi-Factor Authentication**. verrà visualizzata la pagina di multi-factor authentication di Hello. 
6. Controllare hello casella Avanti toohello o più utenti che si desidera toomanage. In hello destro è visualizzato un elenco di opzioni del passaggio rapido. 
7. Selezionare **Gestisci le impostazioni dell'utente**.
8. Casella hello per **eliminare tutte le password di app generate dagli utenti selezionato hello**.
   ![Eliminare password per le app](./media/multi-factor-authentication-manage-users-and-devices/deleteapppasswords.png)
9. Fare clic su **save**.
10. Fare clic su **chiudi**.

## <a name="restore-mfa-on-all-remembered-devices-for-a-user"></a>Ripristinare MFA in tutti i dispositivi memorizzati per un utente
Una delle funzionalità configurabile di hello di Azure multi-Factor Authentication concede agli utenti i dispositivi di hello opzione toomark come attendibile. Per altre informazioni, vedere [Configurare le impostazioni di Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md#remember-multi-factor-authentication-for-devices-that-users-trust).

Gli utenti possono rifiutare esplicitamente la verifica in due passaggi per un numero configurabile di giorni per i propri dispositivi regolari. Se viene compromesso un account o un dispositivo attendibile viene perso, è necessario toobe tooremove in grado di hello attendibile stato e richiedere di nuovo la verifica in due passaggi.

Hello **ripristino multi-factor authentication per tutti i dispositivi memorizzati** impostazione indica che l'utente hello sarà hello di verifica in due passaggi tooperform citata successivo accesso, indipendentemente dal fatto che sono stati scelti toomark loro dispositivo come attendibile. 

### <a name="how-toorestore-mfa-on-all-suspended-devices-for-a-user"></a>Come toorestore autenticazione a più fattori in tutti i dispositivi sospesi per un utente
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. A sinistra di hello, selezionare **Azure Active Directory** > **utenti e gruppi** > **tutti gli utenti**.
3. Selezionare **Multi-Factor Authentication**. verrà visualizzata la pagina di multi-factor authentication di Hello. 
6. Controllare hello casella Avanti toohello o più utenti che si desidera toomanage. In hello destro è visualizzato un elenco di opzioni del passaggio rapido. 
7. Selezionare **Gestisci le impostazioni dell'utente**.
8. Casella hello per **ripristino multi-factor authentication per tutti i dispositivi memorizzati**
   ![eliminare le password dell'app](./media/multi-factor-authentication-manage-users-and-devices/rememberdevices.png)
9. Fare clic su **save**.
10. Fare clic su **chiudi**.

## <a name="next-steps"></a>Passaggi successivi

- Ottenere altre informazioni su come troppo[impostazioni configurare Azure multi-Factor Authentication](multi-factor-authentication-whats-next.md)

- Se gli utenti per assistenza, facciano riferimento verso hello [manuale dell'utente per la verifica in due passaggi](./end-user/multi-factor-authentication-end-user.md)

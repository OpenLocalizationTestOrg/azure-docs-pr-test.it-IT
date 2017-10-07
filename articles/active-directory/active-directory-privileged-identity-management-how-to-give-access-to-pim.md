---
title: aaaHow toogive accesso tooPrivileged Identity Management - Azure | Documenti Microsoft
description: Informazioni su come tooadd ruoli toousers con hello estensione di Azure Active Directory Privileged Identity Management in modo che possano gestire PIM.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 5d99589af4af766e430d7cecd743ace752f63768
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a>Dando accesso toomanage Azure AD Privileged Identity Management
amministratore globale di Hello che abilita automaticamente Azure AD Privileged Identity Management (PIM) per un'organizzazione di ottenere le assegnazioni di ruolo e accedere tooPIM. Per impostazione predefinita, nessun altro utente ottiene l'accesso in scrittura, inclusi gli altri amministratori globali. Dispongono di accesso in sola lettura tooAzure PIM AD altri amministratori globali, amministratori della sicurezza e i lettori di sicurezza. toogive tooPIM di accesso, utente prima di hello può assegnare ad altri utenti toohello **amministratore del ruolo con privilegi** ruolo. Questa assegnazione deve essere eseguita dall'interno PIM e non può essere modificata tramite PowerShell o altri portali.

> [!NOTE]
> Per la gestione di Azure AD PIM è necessario Azure Multi-Factor Authentication. Poiché gli account Microsoft non possono effettuare la registrazione per Azure MFA, gli utenti che eseguono l'accesso con un account Microsoft non possono accedere a Azure AD PIM.
> 
> 

Assicurarsi che almeno due utenti abbiano sempre il ruolo di amministratore dei ruoli con privilegi, per l'eventualità in cui uno di questi venga bloccato o il suo account venga eliminato.

## <a name="give-another-user-access-toomanage-pim"></a>Assegnare un altro utente accesso toomanage PIM
1. Accedi toohello [portale di Azure](https://portal.azure.com/) e seleziona hello **Azure AD Privileged Identity Management** app dashboard hello.
2. Selezionare **Gestione dei ruoli con privilegi** > **Amministratore dei ruoli con privilegi** > **Aggiungi**.
   
    ![Schermata Aggiungi amministratori dei ruoli con privilegi][1]
3. Nel Pannello di utenti gestiti Aggiungi hello, passaggio 1 è già stato completato. Il passaggio 2, seleziona **selezionare utenti** e la ricerca per utente hello desiderato tooadd.
   
    ![Schermata Seleziona gli utenti][2]
4. Selezionare l'utente hello dai risultati della ricerca hello e fare clic su **eseguita**.
5. Fare clic su **OK** toosave la selezione. Hello l'utente selezionato verrà visualizzata nell'elenco di hello degli amministratori con privilegi di ruolo.
   
   * Ogni volta che si assegna un nuovo toosomeone ruolo, vengono automaticamente configurati come ruolo hello tooactivate idoneo. Se si desidera toomake permanenti nel ruolo di hello, fare clic su utente hello nell'elenco di hello. Selezionare **rendere autorizzazioni** nel menu di informazioni utente hello.
6. Invia hello un collegamento all'utente troppo[Introduzione a Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).

## <a name="remove-another-users-access-rights-for-managing-pim"></a>Rimuovere i diritti di accesso di un altro utente per la gestione di PIM
Prima di rimuovere un utente dal ruolo di amministratore con privilegi di ruolo hello, assicurarsi sempre che sarà ancora presente due utenti assegnati tooit.

1. Nel dashboard PIM hello, fare clic sul ruolo hello **amministratore del ruolo con privilegi**.  verrà visualizzato l'elenco di Hello di utenti attualmente in tale ruolo.
2. Fare clic sull'utente hello nell'elenco di utenti hello.
3. Fare clic su **Rimuovi**.  Verrà visualizzato un messaggio di richiesta di conferma.
4. Fare clic su **Sì** utente hello tooremove dal ruolo hello.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png

---
title: "aaaAzure Active Directory a più livelli di protezione delle password | Documenti Microsoft"
description: Questo articolo spiega in che modo Azure AD applica le password complesse e protegge le password degli utenti dai criminali informatici.
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a>Protezione delle password tooAzure AD un approccio a più livelli

In questo articolo vengono illustrate alcune procedure consigliate è possibile seguire come un utente o un amministratore tooprotect l'Account di Microsoft o di Azure Active Directory (Azure AD).

 > [!NOTE]
 > Gli amministratori di Azure AD possono reimpostare le password utente utilizzando istruzioni hello nell'articolo hello [hello di reimpostazione password per un utente in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).
 >
 > Gli utenti possono reimpostare le proprie password tramite istruzioni hello nell'articolo hello [Guida ho dimenticato la password di Azure AD](active-directory-passwords-update-your-own-password.md).
 >

## <a name="password-requirements"></a>Requisiti delle password

Azure AD incorpora hello password toosecuring di approcci comuni seguenti:

* Requisiti di lunghezza delle password
* Requisiti di complessità delle password
* Scadenza regolare e periodica delle password

Per informazioni su reimpostare la password in Azure Active Directory, vedere l'argomento hello [AD Azure self-service la reimpostazione della password per i professionisti IT hello](active-directory-passwords.md).

## <a name="azure-ad-password-protections"></a>Protezione delle password di Azure AD

Azure AD e sistema di Account Microsoft utilizzare settore rivelato hello si avvicina tooensure protezione sicura della password utente e amministratore, che includono:

* Password vietate in modo dinamico
* Smart Password Lockout

Per informazioni sulla gestione delle password in base alle ricerche corrente, vedere il white paper hello [indicazioni Password](http://aka.ms/passwordguidance).

### <a name="dynamically-banned-passwords"></a>Password vietate in modo dinamico

Azure AD e il sistema di account Microsoft salvaguardano la protezione delle password vietando in modo dinamico le password usate comunemente. il team di protezione dell'identità di Azure ID Hello analizza regolarmente gli elenchi di password escluso, impedendo agli utenti di selezione di password usate comunemente. Questo servizio è disponibile tooAzure AD e clienti del servizio di Account Microsoft hello.

Durante la creazione di password, è importante per gli amministratori tooencourage utenti toochoose password frasi che includono una combinazione univoca di lettere, numeri, caratteri o parole. Questo approccio consente le password utente toomake toobe praticamente compromesso ma più semplice per gli utenti tooremember.

#### <a name="password-breaches"></a>Violazioni delle password

Microsoft sta sempre toostay un unico passaggio precedono criminali informatici.

il team di Azure AD Identity Protection Hello analizza continuamente le password utilizzati di frequente. Criminali informatici inoltre utilizzano simile strategie tooinform gli attacchi, ad esempio creazione un' [tabella arcobaleno](https://en.wikipedia.org/wiki/Rainbow_table) per violare gli hash delle password.

Microsoft analizza continuamente [violazioni dati](https://www.privacyrights.org/data-breaches) toomaintain un elenco aggiornato in modo dinamico la password da escludere, che assicura che le password vulnerabili vengono escluse prima che diventino un reale minaccia clienti tooAzure Active Directory. Per ulteriori informazioni sull'impegno di sicurezza corrente, vedere hello [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).

### <a name="smart-password-lockout"></a>Smart Password Lockout

Quando Azure Active Directory rileva una potenziale toohack durante il tentativo di informatica penali in una password utente, si blocca account utente di hello con blocco Password Smart. Azure AD viene progettato il rischio di hello toodetermine associato alle sessioni di accesso specifico. Quindi l'uso di dati di sicurezza più aggiornati hello, si applicano minacce cyber toostop semantica di blocco.

Se un utente è bloccato da Azure AD, la schermata appare simile toohello uno che segue:

  ![Bloccato da Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

Per gli altri account Microsoft, la schermata appare simile toohello uno che segue:

  ![Bloccato da un account Microsoft](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

Per informazioni su reimpostare la password in Azure Active Directory, vedere l'argomento hello [AD Azure self-service la reimpostazione della password per i professionisti IT hello](active-directory-passwords.md).

  >[!NOTE]
  >Se si è un amministratore di Azure AD, è opportuno toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid con gli utenti di creare password tradizionali completamente.
  >

## <a name="next-steps"></a>Passaggi successivi

* [Come tooupdate la propria password](active-directory-passwords-update-your-own-password.md)
* [Nozioni fondamentali su Hello della gestione delle identità di Azure](fundamentals-identity.md)
* [Rapporto sull'attività di reimpostazione password](active-directory-passwords-reporting.md)



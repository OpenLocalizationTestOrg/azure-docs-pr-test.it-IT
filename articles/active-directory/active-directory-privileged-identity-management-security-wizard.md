---
title: procedura guidata di protezione di aaaThe Azure AD Privileged Identity Management
description: "Hello prima volta che si utilizza l'estensione di Azure Active Directory Privileged Identity Management hello, verrà visualizzata una procedura guidata di protezione. Questo articolo descrive i passaggi di hello per utilizzare la procedura guidata hello."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: a53a3719-8cc7-4fc7-8164-aafca192871b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 0b3019134d3c7cfac33b3acfcf430b4d4f67b119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-security-wizard-in-azure-ad-privileged-identity-management"></a>Utilizzando la procedura guidata protezione hello in Azure AD Privileged Identity Management 
Se si hello prima persona toorun Azure Privileged Identity Management (PIM) per l'organizzazione, verrà visualizzata una procedura guidata. procedura guidata Hello consente di comprendere i rischi di sicurezza hello delle identità con privilegi e come toouse PIM tooreduce tali rischi. Non è necessario toomake le assegnazioni di ruolo tooexisting eventuali modifiche nella procedura guidata hello, se si preferisce toodo posticipato.

## <a name="what-tooexpect"></a>Quali tooexpect
Prima che l'organizzazione inizia a usare PIM, tutte le assegnazioni di ruolo sono permanenti: gli utenti di hello sono sempre a questi ruoli, anche se non è necessario attualmente i propri privilegi.  innanzitutto Hello della procedura guidata hello Mostra un elenco di ruoli con privilegi elevati e il numero di utenti è attualmente in tali ruoli. È possibile analizzare in tooa particolare ruolo toolearn ulteriori informazioni su utenti, se uno o più di esse si ha dimestichezza.

secondo passaggio di Hello della procedura guidata hello offre le assegnazioni di ruolo dell'amministratore toochange opportunità.  

> [!WARNING]
> È importante che siano presenti almeno un amministratore globale e più amministratori dei ruoli con privilegi con account aziendali e non account Microsoft. Se è presente solo un amministratore del ruolo con privilegi, organizzazione hello non sarà in grado di toomanage PIM se tale account viene eliminato.
> Tenere inoltre le assegnazioni di ruolo permanente se un utente dispone di un account Microsoft (account utilizzano toosign in servizi tooMicrosoft Skype e Outlook.com). Se si prevede di toorequire autenticazione a più fattori per l'attivazione per tale ruolo, tale utente verrà bloccato.
> 
> 

Dopo avere apportato modifiche, la procedura guidata hello non mostrerà più. Hello successivo utilizzo di un ruolo con privilegi amministratore PIM, verrà visualizzato il dashboard PIM hello.  

* Se si sarebbe ad esempio tooadd o rimuovere utenti dai ruoli o modificare le assegnazioni da tooeligible permanente, leggere informazioni, vedere [come tooadd o rimuovere un ruolo utente](active-directory-privileged-identity-management-how-to-add-role-to-user.md).
* Se si desidera toogive toomanage PIM, accedano a più utenti di leggere informazioni, vedere [modalità di accesso toomanage in PIM toogive](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]


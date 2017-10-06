---
title: aaaDelegate inviti per la collaborazione B2B di Azure Active Directory | Documenti Microsoft
description: "Le proprietà di un utente di Collaborazione B2B di Azure Active Directory sono configurabili"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a>Delegare gli inviti per Collaborazione B2B di Azure Active Directory

Con la collaborazione business-to-business (B2B) di Azure Active Directory (Azure AD), non si dispone toobe gli inviti toosend un amministratore globale. Al contrario, è possibile usare i criteri e delegare toousers inviti con ruoli consentono inviti toosend. Un importante nuovo modo toodelegate guest utente inviti è tramite il ruolo di mittente dell'invito Guest hello.

## <a name="guest-inviter-role"></a>Ruolo Mittente dell'invito guest
È possibile assegnare hello utente tooGuest inviti toosend ruolo di mittente dell'invito. Non è membro toobe inviti toosend ruolo amministratore globale di hello. Per impostazione predefinita, gli utenti standard possono anche richiamare hello invito API a meno che un amministratore globale disabilitata inviti per gli utenti standard. Un utente può anche richiamare API hello con hello portale di Azure o PowerShell.

Di seguito è riportato un esempio che illustra come toouse PowerShell tooadd un ruolo di mittente dell'invito Guest toohello utente:

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a>Controllare i mittenti degli inviti

![Controllo modalità tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

Con la collaborazione B2B di Azure AD, un amministratore tenant possibile impostare hello base invito ai criteri:

- Disattivare gli inviti
- Solo gli amministratori e gli utenti nel ruolo di mittente dell'invito Guest hello è possono invitare
- Membri, il ruolo di mittente dell'invito Guest hello e amministratori possono invitare
- Possono inviare inviti tutti gli utenti, inclusi gli utenti guest

Per impostazione predefinita, i tenant sono troppo n. 4. Tutti gli utenti, inclusi gli utenti guest, possono inviare inviti a utenti B2B.

## <a name="next-steps"></a>Passaggi successivi

Vedere gli altri articoli su Azure AD B2B Collaboration.

* [Che cos'è Azure AD B2B Collaboration?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Proprietà dell'utente di Collaborazione B2B](active-directory-b2b-user-properties.md)
* [Aggiunta di un ruolo di tooa utente collaborazione B2B](active-directory-b2b-add-guest-to-role.md)
* [Gruppi dinamici e Collaborazione B2B](active-directory-b2b-dynamic-groups.md)
* [Codici ed esempi di PowerShell per Collaborazione B2B](active-directory-b2b-code-samples.md)
* [Configurare app SaaS per Collaborazione B2B](active-directory-b2b-configure-saas-apps.md)
* [Token utente in Collaborazione B2B](active-directory-b2b-user-token.md)
* [Mapping delle attestazioni utente per Collaborazione B2B](active-directory-b2b-claims-mapping.md)
* [Condivisione esterna di Office 365](active-directory-b2b-o365-external-user.md)
* [Limitazioni correnti di Collaborazione B2B](active-directory-b2b-current-limitations.md)

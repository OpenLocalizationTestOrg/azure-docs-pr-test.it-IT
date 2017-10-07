---
title: aaaDynamic gruppi e collaborazione B2B di Azure Active Directory | Documenti Microsoft
description: "Collaborazione B2B di Azure Active Directory può essere usato con i gruppi dinamici di Azure AD"
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
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a>Gruppi dinamici e Collaborazione B2B di Azure Active Directory

## <a name="what-are-dynamic-groups"></a>Che cosa sono i gruppi dinamici
Configurazione dinamica dell'appartenenza al gruppo di sicurezza per Azure Active Directory (Azure AD) è disponibile in [hello Azure portal](https://portal.azure.com). Gli amministratori possono impostare regole toopopulate gruppi creati in Azure Active Directory in base agli attributi utente (ad esempio userType, reparto o paese). I membri possono essere aggiunti automaticamente tooor rimossi da un gruppo di sicurezza in base ai relativi attributi. Questi gruppi è possono accedere alle risorse tooapplications o cloud (siti di SharePoint, documenti) e tooassign toomembers le licenze. Per altre informazioni sui gruppi dinamici, vedere [Gruppi dedicati in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).

Hello appropriato [licenze di Azure AD Premium P1 or P2](https://azure.microsoft.com/pricing/details/active-directory/) è gruppi dinamici toocreate e l'utilizzo richiesti. Altre informazioni nell'articolo hello [creare regole basate su attributi per l'appartenenza dinamica ai gruppi in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).

## <a name="what-are-hello-built-in-dynamic-groups"></a>Quali sono gruppi dinamici incorporato hello?
Hello **tutti gli utenti** gruppo dinamico consente toocreate amministratori tenant fare clic su un gruppo contenente tutti gli utenti nel tenant di hello con un singolo. Per impostazione predefinita, hello **tutti gli utenti** gruppo include tutti gli utenti nella directory di hello, inclusi i membri e Guest.
All'interno di hello nuovo Azure Active Directory portale di amministrazione, è possibile scegliere hello tooenable **tutti gli utenti** gruppo hello consente di visualizzare le impostazioni di gruppo.

![Gruppi predefiniti](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a>Protezione avanzata hello gruppo dinamico di tutti gli utenti
Per impostazione predefinita, hello **tutti gli utenti** gruppo contiene anche gli utenti di collaborazione (guest) B2B. È possibile proteggere ulteriormente i **tutti gli utenti** gruppo tramite una regola di tooremove utenti guest. Hello illustrazione che segue hello **tutti gli utenti** modifica del gruppo guests tooexclude.

![Abilitare il gruppo Tutti gli utenti](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

Può inoltre risultare utile toocreate un nuovo gruppo dinamico che contiene solo gli utenti guest, in modo che sia possibile applicare toothem criteri (ad esempio criteri di accesso condizionale di Azure AD).
Un gruppo può avere questo aspetto:

![Escludere gli utenti guest](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a>Passaggi successivi

Vedere gli altri articoli su Azure AD B2B Collaboration.

* [Che cos'è Azure AD B2B Collaboration?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Proprietà dell'utente di Collaborazione B2B](active-directory-b2b-user-properties.md)
* [Aggiunta di un ruolo di tooa utente collaborazione B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegare gli inviti a Collaborazione B2B](active-directory-b2b-delegate-invitations.md)
* [Codici ed esempi di PowerShell per Collaborazione B2B](active-directory-b2b-code-samples.md)
* [Configurare app SaaS per Collaborazione B2B](active-directory-b2b-configure-saas-apps.md)
* [Token utente in Collaborazione B2B](active-directory-b2b-user-token.md)
* [Mapping delle attestazioni utente per Collaborazione B2B](active-directory-b2b-claims-mapping.md)
* [Condivisione esterna di Office 365](active-directory-b2b-o365-external-user.md)
* [Limitazioni correnti di Collaborazione B2B](active-directory-b2b-current-limitations.md)

---
title: mapping in Azure Active Directory di attestazioni utente collaborazione aaaB2B | Documenti Microsoft
description: Informazioni sul mapping delle attestazioni per Collaborazione B2B in Azure Active Directory
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 9e26085e91a6004b2f11286ae9c1df133bd47341
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a>Mapping delle attestazioni utente per Collaborazione B2B in Azure Active Directory

Azure Active Directory (Azure AD) supporta la personalizzazione di attestazioni di hello rilasciate nel token SAML hello per gli utenti di collaborazione B2B. Quando un utente esegue l'autenticazione dell'applicazione toohello, Azure AD rilascia una app toohello token SAML che contiene informazioni (o attestazioni) sull'utente hello che li identifica in modo univoco. Per impostazione predefinita, sono inclusi il nome utente dell'utente hello, indirizzo di posta elettronica, nome e cognome. È possibile visualizzare o modificare attestazioni hello inviate in hello applicazione toohello token SAML nella scheda attributi hello.

Esistono due possibili motivi per cui potrebbe essere necessario attestazioni di hello tooedit rilasciate nel token SAML hello.

1. è stato scritto toorequire un diverso set di URI di attestazione o i valori di attestazione a un'applicazione Hello

2. L'applicazione richiede toobe di attestazione NameIdentifier hello diverso dal nome dell'entità utente hello archiviati in Azure Active Directory.

  ![Visualizzare le attestazioni nel token SAML](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

Per informazioni su come tooadd e modifica attestazioni, vedere l'articolo specificato di personalizzazione di attestazioni, [personalizzazione di attestazioni rilasciate nel token SAML hello per le app preintegrate in Azure Active Directory](develop/active-directory-saml-claims-customization.md). Per gli utenti di Collaborazione B2B, il mapping tra NameID e UPN tra tenant non è consentito per motivi di sicurezza.


## <a name="next-steps"></a>Passaggi successivi

Vedere gli altri articoli su Azure AD B2B Collaboration.

* [Che cos'è Azure AD B2B Collaboration?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Proprietà dell'utente di Collaborazione B2B](active-directory-b2b-user-properties.md)
* [Aggiunta di un ruolo di tooa utente collaborazione B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegare gli inviti a Collaborazione B2B](active-directory-b2b-delegate-invitations.md)
* [Gruppi dinamici e Collaborazione B2B](active-directory-b2b-dynamic-groups.md)
* [Codici ed esempi di PowerShell per Collaborazione B2B](active-directory-b2b-code-samples.md)
* [Configurare app SaaS per Collaborazione B2B](active-directory-b2b-configure-saas-apps.md)
* [Condivisione esterna di Office 365](active-directory-b2b-o365-external-user.md)
* [Token utente per Collaborazione B2B](active-directory-b2b-user-token.md)
* [Limitazioni correnti di Collaborazione B2B](active-directory-b2b-current-limitations.md)

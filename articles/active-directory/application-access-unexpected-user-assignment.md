---
title: aaaHow tooAssign utenti tooapplications | Documenti Microsoft
description: Comprendere come gli utenti vengano assegnati tooan applicazione nel tenant
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a>Come tooassign utenti tooapplications

Questo articolo è utile toounderstand come gli utenti vengano assegnati tooan applicazione nel tenant.

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a>Come gli utenti vengano assegnati tooan applicazione in Azure AD?

Per un utente tooaccess un'applicazione, è necessario innanzitutto assegnare tooit in qualche modo. Assegnazione può essere eseguita da un amministratore, un delegato di business o in alcuni casi, utente hello autonomamente. Di seguito descrive gli utenti possono ottenere assegnati tooapplications modi di hello:

1.  Un amministratore [assegna un utente](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello applicazione direttamente

2.  Un amministratore [assegna un gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) utente hello è un membro dell'applicazione toohello, tra cui:

  * Un gruppo che è stato sincronizzato da locale

  * Un gruppo di sicurezza statico creato in un cloud hello

  * Oggetto [gruppo di sicurezza dinamica](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) create in un cloud hello

  * Un gruppo di Office 365 creato nel cloud hello

  * Hello [tutti gli utenti](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) gruppo

3.  Un amministratore abilita [accesso all'applicazione Self-Service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow tooadd un utente un'applicazione utilizzando hello [Pannello di accesso dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Aggiungi App** funzionalità **senza l'approvazione di business**

4.  Un amministratore abilita [accesso all'applicazione Self-Service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow tooadd un utente un'applicazione utilizzando hello [Pannello di accesso dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Aggiungi App** funzionalità, ma solo w **i-esimo preventiva approvazione da un set selezionato di responsabili approvazione di business**

5.  Un amministratore abilita [gestione dei gruppi Self-Service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow toojoin un utente un gruppo che un'applicazione è troppo**senza l'approvazione di business**

6.  Un amministratore abilita [gestione dei gruppi Self-Service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow toojoin un utente un gruppo che un'applicazione viene assegnata a, ma solo **previa autorizzazione da un set selezionato di responsabili approvazione di business**

7.  Un amministratore assegna un utente tooa licenza direttamente per la prima applicazione di terze parti, ad esempio [Microsoft Office 365](http://products.office.com/)

8.  Un amministratore assegna a un gruppo di licenze tooa che hello utente è membro tooa prima applicazione di terze parti, ad esempio [Microsoft Office 365](http://products.office.com/)

9.  Un [amministratore acconsente applicazione tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe utilizzato da tutti gli utenti e quindi un utente accede toohello applicazione

10. Un utente [acconsente applicazione tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) stesse effettuando l'accesso dell'applicazione toohello

## <a name="next-steps"></a>Passaggi successivi
[Gestione di applicazioni con Azure Active Directory](active-directory-enable-sso-scenario.md)

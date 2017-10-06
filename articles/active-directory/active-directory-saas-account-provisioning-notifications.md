---
title: le notifiche di provisioning aaaAccount | Documenti Microsoft
description: Informazioni su come tooensure la notifica dei problemi correlati toouser provisioning che richiedono attenzione abilitando le notifiche di provisioning dell'account.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a637aac7-f06b-48ef-a66d-639835a8edec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: e33d1dd806fff43fc96f843a9dcddd7375d2e3c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="account-provisioning-notifications"></a>Notifiche relative al provisioning dell'account
Con il provisioning utente, è possibile automatizzare il processo di hello di gestione degli utenti nelle applicazioni SaaS di terze parti. <br>
Si tratta di un processo automatizzato, l'interazione con questo processo è da tootime tempo richiesto. <br>
Questo accade, ad esempio hello, quando password hello dell'account hello configurato tooexchange dati con un terzo di terze parti SaaS applicazione è scaduta. 

Abilitando le notifiche di provisioning dell'account, è possibile garantire la notifica di problemi correlati toouser provisioning che richiedono attenzione.

È possibile attivare o disattivare le notifiche di provisioning dell'account come parte della configurazione del provisioning utenti per un'applicazione SaaS di terze parti.

![Provisioning utente][1] 

le notifiche di provisioning dell'account tooactivate, selezionare hello casella di controllo correlato hello **conferma** nella pagina e alias del tipo di messaggio di posta elettronica hello del destinatario hello.

![Notifiche relative al provisioning dell'account][2]

È possibile immettere una lista di distribuzione come destinatario. Tuttavia, è importante toonote che posta elettronica di notifica hello contiene collegamenti tooreports che accessibili solo dagli amministratori di hello Azure AD.

Se sono abilitate le notifiche di provisioning dell'account si riceveranno e-mail riguardo problemi critici che sono correlati toouser provisioning. Tuttavia, tooavoid un sovraccarico di posta elettronica, è solo riceverà una notifica tramite posta elettronica al giorno per ogni SaaS applicazione hello notifica tramite posta elettronica è abilitata per.

## <a name="related-articles"></a>Articoli correlati
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Automatizzare tooSaaS utente Provisioning o Deprovisioning App](active-directory-saas-app-provisioning.md)
* [Personalizzazione dei mapping degli attributi per il Provisioning dell’utente](active-directory-saas-customizing-attribute-mappings.md)
* [Scrittura di espressioni per i mapping degli attributi](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Ambito dei filtri per il Provisioning utente](active-directory-saas-scoping-filters.md)
* [Utilizzando SCIM tooenable il provisioning automatico degli utenti e gruppi da Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Elenco di esercitazioni sulla tooIntegrate App SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-account-provisioning-notifications/ic766307.png
[2]: ./media/active-directory-saas-account-provisioning-notifications/ic766308.png

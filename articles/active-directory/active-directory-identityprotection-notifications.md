---
title: Notifiche di Azure Active Directory Identity Protection| Documentazione Microsoft
description: "Informazioni su come le notifiche agevolano le attività di analisi."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestione applicazioni, sicurezza, rischio, livello di rischio, vulnerabilità, criteri di sicurezza"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 079d16bbf75cd2b3b94269d684e1ae1a0e6aa967
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a>Notifiche di Azure Active Directory Identity Protection
Azure AD Identity Protection invia due tipi di messaggi di posta elettronica di notifica automatica per la gestione del rischio utente e degli eventi di rischio:

* Messaggio di posta elettronica di avviso utente compromesso
* Messaggio di posta elettronica di riepilogo settimanale

## <a name="user-compromised-alert-email"></a>Messaggio di posta elettronica di avviso utente compromesso
Quando Azure AD Identity Protection identifica un account come compromesso, viene generato un avviso di posta elettronica utente compromesso. Il messaggio include un collegamento al report relativo agli utenti contrassegnati per il rischio nel dashboard di Identity Protection. È consigliabile analizzare immediatamente le notifiche relative agli account compromessi.

## <a name="weekly-digest-email"></a>Messaggio di posta elettronica di riepilogo settimanale
Il messaggio di riepilogo settimanale contiene un riepilogo dei nuovi eventi di rischio.<br>
Sono inclusi:

* Utenti a rischio.
* Attività sospette
* Vulnerabilità rilevate.
* Collegamenti ai report correlati in Identity Protection.

<br>
![Monitoraggio e aggiornamento](./media/active-directory-identityprotection-notifications/400.png "monitoraggio e aggiornamento")
<br>

È possibile disattivare l’invio del messaggio di posta elettronica settimanale contenente il riepilogo.
<br><br>
![Rischi per gli utenti](./media/active-directory-identityprotection-notifications/62.png "rischi per gli utenti")
<br>

**Per aprire la relativa finestra di dialogo di configurazione**:

1. Nel pannello **Azure AD Identity Protection** fare clic su **Impostazioni**.
   <br><br>
   ![I criteri di rischio utente](./media/active-directory-identityprotection-notifications/401.png "rischio utente")
   <br>
2. Nella sezione **Generale** fare clic su **Notifiche**.
   <br><br>
   ![I criteri di rischio utente](./media/active-directory-identityprotection-notifications/405.png "rischio utente")
   <br>

## <a name="see-also"></a>Vedere anche
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

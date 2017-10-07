---
title: le notifiche di Active Directory Identity Protection aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: 19e62374873f034591c658a779f97d935766c612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a>Notifiche di Azure Active Directory Identity Protection
Azure AD Identity Protection invia due tipi di notifica automatica tramite posta elettronica toohelp per gestire il rischio di utente e gli eventi di rischio:

* Messaggio di posta elettronica di avviso utente compromesso
* Messaggio di posta elettronica di riepilogo settimanale

## <a name="user-compromised-alert-email"></a>Messaggio di posta elettronica di avviso utente compromesso
Quando Azure AD Identity Protection identifica un account come compromesso, viene generato un avviso di posta elettronica utente compromesso. posta elettronica Hello include un collegamento di toohello che utenti contrassegnati per report rischi nel dashboard di hello Identity Protection. È consigliabile analizzare immediatamente le notifiche relative agli account compromessi.

## <a name="weekly-digest-email"></a>Messaggio di posta elettronica di riepilogo settimanale
Hello settimanale digest messaggio di posta elettronica contenente un riepilogo di nuovi eventi di rischio.<br>
Sono inclusi:

* Utenti a rischio.
* Attività sospette
* Vulnerabilità rilevate.
* Toohello collegamenti correlati di report nella protezione di identità

<br>
![Monitoraggio e aggiornamento](./media/active-directory-identityprotection-notifications/400.png "monitoraggio e aggiornamento")
<br>

È possibile disattivare l’invio del messaggio di posta elettronica settimanale contenente il riepilogo.
<br><br>
![Rischi per gli utenti](./media/active-directory-identityprotection-notifications/62.png "rischi per gli utenti")
<br>

**finestra di dialogo di configurazione correlato hello tooopen**:

1. In hello **Azure AD Identity Protection** pannello, fare clic su **impostazioni**.
   <br><br>
   ![I criteri di rischio utente](./media/active-directory-identityprotection-notifications/401.png "rischio utente")
   <br>
2. In hello **generale** fare clic su **notifiche**.
   <br><br>
   ![I criteri di rischio utente](./media/active-directory-identityprotection-notifications/405.png "rischio utente")
   <br>

## <a name="see-also"></a>Vedere anche
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

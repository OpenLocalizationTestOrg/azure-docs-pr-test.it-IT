---
title: aaaAzure notifiche dei report di Active Directory
description: Come toouse hello notifiche reporting di Azure Active Directory per l'accesso sospetti aggiuntivi.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.custom: oldportal
ms.reviewer: dhanyahk
ms.openlocfilehash: 3843c45eaf9d68e671943bfdbc7ab68933f38fbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-notifications"></a>Notifiche di Report di Azure Active Directory
## <a name="what-reports-generate-email-notifications"></a>Quali report generano notifiche tramite posta elettronica
In questo momento, notifiche tramite posta elettronica solo nei trigger report attività hello di accesso irregolare.

## <a name="what-is-an-irregular-sign-in"></a>Che cos'è un "Accesso irregolare"?
Accessi irregolari sono quelli che sono stati identificati dagli algoritmi, su base hello di una condizione di "Impossibile viaggio" combinata con un percorso di accesso anomalo e dispositivo di apprendimento automatico. Questo può indicare che un pirata informatico abbia tentato toosign utilizzando questo account.

## <a name="who-receives-hello-email-notifications"></a>Chi riceverà le notifiche di posta elettronica hello?
messaggio di posta elettronica Hello viene inviato tooall gli amministratori globali che sono stati assegnati una licenza di Active Directory Premium. tooensure che viene recapitato, inviato anche toohello admins indirizzo di posta elettronica alternativo. Gli amministratori devono includere aad-alerts-noreply@mail.windowsazure.com nel proprio elenco Mittenti attendibili in modo che non perdere il messaggio di posta elettronica hello.

## <a name="how-often-are-these-emails-sent"></a>Con quale frequenza vengono inviati i messaggi di posta elettronica?
messaggio di posta elettronica Hello viene inviato se 10 nuove irregolari Accedi attività si verificano in hello ultimi 30 giorni, oppure perché è stato inviato l'ultimo messaggio di posta hello, qualunque sia inferiore.

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a>La modalità di accesso di report hello indicato nel messaggio di posta elettronica hello?
Quando si fa clic sul collegamento hello, sarà reindirizzato toohello pagina del report all'interno di hello portale di Azure classico. In ordine tooaccess hello report, è necessario toobe entrambi:

* Un amministratore o un coamministratore della sottoscrizione di Azure.
* Un amministratore globale nella directory di hello e assegnata una licenza di Active Directory Premium. Per altre informazioni, vedere [Edizioni di Azure Active Directory](active-directory-editions.md).

## <a name="can-i-turn-off-these-emails"></a>È possibile disattivare questi messaggi di posta elettronica?
Sì, tooturn le notifiche correlate tooanomalous accessi all'interno di hello portale di Azure classico, fare clic su **configura**, quindi selezionare **disabilitato** in hello **notifiche**sezione.

## <a name="whats-next"></a>Passaggi successivi
* Per informazioni sui report di sicurezza, controllo e attività disponibili, Vedere [Report di sicurezza, controllo e attività di Azure AD](active-directory-view-access-usage-reports.md)
* [Introduzione ad Azure Active Directory Premium](active-directory-get-started-premium.md)
* [Aggiungere personalizzazione delle pagine di accesso e il pannello di accesso tooyour della società](active-directory-add-company-branding.md)


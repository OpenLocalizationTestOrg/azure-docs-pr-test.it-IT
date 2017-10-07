---
title: avvisi di sicurezza tooconfigure aaaHow | Documenti Microsoft
description: Informazioni su come avvisi di sicurezza tooconfigure per l'estensione Azure Privileged Identity Management.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4e0c911a-36c6-42a0-8f79-a01c03d2d04f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 1b3c4a7d36fa3f81bb3fe2574d675fdf0ab34909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-security-alerts-in-azure-ad-privileged-identity-management"></a>La modalità di avviso di sicurezza tooconfigure in Azure AD Privileged Identity Management
## <a name="security-alerts"></a>Avvisi di sicurezza
Azure Privileged Identity Management (PIM) genera avvisi nel caso di attività sospette o non sicure nel proprio ambiente. Quando viene attivato un avviso, viene visualizzato nel dashboard PIM hello. Selezionare toosee avviso hello un report che elenchi hello utenti o ruoli che ha attivato hello avviso.

![Schermata Avvisi di sicurezza del dashboard di PIM][1]

| Avviso | Trigger | Raccomandazione |
| --- | --- | --- |
| **I ruoli vengono assegnati all'esterno di PIM** |Un amministratore è stato assegnato in modo permanente il ruolo di tooa, di fuori di interfaccia PIM hello. |Esaminare nuova assegnazione di ruolo hello. Poiché altri servizi è possono assegnare solo gli amministratori permanenti, modificarlo assegnazione idonei tooan se necessario. |
| **I ruoli vengono attivati con una frequenza eccessiva** |Si sono verificati troppi riattivazioni di hello stesso ruolo entro il tempo di hello consentito nelle impostazioni di hello. |Contattare hello utente toosee perché sono attivati ruolo hello così tante volte. Forse limite è troppo corto relativa di tempo hello toocomplete le proprie attività, oppure potrebbe essere in uso consente di generare script tooautomatically attivare un ruolo. |
| **I ruoli non richiedono l'autenticazione MFA per l'attivazione** |Sono presenti ruoli senza autenticazione a più fattori abilitata nelle impostazioni di hello. |È necessaria l'autenticazione MFA per i ruoli di hello privilegiata più elevati, ma consiglia vivamente di abilitare l'autenticazione a più fattori per l'attivazione di tutti i ruoli. |
| **Gli amministratori non usano i ruoli con privilegi** |Sono presenti amministratori idonei che non hanno attivato i ruoli di recente. |Avviare una revisione toodetermine hello agli utenti di accesso non più necessario l'accesso. |
| **Il numero di amministratori globali presenti è eccessivo** |Sono presenti più amministratori globali di quanti consigliati. |Se il numero di amministratori globali è elevato, è probabile che ottengano più autorizzazioni di quelle necessarie. Tooless agli utenti di spostare i ruoli con privilegi oppure rendere alcuni di essi idoneo per il ruolo di hello anziché assegnato in modo permanente. |

## <a name="configure-security-alert-settings"></a>Configurare le impostazioni degli avvisi di sicurezza
È possibile personalizzare alcuni degli avvisi di sicurezza hello in toowork PIM con l'ambiente e gli obiettivi di protezione. Seguire questi pannello delle impostazioni dei passaggi tooreach hello:

1. Accedi toohello [portale di Azure](https://portal.azure.com/) e seleziona hello **Azure AD Privileged Identity Management** riquadro dal dashboard hello.
2. Selezionare **Managed privileged roles (Ruoli con privilegi gestiti)** > **Impostazioni** > **Impostazioni degli avvisi**.
   
    ![Passare le impostazioni degli avvisi toosecurity][2]

### <a name="roles-are-being-activated-too-frequently-alert"></a>Avviso "I ruoli vengono attivati con una frequenza eccessiva"
Questo avviso se un utente attiva i trigger hello stesso ruolo con privilegi più volte in un periodo specifico. È possibile configurare entrambi hello tempo periodo e hello il numero di attivazioni.

* **Intervallo di tempo di attivazione rinnovo**: specificare in giorni, ore, minuti e tempo hello secondo periodo si desidera toouse tootrack sospette rinnovo.
* **Numero di rinnovo attivazione**: specificare il numero di hello di attivazioni, da too100 2, da considerare come richiedere un avviso, all'interno di hello intervallo di tempo scelto. È possibile modificare questa impostazione dal dispositivo di scorrimento hello mobile o digitando un numero nella casella di testo hello.

### <a name="there-are-too-many-global-administrators-alert"></a>Avviso "Il numero di amministratori globali è eccessivo"
Se vengono soddisfatti due criteri diversi ed è possibile configurarli entrambi, PIM attiva l'avviso. In primo luogo, è necessario tooreach una determinata soglia di amministratori globali. Una determinata percentuale del totale di assegnazioni di ruoli deve essere rappresentata da amministratori globali. Se si soddisfa solo una di queste misure, non viene visualizzato alcun avviso hello.  

* **Numero minimo di amministratori globali**: specificare il numero di hello degli amministratori globali, da 2 too100, prendere in considerazione una quantità non sicura.
* **Percentuale di amministratori globali**: specificare la percentuale hello di gli amministratori globali, tra 0% too100%, che è sicuro nell'ambiente in uso.

### <a name="administrators-arent-using-their-privileged-roles-alert"></a>Avviso "Gli amministratori non usano i ruoli con privilegi"
Questo avviso viene attivato se un utente non attiva un ruolo dopo un determinato periodo.

* **Numero di giorni**: specificare hello numero di giorni, da 0 too100, che un utente possono essere inseriti senza l'attivazione di un ruolo.

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_dash.png
[2]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_settings.png

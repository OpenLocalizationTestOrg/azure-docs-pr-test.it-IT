---
title: aaaTroubleshooting dell'appartenenza dinamica per i gruppi | Documenti Microsoft
description: Suggerimenti per la risoluzione dei problemi di appartenenza dinamica per i gruppi di Azure AD.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a>Risoluzione dei problemi di appartenenza dinamica per i gruppi
**Ho configurato una regola in un gruppo, ma nessuna appartenenza vengono aggiornata nel gruppo hello**<br/>Verificare che hello **Abilita gestione gruppi delegata** impostazione troppo**Sì** in hello **configura** scheda. Questa impostazione verrà visualizzato solo se si è connessi come viene assegnato un toowhom utente una licenza di Azure Active Directory Premium. Verificare i valori hello per gli attributi utente sulla regola hello: sono presenti utenti che soddisfano la regola hello?

**Ho configurato una regola, ma ora in cui vengono rimossi i membri esistenti hello della regola hello**<br/>Si tratta di un comportamento previsto. I membri esistenti del gruppo di hello vengono rimossi quando una regola è abilitata o modificata. gli utenti di Hello restituiti dalla valutazione della regola hello vengono aggiunti come gruppo toohello membri.     

**Quando si aggiunge o modifica una regola non vengono visualizzate immediatamente le modifiche a livello di appartenenza. Perché?**<br/>La valutazione dell'appartenenza dedicata viene eseguita periodicamente in un processo asincrono in background. Quanto tempo richiede processo hello è determinato dal numero di hello di utenti, le dimensioni di directory e hello del gruppo di hello creato come risultato della regola hello. In genere, le directory con un numero limitato di utenti verranno visualizzato modifiche all'appartenenza di gruppo hello in meno di cinque minuti. Directory con un numero elevato di utenti può richiedere 30 minuti o più toopopulate.

### <a name="next-steps"></a>Passaggi successivi
Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.

* [Gestione di accesso tooresources con gruppi di Azure Active Directory](active-directory-manage-groups.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Informazioni su Azure Active Directory](active-directory-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)

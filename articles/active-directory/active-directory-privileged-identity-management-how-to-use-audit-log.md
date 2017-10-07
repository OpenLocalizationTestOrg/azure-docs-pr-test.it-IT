---
title: log di controllo di aaaHow toouse hello in Azure AD Privileged Identity Management | Documenti Microsoft
description: Informazioni su come di log di controllo di hello toouse nell'estensione di hello Azure Privileged Identity Management.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a>Utilizzo di log di controllo hello in PIM
È possibile utilizzare tutte le assegnazioni utente hello e attivazioni hello Privileged Identity Management (PIM) audit log toosee all'interno di un determinato periodo di tempo. Se si desidera cronologia di controllo completo hello toosee dell'attività nel tenant, tra cui l'amministratore, l'utente finale e attività di sincronizzazione, è possibile utilizzare hello [report di utilizzo e di accesso di Azure Active Directory.](active-directory-view-access-usage-reports.md)

## <a name="navigate-toohello-audit-log"></a>Passare il log di controllo toohello
Da hello [portale di Azure](https://portal.azure.com) dashboard, seleziona hello **Azure AD Privileged Identity Management** app. Da qui, accedere ai log di controllo hello facendo clic **gestire i ruoli con privilegi** > **cronologia controlli** nel dashboard PIM hello.

## <a name="hello-audit-log-graph"></a>grafico di log di controllo Hello
È possibile utilizzare attivazioni totali di hello audit log tooview hello attivazioni max al giorno e attivazioni medie al giorno in un grafico a linee.  È anche possibile filtrare i dati hello dal ruolo se è presente più di un ruolo nella cronologia di controllo hello.

Hello utilizzare **ora**, **azione**, e **ruolo** pulsanti toosort hello log.

## <a name="hello-audit-log-list"></a>elenco di log di controllo Hello
Hello colonne nell'elenco di log di controllo hello sono:

* **Richiedente** -utente hello che ha richiesto l'attivazione del ruolo hello o modifica.  Se il valore di hello è di tipo "Sistema Azure", vedere il log di controllo di Azure di hello per altre informazioni.
* **Utente** -utente hello in fase di attivazione o tooa ruolo.
* **Ruolo** -ruolo hello assegnato o attivato dall'utente hello.
* **Azione** - azioni hello dal richiedente hello. Le azioni possono includere assegnazione, annullamento dell'assegnazione, attivazione o disattivazione.
* **Tempo** : quando si è verificata hello azione.
* **Ragionamento** -se il testo è stato immesso nel campo motivo hello durante l'attivazione, verrà visualizzato.
* **Scadenza** : rilevante solo per l'attivazione dei ruoli.

## <a name="filter-hello-audit-log"></a>Log di controllo di filtro hello
È possibile filtrare le informazioni di hello che viene visualizzato nel log di controllo hello facendo hello **filtro** pulsante.  Hello **blade di parametri di aggiornamento grafico** verranno visualizzati.

Dopo aver impostato i filtri di hello, fare clic su **aggiornamento** dati hello toofilter nel registro hello.  Se non viene visualizzato immediatamente dati hello, aggiornare la pagina hello.

### <a name="change-hello-date-range"></a>Modificare l'intervallo di date hello
Hello utilizzare **oggi**, **settimana precedente**, **mese scorso**, o **personalizzato** i pulsanti di intervallo di tempo toochange hello del log di controllo hello.

Quando si sceglie di hello **personalizzato** pulsante, verrà assegnato un **da** campo Data e un **a** data toospecify campo un intervallo di date per il log di hello.  È possibile immettere date hello in formato MM/gg/aaaa o fare clic su hello **calendario** icona e scegliere Data hello da un calendario.

### <a name="change-hello-roles-included-in-hello-log"></a>Modificare i ruoli di hello inclusi nel registro hello
Selezionare o deselezionare hello **ruolo** casella di controllo successivo tooeach ruolo tooinclude o escludere dalla hello del log.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]


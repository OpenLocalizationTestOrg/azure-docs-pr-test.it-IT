---
title: Operazioni di Synchronization Service Manager per Azure AD Connect | Microsoft Docs
description: Comprendere scheda operazioni hello in hello Synchronization Service Manager per Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: decbc53613d456a71cd116c40c5e1fd761efd4af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-sync-service-manager-operations-tab"></a>Utilizzo di hello scheda operazioni di gestione del servizio di sincronizzazione

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

scheda operazioni Hello Mostra i risultati di hello delle operazioni più recenti di hello. Questa scheda è chiave toounderstand e risolvere i problemi.

## <a name="understand-hello-information-visible-in-hello-operations-tab"></a>Comprendere le informazioni di hello visibili nella scheda operazioni hello
Nella metà superiore Hello Mostra tutte le esecuzioni in ordine cronologico. Per impostazione predefinita, i log di operazioni hello mantiene informazioni hello negli ultimi sette giorni, ma questa impostazione può essere modificata con hello [dell'utilità di pianificazione](active-directory-aadconnectsync-feature-scheduler.md). Si desidera toolook per qualsiasi esecuzione che mostrano uno stato di esito positivo. È possibile modificare l'ordinamento facendo clic sulle intestazioni hello hello.

Hello **stato** colonna è informazioni più importanti hello e Mostra hello problema più grave per l'esecuzione. Ecco un breve riepilogo di stato di hello più comuni in ordine di priorità tooinvestigate (dove * indicare diverse stringhe di messaggio di errore).

| Stato | Commento |
| --- | --- |
| stopped-* |non è stato possibile completare Hello eseguire. Ad esempio, se hello sistema remoto è inattivo e non può essere contattato. |
| stopped-error-limit |Sono presenti più di 5.000 errori. eseguire Hello automaticamente è stato arrestato a causa di toohello numero elevato di errori. |
| completato-\*-errori |Hello eseguire completata, ma sono presenti errori (meno di 5.000) che devono essere esaminati. |
| completato-\*-avvisi |eseguire Hello completata, ma alcuni dati non sono in stato di hello previsto. Se sono presenti errori, questo messaggio è in genere solo un sintomo. Evitare di analizzare gli avvisi fino a quando gli errori non sono stati risolti. |
| esito positivo |Non sono presenti problemi. |

Quando si seleziona una riga, nella parte inferiore di hello Aggiorna i dettagli di hello tooshow di esecuzione. toohello all'estrema sinistra della parte inferiore di hello, si potrebbe ricevere un detto elenco **passaggio #**. L'elenco è mostrato solo quando nella foresta sono presenti più domini e ogni dominio è rappresentato da un passaggio. è possibile trovare il nome di dominio Hello titolo hello **partizione**. In **le statistiche della sincronizzazione**, è possibile trovare altre informazioni sul numero di hello di modifiche che sono stati elaborati. È possibile fare clic su hello collegamenti tooget un elenco di oggetti hello modificato. Se alcuni oggetti presentano errori, questi verranno visualizzati in **Synchronization Errors**(Errori di sincronizzazione).

Per altre informazioni, vedere [Risoluzione dei problemi relativi a un oggetto che non esegue la sincronizzazione in Azure AD](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su hello [sincronizzazione di Azure AD Connect](active-directory-aadconnectsync-whatis.md) configurazione.

Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).

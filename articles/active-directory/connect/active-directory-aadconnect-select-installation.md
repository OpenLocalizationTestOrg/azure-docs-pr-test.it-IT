---
title: 'Azure AD Connect: Selezionare il tipo di installazione | Documentazione Microsoft'
description: "Questo argomento viene illustrata la modalità installazione hello tooselect digitare toouse per Azure AD Connect"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a>Selezionare quali toouse di tipo di installazione per Azure AD Connect
Per Azure AD Connect sono disponibili due tipi di installazione: rapida e personalizzata. In questo argomento contribuisce di toodecide quale opzione toouse durante l'installazione.

## <a name="express"></a>Express
Express è l'opzione più comuni di hello e viene utilizzato circa il 90% di tutte le nuove installazioni. È stato progettato tooprovide una configurazione adatta per scenari più comuni di clienti hello.

Richiede:

- Una singola foresta Active Directory locale.
- Si dispone di un account di amministratore dell'organizzazione che è possibile utilizzare per l'installazione di hello.
- Meno di 100.000 oggetti nell'istanza locale di Active Directory.

Offre:

- [La sincronizzazione delle password](active-directory-aadconnectsync-implement-password-synchronization.md) da on-premise tooAzure AD per single sign-on.
- Una configurazione che consente di sincronizzare [utenti, gruppi, contatti e computer Windows 10](active-directory-aadconnectsync-understanding-default-configuration.md).
- Sincronizzazione di tutti gli oggetti idonei in tutti i domini e tutte le unità organizzative.
- [L'aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md) è abilitato toomake è necessario utilizzare sempre hello versione più recente disponibile.

Casi in cui è comunque possibile usare l'installazione rapida:

- Se non si desidera toosynchronize tutte le unità organizzative, è possibile comunque utilizzare Express e sull'ultima pagina hello, deselezionare **avviare il processo di sincronizzazione hello...** *. Quindi eseguire di nuovo l'installazione guidata di hello e modificare le unità organizzative hello [opzioni di configurazione](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) e attivare la sincronizzazione pianificata.
- Si desidera tooenable una delle funzionalità di hello in Azure AD Premium, ad esempio il writeback delle Password. Vengono prima sottoposti installazione iniziale hello tooget express completata. Quindi eseguire di nuovo l'installazione guidata di hello e modificare hello [opzioni di configurazione](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).

## <a name="custom"></a>Personalizzate
percorso personalizzato Hello consente molte più opzioni rispetto alla versione express. Deve essere utilizzata in tutti i casi in cui configurazione hello descritta nella sezione precedente per le edizioni express non è rappresentativo dell'organizzazione.

Usare questo tipo nei seguenti casi:

- Account di accesso tooan enterprise admin non è in Active Directory.
- Si dispone di più di una foresta o toosynchronize si prevede più di una foresta in hello future.
- Sono presenti domini della foresta non è raggiungibile dal server di connessione hello.
- Si prevede di federazione toouse o autenticazione pass-through per l'accesso utente.
- Si dispone di più di 100.000 oggetti ed è necessario toouse una versione completa di SQL Server.
- Si prevede di filtraggio basato su un gruppo di toouse e non solo dominio o il filtro basato su unità Organizzativa.

## <a name="upgrade-from-dirsync"></a>Aggiornamento da DirSync
Se si utilizza DirSync, quindi seguire hello [l'aggiornamento da DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade la configurazione esistente. Sono disponibili due diverse opzioni di aggiornamento:

- Connettersi tooinstall aggiornamento sul posto in hello stesso server.
- Parallela distribuzione tooinstall Connect in un nuovo server mentre il server DirSync esistente di hello è ancora operativo.

## <a name="upgrade-from-azure-ad-sync"></a>Aggiornamento da Azure AD Sync
Se si utilizza Azure AD Sync, quindi è possibile seguire hello [stessi passaggi](active-directory-aadconnect-upgrade-previous-version.md) come quando esegue l'aggiornamento da una connessione versione tooa più recente. Sono disponibili due diverse opzioni di aggiornamento:

- Connettersi tooinstall aggiornamento sul posto in hello stesso server.
- Migrazione di attività tooinstall Connect in un nuovo server mentre il server di Azure AD Sync esistente hello è ancora operativo.

## <a name="migrate-from-fim2010-or-mim2016"></a>Migrazione da FIM2010 o MIM2016
Se si usano attualmente Forefront Identity Manager 2010 o Microsoft Identity Manager 2016 con hello connettore Azure AD, l'unica possibilità è una migrazione. Seguire i passaggi di hello descritti in [apertura migrazione](active-directory-aadconnect-upgrade-previous-version.md#swing-migration). Nei passaggi hello, sostituire tutti i riferimenti di Azure AD Sync con FIM2010/MIM2016.

## <a name="next-steps"></a>Passaggi successivi
A seconda opzione hello selezionato toouse, utilizzare la tabella hello di toofind sinistro toohello contenuto dell'articolo con hello passaggi dettagliati.

---
title: "Funzionalità in anteprima di Azure AD Connect | Documentazione Microsoft"
description: "Questo argomento descrive in maggiore dettaglio le funzionalità in anteprima di Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a>Altre informazioni sulle funzionalità in anteprima
In questo argomento viene descritto come toouse funzionalità attualmente in anteprima.

## <a name="group-writeback"></a>Writeback dei gruppi
opzione Hello per writeback dei gruppi di funzionalità facoltative consente toowriteback **gruppi di Office 365** tooa foresta con Exchange installato. Si tratta di un gruppo che è sempre gestito nel cloud hello. Se si dispone di Exchange locale, quindi è possibile scrivere nuovamente locale tooon questi gruppi in modo da inviare e ricevere messaggi di posta elettronica da questi gruppi di utenti con una cassetta postale di Exchange locale.

Ulteriori informazioni sui gruppi di Office 365 e come toouse li può essere trovati [qui](http://aka.ms/O365g).

Un gruppo di Office 365 viene rappresentato come gruppo di distribuzione in AD DS locale. Exchange server locale deve trovarsi in Exchange 2013 aggiornamento cumulativo 8 (rilasciato nel marzo 2015) o Exchange 2016 toorecognize questo nuovo tipo di gruppo.

**Note durante l'anteprima di hello**

* attributo di Hello address book attualmente non viene popolata in anteprima hello. Senza questo attributo, il gruppo di hello non è visibile nell'elenco indirizzi globale hello. Hello toopopulate modo più semplice l'attributo è di cmdlet di Exchange PowerShell hello toouse `update-recipient`.
* Solo le foreste con uno schema di Exchange hello sono destinazioni valide per i gruppi. Se è stato rilevato alcun Exchange, quindi writeback dei gruppi non è possibile tooenable.
* Attualmente sono supportate solo le distribuzioni in organizzazioni di Exchange a foresta singola. Se si dispone di più di Exchange dell'organizzazione locale, è necessario una soluzione GALSync locale per questi gruppi tooappear le altre foreste.
* funzionalità di writeback gruppo Hello non gestisce i gruppi di protezione o gruppi di distribuzione.

> [!NOTE]
> TooAzure una sottoscrizione AD Premium è necessario per il writeback di gruppo.
> 
>

## <a name="user-writeback"></a>Writeback degli utenti
> [!IMPORTANT]
> Hello writeback anteprima funzionalità utente è stata rimossa in tooAzure di aggiornamento di agosto 2015 hello AD Connect. Se questa funzionalità è stata abilitata, è necessario disabilitarla.
>
>

## <a name="next-steps"></a>Passaggi successivi
Continuare l'[Installazione personalizzata di Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).

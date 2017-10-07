---
title: "aaaWhat è basata sul gruppo di licenza in Azure Active Directory? | Microsoft Docs"
description: Informazioni sulle licenze basate sui gruppi di Azure Active Directory, come funzionano e procedure consigliate
services: active-directory
keywords: Licenze di Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/29/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 11647de6b76022cd2393751fcafc67ce671aeba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="group-based-licensing-basics-in-azure-active-directory"></a>Concetti base sulle licenze basate sui gruppi in Azure Active Directory

Per utilizzare i servizi cloud Microsoft a pagamento come Office 365, Enterprise Mobility + Security, Dynamics CRM e altri prodotti simili è necessaria la licenza. Queste licenze assegnate tooeach gli utenti che devono accedere a servizi toothese. licenze toomanage, gli amministratori di utilizzano uno dei portali di gestione di hello (Office o Azure) e i cmdlet di PowerShell. Azure Active Directory (Azure AD) è l'infrastruttura sottostante hello che supporta la gestione di identità per tutti i servizi cloud Microsoft. Azure AD archivia le informazioni sugli stati di assegnazione delle licenze per gli utenti.

Fino ad ora, licenze può essere assegnate solo a livello di singolo utente hello, che può rendere difficile la gestione su larga scala. Ad esempio, tooadd o rimuovere licenze utente in base alle modifiche organizzative, ad esempio utenti partecipazione o sull'uscita hello organizzazione o un reparto, un amministratore spesso necessario scrivere uno script di PowerShell complesso. Questo script richiama singolo servizio cloud toohello.

tooaddress quelli ostacoli, Azure AD ora include in base al gruppo di licenze. È possibile assegnare uno o più licenze tooa categoria. Azure AD garantisce che assegnazione delle licenze hello tooall i membri del gruppo di hello. Tutti i nuovi membri che partecipa a gruppo hello sono assegnati le licenze appropriate hello. Quando escono dalla gruppo hello, vengono rimosse le licenze. Questo elimina la necessità hello per l'automazione della gestione delle licenze tramite PowerShell tooreflect modifiche nell'organizzazione di hello e struttura reparto a ogni utente.

## <a name="features"></a>Funzionalità

Di seguito sono funzionalità principali di hello di licenze basate su gruppo:

- Le licenze possono essere assegnate tooany gruppo di sicurezza di Azure AD. I gruppi di sicurezza possono essere sincronizzati in locale tramite Azure AD Connect. È anche possibile creare gruppi di sicurezza direttamente in Azure AD (detto anche gruppi solo cloud), o automaticamente tramite la funzionalità dei gruppi dinamici hello Azure AD.

- Quando il gruppo tooa viene assegnata una licenza di prodotto, amministratore hello possibile disabilitare uno o più piani di servizio nel prodotto hello. Questa operazione viene eseguita in genere, quando l'organizzazione hello non è ancora pronto toostart utilizzando un servizio incluso in un prodotto. Ad esempio, hello amministratore potrebbe assegnare reparto tooa Office 365, ma disabilitare temporaneamente il servizio di Yammer hello.

- Sono supportati tutti i servizi cloud Microsoft che richiedono licenze a livello di utente. Sono inclusi tutti i prodotti di Office 365, Enterprise Mobility + Security e Dynamics CRM.

- In base al gruppo di licenze è attualmente disponibile solo tramite [hello Azure portal](https://portal.azure.com). Se si utilizzano principalmente altri portali di gestione per la gestione utenti e gruppi, ad esempio il portale di Office 365 hello, è possibile continuare toodo così. Ma è necessario utilizzare licenze toomanage portale Azure hello a livello di gruppo.

- Azure AD gestisce automaticamente le modifiche alle licenze determinate da modifiche all'appartenenza a gruppi. In genere, le modifiche alle licenza sono attive dopo pochi minuti rispetto alle modifiche all'appartenenza.

- Un utente può essere membro di più gruppi con norme di licenza specificate. Un utente può anche disporre di alcune licenze assegnate in modo diretto, indipendentemente dai gruppi. Hello risultante lo stato utente è una combinazione di tutti i prodotti assegnato e licenze di servizio.

- In alcuni casi, le licenze non possono essere assegnate a utente tooa. Ad esempio, potrebbero non essere presenti numero sufficiente di licenze disponibili nel tenant hello o servizi incompatibili potrebbero sono stati assegnati a hello stesso tempo. Gli amministratori hanno accesso tooinformation sugli utenti a cui Azure AD non completamente può elaborare le licenze di gruppo. Possono adottare misure correttive in base a tali informazioni.

- Durante l'anteprima pubblica, gestione delle licenze in base al gruppo di hello tenant toouse è necessaria una sottoscrizione a pagamento o di valutazione per le edizioni di Azure AD Basic o Premium.

## <a name="next-steps"></a>Passaggi successivi

toolearn più informazioni sugli altri scenari per la gestione delle licenze tramite in base al gruppo di licenze, vedere:

* [Introduzione alle licenze di Azure Active Directory](active-directory-licensing-get-started-azure-portal.md)
* [L'assegnazione gruppo di licenze tooa in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Identificazione e risoluzione dei problemi relativi alle licenze per un gruppo in Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Come singoli toomigrate concesso in licenza agli utenti in base toogroup licenze in Azure Active Directory](active-directory-licensing-group-migration-azure-portal.md)
* [Scenari aggiuntivi relativi alle licenze basate sui gruppi in Azure Active Directory](active-directory-licensing-group-advanced.md)

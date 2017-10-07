---
title: aaaLimitations di collaborazione B2B di Azure Active Directory | Documenti Microsoft
description: Limitazioni correnti di Collaborazione B2B di Azure Active Directory
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 322081f32fbacfe67ee1300993c7df1870e498bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a>Limitazioni di Collaborazione B2B di Azure AD
Collaborazione B2B di Active Directory (Azure AD) di Azure è attualmente limitazioni toohello soggetto descritte in questo articolo.

## <a name="possible-double-multi-factor-authentication"></a>Possibile autenticazione a più fattori doppia
Con Azure AD B2B, è possibile applicare multi-factor authentication all'organizzazione risorse hello (Buongiorno si invitano organizzazione). vengono descritti in dettaglio i motivi Hello per questo approccio [accesso condizionale per gli utenti di collaborazione B2B](active-directory-b2b-mfa-instructions.md). Se un partner dispone già di multi-factor authentication consente di impostare e applicati, gli utenti necessario autenticazione hello tooperform una volta all'interno dell'organizzazione principale e quindi nuovamente in quelle in uso.

## <a name="instant-on"></a>Immediatezza
Nei flussi di collaborazione B2B di hello, aggiungiamo directory toohello users e aggiornarli in modo dinamico durante il riscatto di invito, assegnazione di app e così via. gli aggiornamenti di Hello e scritture in genere avvengono nell'istanza di una directory e devono essere replicate in tutte le istanze. La replica viene completata quando tutte le istanze sono state aggiornate. A volte quando oggetto hello viene scritto o aggiornato in un'istanza e hello chiamare tooretrieve questo oggetto è tooanother istanza, possono verificarsi le latenze di replica. In tal caso, aggiornare o riprovare toohelp. Se si scrive un'app usando l'API, quindi tentativi con backoff è un tooalleviate difensivo, buona pratica questo problema.

## <a name="next-steps"></a>Passaggi successivi

Vedere gli altri articoli su Azure AD B2B Collaboration.

* [Che cos'è Azure AD B2B Collaboration?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Proprietà dell'utente di Collaborazione B2B](active-directory-b2b-user-properties.md)
* [Aggiunta di un ruolo di tooa utente collaborazione B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegare gli inviti a Collaborazione B2B](active-directory-b2b-delegate-invitations.md)
* [Gruppi dinamici e Collaborazione B2B](active-directory-b2b-dynamic-groups.md)
* [Codici ed esempi di PowerShell per Collaborazione B2B](active-directory-b2b-code-samples.md)
* [Configurare app SaaS per Collaborazione B2B](active-directory-b2b-configure-saas-apps.md)
* [Token utente in Collaborazione B2B](active-directory-b2b-user-token.md)
* [Mapping delle attestazioni utente per Collaborazione B2B](active-directory-b2b-claims-mapping.md)
* [Condivisione esterna di Office 365](active-directory-b2b-o365-external-user.md)

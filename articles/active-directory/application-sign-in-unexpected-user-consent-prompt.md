---
title: richiesta di consenso aaaUnexpected durante l'accesso dell'applicazione tooan | Documenti Microsoft
description: "Come tootroubleshoot quando un utente visualizza una richiesta di consenso per un'applicazione è stata integrata con Azure Active Directory che non prevista"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a>Consenso imprevisto durante l'accesso dell'applicazione tooan

Molte applicazioni che si integrano con Azure Active Directory richiedono risorse di toovarious autorizzazioni in ordine toorun. Quando queste risorse sono inoltre integrate con Azure Active Directory, framework di consenso tooaccess autorizzazioni li viene richiesto tramite hello Azure AD. 

Ciò comporta una richiesta di consenso visualizzandola hello prima volta che un'applicazione, è spesso un'unica operazione. 

## <a name="scenarios-in-which-users-see-consent-prompts"></a>Scenari in cui gli utenti visualizzano richieste di consenso

Ulteriori richieste aggiuntive sono possibili in vari scenari:

* Hello insieme di autorizzazioni richiesto dall'applicazione hello è stato modificato.

* gli utenti Hello originariamente acconsentito toohello applicazione non è un amministratore, e ora un utente diverso (non-admin) si usa un'applicazione hello per hello prima volta.

* gli utenti Hello originariamente acconsentito toohello applicazione sono un amministratore, ma essi non fornire il consenso per conto di tutta l'organizzazione hello.

* utilizza un'applicazione Hello [consenso incrementale e dinamico](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest autorizzazioni aggiuntive dopo che è stato inizialmente consenso. Questo tipo di consenso viene frequentemente usato quando funzionalità facoltative di un'applicazione richiedono autorizzazioni ulteriori a quelle richieste per la funzionalità di base.

* Il consenso è stato revocato dopo essere stato inizialmente consentito.

* sviluppatore Hello è configurato toorequire applicazione hello una richiesta di consenso ogni volta che viene utilizzata (Nota: questo non è consigliata).

## <a name="next-steps"></a>Passaggi successivi

-   [App, autorizzazioni e consenso in Azure Active Directory (endpoint v1.0)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [Gli ambiti, autorizzazioni e consenso hello Azure Active Directory (endpoint v 2.0)](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)



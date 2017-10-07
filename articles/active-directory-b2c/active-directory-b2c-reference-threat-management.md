---
title: 'Azure Active Directory B2C: Gestione delle minacce | Documentazione Microsoft'
description: Vengono illustrate le tecniche di rilevamento e mitigazione di attacchi Denial of Service e attacchi alle password in Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: vigunase
manager: Ajith Alexander
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2016
ms.author: 
ms.openlocfilehash: 60bc0cc392b332cc4e9741ddb97dfa58e68ed420
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a>Azure Active Directory B2C: Gestione delle minacce

Gestione delle minacce include la pianificazione per la protezione da attacchi contro il sistema e le reti. Attacchi Denial of service potrebbero rendere le risorse agli utenti di toointended non disponibile. Password attacchi lead toounauthorized accesso tooresources. Azure Active Directory B2C (Azure AD B2C) offre funzionalità incorporate che aiutano a proteggere i dati da queste minacce in diversi modi.

## <a name="denial-of-service-attacks"></a>Attacchi Denial of Service

Azure Active Directory B2C utilizza tecniche di rilevamento e prevenzione come cookie SYN e tooprotect di limiti di velocità e connessione sottostante risorse contro gli attacchi di tipo denial of service.

## <a name="password-attacks"></a>Attacchi alle password

Azure AD B2C dispone inoltre di tecniche di mitigazione per gli attacchi alle password. Questa mitigazione include sia attacchi di forza bruta che attacchi con dizionario alle password. Le password impostati per gli utenti sono necessari toobe piuttosto complessi. Tramite segnali diversi, Azure AD B2C analizza integrità hello delle richieste. Azure Active Directory B2C è progettato toointelligently differenziare utenti previsti da pirati informatici e botnet bloccate. Azure Active Directory B2C fornisce un toolock strategia sofisticate gli account basati su password hello immesse, probabilità hello di un attacco.

Per ulteriori informazioni, visitare hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).

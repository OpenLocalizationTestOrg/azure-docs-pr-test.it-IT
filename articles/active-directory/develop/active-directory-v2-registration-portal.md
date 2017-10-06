---
title: Argomenti della Guida portale di registrazione aaaApp | Documenti Microsoft
description: "Una descrizione delle varie funzionalità nel portale di registrazione app Microsoft hello."
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: f0507c28-9464-4d3e-bd53-de9053fd5278
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: 3eb17b629577446a336152799497e7d980fb825d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="app-registration-reference"></a>Riferimento alla registrazione delle app
Questo documento fornisce contesto e le descrizioni delle diverse funzionalità nel portale di registrazione di Microsoft App hello [https://apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).

## <a name="my-applications"></a>Applicazioni personali
Questo elenco contiene tutte le applicazioni registrate per essere utilizzate con l'endpoint v 2.0 hello Azure AD.  Queste applicazioni hanno hello possibilità toosign gli utenti con entrambi gli account personali dell'account Microsoft e account di lavoro o dell'istituto di istruzione da Azure Active Directory.  toolearn informazioni sull'endpoint v 2.0 hello Azure AD, vedere il nostro [Panoramica v 2.0](active-directory-appmodel-v2-overview.md).  Queste applicazioni possono inoltre essere toointegrate utilizzato con l'endpoint di autenticazione account di Microsoft hello, `https://login.live.com`.

## <a name="live-sdk-applications"></a>Applicazioni Live SDK
Questo elenco include tutte le applicazioni registrate per l'uso solo con l'account Microsoft.  Non sono abilitate per l'uso con Azure Active Directory.  Si tratta di dove sono disponibili tutte le applicazioni che in precedenza era state registrate con il portale per sviluppatori di MSA hello in `https://account.live.com/developers/applications`.  Tutte le funzioni eseguite in precedenza in `https://account.live.com/developers/applications` ora possono essere eseguite nel nuovo portale, `https://apps.dev.microsoft.com`.  Per altre domande relative alle applicazioni dell'account Microsoft, è possibile contattare Microsoft.

## <a name="application-secrets"></a>Segreti applicazione
I segreti dell'applicazione sono credenziali che consentono l'applicazione tooperform affidabile [l'autenticazione client](http://tools.ietf.org/html/rfc6749#section-2.3) con Azure AD.  In OAuth e OpenID Connect di segreti un'applicazione è comunemente noti tooas un `client_secret`.  Nel protocollo v 2.0 hello, qualsiasi applicazione che riceve un token di sicurezza in una posizione indirizzabile web (tramite un `https` schema) deve utilizzare un tooidentify segreto applicazione stesso tooAzure AD al momento di riscatto del token di sicurezza.  Inoltre, qualsiasi client native che riceve i token in un dispositivo verranno proibiti dall'utilizzo di un'autenticazione client secret tooperform applicazione, toodiscourage hello archiviazione di segreti in ambienti non protetti.

Ogni app può contenere due segreti applicazione validi in qualsiasi momento.  Tramite la gestione di due segreti, hai hello ablilty tooperform periodica rollover della chiave in tutto l'ambiente dell'applicazione.  Dopo la migrazione intera hello l'applicazione tooa nuova chiave privata, è possibile eliminare segreto precedente hello e il provisioning di uno nuovo.

A questo punto, sono consentiti solo due tipi di segreti dell'applicazione nel portale di registrazione applicazione hello.  Scelta di **generare una nuova Password** genererà e archiviare una chiave privata condivisa nell'archivio dati di hello, che è possibile utilizzare nell'applicazione.  Scelta di **generare nuova coppia di chiavi** creerà una nuova coppia di chiavi pubblica/privata che può essere scaricata e usata per l'autenticazione di client tooAzure Active Directory.

## <a name="profile"></a>Profilo
sezione profilo Hello del portale di registrazione applicazione hello può essere utilizzato toocustomize hello sign nella pagina per l'applicazione.  In questo momento è possibile modificare hello Accedi logo dell'applicazione della pagina, condizioni per l'URL del servizio e l'informativa sulla privacy.  Hello logo deve essere un trasparente 48 x 48 o 50 x 50 pixel immagine in un file GIF, PNG o JPEG 15 KB o inferiore.  Provare a modificare i valori hello e hello visualizzazione risultante nella pagina di accesso.

## <a name="live-sdk-support"></a>Supporto Live SDK
Quando si abilita "Supporto di Live SDK", archivia qualsiasi applicazione in cui verranno eseguito il provisioning di segreti che crei hello Azure AD e i dati dell'Account Microsoft.  In questo modo l'applicazione toointegrate direttamente con hello servizio Account Microsoft (login.live.com).  Se si desidera toobuild un'app usando Account Microsoft direttamente (come endpoint di v 2.0 toousing anziché hello Azure AD), assicurarsi che il supporto di SDK in tempo reale è abilitato.

Disabilitando il supporto di Live SDK garantisce che il segreto dell'applicazione hello viene scritto nell'archivio dati hello Azure AD.  archivio dati di Azure AD Hello incorpora normative aziendale che consentono un toomeet determinati standard, ad esempio conformità FISMA.  Se si abilita il supporto Live SDK, l'applicazione potrebbe non essere conforme in base ad alcuni di questi standard.

Se si prevede solo l'endpoint toouse hello Azure AD versione 2.0, è possibile disabilitare il supporto di Live SDK.


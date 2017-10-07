---
title: aaaAzure Bus di servizio di autenticazione e autorizzazione | Documenti Microsoft
description: Autenticare le app tooService Bus con l'autenticazione di firma di accesso condiviso (SAS).
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 18bad0ed-1cee-4a5c-a377-facc4785c8c9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: sethm
ms.openlocfilehash: 898a2144c99d8fac074b6d85604f710bf512e71e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-and-authorization"></a>Autenticazione e autorizzazione del bus di servizio

Le applicazioni possono eseguire l'autenticazione tooAzure Bus di servizio di firma di accesso condiviso (SAS) utilizzando l'autenticazione. Condiviso di firma di accesso autenticazione consente applicazioni tooauthenticate tooService Bus usando una chiave di accesso configurata nello spazio dei nomi hello o nell'entità hello a cui sono associati diritti specifici. È quindi possibile utilizzare questa chiave toogenerate un token di firma di accesso condiviso che i client possono usare tooauthenticate tooService Bus.

> [!IMPORTANT]
> È consigliabile utilizzare SAS invece di Azure AD Access Control (anche noto come Servizio di controllo di accesso o ACS), perché quest'ultimo verrà deprecato. La firma di accesso condiviso offre uno schema di autenticazione per il bus di servizio semplice, flessibile e di facile utilizzo. Le applicazioni possono utilizzare SAS negli scenari in cui non è necessario nozione di hello toomanage di "utente autorizzato." Per altre informazioni, vedere [questo post di blog](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/).

## <a name="shared-access-signature-authentication"></a>Autenticazione della firma di accesso condiviso

[L'autenticazione SAS](service-bus-sas.md) consente toogrant è una risorsa di Bus tooService accesso utente con diritti specifici. L'autenticazione di firma di accesso condiviso nel Bus di servizio è inclusa la configurazione di hello di una chiave di crittografia con i relativi diritti in una risorsa del Bus di servizio. I client possono quindi ottenere accesso toothat risorsa presentando un token di firma di accesso condiviso, è costituito da cui si accede di URI della risorsa hello e una scadenza firmata con hello chiave configurata.

È possibile configurare le chiavi per la firma di accesso condiviso in uno spazio dei nomi del bus di servizio. chiave Hello applica tooall le entità di messaggistica nello spazio dei nomi. È anche possibile configurare le chiavi nelle code e negli argomenti del bus di servizio. SAS è anche supportato in [Inoltro di Azure](../service-bus-relay/relay-authentication-and-authorization.md).

toouse firma di accesso condiviso, è possibile configurare un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) oggetto su un spazio dei nomi, coda o argomento. Questa regola è costituita da hello seguenti elementi:

* *KeyName* che identifica la regola hello.
* *PrimaryKey* è una chiave di crittografia utilizzato toosign/convalidare i token di firma di accesso condiviso.
* *SecondaryKey* è una chiave di crittografia utilizzato toosign/convalidare i token di firma di accesso condiviso.
* *Diritti* che rappresenta la raccolta hello di ascolto, invio o gestire le autorizzazioni concesse.

Le regole di autorizzazione configurate a livello di spazio dei nomi hello possono concedere l'accesso tooall entità in uno spazio dei nomi per i client con i token firmati con una chiave corrispondente hello. Backup too12 tali regole di autorizzazione possono essere configurate su una coda, argomento o dello spazio dei nomi di Service Bus. Per impostazione predefinita, un oggetto [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) con tutti i diritti viene configurato per ogni spazio dei nomi quando ne viene eseguito il provisioning per la prima volta.

tooaccess un'entità, i client di hello richiede un token di firma di accesso condiviso generato usando uno specifico [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). token SAS Hello viene generato con una chiave di crittografia associata alla regola di autorizzazione hello hello è richiesto l'algoritmo HMAC-SHA256 di una stringa di risorsa costituito da risorse hello accesso toowhich URI e una scadenza.

Supporto dell'autenticazione SAS per Bus di servizio è incluso in hello Azure .NET SDK versioni 2.0 e versioni successive. Nella firma di accesso condiviso è incluso il supporto per un oggetto [SharedAccessAuthorizationRule](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Tutte le API che accettano una stringa di connessione come parametro includono il supporto per le stringhe di connessione della firma di accesso condiviso.

## <a name="next-steps"></a>Passaggi successivi

- Per altre informazioni su SAS, vedere [Autenticazione del bus di servizio con firme di accesso condiviso](service-bus-sas.md).
- [Modifica degli spazi dei nomi di tooACS abilitato.](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)
- Per informazioni corrispondenti sull'autenticazione in Inoltro di Azure, vedere [Autenticazione e autorizzazione di Inoltro di Azure](../service-bus-relay/relay-authentication-and-authorization.md). 


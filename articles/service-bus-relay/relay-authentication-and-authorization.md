---
title: aaaAzure inoltro autenticazione e autorizzazione | Documenti Microsoft
description: Panoramica dell'autenticazione con firma di accesso condiviso (SAS) in Inoltro di Azure
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: b27914672ce968da2bddba8dafc5683ebf3834ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-authentication-and-authorization"></a>Autenticazione e autorizzazione di Inoltro di Azure
Le applicazioni possono eseguire l'autenticazione tooAzure inoltro utilizzando l'autenticazione di firma di accesso condiviso (SAS). Simile troppo[messaggistica del Bus di servizio](../service-bus-messaging/service-bus-authentication-and-authorization.md), l'autenticazione SAS consente applicazioni tooauthenticate toohello servizio di inoltro di Azure usando una chiave di accesso configurata nello spazio dei nomi inoltro hello. È quindi possibile utilizzare questa chiave toogenerate un token di firma di accesso condiviso che i client possono usare tooauthenticate toohello servizio di inoltro.

## <a name="shared-access-signature-authentication"></a>Autenticazione della firma di accesso condiviso
[L'autenticazione SAS](../service-bus-messaging/service-bus-sas.md) consente toogrant è una risorsa di inoltro tooAzure accesso utente con diritti specifici. L'autenticazione SAS inclusa la configurazione di hello di una chiave di crittografia con i relativi diritti in una risorsa. I client possono quindi ottenere accesso toothat risorsa presentando un token di firma di accesso condiviso, è costituito da cui si accede di URI della risorsa hello e una scadenza firmata con hello chiave configurata.

È possibile configurare le chiavi per la firma di accesso condiviso in uno spazio dei nomi di Inoltro. A differenza della messaggistica del bus di servizio, le [connessioni ibride di inoltro](relay-hybrid-connections-protocol.md) supportano mittenti non autorizzati o anonimi. È possibile abilitare l'accesso anonimo per l'entità di hello quando si crea, come illustrato nella seguente schermata dal portale hello hello:

![][0]

toouse firma di accesso condiviso, è possibile configurare un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) oggetto in uno spazio dei nomi di inoltro costituita dai seguenti hello:

* *KeyName* che identifica la regola hello.
* *PrimaryKey* è una chiave di crittografia utilizzato toosign/convalidare i token di firma di accesso condiviso.
* *SecondaryKey* è una chiave di crittografia utilizzato toosign/convalidare i token di firma di accesso condiviso.
* *Diritti* che rappresenta la raccolta hello di ascolto, invio o gestire le autorizzazioni concesse.

Le regole di autorizzazione configurate a livello di spazio dei nomi hello possono concedere l'accesso tooall connessioni di inoltro in uno spazio dei nomi per i client con i token firmati con una chiave corrispondente hello. Backup too12 tali regole di autorizzazione possono essere configurate in uno spazio dei nomi di inoltro. Per impostazione predefinita, un oggetto [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) con tutti i diritti viene configurato per ogni spazio dei nomi quando ne viene eseguito il provisioning per la prima volta.

tooaccess un'entità, i client di hello richiede un token di firma di accesso condiviso generato usando uno specifico [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). token SAS Hello viene generato con una chiave di crittografia associata alla regola di autorizzazione hello hello è richiesto l'algoritmo HMAC-SHA256 di una stringa di risorsa costituito da risorse hello accesso toowhich URI e una scadenza.

Supporto dell'autenticazione SAS per l'inoltro di Azure è incluso in hello Azure .NET SDK versioni 2.0 e versioni successive. Nella firma di accesso condiviso è incluso il supporto per un oggetto [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Tutte le API che accettano una stringa di connessione come parametro includono il supporto per le stringhe di connessione della firma di accesso condiviso.

## <a name="next-steps"></a>Passaggi successivi
- Per altre informazioni su SAS, vedere [Autenticazione del bus di servizio con firme di accesso condiviso](../service-bus-messaging/service-bus-sas.md).
- Vedere hello [connessioni ibride di inoltro Azure protocollo Guida](relay-hybrid-connections-protocol.md) per informazioni dettagliate sulle funzionalità di connessioni ibride hello.
- Per informazioni corrispondenti sull'autenticazione della messaggistica del bus di servizio, vedere [Autenticazione e autorizzazione del bus di servizio](../service-bus-messaging/service-bus-authentication-and-authorization.md). 

[0]: ./media/relay-authentication-and-authorization/hcanon.png
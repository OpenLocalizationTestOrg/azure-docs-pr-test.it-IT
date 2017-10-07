---
title: aaaSecurity per gli hub di notifica
description: In questo argomento viene illustrata la sicurezza degli hub di notifica di Azure.
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 6506177c-e25c-4af7-8508-a3ddca9dc07c
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f59ad4594c2c0a2e2b22ab0b6d6bad53825a4dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security"></a>Sicurezza
## <a name="overview"></a>Panoramica
In questo argomento viene descritto il modello di sicurezza hello dell'hub di notifica di Azure. Poiché gli hub di notifica sono un'entità del Bus di servizio, implementano hello stesso modello di sicurezza di Service Bus. Per ulteriori informazioni, vedere hello [l'autenticazione del Bus di servizio](https://msdn.microsoft.com/library/azure/dn155925.aspx) argomenti.

## <a name="shared-access-signature-security-sas"></a>Sicurezza della firma di accesso condiviso (SAS)
Gli hub di notifica implementano uno schema di sicurezza a livello di entità denominato firma di accesso condiviso (SAS, Shared Access Signature). Questo schema consente messaggistica entità toodeclare le regole di autorizzazione di too12 nella descrizione che concedono diritti sull'entità.

Ogni regola contiene un nome, un valore di chiave (segreto condiviso) e un insieme di diritti, come illustrato nella sezione hello "Attestazioni di sicurezza". Quando si crea un Hub di notifica, vengono create automaticamente due regole: uno con diritti di ascolto (che hello client app utilizza) e uno con tutti i diritti (che hello app back-end USA).

Quando si gestiscono le registrazioni dalle App client, se le informazioni di hello inviate tramite notifiche non sono riservati (ad esempio aggiornamenti meteorologici), un tooaccess modo comune di un Hub di notifica è toogive valore della chiave hello di hello regola solo l'accesso Listen toohello app client e valore della chiave hello toogive di back-end app toohello hello regola accesso completo.

Non è consigliabile incorporare valore chiave hello in applicazioni client di Windows Store. Un modo tooavoid incorporamento valore chiave hello è toohave hello client app recuperarlo dal back-end app hello all'avvio.

È importante toounderstand che hello chiave con accesso Listen consente a un client app tooregister per qualsiasi tag. Se l'app deve limitare le registrazioni toospecific tag toospecific i client (ad esempio, quando i tag rappresentano gli ID utente), il back-end dell'app deve eseguire registrazioni hello. Per ulteriori informazioni, vedere Gestione della registrazione. Si noti che in questo modo, hello client app non avrà accesso diretto tooNotification hub.

## <a name="security-claims"></a>Attestazioni di sicurezza
Le entità tooother simili, le operazioni di Hub di notifica sono consentite per tre attestazioni di sicurezza: ascolto, invio e gestire.

| Attestazione | Descrizione | Operazioni consentite |
| --- | --- | --- |
| Attesa |Creare o aggiornare, leggere ed eliminare singole registrazioni |Creare o aggiornare una registrazione<br><br>Leggere una registrazione<br><br>Leggere tutte le registrazioni per un handle<br><br>Eliminare una registrazione |
| Invio |Hub di notifica toohello i messaggi di trasmissione |Send message |
| Manage |CRUD negli hub di notifica (incluso l'aggiornamento delle credenziali PNS e le chiavi di sicurezza) e lettura delle registrazioni basata sui tag |Hub di notifica di creazione, aggiornamento, lettura ed eliminazione<br><br>Leggere le registrazioni per tag |

Gli hub di notifica accettano attestazioni concesse dai token di controllo di accesso di Microsoft Azure e dal token di firma generati con chiavi condivise configurate direttamente sull'Hub di notifica hello.


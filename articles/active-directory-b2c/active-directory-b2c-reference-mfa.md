---
title: 'Azure Active Directory B2C: Multi-Factor Authentication | Documentazione Microsoft'
description: Come tooenable multi-Factor Authentication in applicazioni per consumatori protetti da Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 53ef86c4-1586-45dc-9952-dbbd62f68afc
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 29beb1e6ab5d8ab5a65f9c5c068d9e71c60418dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-enable-multi-factor-authentication-in-your-consumer-facing-applications"></a>Azure Active Directory B2C: abilitare Multi-Factor Authentication nelle applicazioni destinate agli utenti
Azure Active Directory (Azure AD) B2C si integra direttamente con [Azure multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) in modo che è possibile aggiungere un secondo livello di esperienze toosign-up e accesso di sicurezza nelle applicazioni per consumatori. Questo è possibile senza scrivere una singola riga di codice. Attualmente è supportata la verifica tramite chiamata telefonica e SMS. Se i criteri di iscrizione e accesso sono già stati creati, è ancora possibile abilitare Multi-Factor Authentication.

> [!NOTE]
> È anche possibile abilitare Multi-Factor Authentication durante la creazione di criteri per l'iscrizione e l'accesso, non solo modificando i criteri esistenti.
> 
> 

Questa funzionalità consente alle applicazioni di gestire scenari come la seguente hello:

* Non sono necessari un'applicazione di multi-Factor Authentication tooaccess, ma necessario tooaccess un altro. Ad esempio, consumer hello possono accedere a un'applicazione di assicurazione automatica con un account locale o di social networking, ma deve verificare il numero di telefono hello prima che l'accesso a un'applicazione hello home assicurazione registrato in hello stessa directory.
* Non sono necessari tooaccess multi-Factor Authentication un'applicazione in generale, ma si richiedono le parti sensibili tooaccess hello in esso contenuti. Consumer hello, ad esempio, per poter accedere tooa applicazione con un account locale o di social networking e verifica il saldo del conto bancario, ma deve verificare il numero di telefono hello prima di tentare un trasferimento tramite rete.

## <a name="modify-your-sign-up-policy-tooenable-multi-factor-authentication"></a>Modificare il tooenable criteri iscrizione multi-Factor Authentication
1. [Seguire questi blade di passaggi toonavigate toohello B2C funzionalità nel portale di Azure hello](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Fare clic su **Criteri di iscrizione**.
3. Fare clic su tooopen i criteri di iscrizione (ad esempio, "B2C_1_SiUp") è.
4. Fare clic su **multi-factor authentication** e attivare hello **stato** troppo**ON**. Fare clic su **OK**.
5. Fare clic su **salvare** nella parte superiore di hello del pannello hello.

È possibile utilizzare funzionalità "Esegui" hello sull'esperienza di hello criteri tooverify hello consumer. Verificare l'esempio hello:

Un account utente viene creato nella directory prima che si verifichi il passaggio di multi-Factor Authentication hello. Durante il passaggio di hello, consumer hello è richiesto tooprovide propria il numero di telefono e verificarlo. Se la verifica ha esito positivo, il numero di telefono hello è collegato toohello account utente per un uso successivo. Anche se il consumer hello Annulla o viene ritirata, che possono essere formulata tooverify un numero di telefono nuovamente durante hello Accedi successivo (con autenticazione a più fattori abilitata).

## <a name="modify-your-sign-in-policy-tooenable-multi-factor-authentication"></a>Modificare il tooenable di criteri di accesso multi-Factor Authentication
1. [Seguire questi blade di passaggi toonavigate toohello B2C funzionalità nel portale di Azure hello](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Fare clic su **Criteri di accesso**.
3. Fare clic su tooopen i criteri di accesso (ad esempio, "B2C_1_SiIn") è. Fare clic su **modifica** nella parte superiore di hello del pannello hello.
4. Fare clic su **multi-factor authentication** e attivare hello **stato** troppo**ON**. Fare clic su **OK**.
5. Fare clic su **salvare** nella parte superiore di hello del pannello hello.

È possibile utilizzare funzionalità "Esegui" hello sull'esperienza di hello criteri tooverify hello consumer. Verificare l'esempio hello:

Quando il consumer hello accede (utilizzando un account locale o di social networking), se è collegato un numero di telefono verificato account consumer toohello che viene richiesto tooverify è. Se non è collegato alcun numero di telefono, consumer hello viene chiesto tooprovide uno e la verifica. La verifica ha esito positivo, in è collegato il numero di telefono hello toohello account utente per un uso successivo.

## <a name="multi-factor-authentication-on-other-policies"></a>Multi-Factor Authentication per altri criteri
Come descritto per l'iscrizione & Accedi criteri sopra indicati, è anche possibile tooenable multi-factor authentication per l'abbonamento o reimpostare i criteri password e i criteri di accesso. Questa opzione sarà presto disponibile tra i criteri di modifica del profilo.


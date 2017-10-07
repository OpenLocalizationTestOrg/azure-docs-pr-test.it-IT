---
title: aaaAuthentication e l'autorizzazione in App mobili di Azure | Documenti Microsoft
description: "Riferimento concettuale e panoramica di hello autenticazione / autorizzazione funzionalità per App mobili di Azure"
services: app-service\mobile
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: a46dbf70-867d-48f6-8885-7f5207ad102e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5255734481ada11afb65982aebe45c2a349402fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-mobile-apps"></a>Autenticazione e autorizzazione in App per dispositivi mobili di Azure
## <a name="what-is-app-service-authentication--authorization"></a>Informazioni sull’autenticazione / autorizzazione di servizio app
> [!NOTE]
> In questo argomento sarà migrato tooa consolidato [l'autenticazione del servizio App / autorizzazione](../app-service/app-service-authentication-overview.md) argomento riguardante Web, dispositivi mobili e App per le API.
> 
> 

L'autenticazione del servizio App / autorizzazione è una funzionalità che consente l'applicazione toolog gli utenti senza modifiche del codice necessario nel back-end app hello. Fornisce un modo semplice di tooprotect dell'applicazione e il lavoro con i dati per ogni utente.

Servizio App Usa identità federate, in cui un parti 3rd **provider di identità** ("IDP") archivia gli account autentica gli utenti, e un'applicazione hello utilizza questa identità anziché il proprio. Servizio App supporta cinque provider di identità predefinito hello: *Azure Active Directory*, *Facebook*, *Google*, *Account Microsoft*, e *Twitter*. È anche possibile espandere il supporto per le app integrando un altro provider di identità o una soluzione di identità personalizzata.

L’app può utilizzare un numero qualsiasi di questi provider di identità, pertanto è possibile offrire agli utenti finali diverse opzioni di modalità di accesso.

Se si desidera tooget adesso, vedere una delle seguenti esercitazioni hello:

* [Aggiungere app per iOS tooyour autenticazione]
* [Aggiungere app xamarin tooyour di autenticazione]
* [Aggiungere app xamarin tooyour di autenticazione]
* [Aggiungere app di Windows Authentication tooyour]

## <a name="how-authentication-works"></a>Funzionamento dell'autenticazione
In ordine tooauthenticate utilizzando uno dei provider di identità hello, è necessario innanzitutto tooconfigure hello identity provider tooknow sull'applicazione. provider di identità Hello quindi fornirà gli ID e i segreti di fornire applicazioni toohello indietro. Questo completa la relazione di trust hello e tooit identità fornite toovalidate di servizio App.

Questi passaggi vengono descritti in dettaglio in hello seguenti argomenti:

* [Come tooconfigure l'accesso di Azure Active Directory toouse app]
* [Come tooconfigure l'account di accesso Facebook toouse app]
* [Come tooconfigure l'account di accesso Google toouse app]
* [Come tooconfigure l'account di accesso di app toouse Account Microsoft]
* [Come tooconfigure l'account di accesso Twitter toouse app]

Dopo aver configurato tutti gli elementi nel back-end hello, è possibile modificare il toolog client in. Di seguito, sono disponibili due approcci:

* Usando una singola riga di codice, consentire hello App per dispositivi mobili client SDK accedere gli utenti.
* Sfruttare un SDK pubblicato da un'identità tooestablish provider di identità specificata e quindi ottenere accesso tooApp servizio.

> [!TIP]
> La maggior parte delle applicazioni devono utilizzare un tooget SDK provider un'esperienza di accesso più nativo-sensazione e supporto dell'aggiornamento tooleverage e altri vantaggi specifici del provider.
> 
> 

### <a name="how-authentication-without-a-provider-sdk-works"></a>Funzionamento dell'autenticazione senza un SDK del provider
Se non si desidera tooset di un provider SDK, è possibile consentire l'accesso hello tooperform di App per dispositivi mobili per l'utente. il client di App per dispositivi mobili Hello SDK verrà aperto un provider di toohello visualizzazione web l'accesso hello scelta e completo. Occasionalmente su blog e forum che verrà visualizzato questo cui tooas hello "flusso server" o "indirizzate al server di flusso" perché il server di hello gestisce accesso hello e client hello SDK non riceve mai il token provider hello.

codice Hello necessario toostart che questo flusso è coperto nell'esercitazione di autenticazione hello per ogni piattaforma. Alla fine hello flusso hello, hello client SDK dispone di un token di servizio App e token hello viene automaticamente collegato tooall back-end toohello di richieste.

### <a name="how-authentication-with-a-provider-sdk-works"></a>Funzionamento dell'autenticazione con un SDK del provider
Utilizzo di un provider SDK consente hello esperienza log toointeract più rigoroso con piattaforma hello app hello del sistema operativo è in esecuzione in. Inoltre, offre un token del provider e alcune informazioni utente sul client hello, che rende molto più semplice grafico tooconsume API e personalizzare l'esperienza utente hello. Occasionalmente su blog e forum verrà visualizzato questo hello tooas denominata "flusso client" o "diretta dal client flusso" dal codice client hello è gestione degli account di accesso hello e token di accesso tooa provider dispone di codice hello del client.

Dopo aver ottenuto un token del provider, è necessario che toobe inviati tooApp servizio per la convalida. Alla fine hello flusso hello, hello client SDK dispone di un token di servizio App e token hello viene automaticamente collegato tooall back-end toohello di richieste. sviluppatore Hello può inoltre includere un token di riferimento toohello provider, se richiesto.

## <a name="how-authorization-works"></a>Funzionamento dell’autorizzazione
L'autenticazione del servizio App / autorizzazione espone diverse opzioni per **tootake azione quando la richiesta non è autenticata**. Prima che il codice riceva una determinata richiesta, possono avere toosee controllo servizio App se hello richiesta è autenticata e in caso contrario, Rifiuta e tentare di toohave hello accesso degli utenti prima di riprovare.

Un'opzione è tooone hello del provider di identità di reindirizzare le richieste autenticate toohave. In un web browser, questa operazione richiederebbe effettivamente nuova pagina tooa utente hello. Tuttavia, in questo modo il client per dispositivi mobili non può essere reindirizzato e le risposte non autenticate riceveranno una risposta HTTP *401 - Non autorizzato*. Detto questo, il client effettua la richiesta prima hello deve essere sempre toohello endpoint di accesso e apportare quindi chiama tooany altre API. Se si tenta un'altra API toocall prima di accedere, il client riceverà un errore.

Se si desidera più granulare toohave controllare su quali endpoint richiede l'autenticazione, è anche possibile selezionare "Nessuna azione (Consenti richiesta)" per le richieste non autenticate. In questo caso, tutte le decisioni di autenticazione vengono posticipate tooyour codice dell'applicazione. Ciò consente inoltre agli utenti di toospecific tooallow accesso in base alle regole di autorizzazione personalizzato.

## <a name="documentation"></a>Documentazione
Hello seguenti esercitazioni Mostra come tooadd autenticazione tooyour client mobili tramite il servizio App:

* [Aggiungere app per iOS tooyour autenticazione]
* [Aggiungere app xamarin tooyour di autenticazione]
* [Aggiungere app xamarin tooyour di autenticazione]
* [Aggiungere app di Windows Authentication tooyour]

Hello seguenti esercitazioni Mostra come provider di autenticazione diversi tooleverage tooconfigure servizio App:

* [Come tooconfigure l'accesso di Azure Active Directory toouse app]
* [Come tooconfigure l'account di accesso Facebook toouse app]
* [Come tooconfigure l'account di accesso Google toouse app]
* [Come tooconfigure l'account di accesso di app toouse Account Microsoft]
* [Come tooconfigure l'account di accesso Twitter toouse app]

Se si desidera toouse un sistema di identità diverso da hello quelle fornite in questo caso, è anche possibile sfruttare hello [anteprima supporto dell'autenticazione personalizzata hello .NET Server SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth).

[Aggiungere app per iOS tooyour autenticazione]: app-service-mobile-ios-get-started-users.md
[Aggiungere app xamarin tooyour di autenticazione]: app-service-mobile-xamarin-ios-get-started-users.md
[Aggiungere app xamarin tooyour di autenticazione]: app-service-mobile-xamarin-android-get-started-users.md
[Aggiungere app di Windows Authentication tooyour]: app-service-mobile-windows-store-dotnet-get-started-users.md

[Come tooconfigure l'accesso di Azure Active Directory toouse app]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Come tooconfigure l'account di accesso Facebook toouse app]: app-service-mobile-how-to-configure-facebook-authentication.md
[Come tooconfigure l'account di accesso Google toouse app]: app-service-mobile-how-to-configure-google-authentication.md
[Come tooconfigure l'account di accesso di app toouse Account Microsoft]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Come tooconfigure l'account di accesso Twitter toouse app]: app-service-mobile-how-to-configure-twitter-authentication.md
